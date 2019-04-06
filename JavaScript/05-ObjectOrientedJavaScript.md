# Object Oriented Programming
It is a programming paradigm where an object is a box containing information and operations that refer to the same concept. Its like we are modeling real world objects.

For example, an object representing a car would have properties, like make, model, and year, and methods, like engineOn, driveForward, and park.

The properties allows us to keep track of the state of the object and the methods allow us to manipulate the state of the object to model the real world.

In object oriented oriented programming we want to look at the real world and what we want to do and organize our code into these small object oriented boxes. Everything is divided and organized.

There are two main types of OOP:
* class-based OOP
* prototype-based OOP 

# Factory Functions
Functions that create objects for us. In the example below, if we need to create 1000 elfs we just run the createElf function and store it in a variable. GREAT! The drawback is that each elf is stored in a different place in memory. This is great for the name and weapon because they will be different for each elf, BUT the same attack function will be stored in 1000 different places in memory. Now imagine if we had ten different function in each object!
```js
function createElf(name, weapon) {
  return {
    // this is ES6 syntax for name: name, weapon: weapon
    name,
    weapon,
    attack() {
      return `Attack with ${weapon}!`;
    }
  }
}

const peter = createElf('Peter', 'stones');
peter.attack(); // Attack with stones!

```

# Object.create()
We can use Object.create to improve on the factory function above.

```js
// We create an object with the attack function. This way we are referencing the attack function instead of recreating the same attack function 1000 times.
const elfStore = {
  attack() {
    return `attack with ${this.weapon}`;
  }
}

function createElf(name, weapon) {
  // We create a new object from elfStore. This creates prototypal inheritance between the elfStore object and the newElf Object
  let newElf = Object.create(elfStore);
  // We attach the name and weapon properties to newElf
  newElf.name = name;
  newElf.weapon = weapon
  return newElf
}

const peter = createElf('Peter', 'stones');
peter.attack(); // Attack with stones!
```
But this is still not used very much out in the field.

# Contructor Functions
Before Object.create() there were constructor functions.
There are two types of constructors: native (aka built-in) constructors like Array and Object (this is what is used when we create our own arrays and objects), which are available automatically in the execution environment at runtime; and custom constructors, which define properties and methods for your own type of object.

A constructor is useful when you want to create multiple similar objects with the same properties and methods.

* All constructor function are called with the 'new' keyword.
* All constructor function names must start with a capital letter.
* All constructor functions have a prototype property that we can attach things to
```js
// with a constructor function we don't return anything. Here, we are basically constructing an elf. The only way to add properties to the constructor function is with the 'this' keyword
function Elf(name, weapon) {
  this.name = name;
  this.weapon = weapon.
}

// Because Elf is a constructor function, we can use the prototype property to attach the attack method.
Elf.prototype.attack() = function() {
  return `attack with ${this.weapon}!`;
}

// all constructor functions need the 'new' keyword to be invoked.
// The 'new' keyword creates a new object and assigns 'this' to peter
const peter = new Elf('Peter', 'stones');
// now we have access to peter
peter.name; // Peter

// peter doesn't have the attack method, but goes up the prototype chain to find it. 
peter.attack // Attack with stones.
```

SIDENOTE: What would happen if we used an arrow function when we attached the attack method above?

this.weapon would be undefined because arrow functions are lexically scoped. It defines 'this' based on where it is written. In this case it is written inside the Elf object, not peter. The regular function() syntax is dynamically scoped.
```js
Elf.prototype.attack() = () => {
  return `attack with ${this.weapon}!`;
}
```

Constructor functions and prototypal inheritance in JS is not very pretty. You will see it more in older code bases. 


# Classes
With ES6 we finally got the 'class' keyword. A class is a blueprint of what we want to create. With classes and OOP, we want to keep all the relevant functionality/methods and data/properties together in one box.

When we create an object from a class, it is an instance of that class. For example, if we build an elf named Peter, Peter is an instance of the Elf class. This is also called instantiation.

```js
// The Elf class is the blueprint to build elfs. Any time we need to make chnages or updates to the Elf class, we can make those changes in one place and all the objects that were instantiated from the Elf class will get the change or update.
class Elf {
  // the constructor function runs every time we instantiate a new object from the class or when we use the 'new' keyword on a class.
  constructor(name, weapon) {
    this.name = name,
    this.weapon = weapon
  }
  attack() {
    return `Attack with ${this.weapon}`
  }
}

// We build an elf named Peter from the Elf class with the 'new' keyword. This is called instantiation. 
const peter = new Elf('Peter','stones')
console.log(peter.attack());
```

SIDENOTE: Classes in JavaScript are still using prototypal inheritance under the hood. Classes are syntactic sugar and allow us to better organize our code. 

## In the above example, why is the attack function outside of the constructor function?

When we instantiate an object from a class, in this case Peter, the constructor function runs and this.name and this.weapon are put into a new memory space. When we create another instance of Elf, lets say Sally, the properties in the constructor function for Sally are put into a different memory space because Sally is a completely different object than Peter.

The attack method is left outside of the constructor function because it is the same for each instance. If we put it inside the constructor, we would be creating the same method in different memory spaces. It is inefficient. By leaving it outside, the method lives in one place in memory and each instance of the class can find it through the prototype chain.

# 'this' 4 ways
## 'new' Binding
```js
function Person(name, age) {
  this.name = name;
  this.age = age;
}
// With constructor functions the 'new' keyword binds 'this' to person1
const person1 = new Person('James', 40);
```

## implicit Binding
```js
// When we use 'this' inside an object, it is implied that 'this' references that object.
const person = {
  name: 'karen',
  age: 40,
  hi() {
    console.log(`hi ${this.name}`)
  }
}
```

## explicit binding
```js
// explicit is when we dictate exactly what 'this' should reference
const person = {
  name: 'karen',
  age: 40,
  hi: function() {
    // here we use bind to tell it to bind to the window object.
    console.log('hi' + this.setTimeout)
  }.bind(window)
}
```

## arrow function binding
```js
// 'this' is dynamically scoped. Arrow functions are lexically scoped. So, when we use an arrow function 'this' binds to the object where it was called. 
const person = {
  name: 'karen',
  age: 40,
  hi: function() {
    // if we didnt use an arrow function here, because innerFunction is a function within a function, 'this' would bind to the window object instead of person. 
    var innerFunction = () => {
      console.log('hi' + this.name)
    }
    return innerFunction()
  }
}
```

# Inheritance
Inheritance is passing knowledge down. We can use inheritance to create a new class by extending a base/super class.

```js
// In our imaginary game, every character in the game has a name, a weapon, and the attack method.
class Character {
  constructor(name, weapon) {
    this.name: name,
    this.weapon: weapon
  }
  attack() {
    return `Attack with ${this.weapon}`;
  }
}

// But what if we had a character in the game that had other special abilities (methods) or properties. We could create another class like below, but this would be inefficient because we are rewriting the same code. And we are storing the exact same attack function in two places in memory. 
class Ogre {
  constructor(name, weapon) {
    this.name: name,
    this.weapon: weapon
  }
  attack() {
    return `Attack with ${this.weapon}`;
  }
}

// Instead of creating a new separate class, we can extend the character class to create a subclass called Ogre. This is called subclassing. By extending the Character class, we inherit all of its properties and methods.

// we use the 'extends' keyword to inherit from the Character class
class Ogre extends Character {
  constructor(name, weapon, health) {
    // when we extend a class, in order to use 'this' inside of the constructor, we have to call the super constructor function. 'super' calls the construnctor function in the super class, in this case Character.
    super(name, weapon);
    this.health: health
  }
  // In our game, an Ogre has a name, weapon, and can attack just like any other Character in the game, but it also has the ability to heal itself.
  heal() {
    return `Health 100%`;
  }
}
```

## Public vs Private
In javascript the idea of public and private properties and methods is still in the works. In other languages pulic and private can be set.

# The 4 Pillars of OOP
## Encapsulation
We put things into objects or containers to model the real world. These boxes can interact with one another through their methods. This makes code easier to maintain. 
## Abstraction
Hiding the complexity from the user. You just instantiate a class with all the properties and methods. 
## Inheritance
We can inherit the properties and methods from other classes. We can save memory by sharing methods and avoid having to rewrite the same code. 
## Polymorphism
The ability to call the same method in different objects and each object responds in different ways. 

# The benefits of object oriented programming:
* code is clearn and understandable
* code is easy to extend
* code is easy to maintain
* code is memory efficient
* code is DRY