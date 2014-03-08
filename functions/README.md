### First-class objects

Functions are first-class objects. They can be

- Created via literals
- Assigned to variables, array entries and properties of other objects
- Passed to and returned from functions

Ex. Sort an array in JS 
<pre>
var values = [123, 319, 539, 1599, 20, 293];
values.sort(function(a, b) { return a - b}); // for ascending order
</pre>

### Anonymous functions

- When a function is named, it is valid throughout the scope of the parent function.
- Functions declared at the top-level belong to the window object.
- All functions have a property called `name` which is assigned to an empty string in case of anonymous functions.

<pre>
var myfunc = function() {  // this is an anonymous function
    console.log("hello");
}

var anotherFunc = function hello() { // this has a name property as hello
    console.log("world");
}

console.log(anotherFunc.name === "hello") // true
</pre>

### Scoping

- Variable scoping only lasts within the function they are declared not in the block.
- Named functions are in the scope of the window object aka global

Invocations
====

There are 4 different ways to invoke a function 

1. As a function (straightforward manner).
<pre>
sayHello();
</pre>

2. As a method of an object.
<pre>
person.sayHello();
</pre>

3. As a constructor which instantiates a new object.
<pre>
var person = new Person();
</pre>

4. Via a function's `apply()` or `call()` methods.
<pre>
console.log.call(this, "hello world"); // hello world
</pre>

### Function Arguments 

- There is **NO ERROR** raised when there's a mismatch between the number of arguments provided and the parameters used. The left out parameters are left undefined.
- All function invocations are passed **two implicit parameters**: *this* and *arguments*
- **ARGUMENTS PARAMETER** : is a collection of all arguments passed to the function. It has a length property but it is *not an array*.
- **THIS PARAMETER** : Refers to the object that is implicitly *associated* with the function invocation and is called the *function context*.

#### Understanding the value of `this` in the 4 types of invocations

a. Function Invocation

This type is a special case of invocation as a method wherein the method is the `window` object.

b. Invocation as a method

In this type of invocation the *function context (or this)* refers to the object to which the method belongs.

c. Invocation as a constructor

In this case

    - A new object is created
    - This object is passed to the constructor as `this` parameter
    - In the absence of an explicit return value the new object is returned.

d. Invocations with call and apply

`call` and `apply` allow you to set the function context manually. When a function is called with by `apply` its method property it can be passed a function context and an array of values to be used as the invocation arguments. The `call` method behaves in the same away apart from the fact that arguments are passed directly in the argument list rather than an array.

<pre>
console.log.apply(this, [12, 31, 41]);
console.log.call(this, 12, 31, 41);
function forEach(list, callback) {
	for (var i = 0; i < list.length; i++) {
		callback.call(list[i], i);	}}
var names = ["alpha", "beta", "gamma", "delta"];
forEach(names, function(index) { console.log(this, index); });
</pre>