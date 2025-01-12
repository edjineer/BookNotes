# Clean Code

By Robert C Martin, 2009

## Look Up Later

* Jar, war, ear files
* Additional Authors per chapter

## Chapter 2: Meaningful Names

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



## Chapter 7: Error Handling

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

## Chapter 6: Objects and Data Structures

## Chapter 10: Classes

## Chapter 9: Unit Tests

## Chapter 13: Concurrency
