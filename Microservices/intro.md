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

**Distributed Services**

Since there are many services and each can have changing addresses, we need a way for them to find one another. Enter the **Service Registry**, a "phone book" that can look up services by their name.

Services much register on startup and de-register on shut down. Wayfair uses Consul, although only in a limited way. Others include ZooKeeper and Eureka.

CORS is also an issue, since different microservices have different IPs, MSs have to add http headers that enable CORS.

## Summary
- We start with a business that has a domain (e.g. e-commerce) and sub-domains (e.g. user-management; orders; inventory; product)
- We create microservices based on the subdomains. Each is independent, with its own database, team, and versioning.
- We need a **gateway** so the user interface is uniform across all these microservices
- Databases need to exchange information but without directly relying on one another. This is where we use messaging with events and a system like Kafka.
- Microservices need to expose API contracts so other services can use them
- Since remote services can fail, we need **circuit breakers** to protect each call
- The Gateway handles the service registry, authentication, and authorization
- In order to enable monitoring, each microservice needs to expose a health check API
- The system will have greater up-time (Availability) because it still works even if one service is down. However, every server must therefore be prepared for other services to fail and must _degrade gracefully_. Further, some services are critical, such as authentication; these must be highly available.

## DURS
Deploy, Update, Replace, and Scale. Each service must be able to do these things independently.

## Pros and Cons
- There is no standard tech stack for micro services, so you can't go to a single source for help. You need to stitch things together. 
- designing your microservices is very much an art and there aren't firm rules; however, there are patterns and strategies for helping with domain driven design.
- It is challenging to work with a distributed system. Network failure will occur, so services need to handle failure smartly.
- Security: more services, more potential vulnerabilities. You need to take it seriously. 
- Testing: easy if you only test your own service but much harder with integrated tests. Some companies therefore test in production and use "chaos" testing, which deliberately introduces errors. 
- The more services, the more logs and monitoring; this will be hard. 

Pros in green, cons in magenta

<img width="1324" alt="image" src="https://user-images.githubusercontent.com/2437758/174458842-77e9d5cc-33eb-4740-a03a-2b6401892cb7.png">

