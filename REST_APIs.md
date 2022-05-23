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
- <code>GET</code>
- `POST`
- PUT
- PATCH
