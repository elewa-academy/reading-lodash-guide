## Tracify Your Refactor

Introduce a non-breaking change to your function's specs that allows a developer to trace the behavior, chunk by chunk.  This will help with debugging, and allow them to understand the implementation without having to do a complete analysis of the source.

Different from the Trace-Log in Expansions, your tracified Lodash function will have no Strings and the trace will be embedded directly into the main function's execution.  It is also tracing  

_Non-Breaking API Changes_ are changes made to the arguments or return value of a function that would not force you to re-write code that used the old version.

In this case, we are adding an extra boolean argument called "trace". If this argument is passed, the function will behave differently.  If not, it behaves exactly as it did before this refactor.

___

* Add a "trace" parameter to your function
* Under each step in your solution, add an if statement to build the trace that records what changed
    * {chunk_function: return_value}
    * See the completed demo for an example to study
* Update the docs in the comments of 4-___-tracible.js
* Run it through your original tests. If it passes, Win.


___
___
### <a href="http://elewa.education/blog" target="_blank"><img src="https://user-images.githubusercontent.com/18554853/34921062-506450ae-f97d-11e7-875f-6feeb26ad72d.png" width="100" height="40"/></a>
