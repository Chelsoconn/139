**Assertion**

Part of a test which confirms that the result we are getting from the interface being tested match what is expected. We first input what we are expecting the code to return, and then the code we are testing. An assertion will compare the expected value with the return value... They represent what you are trying to verify. 

```ruby 
assert(obj, [error message])
assert_raises(ErrorType) { ... }
assert_equal(expected, actual) # value equivalence #==
assert_includes(collection, object) #include?
assert_instance_of(class, object)
assert_in_delta(3.145, Math::PI, 0.001)
assert_empty(collection) #empty?
assert_nil(obj) #nil?
assert_same(array, array.sort!) # object equivalence
assert_match(regex, obj)
```

**Code Coverage**

How much of the code (private and public) is actually tested in the test suite. 100% means you have tested 100% of the methods in the code base. This does not mean that you have covered every edge case or bugs. It gauges code quality. It is not necessary to get 100% every time, but it does make your code more fault tolerant. 

**DSL (Domain Specific Language)**

A higher level language built with a general purpose language that helps solve a problem within a specific domain. It has a specialized and specific application. ex/ RSpec (domain specific to testing), Rails (domain specific to setting up web applications)

**Equivalence**

Different assertions use different methods to test for equality.

`assert_equal` - tests for value equality. It uses the `==`method defined for the object in question to determine if two objects have equivalent values. 

`assert_same`- tests for objects equality. Ensures that two objects are the same object in memory. 

*If you create custom objects then you should implement your own `==` method, so `BasicObject#==`doesnt implement. 

**Minitest**

A Ruby gem that helps us with unit testing. It is the default testing library that comes with Ruby. Allows us to write tests in ordinary Ruby code, and not rely on a DSL, as with RSpec. 

​	**2 types of Minitest syntax options**

		1) Assert-style : Uses regular Ruby code, more intuitive for beginning Ruby developers. A series of methods beginning with `test_` to test certain aspects of code, each method may contain one or more assertions. 
		1) Expectation or Spec-Style : More in line with RSpec testing style. Groups tests into `describe` blocks and writes individual tests with the `it` method.  Uses expectation matchers instead of assertions. 

​	*4 outputs when a minitest is run 

	- `.`= the test passed successfully 
	- `F`= the test failed
	- `S`= the test was skipped
	- `E`= the program raised an errror and stopped execution

**Refutation**

Opposite of assertions. Instead of confirming that an value is in line with some returned value, it confirms that these two results are not in line with eachother. They prove the expression to be false.

ex/ `refute_equal` expects the value given and the result of the executed code to not be equal 

- Every assertion has a corresponding refutation. The corresponding refutation takes the exact same arguments as the assertion, except looks for a false or falsey result. 

**Regression**

A type of bug in software that occurs after the program in question has been working already. Usually describes a bug that arised from some change to the code base (adding new features/ functionality or refactoring)

​	*3 Types of Regression

		- Local Regression- A bug that is introduced by and included in any changes or additions to code. 
		- Remote Regression- Refers to a change in one part of the code that casues a different part of the code to break (seperate module or class)
		- Unmasked Regression- Refers to a bug that is revealed by a change to code, where the bug existed before the change but didn't previously affect the program of functionality. 

**SEAT Approach**

Describes the common algorithm used for writing tests.

1. `S` = Set up the necessary objects

​	1. Instead of running any repeated 'setup' steps for each of our test methods, we can extract these repeated steps into a method that gets executed before running each test. In Minitest this is achieved by using the `setup` instance method. This will automatically run before each of the `test_..` methods. This is a good place to put something like object instantiation. By assigning objects to an instance variable, you ensure that they are available throughout the rest of the `test_` methods in the testing class. 

2.`E` = Execute the code against the object to test

1) This is where any code you need to execute in order to test it gets run. For example, let us say that we want to ensure that `2+2` is equal to `4`.. In order to test this, we will have to run the statement `2+2`, and then test the results against our expected value `4` in an assertion. Sometimes code that needs to be executed is simple enough to run within the assertion itself, such as the above example. Other times, it may require multiple steps, and it is better to run it outside of the assertion and save the result in a local variable for comparison.

3.`A` = Assert the results of the execution

1) This is where our assertions come in. We either assert or refute the result of our executed code with the expected results, to determine if the behavior of our program is in line with the particular 'rule' we have defined for this particular test.  This might be to see if a calculated value is equal to an expected one, if a certain action raises a certain error, to ensure that an object us instantiated properly, or any number of different things. 

4.`T` = Tear down and clean up lingering artifacts 

1) Similar to the set up step, we may also need a teardown step. This gets run after the execution of each test in our testing class. In Minitest we can define our 'teardown' steps in a teardown method. Actions that we might complete here include cleaning up and deleting files, logging results, or closing database connections. 

**simplecov**

Ruby gem that is a code coverage testing tool. Install it by `gem install simplecov`. include hte following lines at the top of your test file:

 ```ruby 
 require 'simplecov'
 SimpleCov.start
 ```

It will generate a file within a coverage directory that details all the metrics of your code coverage. 

**Skip**

The `skip` keyword is a special keyword we can use with Minitest test. It tells minitest to skip to the next test. This will be reported in the output of minitest with an `S`. 

**Test**

A situation or context in which tests are run. A test ensures that a single 'rule' about the interface in question is being upheld. For example, a test can ensure that you get an error message about trying to log in with the wrong password, or be as simple as ensuring that an instantiated object exists. 

A test is made up of assertions. 

**Test Suite**

The entire set of tests that accompany an application or program. This can include unit tests, integrations tests, regression tests, and a number of other things. Basically, includes all the tests involved in a project. 

**Unit Testing**

Automated tests that are designed and run to ensure that the smallest possible 'unit' of a program is functioning as intended. In OOP, this 'unit' usually consists of a single interface, as in that of a class. 

The goal of unit testing is to endure that each isolated piece of a program is functioning correctly. By using induvidual assertions, is provides a written contract that the interface in question must satisfy.  We can build 'units' based on this contract. Once all the tests pass, we consider the interface in question to be complete. 

Further, we can run these tests each time a change is made to ensure that the unit in question will continuously fulfull its obligations and no regression occurs. 