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