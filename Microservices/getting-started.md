# Getting Started
See https://app.pluralsight.com/library/courses/getting-started-microservices/table-of-contents

Note that this course is mostly a re-cap of [the other beginner one](https://github.com/akiryk/tutorials-learning-lessons/blob/master/Microservices/intro.md). However, it has some useful additional information. 

## Example Microservice Patterns
- Early stage migration. Leave monolith intact but start building some -- even just one -- microservice. The monotlith can shrink over time, if microservices are beneficial; or, you can keep it and just use a few services.
- Hub and Spoke model: If above approach works, the monolith may shrink until it is just an API gateway that defers to microservices. The Gateway can also handle cross-cutting concerns, such as authorization and authentication.
- Event Driven architecture:  Services communicate via a message bus, that is services don't communicate directly with one another but through a "bus".

## Challenges
First, microservices are hard.

Slow performance. Communication isn't as fast as between modules in a monolith. When in a monolith, services are all in the same server; they are "in-process". In contrast, microservices will need to hit various networks. For this reason, the design of MS APIs needs to take network performance very seriously.

Networks fail. We need to be prepared for unreliability. For simple cases, this can be handled by trying again when something fails. But we 
need a way _to handle stateful logic across systems_. For example, say we have a payment service and a content-screening service. If payment succeeds but content screening does not, we need to unwind the payment. We need some kind of stateful logic. 

Security is more complex.

Analyzing telemetry data is hard since it comes from multiple places. There are multiple sources of data from different services and some operations span services. You can't treat metrics and logging as an afterthought. 

Need for robust automation with build tools for testing, deployment, monitoring, and scaling is critical. You can't do this stuff manually and there are so many tasks that can be automated in microservices architectures.  

Oversight/Governance is essenstial. You need a full time architect or team of architects to provide guidance managing the inter-related services and governance. For example, you need to balance autonomy with consistency. 

Beware of pseudo microservices, in which the services are coupled in some way, e.g. by using a shared database. This gets you the complexity of microservices with the inflexibility of a monolith. The worst of both worlds. 

## Synchronous Architectures

-> When we talk about synchronous architectures, we're talking about RPCs.

### Remote Procedure Call (RPC)
RPC is the network equivalent of calling a function to help run your code. This is another way to design an API that is distinct from REST. It's a way for a server to run a procedure as thought it were on the local machine but is in fact out on the network. SOAP is RPC.  
- RPCs have arguments and return values
- they are expected to be executed immediately
- the call is synchronous; the client that uses the RPC needs to wait for a response before continuing
### Service Discovery
The network address of a given server is located dynamically. Using service discovery is a way to ensure services remain truly independent. 
Ways to do this include:
- DNS One option is simply to use DNS and this is frequently possible with cloud services. 
- Apache Zookeeper, which supports Hadoop and Kafka
- Others
- if all your services are on one provider like GCP, you're best bet is probably to use the GCP service-discovery tools

### Stateless RPCs
There are two types of stateless RPCs:

1. Functional procedures (as in functional programs) are relatively simple. An example might be generating a PDF based on some data passed in as arguments. 
2. Conduits are a form of facade. This might be a service that helps you communicate with a 3rd party services. 

### Stateful RPCs
These are more complex but more useful. It's important to determine _where_ state lives. Rule of thumb is to have a particular slice of state owned by a single service to reduce risk of coupling.  

Idempotence: property of a system where it doesn't change if you perform the same operation multiple times. E.g. if you send a message and there's a failure to notify sender of success, what happens? The sender re-sends the same message. But the recipient microservice has already recieved it. It should recognize this is the same thing and not treat it as a second or third message. This is idempotence and is important in microservices. 

This has three benefits:
1. state should be unchanged when there's duplicate data
2. simplifies implementation for clients because they don't have to worry about tracking state
3. reduces coupling because it ensures business logic only happens in one place rather than several. That is, in our message example, rather than tracking which messages require notifications in both our client (sender) _and_ our notification service, we only do it in the notification service. 

**Network Partition** and **failure modes**: a division of a network that into relatively independent parts such that one doesn't necessarily know about what happens in the other. This is important for microservices that have to handle failures. Example: your phone communications with a chat service. The chat service communicates with a notification service. In this case, there's a network partition between your phone and the services. Your phone doesn't know if there was a problem between the chat service and the notification service, it just knows that it sent or received a message. 

You need to choose a failure mode, meaning which service's state is more important. One service's state may not get changed as a result of a transaction so as not to leave the overall system in an inappropriate state. 

### Performance and availability in synchronous architectures
If you have a service, `A`, with an availability SLA of 99% that is available 99.9% of the time, you're golden. If `A` depends on services `B` and `C`, however, and these each have SLAs of 99.5%, you need to take that into account. 99.9 * 99.5 * 99.5 = 98.9% — below our SLA! This architecture won't work. 

### Availability vs Speed
Improving one may adversely affect the other. Why? because if you want to be more available, you'll need to set up to enable more re-tries in the event of a failure, which will add to latency. If you want greater speed, you'll have to sacrifice some availability when services don't respond. 

One way to overcome these challenges is with asynchronous, messaging-based communications. 

# Status
I made it here: https://app.pluralsight.com/course-player?clipId=8f2116a0-f756-4926-baac-25f87549e87f
