# JavaScript Types
## Primitive Types. Primitive types directly store a value
* numbers
* booleans
* strings
* undefined - absence of a definition
* null - absence of a value
* Symbol

## Non Primitive Types. Store a reference to the value. 
* objects

Arrays and function are objects

# Array.isArray()
Arrays are objects in JavaScript.

```js
let anArray = [1,2,3];
typeof anArray;
// type of would return object
```

If we need to figure out if an object is an array we can use Array.isArray();
```js
let anArray = [1,2,3];
// this returns true if an object is an array
Array.isArray(anArray);
// true
```

# Pass by Value vs Pass by Reference
Primitive types are passed by value.
Non primitive types are passed by reference.

```js
// when we assign variable a to variable b, the javascript engine copies the value and puts it in a new memory space. This is passed by value.
var a = 5;
var b = a;
// here we increment variable b, but it does not affect the value of variable a because we only passed the value of variable a when we defined variable b.
b++;

// variable c is passed by reference to variable d. The value of variable d points back to the memory space where variable c is stored.
var c = {hello: 'hello'};
var d = c;

// here we change the value of the hello property in variable d. Since variable d is referencing variable c, the change is made to the value in the same memory space where we stored variable c.
d = {hello: 'goodbye'};
c.hello; // goodbye

// the same thing happens with array since they are objects.
var arr1 = [1, 2, 3];
var arr2 = arr1;
arr2.push(4, 5, 6);

console.log(arr1); // [1, 2, 3, 4, 5, 6]
```
The benefit of pass by reference is that we save memory. But the problem is that its easy for someone to accidently change the values in an object.

## Creating a new copy of an object
To create a new copy of an existing object in a new memory space we can do the following.

```js
// for an array we can use concat()
var arr1 = [1, 2, 3];
var arr2 = [].concat(arr1);

// we can also use the spread operator
var arr1 = [1, 2, 3];
var arr2 = [...arr1];

// in objects we can use Object.assign
var obj1 = { a:'a', b:'b'}
var obj2 = Object.assign({}, obj1);

// again, we can use the spread operator
var obj1 = { a:'a', b:'b'}
var obj2 = {...obj1};
```

## What if we have an object within an object?
```js
// this object is stored in some memory space
var obj1 = {
  a: 'a',
  b: 'b',
  // c is another object and is stored in a different memory space. 
  c: {
    deep: 'hello';
  }
}

// We clone obj1 and store it in a new memory space
var obj2 = {...obj1};

// we change the value of the 2nd object inside of obj1
obj1.c.deep = 'goodbye';

// although we cloned obj1 and stored it in a new memory space, the 2nd object inside of obj2 is still referencing the change made to obj1.
// this happens because we only cloned obj1, which contained a second object. That second object was passed by reference and is still pointing back to the second object inside of obj1
console.log(obj2.c.deep); // goodbye

// In order to clone the entire object, including the inner object, and create a new object in a new memory space, we can use JSON
var obj1 = {
  a: 'a',
  b: 'b',
  c: {
    deep: 'hello';
  }
}

// this turns obj1 into a string, then back to an object. Giving us a new object to assign to obj2.
var obj2 = JSON.parse(JSON.stringify(obj1));

// note: using the JSON method can have performance implications if you have a large and deep object.

```

## If you need to compare objects
This works when you have simple JSON-style objects without methods and DOM nodes inside:
```js
JSON.stringify(obj1) === JSON.stringify(obj2) 

// The ORDER of the properties IS IMPORTANT, so this method will return false for following objects:
// x = {a: 1, b: 2};
// y = {b: 2, a: 1};
 ```

 # Type Coercion
 Type coercion happens when you use the == operator and you have two differes types of operands.
 We should always use === because there is no type coercion.