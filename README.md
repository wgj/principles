# Principles and guidelines for programming
This is a list of concepts and ideas I like to think about when I write and read code. 
The collection slants heavily towards C and Go, and has been cherry picked from larger like-minded lists.

I try to cite whenever possible, and I accept pull requests :)

## General
### [Don't Repeat Yourself (DRY)](http://wiki.c2.com/?DontRepeatYourself)
Duplication (inadvertent or purposeful duplication) can lead to maintenance nightmares, poor factoring, and logical contradictions.
### [You Ain’t Gonna Need It (YAGNI)](http://wiki.c2.com/?YouArentGonnaNeedIt)
Implement things when you actually need them, never when you _just_ think that you need them.
### [Zero One Infinity (ZOI)](http://wiki.c2.com/?ZeroOneInfinityRule)
You will either need zero of a thing, one of a thing, or an arbitrary number of the thing. Don't place arbitrary limits on objects.

## [Go Proverbs](https://go-proverbs.github.io/)
### [The bigger the interface, the weaker the abstraction](https://www.youtube.com/watch?v=PAAkCSZUG1c&t=5m17s)
An interface is more useful when it's easier to satisfy it.

### [Gofmt's style is no one's favorite, yet gofmt is everyone's favorite](https://www.youtube.com/watch?v=PAAkCSZUG1c&t=8m43s)
> "Who cares? Shut up"

_-Rob Pike_
### [A little copying is better than a little dependency.](https://www.youtube.com/watch?v=PAAkCSZUG1c&t=9m28s)
You can make your programs compile faster, easier to maintain, and simpler if you keep the dependency tree small.

>"Y'know what? I don't need that whole library. All I need are these three lines of code, and I can just copy, and it's fine."

_-Rob Pike_
### [Clear is better than clever](https://www.youtube.com/watch?v=PAAkCSZUG1c&t=14m35s)
>"You should be thinking about making the simple clear code, rather than trying to make cleverst densest stuff you can."

_-Rob Pike_
### [Don't just check errors, handle them gracefully](https://www.youtube.com/watch?v=PAAkCSZUG1c&t=17m25s)
>"A big part of all programming is how you handle errors. And people are too quick to jump to just return error up the tree and forget about it, rather than thinking about how an error should really work."

_-Rob Pike_

### [Documentation is for users](https://www.youtube.com/watch?v=PAAkCSZUG1c&t=19m07s)
Don't focus comments on [what](https://www.reddit.com/r/ProgrammerHumor/comments/60adxr/typical_code_comments/) your code is doing, focus on _why_.
>"Think of the user when you write documentation. Don't be afraid to explain things so that they make sense."

_-Rob Pike_
### Don't panic
Don't use panic for normal error handling. Use error and multiple return values.
Only fail when it's impossible to recover. Give clients errors, and let them try to recover.

## SOLID
### [Single responsibility principle](https://en.wikipedia.org/wiki/Single_responsibility_principle)
A class should have only a single responsibility (i.e. only one potential change in the software's specification should be able to affect the specification of the class).
### [Open/closed principle](https://en.wikipedia.org/wiki/Open/closed_principle)
A class should be open for extension, but closed for modification.
### [Liskov substituion principle](https://en.wikipedia.org/wiki/Liskov_substitution_principle)
Objects in a program should be replaceable with instances of their subtypes without altering the correctness of that program.
### [Interface segregation principle](https://en.wikipedia.org/wiki/Interface_segregation_principle)
No client should be forced to depend on methods it does not use. Many client-specific interfaces are better than one general-purpose interface.
### [Dependency inversion principle](https://en.wikipedia.org/wiki/Dependency_inversion_principle)
High-level modules should not depend on low-level modules. Both should depend on abstractions. Abstractions should not depend on details. Details should depend on abstractions.

## Go wiki's CodeReviewComments
### [Gofmt](https://github.com/golang/go/wiki/CodeReviewComments#gofmt)
Run gofmt on your code to automatically fix the majority of mechanical style issues.
### [Comment Sentences](https://github.com/golang/go/wiki/CodeReviewComments#comment-sentences)
Comments documenting declarations should be full sentences, even if that seems a little redundant. Comments should begin with the name of the thing being described and end in a period.
### [Doc Comments](https://github.com/golang/go/wiki/CodeReviewComments#doc-comments)
All top-level, exported names should have doc comments, as should non-trivial unexported type or function declarations.
### [Error Strings](https://github.com/golang/go/wiki/CodeReviewComments#error-strings)
Error strings should not be capitalized (unless beginning with proper nouns or acronyms) or end with punctuation, since they are usually printed following other context.
### [Handle Errors](https://github.com/golang/go/wiki/CodeReviewComments#handle-errors)
Do not discard errors. If a function returns an error, check it to make sure the function succeeded. Handle the error, return it, or, in truly exceptional situations, panic.
### [Receiver Type](https://github.com/golang/go/wiki/CodeReviewComments#receiver-type)
Choosing whether to use a value or pointer receiver on methods can be difficult, especially to new Go programmers. If in doubt, use a pointer, but there are times when a value receiver makes sense, usually for reasons of efficiency, such as for small unchanging structs or values of basic type. Some useful guidelines:
<ul>
<li>If the method needs to mutate the receiver, the receiver must be a pointer.</li>
<li>If the receiver is a large struct or array, a pointer receiver is more efficient. How large is large? Assume it's equivalent to passing all its elements as arguments to the method. If that feels too large, it's also too large for the receiver.</li>
<li>If the receiver is a struct, array or slice and any of its elements is a pointer to something that might be mutating, prefer a pointer receiver, as it will make the intention more clear to the reader.
</li>
<li>Finally, when in doubt, use a pointer receiver.</li>
</ul>

### [Useful Test Failures](https://github.com/golang/go/wiki/CodeReviewComments#useful-test-failures)
Tests should fail with helpful messages saying what was wrong, with what inputs, what was actually got, and what was expected.
### [Variable Names](https://github.com/golang/go/wiki/CodeReviewComments#variable-names)
The further from its declaration that a name is used, the more descriptive the name must be.
Common variables such as loop indices and readers can be a single letter (i, r). More unusual things and global variables need more descriptive names.

## Zed Shaw's Defensive Programming 
### The Creative Programmer's Mind-Set
Programming is a creative process, and fear kills creativity. With this mind-set, accidents are designed to make you unafraid of taking chances and looking like an idiot:
<ul>
<li>I can't make a mistake.</li>
<li>It doesn't matter what people think.</li>
<li>Whatever my brain comes up with is going to be a great idea.</li>
</ul>

However, this mind-set should not be carried over into the dark-site of the creative mind-set: Destructive Programmer's Mind-Set. These are lies:
<ul>
<li>It's possible to write perfect software.</li>
<li>My brain tells me the truth, and it can't find any errors: I have therefore written perfect software.</li>
<li>My code is who I am and people who criticize its perfection are critizing me.</li>
</ul>


### The Defensive Programmer's Mind-Set
The defensive programmer basically hates your code and believes:
<ul>
<li>Software has errors.</li>
<li>You aren't your software, yet you're responsible for the errors.</li>
<li>You can never remove the errors, only reduce their probability.</li>
</ul>

### The Eigth Defensive Programmer Strategies
#### Never Trust Input
Never trust the data you're given and always validate it.
#### Prevent Errors
If an error is possible, no matter how probable, try to prevent it.
#### Fail Early and Openly
Fail early, and openly, stating what happened, where, and how to fix it.
#### Document Assumptions
Clearly state the pre-conditions, post-conditions, and invariants.
#### Prevention over Documentation
Don't do with documentation that which can be done with code of avoided completely.
#### Automate Everything
Automate everything, especially testing.
#### Simplify and Clarify
Always simplify the code to the smallest, cleanest form that works without sacrificing safety.
#### Question Authority
Don't blindly follow or reject rules.

## [The Power of 10: Rules for Developing Safety-Critical Code](https://en.wikipedia.org/wiki/The_Power_of_10:_Rules_for_Developing_Safety-Critical_Code)
<ol>
<li>Avoid complex flow constructs, such as goto and recursion.</li>
<li>All loops must have fixed bounds. This prevents runaway code.</li>
<li>Avoid heap memory allocation.</li>
<li>Restrict functions to a single printed page.</li>
<li>Use a minimum of two runtime assertions per function.</li>
<li>Restrict the scope of data to the smallest possible.</li>
<li>Check the return value of all non-void functions, or cast to void to indicate the return value is useless.</li>
<li>Use the preprocessor sparingly.</li>
<li>Limit pointer use to a single dereference, and do not use function pointers.</li>
<li>Compile with all possible warnings active; all warnings should then be addressed before release of the software.</li>
</ol>

## Test Driven Development (TDD)
### [The Three Laws of TDD](http://butunclebob.com/ArticleS.UncleBob.TheThreeRulesOfTdd)
<ol>
<li>You are not allowed to write any production code unless it is to make a failing unit test pass.</li>
<li>You are not allowed to write any more of a unit test than is sufficient to fail; and compilation failures are failures.</li>
<li>You are not allowed to write any more production code than is sufficient to pass the one failing unit test.</li>
</ol>

## [Hitchhiker's Guide to Python](http://docs.python-guide.org/en/latest/)
### [Testing Your Code](http://docs.python-guide.org/en/latest/writing/tests/)
<ol>
<li>A testing unit should focus on one tiny bit of functionality and prove it correct.</li>
<li>Each test unit must be fully independent. Each test must be able to run alone, and also within the test suite, regardless of the order that they are called. The implication of this rule is that each test must be loaded with a fresh dataset and may have to do some cleanup afterwards. This is usually handled by setUp() and tearDown() methods.</li>
<li>Try hard to make tests that run fast. If one single test needs more than a few milliseconds to run, development will be slowed down or the tests will not be run as often as is desirable. In some cases, tests can’t be fast because they need a complex data structure to work on, and this data structure must be loaded every time the test runs. Keep these heavier tests in a separate test suite that is run by some scheduled task, and run all other tests as often as needed.</li>
<li>Learn your tools and learn how to run a single test or a test case. Then, when developing a function inside a module, run this function’s tests frequently, ideally automatically when you save the code.</li>
<li>Always run the full test suite before a coding session, and run it again after. This will give you more confidence that you did not break anything in the rest of the code.</li>
<li>It is a good idea to implement a hook that runs all tests before pushing code to a shared repository.</li>
<li>If you are in the middle of a development session and have to interrupt your work, it is a good idea to write a broken unit test about what you want to develop next. When coming back to work, you will have a pointer to where you were and get back on track faster.</li>
<li>The first step when you are debugging your code is to write a new test pinpointing the bug. While it is not always possible to do, those bug catching tests are among the most valuable pieces of code in your project.</li>
<li>Use long and descriptive names for testing functions. The style guide here is slightly different than that of running code, where short names are often preferred. The reason is testing functions are never called explicitly. square() or even sqr() is ok in running code, but in testing code you would have names such as test_square_of_number_2(), test_square_negative_number(). These function names are displayed when a test fails, and should be as descriptive as possible.</li>
<li>When something goes wrong or has to be changed, and if your code has a good set of tests, you or other maintainers will rely largely on the testing suite to fix the problem or modify a given behavior. Therefore the testing code will be read as much as or even more than the running code. A unit test whose purpose is unclear is not very helpful in this case.</li>
<li>Another use of the testing code is as an introduction to new developers. When someone will have to work on the code base, running and reading the related testing code is often the best thing that they can do to start. They will or should discover the hot spots, where most difficulties arise, and the corner cases. If they have to add some functionality, the first step should be to add a test to ensure that the new functionality is not already a working path that has not been plugged into the interface.</li>
</ol>