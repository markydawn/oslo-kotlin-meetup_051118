# Oslo Kotlin Meetup 05.11.18 - Testing in Kotlin - and YOU!
Testing in Kotlin and YOU! Code examples and slides from my presentation. Code is meant to be educational, not perfectly structured :) 

* the `master`-branch contains code as it was before the meetup. If you want, you can use the code here to experiment with writing tests. 
* the `meetup-coding`-branch contains the solutions as we live-coded in the meetup. 


## Retrospective
Here are a few things I think is worth mentioning after the meetup. If might be something we learned, or some other things worth mentioning.

### Kluent dependency
Here I must confess, I still don't know why it won't load. In other projects where I used Gradle, everything works like a charm. If you know what the issue is, please let me know! I have tried downgrading the version, changing the type and more. Even removing type and just setting scope test. In a Gradle project the guides from the [Kluent github page](https://github.com/MarkusAmshove/Kluent) works just fine. 


### MockK
* During the meetup we found some weird behavior in MockK. No matter what we tried, MockK replaced the method with the name `get` in the `Environment`-class with its own `get`-method (which has a different return type!). This lead to us getting error messages stating that we gave the wrong return type. The reason for this is not well-covered in the documentation, but I managed to find some example of it. Take a look at the [first example on this page](https://github.com/mockk/mockk#private-functions-mocking--dynamic-calls). See something familiar? `mock["accelerate"]` which is used to get the field `accelerate` in the object called `mock`. This means that inside of MockK calls, the method `get` is overriden (just like I said was my guess in the meetup). The scary part is that if we had put some spaces in our code `environment.getProperty("themkat.favouriteComputers")`, so it ended up like this `environment getProperty "themkat.favouriteComputers"` `getProperty` would no longer be interpreted as the method in `Environment`, but part of the MockK DSL. I find this a bit weird, but I realize I that there are not that many cases where you would use `get` or `getProperty` as names of functions you could mock. I'm happy that I learned this together with all of you today :)  
* If the mocking demo hadn't gotten the unexpected errors (which was still cool to learn!) I would have covered verifications as well. Verifications are as simple as mocking, but they are used to verify that a given function or method is called. If you have a mock (or spy) `mymock`, then `verify(exactly = 1) { mymock.method(1) }` will check that the method `method` in `mymock` is called exactly once. Read more about that and more in [the MockK documentation](https://github.com/mockk/mockk). 


## Extra resources
These resources may help you to learn more about the topics from the meetup presentation. Some of them may go more into detail, which can help you in deciding what you should use for your project.
* [JUnit 5 user guide](https://junit.org/junit5/docs/current/user-guide/) (contains a lot of information on what's new)
* [Parameterized tests](https://blog.codefx.org/libraries/junit-5-parameterized-tests/)
* [Assertion library: Kluent documentation](https://markusamshove.github.io/Kluent/)
* [Interesting article on writing clean tests with Test Data Builders](https://www.petrikainulainen.net/programming/testing/writing-clean-tests-new-considered-harmful/)
* [Combining Test Data Builders and Object Mother](https://blog.codeleak.pl/2014/06/test-data-builders-and-object-mother.html)
