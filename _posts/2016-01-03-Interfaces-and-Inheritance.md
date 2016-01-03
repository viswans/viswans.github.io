---
layout: post
title: Interfaces and Inheritance in JS
---

This chapter is really eye opening and mouth-widing for some reasons. It
somehow gives the feeling that I am confused about how to construct solid
programs in JS. Nevertheless, let me jot down the important points.

1. Each function is an object. They can hold internal state which can be 
referred by using the `this` keyword. The magic methods `apply` and `bind`
basically operate on top of this feature. 
`function_name.apply(<object>, [<arg_list>])` calls the method by picking
all member variables from `<object>` and applying the arguments provided
from `arg_list`. Similarly `call` and `bind` work as well - the former 
instead taking the arguments directly, and bind  The usage of bind seems
to be first in first out, and arbitrary input can't be bound. 
[Interesting link on bind]([1])

2. Given that there are no types per se, there is no obvious way of defining
interfaces. Any function takes only an interface, and anything that doesn't
satisfy that would just log an error! But `public inheritance` C++-style 
can be implemented using prototypes. `Object.getPrototypeOf` returns the prototype
of an object. Functions with call to `new` act as constructors - atleast in my
head inline with point 1 from above.

3. Function overriding of inherited methods can be done by just setting the
function variable in the prototype to a new function. Changing a prototype is
as simple as adding a new property to that function's prototype and it shows
up in all downstream objects. `Object.defineProperty` seems like a multi-purpose
utility that can do a lot of magic. Setting a property to be not enumerable
ensures that it doesn't turn up when enumerating through a for loop. 
`Object.hasOwnProperty` checks if a property is from that function or from
a prototype that was used to derive this function. `Object.create(null)` ensures 
that the object created doesn't carry any property. Otherwise, even functions
of the prototype show up while enumerating!

4. Reemphasize on the usage of prototypes, adding a function is just about a
setting a new property for the functions prototype object. Getters and setters
can be defined by using JS magic - by using syntax `get height()` and 
`set height(value)` will allow `height` to be used as a normal property. It
can also be created using `Object.defineProperty`. To publicly inherit a prototype
say, B inherits from A, then `B.prototype = Object.create(A.prototype)` will do
the magic. To call the constructor from within B, would be equal to saying 
`A.call(this, arguments)`.

5. `instanceOf` keyword helps us identify types. Can be used to establish 
prototype hierarchy.


[1] [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind]
