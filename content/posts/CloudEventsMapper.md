---
title: CloudEvents Mapper for Ditto
date: 2022-06-02T14:03:52+05:30
draft: false
---



<p><img src="/GSoC1.png" alt="GSoCLogo" class="center" width="400px"></p>


*This year, the Eclipse Foundation participated in Google Summer of Code as an organisation. Amongst the various project ideas for the year was the idea for a CloudEvents mapper for Eclipse Ditto: an IoT project which implements the software pattern "Digital Twins"  persists the digital state of real life "things"(Electric Car,sensors etc).*

*Under the guidance of the project mentor [Jens Reimann](https://github.com/ctron "Jens Reimann") , I was able to write a proposal for the project and get a chance to work on this*

*I am writing this blog as a way to document the initial goals for the project, gain feedback from the community as well as see how this project evolves.*


---

## CloudEvents

[CloudEvents](https://cloudevents.io/ "CloudEvents") is a specification for describing event data in a common way, which can be mapped to multiple event driven technologies. This facilitates developers as developers need to constantly relearn how to consume events depending on the payload. Example: a payload like this:

```
{ 
  "action": "new-item",  
   "itemID": 93
}
```


would look like

 
 
 ```
 {  
    "specversion" : "1.0",
    "type" : "com.newItem.myItem",
    "source" : "http://myItem.com/example",
    "subject" : "123",
    "id" : "3242-121d",
    "time" : "2018-04-05T17:31:00Z",
    "comexampleextension1" : "value",
    "comexampleothervalue" : 5,
    "data" : {
      “action”: “new-item”,
      “itemID”:93
    }
}
```


## Ditto Protocol


[Ditto Protocol](https://www.eclipse.org/ditto/protocol-overview.html#communication-pattern "Ditto Protocol") defines a JSON based text protocol for communicating with digital twins and the actual physical devices they mirror.

It defines several commands both the actual device and the digital twin are able to understand.

Since every device sends payload in different format, it needs to be converted into a format understood by ditto.


## Proposed Steps


1. To begin, we need to validate incoming headers and payload to check whether they comply with the CloudEvents specifications. [See this](https://github.com/cloudevents/spec/blob/v1.0.2/cloudevents/spec.md "CloudEvents Specs") to check the required attributes for CloudEvents. 

1. We then need to specify a mapping specification to transform the incoming payload to ditto protocol. This can be done through POJO classes or existing ditto classes allowing us to reuse the code.

1. Implement Normalization of payload during the outbound process in a way it makes sense. This will be done as part of the outbound mapper.

1. Creating relevant tests and documentation.






<br>



*Feedback is appreciated. Write in to [pranshu.grover18@gmail.com](pranshu.grover18@gmail.com)*