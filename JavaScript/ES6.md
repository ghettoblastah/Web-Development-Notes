# ES6 additions

## Table of Content

- [Const and Let](#Const-and-let-vs-var)
- [Arrow Functions](#Arrow-functions)
- [Default paramenters in functions](#Functions-with-default-parameters)
- [Destructuring Aassignments](#Destructuring-assignments)
- [Spread Operator](#Spread-operator)
- [Rest Operator](#Rest-operator)
- [OOP Implementations](#OOP-alike-implementations)
- [Import, Export and Default Export](#import-and-export))
- [Functional Programming: map, filter and reduce](#Functional-programming-methods)
- [PadStart and PadEnd](#PadStart-and-PadEndMethods)

---

## Const and Let VS Var

We've seen the introduction of two new ways of declaring variables:

- Const
- Let

### Const

It's the reserved keyword for declaring _constant_ variables, for those identifiers that can't be reassigned.
The important thing to note here, is that they are not immutable datatypes. A **const** object can have it's properties reassigned. The only things that can't change is the reference to the data type.

```javascript
const person1 = {
  name: "Mike",
  age: 21,
  gender: "male"
};

person1.name = "Rob";
console.log(person1.name); // Rob
```

Under this directive, we're seeing more often developers abusing the keyword const before declaring functions, arrays, objects... My initial thoughts about it were that they were going to be used as a THIS_IS_A_CONSTANT word, and leave **Let** for the other cases. But I was utterly wrong.

Therefore, as a rule of thumb, we should always try to use **const**, as it's dead simple to change a variable to **let** if we see later on that we need to reassign it.

### Let

Since we're going all the way with **Const**, **Let** should be reserved for loops and other cases not mentioned above.

It's encouraged to drop the use of **var**. At the moment of writing these notes, and having transitioned to ES6 for almost a year ago, I must say I haven't used it a single time. But, in theory, there's a use-case that we need to denote:

-> The **var** keyword works on a enclosing function scope, while **let** works on a block scope. <-

---

## Arrow Functions

As a quick reminder: we have a few ways of declaring functions in JavaScript:

- Function Declaration / Named Function
- Function Expression
- IIFE

[Read more about functions in JS](OldFunctions.md)

In ES6, we find a new type of functions.

```javascript
// Old way
const fooWithoutParameters = function() {
    // Code
};
const fooWithOneParameter = function(a) {
    // Code
};
const fooWithTwoParameters = function (a,b) {
    // Code
};

// Fat Arrows join the game
const arrowWithoutParam = () => {
    // Code
};
const arrowWithOneParam = a => {
    // Code
};
const arrowWithTwoParams = (a,b) {
    // Code
};
```

The cool thing about this functions is how easy we can make one-liners, and promote a more functional-programming approach. We can omit the curly brackets, and the _return_ keyword in certain cases.

```javascript
const foo = () => {
  return result;
};
// Turns into
const foo = () => result;
```

We can make use of the method-chaining to achieve this when they get slightly complex.
_I.E. array.method1().method2()_

## Functions with default parameters

Another addition to the tool-box is being able to pass defualt parameters inside the functions, that can be used in case that parameter is omitted.

```javascript
const sum = (param1, param2 = 5) => param1 + param2;

sum(5, 10); // 15
sum(5); // 10
```

---

## Destructuring Assignments

It's a JavaScript expression that let us extract values from arrays and properties from objects as variables

It tends to be pretty similar to referencing an object's method or attribute as a variable locally accessible.

```javascript
let animal = {
    species: "dog",
    weight: 21,
    sound: "woof"
};

let { species, sound } = animal;
// It'd be similar to:
// let species = animal.species;
// let sound = animal.sound;
// With the difference that it proves itself more useful when it can take optional default parameters

console.log(`The ${species} makes ${sound}!`);
```

Another example is when we do it with the React imports.

```javascript
import React, { Component } from 'react';

class App extends React {
    // ...
}
```

Instead of:

```javascript
import React from 'react';

class App extends React.Component {
    // ...
}
```

---

## Spread Operator

We can use the spread operator to copy an array or combine two of them.

```javascript
// Copy
const arr = [ 2, 3, 4, 5 ];
const resultArr = [...arr]; // [ 2, 3, 4, 5 ]
```

```javascript
// Combine two arrays
const arr1 = [ 1, 2, 3, 4, 5 ];
const arr2 = [ 6, 7, 8, 9, 10 ];
const resultArr = [...arr1, ...arr2]; // [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
```

## Rest Operator

Similar to the spread operator, we can represent an indefinite number of arguments as an array with the `...` three dots.
It will turn into an array from 0 to the actual number of arguments passed in the function defined.

It must go as the only or last argument of said functions.

```javascript
function sum(...args) {
    return args.reduce((accumulator, currentValue) => accumulator + currentValue;
    // It will sum all the arguments passed
}
```

---

## OOP alike implementations

Now, in JavaScript we can emulate OOP concepts like classes, constructors, getters, and setters.
Although it doesn't reach the same level of encapsulation and abstraction that we can achieve in other langaiuges like Java, it's worth knowing it.

```javascript
// Create a class
class Thermostat {
  // Create a constructor
  constructor(temp) {
    this.temp = temp;
  }
  // Getter
  get temperature() {
    return this.temp;
  }
  // Setter
  set temperature(newTemp) {
    this.temp = newTemp;
  }
}
```

---

## Import and Export

### Import

Before ES6, we used **require()** to import whole modules from one script to another.
But now we have a new keyword that allow us to import certain parts of other code. Being possible to bring functions or variables to our code from other sources.

```javascript
import { sum } from "arithmeticFunctions";

sum(2, 3);
```

It worth noting that this syntax doesn't work on a browser at the time of writing this. Just for use in NodeJS.
Because of this, if you want to look outside the _node_modules_ folder, you'll need **" ./ "**.

We can also import the whole document with:

```javascript
import * as arithmetics from "arithmeticFunctions";
arithmetic.sum(2, 3);
```

### Export (Named Export)

For being able to import code, we'll need to **export** it from the source. This is called _named export_.

```javascript
    // Export a function already declared
    export { sum }
    // Export a variable
    export const foo = "bar";
    // Export everything in one line
    const foo = "bar";
    export { sum, foo }
```

### Default Export

Another **export** syntax, is the _export default_. We'll use this type of syntax if only one value is being exported, or to create a fallback value for a module.

```javascript
export default function add(x,y) => {
    return x + y;
};
```

**Note:** We can't use _export default_ with _var_, _let_ or _const_.

If we want to import this **Default Export**, we'll use:

```javascript
import add from "arithmeticFunctions";
add(2, 3);
```

**Note:** We won't add the curly brackets to the imported value.

---

**Downwards data-flow:** It means that only the "most parent" component should fetch data.

---

## Functional programming methods

There's a few methods that encourage functional programming in JavaScript: `reduce()`, `map()` and `filter()`.

- **map():** will apply the passed function to each element of an array and return a new array.
- **filter():** will apply a test function to each element of an array and return a new array with the parameters that pass the test.
- **reduce():** will apply a given function against an accumulator and each element of an array from left to right to reduce to a single value. In praqctice, for me, it's the hardest to use, but as a general rule of thumb, I tend to write it down in a certain way that helps me use it.

```javascript
    [array].reduce((accumulator, currentValue) => {
        // code
    }, 0 [initialValue:optional:];
```

---

## PadStart and PadEnd Methods

Methods used in Strings that gives us a way to add values to the beginning or end of a string.

```javascript
let example = 'Jose';
// It will fill the string up to the specified length
console.log(example.padStart(10, 'a')); // aaaaaaJose

let example2 = 'Pablo Perez';
console.log(example2.padStart(10, 'a')); // Pablo Perez

console.log(example.padEnd(10,'a')); // Joseaaaaaa

console.log(example2.padEnd(10, 'a')); // Pablo Perez

let example3 = 'This is a string of 33 characters';
console.log(example3.length); // 33
console.log(example3.padStart(100)); // 'This is a string of 33 characters...'
console.log(example3.padStart(100).length); // 67 empty characters
console.log(example3.padEnd(1)); // 'This is a string of 33 characters'
```

It worth noting, if it's not clear enough by the example code, that if the passed length parameter is shorter or equal to the string, it won't change.