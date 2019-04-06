# Functions are Objects
When we invoke a function we automatically get a few things. The 'this' keyword and 'arguments' and we also get a local variable environment.



# First Class Citizens
Functions are first class citizens in JavaScript, which means they can be passed around as data. They can be assigned as values, they can be passed as parameter to functions, and they can be returned as values in function. Anything you can do with other types, you can do with functions in JavaScript.

# Something to watch out for in functions
* Don't initialize functions in loops. Instead, initialize them outside the loop and then call them from inside the loop.

# Higher Order Functions
A function that can take a function as an argument or a function that return another function.

## Why are they useful?
We are able to make code more general and flexible. Keeping our code DRY and not repeating ourselves.
```js
// multiplyBy is a function that return another function.
const multiplyBy = function(num1) {
  return function(num2) {
    return num1 * num2;
  };
}

// we can simplify the above function with arrow functions
const multiplyBy = (num1) => (num2) => num1 * num2;

// We are able to create different functions using the one multiply function
const multiplyByTwo = multiplyBy(2);
multiplyByTwo(4); // 8
multiplyByTwo(5); // 10

const multiplyByTen = multiplyBy(10);
multiplyByTen(4); // 40
multiplyByTen(5); // 50

```

# Pillar 1: Closures
Before a function runs, the engine already knows which functions have access to which variables. Usually when a function runs it gets pushed onto the stack. When the function ends or returns it is popped off the stack and the variables are sweeped from memory by garbage collection. BUT if there are variables that are referenced by other functions, JavaScript creates a closure and keeps them around. Closures are a feature of JavaScript.
```js
function a() {
  let grandpa = 'granpa';
  return function b() {
    let father = 'father';
    // when function b returns, mother is sweeped from memory by garbage collection because it is no longer needed and it is not being referenced in any other function. 
    let mother = 'mother';
    return function c() {
      let son = 'son';
      return `${grandpa} > ${father} > ${son}`;
    };
  };
}

a(); // func b
a()(); // func c
a()()(); // grandpa > father > son

```
# Closures and Memory
A benefit of closures is that they are memory efficient
```js
function heavyDuty(index) {
  const bigArray = new Array(7000).fill('hello');
  console.log('created bigArray')
  return bigArray[index];
}
// If we have a function that we call many times, it can be memory inefficient. Here we call heavyDuty() to access an item at a specific index. But every time we call heavyDuty() we re-create bigArray.
heavyDuty(600);
heavyDuty(601);
heavyDuty(602);
// created bigArray
// created bigArray
// created bigArray

// we can use closures to make this more efficient
function heavyDuty2() {
  const bigArray = new Array(7000).fill('hello');
  console.log('created bigArray')
  return function(index) {
    bigArray[index];
  }
}

// heavyDuty2 run and is pushed onto the stack. It returns a function, which is stored in getHeavyDuty, and then is popped off the stack. bigArray is kept in a closure because there is a reference to it in the returned function.  
const getHeavyDuty = heavyDuty2();
// now every time we run the getHeavyDuty function we are referencing the bigArray closure. No matter how many times the function runs, bigArray was only created once.
getHeavyDuty(600);
getHeavyDuty(601);
getHeavyDuty(602);
// created bigArray
```

# Closures and Encapsulation
We can use closures to limit access to certain variables that might be important. Closures hide information that is unnecessary to be seen or manipulated by the outside world.

```js
// 
const makeNuclearButton = () => {
  // timeWithoutDestruction is a closure because its referenced within the other functions.
  let timeWithoutDestruction = 0;
  const passTime = () => timeWithoutDestruction++;
  const totalPeaceTime = () => timeWithoutDestruction;
  const launch = () => {
    timeWithoutDestruction = -1;
    return '💥';
  }

  setInterval(passTime, 1000);
  // Here we give access to the totalPeaceTime function, but everything else is hidden. The information, in this case timeWithoutDestruction, is not directly accessible, but we can still use the information through the totalPeaceTime function.
  return {totalPeaceTime}
}

const ww3 = makeNuclearButton();
ww3.totalPeaceTime()
```

# Pillar 2: Prototypal Inheritance 
Inheritance is an object getting access to the properties and methods of another object through the prototype chain.

from the base object we create the base array, and base function. From this base array and base function we can create other array and functions.


```
        |---prototype--chain--- BASE ARRAY --------- arrayOne
        |
BASE    |
OBJECT  |---prototype--chain--- BASE FUNCTION ------ functionOne
        |
        |
        |---prototype--chain--- objectOne
```

## How do we go up the protype type and inherit properties and methods
```js
let dragon = {
  name: 'Fyre',
  breathe() {
    console.log('FIREEEEEEE!');
  }
}

let lizard = {
  name: 'Jamie',
  run() {
    console.log('Ruuuuuunnnnn!');
  }
}

// this doesn't work because we don't have access to the breathe method.
lizard.breathe(); //undefined

// we can inherit the breathe property by setting the __proto__ property to dragon. We inherit the properties and methods from dragon, but anything that we already have defined overrides the inherited property or method.
lizard.__proto__ = dragon;
lizard.breathe(); // FIREEEEEEE!
```

We are not copying the properties and methods, __ proto__ is pointing to or referencing the prototype object in the next object up the protype chain. This pattern continues until we get to the Base Object.

Note: For performance reasons we should never use __ proto __, there are other ways to inherit.

