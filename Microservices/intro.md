# Miroservices: The Big Picture

[Pluralsite course](https://app.pluralsight.com/course-player?clipId=a991691d-f991-468d-839a-67d858d2a4fc)

## What is a Microservice?
Small autonomous services that work together. The point is to enable small teams to work faster by focusing on smaller things.

"Micro"

No fixed definition of how small is "micro", but the idea is basically: 

- it does one thing
- bounded context, that is, a single business capability that can be deployed independently
- for a large business, we need to identify our sub-domains and build each as a micro service

Example: an e-commerce business could be divided into sub-domains such as user-management, inventory, catelog, etc.

"Service"

- independently deployable compnonent
- interoperability (should work across different OS's, languages, platforms, etc)
- message based communication
- sounds like Service Oriented Architecture (SOA, a set of guidelines having services communicate with one another; SOAP is a set of rules)

## Microservice Elements

### Monolith
Pros:
- simple to build it
- simple to develop with it
- simple to deploy
- simple to scale (just create additional instances behind a load balancer)
- simple to test
- easy for developers to move around codebase since it's all the same

Cons
- hard for teams to work independently
- harder to take advantages of new technologies
- scaling hard -- if you need to scale one part for one specific reason, the entire monolith has to scale 
- huge database, which could impact performance

### Microservices
We can use domain-driven design to create services corresponding to our sub-domains. 

Domain: e-commerce

Subdomains:
- User (account, address, auth)
- Order (invoice, cart)
- Product (specs, media, pricing)

**Data-store**

Sharing databases is an antipattern in microservices. Each subdomain will have its own database so it can be independent of the others. Using a database per service
ensures the services are **loosely coupled**.

-> But how then do you synchronize data?

Say a user changes their email address. You update the User subdomain's db, but you can't update the Order subdomain's db because this is antithetical
to microservices approach. It would tightly couple the two and could hurt performance.

Solution is _eventual consistency_ with events. When a db is updated, it publishes an event that other services consume. This means a given item may 
have different data on different subdomains. **Kafka** is a tool for publishing these events. 

**User Interface**

How to have consistent UIs that display data from different microservices? A UI may need to call 2 or 3 or more microservices. 
We can solve this with composition, **UI Composition**. There are two ways to do this:

- Service side composition: compose HTML fragments composed by different services.
- Client side composition: build a skeleton that aggregates microservice components.
