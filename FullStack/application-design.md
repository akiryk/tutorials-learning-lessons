# Application Design / Architecture

These are notes from the [Clean Architecture course](https://app.pluralsight.com/library/courses/clean-architecture-patterns-practices-principles/table-of-contents) on Pluralsite. 

## Introduction
Application Architecture is high level; it's structural — how the software is organized; layers, which are vertical partitians of the system; components, which are horizontal partitions within each layer.
Finally, it has to do with relationships — how everything is wired together.

<img width="1076" alt="image" src="https://user-images.githubusercontent.com/2437758/183748516-ba2c1e9d-7a27-463f-92b8-b35ba162a7be.png">

What is **good** architecture?
It is simple, understandable, flexible, testable, and maintainable. Clean architecture designs for the users of the system, the developers building it, and the ones who maintain it.
We care more about the people who use it than the machines that run it — i.e. avoid premature optimization.
