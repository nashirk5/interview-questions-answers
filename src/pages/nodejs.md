<!-- Start NodeJS -->

## **NodeJS**

<div align="right"><b><a href="../../README.md">↥ Back to home</a></b></div>

### Q 1. What is NodeJs?

Node.js is an open-source JavaScript runtime environment which is built on Chrome’s V8 engine. That uses a single-threaded, event-driven, non-blocking I/O model, where the event loop, powered by libuv, efficiently handles asynchronous operations. This architecture enables highly scalable server-side and real-time applications.

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 2. How does NodeJs work?

Node.js is single-threaded, event-driven, non-blocking I/O model.

A new request coming in is one kind of event. The server starts processing it and when there is a blocking IO operation, it does not wait until it completes and instead registers a callback function. The server then immediately starts to process another event ( maybe another request ). When the IO operation is finished, that is another kind of event, and the server will process it ( i.e. continue working on the request ) by executing the callback as soon as it has time.

Node.js Platform does not follow Request/Response Multi-Threaded Stateless Model. It follows Single Threaded with Event Loop Model. Node.js Processing model mainly based on Javascript Event based model with Javascript callback mechanism.

![css_box_model](../assets/images/nodejs_execution.png)

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 3. Create a simple server?

Step 1: Initialize project and Install ExpressJS

```js
  npm init -y
  npm install express
```

Step 2: Now create a file `server.js`

```js
const express = require("express");
const app = express();

const PORT = 3000;

// Basic route
app.get("/", (req, res) => {
  res.send("Hello, World!");
});

// Start server
app.listen(PORT, () => {
  console.log(`Server is running on http://localhost:${PORT}`);
});
```

Step 4: Run the app

```js
  node app.js
```

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 4. What are some commonly used timing features of Node.js?

**1️⃣ `setTimeout()`:** Executes a callback after a minimum delay (exact timing is not guaranteed). Runs in the Timers phase of the event loop.

```js
setTimeout(() => {
  console.log("Runs after ~1000ms");
}, 1000);
```

**2️⃣ `setInterval()`:** Executes a callback repeatedly at a fixed interval. Also runs in the Timers phase.

```js
setInterval(() => {
  console.log("Runs every 2 seconds");
}, 2000);
```

**3️⃣ `setImmediate()`:** Executes a callback after the current I/O cycle completes. Runs in the Check phase.

```js
setImmediate(() => {
  console.log("Runs in check phase");
});
```

**4️⃣ `process.nextTick()`:** Executes a callback immediately after the current operation, before the event loop continues, and before Promises. Runs in the microtask queue.

```js
process.nextTick(() => {
  console.log("Runs before next event loop phase");
});
```

| Timing Feature                           | When to Use                                                                          | Real-World Example                                          | Event Loop Phase |
| ---------------------------------------- | ------------------------------------------------------------------------------------ | ----------------------------------------------------------- | ---------------- |
| `setTimeout()`                           | Delay a task                                                                         | Retry an HTTP request after 2 seconds if it fails           | Timers           |
| `setInterval()`                          | Run recurring tasks                                                                  | Poll a database every 5 minutes for updates                 | Timers           |
| `setImmediate()`                         | Defer until after current I/O                                                        | Log request metrics right after handling an HTTP request    | Check            |
| `process.nextTick()`                     | Run immediately after current operation                                              | Validate input or update internal state before continuing   | Microtask queue  |
| `Promise.then()` / async                 | Run lightweight async tasks after current operation but before next event loop phase | Update cache or internal counters after an async operation  | Microtask queue  |
| `timers/promises` (`await setTimeout()`) | Async/await-friendly delays                                                          | Wait before retrying a failed API call in an async function | Timers           |

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 5. What is the difference between process.nextTick() and setImmediate()?

| Feature                | `process.nextTick()`            | `setImmediate()`                     |
| ---------------------- | ------------------------------- | ------------------------------------ |
| Execution timing       | Before the event loop continues | On the next event loop iteration     |
| Priority               | Very high                       | Lower than nextTick                  |
| Use case               | Defer execution but run ASAP    | Defer execution without blocking I/O |
| Can starve event loop? | Yes, if abused                  | No                                   |

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 6. What is EventEmitter and how does it works?

The EventEmitter is a class that provides communication/interaction between objects in Node.js. That allows objects to emit events and listen for events.

**How EventEmitter works**

- Event Emitter emits the data in an event called message
- A Listened is registered on the event message
- when the message event emits some data, the listener will get the data

**Building Blocks:**

- `.emit()` - This method in event emitter is to emit an event in module
- `.on()` - This method is to listen to data on a registered event in node.js
- `.once()` - It listen to data on a registered event only once.
- `.addListener()` - it checks if the listener is registered for an event.
- `.removeListener()` - It removes the listener for an event.

**Example 1: Basic EventEmitter**

```js
const EventEmitter = require("events");
const myEmitter = new EventEmitter();

// Add listener
myEmitter.on("greet", () => {
  console.log("Hello World!");
});

// Emit event
myEmitter.emit("greet"); // Output: Hello World!
```

**Example 2: Real use case**

```js
const EventEmitter = require("events");

class ChatApp extends EventEmitter {}

const chat = new ChatApp();

// Listener for new message
chat.on("message", (from, to, text) => {
  console.log(`[Message] ${from} → ${to}: ${text}`);
});

// Listener for user login
chat.on("login", (username) => {
  console.log(`[Login] ${username} joined the chat`);
});

// Listener for user logout
chat.on("logout", (username) => {
  console.log(`[Logout] ${username} left the chat`);
});

// Simulate events
chat.emit("login", "Alice");
chat.emit("login", "Bob");

chat.emit("message", "Alice", "Bob", "Hi Bob!");
chat.emit("message", "Bob", "Alice", "Hello Alice!");

chat.emit("logout", "Alice");
chat.emit("logout", "Bob");
```

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 7. What is Streams and Backpressure.?

**Streams** is a way to process data piece by piece (chunks) instead of loading the entire data into memory at once.

**Backpressure** is a flow-control mechanism in streams. For example, during a 2GB file upload, if data arrives faster than the disk can write it, Node automatically pauses the incoming stream and resumes it when the disk catches up. This prevents excessive memory usage and keeps the application stable.

**Follow-Up Questions**

1. Does Node handle backpressure automatically?
   - Yes. When using streams with pipe(), Node automatically manages backpressure by pausing and resuming the flow of data.

**Types of Streams**

| Type          | Description                                                            | Example                            |
| ------------- | ---------------------------------------------------------------------- | ---------------------------------- |
| **Readable**  | Used to **read data** from a source                                    | `fs.createReadStream('file.txt')`  |
| **Writable**  | Used to **write data** to a destination                                | `fs.createWriteStream('file.txt')` |
| **Duplex**    | Can **read and write** data                                            | `net.Socket`                       |
| **Transform** | A special duplex stream that can **modify data while reading/writing** | `zlib.createGzip()`                |

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 8. What buffers?

A Buffer is a temporary memory allocation used to store raw binary data. It is mainly used when handling files, streams, or network data. Buffers allow Node.js to efficiently process binary data outside the JavaScript engine.

**Example 1: Creating a Buffer from a String**

```js
const buf = Buffer.from("Hello Node.js");
console.log(buf);
console.log(buf.toString());

// Output
<Buffer 48 65 6c 6c 6f 20 4e 6f 64 65 2e 6a 73>
Hello Node.js
```

**Example 2: Reading from a File Using Buffers**

```js
const data = fs.readFileSync("example.txt");
console.log(data);           // Shows binary buffer
console.log(data.toString()); // Converts to readable string

// Output
<Buffer 54 68 69 73 20 69 73 20 61 20 62 75 66 66 65 72 20 65 78 61 6d 70 6c 65 21>
This is a buffer example!
```

Buffer.from() converts a string to binary data, and toString() converts it back to a readable string.

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 9. What is REPL?

**REPL stands for Read–Eval–Print–Loop**

It is an interactive Node.js shell that reads user input, evaluates the JavaScript code, prints the result, and then loops back to wait for the next command. It is mainly used for quick testing, debugging.

**Example:**

**Step 1: Start REPL**

```js
// Open terminal and type:
node;

// You will see:
>

> 5 + 5
10
```

- Read → 5 + 5
- Evaluate → Calculates result
- Print → 10
- Loop → Waits for next input

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 10. What is a stub?

A stub is a fake implementation used in testing to replace a real function. It is mainly used in unit testing to avoid calling real databases, APIs, or external services. Using sinon, we replace the HTTP method with a fake response.

**🔹 Example: Actual Function Without Stub (api.js)**

```js
// api.js
const axios = require("axios");

const getUser = async (id) => {
  const response = await axios.get(`https://api.example.com/users/${id}`);
  return response.data;
};

module.exports = getUser;
```

**Unit Test With Stub (api.test.js)**

```js
const sinon = require("sinon");
const axios = require("axios");
const { expect } = require("chai");
const getUser = require("./api");

describe("getUser - with Stub", () => {
  before(() => {
    sinon.stub(axios, "get").resolves({
      data: {
        id: 1,
        name: "John Doe",
        email: "john@example.com",
      },
    });
  });

  after(() => {
    axios.get.restore();
  });

  it("should return user data", async () => {
    const user = await getUser(1);

    expect(user).to.have.property("id");
    expect(user.name).to.equal("John Doe");
    expect(user.email).to.equal("john@example.com");
  });
});
```

Here, we replace the real DB function with a fake one.

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 11. What is a test pyramid?

The Test Pyramid is a testing strategy that recommends having many unit tests, fewer integration tests, and very few end-to-end tests. It ensures fast, reliable, and maintainable testing.

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 12. What Control Flow?

Control flow is the order in which statements, functions, or instructions are executed in a program. In Node.js, it includes handling both synchronous and asynchronous operations.

**🔹 Examples of Control Flow in Node.js**

**Sequential Execution (Synchronous)**

```js
console.log("Start");
console.log("Middle");
console.log("End");

Output: Start;
Middle;
End;
```

**Conditional Execution**

```js
const x = 10;
if (x > 5) {
  console.log("x is greater than 5");
} else {
  console.log("x is 5 or less");
}
```

**Asynchronous Control Flow**

```js
setTimeout(() => {
  console.log("Async operation done");
}, 1000);

console.log("This runs first");

Output:

This runs first
Async operation done
```

Here, the event loop handles the asynchronous control flow.

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 13. What is `spawn()` and `fork()` and difference?

**`spawn()`:** It is a method in Node.js’s child_process module. It is used to creates a child process to run any OS command and streams output via `stdout`/`stderr`

**Example:**

```js
const { spawn } = require("child_process");

// Run the 'ls' command (list files in current directory)
const ls = spawn("ls", ["-l"]);

ls.stdout.on("data", (data) => {
  console.log(`Output:\n${data}`);
});

ls.stderr.on("data", (err) => {
  console.error(`Error: ${err}`);
});

ls.on("close", (code) => {
  console.log(`Child process exited with code ${code}`);
});
```

**`fork()`:** It is a special case of `spawn()` used only to create Node.js child processes with a built-in IPC channel for parent-child communication. Used when you want multiple Node.js scripts to run in parallel and communicate.

**Example:**

```js
//child.js

process.on("message", (msg) => {
  console.log("Child received:", msg);
  process.send(`Hello from child!`);
});

//parent.js

const { fork } = require("child_process");
const child = fork("child.js");

child.on("message", (msg) => {
  console.log("Parent received:", msg);
});

child.send("Hello from parent!");
```

**Key Differences Between spawn() and fork()**
| Feature | `spawn()` | `fork()` |
| ------------- | -------------------------------------- | ------------------------------------------------- |
| Purpose | Run **any command** as child process | Run **Node.js scripts** as child process |
| Communication | Uses **stdout/stderr streams** | Built-in **IPC channel** (`send` / `message`) |
| Usage | `spawn(command, args, options)` | `fork(modulePath, args, options)` |
| Return Type | ChildProcess object | ChildProcess object with **IPC support** |
| Suitable for | Long-running processes, shell commands | Parallel Node.js scripts that need to communicate |

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 14. What is the event loop in Node.js, and how is it handled in depth?

Event-loop is a mechanism that handles asynchronous operations by continuos checking in the call stack and the task queue. When the call stack is empty, it pushes the tasks from the task queue to the call stack, enabling non-blocking, asynchronous execution.

![css_box_model](../assets/images/nodejs_async_code_execution_flow.png)

Now we’ll explain the Node.js event loop strictly phase-by-phase, exactly in this order:

1. Run Synchronous Code
2. Run Microtasks (nextTick → Promises)
3. Timer Queue (Timers Phase)
4. I/O Queue (Pending Callbacks)
5. I/O Polling (Poll Phase)
6. Check Phase (setImmediate)
7. Close Queue

**1️⃣ Synchronous Code (Before Event Loop Starts)**

The event loop first runs all normal JavaScript, including console.log, variable declarations, function calls, and blocking operations like fs.readFileSync() or JSON.parse(). During this stage, async APIs are registered, timers are scheduled, and Promises are created, but nothing asynchronous executes yet.

**2️⃣ Microtasks (Runs Between Phases)**

After each phase, Node executes microtasks, which include process.nextTick() callbacks and Promise .then() callbacks. These run immediately before moving to the next phase, ensuring high-priority tasks complete first. Overusing nextTick() can delay I/O operations.

**3️⃣ Timer Queue (Timers Phase)**

In the timers phase, callbacks scheduled by setTimeout() and setInterval() run if their delay has expired. A 0ms delay does not run immediately; it only executes in this phase when the event loop reaches it. Precise timing is not guaranteed.

**4️⃣ I/O Queue (Pending Callbacks Phase)**

This phase handles some TCP errors, deferred system-level I/O, and certain network error callbacks. Normal file or database callbacks do not run here — they go to the poll phase. The order can be unpredictable.

**5️⃣ I/O Polling (Poll Phase)**

The poll phase is the main phase for executing most asynchronous I/O, including fs.readFile(), database queries, network responses, and HTTP request handlers. It waits for I/O to complete and executes callbacks. If no timers are ready, it can block until an event occurs.

**6️⃣ Check Phase**

The check phase runs callbacks scheduled with setImmediate(). If called inside an I/O callback, setImmediate() executes before setTimeout(). Overusing setImmediate() unnecessarily can reduce performance and confuse timing.

**7️⃣ Close Queue (Close Callbacks Phase)**

The close phase executes callbacks for resources that are fully closed, such as socket.on("close"), stream.on("close"), or server.on("close"). Forgetting cleanup here can cause memory leaks or dangling resources, as the close callbacks do not run immediately.

<!-- **1️⃣ Synchronous Code (Before Event Loop Starts)**

**✅ What Runs Here**

- All normal JavaScript execution
- `console.log`
- Variable declarations
- Function calls
- Blocking operations
- `fs.readFileSync()`
- `JSON.parse()` (large payloads)

**Also during this stage:**

- Async APIs are registered
- Timers are scheduled
- Promises are created

**2️⃣ Important: Microtasks (Runs Between Phases)**

_After every phase, Node executes:_

- `process.nextTick()` callbacks
- Promise `.then()` callbacks

> ⚠️ Overusing nextTick() can starve I/O.

**3️⃣ Timer Queue (Timers Phase)**

**✅ What Runs Here**

- `setTimeout()`
- `setInterval()`

**⚠️ Pitfalls**

- 0ms does NOT mean immediate — it means: "Run in the timers phase when delay has expired
- Assuming exact timing (Node doesn’t guarantee precision)

**4️⃣ I/O Queue (Pending Callbacks Phase)**

**✅ What Runs Here**

- Some TCP errors
- Certain system-level I/O callbacks
- Deferred I/O from previous loop

**⚠️ Pitfalls**

- This is NOT where normal file read callbacks run — those go to Poll phase.
- Hard to predict ordering
- Network error callbacks may appear here

**5️⃣ I/O Polling (Poll Phase)** This is the most important phase.

**✅ What Runs Here**

- `fs.readFile()`
- Database callbacks
- Network responses
- HTTP request handlers
- Most async I/O

**The poll phase:**

- Waits for I/O to complete
- Executes I/O callbacks
- May block waiting for events (if no timers exist)

**6️⃣ Check Phase**

_✅ What Runs Here_

- setImmediate()

_Runs after Poll phase completes._

**Important:** Inside an I/O callback → `setImmediate()` runs before `setTimeout()`.

**⚠️ Pitfalls**

- Confusion between `setTimeout(0)` and `setImmediate()`
- Overusing `setImmediate` unnecessarily

**7️⃣ Close Queue (Close Callbacks Phase)** Final phase of the loop.

**✅ What Runs Here**

- socket.on("close")
- stream.on("close")
- server.on("close")

_Runs when resource is fully closed._

**⚠️ Pitfalls**

- Forgetting cleanup logic
- Memory leaks if resources not properly closed
- Assuming close runs immediately -->

**🎯 Interview-Ready 3-Line Answer**

Node first runs synchronous code, then microtasks (nextTick before Promises).
After that, event loop phases execute in order: Timers → I/O pending → Poll → Check → Close.
Blocking code in any phase can delay the entire loop and hurt performance.

_Repeat until empty._

<details>
<summary>🔥 Tricky Interview Question with deep explanation</summary>

```js
const fs = require("fs");

console.log("start");

setTimeout(() => {
  console.log("timeout");
}, 0);

setImmediate(() => {
  console.log("immediate");
});

fs.readFile(__filename, () => {
  console.log("file read");
});

process.nextTick(() => {
  console.log("nextTick");
});

Promise.resolve().then(() => {
  console.log("promise");
});

console.log("end");
```

**Output**

```js
start
end
nextTick
promise
timeout
immediate
file read
```

### 🔍 Full Breakdown (Event Loop + libuv)

We are running in Node.js.

**1️⃣ Synchronous Code Runs First**

```js
start;
end;
```

**2️⃣ Microtasks Run** - Node has two microtask queues:

1. `process.nextTick()` (higher priority) runs before Promises in Node.
2. Promise queue

```js
nextTick;
promise;
```

**3️⃣ Now the Event Loop Starts**

- Timers Phase

  `setTimeout(..., 0)` goes here.

  ```js
  timeout;
  ```

- Poll Phase

  This is where I/O callbacks run.

  `fs.readFile()` is handled by libuv thread pool.

  _Here’s the key:_
  - fs.readFile is delegated to libuv.
  - libuv uses its thread pool.
  - When finished, callback is queued in the poll phase.

  But depending on timing, the poll phase might not execute it immediately.

- Check Phase

  `setImmediate()` runs here.

  ```js
  immediate;
  ```

- File Read Callback

  When the file read completes, it gets executed in the poll phase:

  ```js
  file read
  ```

**🚨 The Real Trick**

If you move `setImmediate()` inside `fs.readFile()` like this:

```js
fs.readFile(__filename, () => {
  setTimeout(() => console.log("timeout"), 0);
  setImmediate(() => console.log("immediate"));
});
```

Now the output order becomes predictable:

```js
immediate;
timeout;
```

_Why?_

Because when inside an I/O cycle:

- Poll phase finishes
- Then Check phase runs (setImmediate)
- Then next loop → Timers phase (setTimeout)

> This is a VERY common senior interview trick.

**🧩 Where libuv Comes In**

Here’s what many candidates miss:

- fs.readFile() is NOT handled by JavaScript.
- It goes to libuv’s thread pool.
- When finished, libuv pushes callback to poll queue.
- Event loop executes it in the poll phase.

Without libuv, Node could not do async file reading.

So the interaction is:

> **JavaScript → libuv → OS/thread pool → callback → event loop → execution**

**💥 Performance Insight**

If you have any block level code then the event loop cannot move while the call stack is busy. That’s why CPU-heavy work breaks Node performance.

</details>

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 15. What libuv?

libuv is a C library used by Node.js to handle asynchronous I/O operations and implement the event loop. It interacts with the OS (operating system) and manages a thread pool for tasks like file system access and networking. It plays a role similar to Web APIs in the browser, but it’s a lower-level system library used in server-side environments.

**Thread Pool:** Node.js uses libuv thread pool to handle blocking operations like file system, crypto, DNS, and compression. The default size is 4 threads, and tasks are queued when all threads are busy. This allows Node.js to keep the event loop free while handling heavy async work in the background.

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 16. What is a Callback Function?

A callback function is a function passed as an argument to another function and is executed later after a task is completed.

In Node.js, callbacks are mainly used for handling asynchronous operations, like reading files, querying databases, or making HTTP requests.

**Example 1: Simple Callback**

```js
function greet(name, callback) {
  console.log(`Hello, ${name}`);
  callback();
}

function sayGoodbye() {
  console.log("Goodbye!");
}

greet("Alice", sayGoodbye);

// Hello, Alice
// Goodbye!
```

**Example 2: Async Callback with File Read**

```js
const fs = require("fs");

fs.readFile("example.txt", "utf8", (err, data) => {
  if (err) {
    console.error("Error reading file:", err);
    return;
  }
  console.log("File content:", data);
});
```

**Key Points**

- Callbacks enable async programming in Node.js.
- They often follow the error-first pattern: (err, result) => { ... }.
- Using too many nested callbacks can lead to “callback hell”, which is solved by Promises or async/await.

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 17. What is an error-first callback?

An error-first callback is a standard pattern in Node.js for handling `asynchronous` operations.

- The first argument is always reserved for an error (if any occurred).
- The second argument (and others) contains the result of the operation.
- This makes it easy to check for errors before using the data.

**Example 1: Reading a file**

```js
const fs = require("fs");

fs.readFile("example.txt", "utf8", (err, data) => {
  if (err) {
    console.error("Error reading file:", err);
    return; // stop execution if error
  }
  console.log("File content:", data);
});
```

> ✅ Here, err is the first argument, and data is the second argument.

**Example 2: Custom function with error-first callback**

```js
function divide(a, b, callback) {
  if (b === 0) {
    callback(new Error("Division by zero")); // send error
  } else {
    callback(null, a / b); // no error, send result
  }
}

divide(10, 2, (err, result) => {
  if (err) {
    console.error("Error:", err.message);
    return;
  }
  console.log("Result:", result);
});

Output:
a = 2, b = 3
Result: 5

a = 2, b = 0
Error: Division by zero
```

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 18. What is a callback hell and how to avoid it?

Callback Hell happens when you have multiple nested callbacks which makes code hard to read and debug when dealing with asynchronous logic. The callback hell usually looks like a pyramid of doom.

_**Example:**_

```javascript
// Example 1:
async1(function(){
    async2(function(){
        async3(function(){
            async4(function(){
                ....
            });
        });
    });
});

// Example 2:
doSomething(function(err, result1) {
    if (err) throw err;
    doSomethingElse(result1, function(err, result2) {
        if (err) throw err;
        doAnotherThing(result2, function(err, result3) {
            if (err) throw err;
            finalTask(result3, function(err, result4) {
                if (err) throw err;
                console.log('All tasks completed:', result4);
            });
        });
    });
});
```

**Ways to Avoid Callback Hell:**

- **Using Promises**.

  ```js
  doSomething()
    .then((result1) => doSomethingElse(result1))
    .then((result2) => doAnotherThing(result2))
    .then((result3) => finalTask(result3))
    .then((result4) => {
      console.log("All tasks completed:", result4);
    })
    .catch((err) => {
      console.error("Error:", err);
    });
  ```

- **Using async/await**

  ```js
  async function main() {
    try {
      const result1 = await doSomething();
      const result2 = await doSomethingElse(result1);
      const result3 = await doAnotherThing(result2);
      const result4 = await finalTask(result3);

      console.log("All tasks completed:", result4);
    } catch (err) {
      console.error("Error:", err);
    }
  }

  main();
  ```

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 19. What is load balancer and how it works?

A load balancer distributes incoming client requests across multiple servers to improve: Performance, Availability & Scalability.

It sits between the client and the backend servers and forwards requests using algorithms like Round Robin, Least Connections.

**How Does a Load Balancer Work?**

- Client sends request.
- Load balancer receives the request.
- It selects a backend server using a load-balancing algorithm.
- The selected server processes the request.
- Response goes back to the client through the load balancer.

**1️⃣ Load Balancing using Cluster (Built-in Node.js):** NodeJS has a built-in module called Cluster Module. It creates multiple worker processes that share the same server port. Requests are distributed using round-robin (default). Uses multiple CPU cores.

> 🔄 **Flow:** Client → Master Process → Worker 1 / Worker 2 / Worker 3

**Example using Cluster**

```js
const cluster = require("cluster");
const http = require("http");
const os = require("os");

if (cluster.isMaster) {
  const cpuCount = os.cpus().length;

  for (let i = 0; i < cpuCount; i++) {
    cluster.fork(); // create workers
  }
} else {
  http
    .createServer((req, res) => {
      res.end(`Handled by process: ${process.pid}`);
    })
    .listen(3000);
}
```

**2️⃣ Load Balancing using PM2:** PM2 is a production process manager with built-in cluster mode. It allows you to keep applications alive forever. Automatically balances load, Restarts crashed processes and Zero-downtime reload.

```js
pm2 start app.js -i max
```

`-i max` → Runs app on all CPU cores.

**Common Load Balancing Algorithms**

- Round Robin(Default) – Requests are distributed one by one in order.
- Least Connections – Sends request to the server with fewer active connections.
- IP Hash – Uses client IP to decide which server handles the request.

**🔹 Simple Real-World Example**

Imagine your server has 4 CPU cores.

- Without Cluster/PM2:
  - Only 1 core works ❌
  - Other 3 cores idle
- With Cluster or PM2:
  - All 4 cores handle requests ✅
  - Faster response
  - Better performance

> 🔹 Important Note

This is load balancing inside one server (process-level load balancing).
For balancing across multiple servers, you need tools like Nginx or cloud load balancers.

- Cluster and PM2 provide load balancing inside a single server (process-level).
- For load balancing across multiple servers, we required tools like: Nginx or Cloud Load Balancers (AWS ELB, etc.).

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 20. Difference Between Cluster and PM2?

| Feature          | Cluster                 | PM2                       |
| ---------------- | ----------------------- | ------------------------- |
| Type             | Node.js built-in module | External process manager  |
| Setup            | Manual coding required  | Simple CLI commands       |
| Auto restart     | No (manual handling)    | Yes                       |
| Monitoring       | Basic                   | Advanced dashboard & logs |
| Production ready | Needs setup             | Yes                       |

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 21. What is middleware?

Middleware is a function that runs between the request and response cycle. It can perform tasks like authentication, validation, logging, and error handling. It uses the `next()` function to pass control to the next middleware.

> _**👉 Note:** Forgetting to call `next()` can leave requests hanging indefinitely._

**Example:**

```js
const express = require("express");
const app = express();

// Custom middleware
app.use((req, res, next) => {
  console.log("Request received at:", new Date());
  next(); // pass control to next middleware
});

app.get("/", (req, res) => {
  res.send("Hello World");
});

app.listen(3000);

// Here:
// Middleware logs the request
// next() moves control to the route handler
```

**🔹 Types of Middleware**

- Application-level middleware: It runs across the entire Express application.
- Router-level middleware: It runs only for specific route groups
- Error-handling middleware: Error-handling middleware is used to catch and process application errors and has the signature (err, req, res, next).
- Built-in middleware (e.g., express.json()): I have created Role-Based Authorization, Response Formatting, Rate Limiting,

**Interview Follow-Up Questions**

1. What happens if a middleware sends a response and then calls next()?
   - If a middleware sends a response and then calls next(), Express continues executing the next middleware. If the next middleware tries to send another response, Express will throw an error because HTTP allows only one response per request.

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 22. What are the security mechanisms available in Node.js?

**1️⃣ Authentication & Authorization**

- What it protects against:
  - Unauthorized access
  - Privilege escalation
- Common methods:
  - JWT (JSON Web Token)
  - OAuth
  - Sessions
  - Role-based access control (RBAC)

**Example (JWT Authentication Middleware)**

```js
const jwt = require("jsonwebtoken");

function authMiddleware(req, res, next) {
  const token = req.headers.authorization;

  if (!token) {
    return res.status(401).json({ message: "Unauthorized" });
  }

  try {
    const decoded = jwt.verify(token, "secretKey");
    req.user = decoded;
    next();
  } catch (err) {
    return res.status(403).json({ message: "Invalid token" });
  }
}
```

**2️⃣ Input Validation & Sanitization**

- What it protects against:
  - SQL Injection
  - NoSQL Injection
  - XSS attacks

**Example using validation:**

```js
const { body, validationResult } = require("express-validator");

app.post("/user", body("email").isEmail(), (req, res) => {
  const errors = validationResult(req);
  if (!errors.isEmpty()) {
    return res.status(400).json({ errors: errors.array() });
  }
  res.send("Valid input");
});
```

Never trust user input.

**3️⃣ HTTP Security Headers (Helmet):** This automatically sets secure HTTP headers.

- Prevents:
  - Clickjacking
  - XSS
  - MIME sniffing
  - Content injection

**Example:**

```js
const helmet = require("helmet");
app.use(helmet());
```

**4️⃣ Protection Against Common Attacks**

**🔹 CORS Protection** Prevents unauthorized cross-origin requests.

```js
const cors = require("cors");
app.use(cors({ origin: "https://yourdomain.com" }));
```

**🔹 Rate Limiting (Prevent Brute Force & DDoS)** Limits repeated requests.

```js
const rateLimit = require("express-rate-limit");

const limiter = rateLimit({
  windowMs: 15 * 60 * 1000,
  max: 100,
});

app.use(limiter);
```

**5️⃣ Secure Communication (HTTPS / TLS)**

Use HTTPS instead of HTTP:

```js
const https = require("https");
const fs = require("fs");

https
  .createServer(
    {
      key: fs.readFileSync("key.pem"),
      cert: fs.readFileSync("cert.pem"),
    },
    app,
  )
  .listen(443);
```

**6️⃣ Environment Variable Security**

Never store secrets in code:

```js
require("dotenv").config();
const dbPassword = process.env.DB_PASSWORD;
```

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 23. Explain the terms body-parser, cookie-parser, morgan, nodemon, pm2, serve-favicon, cors, dotenv, fs-extra, moment in Express.js??

**1️⃣ body-parser:** Parses incoming request bodies so you can access req.body.

**Used for:**

- JSON data
- Form data

> ⚠️ Note: In modern Express (v4.16+), express.json() replaces body-parser.

**Example:**

```js
app.use(express.json());
app.use(express.urlencoded({ extended: true }));
```

> ⚠️ Note: Without this, req.body will be undefined.

**2️⃣ cookie-parser:** Parses cookies from incoming requests and makes them available in req.cookies.

**Used for:**

- Session management
- Authentication tokens

**Example:**

```js
const cookieParser = require("cookie-parser");
app.use(cookieParser());

app.get("/", (req, res) => {
  console.log(req.cookies);
});
```

**3️⃣ morgan:** HTTP request logger middleware.

**Used for:**

- Logging request method
- URL
- Status code
- Response time

**Example:**

```js
const morgan = require("morgan");
app.use(morgan("dev"));
```

Very useful in development & monitoring.

**4️⃣ nodemon:** Automatically restarts your server when file changes are detected.

Used in development only.

```js
nodemon app.js
```

**5️⃣ PM2:** Production process manager for Node.js.

**Features:**

- Cluster mode
- Auto restart
- Monitoring
- Zero downtime reload

```js
pm2 start app.js -i max
```

**6️⃣ serve-favicon:** Serves favicon efficiently. Prevents unnecessary repeated favicon requests.

**Example:**

```js
const favicon = require("serve-favicon");
app.use(favicon(\_\_dirname + "/public/favicon.ico"));
```

**7️⃣ cors:** Enables Cross-Origin Resource Sharing. Prevents frontend-backend origin blocking issues.

**Example:**

```js
const cors = require("cors");
app.use(cors());
```

Used when frontend & backend run on different domains/ports.

**8️⃣ dotenv:** Loads environment variables from .env file into process.env.

**Used for:**

- Database credentials
- API keys
- Secrets
- Never hardcode secrets.

**Example:**

```js
require("dotenv").config();
console.log(process.env.DB_PASSWORD);
```

**9️⃣ fs-extra** Enhanced version of Node’s built-in fs module.

**Adds:**

- Promise support
- Extra methods like `copy`, `move`, `remove`

**Example:**

```js
const fs = require("fs-extra");
await fs.copy("source.txt", "dest.txt");
```

Cleaner and easier than native fs.

**🔟 moment:** Date and time formatting library.

**Example:**

```js
const moment = require("moment");
console.log(moment().format("YYYY-MM-DD"));
```

> ⚠️ Note: Moment is now considered legacy. Modern alternatives:

- Day.js
- date-fns
- Native Intl

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 24. What are RESTful Web Services?

RESTful web services in Node.js are APIs that follow REST principles using resource-based URLs and standard HTTP methods like GET, POST, PUT, and DELETE. They are stateless and typically return JSON responses with proper HTTP status codes.

**HTTP methods:**

- `GET` → Used to retrieve data.
- `POST` → Used to create new data.
- `PUT` → Used to update/replace existing data completely.
- `PATCH` → Used to partial update of existing data.
- `DELETE` → Used to remove data.

**Uses Standard HTTP Status Codes**

- 200 → OK
- 201 → Created
- 400 → Bad Request
- 401 → Unauthorized
- 404 → Not Found
- 500 → Server Error

> Note: PATCH is used to partially update a resource, while PUT replaces the entire resource.

**🔹 Example: Simple REST API in Node.js (Express)**

```js
const express = require("express");
const app = express();

app.use(express.json());

let users = [];

// GET - Read
app.get("/users", (req, res) => {
  res.status(200).json(users);
});

// POST - Create
app.post("/users", (req, res) => {
  const user = req.body;
  users.push(user);
  res.status(201).json(user);
});

// PUT - Update (Replace Entire Object)
app.put("/users/:id", (req, res) => {
  const id = req.params.id;

  if (!users[id]) {
    return res.status(404).json({ message: "User not found" });
  }

  users[id] = req.body;
  res.status(200).json(users[id]);
});

// PATCH - Partial Update
app.patch("/users/:id", (req, res) => {
  const id = req.params.id;

  if (!users[id]) {
    return res.status(404).json({ message: "User not found" });
  }

  // Merge existing user with new fields
  users[id] = { ...users[id], ...req.body };

  res.status(200).json(users[id]);
});

// DELETE - Remove
app.delete("/users/:id", (req, res) => {
  if (!users[req.params.id]) {
    return res.status(404).json({ message: "User not found" });
  }

  users.splice(req.params.id, 1);
  res.status(200).json({ message: "Deleted" });
});

app.listen(3000);
```

**Comparison**

| Method | Purpose           | Sends Data in Body? | Idempotent? | Example              |
| ------ | ----------------- | ------------------- | ----------- | -------------------- |
| GET    | Read data         | ❌ No               | ✅ Yes      | Get user list        |
| POST   | Create data       | ✅ Yes              | ❌ No       | Create new user      |
| PUT    | Replace full data | ✅ Yes              | ✅ Yes      | Replace user details |
| PATCH  | Partial update    | ✅ Yes              | ✅ Yes      | Update user email    |
| DELETE | Remove data       | ❌ Usually No       | ✅ Yes      | Delete user          |

**🔹 What is Idempotent?**

If you send the same request multiple times and the result remains the same → it is idempotent.

**Example:** DELETE user 5 → Even if you call it 5 times, result is same (user removed).

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 25. Difference Between PUT and PATCH?

PUT replaces the entire resource on the server and requires the full payload. PATCH updates only specified fields and requires a partial payload. Use PUT for complete replacement and PATCH for partial modifications.

| Feature          | PUT                         | PATCH                      |
| ---------------- | --------------------------- | -------------------------- |
| Update Type      | Full resource replacement   | Partial update             |
| Payload Required | Full object                 | Only fields to update      |
| Idempotent       | Yes                         | Yes                        |
| Use Case         | Replace resource completely | Modify only certain fields |

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 26. How many types of API functions are there?

There are two types of API functions in Node.js:

- Synchronous (Sync), Blocking functions API functions
  - These block the execution until the operation completes.
  - Example: fs.readFileSync()
- Asynchronous (Async), Non-blocking API functions
  - These don’t block the execution. They take a callback to handle the result when the operation completes.
  - Example: fs.readFile()

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 27. What is the difference between req.params and req.query?

- `req.params` is used to get route parameters defined in the URL path, like `/users/:id`.
- `req.query` is used to get query string values after the `?`, like `/users?age=25`.
- Params identify a specific resource, while query is mainly used for filtering or searching.

**Example for `req.params`:**

```js
app.get("/users/:id", (req, res) => {
  console.log(req.params.id);
  res.send("User ID received");
});

// GET /users/10
// 10
```

**Example for `req.query`:**

```js
app.get("/users", (req, res) => {
  console.log(req.query.age);
  res.send("Query received");
});

// GET /users?age=25
// 25
```

**Comparison**

| Feature   | req.params        | req.query        |
| --------- | ----------------- | ---------------- |
| Location  | URL path          | After `?` in URL |
| Used For  | Specific resource | Filters/search   |
| Required? | Usually required  | Optional         |
| Example   | `/users/5`        | `/users?age=25`  |

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 28. What is the difference between Asynchronous and Non-blocking?

Asynchronous means a task executes separately and completes later using callbacks or promises.
Non-blocking means the system does not stop execution while waiting for a task, especially I/O operations.
All non-blocking operations are asynchronous, but not all asynchronous operations are non-blocking.

**Example for Asynchronous:**

```js
setTimeout(() => {
  console.log("Done");
}, 2000);

console.log("Start");
```

**Example for Non-blocking:**

```js
const fs = require("fs");

fs.readFile("file.txt", "utf8", (err, data) => {
  console.log(data);
});

console.log("Reading file...");
```

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 29. What are REST, GraphQl and SOAP, and its difference?

**REST**
REST is an architectural style for building APIs that use standard HTTP methods to access and manage resources, usually returning data in JSON format in a simple and scalable way.

```js
// Request:
GET /users/1

// Response:
{
  "id": 1,
  "name": "John",
  "email": "john@example.com"
}
```

**GraphQL**
GraphQL is a query language for APIs that allows the client to request exactly the data it needs from a single endpoint, making data fetching more flexible and efficient.

```js
// Request:
query {
  user(id: 1) {
    name
    email
  }
}

// Response:
{
  "data": {
    "user": {
      "name": "John",
      "email": "john@example.com"
    }
  }
}
```

**Interview Follow-Up Questions**

1. What is the N+1 Problem in GraphQL and How Does DataLoader Solve It?
   - The N+1 problem occurs when GraphQL executes one query to fetch records and then N additional queries to fetch related data. DataLoader solves this by batching multiple requests into a single database query and caching results within the same request. This significantly reduces database calls and improves GraphQL performance and scalability.

**SOAP**
SOAP is a protocol for exchanging structured information using XML, mainly used in enterprise systems where strict standards, security, and reliability are required.

```js
// Request:
<soap:Envelope>
  <soap:Body>
    <GetUser>
      <UserId>1</UserId>
    </GetUser>
  </soap:Body>
</soap:Envelope>

// Response:
<soap:Envelope>
  <soap:Body>
    <GetUserResponse>
      <User>
        <Id>1</Id>
        <Name>John</Name>
        <Email>john@example.com</Email>
      </User>
    </GetUserResponse>
  </soap:Body>
</soap:Envelope>
```

**🔎 Comparison**

| Feature     | REST                | GraphQL                 | SOAP             |
| ----------- | ------------------- | ----------------------- | ---------------- |
| Type        | Architectural style | Query language          | Protocol         |
| Data Format | JSON (mostly)       | JSON                    | XML only         |
| Endpoints   | Multiple endpoints  | Single endpoint         | Single endpoint  |
| Flexibility | Fixed response      | Client-defined response | Strict structure |

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 30. What is crypto in Node.js?

The crypto module in Node.js is a built-in module used for cryptographic operations like hashing, encryption, decryption, and generating secure random data. It is commonly used for password hashing, tokens, and data security.

**🔹 Example 1: Hashing a Password**

```js
const crypto = require("crypto");

const hash = crypto.createHash("sha256").update("mypassword").digest("hex");

console.log(hash);
```

This converts a password into a secure hash.

```js
🔹 Example 2: Generate Random Token
const crypto = require("crypto");

const token = crypto.randomBytes(16).toString("hex");
console.log(token);
```

Used for: Password reset tokens, API keys & Session IDs

**🔹 Common Methods**

- `createHash()` → Create hash (SHA256, MD5, etc.)
- `createCipheriv()` → Encrypt data
- `createDecipheriv()` → Decrypt data
- `randomBytes()` → Generate secure random values

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 31. How to debug an application in Node.js?

Node.js applications can be debugged using console logs, the built-in Node inspector, or IDE debuggers like VS Code.

In production, tools like PM2 logs and debugging libraries help track errors and performance issues.

**🔹 1️⃣ Using console.log() (Basic Debugging)**

The simplest way:

```js
console.log("Value of x:", x);
```

Used to: Check variable values, Verify execution flow.

**🔹 2️⃣ Using Node.js Built-in Debugger**

Run your app with:

```js
node inspect app.js

// Or:

node --inspect app.js

// Then open:

chrome://inspect
```

**🔹 3️⃣ Using VS Code Debugger (Most Common)**

- Steps:
  - Open project in VS Code
  - Go to Run & Debug
  - Click Add Configuration
  - Select Node.js
  - Set breakpoints
  - Press ▶️ Run
- You can:
  - Pause execution
  - Step over / into functions
  - Inspect variables
  - Watch expressions

**🔹 4️⃣ Using debug Module (Advanced Logging)**

Install:

```js
npm install debug

// Example:

const debug = require("debug")("app");

debug("Server started");

// Run with:

DEBUG=app node app.js
```

Used for controlled logging in production.

**🔹 5️⃣ Using PM2 Logs (Production Debugging)**

If running with PM2:

```js
pm2 logs
```

Used to monitor: Errors, Crashes & Performance

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 32. What is Garbage collection and how it works?

Garbage collection is the automatic process of freeing unused memory in Node.js. Node.js memory is divided into code segment, stack, and heap. Garbage collection only works on heap memory where objects are stored. The V8 engine uses a mark-and-sweep algorithm to remove unreachable objects from memory.

- **Code Segment:** Stores the program’s instructions and function definitions. This memory is static and does not change during execution.
- **Stack:** Holds function calls, local variables, and execution contexts in LIFO order. It is automatically cleared when functions finish executing.
- **Heap:** Stores objects, arrays, and dynamic data. Garbage collection works here to remove unreachable objects and free memory.

**🔹 How Garbage Collection Works in Node.js**

Node.js uses the V8 engine’s garbage collector, which mainly follows a Mark-and-Sweep algorithm.

- **Memory Allocation:** When you create variables, objects, or functions. Memory is allocated in the heap.
- **Mark Phase:** The garbage collector starts from the root object (global scope) and marks all objects that are still reachable (in use). If an object can be accessed, it is marked as active.
- **Sweep Phase:** After marking, V8 removes all unmarked (unreachable) objects from memory. Now the original object is unreachable → GC will remove it.

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 33. What memory leaks and its types?

A memory leak occurs when unused memory is not released and heap usage keeps increasing.

It usually happens due to global variables, unremoved listeners, timers, or retained references. It can be prevented by proper cleanup, limiting cache, and monitoring memory usage.

**🔹 How to Prevent Memory Leaks**

- Avoid Global Variables
- Remove Event Listeners
- Clear Timers
- Limit Cache Size
- Close Database Connections
- Use WeakMap / WeakSet for temporary references
- Monitor Memory Usage (`process.memoryUsage()`)

**🔹 Types of Memory Leaks in Node.js**

**1️⃣ Global Variables:** Objects stored in global scope are never garbage collected. Since it’s globally referenced, GC cannot remove it.

**2️⃣ Unused References (Forgot to Nullify):** If references are not removed, memory stays allocated. If not set to null or removed, GC won’t clean it.

```js
let data = { name: "John" };
data = null; // Proper cleanup
```

**3️⃣ Closures Holding Memory:** Closures can unintentionally retain large objects. `largeData` remains in memory due to closure reference.

```js
function outer() {
  const largeData = new Array(1000000);
  return function inner() {
    console.log("Using closure");
  };
}
```

**4️⃣ Unremoved Event Listeners:** If listeners are not removed, they keep references alive.

```js
emitter.on("data", handler);

// Remove
emitter.removeListener("data", handler);
```

**5️⃣ Timers Not Cleared:** Uncleared intervals keep running and holding memory.

```js
const interval = setInterval(() => {
  console.log("Running");
}, 1000);

// clearInterval(interval);
```

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 34. How do you identify and debug memory leaks?

I first monitor heap memory usage. If memory continuously grows and doesn't reduce after garbage collection, I suspect a memory leak. Then I take heap snapshots using Chrome DevTools or Node Inspector, compare snapshots over time, identify growing objects, and trace why references to those objects are not being released.

**How to Debug It?**

1. Monitor Memory

   ```js
   setInterval(() => {
     console.log(process.memoryUsage());
   }, 5000);

   heapUsed;
   heapTotal;
   rss;

   // If heapUsed continuously grows, investigate further.
   ```

2. Take Heap Snapshots

   ```js
   node --inspect app.js

    // Open Chrome:
    chrome://inspect

    // Then:

    Memory Tab
    ↓
    Take Heap Snapshot

    // Take:

    Snapshot 1
    ↓
    Generate Traffic
    ↓
    Snapshot 2

    // Compare both snapshots.
   ```

3. Monitor Using PM2

   ```js
   // Start application:

   pm2 start app.js

   // Monitor:

   pm2 monit

   // Look for:

   Memory: 200 MB
   Memory: 400 MB
   Memory: 800 MB
   Memory: 1.5 GB

   // If memory continuously grows, investigate further.
   ```

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 35. Explain Error Handling approaches in Node.js?

**1. Using try-catch block:**

```js
function square(num) {
  if (typeof num !== "number")
    throw new TypeError(`Expected number but got: ${typeof num}`);

  return num * num;
}

try {
  square("10");
} catch (err) {
  console.log(err.message); // Expected number but got: string
}
```

**2. Error-First Callbacks (Classic Node.js):** The traditional Node.js pattern passes error as the first argument to a callback.

```js
fs.readFile("file.txt", (err, data) => {
  if (err) {
    console.error("Error reading file:", err);
    return;
  }
  console.log("File data:", data.toString());
});
```

**3. Promises:** Promises allow handling errors using .catch() while keeping code readable.

```js
const fs = require("fs").promises;

fs.readFile("file.txt")
  .then((data) => console.log("File data:", data.toString()))
  .catch((err) => console.error("Error reading file:", err));
```

**4. Async / Await:** With async/await, errors can be handled using try/catch blocks, making asynchronous code look synchronous.

```js
const fs = require("fs").promises;

async function readFile() {
  try {
    const data = await fs.readFile("file.txt");
    console.log("File data:", data.toString());
  } catch (err) {
    console.error("Error reading file:", err);
  }
}

readFile();
```

**5. Using Error Middleware (Express.js):** In Express.js apps, use a middleware to catch errors:

```js
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).send("Something broke!");
});
```

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 36. What is Redis and how to implement it?

Redis is an open-source, in-memory data store used as a database, cache, and message broker. It follows a key-value storage model, allowing data to be stored and retrieved directly from RAM using commands like `SET` and `GET`. It supports data types like strings, lists, sets, sorted sets, and hashes.

| Data Type      | Description                                                   |
| -------------- | ------------------------------------------------------------- |
| **String**     | Simple key-value, can store text, numbers, or JSON as string. |
| **List**       | Ordered collection of strings (like an array).                |
| **Set**        | Unordered collection of unique strings.                       |
| **Sorted Set** | Set of strings with scores for ordering.                      |
| **Hash**       | Map of fields and values (like an object).                    |

**🔹 How to Implement Redis in Node.js**

**🔹 Example: Basic Key-Value Operations**

```js
const redis = require("redis");

// Create Redis client
const client = redis.createClient();

client.on("error", (err) => console.error("Redis Error:", err));

async function run() {
  await client.connect(); // Connect to Redis server

  // Set a key-value
  await client.set("username", "JohnDoe");

  // Get the value
  const username = await client.get("username");
  console.log("Username from Redis:", username);

  // Delete the key
  await client.del("username");

  await client.quit(); // Disconnect
}

run();
```

**🔹 Example: Using a Hash**

```js
async function hashExample() {
  await client.connect();

  // Set multiple fields in a hash
  await client.hSet("user:1", {
    name: "Alice",
    age: "25",
    email: "alice@example.com",
  });

  // Get all fields
  const user = await client.hGetAll("user:1");
  console.log("User Hash:", user);

  await client.quit();
}

hashExample();
```

**Example: Database + Redis Cache**

```js
const express = require("express");
const mongoose = require("mongoose");
const redis = require("redis");

const app = express();
app.use(express.json());
const PORT = 3000;

// Redis client
const client = redis.createClient();
client.on("error", (err) => console.error("Redis Error:", err));

// MongoDB connection
mongoose.connect("mongodb://localhost:27017/usersdb", {
  useNewUrlParser: true,
  useUnifiedTopology: true,
});

// User schema
const userSchema = new mongoose.Schema({
  name: String,
  email: String,
});
const User = mongoose.model("User", userSchema);

// GET user with Redis caching
app.get("/user/:id", async (req, res) => {
  const userId = req.params.id;

  try {
    // 1️⃣ Check Redis first
    const cachedUser = await client.get(`user:${userId}`);
    if (cachedUser) {
      console.log("Serving from Redis cache");
      return res.json(JSON.parse(cachedUser));
    }

    // 2️⃣ If not in cache, fetch from MongoDB
    const user = await User.findById(userId);
    if (!user) return res.status(404).json({ message: "User not found" });

    // 3️⃣ Store result in Redis for 1 hour (3600 seconds)
    await client.setEx(`user:${userId}`, 3600, JSON.stringify(user));

    console.log("Serving from MongoDB");
    res.json(user);
  } catch (err) {
    console.error(err);
    res.status(500).json({ error: "Internal Server Error" });
  }
});

app.listen(PORT, async () => {
  await client.connect();
  console.log(`Server running on http://localhost:${PORT}`);
});
```

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 37. How to improve Node.js performance?

**1. Use Asynchronous & Non-Blocking Code**

- Avoid blocking the event loop with synchronous operations like fs.readFileSync or heavy loops.
- Use async APIs, Promises, or async/await for I/O and database calls.

  ```js
  // Bad: blocking
  const data = fs.readFileSync("file.txt");

  // Good: non-blocking
  fs.readFile("file.txt", (err, data) => { ... });
  ```

**2. Query Optimization**

Basic tips to improve your database performance/optimization overview

- Indexing - Indexing is an approach to optimize the performance of a database by minimizing the number of disk accesses required when a query is processed.
- Avoid SELECT - Use the SELECT statement to query only the data you need and avoid extra fetching loads to your database.

  ```js
  -- query1
  SELECT * FROM Customers

  -- query2 (optimized)
  SELECT FirstName, LastName, Address, City, State, Zip FROM Customers
  ```

- Use LIMIT - LIMIT will return only the specified number of records.

  ```js
  SELECT FirstName, LastName, Address, City, State, Zip FROM Customers LIMIT 100
  ```

- Wildcard (%) - Use wildcard (%) character appropriately

  ```js
  -- SELECT customers whose first names start with "Avi"

  -- query1
  SELECT FirstName from Customers where FirstName like '%avi%'

  -- query2 (optimized)
  SELECT FirstName from Customers where FirstName like 'avi%'
  ```

**3. Implement Caching**

- Use Redis or in-memory caches for frequently accessed data to reduce database calls.
- Cache API responses, computed values, or session data.

**4. Load Balancing:**

The cluster module to allow load balancing and distribute incoming connections across all workers in an environment's numerous CPU cores using a round-robin technique.

Using the PM2 process manager to keep applications alive indefinitely is another option. PM2 includes a cluster feature that allows you to run numerous processes over all cores without having to worry about changing the code to use the native cluster module.

**5. Gzip Compression**

Gzip compresses HTTP requests and responses.
Gzip compresses responses before sending them to the browser, thus, the browser takes a shorter time to fetch them. Gzip also compresses the request to the remote server, which significantly increases web performance.

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 38. How to use JSON Web Token (JWT) for authentication?

JWT is a secure token-based authentication mechanism.
Users log in and receive a signed JWT, which they send in request headers to access protected routes.
The server verifies the token on each request, allowing stateless, scalable authentication without storing sessions.

**🔹 How It Works**

- Login: User sends credentials → Server verifies → Generates JWT → Returns token.
- Access protected route: Client sends token in Authorization: Bearer <token> → Server verifies token → Grants access if valid.
  -Token expires automatically based on the expiresIn setting.

**Example**

```js
const express = require("express");
const jwt = require("jsonwebtoken");
const bcrypt = require("bcrypt");

const app = express();
app.use(express.json());

const SECRET_KEY = "mysecretkey"; // In production, store securely

// Mock user database
const users = [
  { id: 1, username: "john", password: "$2b$10$k4mN..." }, // hashed password
];

// Login route
app.post("/login", async (req, res) => {
  const { username, password } = req.body;
  const user = users.find((u) => u.username === username);
  if (!user) return res.status(401).json({ message: "Invalid credentials" });

  const valid = await bcrypt.compare(password, user.password);
  if (!valid) return res.status(401).json({ message: "Invalid credentials" });

  // Generate JWT token
  const token = jwt.sign({ id: user.id, username: user.username }, SECRET_KEY, {
    expiresIn: "1h",
  });
  res.json({ token });
});

// Protected route
app.get("/profile", (req, res) => {
  const authHeader = req.headers["authorization"];
  if (!authHeader)
    return res.status(401).json({ message: "No token provided" });

  const token = authHeader.split(" ")[1];
  try {
    const user = jwt.verify(token, SECRET_KEY);
    res.json({ message: "Profile data", user });
  } catch (err) {
    res.status(403).json({ message: "Invalid token" });
  }
});

app.listen(3000, () => console.log("Server running on http://localhost:3000"));
```

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 39. In a large application with around 100 protected APIs, would you perform JWT authentication and RBAC authorization checks on every request?

Yes, every protected API verifies the access token because JWT authentication is stateless.

We use short-lived access tokens(15 - 30min) and validate them on every protected request. To keep users logged in, we use refresh tokens(7 - 15days) to generate new access tokens when they expire. This approach provides better security while avoiding frequent logins and reducing the impact of stale permissions.

We validate JWT on every protected request because authentication is stateless. For RBAC, we typically store role information in the token to avoid database lookups. If permissions must take effect immediately, I use token versioning, where the token version is stored in both the JWT and Redis. When roles or permissions change, the version is incremented, causing all previously issued tokens to become invalid instantly.

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 40. How did you implement logging in your project and its types?

We used Winston for structured JSON logging. We logged API requests, responses, errors, and audit events. Each request was assigned a correlation ID to trace it across services. Logs were centralized in ELK/CloudWatch for monitoring and troubleshooting.

ELK and CloudWatch are centralized logging platforms used to collect, store, and analyze application logs. ELK consists of Elasticsearch, Logstash, and Kibana, while CloudWatch is AWS's managed logging service. They help teams search logs, trace requests using correlation IDs, monitor errors, and create alerts.

1. Application Logs: Normal application activity. Used for monitoring and debugging. Logs will store 30-90 Days.
2. Error Logs: When something fails. Used for troubleshooting. Logs will store 90 Days.
3. Audit Logs: Tracks who did what. Used for compliance and security. Logs will store 1-7 Years.

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 41. How microservices communicate with each other?

Microservices can communicate synchronously using REST, GraphQL, or gRPC, and asynchronously using message brokers like Kafka or RabbitMQ.

I use synchronous communication when an immediate response is needed and asynchronous communication for scalable event-driven workflows.

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 42. RabbitMQ and Kafka in Node.js?

RabbitMQ is a message broker primarily used for task queues and reliable message delivery. Once a message is consumed, it is typically removed from the queue. Kafka is an event streaming platform where events are stored for a configurable retention period and can be consumed by multiple services independently. I generally use RabbitMQ for background jobs and Kafka for event-driven architectures, analytics, and high-throughput systems.

**Follow-Up Questions**

1. What happens if a consumer is down?
   - **RabbitMQ:** Message stays in the queue until a consumer processes it.
   - **Kafk:** Message remains in the topic and can be consumed later.

2. Can multiple consumers read the same message?
   - **RabbitMQ:** Typically one message is processed by one consumer (within a consumer group/queue pattern).
   - **Kafka** Many independent consumer groups can read the same event.

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 43. What is Connection pooling?

Connection pooling is a mechanism that maintains a reusable set of database connections. Instead of creating and closing a connection for every request, the application borrows a connection from the pool, executes the query, and returns it back. This reduces connection overhead, improves response time, and helps applications handle high traffic efficiently.

In Node.js, libraries like MySQL2 and PostgreSQL provide built-in connection pooling support. While configuring pools, I ensure the total number of connections across all application instances stays within the database server's connection limit.

**Real-World Analogy**

Imagine a company has 100 employees and only 10 meeting rooms. Employees don't build a new meeting room every time they need one.

- Take an available room.
- Conduct the meeting.
- Leave the room.
- The room becomes available for others.

A connection pool works the same way.

```javascript
// Node.js Example (MySQL)

const mysql = require("mysql2");

const pool = mysql.createPool({
  host: "localhost",
  user: "root",
  password: "password",
  database: "testdb",
  connectionLimit: 10,
});

// Using the pool:
pool.query("SELECT * FROM users", (err, results) => {
  console.log(results);
});
```

**Interview Follow-Up**

1. What happens if all connections are busy?
   - First 10 requests get connections. Remaining 40 requests wait in a queue. As connections are released, waiting requests receive them. If the wait exceeds the configured timeout, an error may occur.

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 44. What is Worker Threads vs Cluster vs Child Process, difference, and when to use?

**Worker Threads** are used when your Node application has CPU-intensive work such as image processing, PDF generation, encryption, or large calculations. They create additional JavaScript threads within the same process.

When to Use: Image processing, Video processing, PDF generation, Data transformation, Encryption, and CPU-heavy calculations.

```javascript
const worker = new Worker("./imageProcessor.js");
```

_A user uploads a large image and resizing it takes 5 seconds. Running this in the main thread would block all requests. A Worker Thread prevents that._

**Cluster** is used when you want to scale your Node server across multiple CPU cores. Each cluster worker is a separate Node process that can handle incoming requests independently.

When to Use: Running Express APIs, High traffic applications, and Multiple CPU cores available.

```javascript
const cluster = require("cluster");
const os = require("os");

if (cluster.isPrimary) {
  for (let i = 0; i < os.cpus().length; i++) {
    cluster.fork();
  }
}
```

_If a server has 8 cores, cluster can create 8 Node processes so all cores are utilized._

**Child Process** is used when you need to execute an external process or program such as Python scripts, shell commands, FFmpeg, Git commands, or another Node application.

When to Use: Running Python scripts, Executing shell commands, Using FFmpeg, and Calling external tools.

```javascript
const { spawn } = require("child_process");

spawn("python", ["predict.py"]);
```

_A Node API receives an image and sends it to a Python AI model for prediction._

> _**👉 Note:** All three help Node.js perform work outside the main Event Loop, but they solve different problems.._

**Think of it like this:**

- Worker Thread → "Help me do heavy calculations."
- Cluster → "Help me serve more users."
- Child Process → "Help me run another application."

**When to Use**

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

**Worker Threads**
**Cluster**
**Child Process**

**Follow-Up Questions**

- Why not use Worker Threads for database queries?
  - Database queries are I/O operations. Node already handles I/O asynchronously through the Event Loop and libuv. Using Worker Threads adds unnecessary overhead.
- What is the difference between Cluster and Worker Threads?
  - Cluster creates multiple Node processes, each with its own memory and Event Loop. Worker Threads create multiple threads inside the same Node process and can share memory using SharedArrayBuffer.Cluster is for scaling servers. Worker Threads are for CPU-intensive tasks.

### Q 45. How to Handle a 2GB File Upload in Node.js?

For large files such as 2GB, I would implement chunked uploads where the file is split into smaller pieces, typically 5MB each. The backend stores each chunk and merges them after all chunks are received. In production, I would use parallel uploads, streaming, and resumable uploads with metadata stored in Redis or a database.

**Follow-Up Questions**

- Why use chunk upload instead of a single upload?
  - If the network fails at 95%, only the failed chunk needs to be retried instead of uploading the entire 2GB file again.
- How would you implement resumable uploads?
  - Generate an uploadId, store uploaded chunk numbers in Redis or a database, and when the user reconnects, upload only the missing chunks.

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 46. How does Node handle concurrency?

Node.js handles concurrency using the Event Loop, libuv, and non-blocking I/O. When an operation like a database query, file read, or external API call is made, Node doesn't wait for it to complete. Instead, it delegates the work to libuv and continues processing other requests. Once the operation finishes, the callback is placed back in the Event Loop for execution. This enables a single Node.js process to handle thousands of concurrent connections efficiently.

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 47. How do you scale a Node.js application?

I scale Node.js applications both vertically and horizontally. For a single server, I use Cluster to utilize all CPU cores, and for larger systems, I deploy multiple instances behind a load balancer. I also use Redis, connection pooling, and database optimization to eliminate backend bottlenecks.

There are two main ways to scale a Node.js application:

1. **Vertical Scaling (Scale Up):** Increase server resources:

   ```js
   2 CPU → 8 CPU
   4 GB RAM → 16 GB RAM
   ```

   - **Pros:** Simple and No code changes.
   - **Cons:** Hardware limit exists and Expensive

2. **Horizontal Scaling (Scale Out):** Run multiple application instances.

   ```js
          Load Balancer
                ↓
     ┌──────────┼──────────┐
     ↓          ↓          ↓
   Node 1     Node 2     Node 3
   ```

   - **Pros:** Better scalability and High availability
   - **Cons:** More infrastructure complexity

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 48. Database Scaling?

I usually start database scaling with query optimization, indexing, and connection pooling. If traffic continues to grow, I introduce Redis caching and read replicas to reduce database load. For very large systems, I consider sharding and horizontal database scaling.

1. **Connection Pooling:** Maintains a pool of reusable database connections instead of creating a new connection for every request. This reduces connection overhead and improves database performance.

2. **Redis Caching;** Stores frequently accessed data in memory so requests can be served faster without hitting the database. This reduces database load and improves response times.

3. **Read Replicas:** Creates one or more copies of the primary database to handle read queries. This helps distribute read traffic and reduces load on the primary database to INSERT, UPDATE, DELETE.

4. **Database Indexing:** Creates a data structure that allows the database to find records quickly without scanning the entire table. It improves read performance but can slow down writes.

5. **Query Optimization:** Improves SQL queries by reducing unnecessary scans, joins, and computations. Often the cheapest and most effective way to improve database performance.

6. **Sharding:** Splits data across multiple database servers based on a sharding key (e.g., User ID). Used when a single database can no longer handle the volume of data or traffic.

7. **Partitioning:** Divides a large table into smaller logical partitions within the same database. This improves query performance and makes large datasets easier to manage.

8. **Materialized Views:** Stores precomputed query results so expensive aggregations don't need to run repeatedly. Useful for reporting and analytics workloads.

9. **Denormalization:** Stores duplicate data to reduce joins and improve read performance. Common in high-read applications where performance is more important than storage efficiency.

10. **Archiving:** Moves old or rarely accessed data to separate storage or tables. This keeps active tables smaller and improves query performance.

> I use Partitioning when a table becomes very large but still fits within a single database server. I use Sharding when a single database server can no longer handle the storage, traffic, or resource requirements. Partitioning improves query performance, while Sharding improves overall scalability.

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 49. MySQL vs PostgreSQL vs MongoDB?

**MySQL:** MySQL is an open-source relational database management system (RDBMS) that stores data in tables consisting of rows and columns and uses SQL (Structured Query Language) to manage and query data.

- Use for: E-commerce, Blogging platforms, & Traditional web applications

**PostgreSQL:** PostgreSQL is an advanced open-source object-relational database management system (ORDBMS) that extends traditional relational database capabilities with advanced features such as JSON support, complex queries, custom data types, and strong ACID compliance.

- Use for: Complex reporting systems, Banking systems, & SaaS products

**MongoDB:** MongoDB is a NoSQL document-oriented database that stores data in flexible JSON-like documents (BSON) instead of tables and rows, allowing dynamic schemas and rapid application development.

- Use for: Rapidly changing data structures, Social media, & Content management.

| Feature         | MySQL            | PostgreSQL         | MongoDB                                |
| --------------- | ---------------- | ------------------ | -------------------------------------- |
| Type            | Relational       | Relational         | NoSQL                                  |
| Schema          | Fixed            | Fixed              | Flexible                               |
| Joins           | Yes              | Yes                | Limited                                |
| ACID            | Yes              | Strong             | Yes (multi-document support available) |
| Complex Queries | Good             | Excellent          | Limited                                |
| JSON Support    | Basic            | Excellent          | Native                                 |
| Scalability     | Good             | Excellent          | Excellent                              |
| Best For        | Traditional Apps | Enterprise Systems | Flexible Data Models                   |

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 50. TypeORM vs Prisma?

**TypeORM:** TypeORM is a traditional ORM (Object Relational Mapper) that maps database tables directly to TypeScript/JavaScript classes using decorators.

```ts
@Entity()
class User {
  @PrimaryGeneratedColumn()
  id: number;

  @Column()
  name: string;
}
```

**Prisma:** Prisma is a modern type-safe ORM that generates a database client from a schema file, providing autocompletion and compile-time type safety.

```ts
model User {
id Int @id @default(autoincrement())
name String
}
const users = await prisma.user.findMany();
```

- Which ORM would you choose for a new Node.js project?
  - Prisma. It provides excellent TypeScript support, better developer experience, and compile-time type safety.

- Why do many teams move from TypeORM to Prisma?
  - Because Prisma offers better type safety, simpler migrations, improved autocompletion, and fewer runtime surprises.

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 51. Database Transactions?

A Transaction is a group of database operations that are executed as a single unit of work.

Either: `All operations succeed` or `All operations fail (Rollback)`.

```js
// Bank Transfer: Suppose: John Account = ₹1000 and Mike Account = ₹500. John transfers: ₹200 → Mike

Steps:

1. Deduct ₹200 from John
2. Add ₹200 to Mike

// If step 1 succeeds and step 2 fails: John = ₹800 and Mike = ₹500. Money is lost ❌

// Using a transaction:

BEGIN;

UPDATE accounts
SET balance = balance - 200
WHERE id = 1;

UPDATE accounts
SET balance = balance + 200
WHERE id = 2;

COMMIT;

// If any step fails:

ROLLBACK;

// Database returns to the original state.
```

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 52. ACID Properties?

ACID properties are implemented by the database engine, not manually by developers. In applications, we use transactions with BEGIN, COMMIT, and ROLLBACK to ensure Atomicity, while the database handles Consistency, Isolation, and Durability internally through constraints, isolation levels, and transaction logs.

- **A - Atomicity** Either everything happens or nothing happens.
- **C - Consistency** Data must always remain valid before and after a transaction.
- **I - Isolation** Multiple transactions should not interfere with each other. Example: Two users update the same account simultaneously. Database ensures transactions are handled safely.
- **D - Durability** Once committed, data is permanently stored even if the database crashes.

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 53. Design Patterns?

Design patterns are reusable solutions to common software design problems. In backend development, I frequently use Singleton for database connections, Strategy for payment processing, Observer for event-driven systems, Factory for object creation, and Repository to separate business logic from data access.

1. **Singleton Pattern:** Ensures only one instance of a class exists throughout the application. Used For Database connections and Redis clients.

2. **Factory Pattern:** Creates objects without exposing the creation logic. Used For Payment gateways and Notification providers

3. **Strategy Pattern:** Allows switching algorithms or behaviors at runtime. Used For
   Payment systems, Discount calculations, and Tax calculations

4. **Observer Pattern:** One object notifies multiple objects when an event occurs. Used For
   Event-driven architecture, Notifications, and Microservices events

5. **Repository Pattern:** Separates database access from business logic.

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 54. Normalization?

Normalization is the process of organizing data into multiple related tables to reduce data duplication and improve data consistency.

`1NF` ensures each column contains a single value, `2NF` removes duplicate data by separating entities into related tables, and `3NF` removes transitive dependencies where a non-key column depends on another non-key column. Together, they reduce redundancy and improve data consistency.

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 55. Optimistic Locking vs Pessimistic Locking?

Both are techniques used to handle concurrent updates to the same data.

**Optimistic Locking:** Assumes conflicts are rare. Instead of locking the row, it checks whether someone else modified the data before saving. Usually implemented using a: version column or timestamp column. Used in E-commerce and Low chance of conflicts.

**Pessimistic Locking:** Assumes conflicts are likely. Locks the row immediately so nobody else can modify it. Used in Banking and Payment Systems.

| Feature           | Optimistic   | Pessimistic         |
| ----------------- | ------------ | ------------------- |
| Locks Data?       | No           | Yes                 |
| Performance       | Faster       | Slower              |
| Concurrency       | High         | Lower               |
| Conflict Handling | Detect Later | Prevent Immediately |
| Best For          | Web Apps     | Banking/Payments    |

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 56. N+1 Query Problem (Very Common ORM Interview Question).?

The N+1 Query Problem occurs when an application executes one query to fetch parent records and then executes additional queries for each related record. This causes excessive database calls and poor performance. I typically solve it using JOINs, eager loading, or ORM relation loading to fetch related data in a single query.

```ts
// Bad
const users = await userRepository.find();

for (const user of users) {
  user.orders = await orderRepository.find({
    where: { userId: user.id }
  });
}

// Good
SELECT *
FROM users u
LEFT JOIN orders o
ON u.id = o.user_id;
```

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div>

### Q 57. SQL JOINs (INNER JOIN vs LEFT JOIN vs RIGHT JOIN vs FULL JOIN).?

Joins are used to combine data from multiple tables based on a related column.

```js
// Example Tables
// Users
id | name
-----------
1  | John
2  | Mike
3  | David
// Orders
id | user_id | product
----------------------
1  | 1       | Laptop
2  | 1       | Mouse
3  | 2       | Mobile
```

1. **INNER JOIN:** Returns only matching records from both tables. Use it When you only want records that exist in both tables.

   ```js
   SELECT u.name, o.product
   FROM users u
   INNER JOIN orders o
   ON u.id = o.user_id;

   // Result
   John   Laptop
   John   Mouse
   Mike   Mobile
   ```

2. **LEFT JOIN:** Returns all rows from the left table and matching rows from the right table.

   ```js
   // Query
   SELECT u.name, o.product
   FROM users u
   LEFT JOIN orders o
   ON u.id = o.user_id;

   // Result
   John   Laptop
   John   Mouse
   Mike   Mobile
   David  NULL
   ```

3. **RIGHT JOIN:** Returns all rows from the right table and matching rows from the left table.

   ```js
   // Query
   SELECT u.name, o.product
   FROM users u
   RIGHT JOIN orders o
   ON u.id = o.user_id;

   // Result

   John   Laptop
   John   Mouse
   Mike   Mobile
   ```

4. **FULL JOIN:** All rows from Left Table + All rows from Right Table. Whether matching or not.

   ```js
   // Query
   SELECT u.name, o.product
   FROM users u
   FULL JOIN orders o
   ON u.id = o.user_id;

   // Result
   John   Laptop
   John   Mouse
   Mike   Mobile
   David  NULL
   NULL   Tablet
   ```

<!-- ### Q 36. ?

<div align="right"><b><a href="#nodejs">↥ Back to top</a></b></div> -->

##
