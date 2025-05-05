# Clean Code

By Robert C Martin, 2009

## Look Up Later

* Jar, war, ear files
* Additional Authors per chapter
* Practice classifying Object Oriented vs Procedural Code
* Kent Beck: four rules of Simple Design
* 

## Book Club Chapters

### Chapter 2: Meaningful Names

Discussion Questions

* pg 25, use static factory methods
* is pg 29 actually better?
* any horror stories or worst nams youve seen around? im guilty of mpromethius misspelling
* Tim Ottinger as the author

Notes

* Use intention-revealing names
  * Takes time but saves even more time
  * Address why it exists, what it does, how it is used
  * If a name requires a comment, then it is not named correctly
  * Problems with implicity of the code
* Avoid Disinformation
  * Avoid words that mean different things in diferent contexts
  * Don't encode container type into a name
  * Be aware of name shapes that are similar length and look alike
* Make meaningful distinctions
  * Don't change spellings just to make something compile
  * Noise words or filler shouldnt go in names
  * No need for "SomethingStr" when it is obviously a string
* Use pronouncable names
* Use searchable names
* Avoid encodings
* Avoid mental mapping
  * Clarity is king
* Names
  * Class names should be nouns
  * Methods should be verbs
* Don't be cute
  * Say what you mean, mean what you say
* Pick one word per concept
  * Don't do fetch, retrieve, get 
* Don't pun
* Use Solution Domain Names
* Don't add Gratuitous Context

### Chapter 7: Error Handling

Discussion Questions

* Michael Feathers authored this section? Many sections had different authors, neat!
* Does C++ and python still not have checked exceptions? pg 106
* Open/Closed Principle violation
* Example of unchecked exception
* Special Case Pattern: agree? Disagree? Meh?

Notes

* Intro
  * If error handling obscures logi, it is wrong
* Use exceptions rather than return codes
* Write your try-catch-finally first
  * Write tests that test the exceptions
* Use unchecked exceptions
  * NEED AN EXAMPLE OF this and explanation
* Provide context with exceptions
  * Give at least source and location of the error
  * Nice to have logs and detailed error messages
* Define exception classes in terms of a caller's needs
  * Classify your errors
  * Best practice: wrap your 3rd party API calls: then you minimize your dependencies on it
* Define the normal flow
  * Separate your error handling from business logic
  * Fowler's Special Case Pattern
* Don't return null
* Don't pass null

### Chapter 6: Objects and Data Structures

Discussion Topics

* Pg 95, do you agree that the 6-4 is preferable? When would that change?
* Pros and Cons of getters and setters
* Reinforce the Difference between an object and a DS
* Procedural Code = code using data structures vs OO Code, classify which for cases
* When creating a new class or abstraction, when would you lean towards a more OO approach, and when would you use procedural? Is there space in a code base for both?
* History of Law of Demeter in CS
* Law of Demeter in our code base; im guilty of doing this before, how bad is it actually?
* Train Wreck
* Pg 99: beans?, pg 100 example explained

Notes

* Listing as a point
  * Implies cartesian x,y from variable names
  * Class = allows users to manipulate the essence of the data
  * Argues that abstraction is better than getters/setters
* Data/Object Anti-Symmetry
  * Objects hide their data behind abstractions and expose functions that operate on that data (Shape, Duck)
  * Data Structures Expose their data, have no meaningful functions (List, map, vector)
  * Object-Oriented/Polymorphic Approach: if you add a new function, all instances need updating. If you add a new shape, nothing needs updating.
  * Procedural Code = DS Oriented, makes it easy to add functions but hard to add new classes
  * OO Code = Object, easy to add new classes, hard to add new functions
* Law of Demeter
  * A module should not know about the innards of the object it manipulates
  * Don't invoke methods on objects returned by allowed functions
  * Train Wreck
  * Hybrids = Make it hard for both
* Data Transfer Objects
  * Data structure distilled
  * Useful for DBs, sockets
  * Used to translate raw data into an object
* Activate Record
  * DSs with public variables, but also safe and find navigate methods

### Chapter 10: Classes

Discussion Topics

* Jeff Langr is author, what is his background
  * Cpp with test driven development, Clean Agil, Java
* Private Utilities used by public function
* Agree with "Classes should be small?"
* I think its more inconveneint to have to hunt through dozens of files when it could be in one class
* Maximal Cohesion
* "Literate Programming" by Knuth
* SOAP Service
* Dependency Inversion Principle

Notes

* Class Organization
  * Begin a class with its variables (public ten private), functions(public then private)
  * Encapsulation
    * Sometimes loosened for testing, but don't push much further than that
* Classes Should be Small
  * Measured by responsibilities
  * Name should be what responsibilities it fills
  * Words like PRocessor or Manager hint at aggregation of too many responsibilities
  * Single Responsibility Principle
    * Class should have only one reason to change, one responsibility
    * Single most abused class design principle. Many classes do way too much
  * Cohesion
    * "Maximal Cohesion" as a concept
  * Maintaining Cohesion Results in Many Small Classes
* Organizing for Change
  * Isolating From Change
  * Dependency Inversion Principle: Classes should depend on abstractions, not concrete details

### Chapter 9: Unit Tests

Discussion Topics:

* Do we do TDD? Or is it too granular?
* Second law, no idea what he's saying
* Thoughts on single concept per test?

Notes:

* Intro
  * This chapter is written by Uncle Bob
  * In 1997 Test Driven Development was not a thing
  * Apparently people used to throw the test code away
  * Now look for nooks and crannies
  * Three Laws
    1. You may not write production code until you've written a failing unit test
    2. You may not write more of a unit test than is sufficient to fail, and not compiling is failing
    3. You may not write more production code than is sufficient to pass the currently failing test
* Keeping Tests Clean
  * "Dirty tests > no tests"
  * The dirtier the tests, the harder they are to update
  * Dirty tests lead to the whole suite being thrown out
  * Higher test coverage, the less you need to fear changes
* Clean Tests
  * What makes a clean test: readability
  * What makes a bad test: duplicate code, irrelevant details, code that is not designed to be read, domain specific testing language
* One Assert Per Test
  * Kinda a JSUnit specific thing
  * Allows for a quick conclusion to be made
  * Eh, more like asserts per test should minimized
  * Single Concept per test is a better guideline
* "FIRST"
  * Fast
  * Independent
  * Repeatable
  * Self-Validating: Boolean output
  * Timely: Written just before or right after prod code is written

### Chapter 13: Concurrency

Author: Brett Schuchert

Discussion Topics:

* I don't think the tips alone are enough; using a "sync" keyword does not enforce anything. Locks and mutexes have a higher chance to be effective
* Copies of data is not always a good idea; shared memory with locks is another option

Details:

* Intro
  * Clean concurrent programs are hard
  * Concurrent programs may look clean but can break under stress
* Why Concurrency
  * Decoupling Straetegy: separate what gets done from when it gets done
  * Improves throughput and structure of applications
  * Allows processing in parallel
* Myths and misconceptions
  * "Always improves performance": no, improves more when there is a lot of wait that can be split between muptiple threads or processors
  * "Design does not chance gor concurrency"
* Challenges
* Concurrency Defense Principles
  * Single responsibility principle
    * Keep your concurrency related code separate from other code
  * Limit The Scope of Data: Protect critical sections of code
  * Take data encapsulation to heart; limit access of any data that may be shared
  * Use Copies of data
    * Avoids synchronizing
  * Threads should be independent
    * Partition data into independent subsets
* Know your Library
* Know Execution Models
  * Producer/Consumer
  * Readers/Writers
* Beware Dependencies between Synchronized Methods
  * Locking: client based, server based, adapted server
* Keep syncronized sections small
* Writing Correct Shut-Down Code is hard
  * Issues: Deadlock, zombie threads
* Testing Threaded Code
  * Write tests that expose potential problems
  * Treat Spurious Failure as Candidate Threading Issues
    * One-off problems are never actually one-off
  * Get your non-threaded code working first
  * Make it pluggable, adaptable to multiple configurations
  * Make it tunable
  * Run with more threads than processors
  * Run on different platforms
  * Instrument your code to force failures
* Options to Debug
  * Inject waits, yield, sleep, priority
  * Inject some "jiggling"

Appendix A: Concurrency II pg 317

* Client Server Example
  * Validate the throughput of your system
* Possible Paths of Execution
* Knowing your Library
  * NonBlocking Solutions
  * Dependencies between methods can break concurrent code
* Increasing Throughput
  * Mutex
  * Lock & Wait
  * No preemption
  * Circular Wait

## Bonus Chapters

### Chapter 3: Functions

Details

* Goal = Easy to read and understand
* Small
  * No bigger than a screen-full
* Do one thing
  * Do it only, do it well
* One level of abstraction per function
  * 

### Chapter 11: Systems

Author: Kevin Dean Wampler

Details

* Cities are run by many people: big picture vs details
* Construction vs Use
  * Keep in mind the Single Responsibility Principle
  * Idea: All construction in main
  * Abstract Factory
  * Dependency Injection
  * Scaling Up
    * Getting things "right the first time" is a myth
  * Test Drive the System Architecture
    * Not Necessary to do a Big Design Up Front
  * Optimize Decision Making
  * Use Standards when they add demonstrable value
  * At all levels, intetn should be clear
  * Use the simplest thing that can possibly work

### Chapter 12: Emergence

Author: Jeff Langr

Details:

* Kent Beck: four rules of Simple Design
  1. Run all the tests
      * Systems that arent testable are not verifiable
      * ...and should never be deployed
      * Tests should follow SRP
  2. Contains no duplication
      * Dupliction is enemy of a well designed system
  3. Expresses the intent of the programmer
      * Cost is long-term maintenance
      * Choose good names
      * Keep functions small
      * Just try to be expressive, explain for the next coder
  4. Minimize the number of classes and methods
      * Keep function and class counts low
