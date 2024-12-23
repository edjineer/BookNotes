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
* C++ ifdef __TEST__ pg 193


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
  * __T1: Care about your craft__
  * __T2 Think about your work__
* Kaizen: Continuous Learning

## 1. A Pragmatic Philosophy

* Pragmatic Programmer = aware of the bigger picture, make intelligent comprimises and informed decisions
  * Take responsibility in everything they do
* The Cat Ate my Source Code
  * "The greatest of all weaknesses is the fear of appearing weak"-JB Bousset
  * You have the right not to take on a responsibility for an impossible situation or where the risks are too great.
  * By accepting responsibility for an outcome, you're held accountable for it.
  * Its up to the programmer to provide solutions, not excuses.
  * __T3 Provide Options, Don't make lame excuses__
* Software Economy
  * __T4 Don't live with broken windows__
  * Broken window theory: broken window = small things lead to bigger problems
* Stone Soup and Boiled Frogs
  * Soldiers were catalyst to bring the group together
  * "Start up fatigue" = guarding resources
  * People find it easier to join a an ongoing success
  * __T5: be a catalyst for change__
  * Gentle and gradual deception
  * __T6: Remember the big picture__
  * Take time to look around to view the bigger picture before it's too late (frog soup)
* Good Enough Software
  * Software is often better in shorter incubation
  * Involve users in the trade off process
  * __T7: Make Quality a Requirements Issue__
  * Rough edges today can be better than waiting a year with nothing good in the meantime
  * Know When to stop: from an artists perspective
* Your Knowledge Portfolio
  * Knowledge is an expring asset: it gets out of date quickly
  * Invest in your knowledge regularly, diversify it, manage risk (dont put all your eggs in one basket), rebalance regularly (the industry changes rapidly)
  * __T8: Invest regularly in your knowledge portfolio__
  * Pg 15 has recommendations on staying current
  * When you can't answer a question, find someone who can, and learn from them
  * __T9: Critically Analyze what you read and hear__
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
    * __T10: Its both what you say and the way you say it__

## 2. A Pragmatic Approach

* The Evils of Duplicaion
  * __Tip 11__ DRY Principle: Don't repeat yourself
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
      * __T12__ Make it easy to reuse
* Orthogonality
  * Ortho = independence, decoupling
  * Benefits of Orthogonality
    * __T13__ Eliminate Effects between unrelated things
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
  * __T14__ There are no final decisions
  * Schroedinger's cat: the target will always be changing
* Tracer Bullets
  * In ambiguous requirements, Specifying to death is not good
  * __T15:__ Use Tracer bullets to find the target. AKA Build something quick to get closer to final target
  * Tracer bullets don't always hit the target, you only see where they are headed. Thus, you still need to aim.
  * Is NOT prototyping. Prototype implies throw-away, tracer implies foundational
* Prototypes and Post-it Notes
  * Prototypes don't need to be code; can be thrown away
  * __T16__ Prototype to learn
  * Prototypes can ignore:
    * Correctness
    * Completeness
    * Robustness
    * Style
  * Caveat: Make sure everyone knows its disposable
* Domain Languages
  * __T17__: Program close to the problem domain
* Estimating
  * __T18:__ Estimate to avoid surprises
  * How Accurate is needed?
    * Ask what context will the estimate be used in
    * LOL: 1897 Indiana tried to rule that Pi should be 3; mathmaticians called them out
    * Units matter too: 130 days sounds precise, "around 6 months" has wiggle room
  * Draw on others experience before solidifying estimates
  * Think about scope before making a guess
  * Build a model, break it into components, identify parameters, set sample values, justify how you calculate each
  * Reflect on how on or off your estimates were
  * __T19:__ Iterate the schedule with the Code
  * When asked for an estimate, say "I'll get back to you"

## 3. The Basic Tools

* Intro
  * Tools amplify your talent
* Plain Text
  * __T20:__ Keep Knowledge in Plain Text
  * Human Readable files will outlive binaries
  * All software becomes legacy as soon as its written
  * Unix Philosophy, centered around plain text
  * All parties should communicate in a common standard, and plain text can be that
* Shell Games
  * __T21__: Use the power of command shells
  * Cygwin
* Power Editing
  * __T22__ Use a single editor well
  * Reduce the number of keystrokes you need to do things
* Source Code Control
  * __T23:__ Always use Source Control
  * Helps builds be automatice and repeatable
* Debugging
  * Can be sensitive, emotional
  * __T24:__ Fix the problem, not the blame
  * __T25:__ Don't Panic
  * DDD Debugger
  * __T26__: The OS probably isnt broken. If you see hoofprintes, think horses not zebras
  * __T27__: Don't assume it, prove it
  * Debugging Checklist pg 98
* Text Manipulation
  * __T28:__ Learn a text manipulation language
* Code Generators
  * __T29:__ Write code that writes code
  * Active and Passive

## 4. Pragmatic Paranoia

* Intro
  * __T30:__ You can't write perfect software
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
  * __T31:__ Design with Contracts
  * Assertions
    * Downside: not prpopgated to children
* Dead Programs tell no lies
  * __T32__ Crash Early
  * A dead program does less damage than a crippled one
* Assertive Programming
  * __T33__: If it can't happen, use assertions to ensure it won't happen
  * Don't turn off asserts in production code
* When to use Exceptions
  * __T34:__ Use Exceptions for exceptional problems
  * Java has a "Remote Method Invocation" facility
* How to balance Resources
  * __T35:__: Finish what you Start
  * Similarities to Ctor and Dtor

## 5. Bend, or Break

* Intro
  * Adaptability to Life's changes
  * Write less code to stay most flexible
  * Metaprogramming
* Decoupling and the Law of Demeter
  * Isolation between services is a good thing
  * Unecessary coupling leads to fear when a code change happens
  * __T36__: Minimize Coupling between Modules
* Metaprogramming
  * __T37:__ Configure, don't integrate
  * Metadata is accessed and used at runtime not compile time
  * __T38:__ Put abstractions in the code, details in the Metadata
  * Program for the general case, put the specifics elsewhere
* Temporal Decoupling
  * Concurrency
  * __T39:__ Analyze workflow to improve concurrency 
  * __T40__: Design using services: independent concurrent objects behind well-defined, consistent interfaces
  * __T41__: Always design for concurrency
* It's Just a View
  * A good definition of a module is that it has a single well-defined responsibility
  * Events: can be used to minimize coupling between objects
  * Publish/subscribe protocol
  * __T42__ Separate Views from Modules
  * Model View Controller review
* Blackboards
  * __T43__: Use blackboards to coordinate workflow

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
  * __T44:__ Don't program by coincidence
* Algorithm Speed
  * Estimate your resources (speed, memory, etc)
  * Big O notation
  * Common Sense estimation
  * __T45:__ Estimate the order of your algorithms (like the magnitude)
  * Use code profilers to count how many times steps get executed
  * Fastest might not always be best. There are tradeoffs
  * __T46:__ Test your estimates
* Refactoring
  * __T47:__ Refactor early, refactor often
  * SW is gardening: it is organic. Some decisions thrive, others are compost
  * Reasons to refactor: Duplication, Nonorthogonal design, Outdated knowledge, and performance.
  * When you refactor, fix not only the refactored part, but also everything that depends on it
* Code that's easy to test
  * Software Integrated Circuit
  * Unit Testing: Creates an atificial environment, invoke routines
  * Testing against contract: checks that code honors its contract, and if the contract actually works as intended
  * Goal is to avoid creating a time bomb: something that blows up at an awkward moment later in the project
  * Test Harnesses: useful for specifying setup, cleanup, select individual tests, analyze outputs,standard failure reporting
  * Tests should be composable: has subtests
  * Don't add+remove ad hoc tests, add them into a unit test
  * Test Window: Log files, hot key sequence to bring up diagnostic data
  * Culture of testing: Testing is more cultural than technical
  * __T48:__ Design to test
  * __T49:__ Test your software or your users will
* Evil Wizards
  * No one should write code they don't understand
  * __T50:__ Don't use wizard code you don't understand

## 7. Before the Project

* Intro
* The Requirements Pit
  * __T51:__ Don't gather requirements, dig for them
  * Policies change frequenty, make sure you're not doing business policy when you need a requirement
  * Understand why users do a specific thing, not just the WAY they do it
  * Shadow a user to understand what they really need
  * __T52:__ Work with a user to think like a user
  * Use Cases: specify a use of the system
  * Don't duplicate what already exists (example, confusing warpper around a micing board)
  * Use Case Template (pg 206)
    * Goal, Scope, Level, Preconditions, Success End condition, fail end condition, primary actor, variations, related info (priority, performance targe, frequency), schedule, open issues
    * Don't be a slave to formatting
    * Don't be too specific in a requirement
    * Shut down scope creep: "just one more" is an endless loop
  * __T53:__ Abstractions live longer thna details
  * __T54:__ Use a project Glossary
* Solving Impossible Puzzles
  * Some constraints are absolute, others are preconceived notions
  * Enumerate all possivle avenues before you commit to one
  * Categorize and prioritize your constraints
  * Questions to ask when something seems too hard:
    * Is there an easier way?
    * Are you solving the right problem
    * Why is it a problem?
    * What is making it so hard to solve?
    * Does it have to be done this way, or done at all?
  * __T55:__ Don't think outside the box, find the box
* Not until you're ready
  * Know when to start and know when to wait
  * __T56:__ Listen to nagging doubts: start when you're ready
  * When procrastinating in starting something new, just start prototyping
* The Specification trap
  * __T57:__ Some things are better done than described
  * Specifications are security blankets
* Circles and Arrows
  * __T58:__ Don't be a slave to formal methods
  * __T59:__ Expensive tools do not produce better designs

## 8. Pragmatic Projects

* Intro
* Pragmatic Teams
  * Quality is a team issue
  * Quality officer is a bad approach
  * For good teams, generate a brand externally
  * __T60__: Organize around functionality, not job functions
  * Know when to stop adding paint
* Ubiquitous Automation
  * __T61__ Don't use manual procedures
* Ruthless Testing
  * __T62__: Test Early. Test Often. Test Automatically
  * Types of tests
    * Unit tests
    * Integration tests
    * V&V
    * Resource exhaustion errors recovery
      * Assess behavior in real world condtions
      * Run out of disc space, memory, etc
    * Performance Testing
    * Usability Testing
  * __T63__: Coding aint done till all the tests runtime
  * How to test
    * Regression Testing
    * Test Data
      * Real world data vs synthetic data
    * Exercising GUI systems
    * Testing the tests
    * Testing thuroughly
      * Coverage analysis
      * Test for state coverage, not lines of code covered
  * Metrics around code
    * McCabe Cyclomatic Complexity Metric (complexity of decision structures)
    * Inheritance fan-in and fan-out
    * Response Set
    * Class Coupling ratios
  * __T64:__ Use sabeteurs to test your Testing
  * __T65__: Test state coverage, not code coverage
  * __T66__: Find bugs once
* It's all Writing
  * __T67__: Treat English as another programming language
  * Comments in Code: why something is done, its purpose and goal. Don't do misleading names or meaningless names
  * Stroop Effect: something does non-intuitive
  * __T68__: Build Documentation in, dont bolt it once
* Great Expectations
  * __T69__: Gently exceed your users expectations
* Pride and Prejudice
  * __T70__: Sign your work
  * But remember you are a team, cooperate

## Resources

Professional Societies and resources

* ACM
* IEEE
* Slashdot
