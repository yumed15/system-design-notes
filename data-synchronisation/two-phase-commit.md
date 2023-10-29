# CQRS

### Motivation

We need a way of implementing a query that retrieves data from multiple services in a microservice architecture.

### Solution

* define a view database, which is a read-only replica that is designed to support that query
* the application keeps the replica up to data by subscribing to Domain events published by the service that own the data.



TBA...
