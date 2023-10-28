# API Gateway

\= server-side architectural component in a software system that acts as an intermediary between clients (such as web browsers, mobile apps, or other services) and backend services, microservices, or APIs.

### **Purpose**

* **Routing**
  * receives requests from clients and routes them to the appropriate microservice. This enables clients to access the various microservices through a single entry point, simplifying the overall system design.
* **Authentication and Authorisation**
* **Rate limiting and throttling**
  * can help prevent denial of service attacks and other types of malicious behaviour.
* **Caching**
  * can cache responses from the microservices, reducing the number of requests that need to be forwarded to the microservices and improving the overall performance of the system.
* **Monitoring**
  * can collect metrics and other data about requests and responses, providing valuable insights into the performance and behaviour of the microservices.
* **Logging**
* **Transformation**
  * can be used to transform the data received from the microservices into a format that is more convenient for the clients to use. This can include tasks such as converting between different data formats, such as XML and JSON, or aggregating data from multiple microservices into a single response.
* **Request and response validation**
  * can be used to validate the requests and responses from the microservices to ensure that they conform to the expected format and structure.
* **Service discovery**
  * can be used to discover the available microservices and their locations, enabling the clients to access them without knowing their specific addresses.
* **Circuit breaker**
  * can help to prevent a single failed microservice from bringing down the entire system. The circuit breaker can monitor the health of the microservices and automatically fail over to a backup service if necessary.
* **API Versioning**
  * can manage multiple versions of an API, allowing developers to introduce new features or make changes to existing ones without disrupting existing clients.

### Gateway vs Load Balancer

API gateway is focused on **routing** requests to the appropriate microservice.

Load balancer is focused on **distributing** requests evenly across a group of backend servers.
