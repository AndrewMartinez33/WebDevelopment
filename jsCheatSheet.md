# Strings
```js
// concats arguments to the calling string, returns a new string.
String.concat('string1', 'stringN')

// determines if one string is in the calling string, returns true or false
String.includes('string')

// Returns the index within the calling String object of the first occurrence of the specified value, or -1 if not found.
String.indexOf('string')

// Returns the index within the calling String object of the last occurrence of the specified value, or -1 if not found.
String.lastIndexOf('string')

// Used to find a match between a regular expression and a string, and to replace the matched substring with a new substring.x
String.replace(regEx, 'replacement')

// Extracts section of calling string from beginIndex to endIndex (not included). If you use negative number, then it starts at the end of the string. Providing first arg only returns the string beginIndex to the end.
String.slice('beginIndex', 'endIndex')

// Splits a string into an array using separator to determine where to make each split. If arg is left empty, the entire string will be one item in the array
String.substring('separator')

// Converts string to all lower case letters
String.toLowerCase()

// Converts string to all lower case letters
String.toUpperCase()
```


# Arrays
```js
// Remember that arrays are objects, therefore they are passed by reference. To create a new array from another array:
let arr1 = [1, 2, 3];
let arr2 = [...arr1]; // creates new array
let arr2 = Array.from(arr1); // creates new array
let arr3 = [].concat(arr1); // creates new array


Array.findIndex()
Array.forEach()
Array.includes()
Array.indexOf()
Array.join()
Array.keys()
Array.pop()
Array.push()
Array.reverse()
Array.shift()
Array.slice()
Array.some()
Array.splice()
Array.toString()
Array.unshift()

Array.filter()
Array.map()
Array.reduce()
Array.sort()
```

# Objects
Objects are collections of key-value pairs.
```js
const person = {
  name: 'Andrew',
  run: function() { some code; }, // function inside an object is known as a method
  walk() { some code; }           // new method syntax in ES6
};

//Accessing properties: Dot Notation and Bracket Notation
// Use brackets when you don't know the property you are searching for ahead of time.
person.name;
person['name'];


// creates a new object from an existing object.
Object.create(sourceObject)

// returns an array whose elements are arrays of the key-value pairs in the object.
Object.entries(object)

// transforms a list of key-value pairs into an object
// [ [age: 30], [name: Andrew] ]
Object.fromEntries(list)

// returns array of object's key names.
Object.keys(object)

// returns array of object's property values.
Object.values(object)
```

# Object Destructuring
Destructuring allows us to extract data from arrays, objects, maps and sets into their own variable.

```js
//Sometimes you need to make a variable from something that is inside of an object.

const address = {
  street: "Jacinto",
  city: "Long Beach",
  country: "United States"
};

//We access the properties within the object like this:
const street = address.street;
const city = address.city;
const country = address.country;

//What we could do instead of creating multiple variables, we destructure them in a single line. This is basically saying get the values of properties street, city, and country from the address object and store them in variables named street, city, and country.
const { street, city, country } = address;

// What if you want to name the variable something different? You can use an alias like so:
const { street: myStreet, city: myCity, country: myCountry } = address;

//What if the value you are trying to set does not exist? You will get undefined unless you set a default value. Default values kick in ONLY when the value is undefined. You can set default values like so:
const { street = "unknown", phone = "unknown" } = address;

console.log(street); // Jacinto
console.log(phone); //unknown
```

# Loops
```js
// FOR LOOP
for (initial expression; condition; incrementExpression) {
  statements
}
for (let i = 0; i < 10; i++) {
  some code;
}

// WHILE LOOP
while (condition) {
  statements;
}

// DO WHILE LOOP
// runs code before checking condition
do {
  statements
} while (condition);

// FOR IN LOOP
// iterates over keys
for (variable in object) {
  statements
}

// FOR OF LOOP
// iterates over values
for (variable of object) {
  statements
}

// BREAK
// breaks out of innermost loop
for (variable of object) {
  break;
}

// CONTINUE
// terminates the current loop iteration and continues the next iteration
for (variable of object) {
  continue;
}

// NOTE: In JavaScript, Objects are not iterable unless they implement the iterable protocol. Therefore, you cannot use for…of to iterate over the properties of an object. Instead you have to use Object.keys or Object.entries, to iterate over the properties or entries of an object.
```


# Iterators & Generators
In JavaScript, Objects are not iterable unless they implement the iterable protocol. Therefore, you cannot use for…of to iterate over the properties of an object. Instead you have to use Object.keys or Object.entries, to iterate over the properties or entries of an object.




# Functions
```js
// FUNCTION DECLARATION
function functionName(parameters){
  statements;
  return;
}


// FUNCTION EXPRESSION
// anonymous function
let functionName = function(parameters) {
  statements;
  return
};


// ARROW FUNCTIONS
// A cleaner, simpler way of writing functions in ES6

// Arrow Function Syntax
(param, param) => { some code; };

// The Old Way
const funcName = function(parameter) {
  return parameter + parameter;
}

// The New Way
const funcName = (parameter) => { return parameter + parameter; };

// But if you have ONLY ONE parameter you can omit the parenthesis
const funcName = parameter => { return parameter + parameter; };

// If the body of the function only includes a SINGLE LINE and a RETURN, we can simplify even further by omiting the curly braces, return keyword, and semi-colon.
const funcName = parameter => parameter + parameter;

// If you have no parameters, use empty parenthesis
const funcName = () => some code;



// DEFAULT PARAMETERS
// you can give parameters default values
function funcName(name='Andrew', age=33) {
    console.log(`My name is ${name}, I am ${age} years old.`);
}
// this will pass the default parameters to console.log
funcName(); 



// REST PARAMETERS
// collects all remaining elements into an array. Rest parameters have to be the last argument. This is because it collects all remaining/ excess arguments into an array.

// This function call returns 3, this is because in Javascript it is possible to call a function with any number of arguments. However, only the fist two arguments will be counted.
function add(x, y) { return x + y; }
add(1, 2, 3, 4, 5) // returns 3

// With rest parameters we can gather any number of arguments into an array and do what we want with them. So we can re-write the add function like this:
function add(...args) {
  let result = 0;
  for (let arg of args){
    result += arg;
  } 
  return result
}
add(1,2) // returns 3
add(1, 2, 3, 4, 5) // returns 15

// We can separately define the first arguments, and the rest of the arguments in the function call (no matter how many they are) will be collected into an array by the rest parameter.
function xyz(x, y, ...z) {
  console.log(x, ' ', y);
  console.log(z);
  console.log(z[0]);
  console.log(z.length);
}
xyz("hey", "hello", "wassup", "goodmorning", "hi", "howdy")
// hey hello
// ["wassup", "goodmorning", "hi", "howdy"]
// wassup
// 4



// CURRYING
// the process of converting a function that takes multiple arguments into a function that takes the arguments one at a time.

const multiply = (a, b) => a * b;

// the curried version. think of it as a function within a function.
const curriedMultiply = (a) => (b) => a * b;

//to call it
curriedMultiply(3)(4); //would return 12

// if you only only supply one argument
// it would return a function
curriedMultiply(3); // would return (b) => a*b;

// but why use this? it makes things more extensible.
//  you could use curriedMultiply() to create another function.

//new function that multiplies everything by 5.
// you are supplying the first argument for curriedMultiply
const newCurry = curriedMultiply(5);

//to call it
//no you are supplying the second argument to curried multiply
newCurry(6); // returns 30.



// COMPOSE
// is the act of putting two functions together to form a third function where the output of one function in the input of the other.

// parameters 'f' and 'g' return a function that takes parameter 'a'
// parameter 'a' returns function 'f' that takes a parameter, function 'g', which takes in parameter a. 
const compose = (f,g) => (a) => f(g(a));

// now lets do something with it
const sum = (num) => num + 1;

// f is sum
// g is sum
// a is 5
// what happens when this runs?
// first, g(a) runs and returns 6
// the f(6) runs and returns 7
// so the result is 7
compose(sum, sum)(5);
```

# Spread Operator
The spread operator allows an iterable to expand in places where 0+ arguments are expected. Huh? Let's look at some examples:

```js

// Combining arrays
const array1 = [1, 2, 3];
const array2 = [4, 5, 6];

const array3 = array1.concat(array2);

//The above code works, but what if you wanted to add another element between the two arrays. The code would look a lot more complicated. Or we can use the spread operator to achieve this.

const array3 = [...array1, 'another element', ...array2];
>> [1, 2, 3, 'another element', 4, 5, 6]

// We can use it with the Math object
const maxNumber = Math.max(...array1);
>> 3

// We can create a new array from another array.
const newArray = array1;

// The above code creates a reference to the same array as array1. Any changes to newArray would be reflected in array1 as well. Instead we can use the spread operator to create a new array, seperate from the source array. This works because the value of array1 is spread into the new array as individual values and not as a reference of array1.
const newArray = [...array1];

// We can also use the spread operator to convert a string into an array.
const string1 = 'Hello';
const newArray = [...string1];
>> ['H', 'e', 'l', 'l', 'o']

// We can also use the spread operator on objects
const obj1 = { first: 'Andrew'};
const obj2 = { last: 'Martinez'};

const obj3 = { ...obj1, ...obj2, email: 'andrew@email.com' };
>> {first: 'Andrew', last: 'Martinez', email: 'andrew@email.com'}

// We can also use the spread operator to easily clone an object
const obj4 = { ...obj3 };
```


# Dates
```js
let event = new Date('December 17, 1995 03:24:00');
let event2 = new Date('1995-12-17T03:24:00');

// returns the number of milliseconds elapsed since January 1, 1970 00:00:00 UTC.
let event3 = Date.now();

// returns day of the month
Date.getDate();

// returns day of the week where 0 represents Sunday
Date.getDay();

// returns year of the specified date
Date.getFullYear();

// returns hour for the specified date
Date.getHours();

// returns milliseconds in the specified date
Date.getMilliseconds();

// returns minutes of specified date
Date.getMinutes();

// returns month of specified value. January = 0.
Date.getMonth();

// returns seconds in specified date
Date.getSeconds();

// returns milliseconds since Jan 1, 1970, 00:00:00.000 GMT
Date.getTime();

Date.setDate();
Date.setDay();
Date.setFullYear();
Date.setHours();
Date.setMilliseconds();
Date.setMinutes();
Date.setMonth();
Date.setSeconds();
Date.setTime();
```

# Numbers

# Math


# Classes
Often we need to represent an idea or concept in our programs — maybe a car engine, a computer file, a router, or a temperature reading. Representing these concepts directly in code comes in two parts: data to represent the state, and functions to represent the behavior. ES6 classes give us a convenient syntax for defining the state and behavior of objects that will represent our concepts.

```js
// We can use an object to represent a person.
const person = {
  name: "Andrew",
  walk() {
    console.log(this);
  }
};

// If we wanted to represent multiple people we could create multiple objects, but in this case we would be duplicating the walk method over and over. And if there was a bug in the walk method we would need to go into every person object and change the code.
const person = {
  name: "Jay",
  walk() {
    console.log(this);
  }
};

const person = {
  name: "Mike",
  walk() {
    console.log(this);
  }
};

// Instead, we can use classes to create a blueprint of a person and then create objects from that blueprint to represent different people.

// class name is capitalized
// The constructor's job is to initialize an instance to a valid state, and it will be called automatically so we can’t forget to initialize our objects.
class Person {
  constructor(name) {
    this.name = name;
  }
  walk() {
    console.log(this);
  }
}

// We create a person object with the 'new' operator and the Person class, passing in any parameters to the constructor function.
// Anytime an object is created from a class, it is called an instance of that class.
const person1 = new Person("Jessica");
```

# Inheritance
```js
class Person {
  constructor(name) {
    this.name = name;
  }
  walk() {
    console.log("walk");
  }
}

// The teacher class inherit the constructor properties and method from Person. Super is needed to initialize the constructor from Person.
class Teacher extends Person {
  constructor(name, degree) {
    super(name);
    this.degree = degree;
  }
  Teach() {
    console.log("teach");
  }
}

const teacher = new Teacher("Andrew", "Bachelors");
```

