---
layout: post
title: Objects and Arrays in JS
---

[Objects and Arrays](http://eloquentjavascript.net/04_data.html) deals with 
objects and arrays exclusively in JS. The important thing that I would like to 
remember are the following.

* There are no types. Each object can be loosely created by just adding an 
attribute directly. 
{% highlight javascript %}
var object = {};
object.property = 0;
object = {
   life: 2,
   name: "Sud"
};
{% endhighlight %}
* Scanning the object is achieved by iterating through the object. In essence,
treating the object as a map between properties which are keys and the values.
There seems to be a subtle difference between `object.elem` and `object[elem]`
where in the second case, the argument to the `[]` operator is evaluated before
checking for the value in object.
{% highlight javascript %}
for( var elem in object )
  console.log( object[elem] );
  console.log( object.elem );
{% endhighlight %}
* Strings, Integers, and Boolean values are immutable. Found it to be pedantic,
and think it might possibly be an implementation detail.
* Array methods of interest: `push`, `shift`, `unshift`, `indexOf`, `lastIndexOf`,
`slice`, `concat`. Strings can also be called with these functions. `trim` method
strips of spaces and newlines.
* `arguments` object seem to be magic argument to functions. It is an array of
all inputs to the function _apart_ from the named arguments.
* Math has a lot of functions defined. All global variables are essentially 
properties of the window object.

The final deep comparison exercise showed some of the above points. Given my 
propensity to forget things let me put this up here for my own future reference
at personal risk of totally showing of my JS n00bness.

{% highlight javascript %}
function deepEqual( lhs, rhs )
{
  //console.log( lhs + rhs );
  if( lhs == null && rhs == null )
    return true;
  if( typeof(lhs) == "object" && typeof(rhs) == "object" )
  {
    var isEqual = true;
    for( var elem in lhs )
    {
      if( !( elem in rhs ) )
        return false;
      isEqual &= deepEqual( lhs[elem], rhs[elem]);
    }
    return (isEqual)? true: false;
  }
  else
    return lhs === rhs;
}

var obj = {here: {is: "an"}, object: 3, left: "right"};
console.log(deepEqual(obj, obj));
// → true
console.log(deepEqual(obj, {here: 1, object: 2}));
// → false
console.log(deepEqual(obj, {here: {is: "an"}, object: 2}));
// → true
{% endhighlight %}
