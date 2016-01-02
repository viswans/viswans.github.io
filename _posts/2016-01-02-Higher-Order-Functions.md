---
layout: post
title: Higher Order Functions
---

[Higher Order Functions](http://eloquentjavascript.net/05_higher_order.html) gives
an introduction to the usage of higher order of functions in JS. Importantly, 
mentioning `map`, `forEach`, `filter`, `reduce` 

The introduction also points out to slightly uneasy notions that I am not used to.
In the absence of types, when a function returns another function with some 
binding. For example
{% highlight javascript %}
function greaterThan(m) {
  return function(n) {
    return (n > m );
  }
}
var greaterThan10 = greaterThan(10);
{% endhighlight %}
It creates a confusion given that somehow it mixes up binding `m` within 
the anonymous function which is returned from within `greaterThan`. 
The other highlights were 
* The usage of `apply` which allows argument passing between wrapper function
and the function which it calls into. The `null` argument is right now unexplained.
It would have been better to describe the difference with `f(arguments)` as well.
{% highlight javascript %}
function transparentWrapping(f) {
  return function() {
    return f.apply(null, arguments);
  };
}
{% endhighlight %}
* JSON is officially introduced. `JSON.stringify` and `JSON.parse` are friends.
* A custom reduce function was written to handle a specific case where the
family tree needs to be simplified without making a mistake in the Math. Important
points to note are that none of the standard higher order functions listed above
seemed to work out in this usecase. The usage of `valueFor` could have been done
away by recursively calling `reduceAncestors`, but this is much more convenient.
Value for a person would be a function of his value, and parents' value combined
by the reducing function f.
{% highlight javascript %}
function reduceAncestors(person, f, defaultValue) {
  function valueFor(person) {
    if (person == null)
      return defaultValue;
    else
      return f(person, valueFor(byName[person.mother]),
                       valueFor(byName[person.father]));
  }
  return valueFor(person);
}
{% endhighlight %}
* `bind` is a magic function which can be used instead of writing wrapper
functions to bind values and return them. Instead just calling bind on the function
followed by arguments seems to do the trick. There is a `null` being passed
to bind, which is the similar guy to the one in `apply`.
