# C++ Memory Management

Author: Patrice Roy, 2025

## Revisit Later

Recommendations to explore later

* [Book's Github](https://github.com/PacktPublishing/C-Plus-Plus-Memory-Management)
* [Other Resources from Packt Publishing](https://github.com/PacktPublishing/)
* C++ Standard Sections:
  * Basics: https://eel.is/c++draft/basic.memobj
* C++ High performance by Adnrist and Sehr
* Refactoring with C++ by Danilov
* Effective C++: Specific Ways to Improve Your Programs and Designs, Scott Meyers

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
* Pointer Arithmetic and why reference arithmetic isnt a thing
* Forward declarations
* Private Inheritance
* Empty base optimizations
* Move Semantics (C++11)
* Safe assignment idiom
* Memory Tagging Extensions MTEs
* CAR Hoare
* How do C++ Unions work? Active member
* Common initial sequence
* Const at various parts (function, etc)
* Why static_cast works with constexpr
* Can you derive from multiple classes? `class D : public D0, public D1 {};` pg51
* RTTI: runtime type information
* Space implications of virtual, hinted details from pg62
* RAII
* Test out the throwing from a dtor, should see crash
* thread_local, globals, static comparison
* history of auto_ptr
* Empty Base Optimization EBO
* std::void_t
* Substitution failure is not an error SFINAE
* Heap Allocation Optimization HALO
* Tag types like std::nothrow
* Placement new
* Small object optimization SOO
* OVeraligned type requirements
* Destroying delete
* Singleton design pattern
* Meyers singleton
* Static Initialization order fiasco
* Torn read and torn write in multithreaded programs
* Implicit Lifetime types

Questions

* pg 400: how can it = 0 when it is a void return type
* Talk through dynamic dispatch vs static dispatch
* sizeof(char) is 1 byte, short is 2, int is 4

Takeways

* Definition of C++ Object (pg11)
* Lifetime of Automatic, Static, and dynamic objects (ch1)
* Define and explain IFNDR, ODR, UB
* Explain casts: static_cast, dynamic_cast, const_cast, reinterpret_cast, bit_cast, duration_cast, c cast
* RAII: helps to automate actions through DTors
* When ctor'd and dtor'd: static objects, automatic objects
* Smart Pointers: unique_ptr and shared_ptr, raw pointers (pg 129/108)
* Why make_shared is a better call than shared_ptr
* Define basics of a singleton design pattern



## Notes from Chapters

### Impressions to incorporate into the review

* Accessibility
* Wide range: basics to advanced to get equal ground and build mastery
* Practical and Theoretical
* Modern tips that set a strong foundation for any level in a code base that prioritizes quality
* Well explained examples
* Break open and craft versions to understnad how fundamental concepts actually work under the hood

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
  * References
    * Reference = alias for existing entity
    * Pointers are objects( they use space, have a type and an address), but References are not objects (no storage)
    * No such thing as reference arithmetic; so references are a bit safer than pointers

Understanding the Fundamental properties of objects

* Object Lifetime
  * C++ Strength is control over lifetime of objects
  * Automatic objects are destroyed at end of scope in defined order
  * Static Objects are desticted on program termination
  * Dynamically allocated objects are destroyed when program says so
  * Pointer(automatic mobject) vs pointeee(dynamic object if declared with new)
* Object Size, Alignment, and padding
  * `sizeof` operator makes compile time non-zero object, results in number of bytes
  * Smallest unit for an object in C++ is 1 byte
  * C++ does not standardize the size of all fundamental types
  * Empty Base Optimization: if base is empy, then it gets flattened into the derived classes
  * Alignment of memory makes sure objects round up to power of 2
    * `alignof` operator yeilds natural alignment
    * `alignas` lets you control alignment of an object. can only increase, not reduce alignment
    * The order you declare in class affects memory: char, short, int takes up less than short, int, char. Each type has to line up with memory address boundary for access (int is on a 4 byte accessible address)
* Copy and movement
  * Six Member cuntions are special:
    * Default CTor
    * Dtor
    * Copy Ctor
    * Move assignment
    * Move Ctor
    * Move assignment
  * If you wrote custom for one, then either write custom for all, or do `= default` for others
  * Rule of Five
  * Copy Operators
    * Safe assignment idiom: copy and swap
  * Move operations
* Arrays
  * Array = contiguous sequence of elements of the same type
  * `std::string a1[20]`

#### 2. Things to be Careful With

Intro

* Ways that trouble forms:
  * The compiler cannot reliably diagnose the issue
  * Type casting

Different kinds of Evil

* Ill-formed, no diagnostic required IFNDR
  * Means forgram is broken
  * One definition rul ODR is example of INDR
  * Example: ODR violated, one def has differnet alignment than other in different translation units
* Undefined behavior UB
  * No idea what will happen at runtime
  * Compiler might remove UB code to make it unreachable
* Implementation-defined Behavior
  * Behavior that happens on a specific platform, but might be different on others
  * Examples: Max nested parens, max case labels in a switch, size of an object, bits in a byte, bytes in an int, char being signed or unsigned
  * Spell out your assumptions through static_asserts so it can be validated at compile time on a different platform
* Unspecified behavior (not documented)
  * "Valid but unspecified" behavior
* The ODR: One definition rule
  * One def of an object/fcn etc per translation unit, but can be declared multiple times 
* Erroneous behavior
  * UB, but Boundaries are provided to the consequences, may be introduced in Cpp26
  * Ex: Read from uninitialized variable 

Pointers

* Uses of pointer arithmetic within an array
  * If you jump out of array, UB
* Pointer interconvertibility
  * Use one pointer to point to other castable object
* Uses of pointer arithmetic within an object
  * The null pointer
    * Express it as `nullptr`
    * nullptr is not a ptr, it implicitly converts to a pointer
    * Dereference nulltpr is UB

Type Punning

* Intro
  * Subverting the languages type system
* Type Punning throuhg memebers of a union
  * Uniion = type where members are all at same address
  * Size of union is size of largets member
  * Common initial sequence
* The intptr_t and uintptr_t types
  * Aliases for int type to hold an address
* The std::memcpy function
  * Can start the lifetime of an object
* The special cases of char* unsigned char* adn std::byte*
  * Can point anywhere and alias anything
* The std::start_lifetime_as<T>() function
  * C++23
  * Take arguments and return pointer to T pointing to buffer


#### 3. Casts and cv-qualifications

Intro 

* What is a cast
  * Cast = adjust the cpmpiler's view on a type
* Safety in the type system - cv qualifications
  * `const` qualifier
    * Object is immutable in its current scope
    * Having a `int f() const {}` needs to apply const to its members, trasitively
    * "Const correct"
  * `volatile`qualifier
    * `volatile int` = object can be accessed in ways unknown to compiler. Example = drivers
    * Prevents optimizations that compiler would otherwise do
    i/O operation

The C++ Casts

* Your best friend most of the time: sttic_cast
  * Most efficient option: safe, costs nearly nothing, can be used with constexpr. Good for compile time maneuvers
  * Ex: int to float, pointer to reference from derived class to a base
  * Does not perform runtime checks
  * Ok = convert from base class to derived class, but ensure runtime is fine
  * Static_cast can change memory address accessed
* A sign something is wrong: dynamic_cast
  * Incorrect pointer conversion will be nullptr, incorrect reference conversion will throw bad_cast
  * Runtime Type Information (RTTI)
* Playing tricks withsafety: const_cast
  * Used if you need to change cv qualifiers for an expression
  * Removes  the const or volatile
  * Only works on a pointer or reference
* "Believe me compiler": reinterpret_cast
  * Gives ability o cast a pointer of some type to a pointer of unrelated type
  * Only changes the type associated with an expression
* I know the bits are right: bit_cast
  * C++20
  * Copy bits of one object to another of the same width
* duration_cast
  * Added in C++11
  * Used for microbenchmarking
  * Found in stD::chrono library
  *Convert between expressions of different measurement units
* The reviled one: c_cast

### Part 2: Implicit Memory Management Techniques

#### 4. Using Destructors

Intro

* "The most beautiful instruction in C++ is }" oof
* Dtors recap
  * Typically `X::~X()`
  * When running delete, the pointee is destroyed followed by deallocation of memory block
  * Be sure to mark as virtual to call the right destructor (good example pg 62)

Managing Resources

* Almost any function could throw (only those with `noexcept` won't)
  * We want code to be exception safe, and exception neutral (no leaks, and don't hide the exception)
* Exception Handling...or not
  * Requirements for throwing an exception are different than handling an exception
  * Best practice is to automate handling exceptions

RAII Idiom

* RAII = Resource Acquisition is initialization
* Objects acquire resources at construction, and release resources at the end of the lifetime. More to do with Dtors than ctors
* Using scope to automate actions
* RAII and C++'s special member functions

Pitfalls

* Dtors should not throw, bad idea to do so
  * Ctors CAN and should throw
  * Dtors are implicitly `noexcept`, will call an `std::terminate`
* Know destruction order
  * Generally things are dtor'd in reverse construction order
  * More complicated with non-automatic objects
    * Static objects: constructed when fccn is called for first time, dtored until whole program ends
    * Global objects are destroyed in reverse order of construction, but construction might be tricky
    * Example pg 70
      * Class's static ctored first
      * Then Globals Ctor'd next

Standard Resource Management and Automation Tools

* unique_ptr<T> and shared_ptr<T>
  * Smart pointer types
  * unique_ptr
    * uncopiable
    * destroys the pointee at the end of the lifetime
    * Calls delete on the pointer it manages
    * Default unique_ptr represents an empty object, works like a nullptr
    * Expresses exclusive ownership of a resource
  * shared_ptr
    * Shared ownership of resource
    * The last co-owner is in charge of freeing the object
    * Default shared pointer is an empty object
* lock_guard and scoped_lock
  * Autmates locking and unloakcing the mutex
* stream objects
  * iostream and fstream have good dtors that close streams
* vector<T> and other containers
  * Using vector is safer and faster than dynamically allocated arrays


#### 5. Using Standard Smart Pointers

Intro

* Advise against using raw pointers
* auto_ptr used to exist and has been removed
* Standard Smart Pointers
  * With raw pointers, we cannot tell who is responsible for pointer and pointee. Does not give clear ownership info
* Exposition of intent through function signatures
  * Owning a pointee is not the same thing as sharing a pointee
  * Function signatures convey meaning

Type unique_ptr

* Handling Objects
  * Unique_ptr object is Non-copyable
  * Can't do pointer arithmetic on unique_ptr
  * Size of unique_ptr is the size of the object'pointer it is pointing to
* Handling Arrays
  * Unique+ptr has a specialization for arrays
* Custom Deleters
  * Unique_ptr will not work inherently with private or protected fcns
  * UP can take a custom deleter unique_ptr<T, D>, D might need to be a friend of T
* make_unique
  * Factory function that forwards its arguments to ctor of T, allocates and contructs T
  * Serves as a security feature to avoid exposing ownerless resources
* Most of the time, unique_ptr is your best bet as a smart pointer
  * It is small

Type shared_ptr and weak_ptr

* When unique_ptr is not the best choice
  * Shared wnership is needed 
  * Last owner of the resource is not known ahead of time
  * Concurrent code
* shared_ptr attributes 
  * copy ctor(shares resource and ++ the counter),
  * copy assignment (decrements cunter), and
  * dtor (decrement counter, and destroy if counter is now zero)
* Usefullness and costs
  * Size of shared_ptr is greater than size of unique_pointer
  * shared_ptr is not cheap, maintaining the counter requires synchronization
  * Two allocations (one for object, and one for counter)
  * Less efficient
* make_shared()
  * Can alleviate allocation costs
* weak_ptr
  * narrower niche than shared_ptr
  * Temporary ownership
  * Doesnt own resource until you call lock on it
  * Can be used to break cycles if shared_ptr objects refer to each other

When to use raw ptrs

* Only in controlled situations
* Function needs to be an observer, not owner of the type
* Neede for low level interfaces like system calls

#### 6. Writing Smart Pointers

Intro

* Ownership Semantics
  * Smart pointers are all about clarifying ownership over indirectly accessed resources
  * Great table to reference on pg 129

Writing your own unique_ptr

* Type Signature
  * Type, and deleter are input parameters
  * 2 types: scalar and array unique_ptr
  * Deleters should be stateless and use EBO Empty base optimization
* Special Member Functions
* Pointer-like functions
  * different for scalar and array cases

Writing your own shared_ptr

* Details
  * Harder because it has two responsibilities: co-owning, and counter management
  * Synchronization is required to avoid a data race
* Make_shared
  * Instead of `std::shared_ptr<X>p{new X {}}`, do `auto p = std::make_shared<X>`
  * Make_shared will allocate bot hthe object and counter in same allocation of memory, puts them both on the same cache line

Writing a policy-based duplicating pointer

* Detection through interfaces
* Detection through traits
* Detection through concepts

Some not-so-smart but useful smart pointers

* non_null_ptr type
* observer_ptr type

### Part 3: Taking Control of Memory Management Mechanisms

#### 7. Overloading Memory Allocation Operators

Intro

* Why overload allocation functions?
  * There are generic solutions, and specific solutions out there
* Overview of X language allocation functions
  * malloc, free, calloc, realloc, etc
  * `malloc(size_t n)`details
    * Finds location where at least n consecutive bytes are available
    * Returns an abstract pointer to beginning of the memory
  * `free(void *p)` details
    * Ensure memory pointed by p becomes available
    * UB to use free on memory that did not originate from malloc

Overview of C++ Allocation Operators

* Four general options: new, new[]. delete, and delete[]
  * If you overload one, you should overload all four
  * Errors manifest as `std::bad_alloc`
* Global allocation operators
  * new does not create objects; it finds locations where object will be constructed. The ctor turns that into an object
    * 1. Allocate space
    * 2. Construct object at that location
  * Delete and delete[] take void* as argument
    * Operator deletes Cannot destroy object: instead destroys pointed to obj, then free the memory
      * 1. p->~X()
      * 2. operator delete(p)
    * There are size operator ones available too
* Non throwing versions of allocation operators
  * Provide additional argument `const std::nothrow_t&)` to operator new
  * This would return nullptr instead of exception
  * std::nothrow is a tag type
* Operator new placement new
  * Placement allocation functions = placement new
* Member versions of the allocation operators
  * Overloaded operators will be inherited by derived classes
* Alignment aware versions of the allocation operators
  * Overaligned type requirements (C++17)
  * Some types have stricter alignment constraints than others
  * To fix, add additional parameter to `operator new (std::size_t n, std::align_val_t a1)`
* Destroying Delete

#### 8. Writing a Naiive Leak Detector

Intro

Implementation Tips

* Plan Details
  * Use overloaded global forms of memory allocation operators
  * Those need to share some state
  * Would need to use a global variable
  * Singleton = class where there is only one instance in the program
    * Difficult to test and mock
    * Requires synchronization
    * Reason for problems is shared mutable state that is globlally accessible throug the program
    * For delete to work, it stores the size as first byte, then the rest of the bytes
* Meyers Singleton
  * Tries to avoid the static initialization order fiasco
  * When you have multiple TUs, you cant know from the source code which order the globals will be constructed
  * Resolved by declaring a singleton object as static local variabl
* Implementing te new and new[] operators
* Implementing the delete and delete[] operators

#### 9. Atypical Allocation Mechanisms

Intro

Placement new and memory mapped hardware

Simplifying the nowthros new usage

Out of memory situations and new_handler

Standard C++ and Exotic Memory

#### 10. Arena-Based Memory Management and Other Optimizations

Intro

Arena Based Memory Management

When parameters change

Chunked pools

#### 11. Deferred Reclamation

Intro

Reclamation without finalization at the end of the program

Reclamation and finalization at the end of the program

Reclamation and finalization at the end of scope

### Part 4: Writing Generic Containers

#### 12. Writing Generic Containers with explicit Memory Management

Intro

Writing own vector

Writing own forward_list

Better Memory Management

* More efficient vector
* Low level standard facilities
* Const or reference members and std::launder

#### 13. Writing Generic Containers with Implicit Memory Management

Intro 

Why explicit memory management complicates our implementation

Implicit memory management with a smart pointer

Consequences of this redesign

Generalizing to ForwardList<T>

#### 14. Writing Generic Containers  with Allocator Support

Intro

* Why Allocators

Traditional Allocators

Polymorphic Memory Resource Allocators

#### 15. Contemporary Issues

Starting object lifetime without constructors

Trivial Relocation

Type-Aware Allocation and Deallocation Functions
