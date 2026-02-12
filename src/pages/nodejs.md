<!-- Start NodeJS -->

## **NodeJS**

<div align="right"><b><a href="../../README.md">↥ Back to home</a></b></div>

### Q 1. What is NodeJs?

Node.js is an open-source, cross-platform JavaScript runtime environment built on Chrome's V8 JavaScript engine. It allows developers to run JavaScript code on the server-side, enabling the development of scalable and high-performance web applications.

_Key features of NodeJs:_

1. **Asynchronous and Event-Driven:** Node.js uses a non-blocking, event-driven architecture, which allows it to handle multiple concurrent connections efficiently. This makes it suitable for building real-time applications like chat applications or streaming services.

2. **JavaScript Everywhere:** Node.js enables developers to use JavaScript for both client-side and server-side development, fostering code reuse, and reducing context switching between languages.

3. **V8 Engine:** Node.js is built on Chrome's V8 JavaScript engine, which compiles JavaScript code to native machine code, resulting in high performance and efficiency.

4. **Package Ecosystem (npm):** Node.js has a vast ecosystem of open-source libraries and packages available through npm (Node Package Manager). Developers can easily install and manage dependencies for their projects using npm.

5. **Single-Threaded, Event Loop:** Node.js operates on a single-threaded event loop model, where I/O operations are non-blocking and handled asynchronously. This allows Node.js to handle a large number of concurrent connections without the overhead of thread-based concurrency.

6. **Scalability:** Node.js applications can be easily scaled horizontally by adding more instances or vertically by utilizing more powerful hardware. It also supports clustering for leveraging multiple CPU cores.

Node.js is commonly used for building various types of applications, including web servers, RESTful APIs, real-time web applications, microservices, command-line tools, and more. Its lightweight, efficient, and scalable nature makes it a popular choice for building modern web applications.

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 2. How does NodeJs work?

Node.js operates on a single-threaded, event-driven architecture to handle asynchronous I/O operations efficiently. It enables developers to build scalable and high-performance applications by utilizing non-blocking I/O, modular code organization, and a vast ecosystem of npm packages.

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 3. Create a simple server?

Step 1: Initialize project

```
 npm init
```

```
 entry point: (index.js) to app.js
```

Step 2: Install ExpressJS

```
 npm install express --save
```

Step 3: app.js

```javascript
/**
 * Express.js
 */
const express = require("express");
const app = express();

app.get("/", function (req, res) {
  res.send("Hello World!");
});

app.listen(3000, function () {
  console.log("App listening on port 3000!");
});
```

Step 4: Run the app

```
  node app.js
```

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 4. What are some commonly used timing features of Node.js?

- **setTimeout/clearTimeout:** This is used to implement delays in code execution.
- **setInterval/clearInterval:** This is used to run a code block multiple times.
- **setImmediate/clearImmediate:** Any function passed as the setImmediate() argument is a callback that's executed in the next iteration of the event loop.
- **process.nextTick:** Both setImmediate and process.nextTick appear to be doing the same thing; however, you may prefer one over the other depending on your callback’s urgency.

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 5. What is fork in nodeJS?

A fork in general is used to spawn child processes. In node it is used to create a new instance of v8 engine to run multiple workers to execute the code.

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 6. How many types of API functions are there?

There are two types of API functions:

1. **Blocking or Synchronous APIs:**
   - These functions directly block further execution until the current operation completes. They are simple to understand and use because the code execution happens in a sequence that is easy to follow. However, using blocking calls can lead to performance issues in Node.js applications, especially in I/O operations, because they tie up the event loop and prevent it from doing anything else.
   - Example: Reading a file synchronously using `fs.readFileSync()`.
2. **Non-blocking or Asynchronous APIs:**
   - Non-blocking functions allow Node.js to start an operation and then move on to the next task without waiting for the operation to complete. These types of functions usually accept callbacks and return immediately, promoting efficient use of the event loop and improving the application's scalability and performance.
   - Example: Reading a file asynchronously using `fs.readFile()` with a callback function

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 7. What is an event-loop in Node JS?

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 1. What?

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 1. What?

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 1. What?

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 1. What?

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 1. What?

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

##

<!-- Start MySQL -->

## **MySQL**

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

##

<!-- Start JavaScript basic programs  -->

## **JavaScript basic programs**

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

##

<!-- Formatting -->

<!-- [Back to top](#nodejs) -->
<!-- <div ><b><a href="#nodejs">↥ Back to top</a></b></div> -->

<!-- - HTML

  1. [What is HTML?](#q-1-what-is-html)
  2. [What are Tags, Elements and Attributes?](#q-2-what-are-tags-elements-and-attributes)
  3. [What are Semantic Elements?](#q-3-what-are-semantic-elements)
  4. [What are HTML APIs?](#q-4-what-are-html-apis)
  5. [What is the difference between Cookie, Local storage and Session storage?](#q-5-what-is-the-difference-between-cookie-local-storage-and-session-storage)

- CSS

  1. [What is CSS?](#q-1-what-is-css)
  2. [What is the Box model in CSS?](#q-2-what-is-the-box-model-in-css)
  3. [What are Pseudo class and Pseudo element?](#q-3-what-are-pseudo-class-and-pseudo-element)
  4. [What is a z-index?](#q-4-what-is-a-z-index)
  5. [Explain CSS Absolute and Relative position property?](#q-5-explain-css-absolute-and-relative-position-property)
  6. [How to center align a div inside another div?](#q-6-how-to-center-align-a-div-inside-another-div)
  7. [How can we make our website responsive using CSS?](#q-7-how-can-we-make-our-website-responsive-using-css)
  8. [How to change the color for even and odd list items?](#q-8-how-to-change-the-color-for-even-and-odd-list-items)
  9. [What is CSS flexbox, and what are its properties?](#q-9-what-is-css-flexbox-and-what-are-its-properties)
  10. [What is CSS Grid?](#q-10-what-is-css-grid) -->
