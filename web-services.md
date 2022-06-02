# Web Services
See also [REST APIs](https://github.com/akiryk/tutorials-learning-lessons/blob/master/REST_APIs.md)

The basic idea is to enable communication between clients and servers.
There are two main kinds of web services: REST and SOAP.

**SOAP**
- sends messages in XML and only XML
- is very structured
- can be stateful

SOAP isn't as good for mobile applications because it sends a lot of extra data over the network.

**REST**
- uses HTTP protocol
- sends payloads in XML, JSON, or other formats with lots of flexibility

 **Concerns**
 - latency over the network
 - partial network failures (something that is supposed to get returned doesn't get returned)

**Security**
- authentication: validate identity of the client. Think `ic` for `ID`
- authorization: what level of access does a particular user have? What are their privileges/credentials?

## RESTful APIs

**HATEOAS** Hypermedia as the engine of application state
 This is an agreement RESTful APIs should adhere to: Whenever a response is sent, it should include links associated to other resources. The response tells you what you can do and how to do it. 
 
**Postman** a useful tool for testing RESTful apis
**Swagger** a tool for creating documentation of the API
