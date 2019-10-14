# Representational State Transfer (REST)

Representational State Transfer is an API design pattern for accessing objects in a client-server system.

## Resources
- [What is REST?](http://www.restapitutorial.com/lessons/whatisrest.html)

## Ideology

Resource-based (instead of action-based)
  - Talking about nouns instead of verbs
  - Identified by unique resource identifiers (URI's)

Representations
e.g. 
  - Resource: Person
  - Service: Contact information
  - Representation:
    § Name, address, phone in JSON/XML

Six constraints
  1. Uniform interface
  2. Statelessness
  3. Client-server
  4. Cacheable
  5. Layered system
  6. Code on demand

Uniform Interface: defines an interface between client and server to decouple architecture

Stateless: server has no client state, requests have enough content to process messages (state, if any, is in client)

Client-server: decoupling of client and server, separation of concerns, communicating with uniform interface

Cacheable: responses (representations) could be cacheable

Layered System: client can't assume direct connection to server, only focus on API

Code On Demand: server can transfer logic to client (like JavaScript or java applets)

Violating any (but code on demand) makes it not RESTful

Compliance allows…
  - Scalability
  - Simplicity
  - Modifiability
  - Visibility
  - Portability
  - Reliability

Identification of resources is a universal standard (URI), can link, bookmark, and act as entry point.
