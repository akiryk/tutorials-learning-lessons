# Web Services
See also [REST APIs](https://github.com/akiryk/tutorials-learning-lessons/blob/master/REST_APIs.md)

The basic idea is to enable communication between clients and servers.
There are two main kinds of web services: REST and SOAP.

**SOAP**
- sends messages in XML
- is very structured
- can be stateful

**REST**
- uses HTTP protocol

 **Concerns**
 - latency over the network
 - partial network failures (something that is supposed to get returned doesn't get returned)

**Security**
- authentication: validate identity of the client. Think `ic` for `ID`
- authorization: what level of access does a particular user have? What are their privileges/credentials?
