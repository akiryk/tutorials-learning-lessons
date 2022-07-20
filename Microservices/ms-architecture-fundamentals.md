# Microservices Architecture Fundamentals

[See PluralSite course here](https://app.pluralsight.com/library/courses/microservices-fundamentals/table-of-contents).

## Introducing Microservices
Review the pros and cons of microservices approach vs monolith approach.

#### Challenges with monoliths in a nutshell:

Monolith: all code is in a single codebase with a single database and a single programming language
- simple
- easy to update

but...
- hard to scale
- accumulation of tech debt
- modules tend to become entangled, lots of coupling
- deployments are harder, take longer
- hard to scale horizontally (more servers); you need to scale vertically (get a better server)
- wedded to legacy technology; hard to transition because of so many dependencies

#### Challenges with microservices
In a nutshell, microservices introduce complexity which can impact developer productivity. You need a way to monitor all of your services; you need a way to automate deploys, since there will be so many; and you need to watch out for overly chatty communications among all of your microservices.

## Architecting Microservices
