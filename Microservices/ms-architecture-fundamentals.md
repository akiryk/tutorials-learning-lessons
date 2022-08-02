# Microservices Architecture Fundamentals

[See PluralSite course here](https://app.pluralsight.com/library/courses/microservices-fundamentals/table-of-contents).

## Introducing Microservices
Review the pros and cons of microservices approach vs monolith approach.

### Challenges with monoliths in a nutshell:

All code is in a single codebase with a single database and a single programming language
- simple
- easy to update

but...
- hard to scale
- accumulation of tech debt
- modules tend to become entangled, lots of coupling
- deployments are harder, take longer
- hard to scale horizontally (more servers); you need to scale vertically (get a better server)
- wedded to legacy technology; hard to transition because of so many dependencies

### Challenges with microservices
In a nutshell, microservices introduce complexity which can impact developer productivity. You need a way to monitor all of your services; you need a way to automate deploys, since there will be so many; and you need to watch out for overly chatty communications among all of your microservices.

## Architecting Microservices
Recommendation: don't start with a microservices-approach, since it's often difficult to get the boundaries right and to know which services make sense. Plus, the approach isn't really suited to small projects (that is, new projects). On the other hand, once you have a monolith underway, there are different methods to transition to microservices once you know more about your domain.
- augment: add new services as they are needed
- decompose: extract services one at a time as it makes sense

**Rule**: each microservice must own its own data; don't use a shared data store. 

**Consequence**: you can no longer use joins or do other db processes on multiple services at once, you'll have to make separate calls. You need a way to cope with the temporary inconsistency, which occurs under these conditions -- we aim for what is called "eventual consistency". We can minimize the issues by having good service boundaries; caching; identify natural "seams" in the dababase.
<img width="763" alt="image" src="https://user-images.githubusercontent.com/2437758/180239153-843f8cfb-1f8c-4bf6-9191-c1a828667ba1.png">

### Microservices are independently deployable
The main consequence of this rule is that you must never make a breaking change to your API. In fact, it's often not called an "API" but a "contract". How can you do this?

- make changes additive, say with new endpoints; new properties on DTOs
- use versioning (although you must continue to support earlier versions)
- use automated tests that ensure all versions/variations work

### Identifying Microservice Boundaries
Using domain driven design is often very helpful, as is using your existing monolith and database structure to help you identify seams. Some indications that you may not have the right boundaries are:
- clusters of services that all need to frequently communicate
- circular dependencies

### Example microservices boundaries
In the example e-commerce site, we have separate services for Catalog, Basket, Ordering, Identity, and others. Catalog needs to support flexible queries and lots of data so it uses SQL Server. Basket is short lived data, so it uses Redis. 

## Building Microservices

https://github.com/dotnet-architecture/eShopOnContainers
