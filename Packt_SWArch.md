# Software Architecture wit h C++

Designing robust C++ systems with modern architectural practices, 2nd Edition

Authors: Gavrilian, Ostrowski, Gaczkowski

## Metadata

### Revisit Later

* Zero cost abstraction
* String_view vs string
* SOLID and DRY Principles

### Links

* Additional Resources
* <https://github.com/PacktPublishing/SoftwareArchitecture-with-Cpp-2E>

### Notes for Review

* Leave Review here: <https://packt.link/r/1803243015>

### Questions

* asdf

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

*

#### Ch 2: Architectural Styles

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
