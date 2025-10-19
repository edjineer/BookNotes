# C++ Memory Management

Author: Patrice Roy, 2025

## Revisit Later

Recommendations to explore later

* [Book's Github](https://github.com/PacktPublishing/C-Plus-Plus-Memory-Management)
* [Other Resources from Packt Publishing](https://github.com/PacktPublishing/)
* C++ Standard Sections:
  * Basics: https://eel.is/c++draft/basic.memobj

Topics to experiment with

* override, virtual, abstract classes
* dynamic dispatch vs static dispatch
* Type traits and/or concepts
  * When are true_type nad false_type actually useful
* Type aliases
* typename keyword
* Differences in use between decltype and auto
* Deep dive into qualifiers and/or value categories
* Reference collapsing
* Magic statics

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
    * Example of an object, parens not required: `int n; auto s1 = sizeof n;
* Assertions
  * Dynamic assertions= info known at runtime
    * Can use cassert's `assert()`
    * Most people disable assert from production code
    * NDEBUG macro before compilation
    * Assert is a library macro
  * Static Assertions: info known at compile time, like "this system has a 4 byte int
    * `static_assert` is a language feature, prevents compilation if a condition isn't met
    * Has no runtime cost, documents our asserts in a verifiable manner, no downsides
* UB
  * Means its not portable between platforms, unpredictable or bad behavior, etc
* Type Traits
  * Examples: const, trivially copyable
  * `type_traits` header is useful
    * `std::is_const<T>`
    * `std::remove_const<T>
    * Since std C++14, traits that yield type have aliases that end with _t
  * Concepts are related, but different from type traits
* std::true_type and std::false_type
  * Included from the <type_traits> header
* std::conditional<B,T,F> trait
  * Select one of two types based on a compile-time boolean condition
  * `std::conditional<B,T,F>::type
  * B=boolean condition, T=type to use if B is true, F=type to use if B is false, resulting type
  * Used in template metaprogramming to select types based on compile time conditions
  * Type aliases
    * Pre-C++14 = `std::conditional<B, T, F>::type`
    * Post 14: can do `std::conditional_t<B, T, F>`
  * Typename keyword
    * Used to indicate a dependent name in a template is a type, helps compiler distinguish types and non-types
* Algorithms
  * Std library comes with plenty
  * `std::copy`
  * [begin and end) are half open range
  * <ranges> library introduced in C++20
* Functors and Lambdas
  * Functor = function object, represent stateful computations
  * Lambda expressions are functors that limit themselves to a ctor and operator() member function
    * `[capture_list](parameters)-> -> return type{function body}`
    * Capture list is what variables does it have access to
      * [] = no variables captured (stateless lambda)
      * [=] capture all variables by value (example of a stateful lambda)
      * [&] capture all variables by reference
    * return type is optional; compiler can figure it out
  * Good example in algorithms library: `std::for_each(begin, end, func)`: lambda is func
* Friends
  * Full access to all of the members including protected or private
  * Better than exposing data as public, but does break encapsulation a little bit
  * Friendship is not reflexive or transitive or inherited
* Decltype
  * `auto` is one option for type detection, introduced in C++11. Does not keep qualifiers or references unless explicitly specified 
  * `decltype also introduced in C++11
  * Deduces the type of an expression at compile time, includes const, ref, rvals, etc
  * `int x = 42; int& ref = x; decltype(ref) y = x;`
* Perfect Forwarding
  * Templates introduced in C++11
  * Forwarding references: `std::forward<t>` from the utility library, behaves as a cast
    * Can bind both lvals and rvals, declared using T&&, T is deduced template parameter
    * Reference collapsing applies: T&&->T&, etc
  * Perfect forwarding allows teplate to forward its arguments exactly as passed in, preserves value category and qualifiers (lval, const, ). Achieved using std::forward and forwarding references
  * Useful for wrapper functions, emplacement in containers (used in emplace_back fcn)
* Singleton Design Pattern
  * Generally not well-liked pattern since testing is difficult, dependencies on global state, single point of failure in program, complicates multithreading
  * Instantiation at Program Startup
    * Instantiate a singleton by creating before main
    * Declare it separate from defining it (avoid ODR problems)
  * Instantiation of the first call
    * static can help too
    * Maigc statics: statics that are local ot functions. C++ guarantees only constructed once
* Std::Exchange
  * Hidden in utility library
  * `std::swap`: swaps values 
  * `a = std::exchange(b,c)`: puts value of c into b, and retains b's old value in a 

### Part 1: Memory in C++

#### 1. Objects, Pointers and References

* Recommendation to start at "Things You Should Know" in Annex (pg 24)
* Representation of Memory in C++
  * Memory = one or more sequences of contiguous bytes
  * Every byte has unique address
  * Byte needs to be wide enough for literal encoding of any element and the 8-bit code units of UTF-8, contiguous sequence of bits. At least 8 bits, but coudl be more
  * Byte is intended to be smallest addressable unit of memory in a program
  * Objects
    * Defining an Object:
      * How is an object created explicitly and implicitly
      * It has an address and occupies non-zero space
      * Properties: name, type, storage duration, etc
    * Functions are not objects
    * <type_traits> library has std::`is_object_v` to say whether something is an object, neat! 
      * Works as either is_object_v, or is_object<int>::value
  * Pointers
    * Definition: A typed address
    * The pointer itself is an object
    * To initialize to nullptr, you can `int * p = 0; int * p = nullptr`
    * Don't do pointer arithmetic, it's just silly
    * Special Types for pointer manipulation
      * `void*`: A "Generic Pointer", or address with no associated type. All ptrs implicitlyconvert to void *. Used in C 
      * `char*`: pointer to a byte, can be anything in memory
      * `std::byte*`: new pointer to a byte since C++17, a replacement for char* with a better name

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
