# The Pragmatic Programmer: From Journeyman to Master

Authors: Andrew Hunt and David Thomas, 1999

## Revisit Later

* Pg 15 list of ways to stay current
* "Dinosaur Brains" = book recommendation
* Singleton pattern
  * Design Patterns [GHJv95]
* Unix Philosophy
* Shell Games! pg 79
  * Ask GPT for fun exercises/prompts for mastering the shell
* Gnu General Publisher's License
* Cygwin
* Active and Passive Code Generators
* Is javas final keyword similar to cpps const?
* "More Effective C++" Mey 1996
* "Large Scale C++ Software Design" by John Lakos
* UML Activity Diagram


Discuss with butler:

* Tracer Code vs prototype
* Orthogonality
* Like to tell stories, any interesting ones he has for how we are here?

Discuss with James

* How is your VSCode set up, bc I am always FRUSTRATED
* My prefered drama: tech issues and pros/cons that are measurable but conflicts prioritization

## Intro

Forward

* Quality without a name
* SW does not have "laws"

Preface

* Characteristics of a Pragmatic Programmer
  * Early/Fast Adopter: Love trying things out. Confidence born of exptertise.
  * Inquisitive
  * Critical Thinker
  * Realistic
  * Jack of all trades
  * **T1: Care about your craft**
  * **T2 Think about your work**
* Kaizen: Continuous Learning

## 1. A Pragmatic Philosophy

* Pragmatic Programmer = aware of the bigger picture, make intelligent comprimises and informed decisions
  * Take responsibility in everything they do
* The Cat Ate my Source Code
  * "The greatest of all weaknesses is the fear of appearing weak"-JB Bousset
  * You have the right not to take on a responsibility for an impossible situation or where the risks are too great.
  * By accepting responsibility for an outcome, you're held accountable for it.
  * Its up to the programmer to provide solutions, not excuses.
  * **T3 Provide Options, Don't make lame excuses**
* Software Economy
  * **T4 Don't live with broken windows**
  * Broken window theory: broken window = small things lead to bigger problems
* Stone Soup and Boiled Frogs
  * Soldiers were catalyst to bring the group together
  * "Start up fatigue" = guarding resources
  * People find it easier to join a an ongoing success
  * **T5: be a catalyst for change**
  * Gentle and gradual deception
  * **T6: Remember the big picture**
  * Take time to look around to view the bigger picture before it's too late (frog soup)
* Good Enough Software
  * Software is often better in shorter incubation
  * Involve users in the trade off process
  * **T7: Make Quality a Requirements Issue**
  * Rough edges today can be better than waiting a year with nothing good in the meantime
  * Know When to stop: from an artists perspective
* Your Knowledge Portfolio
  * Knowledge is an expring asset: it gets out of date quickly
  * Invest in your knowledge regularly, diversify it, manage risk (dont put all your eggs in one basket), rebalance regularly (the industry changes rapidly)
  * **T8: Invest regularly in your knowledge portfolio**
  * Pg 15 has recommendations on staying current
  * When you can't answer a question, find someone who can, and learn from them
  * **T9: Critically Analyze what you read and hear**
  * "Care and cultivation of gurus" = man a lot of this is easier now with Chat GPT, but you HAVE to apply the critical thinking lense to it
* Communicate
  * "A good idea is an orphan without effective communication"
  * Ideas for effective communication
    * Know what to say
    * Know your audience
    * Choose your moment
    * Choose a style (just the facts)
    * Make it look good
    * Involve your audience
    * Be a listener
    * Get back to people
    * **T10: Its both what you say and the way you say it**

## 2. A Pragmatic Approach

* The Evils of Duplicaion
  * **Tip 11** DRY Principle: Don't repeat yourself
  * How does duplication arise?
    * Imposed Duplication: "no choice" for developers
      * Multiple Representations of info
      * Documentation in the code
      * Documentation and code
      * Language issues (C++)
    * Inadvertent Duplication: Devs don't realize they're duplicating
      * Mistakes in the design
      * Localize the impact: minimize the duplication
    * Impatient Duplication: Devs get lazy because it seems easier
      * "Short Cuts make for long delays"
      * Example: Y2k
    * Interdeveloper Duplication: People on a team duplicate a piece of info
      * Functionality may be duplicated across sections of a large project
      * Example: 10,000 programs to validate SSNs in the gov
      * Encourae active and frequent communication between devs
      * Facilitate an exchange of knowledge
      * **T12** Make it easy to reuse
* Orthogonality
  * Ortho = independence, decoupling
  * Benefits of Orthogonality
    * **T13** Eliminate Effects between unrelated things
    * Nonorthogonal systems are inherently more complex to change and control
    * Benefit: Gain Productivity
      * Promotes reuse
      * Small functions have small focuses
    * Benefit: Reduce Risk
      * Easier to cut and transplant new code of irrelevant sections
      * Resulting system is less fragile
      * Can test it better
      * Not tightly tied to a vendor or product or platform
    * Project Teams
      * Overlap of responsibilities is confusing
    * Design
      * Layer Diagram
      * If you change one thing, how many things need updates too
    * Toolkits and Libraries
      * Does a toolkit impose changes that shouldn't be there?
    * Coding with Orthogonality
      * Keep your code decoupled, write shy code that doesnt reveal too much and doesn't ask much of other components
      * Avoid Global Data: Use a singleton pattern
      * Avoid Similar Functions: Design patterns might be better
      * Be constantly critical of your code
    * Testing
      * Ortho helps with unit tests
    * Documentation
    * Living with Ortho
      * Systems are more flexible, easier to test
* Reversibility
  * Reversing decisions around critical components of your application are costly, especially late in a program
  * Ortho helps in these cases
  * **T14** There are no final decisions
  * Schroedinger's cat: the target will always be changing
* Tracer Bullets
  * In ambiguous requirements, Specifying to death is not good
  * **T15:** Use Tracer bullets to find the target. AKA Build something quick to get closer to final target
  * Tracer bullets don't always hit the target, you only see where they are headed. Thus, you still need to aim.
  * Is NOT prototyping. Prototype implies throw-away, tracer implies foundational
* Prototypes and Post-it Notes
  * Prototypes don't need to be code; can be thrown away
  * **T16** Prototype to learn
  * Prototypes can ignore:
    * Correctness
    * Completeness
    * Robustness
    * Style
  * Caveat: Make sure everyone knows its disposable
* Domain Languages
  * **T17**: Program close to the problem domain
* Estimating
  * **T18:** Estimate to avoid surprises
  * How Accurate is needed?
    * Ask what context will the estimate be used in
    * LOL: 1897 Indiana tried to rule that Pi should be 3; mathmaticians called them out
    * Units matter too: 130 days sounds precise, "around 6 months" has wiggle room
  * Draw on others experience before solidifying estimates
  * Think about scope before making a guess
  * Build a model, break it into components, identify parameters, set sample values, justify how you calculate each
  * Reflect on how on or off your estimates were
  * **T19:** Iterate the schedule with the Code
  * When asked for an estimate, say "I'll get back to you"

## 3. The Basic Tools

* Intro
  * Tools amplify your talent
* Plain Text
  * **T20:** Keep Knowledge in Plain Text
  * Human Readable files will outlive binaries
  * All software becomes legacy as soon as its written
  * Unix Philosophy, centered around plain text
  * All parties should communicate in a common standard, and plain text can be that
* Shell Games
  * **T21**: Use the power of command shells
  * Cygwin
* Power Editing
  * **T22** Use a single editor well
  * Reduce the number of keystrokes you need to do things
* Source Code Control
  * **T23:** Always use Source Control
  * Helps builds be automatice and repeatable
* Debugging
  * Can be sensitive, emotional
  * **T24:** Fix the problem, not the blame
  * **T25:** Don't Panic
  * DDD Debugger
  * **T26**: The OS probably isnt broken. If you see hoofprintes, think horses not zebras
  * **T27**: Don't assume it, prove it
  * Debugging Checklist pg 98
* Text Manipulation
  * **T28:** Learn a text manipulation language
* Code Generators
  * **T29:** Write code that writes code
  * Active and Passive

## 4. Pragmatic Paranoia

* Intro
  * **T30:** You can't write perfect software
  * Code defensively (similar to driving defensively)
  * Validate all Info we are given
  * Don't trust yourself either
  * Design by contract: clients and suppliers must agree on rights and responsibilities
* Design by Contract (DBC)
  * Defines your rights and responsibilities
  * Repercussions if eitehr party fails the contract
  * Preconditions
  * Postconditions
  * Class Invariants
  * **T31:** Design with Contracts
  * Assertions
    * Downside: not prpopgated to children
* Dead Programs tell no lies
  * **T32** Crash Early
  * A dead program does less damage than a crippled one
* Assertive Programming
  * **T33**: If it can't happen, use assertions to ensure it won't happen
  * Don't turn off asserts in production code
* When to use Exceptions
  * **T34:** Use Exceptions for exceptional problems
  * Java has a "Remote Method Invocation" facility
* How to balance Resources
  * **T35:**: Finish what you Start
  * Similarities to Ctor and Dtor

## 5. Bend, or Break

* Intro
  * Adaptability to Life's changes
  * Write less code to stay most flexible
  * Metaprogramming
* Decoupling and the Law of Demeter
  * Isolation between services is a good thing
  * Unecessary coupling leads to fear when a code change happens
  * **T36**: Minimize Coupling between Modules
* Metaprogramming
  * **T37:** Configure, don't integrate
  * Metadata is accessed and used at runtime not compile time
  * **T38:** Put abstractions in the code, details in the Metadata
  * Program for the general case, put the specifics elsewhere
* Temporal Decoupling
  * Concurrency
  * **T39:** Analyze workflow to improve concurrency 
  * **T40**: Design using services: independent concurrent objects behind well-defined, consistent interfaces
  * **T41**: Always design for concurrency
* It's Just a View
  * A good definition of a module is that it has a single well-defined responsibility
  * Events: can be used to minimize coupling between objects
  * Publish/subscribe protocol
  * **T42** Separate Views from Modules
  * Model View Controller review
* Blackboards
  * **T43**: Use blackboards to coordinate workflow

## 6. While you are Coding

* Intro
* Programming by Coincidence
  * False conclusions can lead to disaster
  * Program Deliberately
  * Undocumented behavior may change with a future release
  * Don't code blindfolded
  * Make Plans
  * Rely only on reliable things
  * Document your assumptions. Test your assumptions
  * Don't be a slave to history
  * **T44:** Don't program by coincidence
* Algorithm Speed
  * Estimate your resources (speed, memory, etc)
  * Big O notation
  * Common Sense estimation
  * **T45:** Estimate the order of your algorithms (like the magnitude)
  * Use code profilers to count how many times steps get executed
  * Fastest might not always be best. There are tradeoffs
  * **T46:** Test your estimates
* Refactoring
  * **T47:** Refactor early, refactor often
  * SW is gardening: it is organic. Some decisions thrive, others are compost
  * Reasons to refactor: Duplication, Nonorthogonal design, Outdated knowledge, and performance.
  * 
* Code that's easy to test
  * **T48:** Design to test
  * **T49:** Test your software or your users will
* Evil Wizards
  * **T50:** Don't use wizard code you don't understand

## 7. Before the Project

* Intro
* The Requirements Pit
  * **T51:** Don't gather requirements, dig for them
  * **T52:** Work with a user to think like a user
  * **T53:** Abstractions live longer thna details
  * **T54:** Use a project Glossary
* Solving Impossible Puzzles
  * **T55:** Don't think outside the box, find the box
* Not until you're ready
  * **T56:** Listen to nagging doubts: start when you're ready
* The Specification trap
  * **T57:** Some things are better done than described
* Circles and Arrows
  * **T58:** Don't be a slave to formal methods
  * **T59:** Expensive tools do not produce better designs

## 8. Pragmatic Projects

* Intro
* Pragmatic Teams
  * **T60**: Organize around functionality, not job functions
* Ubiquitous Automation
  * **T61** Don't use manual procedures
* Ruthless Testing
  * **T62**: Test Early. Test Often. Test Automatically
  * **T63**: Coding aint done till all the tests runtime
  * **T64:** Use sabeteurs to test your Testing
  * **T65**: Test state coverage, not code coverage
  * **T66**: Find bugs once
* It's all Writing
  * **T67**: Treat English as another programming language
  * **T68**: Build Documentation in, dont bolt it once
* Great Expectations
  * **T69**: Gently exceed your users expectations
* Pride and Prejudice
  * **T70**: Sign your work

## Resources
