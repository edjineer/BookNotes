# Software Architecture wit h C++

Designing robust C++ systems with modern architectural practices, 2nd Edition

Authors: Gavrilian, Ostrowski, Gaczkowski

## Metadata

### Revisit Later

* Zero cost abstraction
* String_view vs string
* SOLID and DRY Principles
* SOAP: Simple object access protocol

### Links

* Additional Resources
* <https://github.com/PacktPublishing/SoftwareArchitecture-with-Cpp-2E>

### Notes for Review

* Leave Review here: <https://packt.link/r/1803243015>

### Questions

* What are the traits of a RESTful service?

## Notes By Chapter

### Part 1: Concepts and Components of Software Architecure

#### Ch 1: Importance of Software architecture and Great Design

* Accidental Architectures vs Emerging architecture
* Different Architectures for different scopes
  * Enterprise, Solution, Software, Infrastructure
* Conway's Law: Architecture of a software sysem freflects the organization its working on
* Users are either end users or administrators
* Domain driven design
* PRefer passing string and vector by reference since copying is expensive for these
* SOLID
  * Single responsibility Principle (SRP): don't make god objects
  * open-closed principle (OCP): software entities should be open for extension and closed for modification. Exaple std::ostream
  * liskov substitution (LSP): functions for base class must bea ble to take poitner of derived classes
  * interface segregation: have multiple small interfaces instead of one big one.
  * dependency inversion: high level modules should not depend on low level ones
* Dont repeat yourself: DRY
* Ideal = high cohesion, low coupling

#### Ch 2: Architectural Styles

* Stateful vs Stateless
  * Pros and cons: amount of info crammed into each message
  * HTTPS is stateless, REST is stateless
  * Example Stateful: FTP
* Monoliths
* Services and microservices
  * Service oriented architecture
  * Generally 2 types of services: SOAP and REST and newly gRPC
* Microservices: usually communicate with network protocols
  * Services should have smart endpoints and dumb pipes
  * Benefits of microservices: modularity, better testability, flexibility, integration with legacy, scalability
  * Disadvantages: needs mature devOps and CI/CD, IPC overhead
  * Benefit: scalabiltiy
* Event based architecture
  * Mediator topology
  * Broker Topology
* Event Sourcing
  * Snapshots are necessary
* Layered architecture
* Backends for frontends
* Module based architecture
* Hexagonal Architecture/Ports and adapters

#### Ch 3: Functional and non-functional requirements

### Part 2: Design and Development of C++ Software

#### Ch 4: Architectural and System Design Patterns

#### Ch 5: Leveraging C++ Language Features

#### Ch 6:Design Patterns and C++ Idioms

#### Ch 7: Building and Packaging

#### Ch 8: Package Management

#### Ch 9: The Future of C++ Code Reuse: Using modules

### Part 3: Architectural Quality Attributes

#### Ch 10: Writing Testable Code

#### Ch 11: Continuous Integration and Continuous Deployment

#### Ch 12: Security in Code Deployment

#### Ch 13: Performance

### Part 4: Cloud-Native Design Principles

#### Ch 14: Architecture of Distributed Systems

#### Ch 15: Interservice Communication

#### Ch 16: Containers

#### Ch 17: Observability

#### Ch 18 Cloud native design
