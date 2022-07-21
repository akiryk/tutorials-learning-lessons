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

### Components of a microservice
There doesn't have to be only one process, there can be many. At the least, there's typically your code — say, an API — and a database. But there might be a second process with code to run background tasks or something else. The main point is that each microservice have a clearly defined public interface.
