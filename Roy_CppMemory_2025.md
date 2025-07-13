# C++ Memory Management

Author: Patrice Roy, 2025

## Revisit Later

Recommendations to explore later

* [Book's Github](https://github.com/PacktPublishing/C-Plus-Plus-Memory-Management)
* [Other Resources from Packt Publishing](https://github.com/PacktPublishing/)

Topics to experiment with

* override, virtual, abstract classes
* dynamic dispatch vs static dispatch

Questions 

* pg 400: how can it = 0 when it is a void return type
* Talk through dynamic dispatch vs static dispatch
* 

## Notes from Chapters

### Impressions to incorporate into the review

* Accessibility
* Wide range: basics to advanced to get equal ground and build mastery
* Practical and Theoretical
* Modern tips that set a strong foundation for any level in a code base that prioritizes quality

### Fwd/Intro Sections

* Patrice Roy has been a part of C++ Standardization committee since 2014. Participation in SG14
* Taught computer science, has experience in military and game programming
* Reviewers = Martin Reddy, Kevin Carpenter, Faezeh Sadat Zolfaghari

### Part 1: Memory in C++

#### Objects, Pointers and References

* Recommendation to start at "Things You Should Know" in Annex (pg 24)

#### Things to be Careful With

#### Casts and cv-qualifications

### Part 2: Implicit Memory Management Techniques

#### Using Destructors

#### Using Standard Smart Pointers

#### Writing Smart Pointers

### Part 3: Taking Control of Memory Management Mechanisms

#### Overloading MEmory Allocation Operators

#### Writing a Naiive Leak Detector

#### Atypical Allocation Mechanisms

#### Arena-Based Memory Management and Other Optimizations

#### Deferred Reclamation

### Part 4: Writing Generic Containers

#### Writing Generic Containers with explicit Memory Management

#### Ditto with Implicit Memory Management

#### Ditto with Allocator Support

#### Contemporary Issues

#### Annexure

Things You Should Know

* struct and class:
  * Refresher on `virtual` keyword: allows for pure virtual functions, which lead to abstract classes. In destruction, derived class is destroyed first before base class. `virtual` ensures correct implementation at runtime
  * Refresher on `override`: ensure that it overrides a base class method. If base class has it absent, there is a compiler error 
  * `=default` for a destructor: Defaulted functions, applies typically to rule of 5 kind of functions (ctor, dtor, copy, assignment). Equivalent to `virtual ~Drawable(){}`
  * `virtual ~BaseClass()=default` virtual keyword is needed to ensure that both the DERIVED and then BASE dtors are called IF you have a pointer to the base class delete memory, avoid undefined bahavior
  * `virtual XXX name()=0` for a pure vitrual function, the virtual keyword and =0 are needed
  * For struct, inheritance and members is public by default, and class it is private by default
* size_t = unsigned integral, but actual value caries from compiler to compiler (int, long long, etc)
  * revealed by operator `sizeof`
    * size in bytes of an object or type
    * Evaluated at compile time
    * Example: `auto s0 = sizeof(int)`
    * Example of an object, parens not required: `int n; auto s1 = sizeof n;`
* Assertions
* UB
* Type Traits
* std::true_type and std::false_type
* std::conditional<B,T,F> trait
* Algorithms
* Functors and Lambdas
* Friends
* Decltype
* Perfect Forwarding
* Singleton Design Pattern
* Instantiation at Program Startup
* Instantiation of the first call
* Std::Exchange
