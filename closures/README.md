Closures
===

Closure is the scope created when a function is declared that allows the function to access and manipulate variables that are external to that function.

<pre>
function makeAdder(x) {
    return function adder(y) {
        return x + y
    }
}

var addTwo = makeAdder(2);
console.log(addTwo(4)); // prints 8
</pre>

A closure keeps the variables in the function's scope from being garbage collected as long as the function exists.


