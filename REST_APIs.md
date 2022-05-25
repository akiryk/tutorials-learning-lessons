# REST
Representational State Transfer. 
It isn't a specific techology, rather a data architecture and design methology.

## The Six REST Constraints
1. Client-server architecture: proper separation of concerns between the content and its presentation
2. Statelessness: No state can be stored on the server between requests. 
3. Cacheability: All REST responses must be marked as cacheable or non-cacheable.
4. Layered System: client can't know or care whether it's connected directly to the server or to a CDN or something else
5. Code-on-demand
6. Uniform Interface: this includes several things, but an interesting one is that the REST service must provide links to its different resources with every response. 

When a REST service runs on the web over HTTP, we call it a RESTful API. 

## Resource vs Representation
The key abstraction of REST is a **resource**: an image, a document, a service, a collection... any information that can be named. 
The REST service provides us with a _representation_ of the resource, not the resource itself. A copy that can be modified to fit various purposes, formats, etc.

## Verbs
- <code>GET</code>: success gives a 200 response vs 404
- `POST` gives a 201 success response; errors include 401 (unauthorized); 409 (conflict); 404 not found
- `PUT` is used to replace data at an existing resource with the new data
- `PATCH` modifies an existing resource. It can modify the resource without replacing everything
- `DELETE` can only be used with singleton resource. 
- `OPTIONS` includes description of options
- `HEAD` returns just the head of the response

## Tools
There are tools like Postman for sending RESTful requests, but you can easily use VSCode as well with the `REST Client` extension.
Test with an actual site such as this by creating a new document and using `GET` or `OPTIONS` or `HEAD`.
```
GET https://www.lireo.com/wp-json/wp/v2/posts
```

## Designing a REST API
First, understand the business process. What needs to happen?

Next, it's hard. It's about trade-offs. What functionality to expose and how to expose it? 

### Challenges
- name things clearly
- clear directions 
- iteration with versioning and backwards compatibility

### Approaches
- Bolt on: when you need an API after the fact for existing systems. Fast, but ends up with old badly named terms.
- Greenfield: you have complete freedom. API First. Easiest scenario in many ways but can be hard.
- Facade strategy. Take advantage of existing systems but re-work them.

### Tips for modeling your API
1. Don't worry about the tools as long as you can take notes. 
2. Have a consistent process and document clearly. Involve team early
3. It doesn't count unless it's written down. Assumptions, decisions, deferred tasks. 

### Support the business

Example: Ordering a cup of coffee
 
1. Identify Participants: entities who/that will use our API
Determine the boundaries early or you might take into account a too wide range of processes. We'll focus on customer and barista and cashier. We'll leave out the payment systems, inventory systems, etc.  

2. Identify activities.
What needs to happen for success? Customer makes order. Barista takes order. Cashier takes money. Focus on _who_ does _what_

3. Take note of the key steps and map it out. 
