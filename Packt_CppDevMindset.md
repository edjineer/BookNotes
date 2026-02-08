# The C++ Programmer's Mindset

Author: Sam Morley

Learn Computational, Algorithmic, and Systems thinking to become a better C++ Programmer

## Metadata

### Revisit Later

- SFINAE

### Links/References

### Notes for Review

- Very well organized, that is in general for packt
- A little bit too much on "this is problem solving, here are games about problem solving"
- Beginner, bite sized, back to basics of general high level programming
-
-

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

### Ch 5: Data Structures

### Ch 6: Reusing your code and modularity

170

### Ch 7: Outlining the challenge

188

### Ch 8: Building a simple command line interface

200

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
