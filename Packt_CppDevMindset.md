# The C++ Programmer's Mindset

Author: Sam Morley

Learn Computational, Algorithmic, and Systems thinking to become a better C++ Programmer

## Metadata

### Revisit Later

- SFINAE

### Links/References

- Chandler Carruth Going Nowhere Fast (<https://youtu.be/2EWejmkKlxs?si=diXN9>
4gO9X0JfUM)

### Notes for Review

- Very well organized, that is in general for packt
- A little bit too much on "this is problem solving, here are games about problem solving"
- Beginner, bite sized, back to basics of general high level programming
- More overlap in redundancy in chapters, which means jumping to them isnt a bad idea
- First section is big picture; hardware, machine details, operating system level. Good foundation to build off of since C++ has so many utilities to optimize based on that low-level
- Intersection with Hpca

### Questions

## Notes By Chapter

### Ch 1: Preface and Thinking Computationally

- When performance is paramount, C++ is the obvious choice: you only pay for what you use, has a lot of libraries and options, provides immense control, with flexibility and ease of use
- Goal = Interplay of C++ lang, features, and general computational thinking
- Code bundle link: <https://github.com/PacktPublishing/The-CPP-Programmers-Mindset>
- Components of Computational Thinking
  - Problem has constraints and parameters that are well defined
  - 4 Components
    - Decomposition
    - Abstraction
    - Pattern Recognition
    - Algorithm Design
- Decomposing Problems
  - General Strategies
    - Trial and Error
    - Look at high level components
- Building abstractions and recognizing common patterns
  - Abstractions
  - Identify commonalities in the data
  - Common functional patterns
  - Common structural patterns
- Understanding Algorithms
  - Preconditions and postconditions
  - Characteristics of an algo
    - Finite
    - Definite
    - Inputs and outputs
    - Effective
- Using modern C++ and good practice
  - CMake
  - string_view and span
  - range: xposes a beginning and end, composed with views
  - Templates and concepts
    - Concepts reduce needs o compiler by extracting template params up front
    - Concepts are compil etime constructible
  - Error handling
    - Exceptions
    - C style
    - expected
  - Testing code: unit, integration, and end to end
    - Google test and catch2

### Ch 2: Abstraction in Details

62-86

- Common categories of problems
  - Types
    - Cominatorial
    - IO
      - Serialization
    - Numerical
    - Interface
  - C++ connection
- Understanding standard algorithms
  - Categories of algorithms
    - Search
    - Copy
    - Transformation
    - Permutation
    - Storing and partitioning
    - Binary Searching
    - Generating
- When to use functions
  - Function like objects, lambdas
- When to use classes
  - Polymorphism, comes with runtime cost
  - Object oriented
  - Templates
  - Traits

### Ch 3: Algorithmic thinking and Complexity

86-108

- Understanding Algorithms
  - Proof By Induction
- Computing Complexity
  - Complexity, and amortized
- Designing your own algorithms
  - Iterative, recursive, divide and conquer, graphs, optimization, gradient descent, DP, randomized
- Requirements and Considerations
  - Cache aware algorithms
  - Vectorized operations, SIMD
  - Branch prediction

### Ch 4: Understanding the Machine

108-144

- Understanding modern processor design
  - Components
    - aLU = basic logic, operates on registers
    - Registers obtain data from memory
    - MMU = memory management unit
    - Instruction decoder
    - Cache memory
    - Floating point unit
    - PCI bus
  - Instruction architectures
    - ISA, ARM, RISC
    - CPUID
  - Processor threads
- Storage Spectrum
  - RAM
  - Registers: holds integer or fp value
  - Cache memory
  - Cache lines
  - Query processor for cache size
  - Main memory
  - Dual in-line memory models, CAS latenc
- SIMD
  - SIMD = single instruction multiple data extensions
  - Function versioning
  - Memory alignment
  - Aliasing
- Branch prediction and speculative execution
  - Speculation based vulnerabilities
- OS
  - Kernel Mode
  - VM, divided into pages
  - TLB, thrashing, transparent huge pages
  - Interacting with the Scheduler
    - CPU affinity

### Ch 5: Data Structures

144-170

- Computer memory, pointers, indirection
  - Memory is stack and heap, stack frames, head of stack lives in low level cache
  - RAII automates memory management
  - Infinite Precision Integers
  - Arrays
  - Structured memory
  - Allocation and allocators
  - Smart Pointers
    - Object that holds a pointer to another object and manages its lifetime
    - unique_ptr,shared_ptr, weak references
- Linear memory, vectors, stacks, queues
  - Structure of arrays vs array of structures
  - Stacks and queues
  - Vectors
  - Static vectors
  - Small vectors
  - Views and Spans, management agnostic views into a block of linear data
- Linked lists
  - Stable vectors; hybrid between a linked list and standard vector
- Maps and sets
  - Flat map and flat sets: set that is implemented in a vector. Added in c++23
  - Hash functions
  - Hashsets and hash maps; handle collisions; load factor, rehash
  - Map benchmarks

### Ch 6: Reusing your code and modularity

170-188

### Ch 7: Outlining the challenge

188-200

### Ch 8: Building a simple command line interface

200-216

### Ch 9: Reading Data from Different Formats

216

### Ch 10: Finding information in text

### Ch 11: Clustering Data

### Ch 12: Reflecting on What we have Built

### Ch 13: The Problems of Scale

### Ch 14: Dealing with GPUs and Specialized Hardware

330

### Ch 15: Profiling your Code

356
