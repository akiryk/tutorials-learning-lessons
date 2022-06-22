# Web Services

See also [REST APIs](https://github.com/akiryk/tutorials-learning-lessons/blob/master/REST_APIs.md)

## Overview

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

## REST

**HATEOAS** Hypermedia as the engine of application state
This is an agreement RESTful APIs should adhere to: Whenever a response is sent, it should include links associated to other resources. The response tells you what you can do and how to do it.

**Postman** a useful tool for testing RESTful apis
**Swagger** a tool for creating documentation of the API

## SOAP

Simple Object Access Protocol
Some discussion over the future of SOAP, since REST is so much lighter-weight and flexible for many uses. However, there are uses where SOAP is still prevalent:

- financial services/payment gateways
- identity management
- telecommunication services

Paypal uses SOAP, for example.

[SoapUI](https://www.soapui.org/) is a recommended tool for testing SOAP services.

To make a SOAP endpoint in Java, use the `src.main.java.com.keysoft.soap` package and import `javax.jws.WebService` and `javax.jws.WebMethod`. Then you can annotate the class with a `@WebService` decorator above your Java class.

### Interoperability

A fundamental characteristic of Web Services is that they are interoperable. This means that a client can invoke a Web Service regardless of the client's hardware or software. For example, an interoperable Web Service running on WebLogic Server on a Sun Microsystems computer running Solaris can be invoked from a Microsoft .NET Web Service client written in Visual Basic.

## ACID Compliance

A set of principles that ensure database transactions are processed reliably:

- Atomicity
- Consistency
- Isolation
- Durability

These elements fall on a sliding scale from strong to weak.

**Atomicity** operations must all succeed together or all fail together. It is unacceptable for the bank debit to occur if the transfer fails.

**Consistency** In general, consistency refers to the ability of a system to ensure that it complies (without fail) to a predefined set of rules, which can vary based on context.

**Isolation** each transaction must be serializable; it can occur in its proper order without dependent transactions occurring in tandem.

**Durability** Durability requires that every successful transaction’s data operations are indelible and cannot be lost—even in the event of a complete system shutdown
