**Closure-**

It refers to a chunk of code that can be saved and executed at a later time, possibly from a different location.  Closures work by binding their surrounding artifacts, which include variables, methods, objects, or other pieces of data and code. 

This binding creates an enclosure around all the artifacts so that they can be referenced at such time as the closure is executed. That means that closures can yse and even update local variables that are in scope for them when they are executed, even if the call for execution comes from a place in the code where these variables are not in scope. 

![Closure](https://github.com/gcpinckert/rb130_139/raw/main/study_guide/closures.jpg)

Above, you can see how a closure binds surrounding local variables and references them during execution. The block itself begins with the `do` keyword and contains all the code up until the `end`keyword. Nothe that within our block implementation, we have access to the local variable `results`, which was initialized on line 6 to the value `['']`.  This is because blocks have access to variables initialized in the outer scope. The closure created by the block can retain a memory of this variable and its value via a binding. 

When we invoke this block from within the for_each_in method with the `yield` statement on line 2, we can still access the local variable `results`, even though it is never passed into the method. This works because the block passed to `for_each_in` represnets a closure, and binds the local variable `results` to itself. 

- In ruby, blocks, proc, and lambdas are all ways to implement a closure. Note that a proc is an actual object, an instance of the `Proc` class, and a lambda is really a special kind of Proc object, while a block is not an object. 
- A block isn't an object so it isn't a value that we can return. However, a Proc is an object and also a closure. This means that we can actually assign closures to variables and pass them around. It also means that we can return them from either a method or a block. 



![Method returning a closure](https://github.com/gcpinckert/rb130_139/raw/main/study_guide/closures_2.jpg)