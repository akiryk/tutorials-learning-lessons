# Application Design / Architecture

These are notes from the [Clean Architecture course](https://app.pluralsight.com/library/courses/clean-architecture-patterns-practices-principles/table-of-contents) on Pluralsite. 

## Introduction
Application Architecture is high level; it's structural — how the software is organized; layers, which are vertical partitians of the system; components, which are horizontal partitions within each layer.
Finally, it has to do with relationships — how everything is wired together.

<img width="1076" alt="image" src="https://user-images.githubusercontent.com/2437758/183748516-ba2c1e9d-7a27-463f-92b8-b35ba162a7be.png">

What is **good** architecture?
It is simple, understandable, flexible, testable, and maintainable. Clean architecture designs for the users of the system, the developers building it, and the ones who maintain it.
We care more about the people who use it than the machines that run it — i.e. avoid premature optimization.

## Domain Centric Architecture 

This is an approach that focuses on what is essential rather than what is a detail.

- use cases are essential
- domain is essential
- persistence (how you store the data) is a detail
- UI is a detail (could be a website, app, etc)

This means that your architecture should be designed with domain at the center wrapped in use-cases. No inner layer should know about any outer layer. 

In order to do this, you need to think through what classes belong in a domain layer versus application layer. 

**Follow up with DDD course** https://app.pluralsight.com/library/courses/fundamentals-domain-driven-design/table-of-contents

Next up is the section about the application layer. 

