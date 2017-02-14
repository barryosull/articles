# Growing Object Orientated Software, Guided by Tests

Below is a collection of notes I made after reading [this book](http://www.growing-object-oriented-software.com/). I'm putting them online because it's a useful reference and someone might find it useful. The advice will seem all over the place, eventually I'll edit it so that headings are clearer.

=========================================================================================================================

### Three types of test:
- Acceptance: End to end
- Integration: Test that our code can interact with code that we don't control, eg. an external API ora library
- Unit: Test our objects do the right thing (and are they easy to work with)

Start with a failing acceptance test, then enter the TDD loop until the acceptance test passes. Repeat.

Hard to test objects most likely have a poor design. It means they are hard to understand and hard to use.

Always have end to end tests, they expose uncertainty early

### Brownfield projects (legacy codebases)
- Automate build and deploy
- Add end to end tests for the parts you want to change
- Slowly build testcoverage as you update/fix the codebase (3 types where appropriate) 

Start your acceptance tests with the simplest success case
Keep a note of future failure cases, refactorings and other tasks, allows you to stay focussed on getting the simplest acceptance test passing

Write "a" failing test, don't write all test cases at once (applies to all test types).

Test behaviour, not methods. This means writing tests that show what your object is for, not what it's methods do.Weneed to know how to use the object to achieve a goal. 

### TDD loop
1. Write a failing unit test
2. Make the test pass
3. Refactor
4. Repeat.

Objects communicate via messages. Messages should be immmutable, Objects can have state.

"Encapsulte data" is another way of saying "hide data". If an object is "hiding data" it better have a good reason. Eg. constants in the wrong file

Iteration zero, the  walking skeleton. Get a single use case working end to end using real code and libraries. Proves your concept works, is buildable, testable, and it highlights integration pain points early.

In tests, use null when an argument doesn't matter. make it a named constant though, so the code is easier to read.

Put your tests in a different package to your code, ensures sure you're testing the external API.

Keep the code compiling. The time between changing the codebase (breaking it) and fixing it should be minimal. The more code you have open and in progress, the more you have to keep in your head, slowing you down.

Nothing shakes out a design better than trying to implement it. Up front design is nice, but it will never get it right first time.

Use "DefectException"s, these are a sub type of exception that are only throw if the developer did something wrong. Eg. Forgot to set an environment variable. Very handy for catching these kinds of mistakes, they're usually easy to fix once you know what you're dealing with.

Workign is not the same as finishe. Be sure to refactor your code right after writing a passing test, it's the best time to do it, you have all the context in your head.

Distinguish between test setup and behaviour assertions, keep it clear.

Don't use strings, use domain types instead (ValueObjects).

In tests, don't mock values, use real ones instead. If they're complex to build, then use one of the many object creation patterns and add that to your test codebase.

### Dealing with bloated constructors:
- Pakage the dependencies into a new concept
- Break up the class into multiple classes
- Use default values (if the majority of constructor arguments are values)


Test name should describe features, not methods

Writing test names. It doesn't matter if you write the first or last, as long they're easy to understand and you're consistent.

### Writing a test, what orrder should I do it in?
- Write test name
- Write the call to the target code
- Write assertions/expectations
- Write the setup and teardown

Don't use liternal, give values meaningful names

Builders are great for creating objects, especially in tests. Makes code a lot easier to read and they're reusable.

Builders can be arguments to builders, make it easier to compose complex objects while keeping code clean.

Test expressiveness: Focus on expressing what you want to do, not how you plan to do it

Tests should fail informateively. If a failing test doesn't help you figure out what's wrong, then it's only half helping you.

Mock objects can be viewed as tracer objects, they tell you they're not used as expected

### The TDD loop should really be the following
1. Write a failing unit test
2. Report errors clearly
3. Make the test pass
4. Refactor
5. Repeat.

Test readability and resilience tend to end uo coupled. If your tests are hard to read, then there's a good chance they're fragile.

When writing tests, specifiy what should happen and no more. Try to remove code that isn't important to the expected behaviour.

Command changes state, queries do not. Always remember CQS (and CORS).

