# food-ordering-system
An application is implemented using multiple architecture patterns.
Consist of three microservices.
Each branch consist of particular architecture pattern in extended way sequence is mentioned below:

1) DDD(Domain Driven Design) Architecture Pattern

    Domain-Driven Design offers solutions to common problem when building enterprise software

    Strategic DDD vs Tactical DDD

    Strategic DDD: Introduces boundaries for domain model. Single Bounded context per each domain

               * What is a Domain? Operational area of your application. e.g;  Online food ordering

               * Bounded Context: Central pattern in DDD. Boundary within a Domain

               * Ubiquitous Language: Common language used by domain experts and developers

    Tactical DDD: Implementation patterns.

      * Entities: Domain object with a unique identity. Embodies set of critical business rules.

      * Aggregates: Group of Entity objects which always need to be in consistent state

      * Aggregate Root (AR): Entry point Entity for an aggregate. All business operations should go through root.
         An Aggregate should be referenced from outside through its root only. AR should have pure, side-effect
         free functions

      * Value Objects: Immutable objects without identity. Only value matters. Brings context to the value

      * Domain Events: Decouple different domains. Describe things that happen and change the state of a domain.
         Makes the system extendable. Domain event listeners runs in a different transaction than the event publishers
         In  Domain-driven system, domain events are an excellent way of achieving eventual consistency. 
         Any system or module that needs to update itself when something happens in another module or system    
         can subscribe to the domain events coming from that system

      * Domain Services: Business logic that cannot fit in the aggregate. Used when multiple aggregates required in 
         business logic Can interact with other domain services

      * Application Services: Allows the isolated domain to communicate with outside. Orchestrate transaction,
         security, looking up proper aggregates and saving state changes of the domain to the database. Does not  
         contain any business logic.
         Domain event listeners are special kind of Application services that is triggered by domain events. Each   
         domain event listener can have a separate domain service to handle business logic


2) Clean Architecture and Hexagonal Architecture
   
     Separation of concerns by dividing the software into different layers  

    Use Dependency Inversion and Polymorphism to create a dependency rule to make the domain layer most independent and stable layer

    Source code dependencies can only point inward, towards to domain layer

    Independent of Frameworks, UI, Databases and any external agency

    Testable domain layer without requiring and external element

    Define Entities and Use Cases for domain logic

    Same high level principle with hexagonal and onion architectures: Isolate the domain

    Hexagonal Architecture also known as Ports & Adapters

    Divides the software as insides and outsides, and start with inside, domain layer

    The principle of the hexagonal architecture is to isolate the domain from any dependency, such as UI, Data layer or even a framework like Spring

    It is a response to the desire to create thoroughly testable applications with isolated business logic from the infrastructure and data sources

    Invented in 2005 by Alistair Cockburn 

    As Cockburn says: “Allow an application to equally be driven by users, programs, automated test or batch scripts, and to be developed and tested in isolation from its eventual run-time devices and databases.”

    Especially useful for long-lasting applications that need to keep up with changing requirements

    Improvement to traditional Layered Architecture. The dependencies are now plugins to the business logic. All dependency arrows point to business logic making the domain independent. Reverses the relation using ports and adapters.

    Delay the implementation details of dependencies

    Easier to test the business logic by mocking the dependencies even before deciding the implementation details

    Replace an adapter implementation easily, without touching the business logic

    Easier to maintain as changing a part of software will not affect other parts

    Independent development and deployment of different parts

    Entities: Objects that embodies a small set of critical business rules

    Use Cases: Describes application-specific business rules. Contains the rules that specify how and when the Critical Business Rules within the Entities are invoked.
               Orchestrates the flow of data to and from the entities, and direct those entities 
               to use their Critical Business Rules to achieve the goals of the use case

3) Saga Architecture Pattern

    SAGA: Distributed long running transactions across services. 
    Used for Long Lived Transactions (LLT).  First invented in a 
    publication on 1987
    https://www.cs.cornell.edu/andru/cs711/2002fa/reading/sagas.pdf

    Chain of local ACID transactions to finalise a long running transaction across services.

    Compensating transactions: Rollback in case of failure


4) Outbox Architecture Pattern
 
    Outbox: Help use of local ACID transactions 
    to let consistent (eventual) distributed transactions. 

    It will complete SAGA in a safe and consistent way. 

    Persist events in local database automatically with ACID transaction

    Read the events and publish
         - Pulling Outbox Table: Pull the events with a scheduler
         - Change Data Capture: Listen transaction logs

    Keep track of saga and order status in Outbox Table

    Ensure idempotency: Do not consume same data 

    Optimistic locks and DB Constraints: Prevent data corruption


5) CQRS Architecture Pattern.
 
    (CQRS): Separate read and write operations. Better performance on read part using right technology for reading, and preventing conflicts with update commands. Scale each part separately.

    Leads to eventual consistency, as the read store is updated asynchronously.

    Once the write operation is persisted, an event is stored in event-store.

    Events can be replayed multiple times based on requirements to create different type of query store.

