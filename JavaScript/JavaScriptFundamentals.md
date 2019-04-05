# Execution Context
The first thing the JS engine does when it runs a JS file is it creates the global() execution context and pushes it onto the stack. The global execution context gives you two things, the 'global object' and 'this'. Then, when the JavaScript engine runs the code and it ecounters a function it creates a new execution context for that function and pushes it onto the stack.

# What is Lexical Environment
Where you write something. In JavaScript our lexical scope (available data + variables where the function was defined) determines our available variables. 

```js

// This function is in the global lexical environment
function findOne(){
  // This function is in the findOne lexical environment
  function findTwo(){
    return;
  }
  return;
}

```

# Hoisting
The movement of variables and functions to the top of their respective environments. 


* variables declared with the var keyword are hoisted, but the value is not. If you try to access the value before it is declared, you will get undefined.
* let and const variables are hoisted, but you cannot access them before they are declared.
* Only functions declared with the function keyword are fully hoisted.
* function expression ( var aFunction = function(); ) are hoisted like variables.

# Function Invocation
A function expession is defined at runtime when we actually invoke/call/execute the function.
Function declarations are defined at parse time when the engine looks at the code and starts hoisting and allocating memory

When a new execution context is created for a function, 'this' is created, and you also get an 'arguments' object {}. Arguments contains the arguments that are passed into the function. If no arguments are passed in, an empty arguments object is still created. The arguments object can only be accessed within the lexical context of the function. If you need to use the arguments object, you should use the spread operator or the Array.from() method as shown below. This turns the arguments object into an array.

```js
// Function Expression
var funcOne = () => {
  console.log('hello');
}

// Function Declaration
var funcTwo = (...args) => {
  // using the spread operator to access arguments OR
  console.log(args);
  // using Array.from to access arguments
  console.log(Array.from(arguments));
}

// Function invocation/call/execution
funcOne();
funcTwo();

```

# Scope Chain
Every function has access to variables within its own variable environment. Functions also have a link, called the scope chain, that gives it access to variables in its parent. A function first looks for a variable in its own environment. If it doesn't find the variables, it goes up the scope chain to find the variable until it hits the global scope.

```js

function one(){
  var a = 'a';
  // variables b and c are would not accessible because a function can't look down the scope chain.
  return function two(){
    var b = 'b';
    // variable c would not be accessible because a function can't look down the scope chain.
    return function three(){
      var c = 'c';
      // variable a is accessible because it can go up the scope chain to find it.
      console.log(a);
      // variable b is accessible because it can go up the scope chain to find it.
      console.log(b);
      // variable c is accessible because its in the local scope.
      console.log(c);
    }
  }
}

```

# Function Scope vs Block Scope
JavaScript uses functional scope, meaning that a new lexical environment is only created when a function is created. Most other languages use block scope.

```js
// the 'block scope' would be between the curly braces. If there was block scope, the 'secret' variable would not be accessible outside of the if statement.
if (5 > 4) {
  var secret = 2;
}
console.log(secret); // 2

// the function creates a new scope or lexical environment and 'secret' is not accessible outside of the function.
function scope() {
  var secret = 2;
}
console.log(secret); // secret is undefined

```

The introduction of const and let gave JavaScript block scope
```js
if (5 > 4) {
  const secret = 2;
  let word = 'stuff';
}
console.log(secret); // secret is not defined
console.log(word); // word is not defined

```

# IIFE - Immediately Invoked Function Expression
IIFE's were used to avoid global variable issues. 

```js
// with the first opening parentheses javascript doesn't see the function keyword, so this becomes function expression
// then we create an anonymous function and immediately call it with the final pair of parenthesis.
// no global property is created and everything inside of the function scope is private
(function(){
  // something here
})();

var funcOne = function() {
  
};

```