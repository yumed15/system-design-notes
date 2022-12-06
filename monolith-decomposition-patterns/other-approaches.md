# Other Approaches

### Identify and Size Components Pattern/ Scoping Microservices using DDD

* identify, manage, and properly size components.
* Define the **Bounded Context**
  * find **core domain concepts** (e.g. = main business functions) and **internal models** (supporting the concepts)
  * define the **ubiquitous language** for the concept (= agreed language between domain experts and software experts)
  * identify out of context concepts (which don’t fit in the natural language of the core concept)
  * each BC has an explicit **interface** that needs to be defined
  * communication between BC is carried out using **shared communication** (to ensure our bounded context is completely independent fro other BC)

### Gather Common Domain Components Pattern

* consolidate common business domain logic that might be duplicated across the application, reducing the number of potentially duplicate services in the resulting distributed architecture.

### Flatten Components Pattern

* collapse or expand domains, subdomains, and components, thus ensuring that source code files reside only within well-defined components.

### Determine Component Dependencies Pattern

* identify component dependencies, refine those dependencies, and determine the feasibility and overall level of effort for a migration from a monolithic architecture to a distributed one.
