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
// with a constructor function we don't return anything. Here, we are basically constructing an elf.
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