# Domain-Driven Design

**Domain-driven design (DDD)** offers a collection of **patterns** for the modelling the domains of a system. For microservices, the patterns in the area of strategic design describe how a domain can be subdivided.

### Scope services using DDD

* identify, manage, and properly size components.
* define the <mark style="background-color:yellow;">**Bounded Context**</mark>
  * find <mark style="background-color:yellow;">**core domain concepts**</mark> (e.g. = main business functions) and <mark style="background-color:yellow;">**internal models**</mark> (supporting the concepts)
  * define the <mark style="background-color:yellow;">**ubiquitous language**</mark> for the concept (= agreed language between domain experts and software experts)
  * identify out of context concepts (which don’t fit in the natural language of the core concept)
  * each BC has an explicit <mark style="background-color:yellow;">**interface**</mark> that needs to be defined
  * communication between BC is carried out using <mark style="background-color:yellow;">**shared communication**</mark> (to ensure our bounded context is completely independent fro other BC)

### Building blocks of a Model-Driven Design

The purpose of the model-driven design patterns is to present some of the key elements of object modeling and software design from the viewpoint of domain-driven design. The following diagram is a map of the patterns presented and the relationships between them:

<figure><img src="../.gitbook/assets/Screenshot 2022-12-16 at 10.02.40.png" alt=""><figcaption><p>Taken from <a href="https://www.infoq.com/minibooks/domain-driven-design-quickly/">InfoQ's Domain-Driven Design Quickly</a></p></figcaption></figure>

**Entities** = category of objects which seem to have an identity, which remains the same throughout the states of the software. For these objects it is not the attributes which matter, but a thread of continuity and identity, which spans the life of a system and can extend beyond it.

* implementing entities in software means creating **identity** (either an attribute of the object, a combination of attributes, an attribute specially created to preserve and express identity, or even a behavior)

**Value Objects** = object that is used to describe certain aspects of a domain, and which does not have identity; attributes of a domain element;&#x20;

* can be easily created and discarded
* highly recommended that value objects be immutable - created with a constructor, and never modified during their life time. If Value Objects are shareable, they should be immutable.
* when a Value Object is needed by another party, it can be simply passed by value, or a copy of it can be created and given.

**Services** = object that does not have an internal state, and its purpose is to simply provide functionality for the domain.

* can group related functionality which serves the Entities and the Value Objects.
* act as interfaces which provide operations
* becomes a point of connection for many objects
* should not replace the operation which normally belongs on domain objects
* has 3 characteristics:
  * The operation performed by the Service refers to a domain concept which does not naturally belong to an Entity or Value Object
  * The operation performed refers to other objects in the domain.
  * The operation is stateless.

**Modules** = component of a model, used as a method of organizing related concepts and tasks in order to reduce complexity

* recommended to group highly related classes into modules to provide maximum cohesion possible
* way to increase cohesion and decrease coupling
  * communicational cohesion = achieved when parts of the module operate on the same data. It makes sense to group them, because there is a strong relationship between them.
  * functional cohesion = achieved when all parts of the module work together to perform a well-defined task.
* should be made up of elements which functionally or logically belong together assuring cohesion.
* should have well defined interfaces which are accessed by other modules.
* give the Modules names that become part of the Ubiquitous Language. Modules and their names should reflect insight into the domain.

**Aggregates** = domain pattern used to define object ownership and boundaries.

* \= group of associated objects which are considered as one unit with regard to data changes.
* demarcated by a boundary which separates the objects inside from those outside.
* each Aggregate has one root which is the Entity and is only accesible from the outside.
  * The root can hold references to any of the aggregate objects, and the other objects can hold references to each other, but an outside object can hold references only to the root object.
  * If objects of an Aggregate are stored in a database, only the root should be obtainable through queries. The other objects should be obtained through traversal associations.
  * Objects inside an Aggregate should be allowed to hold references to roots of other Aggregates.
  * The root Entity has global identity, and is responsible for maintaining the invariants. Internal Entities have local identity.
* e.g. customer is the root of the Aggregate, and all the other objects are internal. If the Address is needed, a copy of it can be passed to external objects.

![](<../.gitbook/assets/Screenshot 2022-12-16 at 10.53.31.png>)



**Factories** =  domain pattern used to create objects.

* used to encapsulate the knowledge necessary for object creation, and they are especially useful to create Aggregates.
* when the root of the Aggregate is created, all the objects contained by the Aggregate are created along with it, and all the invariants are enforced.
* it is important for the creation process to be atomic.
* sometimes it may not be needed, and the constructor is enough.

**Repositories** = domain pattern used to store objects.

*   encapsulates all the logic needed to obtain object references. Domain objects won’t have to deal with the infrastructure to get the needed references to other objects of the domain.

    <figure><img src="../.gitbook/assets/Screenshot 2022-12-16 at 10.59.44.png" alt=""><figcaption><p>Taken from <a href="https://www.infoq.com/minibooks/domain-driven-design-quickly/">InfoQ's Domain-Driven Design Quickly</a></p></figcaption></figure>

### Maintaining model integrity

<figure><img src="../.gitbook/assets/Screenshot 2022-12-16 at 11.01.26.png" alt=""><figcaption><p>Taken from <a href="https://www.infoq.com/minibooks/domain-driven-design-quickly/">InfoQ's Domain-Driven Design Quickly</a></p></figcaption></figure>

**Bounded Context** = provides the logical frame inside of which the model evolves.

**Continuous Integration** = process of integration to make sure that all the new elements which are added fit harmoniously into the rest of the model, and are implemented correctly in code.

**Context Map** = document which outlines the different Bounded Contexts and the relationships between them.

### **The Customer-Supplier Pattern**&#x20;

\= relationship between 2 subsystems when one depends on the other.

* they do not have a Shared Kernel, because it may not be conceptually correct to have one, or it may not even be technically possible for the two subsystems to share common code.
* the **supplier is upstream** and the **customer is downstream**. However, the customer can factor their priorities into the planning of the upstream project.
* e.g. payment uses the model of the order process. However, payment defines requirements for the order process. Payment can only be done successfully if the order process provides the required data. So, payment can become a customer of the order process. That way the customer’s requirements can be included in the planning of the order process.

<img src="../.gitbook/assets/file.drawing (1).svg" alt="" class="gitbook-drawing">

### The Conformist Pattern

\= a bounded context simply uses a domain model from another bounded context

* e.g. the bounded contexts, **statistics**, and **order process**, both **use the same domain model**. The statistics are part of a data warehouse. They use the domain model of the order process bounded context and extract some information relevant to store in the data warehouse.
* with the _conformist_ pattern, the data warehouse team **does not have a say** in case of changes to the bounded context. The data warehouse team could not demand additional information from the other bounded context.

<img src="../.gitbook/assets/file.drawing (2).svg" alt="" class="gitbook-drawing">

### The Anti-Corruption Layer (ACL) Pattern

* the bounded context does not directly use the domain model of the other bounded context, but it contains a layer for decoupling its own domain model from the model of the bounded context.
* useful in conjunction with the _conformist_ pattern to generate a separate model decoupled from the other model.
* e.g. the bounded context _shipping_ uses an ACL at the interface to the bounded context _legacy_ so that both bounded contexts have their own independent domain models. This ensures that the model in the legacy system does not affect the bounded context _shipping_. _Shipping_ can implement a clean model in its bounded context

<img src="../.gitbook/assets/file.drawing (3).svg" alt="" class="gitbook-drawing">

### The Separate Ways Pattern

### The Shared Kernel Pattern

### The Open Host Service Pattern

### The Published Language Model Pattern



_(TO DO...)_

### Evolution

There are a number of reasons why new bounded context, and therefore new microservices, might be created:

1. Over time, **new functionalities** might justify **new bounded contexts**.
2. It might become apparent that one bounded context should really be split into two. That might be the case because new logic is added to the bounded context, or the team understands the bounded context better.
3. **New microservices** might be created by dividing a current one due to a **technical reason**&#x20;

### Resources

* [Domain-Driven Design: Tackling Complexity in the Heart of Software](https://www.amazon.co.uk/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215)
* [Domain-Driven Design Distilled](https://www.amazon.co.uk/Domain-Driven-Design-Distilled-Vaughn-Vernon/dp/0134434420)
* [Implementing Domain-Driven Design](https://www.amazon.co.uk/Implementing-Domain-Driven-Design-Vaughn-Vernon/dp/0321834577)
* [InfoQ's Domain-Driven Design Quickly](https://www.infoq.com/minibooks/domain-driven-design-quickly/)
