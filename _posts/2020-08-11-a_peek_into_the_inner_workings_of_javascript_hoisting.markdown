---
layout: post
title:      "A peek into the inner workings of JavaScript Hoisting"
date:       2020-08-11 22:17:08 +0000
permalink:  a_peek_into_the_inner_workings_of_javascript_hoisting
---


In JavaScript, there were several concepts which were a bit more tricky to understand than in Ruby and Rails: from DOM manipulation to asynchrony and advanced functions, many things took me a bit out of my comfort zone during this module. One of the harder things for me to understand, though, was hoisting.

Hoisting itself can be conceptually understood as “moving all variables and functions to the top of a scope.” This happens automatically every time you run your code. Let’s say that you’ve written the following:
```
function animal_sound(animal, sound) {
   return `The ${animal} goes ${sound}!`
}
 
console.log( animal_sound("cow", "moo") )
```
This is typically how it’s taught to use functions. First, you declare the function, and then you can call it below. In this case, we’re printing the output of the function ```animal_sound``` to the console, which, with the arguments we’ve entered, should be “The cow goes moo!” 
However, with hoisting, we can use functions that were declared further down in the code! Let’s say, for example, we want to output the ```animal_sound``` function earlier than we had in the first example. We could utilize hoisting and easily do this:
```
console.log( animal_sound("cow", "moo") )
 
function animal_sound(animal, sound) {
   return `The ${animal} goes ${sound}!`
}
 
console.log( "I am ran after the function call!" )
```

Although there isn’t any function named ```animal_sound``` defined above the first ```console.log()```, we still get the same result! This is because the function is, in a sense, brought all the way up to the top during the compile phase.

...except this isn’t actually what’s happening. What’s really happening behind the scenes is that your code is getting scanned for all of the function and variable declarations that’re contained within it. Once the code is scanned, all of those are loaded into memory in the form of a data structure called the “Lexical Environment.” When you call a function or a variable before it’s been defined, you’re really calling it from the lexical environment, creating an illusion that the function and variable declarations were moved to the top of the scope when, in fact, they’re still right where they were before. 

This redefinition of what really happens when variables and functions are hoisted is critical to understanding where a majority of the bugs and issues that arise while utilizing hoisting come from. Another critical component of hoisting, however, is that hoisting only applies to function and variable declarations, not assignments or initializations.

For example, let’s say that you have the following code:
```
my_function()
 
let my_function = function() {
   console.log("Hello!")
}
```
	In this instance, you’ll get a ```ReferenceError: cannot access ‘my_function’ before initialization```. This is primarily because we haven’t hit the line that assigns the variable ```my_function``` to a function expression, meaning that in the lexical environment, the variable is still uninitialized. 

