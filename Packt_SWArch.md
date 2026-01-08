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
  * CMake modules
  * Hyrum's law
  * IFNDR: ill formed no diagnostic required
  * Binary Module interfaces BMI
  * bdwgc
  * Fils unbelievable garbage colector FUGC
  * GSL
   gherkin, and cucumber framework
  * Ansible and deployment as code
  * Idempotence
  * Packer and Terraform for infrastructure
  * Configuration drift
  * CSP C++ Server pages
  * DVL Dynamic view loading
  * Remote code execution
  * ASan, LSan, ThreadSan, MSan, UBSan
* Measurement tools
* Memcached, redis
* Relationship between OSI and TCP/IP
* PRotobuff
* Hsitory of REST
* URI vs URL
* HATEOAS
* Twelve factor app methodology
* Docker architecture diagram pg 597
* Kubernetes as an orchestrator of containers
* sdplog

### Links/References

* Additional Resources
* <https://github.com/PacktPublishing/SoftwareArchitecture-with-Cpp-2E>
* Design Patterns: Elements of Reusable Object-Oriented Software (1994)
* Talk: m Jeff Dean’s well-known talk Numbers Everyone Should Know <https://www.cs.cornell.edu/projects/ladis2009/talks/dean-keynote-ladis2009.pdf>
* Gregor Hohpe and Bobby Woolf’s Enterprise Integration Patterns
* Arvid Norberg’s The ABI Challenge talk from C++Now 2019
* Sean Parent’s talk Inheritance Is The Base Class of Evil from the GoingNative 2013 conference.
* GCC List of books about compilers
* Rule of Chiel, ranking of fastest compile time operations
* Tool: "include what you use"
* IceCC as a distribution tool, and distcc
* The cathedral and the bazaar from ESR
* C++ Core Guidelines: <https://github.com/isocpp/CppCoreGuidelines>
* Herb Sutter C++ Securuty article: <https://herbsutter.com/2024/03/11/safety-in-context/>
* CVE List <https://cve.mitre.org/>
* Chandler Carruth, Tuning C++: Benchmarks, and CPUs, and Compilers! Oh My! (YouTube video),
CppCon 2015: <https://www.youtube.com/watch?v=nXaxk27zwlk>
* Hubert Matthews, Optimising a Small Real-World C++ Application (YouTube video), ACCU 2019:
<https://www.youtube.com/watch?v=fDlE93hs_-U>

### Notes for Review

* Leave Review here: <https://packt.link/r/1803243015>
* Practical intro to software architecture essentials, ig picture view
* Practical c++ examples with modern tools: cmake integration with Sphinx and doxygen, breathe
* Connecting a lot of relevant pieces that Id only heard in passing but not set foundation to compare/contrast, like service models
* Review questions
* Great recommendations for talks and additional resources of various mediums that serve as strong foundation for multiple disciplines, SW arch, platform deployment, C++ idioms, etc, compilers
* General concepts, but with C++ examples
* Modern tools like drogon, prometheus, etc. Gives overview of available tools, compares contrasts, practical c++ examples
* Cloud native
* Forward and reverse proxy

### Questions

* What are the traits of a RESTful service?
* Single compilation unit build: it combines all cpp files into translation units, how is that not an absolute mess?

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
  * Using multiple compilers
    * Using multiple compilers help identify portability, optimize performance, catch more issues
    * Clang = strives for complieance with C++ standards more than GCC
    * GCC: try not to use gnu variants
    * Cross Compilation
    * CMake: for building testing packaging and distributing cross platform software
    * Toolchain files
  * Reduce build times
    * Use a fast compiler
    * Precompiled header
    * Rethinkng Templates
    * Rule of Chiel: some C++ constructs are most diffucult for compiler
    * Ranking of compile time cost, fast to slow:
      * Look up memoized type
      * Add parameter to alias call
      * Add parameter to a type
      * Calling an alias
      * Instantiating a type
      * Instantiate a function template
      * SFINAE
    * Leveraging tools
      * Single compilaion unit build, unity build. Unclide all cpp files into one translation unit
        * Order of inclusion and composition matters
        * Renders static keyword useless
        * PCH =precompiled header
      * Ninja as a faster generator tool
      * Ccache
      * IceCC: distribute builds across hosts
    * Find potential code issues
      * Ignore warnings from unrelated libraries: use a compiler switch
      * Use -pedantic flag to be informed of all non-standard extensions youre using
      * For Compiler flags, try to do `-Wall -Wextra -Wpedantic and Werror`
  * Using compiler centric tools
    * Static analysers, diagnostics, clang-tidy
* Abstracting the Build Process
  * CMake = Build system generator
    * Configuration Log
    * Two styles of cmake file: variable based (obsolete), or target bsaed (modern)
    * CMake Modules
    * CMake Dir Variables
    * Specify cmake targets
      * Add executable
      * Cmake antipattern = globs
        * Breaks the separation of configure and generate phases. Globs are discouraged for source lists
        * Wouldnt pick up new files by default
        * CONFIgUrE_DEPENDS = tells CMake to rescan globs and reconfigure if dirs changed. But it slows down builds and adds runtime cost
      * target_compile_features(name, PRIVATE/PUBLIC/INTERFACE cxx_std_17)
        * Privte = internal requirement. Just visible to this target, not other targets that depend on it
        * Interface = header only library, only gives a C++ API. Target that is not built
        * Public = both
      * set_target_properties: enfores standard and enable/disables c++ extensions
      * add_library: creates static, object, and interface libraries, define imported libraries
    * Specify the output directories
      * set VARIABLE
      * Dynamic link library files
    * Generator expressions
      * Cmake executes if statements at configure time, not build/install time
      * Generator expressions in target_compile_definitions or target_include_directories
* Using External Modules
  * Top preference: bring in Conan to manage packages
  * Fetching Dependencies
    * Use CMake's fetchContent module
    * Dependency providers
  * Using or writing Find Scripts
    * find_packge(boost)
  * Ctest
* Reusing quality code
* Note: one of my favorite chapters!

#### Ch 8: Package Management

* 300 - 314
* Intro to Package Management
  * Ordinary vs development packages
* Conan
  * Open source, decentralized
  * Conan Dependencies: conanfile.txt
  * Conan targets from CMake
  * Testing conanpackage

#### Ch 9: The Future of C++ Code Reuse: Using modules

* 314 - 330
* History of headers
  * Headers have been around since 1970s to organize code, separating interface from implementation
  * ODR = One definition rule
  * Hyrum's law

* Consuming Modules
  * Compiled into an object file and module interface file
  * Extension .cppm

* Creating your own module unit
  * Module unit, module partition, module linkage, header unit added in Cpp20
  * 2 module unit types: module interface unit and module implementation unit
  * Fragments = section of module interface unit
  * Submodules
  * C++ Linkage: internal and external, and module
  * IFNDR: ill formed no diagnostic required
* Binary Module interfaces BMI
  * Or CMI Compiled module interface
  * Or Cang Precompiled module PCM

### Part 3: Architectural Quality Attributes

#### Ch 10: Writing Testable Code

* 332-362
* Benefits of Testing Code
  * Testing Pyramid of Functional Tests: Unit test(code), Integration test(design), Systme test (requirements), Acceptance Testing (end to end client needs)
  * Non Functional Tests
    * Performance
    * Endurance
    * Security
    * Availability
    * Integrity
    * Usability
  * Regression Testing
    * RTS = Regression test selection strategy, to identify and run only suspected relevant tests
  * Root cause analysis: 5 whys
    * Defense in depth
* Runtime Testing Frameworks
  * Google test, google mock
  * Catch2 for behavior driven development
  * Doctest
  * Boost.test
  * DrogonTest
* Compile time testing techniques
  * Template metaprograming
  * constexpr gives more control of compile time logic, and consteval gives more control of how it is evaluated during compilation
  * Hard to test compile time programming
  * static_assert
* Understanding test doubles
  * Hard to test third party component interaction
  * Different Test Doubles: stubs and fakes
  * TEST_F macro
* Test driven class design
  * Not all classes can be tested easily
  * Tests and Design clash
  * Write tests first
  * Defensive programming
    * Type specificity
    * explicit keyword protects from implicit casts
* Automating app tests for CICD
  * Promote tests from full suite to gating suite
* Automating infrastructure validation for CICD
  * Serverspec, Testingfra, Goss, Terratest

#### Ch 11: Continuous Integration and Continuous Deployment

* 362-394

* CICD Relies on good test coverage
  * CI is more smoke tests
  * CD is more end to end

* Understantind and implementing CI
  * CI = shortening integration cycles by merging changes into code frequently
  * Integration several times a day
  * Quick feedback loop
  * Release early and often
    * Open source movement
    * Rely on automate tests
  * CI Merits
    * integrate work of multiple devs into a single repo
    * prevents "works on my machine" excuse
    * Example wiht gitlab
* Gates
  * Automated checks; unit tests
  * Linters, code formatters, static analysis, git hook for running tools before commit
  * Reviewing code
    * Follow project guidelines, fit in architecture, etc
    * Peer review and architect reviews
    * Cross team expert review
    * Async reviews or in person
    * MR/PRs
* Test driven automation
  * CI and continuous testing are hand in hand
  * Behavior driven development
    * Does change satisfy requirements?
    * Cucumber framework, or Gherkin
  * Writing tests for CI
    * Unit Tests = Self contained (no external dependecies), and run in parallel
* Managing deployment as code
  * Handling deployment with version controlled code
  * Ansible= config management tool that supports deployment as code
    * Shell scripts good for cimple deployments
    * Ansible does better for complexity
    * Integrates with CICD through idempotence
    * Use reusable components roles and playbooks
    * Runs in both push and pull models
* Building deployment code
* Understanding and implementing CD
  * CD = Automated process that originates when someone pushes a change, and finishes with change successfully deployed and tests passing
  * GitOps
  * Git Actions for precommit workflow
  * Implement pipeline with github actions

* Using immutable infrastructure
  * Immutable infrastructure
  * Treat infrastrucutre as any other artifact
  * Deploy in virtual machine
  * Hashicorp tools: Packer and Terraform
  * Configuration drift is obsolete for immutable infra
  * Safer upgrades
  * Would also need to do load balancing and have redundancy in order to work well with immutable infra
  * Instance images with Packer Example: use Elastic block store builder
  * Orchestrate infra with Terraform: build an EC2 instance bsaed on packer using terraform

#### Ch 12: Security in Code Deployment

* 394-428
* Security-conscious design
  * Regulations: GDPR, CCPA, CPRA, PIPL, APPI
  * Making interfaces easy to use and hard to misuse
    * Interface: connection between elements
    * Avoid: ambiguous names of parameters, using output params for results, too many parameters
    * Qsort lacks parametric polymorphism
    * Monomorphization
  * Enabling automatic resource management
    * Poor resource management leads to system instability like memory leaks, race conditions, deadlocks
    * Garbage collection, RAII
    * Guidelines support library
  * Drawbacks of concurrency
    * Gives illusion of simultaneity
    * Concurrency ~= parallelism (good diagram pg 402)
    * RMW primatives: read modify write, and compare-and-swap
  * Secure Coding guidelines
    * GSL helps with this. Header only library to use defined types
    * Defensive coding and validation
      * Avoid using C API directly
      * Intelligent reuse of existing code
      * Defensive programming is not paranoid programming
      * Use Expects() and Ensures()
      * C++ Server pages
    * Common Vulnerabilities (OWASP)
      * Injection
      * Broken authentication
      * Sensitive data exposure
      * XML External entities
      * Broken access control
      * Security misconfiguration
      * XSS
      * Insecure deserialization
      * Using components with known vulnerabilities
      * Insufficient logging and monitoring
* Checking whether dependencies are secure
  * 2 forms of dependencies: external and internal
  * CVE List
    * Common vulnerabiities and exploits
    * Maintained by CVE Numbering authorities and Computer emergency response teams (CERTS)
  * Automated scanners, OWASP dependency check
  * Automated dependency upgrade management: Synk and renovate scan
* Hardening Code
  * Use modern C++ constructions over C equivalents
  * Hardening = reduce system's surface of vulnerability, increase robustness of available functions
  * Tools = firewalls, patches, intrusion detection systems
  * Security oriented memory allocator
    * Heap overflow
    * FreeGuard, hardened_malloc, Scudo
  * Automated checks
    * Compiler warnings
    * Static analysis
      * Static application security testing SAST
      * Cppcheck, flawfinder, LGTM, SonarQube
    * Eliminating dangling references in C++ with lifetime bounds
    * Dynamic analysis
      * Valgrind, Application Verifier
      * Sanitizers
        * ASan, LSan
      * Fuzz Testing
    * Process isolation and sandboxing
* Hardening environment
  * Linking strategies and their security implications
  * Address space layout randomization ASLR
  * DevSecOps: Devops with security in mind from beginning

#### Ch 13: Performance

* 428-492

* Measuring Performance
  * Prepare for accurate and repeatable performance measurements
    * Put machine into performance mode over power saving mode
  * Leveraging different types of measuring tools
    * Benchmarks = measure execution speed in prepared tests
    * Microbenchmarks,simulations, replays, industry standard benchmarks, profilers, tracing
  * Using Microbenchmarks
    * Google benchmark as a tool
    * Compiler explorer and quickbench
    * Argument capture
    * Vary input sizes
  * Using catch2
  * Using nanobench
  * Choosing which benchmark to measure and optimize
    * only on code that matters
  * Create performance tests using benchmarks
  * Performance profiling
    * help analyze where performance numbers came from
    * 2 profilers: instrumentation and sampling
  * Tracing
    * Valuable for distributed systems
    * Log execution path of code

* Helping the compiler generate performant code
  * Optimizing whole programs
    * Link time optimization
  * Optimize based on real world usage patterns
    * Profile guided optimization
    * Profile direscted feedback
    * Feedback directed optimization
  * Cache friendly code
    * flat vd node based implementations
  * Design code with data in mind
* Parallelizing computations
  * Amdahls law
  * Gustafson's law
  * Dr Gunthers universal scalability law
  * Choose between threads and processes
  * Using standard parallel algorithms
  * OpenMP and MPI
* Using Coroutines
  * Coroutines ccan suspend and resume execution
  * Coroutines in c++20 are stackless
  * C++ keywords for coroutines: co_await, co_yield, and co_return
  * cobalt
* Implementing efficient algorithms
  * Recursion and tail recursion

### Part 4: Cloud-Native Design Principles

#### Ch 14: Architecture of Distributed Systems

* 492-526

* Understanding SOA
  * SOA = Service oriented architecture
  * ESB = enterprise service bus
  * Four properties of service = represents a business activity with a defined outcome, self contained, opaque to users, may be composed of other services
  * ESB from peripheral component interconnect, PCI, computer bus
  * MOM = message oriented middleware
  * ESB Component roles: maintain service redundancy, route messages between services, monitor message exchange, resolve contention between components, enforce quality of service
  * Benefits of ESB= better scalability, distributed workload, configuration over implementation, easier to design loose couple services, replaceable services, built in redundancy capability
  * Disadvantages: single point of failure, complex config,message queueing
  * Web Services
  * Messaging and streaming
    * Message queues, used for ISC interservice communication
    * Message brokers
  * Cloud computing
  * Challenges of SOA: costs for RPC, Conway's law

* Diving inro microservices
  * Benefits of microservices: modularity(mono repo or multi repo?), scalability, flexibility, integration with legacy systems, distributed development,
  * Disadvantages: Reliance on mature devOps, harder to debug, additional overhead,
  * Design patterns
    * Decomposition patterns
    * Decomposition by business capability
    * Decomposition by subdomain
    * Database per service pattern
  * Deployment strategies
    * Single service per host
    * Multiple services per host
* Design considerations for scalable microservices
  * Address scalability bottlenecks: memory, storage, computing
  * Outsourcing memory management: memcached, redis
  * Outsourcing storage: AWS S3
  * Outsourcing computing: SWIG: simpified wrapper interface generator
  * Scaling microservices
    * Single service per host deployment
    * Scaling multiple sercices per host
* Leveraging managed services and cloud providers
  * VPS = virutal private server
  * cloud sdk
  * Infrastructure as Code

#### Ch 15: Interservice Communication

* 526-588

* Intro to ISC
  * ISC is a subset of IPC
  * OSI
  * TCP/IP is 4 level variant of OSI

* Interaction styles
  * Client server interactions
  * Synchronous communication or async
  * One to one, one to many, many to one, many to many
* Messaging Systems
  * Low overhead messaging systems
    * MQTT
    * ZeroMQ
  * Brokered messaging systems
    * Apache Kafka, RabbitMQ, event driven architecture
* Using Web Services
  * Tools for working with webservices: wget, curl, libcurl, testing framework, browser extensions, api clients like bruno/hopscotch, testing sw, packet analyzers like wireshark
  * Webapi payload formats
    * Protobuff, bson, orc
  * XML Based web services
    * XML-RPC and SOAP
    * Simple object access protocol
    * URI and WSDL
    * UDDI
    * SOAP libraries: Apache axis and gSOAP
  * JSON based web services
    * JSON-RPC
  * Web API Design approaches
    * REST: representational state transfer
      * architectural style
      * Roy fielding
      * Defines constraints for implementing web service
        * Client server architecture
        * Statelessness
        * Cachability
        * Layered System
        * Uniform interface
          * Resource identification
          * Manipulation of resources through representations
          * Self descriptive messages
          * Hypermedia as engine of Application state HATEOAS
        * REST uses HTTP as transport protocol, uris represent resouces, and HTTP verbs for actions
          * POST, GET, PATCH, DELETE, PUT
        * Group of resources = collection
        * CRUD
    * GraphQL
      * query language based API paradigm
      * Manipulates data directly, allows clients to structure responses
      * Request types: query, mutation, subscriptions
      * Disadvantages: steep learning curve, increased server load, security risks, resolver reliability, complexity in caching, monitoring difficulty, N+1 problem
    * API Description languages
      * OpenAPI/Swagger
      * AsynAPI
* RPCs
  * Thrift (non-HTTP based)
  * gRPC (Http based)

#### Ch 16: Containers

* 588-626

* Reintro to Containers
  * Docker and Kubernetes preceded by Linux containers
  * Linux equivalents = chroot/change root
  * Goal = isolate one execution environment from another
  * Usually share OS kernel as host (different from virtualized envs)
  * Deployment = unpack the continer image
  * Exploring Container types
    * App container, OS container, VM
  * Rise of microservices and containers
    * Twelve factor app methodology best practices to enable portable and resilient apps deployed to the web
      * Exactly one Code base
      * Dependencies are explicit and isolated
      * Config is stored in the environment
      * Backing services are treated as attached resources
      * Build, release, and run: strictly separated in CI/CD pipelines
      * Processes: apps run as one process
      * Port bingding: self contained services are exposed via port binding
      * Concurrency: scale app pool of one or more stateless processes
      * Disposability
      * Dev Prod parity
      * Logs
      * Admin processes
    * ASN = Abstract syntax notation one
  * Choosing when to use containers
    * Benefits of containers
      * Less overhead during runtime
      * Offer smaller images
      * Easier to orchestrate than regular binaries
      * Isolation
      * Standardized runtim means higher portability
    * Disadvantages of containers
      * Tough migration if app does not use IPC or is stateful
      * Persistent storage
      * Hard for Windows
* Building Container images
  * Docker architecture and stack
  * Container images explained
    * Containers: dynamic, running instances from container image
    * Container images: static, composed of layers that are snapshots of filesystem changes and metadata for env vars
    * Docker has UFS = Union file system to manage layes
  * Building container images with dockerfiles
    * Describes operatiosn needed for making the resulting image
    * Use `docker build` to make image from dockerfile
  * Naming and distributing images
    * 3 elements to a name: registry name, image name, and tag
    * Default registry is docker.io
    * Amazon's ECR: elastic container registry, azure container registry, Google artifct registry, jfrog, etc
  * Compiled applications and containers
    * Install all dependencies first, copy source files, compile as one: downside is a lot of uneccessary files
  * Targeting multiple architectures
    * Docker manifest or buildx
  * Alternative tools to build application containers
    * Buildah, podman, skopeo
    * ansible-bender
  * Integrating containers with cmake
    * Configure dockerfile with CMake
    * Build container images with CMake
* Practical runtime considerations for containers
  * Containers give flexibility in testing and deployment environments
  * Fit well with CICD pipelines
  * Easy t oadd nodes
  * Runtime libraries inside containers
    * Name service switch
  * Alternative container runtimes
    * Kata cotainer initiative
* Understanding container orchestration
  * Orchestrator keeps track of all nodes, montoris health and status
  * Self hosted solutions
    * Kubernetes: orchestroator
      * Can use docker commands to interact with kubernetes clusters
      * Docker works on a container, Kubernetes works on a Pod
      * Pod = one or moer containers that share storage volumes, networking resources, and single cluster IP Addresses
      * Containers in a pod can communicate with each other over localhost
      * Pods in a cluster can communicate without Network address translation
      * Networking model in Kubernetes is different than docker: Docker = fwd ports, kuberneters needs a service resource
      * Kubernetes is declarative and eventally consistent
      * CNCF = cloud native computing foundation
    * Docker swarm
      * Docker engine comes with Docker swarm orchestrator
    * Nomad: three jobs: service, batch, or system
    * OpenShift
  * Managed Services
    * AWS ECS
    * Amazon EC2
    * AWS Fargate
    * Azure Service Fabric

#### Ch 17: Observability

* 626-648

* Challenges are finding root causes of issues

* Logging
  * Audit logging/audit trailing
  * Logging with microservices
    * Logging in C++ with sdplog
      * Features: multiple sinks, daily log files, colored console logging, QT widget logging, thread option, sync and async logging, log rotation
      * Automated renaming and archiving
    * Unified logging
      * Layer to fwd logs to destination
    * Logstash
      * Owned by elastic, written in ruby
    * Filebeat
    * Fluentd, Fluentbit
    * Vector
  * Log aggregation
    * Storing and accessing the logs
    * Elastisearch or Loki
  * Log visualization
    * Kibana or Grafana
* Monitoring
  * Collecting and analyzing data to imrpove health and behavior of a system
  * 3 Interesting metrics: availabiltiy, resource utilization, performance
  * Implementing application metrics
    * prometheus
  * Monitoring health checks: liveness, readiness, startup probes, responsiveness
* Tracing
  * Jaeger and OpenTracing
  * Zipkin
  * OpenTelemetry

#### Ch 18 Cloud native design

* 648-694
* Understanding cloud native
  * Just running in the cloud doesnt make something cloud native, it can still be on-prem
  * Cloud native = distrubuted, loosely coupled, scalable
  * CNCF = Cloud native computing foundation
    * Hosts kubernetes
    * Cloud native apps are built within application containers
  * Cloud as an operating system
    * VMs are rarely used in cloud native design
    * Cloud native apps are web and mobile first
  * Load balancing
    * Spreads requests across cluser of services
    * Improves responsiveness and availability
    * More throughput and less downtime
  * Reverse and forward proxies
    * Reverse = added before a load balancer; acts on bealf of servers handling requests
    * Benefits of reverse proxy: security (since it hides address of your server), flexibility and scalability, caching, compression, SSL termination
  * Service Discovery
    * Allows for automatic detection of services on a network
    * Either client side service or server side service discovery
    * LBaaS load balancer as a service
* Using Kubernetes to orchestrate cloud native workloads
  * Features of kubernetes: autoscaling of apps, configurable networking, batch job execution, unified upgrading of applications, declarative configuration
  * Flexible, and can scale
  * Kubernetes structure
    * Cluster is usually 6 machines or more. Three are the control plane, three are worker nodes
    * Control Plane: Deciddes on actions and delegates
      * Runs API Server, Scheduler, etcd, and Additional componenets specific to needs
    * Worker nodes: Container runtime, kubelet, kube-proxy
  * Approaches to deploying kubernetes
    * Kubernetes operations
  * Understanding the Kubernetes concepts
    * Container
    * Pod = one or more containers. All containers in a pod share same network interfaces, volumes and resources
    * Deployment: manages pod and the life cycle
    * Daemonset = controller, manages where pods are distributed
    * Jobs = one-off tasks, restart automatically when containers terminate
    * CronJobs = run periodically within a cluster
    * Services
  * Managing Kubernetes declaratively
    * Supports probes to monitor app health
  * Kubernetes networking: container network interface
    * Container to container communication
      * Control groups in linux kernel
    * Pod to pod communication
      * Each pod has own IP address
    * Pod to service communication
    * External to internal communication
  * Considerations before adopting Kubernetes
    * Infrastructure costs
    * Operations costs
    * Education costs
* Observability in cloud native distributed systems
  * Tracing is essential
  * Instrumenting an App with OpenTelemetry Operator
* Connecting services with a service mesh
  * Service Mesh Basics
    * Trades off some resources for an automated and centrally controlled solution to challenges
    * Features are abstracted out into a dedicated infra layer
    * Gives greater control
  * Sample Solutions
    * Istio
    * Linkerd
    * Consul service mesh
* Going GitOps
  * Extension of CICD where it is more transparent
  * Principles
    * Declarative Description
      * Object has entry, connections, and a sink
      * Entire state of ststem is treated as code
    * System state versioned in Git
    * Auditability
    * Integration with components
    * Configuriation drift prevention
  * Benefits:
    * Increased productivity
    * Better development experience
    * Higher stability and reliability
    * Improved security
  * Gitops tools: FluxCD, ArgoCD, Jenkins X
