First-class objects
====
Functions are first-class objects. They can be

- Created via literals
- Assigned to variables, array entries and properties of other objects
- Passed to and returned from functions

Ex. Sort an array in JS 
<pre>
var values = [123, 319, 539, 1599, 20, 293];
values.sort(function(a, b) { return a - b}); // for ascending order
</pre>

Anonymous functions
====

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
</pre>

