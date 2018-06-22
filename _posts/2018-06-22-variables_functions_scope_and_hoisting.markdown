---
layout: post
title:      "Variables, Functions, Scope, and Hoisting "
date:       2018-06-22 14:02:08 +0000
permalink:  variables_functions_scope_and_hoisting
---


After learning Ruby, I thought learning another programming language would be easier. And it was. But like any language, Javascript comes with its own quirks. I was tasked with quikcly learning some key aspects of javascript that distinguish it from Ruby. 

**Variables**

First things first: naming. 

There are three important conventions to follow when naming Javascript variables:
1. Gotta start those variables with a lower case letter. Starting it with an capital letter is a sure way to invalidate it! 
2. Javascript variables should be written as camelCaseVariables (as opposed to snake_cased_variables).
3. Lastly, refrain from using JavaScript reserved words.


Now, how exactly do we make new variables in JS?
Unlike Ruby, in JS variable creation is a two-step process:
1. Variable declaration (at which point the JS engine stores the declared variable in memory, without a value)
2. Assign a value to the variable 

Upon declaration, all variables are automatically assigned the value of undefined. It's only after we assign a new value that the variable will contain something other than undefined.

Certain types of variables, which we will discuss below, allow for simultaneous declaration and assignment in the same  line of code.


**Variable Types**

Now let's talk about the different kinds of variables!

There are 3 ways of setting variables in Javascript:
1. Var
2. Let
3. Const

We are going to talk about all of them...

*Var*

The var reserved word is the classic way to declare a variable. It's the oldest form of variable declaration in javascript

With var, a variable can be redeclared with no problem (sorta):

```
var e = 2.71828;
//=> undefined

e = 2.71828
 
e = "a famous irrational number, and is one of the most important numbers in mathematics";
//=> "a famous irrational number, and is one of the most important numbers in mathematics"
 
e = a famous irrational number, and is one of the most important numbers in mathematics
```

var comes with a ton of baggage in the form of scope issues — which we will discuss in the lesson on scope in JavaScript — and by allowing developers to play a little too fast and loose with variable declarations.

I said "sorta" before with regards to the ease with which we can redeclare variables set with *var* because, well, it causes some problems, too. 
For instance, with var, no error occurs if you declare a variable twice. This isn't so ideal because variable *re*declaration is often the result of a mistake by a developer unaware that the variable had already been declared.

Var also poses all sorts of scope issues. 

Luckily, ES2015 introduced two new ways to create variables: let and const. Both let and const are useful for a couple of reasons:
1. Both solve the scope issues posed by var 
2. Both send an error when a variable is declared a second time.

Let's get into the nitty gritty.

*let*

Like var, variables declared with let can be *reassigned*. What makes let better than var, though, is that you cannot *redeclare* it without drawing an error.  

```
let e = 2.71828;
//=> undefined

e = 2.71828
 
e = "a famous irrational number, and is one of the most important numbers in mathematics";
//=> "a famous irrational number, and is one of the most important numbers in mathematics"
 
typeof e;
//=> "string"
```

Still, there's yet a safer option to use when declaring variables: const.

*const*

Declaring a variable with const means you can neither reassign the variable's value *or* redeclare the variable. Why does this matter, you ask?

Here're a couple reasons:
1. When we assign a value to a variable declared with const, that variable will always represent that value.
2. It makes it easier for other developers to follow our code when the variable has the same value throughout our code. 

Only caveat to using *const* is that you gotta assign a value to the variable upon its declaration becuase *const* doesn't allow for assignment after declaration.

So...when should you use each type of variable?
* Var: never (or as infrequently as possible).
*  Let: if you know the value of the variable will have to change (like with counters in looping/iteration).
*  Const: every other situation. 

**Functions**

Now that we've explained some key points about variables, *let*'s (see what I did there) dive into another fundamental aspect of JavaScript: functions!

According to Learn's module: 
> A function is an object that contains a sequence of actions (JavaScript statements) that we can execute whenever we want and however many times we want. 

JS functions, like ruby methods, can accept a  inputs, operate on those inputs internally, and output or return a value out of it.

*Function Declaration*

When declaring a function, there are a few things to keep in mind:
1. The number of inputs it should accept.
2. The intended output or return value.
3. The operations that turn the input into the intended output.

There are a few different ways to declare a new function in JavaScript, but the primary one is in a function statement with the function keyword:

```
function myFunc (inputOne, inputTwo, etc...) {
  // Code to execute
}
```

When the JS engine sees the function keyword, it creates a new function object and stores it in memory, kinda like it does when it sees a variable keyword. 

JS function naming-conventions follow those of JS variables:
1. Must start with a letter
2. useCamelCase
3. Can't use JS reserved keywords like "function".

The syntax for functions are a bit more elaborate than variables, though. 

Functions must include:
1. Parentheses — ( )
The pair of parentheses following the name of the function contains a comma-separated list of parameters (mere placeholders for the actual inpt values):
```
function teamOrganizer (manager, analystOne, analystTwo) {
  // Code to execute
}
```
2. Curly Braces — { }
inside the curly braces lies the function body, or the function's internal operations set of statements. It's basically just a block of code. It is important to note, for purposes of scope (which we will get to soon) that inside the function body, the passed-in arguments become local variables that are only available inside the function. 

It is also important to note that when a function is invoked, it will always return a value. By default, however, its return value is undefined, unless otherwise specified:
```

function  teamOrganizer  (manager, analyst, coffee) {
  console.log(`Good morning, ${manager}. Here's the coffee you asked for.`);
	console.log(`Thanks ${analyst}!`)
 
  return coffee;
}
 
teamOrganizer('Bob', 'Joe', 'espresso' );
// LOG: Good morning, Bob. Here's the coffee you asked for.
// LOG: Thanks Joe!
// => "espresso"
```

*Anonymous Functions vs. Named Functions*

The two most common ways to create a function in javascript are by using the function declaration or function operator. Anonymous functions are created using the function operator.

Anonymous functions are functions that are dynamically declared at runtime. They’re called anonymous functions because they aren’t given a name in the same way as normal functions.


If the function keyword appears first in the statement and is followed by a function name, the function is being created by a function declaration:

Here’s a  enample of a named function:

```
function sayGoodMorning()
{
  alert("Good Morning!");
}
sayGoodMorning();
```

Anonymous functions, on the other hand, are declared using the function operator instead of the function declaration. You can use the function operator to create a new function wherever it’s valid to put an expression. For example you could declare a new function as a parameter to a function call or to assign a property of another object.

Here’s the same example created as an anonymous function:

```
var sayGoodMorning = function()
{
  alert("Good Morning!");
}
sayGoodMorning();
```

*So what are the pros to using the different types of functions?*
With named functions, the function’s name can be used to call the function from inside the function itself. That can be useful for recursive functions.

```
var howToBrightenSomeonesDay = function sayGoodMorning() {
  if(!beforeNoon)
    sayGoodMorning();
  else
    alert("It's not morning anymore...);
}
howToBrightenSomeonesDay();
```

It can also useful for debugging because you can see the function’s name in a call stack. Anonymous functions generally all look the same in the call stack. If you have a nasty debugging situation, sometimes giving names to the functions you are interested in can make things clearer.

On the other hand, not having to set a name for an anonymous function is a matter of convenience. In most cases the name of the function doesn’t really matter. Most of the time anonymous functions and named functions will both do any job perfectly well.

**What about Arrow Functions?**

Arrow functions look like this:

```
const arrowFunc = () => {
  return 'Arrow functions look cool'
};
```

Arrow functions are just like regular functions:
1. the body of an arrow function is declared inside the { } brackets. 
2. The function's parameters are declared in the parentheses before the arrow, which points to the body of the function.

There's a little technical difference between arrow functions and regular functions, however. Unlike regular functions, an arrow functions withoutout the curly braces from around the function body or replacing them with parentheses still gives us implicit returns [assuming we wrote the arrow function without brackets]. 

Note: *All arrow functions are anonymous. This is unlike regular functions, which take their names from their identifiers, which arrow functions do not possess.*

So, why use arrow functions?

Normally, when a function is called from another function, the context is global. But with arrow functions, the scope is the same as the scope of the function in which the arrow function is invoked. Let's see it:

```
  const boss = {
    firstName: 'Bob',
    greet: function() {
      return () => {
        return `Hi, I'm ${this.firstName}`
      }
    }
  }
  boss.greet()()
  // "Hi, I'm Bob"
```

**Scope**

Finally, we have arrived at scope, a super important concept in JS. 

Let's look at scope in*Learn's* terminology:
> Scope is, in short, the concept of where something is available. In the case of JavaScript, it has to do with where declared variables and methods are available within our code.

Taking a step back, every line of JavaScript code is run in what's called a JS execution context, where we have access to all of the variables and functions declared in that context. Within any given execution context, we can write an expression that references a variable or invokes a function declared in the same context. 

```
// 'myFunc' is declared in the global scope:
function myFunc () {
  return 2;
}
// => undefined
 
// 'myVar' is able to reference and invoke 'myFunc' because both are declared in the global scope:
const myVar = myFunc() * 2;
// => undefined
 
myVar;
// => 4
```

Try invoking a function declared out of context and you will end up with either some errors or undefined value spaces. 

*Global Scope*
If a variable or function is not declared inside a function or block, it's in the global execution context.

*Function Scope*
A function creates its own scope. So when inside a function, you're not  in the global execution context. This means that inside the function's body you can reference variables or functions declared either in the function or any parent scopes, but something outside the function cannot reference variables in the function:

```
function myFunc () {
  const myVar = 2;
}
// => undefined
myVar * 2;
// Uncaught ReferenceError: myVar is not defined
```


*Block Scope and Variables Scoping*
Since ES2015 came out, JavaScript has partial support for block scoping.

Some important info about scoping and variables:
* Variables declared with var are not block-scoped:
```
if (true) {
  var myVar = 2;
}
myVar;
// => 2
```

* Variables declared with const and let are block-scoped:
```
if (true) {
  const myVar = 2;
  let myOtherVar = 3;
}
myVar;
// Uncaught ReferenceError: myVar is not defined
myOtherVar;
// Uncaught ReferenceError: myOtherVar is not defined
```
*

By the way, make sure to use variable declaring keywords, becuase all variables created without a const, let, or var keyword are always globally-scoped, no matter where you declare it. This can lead to all sorts of messy confusion, so make sure to use those keywords!!!

**Scope Chain**

Every function in JavaScript has access to a scope chain. All this means is that functions can reference objects declared above (or outside) its scope, but not objects declared in inner functions.

Essentially, functions declared at the top level of a JS file are in the global scope. When that new function is invoked, it can access all of the variables and functions declared in the global scope. This means that when called, the function creates a new scope but can still reference objects in the global scope. A function inside the first function would have access to objects in both the outer function's scope and global scope, but things in the outer function and global scope wouldnt be able to access objects in the inner (second function). 

This works:

```
const globalVar = 11;
function firstFunc () {
  const firstVar = 12;
  function secondFunc () {
    const secondVar = 13;
    return secondVar + firstVar + globalVar;
  }
  const resultFromSecondFunc = secondFunc();
  return resultFromSecondFunc;
}
firstFunc();
// => 36
```

But this doesn't because the first function doesnt know what `secondVar` is:
```
const globalVar = 11;
function firstFunc () {
  const firstVar = 12;
	return secondVar + firstVar + globalVar;
  function secondFunc () {
    const secondVar = 13;
  }
  const resultFromSecondFunc = secondFunc();
  return resultFromSecondFunc;
} 
firstFunc();
// => undefined
```


**Hoisting**

This brings us to hoisting.

Hoisting deals with how function and variable declarations seem to get 'hoisted' to the top of the current scope. 

But let's take a step back. Because the JS engine reads a JS files from top-to-bottom, you'd think you'd have to declare a variable before referencing it:

```
function myFunc () {
  return 'Good Morning!';
}
myFunc();
// => "Good Morning!"
```

However, this also works:
```
myFunc();
// => "Good Morning!"
function myFunc () {
  return 'Good Morning!';
}
```

Why?

The answer lies in the JS file reading process:
* During the compilation phase, the JS engine looks for object declaration which it stores in memory, meanwhile skipping  over the actual invocations.
* When the JS engine reaches the execution phase, the object has already been created in memory. So when the engine sees its invocation it knows exactly what to call already.

As cool as hoisting sounds, it comes with a number of issues. However, following a few simple rules will make things much simpler:
1. Declare all functions at the top of their scope. 
2. Only use const and let (avoid var at all costs!).

It is noteworthy that in JavaScript, hoisting applies only to variable declarations (not assignments). So even if you assigned a value when declaring the variable,   the JavaScript engine recordes the variable's existence but maintains an undefined value. As a result, the variable will remain undefined until it's assigned a different value during the execution phase. 

As a result:

```
function myFunc () {
  console.log(sayGoodMorning);
 
  var sayGoodMorning = 'Good Morning!';
 
  return sayGoodMorning;
}
 
myFunc();
// LOG: undefined
// => "Good Morning!"
```

What's going on here? Essentially, the JS Engine saved a memory of the variable name in the compilation phase, but not its value. The `  console.log(sayGoodMorning);` line was invoked before the variable declaration and as a result, even though the engine knew what the variable was, it didnt yet record its value. 


