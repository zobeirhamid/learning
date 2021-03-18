# Microservices: Overview

## Article 1

<a href="https://www.twilio.com/blog/building-javascript-microservices-node-js">Article</a>

First, you create two seperate servers which listens on different port. They are decoupled, so changes in one will not affect the other. They interact with each other through a RESTApi, so they need to know each others address.

### Advantages

- Changes in one codebase will not affect the other
- Scalable

### Problems

- There need to be some kind of protocol between the interaction of the services.
- They need to know the address of the other service

## Article 2

<a href="https://www.twilio.com/blog/eureka-zuul-service-discovery-dynamic-routing-javascript-microservices-node-js">Article</a>

Here, we will solve the issue of knowing the address of the other service. The application will now use Netflix Eureka to register services, this will allow for multiple instances of the same service, which helps if there is a lot of traffic coming in. Netflix Zuul is also added to have another RESTApi which forwards Requests to the Microservices RESTApi. With that it is possible to use the multiple instances of microservices, and not knowing the exact address of the service.

### Advantages

- Multiple instances of one microservice
- Exact address of the microservice is not needed

### Problems

- Multiple instances of one microservice use isolated data sources which leads to inconsistency

## Article 3

<a href="https://www.twilio.com/blog/scale-node-js-javascript-microservices-shared-mongodb-atlas">Article</a>

This article focuses on the problems when using multiple instances of one microservice. If for example, one microservice is using the memory for its storage, which means that for each instance of the microservice the storage is isolated. This means if there are two instances of one microservice, they are working with different data. This can be solved by using a persitent layer, like a Database, where each instance pulls its data from that service, which kinda is a microservice in itself.

### Advantages

- Multiple instances of one microservice use data from the same source to create consistency

## Article 4

<a href="https://www.twilio.com/blog/protecting-javascript-microservices-node-js-json-web-tokens-twilio-authy">Article</a>

TODO
