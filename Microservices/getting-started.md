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
- if all your services are on one provider like GCP, you're best bet is probably to use their service discovery tools
