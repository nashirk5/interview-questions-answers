<!-- Start JavaScript -->

## **JavaScript**

<div align="right"><b><a href="../../README.md">↥ Back to home</a></b></div>

### Q 1. What is Javascript?

JavaScript, created by **Brendan Eich** in **1995**. JavaScript is the most popular scripting language for the Web. It is easy to learn, lightweight, cross-platform, single-threaded, and interpreted compiled language. It is widely used for web development, both on the client side and server side.

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 2. What are the data types in JavaScript?

JavaScript is a dynamically typed (also called loosely typed) scripting language. In JavaScript, variables can receive different data types over time.

**1. Primitive Data Type:**

1. **Number:** Represents numeric values, including integers and floating-point numbers.
2. **String:** Represents textual data enclosed in single quotes ('') or double quotes ("").
3. **Boolean:** Represents a logical value, either true or false.
4. **Undefined:** Represents a variable that has been declared but not assigned a value.
5. **Null:** Represents the intentional absence of any value.
6. **Symbol (ES6):** Represents a unique and immutable value that may be used as the key of an object property.
7. **BigInt:** BigInt is a built-in object in JavaScript that provides a way to represent whole numbers larger than 253-1.

**2. Non Primitive Data Type:**

1. **Object:** Represents a collection of key-value pairs where keys are strings (or symbols) and values can be of any data type, including other objects.
2. **Array:** Represents a collection of elements, usually of the same data type, indexed by non-negative integers.

**3. Special Data Type:**

1. **Function:** Functions are treated as first-class citizens, meaning they can be assigned to variables, passed as arguments to other functions, and returned from other functions.

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 3. What are difference between var, let and const?

| keyword    | var               | let              | const            |
| ---------- | ----------------- | ---------------- | ---------------- |
| Scope      | Global & Function | Function & Block | Function & Block |
| Reassigned | Yes               | Yes              | No               |
| Redeclare  | Yes               | No               | No               |
| Hoisted    | Yes               | No               | No               |

### Q 4. What is hoisting?

Hoisting is the default behaviour of javascript where all the variable and function declarations are moved on top during the compilation.

> _**NOTE:** It's important to understand that only the declarations are **hoisted**, not the initializations or assignments._\
> _To avoid hoisting, you can run javascript in strict mode by using `use strict` on top of the code_

### Q 5. What is closure?

In JavaScript, returning a function from another function means returning function along with its scope. This allows the function to retain access to memory, which can store live data between executions. This combination of the function and its scope chain is called closure.

```javascript
function outer() {
  let counter = 0;

  return function inner() {
    counter++;
    console.log(counter);
  };
}

const fn = outer();
fn(); // 1
fn(); // 2
fn(); // 3
```

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 6. What is passed by value and passed by reference?

In JavaScript, primitive data types are passed by value and non-primitive data types are passed by reference.

1. **Passed by Value:** When a primitive data type (such as numbers, strings, booleans, null, or undefined) is passed to a function, it is passed by value. This means that a copy of the value is passed to the function, and any changes made to the parameter inside the function do not affect the original variable outside the function.

```javascript
function increment(x) {
  x++;
  return x;
}

let num = 5;
console.log(increment(num)); // Output: 6
console.log(num); // Output: 5 (original variable remains unchanged)
```

2. **Passed by Reference:** When an object (including arrays and functions) is passed to a function, it is passed by reference. This means that a reference to the original object is passed to the function, rather than a copy of the object itself. Therefore, changes made to the object's properties or elements inside the function will affect the original object outside the function.

```javascript
function addName(person) {
  person.name = "John";
  return person;
}

let user = { name: "Alice" };
console.log(addName(user)); // Output: { name: 'John' }
console.log(user); // Output: { name: 'John' } (original object is modified)
```

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 7. Explain call(), apply() and, bind() methods?

`call()`, `apply()`, and `bind()` are methods in JavaScript, which is used to invoke a function.

1. **call():** This method invokes a function with a given `this` value and takes arguments as comma separated.

```javascript
var employee1 = { firstName: "John", lastName: "Rodson" };
var employee2 = { firstName: "Jimmy", lastName: "Baily" };

function invite(greeting1, greeting2) {
  console.log(
    greeting1 + " " + this.firstName + " " + this.lastName + ", " + greeting2,
  );
}

invite.call(employee1, "Hello", "How are you?"); // Hello John Rodson, How are you?
invite.call(employee2, "Hello", "How are you?"); // Hello Jimmy Baily, How are you?
```

2. **apply():** This method invokes a function with a given `this` value and takes arguments as an array.

```javascript
var employee1 = { firstName: "John", lastName: "Rodson" };
var employee2 = { firstName: "Jimmy", lastName: "Baily" };

function invite(greeting1, greeting2) {
  console.log(
    greeting1 + " " + this.firstName + " " + this.lastName + ", " + greeting2,
  );
}

invite.apply(employee1, ["Hello", "How are you?"]); // Hello John Rodson, How are you?
invite.apply(employee2, ["Hello", "How are you?"]); // Hello Jimmy Baily, How are you?
```

3. **bind():** Returns a new function and takes arguments as comma separated.

```javascript
var employee1 = { firstName: "John", lastName: "Rodson" };
var employee2 = { firstName: "Jimmy", lastName: "Baily" };

function invite(greeting1, greeting2) {
  console.log(
    greeting1 + " " + this.firstName + " " + this.lastName + ", " + greeting2,
  );
}

var inviteEmployee1 = invite.bind(employee1);
var inviteEmployee2 = invite.bind(employee2);
inviteEmployee1("Hello", "How are you?"); // Hello John Rodson, How are you?
inviteEmployee2("Hello", "How are you?"); // Hello Jimmy Baily, How are you?
```

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 8. What is currying ?

Currying is the process of taking a function with multiple arguments and turning it into a sequence of functions each with only a single argument.

In other words, when a function, instead of taking all arguments at one time, takes the first one and return a new function that takes the second one and returns a new function which takes the third one, and so forth, until all arguments have been fulfilled.

```javascript
// Normal function
const add = (a, b, c) => {
  return a + b + c;
};
console.log(add(10, 10, 10)); // 30

// Currying function
const addCurry = (a) => {
  return (b) => {
    return (c) => {
      return a + b + c;
    };
  };
};
console.log(addCurry(20)(20)(20)); // 60
```

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 9. What is the rest parameter and spread operator?

The rest parameter and spread operator are two features introduced in ECMAScript 6 (ES6) that enhance the functionality of JavaScript functions and arrays, respectively.

> _**NOTE:** Rest parameter should always be used at the last parameter of a function._

1. **Rest Parameter (`...`):** Rest parameter is an improved way to handle function parameters which allows us to represent an indefinite number of arguments as an array.\
    _**Example:**_
   ```javascript
   function sum(...numbers) {
     return numbers.reduce((total, num) => total + num, 0);
   }
   console.log(sum(1, 2, 3, 4, 5)); // Output: 15
   ```
2. **Spread Operator (...):** Spread operator allows iterables( arrays / objects / strings ) to be expanded into single arguments/elements.\
   _**Example:**_

   ```javascript
   function sum(x, y, z) {
     return x + y + z;
   }
   const numbers = [10, 20, 30];

   // Using Apply (ES5)
   console.log(sum.apply(null, numbers)); // 60

   // Using Spread Operator
   console.log(sum(...numbers)); // 60
   ```

   1. **Copying an array:**

      ```javascript
      let fruits = ["Apple", "Orange", "Banana"];
      let newFruitArray = [...fruits];

      console.log(newFruitArray); // Output: ['Apple', 'Orange', 'Banana']
      ```

   2. **Concatenating arrays:**

      ```javascript
      let arr1 = ["A", "B", "C"];
      let arr2 = ["X", "Y", "Z"];

      let result = [...arr1, ...arr2];

      console.log(result); // Output: ['A', 'B', 'C', 'X', 'Y', 'Z']
      ```

   3. **Spread syntax for object literals**

      ```javascript
      const obj1 = { id: 101, name: 'Rajiv Sandal' }
      const obj2 = { age: 35, country: 'INDIA' }

      const employee = { ...obj1, ...obj2 }

      console.log(employee);

      // Output
      {
        "id": 101,
        "name": "Rajiv Sandal",
        "age": 35,
        "country": "INDIA"
      }
      ```

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 10. What are Sets and WeakSet?

1.  **Sets:** Sets are a new object type with ES6 (ES2015) that allow to create collections of unique values. The values in a set can be either simple primitives like strings or integers, but more complex object types like object literals or arrays can also be part of a set.\
    _**Example:**_

    ```javascript
    let numbers = new Set([10, 20, 20, 30, 40, 50]);

        console.log(numbers); Set(5) { 10, 20, 30, 40, 50 }
        console.log(typeof numbers); // Object
    ```

2.  **WeakSet:** Just like Set, WeakSet is also a collection of unique and ordered elements with some key differences. Weakset contains only objects and no other type. Unlike Set, WeakSet only has three methods, add() , delete() and has().\
    _**Example:**_

    ```javascript
    const newSet = new Set([4, 5, 6, 7]);
    console.log(newSet); // Outputs Set {4,5,6,7}

    const newSet2 = new WeakSet([3, 4, 5]); //Throws an error

    let obj1 = { message: "Hello world" };
    const newSet3 = new WeakSet([obj1]);
    console.log(newSet3.has(obj1)); // true
    ```

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 11. What are Map and WeakMap?

1. **Map:** In javascript, Map is used to store key-value pairs. The key-value pairs can be of both primitive and non-primitive types. WeakMap is similar to Map with key differences.
   - The keys and values in weakmap should always be an object.
   - If there are no references to the object, the object will be garbage collected.

     _**Example:**_

     ```javascript
     const map1 = new Map();
     map1.set("Value", 1);

     const map2 = new WeakMap();
     map2.set("Value", 2.3); // Throws an error

     let obj = { name: "Vivek" };
     const map3 = new WeakMap();
     map3.set(obj, { age: 23 });
     ```

2. **WeakMap:** The WeakMap object is a collection of key/value pairs in which the keys are weakly referenced. In this case, keys must be objects and the values can be arbitrary values. WeakMap accepts only objects but not any primitive values (strings, numbers).

   _**Example:**_

   ```javascript
   // WeakMap()
   function Obj() {
     this.val = new Array(10).join("---");
   }

   window.obj = new Obj();
   var map = new WeakMap();
   console.log(window.obj); // {val: "-----------------", constructor: Object}
   map.set(window.obj, 20); // WeakMap {Obj => 20}
   console.log(map);
   ```

**Difference between Map and WeakMap:**

1. A WeakMap accepts only objects as keys whereas a Map, in addition to objects, accepts primitive datatype such as strings, numbers etc.
2. WeakMap objects doesn't avert garbage collection if there are no references to the object which is acting like a key. Therefore there is no method to retrieve keys in WeakMap, whereas in Map there are methods such as Map.prototype.keys() to get the keys.
3. There is no size property exists in WeakMap.

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 12. What is destructing?

Destructuring in JavaScript is a convenient way to extract multiple values from arrays or objects and assign them to variables using a concise syntax. It allows you to "unpack" values from data structures like arrays and objects into separate variables, making it easier to work with complex data in a more expressive and succinct manner.

_**Example:**_

```javascript
const person = { name: "John", age: 30 };
const { name, age } = person;
console.log(name); // Output: "John"
console.log(age); // Output: 30
```

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 13. What are generators?

A generator is a function that can stop midway and then continue from where it stopped. In short, a generator appears to be a function but it behaves like an `iterator`.

_**Example:**_

```javascript
function* generator(num) {
  yield num + 10;
  yield num + 20;
  yield num + 30;
}
let gen = generator(10);

console.log(gen.next().value); // 20
console.log(gen.next().value); // 30
console.log(gen.next().value); // 40
```

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 14. What is the difference between null and undefined?

| Null                                                                                | Undefined                                                                                      |
| ----------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| Type of null is object                                                              | Type of undefined is undefined                                                                 |
| Undefined means a variable has been declared but has yet not been assigned a value. | Null is an assignment value. It can be assigned to a variable as a representation of no value. |
| It is a global property.                                                            | It is not a global property.                                                                   |

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 15. What is the difference between window and document?

| Window                                                                        | Document                                                                                      |
| ----------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| It is the root level element in any web page                                  | It is the direct child of the window object. This is also known as Document Object Model(DOM) |
| It has methods like alert(), confirm() and properties like document, location | It provides methods like getElementById, getElementsByTagName, createElement etc              |

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 16. What is the difference between == and === operators?

In JavaScript, the `==` and `===` operators are used for comparison and `===` checks both the values and the types, and only returns true if both are the same.

_**Example:**_

```javascript
0 == false // true
0 === false // false
1 == "1" // true
1 === "1" // false
null == undefined // true
null === undefined // false
"0" == false // true
"0" === false // false
[] === [] // false, refer different objects in memory
{} === {} // false, refer different objects in memory
```

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 17. What are typeOf, delete, void, and ternary operators?

1. **`typeof` Operator:** This is used to determine the type of a value or expression
   _**Example:**_

   ```javascript
   typeof 42; // Returns "number"
   typeof "hello"; // Returns "string"
   typeof true; // Returns "boolean"
   ```

2. **`delete` Operator:** This operator is used to delete a property from an object.
   _**Example:**_

   ```javascript
   const obj = { a: 1, b: 2 };
   delete obj.a; // Deletes the property "a" from the object
   ```

3. **`void` Operator:** This operator evaluates an expression and returns undefined. It's often used to create a URL with a JavaScript "void" link, where clicking the link does nothing.
   _**Example:**_

   ```html
   <a href="javascript:void(0)">Click me</a>
   ```

4. **Ternary (`? :`) Operator:** The ternary operator is a conditional operator that evaluates a condition and returns one of two expressions based on whether the condition is true or false.
   _**Example:**_

   ```javascript
   const age = 20;
   const status = age >= 18 ? "adult" : "minor";
   console.log(status); // Output depends on the value of age
   ```

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 18. What is isNaN?

The isNaN() function determines whether a value is NaN ( Not a Number ) or not. This function returns true if the value equates to NaN. The isNaN() method converts the value to a number before testing it.

_**Example:**_

```javascript
isNaN("Hello"); // true
isNaN("100"); // false
typeof NaN; // Number
Number.isNaN("Hello"); // false
```

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 19. What are arrow/lambda functions?

An arrow function is a shorter/concise syntax for a function expression and does not have its own this, arguments, super, or new.target. These functions are best suited for non-method functions, and they cannot be used as constructors.

_**Example:**_

```javascript
const arrowFunc1 = (a, b) => a + b; // Multiple parameters
const arrowFunc2 = (a) => a * 10; // Single parameter
const arrowFunc3 = () => {}; // no parameters
```

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 20. What is a first class function?

In javaScript, functions can be stored as a variable or it can be passed as an argument or be returned by another function. That makes function first-class function in JavaScript.

_**Example:**_

```javascript
// 01: Assign a function to a variable
const message = function () {
  console.log("Hello World!");
};
message(); // Invoke it using the variable

// 02: Pass a function as an Argument
function sayHello() {
  return "Hello, ";
}
function greeting(helloMessage, name) {
  console.log(helloMessage() + name);
}
// Pass `sayHello` as an argument to `greeting` function
greeting(sayHello, "JavaScript!");

// 03: Return a function
function sayHello() {
  return function () {
    console.log("Hello!");
  };
}
```

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 21. What is a higher order function?

A Higher-Order function is a function that receives a function as an argument or returns the function as output.

_**Example:**_, `Array.prototype.map()`, `Array.prototype.filter()`, `Array.prototype.forEach()` and `Array.prototype.reduce()` are some of the Higher-Order functions in javascript.

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 22. What are the types of errors in javascript?

Here are some common types of errors in JavaScript:

1. **Syntax Errors:** These errors prevent the code from being executed and are typically detected during the parsing phase.

```javascript
let x = 10;
console.log(x
```

2. **Reference Errors:** Reference errors occur when code tries to access a variable or function that does not exist or is not in scope. These errors are thrown at runtime when the JavaScript engine cannot find the referenced variable or function.

```javascript
console.log(y); // ReferenceError: y is not defined
```

3. **Type Errors:** These errors are thrown at runtime when the JavaScript engine encounters an unexpected data type or an incompatible operation.

```javascript
let x = "10";
console.log(x.toUpperCase()); // TypeError: x.toUpperCase is not a function
```

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 23. What is recursion in a programming language?

Recursion is a method of performing an operation iterate by having a function call itself repeatedly until it reaches a result.

_**Example:**_

```javascript
// Ex: 1
function sumArray(arr, index = 0) {
  // Base case: if the index reaches the end of the array, return 0
  if (index === arr.length) {
    return 0;
  } else {
    // Recursive case: add the current element to the sum of the remaining elements
    return arr[index] + sumArray(arr, index + 1);
  }
}
console.log(sumArray([1, 2, 3, 4, 5])); // Output: 15 (1 + 2 + 3 + 4 + 5)

// Ex: 2
function add(num) {
  if (num === 0) {
    return 0;
  } else {
    return num + calculateSum(num - 1);
  }
}
console.log(calculateSum(5)); // Output: 15 (5 + 4 + 3 + 2 + 1)
```

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 24. What are callbacks?

A callback is a function that is passed as an argument to another function and that will be executed after another function gets executed.

_**Example:**_

```javascript
function divideByHalf(sum) {
  console.log(Math.floor(sum / 2));
}

function multiplyBy2(sum) {
  console.log(sum * 2);
}

function operationOnSum(num1, num2, operation) {
  var sum = num1 + num2;
  operation(sum);
}

operationOnSum(3, 3, divideByHalf); // Outputs 3
operationOnSum(5, 5, multiplyBy2); // Outputs 20
```

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 25. What is a callback hell?

Callback Hell is an anti-pattern with multiple nested callbacks which makes code hard to read and debug when dealing with asynchronous logic. The callback hell looks like below,

_**Example:**_

```javascript
async1(function(){
    async2(function(){
        async3(function(){
            async4(function(){
                ....
            });
        });
    });
});
```

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 26. What is a promise?

Promises are used to handle asynchronous operations. They provide an alternative approach for callbacks by reducing the callback hell and writing the cleaner code.

_There are 3 states in promises:_

1.  **Pending:** Initial state, neither fulfilled nor rejected.
2.  **Fulfilled:** The asynchronous operation has completed successfully, and the promise has a resolved value.
3.  **Rejected:** The asynchronous operation has failed, and the promise has a reason for rejection (usually an error object).

_**Example:**_

```javascript
// Creating a promise
const fetchData = new Promise((resolve, reject) => {
  // Simulating an asynchronous operation (e.g., fetching data from a server)
  setTimeout(() => {
    const data = { message: "Data fetched successfully" };
    // Resolve the promise with the fetched data
    resolve(data);
    // Reject the promise with an error if something goes wrong
    // reject(new Error('Failed to fetch data'));
  }, 1000);
});

// Consuming the promise
fetchData
  .then((data) => {
    console.log(data.message);
  })
  .catch((error) => {
    console.error(error.message);
  });
```

_These are the methods in promises:_

1. **then(onFulfilled, onRejected):** This method is used to handle the resolved value (fulfillment) or the reason for rejection of the promise.
   ```javascript
   promise.then(
     (value) => console.log("Fulfilled:", value),
     (reason) => console.error("Rejected:", reason),
   );
   ```
2. **catch(onRejected):** This method is used to handle the rejection reason of the promise.
   ```javascript
   promise.catch((reason) => console.error("Rejected:", reason));
   ```
3. **finally(onFinally):** This method is used to execute a callback function regardless of whether the promise is fulfilled or rejected. It is commonly used for cleanup operations such as closing resources.
   ```javascript
   promise.finally(() => console.log("Finally executed"));
   ```
4. **Promise.all(iterable):** This method returns a single promise that resolves when all of the promises in the iterable argument have resolved, or rejects with the reason of the first promise that rejects. It is commonly used to wait for multiple asynchronous tasks to complete simultaneously.
   ```javascript
   Promise.all([promise1, promise2, promise3])
     .then((values) => console.log("All resolved:", values))
     .catch((reason) =>
       console.error("One or more promises rejected:", reason),
     );
   ```
5. **Promise.race(iterable):** This method returns a promise that resolves or rejects as soon as one of the promises in the iterable resolves or rejects, with the value or reason from that promise. It is commonly used to race multiple asynchronous tasks and take the result of the fastest one.
   ```javascript
   Promise.race([promise1, promise2, promise3])
     .then((value) => console.log("First resolved:", value))
     .catch((reason) => console.error("First rejected:", reason));
   ```

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 27. What is promise.all()?

Promise.all is a promise that takes an array of promises as an input (an iterable), and it gets resolved when all the promises get resolved or any one of them gets rejected.

_**Example:**_

```javascript
// promise.all()
const promise1 = new Promise((resolve, reject) => {
  setTimeout(resolve, 10, "First");
});

const promise2 = new Promise((resolve, reject) => {
  setTimeout(resolve, 20, "Second");
});

Promise.all([promise1, promise2])
  .then((values) => {
    console.log(values);
  })
  .catch((error) => console.log(`Error in promises ${error}`));
// expected output: Array ["First", "Second"]
```

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 28. Explain arrays?

JavaScript array is an object that represents a collection of similar type of elements. It can holds values (of any type) not particularly in named properties/keys, but rather in numerically indexed positions.

_**Example:**_

1. _Creating an array_

   ```javascript
   // array of numbers
   const numbers = [10, 20, 30, 40, 50];

   // using new keyword
   const numbers = new Array(10, 20, 30, 40, 50);

   // array of strings
   let fruits = ["Apple", "Orange", "Plum", "Mango"];
   ```

2. _Accessing array elements_

   ```javascript
   let fruits = ["Apple", "Orange", "Plum", "Mango"];

   fruits[0]; // Apple
   fruits[fruits.length - 1]; // Mango

   // Iterate array elements
   for (let i = 0; i < fruits.length; i++) {
     console.log(fruits[i]);
   }
   ```

3. _Adding new array elements_

   ```javascript
   let fruits = ["Apple", "Orange", "Plum", "Mango"];

   fruits.push("Grapes"); // Adds a new element (Grapes) to fruits
   ```

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 29. Write some array methods?

1. **array.join():** The join() method creates and returns a new string by concatenating all of the elements in an array.

```javascript
var elements = ["Fire", "Air", "Water"];

console.log(elements.join()); // Output: "Fire,Air,Water"
console.log(elements.join("")); // Output: "FireAirWater"
console.log(elements.join("-")); // Output: "Fire-Air-Water"
```

2. **array.pop():** The pop() method removes the last element from an array and returns that element.

```javascript
var plants = ["broccoli", "cauliflower", "kale"];

console.log(plants.pop()); // Output: "kale"
console.log(plants); // Output: Array ["broccoli", "cauliflower"]
console.log(plants.pop()); // Output: "cauliflower"
```

3. **array.push():** The push() method adds one or more elements to the end of an array.

```javascript
const animals = ["pigs", "goats", "sheep"];

const count = animals.push("cows");
console.log(animals); // Output: Array ["pigs", "goats", "sheep", "cows"]
```

4. **array.shift():** The shift() method removes the first element from an array and returns that removed element.

```javascript
var fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.shift();
console.log(fruits); // Output: Array ["Orange", "Apple", "Mango"]
```

5. **array.unshift():** The unshift() method adds one or more elements to the beginning of an array.

```javascript
var fruits = ["Banana", "Orange", "Apple"];
fruits.unshift("Mango", "Pineapple");
console.log(fruits); // Output: Array ["Mango", "Pineapple", "Banana", "Orange", "Apple"]
```

6. **array.concat():** The concat() method is used to merge two or more arrays. This method does not change the existing arrays, but instead returns a new array.

```javascript
const array1 = ["a", "b", "c"];
const array2 = ["d", "e", "f"];

console.log(array1.concat(array2)); // Output: Array ["a", "b", "c", "d", "e", "f"]
```

7. **array.map():** The map() method creates a new array with the results of calling a provided function on every element in the calling array.

```javascript
var array1 = [1, 4, 9, 16];

// pass a function to map
const map1 = array1.map((x) => x * 2);

console.log(map1); // Output: Array [2, 8, 18, 32]
```

8. **array.filter():** The filter() method creates a new array with all elements that pass the test implemented by the provided function.

```javascript
var words = ["spray", "limit", "elite", "exuberant", "destruction"];

const result = words.filter((word) => word.length > 6);

console.log(result); // Output: Array ["exuberant", "destruction"]
```

9. **array.reduce():** The reduce() method executes a reducer function (that you provide) on each element of the array, resulting in a single output value.

```javascript
const array1 = [1, 2, 3, 4];
const reducer = (accumulator, currentValue) => accumulator + currentValue;

console.log(array1.reduce(reducer)); // Output: 10
console.log(array1.reduce(reducer, 5)); // Output: 15
```

10. **array.every():** The every() method tests whether all elements in the array pass the test implemented by the provided function. It returns a Boolean value.

```javascript
function isBelowThreshold(currentValue) {
  return currentValue < 40;
}

var array1 = [1, 30, 39, 29, 10, 13];
console.log(array1.every(isBelowThreshold)); // Output: true
```

11. **array.some():** The some() method tests whether at least one element in the array passes the test implemented by the provided function. It returns a Boolean value.

```javascript
var array = [1, 2, 3, 4, 5];

var even = function (element) {
  // checks whether an element is even
  return element % 2 === 0;
};

console.log(array.some(even)); // Output: true
```

12. **array.find():** The find() method returns the value of the first element in the provided array that satisfies the provided testing function.

```javascript
var array1 = [5, 12, 8, 130, 44];

var found = array1.find(function (element) {
  return element > 100;
});

console.log(found); // Output: 130
```

13. **array.includes():** The includes() method determines whether an array includes a certain value among its entries, returning true or false as appropriate.

```javascript
var array1 = [1, 2, 3];
console.log(array1.includes(2)); // Output: true

var pets = ["cat", "dog", "bat"];
console.log(pets.includes("at")); // Output: false
```

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 30. Write some string methods?

1. **string.charAt():** Returns the character at the specified index in the string.

```javascript
const str = "Hello";
console.log(str.charAt(0)); // Output: "H"
```

2. **string.concat():** Combines two or more strings and returns a new string.

```javascript
const str1 = "Hello";
const str2 = "World";
console.log(str1.concat(" ", str2)); // Output: "Hello World"
```

3. **string.includes():** Checks if the string contains the specified substring.

```javascript
const str = "Hello World";
console.log(str.includes("World")); // Output: true
```

4. **string.indexOf():** Returns the index of the first occurrence of a specified value in a string, or -1 if not found.

```javascript
const str = "Hello World";
console.log(str.indexOf("o")); // Output: 4
```

5. **string.replace():** Replaces a specified value with another value in a string.

```javascript
const str = "Hello World";
console.log(str.replace("World", "Universe")); // Output: "Hello Universe"
```

6. **string.slice():** Extracts a section of a string and returns a new string.

```javascript
const str = "Hello World";
console.log(str.slice(6)); // Output: "World"
```

7. **string.split():** Splits a string into an array of substrings based on a specified separator.

```javascript
const str = "Hello World";
console.log(str.split(" ")); // Output: ["Hello", "World"]
```

8. **string.toLowerCase():** Converts the string to lowercase or uppercase, respectively.

```javascript
const str = "Hello World";
console.log(str.toLowerCase()); // Output: "hello world"
console.log(str.toUpperCase()); // Output: "HELLO WORLD"
```

9. **string.trim():** Removes whitespace from both ends of a string.

```javascript
const str = "   Hello World   ";
console.log(str.trim()); // Output: "Hello World"
```

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 31. What is the difference between slice and splice?

| Slice                                        | Splice                                       |
| -------------------------------------------- | -------------------------------------------- |
| Doesn't modify the original array(immutable) | Modifies the original array(mutable)         |
| Returns the subset of original array         | Returns the deleted elements as array        |
| Used to pick the elements from array         | Used to insert/delete elements to/from array |

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 32. What is loop?

A loop in JavaScript is a programming construct that allows you to repeatedly execute a block of code multiple times until a specified condition is met. Loops are fundamental for iterating over arrays, processing data, and performing repetitive tasks efficiently. JavaScript provides several types of loops to suit different use cases:

1. **`for` Loop:** The for loop is used to execute a block of code a specified number of times.

```javascript
for (let i = 0; i < 5; i++) {
  console.log(i); // Output: 0, 1, 2, 3, 4
}
```

2. **`while` Loop:** The while loop is used to execute a block of code as long as a specified condition is true.

```javascript
let i = 0;
while (i < 5) {
  console.log(i); // Output: 0, 1, 2, 3, 4
  i++;
}
```

3. **`do...while` Loop:** The do...while loop is similar to the while loop, but it always executes the block of code at least once, even if the condition is false.

```javascript
let i = 0;
do {
  console.log(i); // Output: 0, 1, 2, 3, 4
  i++;
} while (i < 5);
```

4. **`for...in` Loop:** The for...in loop iterates over the enumerable properties of an object, including inherited properties from its prototype chain.

```javascript
const person = { name: "John", age: 30 };
for (let key in person) {
  console.log(key + ": " + person[key]); // Output: name: John, age: 30
}
```

5. **`for...of` Loop:** The for...in loop iterates over the enumerable properties of an object, including inherited properties from its prototype chain.

```javascript
const person = { name: "John", age: 30 };
for (let key in person) {
  console.log(key + ": " + person[key]); // Output: name: John, age: 30
}
```

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 33. What is the difference between for..in and for..of??

- Use for...in to iterate over the keys of an object, including inherited properties.

  ```javascript
  const obj = { a: 1, b: 2, c: 3 };

  for (let key in obj) {
    console.log(key); // Output: "a", "b", "c"
  }
  ```

- Use for...of to iterate over the values of an iterable object, such as arrays, strings, maps, sets, etc.

  ```javascript
  const array = [1, 2, 3];

  for (let value of array) {
    console.log(value); // Output: 1, 2, 3
  }

  const str = "hello";

  for (let value of str) {
    console.log(value); // Output: h,e,l,l,o
  }
  ```

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 34. What is Async/await?

Async/await is a feature in JavaScript that allows you to write asynchronous code in a synchronous-looking manner. It provides a more readable and understandable way to work with asynchronous operations, such as fetching data from a server, reading files, or making network requests.

_Here's a brief overview of how async/await works:_

**Async Functions:** An async function is a function that operates asynchronously via the event loop, and it always returns a promise. You declare an async function using the async keyword before the function declaration.

**Await Operator:** Inside an async function, you can use the await keyword before an expression that returns a promise. The await keyword pauses the execution of the async function until the promise is resolved, and then it returns the resolved value.

_**Example:**_

```javascript
// Example asynchronous function
function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("Data fetched successfully");
    }, 2000);
  });
}

// Async function using async/await
async function getData() {
  try {
    console.log("--- Start ---");
    const result = await fetchData();
    console.log(result);
    console.log("--- End ---");
  } catch (error) {
    console.error("Error fetching data:", error);
  }
}

// Calling the async function
getData();
```

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 35. What are the possible ways to create objects in JavaScript?

_**Example:**_

```javascript
// Example 1:
let object = new Object();

// Example 2:
let object = Object.create(null);

// Example 3:
let person = {};

// Example 4:
function Person(name) {
  let object = {};
  object.name = name;
  object.age = 26;

  return object;
}

let person = new Person("Alex");

// Example 5:
class Person {
  constructor(name) {
    this.name = name;
  }
}

let person = new Person("Alex");
```

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 36. What are the difference between mutable and immutable objects?

A mutable object is an object whose state can be modified after it is created. An immutable object is an object whose state cannot be modified after it is created.

> _**NOTE:** In JavaScript numbers, strings, null, undefined and Booleans are primitive types which are immutable. Objects, arrays, functions, classes, maps, and sets are mutable.._

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 37. What is shallow copy and deep copy?

1. **Shallow Copy:** Shallow copy is a bit-wise copy of an object. A new object is created that has an exact copy of the values in the original object. If any of the fields of the object are references to other objects, just the reference addresses are copied i.e., only the memory address is copied.\
   _A Shallow copy of the object can be done using `object.assign()`_

   ```javascript
   // Shallow Copy
   let obj = {
     a: 10,
     b: 20,
   };

   let objCopy = Object.assign({}, obj);
   console.log(objCopy); // Result - { a: 1, b: 2 }
   ```

2. **Deep Copy:** A deep copy copies all fields, and makes copies of dynamically allocated memory pointed to by the fields. A deep copy occurs when an object is copied along with the objects to which it refers.\
   _A Deep copy of the object can be done using `JSON.parse(JSON.stringify(object))`_

   ```javascript
   // Deep Copy
   let obj2 = {
     a: 10,
     b: {
       c: 20,
     },
   };

   let newObj = JSON.parse(JSON.stringify(obj2));
   obj2.b.c = 30;

   console.log(obj2); // { a: 10, b: { c: 20 } }
   console.log(newObj); // { a: 10, b: { c: 20 } }
   ```

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 38. What are classes in ES6?

In JavaScript, classes are a syntactical sugar over the prototype-based inheritance model. Introduced in ECMAScript 2015 (ES6), classes provide a more familiar and structured way to define object blueprints and create instances of those objects.

```javascript
class Bike {
  constructor(color, model) {
    this.color = color;
    this.model = model;
  }

  getDetails() {
    return this.model + " bike has" + this.color + " color";
  }
}
```

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 39. What is Module.

JavaScript modules are a way to organize and structure code into reusable units. They allow developers to separate code into individual files or modules, making it easier to manage, maintain, and scale large JavaScript applications. ES6 introduced native support for modules, providing a standardized syntax and mechanism for defining module dependencies and exports.

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

### Q 40. List out JavaSCript ES6 features.

ES6 (ECMAScript 2015) is a significant update to the JavaScript language specification, introducing many new features and improvements to the language syntax and functionality. Some key features introduced in ES6 include:

1. Arrow Functions
2. let and const Declarations
3. Template Literals:
4. Destructuring Assignment
5. Spread Operator (...)
6. Rest Parameter
7. Classes
8. Promises
9. Modules

<div align="right"><b><a href="#javascript">↥ Back to top</a></b></div>

##
