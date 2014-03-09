# Functions

## First-class objects

Functions are first-class objects. They can be

- Created via literals
- Assigned to variables, array entries and properties of other objects
- Passed to and returned from functions

Ex. Sort an array in JS 
<pre>
var values = [123, 319, 539, 1599, 20, 293];
values.sort(function(a, b) { return a - b}); // for ascending order
</pre>

## Anonymous functions

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

## Scoping

- Variable scoping only lasts within the function they are declared not in the block.
- Named functions are in the scope of the window object aka global

# Invocations

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


	    console.log.call(this, "hello world");
	    
	    function smallest(arr) {
	    	return Math.min.apply(Math, arr); 
	    }
	    
	    function largest(arr){
	    	return Math.max.apply(Math, arr); 
	    }

## Function Arguments 

- There is **NO ERROR** raised when there's a mismatch between the number of arguments provided and the parameters used. The left out parameters are left undefined.
- All function invocations are passed **two implicit parameters**: *this* and *arguments*
- **ARGUMENTS PARAMETER** : is a collection of all arguments passed to the function. It has a length property but it is *not an array*.
- **THIS PARAMETER** : Refers to the object that is implicitly *associated* with the function invocation and is called the *function context*.
- The `arguments` parameter has a `callee` property that refers to the currently executing function. [ not future proof ]

#### Value of `this`

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
</pre>

### Arguments

Arguments is an Array like object. It supports iteration, indexing and a length property but thats where the similarity ends. However, it can be called with Array methods like so 

<pre>
var args = Array.prototype.slice.call(arguments);

// to find the maximum value in the arguments
function findMaxArg(){
    return Math.max.apply(Math, Array.prototype.slice.call(arguments));
}
</pre>

### Inline Functions

<pre>
var myObj = {
	say: function sayHello() { // this is an inline function
		console.log("hello world"); 
    }
}
</pre>

Inline functions are **only** visible within the scope of the functions themselves. Hence, they dont act like function declarations  that are attached to the global scope, but rather are only available inside the scope of their definition itself.

#### Function Length

All functions have a `length` property (not to be confused with `arguments.length`) property which specifies the number of named arguments that gets passed to the function.

<pre>
function myFunc(first, second, third) {
    console.log("named:", myFunc.length);
    console.log("args passed:", arguments.length);
}

myFunc("hello", "world") 
// named: 3
// args passed: 2
</pre>

**Overloading functions**

<pre>
var something = {};
addMethod(something, "zero", function() { /* do something */});
addMethod(something, "one", function(a) { /* do something */});
addMethod(something, "two", function(a, b) { /* do something */});

function addMethod(obj, name, fn) {
    var old = obj[name];
    obj[name] = function() {
        if (fn.length === arguments.length)
            return fn.apply(this, arguments)
        else if (typeof old === "function")
            return old.apply(this, arguments);
    };
}
</pre>

#### Is a function?

<pre>
console.log( typeof console.log === "function" );
// the above some browser inconsistencies, hence the best way is to check using below

function isFunction(fn) {
    return Object.prototype.toString.call(fn) === "[object Function]"
}
</pre>
