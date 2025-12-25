# Software Architecture wit h C++

Designing robust C++ systems with modern architectural practices, 2nd Edition

Authors: Gavrilian, Ostrowski, Gaczkowski

## Metadata

### Revisit Later

* Zero cost abstraction
* String_view vs string
* SOLID and DRY Principles
* SOAP: Simple object access protocol
* architecture rade off analysis method ATAM
* The open group architecture framework TOGAF
* cppdepend for dependency diagrams
* PRos and cons of each service model, realistic examples to understand all of these better
* Provider as a keyword
* Heroku, Google App Engine, Azure App Service
* Wasm
* CDNs
* Cattle not pets approach to microservices
* CAP Theorem/Brewer;s theorem
* BASE Semantics, PACELC theorem
* Sagas and Eventual Consistency
* SLAs
* Redundancy patterns, replication patterns
* Detecting faults
* Minimizing impact through circuit breaker, bulkhead, geodes
* Deployment patterns
* 7 layers of OSI = open systems interconnection
* C++
  * Iterator hierarchy: contiguous, random-access, bidirectional, forward, input, output
  * CTAD
  * inline namespace
  * SFINAE
  * Argument Dependent Lookup ADL, koenig lookup
  * CRTP
  * SSO/SBO.SOO

### Links/References

* Additional Resources
* <https://github.com/PacktPublishing/SoftwareArchitecture-with-Cpp-2E>
* Design Patterns: Elements of Reusable Object-Oriented Software (1994)
* Talk: m Jeff Dean’s well-known talk Numbers Everyone Should Know <https://www.cs.cornell.edu/projects/ladis2009/talks/dean-keynote-ladis2009.pdf>
* Gregor Hohpe and Bobby Woolf’s Enterprise Integration Patterns
* Arvid Norberg’s The ABI Challenge talk from C++Now 2019

- Sean Parent’s talk Inheritance Is The Base Class of Evil from the GoingNative 2013 conference.

### Notes for Review

* Leave Review here: <https://packt.link/r/1803243015>
* Practical intro to software architecture essentials, ig picture view
* Practical c++ examples with modern tools: cmake integration with Sphinx and doxygen, breathe
* Connecting a lot of relevant pieces that Id only heard in passing but not set foundation to compare/contrast, like service models
* Review questions

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

* Functional = what your solution should do; fetures, functions, behaviors
* NFRs = how well the system performs its functions
  * Quality attributes: performance, maintainability, etc
  * Definition of done/AC
  * Attribute driven design ADD
  * Constraints: non0negotiables

* Recognizing ASRs
  * Architecturally Significant requirements
  * Could be functional or NFRs
  * Iron triangle: budget, time and scope
  * AKA the project diamond or project management body of knowledge
  * Indicators of architecture significance
    * Create sw component to handle it
    * Significant impact on the system
    * Hard to achieve
    * Forcing tradeoffs; architecture rade off analysis method ATAM
  * Hindrances in ASRs and dealing with them
    * Hard to define, and done vaguely
    * Systems are independent, one ASR for one product might not make an ASR for another
  * Gathering Requirements
    * Know the context: note assumptions, ask questions, consider dependencies
    * Know existing documentation
    * Know stakeholders
    * Gather requirements from stakeholders
    * Document requirements, context(what decision was, who made it, when, rationale), and scope
    * Document Functional requirements
      * Easy approach to requirements Syntax EARS:
      * Ubiquitous requirement: the system shall...
      * Event driven: When x. the system shall y
      * Unwanted behavior: If x, the system shall y
      * State Driven: When state, the system shall x
      * Optional feature: Where feature, the system shall y
    * Manage version history
    * Document architecture
      * The open group architecture framework TOGAF
      * Domains of Togaf are: business architecture, data architecture, application architecture, technical architecture
      * 4+1 model: does not enforce a formal notation or standard, fixed set of views, views link together
      * UML
        * Logical View
        * Process view
        * Development View
        * Physical View
        * Scenarios
      * C4
        * Good for small/medium projects
        * Draw.io, mermaid, miro, lucidchart, icepanel
        * Shows big picture
        * Container diagram
        * Component Diagram
        * Code Diagram, UMLs, etc
    * Functional view: defines interfaces, consumed by other teams that interact or rely on it. Clarifies responsibilities between components
    * Information view:
    * Concurrency view: for concurrent units, bottlenecks
    * Development view
    * Deployment and operational views

### Part 2: Design and Development of C++ Software

#### Ch 4: Architectural and System Design Patterns

* 128-174
* Gang of Four
* Understanding the Peculiarities of Distributed Systems
  * Service Models
    * On Premises
      * Classical and pre-cloud era
      * High upfront cost, buy all resources
      * Pro: good for containing data for privacy, network latency
      * Hybrid deployment: Not necessarily a monolith, could deploy cloud on premesis. Comprimist between private and public clouds
    * IaaS
      * Most basic cloud service model
      * Virtual Data Center
      * Provides 3 resources: Compute: vms, containers, or baremetal; Networking: DNS servers, routing, firewalls; Storage: backup and recovery
      * You provide all SW, Os, middleware
      * Pro: Use the cloud's automatic scaling during usage surges
    * Container as a Service
      * Very similar to Iaas
      * Provides containers and orchestration capabilities
    * Platform as a Service
      * When infrastructure is not enough for your needs
      * Provider manages OS middleware and runtime-the platform you deploy your SW onto
      * Gives app versioning, service monitoring, db management, deployment tools
      * Examples: Heroku, Google App Engine, Azure App Service
      * CPAS = Communication Platform as a Service, gives communications backend with audio nad video
    * Function as a Service and Serverless
      * Run service only when needed
      * Like PaaS
      * FaaS gets more expensive than PaaS when service is running a long time
      * Can have better scalability
      * Don't pay for what you don't use
      * Serverless is rarely used with C++
        * Only AWS Lambda and Google Cloud functions support C++
      * Containers are language agnostic
      * Wasm Web Assembly
        * High performance apps in modern web browsers
      * Example Providers: AWS Lambda, Azure Functions, Genezio, Cloudflare workers, Netlify Functions, Google Cloud Functions
    * Software as a Service
      * Gives you a hosted application
      * Provider installs, runs, updates, and maintaines whole stack; backups, licensing and scaling
      * Customer Relationship management CRM
      * Downsides: network outages, service inturruptions, lack of control, data privacy
  * Avoiding fallacies of distributed computing
    * Network reliability: assume data will be lost over network. Add in re-trys, don't wait infinitely for success
    * Latency: don'twait on too many fine-grained calls, send in bulk. Use Content Delivery Networks CDNs
    * Bandwidth:
    * Network security: Defense in depth, use firewall certs and encryption
    * Topology: it can chang
    * Administrators: close collab with development and operations
    * Transport Cost: Protocol buffers to pack binary data
    * Networks arent homogeneous: Different configurations on different machines, differences in resiliency

  * CAP Theorem and Eventual Consistency
    * CAP = Consistency, Availability, Partition Tolerance
    * You pick 2 at most
    * Eventual Consistency: accounts for asynchronicity
      * Saga and compensating transaction patterns
        * Good for distributed transactions
        * two phase commits
        * Choreography based sagas
        * Orchestration based sagas
* Making system fault tolerant and available
  * Availability = percent time system is up and reachable
  * SLA = Service level agreement with could to specify how much downtime can occur per year
  * Building Fault tolerant systems
    * Redundancy Patterns: failover, hot standby, active-passive failover, active active failover, leader election, consensus
    * Replication Patterns: master-slave (all read, only one writes), multi-master replication, queue based load leveling, back pressure pattern
    * Detecting faults: sidecar design, heartbeat mechanism, leaky bucket
  * Handling faults
    * Minimize the impact
    * Retry pattern
    * Avoid cscading failures: circuit breaker, bulkhead pattern, Geodes pattern
* Integrating the system
  * Pipes and filters
  * Competing consumers
  * Transitioning from legacy systems
    * Anti corruption layer pattern
    * Strangler pattern
* Achieving performance at scale
  * CQRS = command query responsibility segregation
    * Good for CRUD systems
  * Command Query separation: separate API calls into separate queries
    * Easier to reason about code, fewer heisenbugs
  * Event Sourcing: Just store changes
  * Caching Patterns
    * Client side
    * Web Server caches
    * DB Caches
    * Application Caches
    * CDNs
  * Updating caches
    * Read through
    * Write Through
    * Write behind
    * Cache aside/lazy loading
    * Write around
    * Refresh ahead: TTL = Time to live
* Designing data storage
  * Decide on SQL or NoSQL based on size of your DB
  * Small DBs = SQL or SQLite
  * If TB or bigger, NoSQL is better
  * If 10 TN, then data warehouse
* Deploying system
  * Sidecar
    * Ambassador and adapters
  * Zero Downtime Deploymnts
    * Blue green
    * Canary Release pattern:
  * External Configuration Store pattern
* Managing APIs
  * API management tools, comprised of:
    * API Gateway, an entrypoint for all users
    * Reporting and analytics
    * Portal for developers
    * Portal for admins
    * Monetezation
  * API Gateways
    * Layer 7 routing
    * OSI Model
      * Physical 1, Data link 2, Network 3, Transport 4, Session 5, Presentation 6, Application 7

#### Ch 5: Leveraging C++ Language Features

* 174-218
* Using RAII
  * REsource acquisition is initialization
  * Where stack based object lifetime is managed by creation and deletion
  * Constructors and destructors
* Specifying the interfaces of containers in C++
  * Argument dependent lookup (ADL)
  * Iterator hierarchy
    * Concepts allow you to add static_assert to check a condition at compile time
  * Deduction Guides
  * Class Template argument deduction (introduced in C++ 17)
* Using raw and smart pointers in interfaces
* Specifying preconditions and postconditions
  * Comments, if statements, or static asserts are options. Contracts might come in for C++26
* Employing inline namespaces
  * Application binary interface (ABI)
* Applying std::optional
  * Brought in with C++17
  * Optional function parameters
  * Optional function return values
    * C++23's std::expected
  * Optional Class Members
* Using monadic interfaces
  * Based on functional programming
  * Monads = subtype of functors
  * Category theory
* Writing declarative code
  * Imperative(code tells machine how to achieve goal) vs declarative (what you want to achieve)
* Moving computations to compile time
  * In 2000s, craze to compute during compile time instead of runtime
  * constint, consteval, constexpr(declared that functions and vars can be evaluated at compile time, even though compiler decides whether it actually does it)
  * const
* Leveraging the power of safe types
  * Casts are type-unsafe
  * Consrain template parameters
    * concepts
    * SFINAE based type traits to enforce constraints

#### Ch 6:Design Patterns and C++ Idioms

* 218-266
* Writing Idiomatic C++
  * GRASP: General Responsibility Assignment Software Patterns
  * Automating scope exit actions using RAII guards
  * Managing copyability and movability
    * Copy ctor and copy assignment
    * Move semantics
  * Implementing non copyable types
    * Examples: unique_ptr and mutex
  * Rules of 3(Cpp98) and 5
  * Rule of 0
    * Set to default for all of them
  * Using hidden friends
  * Argument Dependent Lookup (ADL)
  * Providing exception safety using the copy and swap idiom
    * Safety levels:
      * No guarantee
      * Basic exception safety
      * Strong Exception Safety
      * No throw guarantee
  * Writing niebloids/functors
  * Policy based design idiom
* Applying the curiously recurring template pattern
  * AKA CRTP
  * Dynamic (runtime) vs static(compiletime) polymorphism
  * Type erasure: hiding type under a polymorphic interface
* Implementing deducing this
  * Explicit object parameter
  * Cannot be declared static or virtual
* Creating objects
  * Using factories
    * Factory methods/ named constructor idiom = member function that calls private constructor for you
    * Controlled creation mechanism
    * Factory functions
    * Return type
    * Factory Classes
    * Using Builders
      * When object needs multple steps to be created
      * Named parameter idiom
  * Using Prototypes
    * Object Creation
    * clone keyword
* Tracking state and visiting objects in C++
  * Change beavior through internal stateness
  * std::variant and statically polymorphic double dispatch
* Dealing with Memory efficiently
  * Reducing dynamic allocations using SSO/SBO/SOO
    * Dynamic allocaations Cost CPU cycles, risk memory fragmentation
  * Save memory by herding COWs
    * Copy on Write
  * Leveraging polymorphic allocators
    * Memory arenas/region/memory context
    * Placement: allows you to explicily construct objects at specific memory addresses without additional allocations
    * Monotonic Memory resources
    * Pool Resources
    * Ensure no unexpected allocations
    * Wink out memory

#### Ch 7: Building and Packaging

* 266-300
* Getting the most out of compilers
* Abstracting the Build Process
* Using External Modules
* Reusing quality code

#### Ch 8: Package Management

* 300 - 314

#### Ch 9: The Future of C++ Code Reuse: Using modules

* 314 - 330

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
