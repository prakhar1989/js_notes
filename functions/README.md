Functions are first-class objects. They can be
    - Created via literals
    - Assigned to variables, array entries and properties of other objects
    - Passed to and returned from functions

Ex. Sort an array in JS 
<pre>
    var values = [123, 319, 539, 1599, 20, 293];
    values.sort(function(a, b) { return a - b}); // for ascending order
</pre>
