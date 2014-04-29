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

### Private Variables

<pre>
function Person(name) {
    var _name = name;  // this now becomes private
    
    this.getName = function() {
        return _name;
    };

    this.changeName = function(s) {
        _name = s;
    };
}

var bob = new Person("bob");
console.log(bob.getName === "bob"); // true
console.log(bob._name === undefined) // true 
</pre>
