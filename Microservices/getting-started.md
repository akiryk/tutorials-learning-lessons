# Getting Started
See https://app.pluralsight.com/library/courses/getting-started-microservices/table-of-contents

Note that this course is mostly a re-cap of [the other beginner one](https://github.com/akiryk/tutorials-learning-lessons/blob/master/Microservices/intro.md). However, it has some useful additional information. 

## Example Microservice Patterns
- Early stage migration. Leave monolith intact but start building some -- even just one -- microservice. The monotlith can shrink over time, if microservices are beneficial; or, you can keep it and just use a few services.
- Hub and Spoke model: If above approach works, the monolith may shrink until it is just an API gateway that defers to microservices. The Gateway can also handle cross-cutting concerns, such as authorization and authentication.
- Event Driven architecture:  Services communicate via a message bus, that is services don't communicate directly with one another but through a "bus".

## Benefits
- easier to maintain boundaries between modules. In a monolith, blurring tends to occur and coupling between concerns that should be separate.
- easier to test and maintain because smaller. 
- resilience: the whole system won't be "down" because only one part may be down. 
- ability to isolate third party APIs that might go down behind a single microservice

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

## Asynchronous Communication via Message Bus
These are often called event-driven or message-oriented architectures. Use a message bus to communicate between microservices, including how to coordinate distributed transactions and handle failures.

A message bus handles getting messages from **senders** to **consumers**. Compare this to a remote procedure call. An RPC is **2-way** communication. Client sends off a request and receives by a response. Message-bus uses **1-way** communication in contrast. It's async and therefore lets uses do their work faster. 

Example: click a like button. With RPC, you'd have to wait for several microservices to do their job of notifying, updating preferences, modifying advertising algorithms, etc -- only after all that had done would the like be saved. With bus, all you need to do is get the message delivered to the bus. The bus can then queue up all the different services that need updating and it can handle those things async.

Benefits:

- we can add microservices without changing existing services, which don't even need to know about the new services since it's handled by the bus
- isolate slow services
- absorb spikes in load
- faster, no waiting for RPCs to complete

### Anatomy of a message
- include a payload with the key business info
- include headers with metadata, timestamp, etc
- messages must be small to avoid harming throughput and avoid risk of failure. Often size is limited by the implementation. 
- if messages need to be big, we often put the large part into blog storage and simply refer to that in the message

**Topics**: when publishing a message to a bus, the message is published under a "topic." Subscribers subscribe to one or many topics. Topics are things like "post-liked", "message-sent", "product-rated". 

**Consumer** The consumer subscribes to and listens to topics. They can subscribe to 1 or many and can configure how those messages get delivered via queues. You could have a different queue for each topic or one queue for messages from all topics. This means the same message published to a topic may be routed to one consumer one way, via a combined queue, and another may be delivered to a single queue. 
Once consumer reads the message, it removes the message from the queue. 

### Distributed transactions
This is a sequence of coordinated state changes over distributed services. For example, if I post a photo to some app, I need to upload the photo; screen the photo; notify my friends; update my advertising profile; possibly add some fee to my account; etc. 

Problems and concerns:
- Message routing: best if we have a single service for coordinating how a transaction flows from one service to the next because this gives us a single point of truth representing the entire flow.
- transaction state: if transaction is distrubuted, it's hard to know at any given time precisely what is the state. Ideally, you also have a single service for keeping track of this state. 
- Failure compensation: if a given service fails, with chained routing the whole transaction becomes stuck. 

Potential solutions:

**Saga pattern**

This is pattern centralizes the state of the distributed system into one place, a database in which records are kept for the current state of each transaction. As indicated in this image, the database keeps a record for each transaction, and each transaction has a current state. This enables:
- user-initiated cancelation
- rollback in the event of a failure. That is, if the Advertising step fails, it uses failure compensation to reset to the initial state and this then goes back to photo screening and timeline which can do the same.
- change the sequence by redefining the saga to have a different order, say, screen photos first.
<img width="2619" alt="image" src="https://user-images.githubusercontent.com/2437758/175344427-07d5a86e-1c62-4fe2-af10-0b2fd5332f08.png">

**Routing slip pattern**

A manufacturing routing slip is a document that says what steps need to be performed at what stations on a factory floor. Item A needs to go to stations 1, 2, and 3; at station 1, assemble the bike frame; at station 2, add a cushy seat; etc. 

- change sequence by changing order on "routing slip"
- easy to conditionally do certain steps -- if a transaction doesn't include a photo, don't include screening on the slip
- no centralized state, which can improve performance.
- if failure occurs, it follows the steps backwards

TLDR is that these patterns each have benefits and are best for specific use-cases. E.g. Saga is best for when you need to centralize state, say, for reporting on transaction in progress. If you have conditional routing, routing slip is probably better. 

<img width="2617" alt="image" src="https://user-images.githubusercontent.com/2437758/175347256-15b0b334-1477-4ddd-8ec0-def0397f7100.png">

### Summary of async architectures
Event driven architectures tend to exhibit "eventual consistency" behavior, meaning at any given time there may be a temporary inconsistency. For example, you liked a post but notification has not been set out yet because the message is waiting in a queue. This is necessary for service independence, but can be uncomfortable for people expecting ACID behaviors (Atomicity, Consistency, Isolation, Durability). 

## Microservice Quality
In order to design a ms, we need a clear understanding of its API and its dependencies. This defines the service's boundaries. We have _inputs_ and _outputs_. The inputs are the things that come in from the API (http calls, remote procedure calls, message bus consumers). The outputs are the things that the service is dependent on such as data stores, third party APIs, other services, or  message bus publishing.  

If we have clear boundaries between inputs and outputs, we can design good test coverage using the classic pyramid approach (unit tests on the bottom; integration and manual tests at top).

## Continuous Delivery
In order to continue working with other services and avoid coupling, we need a strategy for modifying and adapting our service

- API versioning: enable others to continue doing what they've been doing but you can move from v1 to v2.
- Feature Toggles: enable functionality based on a condition

## Team Culture
There are certain approaches that are so important to developing microservices that you really want everyone on board:

- automation (in testing, build, monitoring, benchmarking). 
- invest in tooling
- reserve capacity for building and maintaining tooling and automation
- in a word, integration of operations with the dev team: **devops**
- a high performing devops team builds observable software and uses their tools to monitor that everything does as it should

### time allocation
the well-oiled microservices team plans for these important aspects of work and allocates time accordingly:

- building features
- planning
- monitoring
- proactive maintenance
- unplanned work (learning and experimenting)

<img width="864" alt="image" src="https://user-images.githubusercontent.com/2437758/176180364-780a9922-7853-4824-9276-647a02059fb5.png">

- unplanned work (learning and experimenting)
