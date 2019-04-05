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
IIFE's were used to avoid global variable issues, like namespace collision.

```js
// with the first opening parentheses javascript doesn't see the function keyword, so this becomes function expression
// then we create an anonymous function and immediately call it with the final pair of parenthesis.
// no global property is created and everything inside of the function scope is private
(function(){
  // everything in here is only available within this IIFE
})();

var funcOne = function() {
  // b & c are in the local scope
  var b = console.log('hello');
  var c = console.log('goodbye');
  // b and c are private, but by returning this object it exposes these function for us to use as shown below.
  return {
    b: b,
    c: c
  }
};

funcOne.b; // hello
funcOne.c; // goodbye

```

# this Keyword
'this' is the object that the function is a property of.

The two main benefits of the 'this' keyword
* gives methods access to their object, and therefore access to their sibling properties and methods.
* we can execute the same code for multiple objects.

```js
// obj1 has some function and within that function we have access to the 'this' keyword, which refers specifically to obj1
obj1.someFunc(this)

// obj2 has some function and within that function we have access to the 'this' keyword, which refers specifically to obj2
obj2.someFunc(this)

// the 'this' keyword gives methods access to their object, and therefore access to their sibling properties and methods.
const obj3 = {
  name: 'Andrew',
  sing() {
    // we can use the 'this' keyword to access name within obj3. 'obj3.name' would not work here.
    return `la la la ${this.name}`;
  }
  singLouder() {
    // we can also use 'this' to practice DRY coding.
    return `${this.sing()}!!!!!!!`;
  }
}

obj3.sing(); // la la la Andrew
obj3.singLouder(); // la la la Andrew!!!!!!!

// the 'this' keyword allows us to execute the same code for multiple objects.
function importantPerson() {
  console.log(this.name);
}

// this variable is defined in the global scope
const name = 'Sunny';

// both obj4 and obj5 use the same importantPerson function
const obj4 = {
  name: 'Andrew',
  importantPerson: importantPerson
}

const obj5 = {
  name: 'Jessica',
  importantPerson: importantPerson
}

// calling the function on its own, 'this' refers to the global or window object
importantPerson(); // Sunny

// calling the same function from obj4, 'this' refers to obj4 not the global object
obj4.importantPerson(); // Andrew

// calling the same function from obj5, 'this' refers to obj5 not the global object
obj4.importantPerson(); // Jessica

```

# The issue with 'this'
Everything in JavaScript is lexically scoped. Where we write it determines what we have available. Except for the 'this' keyword. 'this' is dynamically scoped, meaning how the function is called determines what is available.

We can fix this issue with Arrow Functions because arrow functions are lexically bound.

```js
const obj ={
  name: 'Andrew',
  sing() {
    console.log('a', this);
    var anotherFunc = function() {
      console.log('b', this);
    }
    anotherFunc();
  }
}

// obj calls the sing method and sing calls the anotherFunc method. Since obj never called anotherFunc(), the 'this' keyword defaults to the window object. 
obj.sing();
// a {obj}
// b {window}
```

Here we use the arrow function

```js
const obj1 ={
  name: 'Andrew',
  sing() {
    console.log('a', this);
    // the arrow function lexically binds 'this' in anotherFunc to obj1
    var anotherFunc = () => {
      console.log('b', this);
    }
    anotherFunc();
  }
}

// because we use the arrow function, 'this' in both methods now reference obj1 
obj.sing();
// a {obj1}
// b {obj1}

```

# call() apply() bind()
We can use call and apply to borrow methods

```js
const wizard = {
  name: 'Merlin',
  health: 50,
  heal() {
    console.log(this.health);
    this.health = 100;
    console.log(this.health);
  }
}

const archer = {
  name: 'Robin',
  health: 30,
}

wizard.heal();
// Merlin 50
// Merlin 100

// we can use call to borrow the heal method from wizard and use it on archer. 
wizard.heal.call(archer);
// Robin 30
// Robin 100

// we can use call to borrow the heal method from wizard and use it on archer. 
wizard.heal.apply(archer);
// Robin 30
// Robin 100

// call and apply do the exact same thing and both can also take in parameter/arguments. The difference is that call takes in comma separated arguments and apply takes in an array of arguments to pass to the method 
wizard.heal.call(archer, argument1, argument2);
wizard.heal.apply(archer, [argument1, argument2]);
```

Like call() and apply(), bind() allows us to borrow methods. But unlike call() and apply() we cannot run the method right away. Instead, bind returns a function or 'this' to store for later use.

```js

const wizard = {
  name: 'Merlin',
  health: 50,
  heal() {
    console.log(this.health);
    this.health = 100;
    console.log(this.health);
  }
}

const archer = {
  name: 'Robin',
  health: 30,
}

// bind return the heal method with 'this' referencing archer, but it never calls it. 
wizard.heal.bind(archer);
// Robin 30
// Robin 30

// bind allows us to store the heal method referencing archer in a variable. Then we can call healArcher.
const healArcher = wizard.heal.bind(archer);
healArcher();
// Robin 30
// Robin 100

```