<!-- Start React -->

## React Interview question and answers

<div align="right"><b><a href="../../README.md">↥ Back to home</a></b></div>

### Q 1. What is React?

React is an open-source JavaScript library used for building user interfaces, especially for single-page applications (SPAs). It follows a component-based architecture, allowing developers to build reusable and independent UI pieces.

**Advantages:** Component-based architecture, high performance with Virtual DOM, reusable components, strong community support.

**Disadvantages:** Handles only the UI layer, requires additional libraries, and can become complex in large applications.

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 2. What is JSX?

JSX stands for JavaScript XML. It is a syntax extension used in React that allows us to write HTML-like code inside JavaScript, making UI code more readable and easier to write.

**Example:**

```javascript
const element = <h1>Hello, World!</h1>;
```

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 3. What is Fragment?

A Fragment in React allows you to group multiple elements without adding extra nodes to the DOM.

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 4. What are keys?

Keys are unique identifiers used by React to track elements in a list when rendering dynamically. They help React efficiently update the DOM by identifying which items changed, were added, or removed.

**Important Notes:**

- Keys must be unique among siblings, not globally.
- Using index as key is not recommended if items can reorder.
- Keys are used internally by React, they are not passed as props.

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 5. What is lifting state up?

Lifting state up means moving the state from a child component to the nearest common parent so that multiple child components can share and modify the same state.

```javaScript
function Parent() {
  const [count, setCount] = React.useState(0); // state lifted up

  return (
    <>
      <ChildA count={count} setCount={setCount} />
      <ChildB count={count} setCount={setCount} />
    </>
  );
}

function ChildA({ count, setCount }) {
  return <button onClick={() => setCount(count + 1)}>Increment</button>;
}

function ChildB({ count }) {
  return <p>Current Count: {count}</p>;
}
```

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 6. What is a component?

A component is a reusable piece of code that returns UI elements and can manage its own state(data) and behavior.

There are two types of components: **Functional Components** and **Class Components**.

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 7. What is Functional components?

A functional component is a JavaScript function that returns JSX and can use React Hooks to manage state and lifecycle features.

**Example with State using Hooks:**

```javascript
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </>
  );
}
```

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 8. What is Class components?

A class component is a React component defined using an ES6 class that extends `React.Component` and uses lifecycle methods and `this.state` to manage data.

**_Why Class Components Are Less Used Today_**

After React Hooks were introduced, functional components became more powerful and easier to use.
So now, functional components are preferred in modern React development.

- **Key Features:**
  - Uses `this.state` to manage data
  - Uses `this.setState()` to update state
  - Supports lifecycle methods like:
    - `componentDidMount()`
    - `componentDidUpdate()`
    - `componentWillUnmount()`

**Example with State:**

```javascript
import React, { Component } from "react";

class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  render() {
    return (
      <>
        <p>Count: {this.state.count}</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Increment
        </button>
      </>
    );
  }
}
```

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 9. What is Controlled Components?

A controlled component is a form element (input, textarea, select) whose value is controlled by React state.

```javaScript
import { useState } from "react";

function ControlledInput() {
  const [name, setName] = useState("");

  const handleChange = (e) => setName(e.target.value);

  return (
    <div>
      <input type="text" value={name} onChange={handleChange} />
      <p>Your name: {name}</p>
    </div>
  );
}
```

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 10. What is Uncontrolled Components?

An uncontrolled component is a form element that manages its own internal state, and React uses refs to access its value.
An uncontrolled component is a form element whose value is managed by the DOM, not by React state. React accesses its value by using refs.

```javaScript
import { useRef } from "react";

function UncontrolledInput() {
  const inputRef = useRef();

  const handleSubmit = () => {
    alert("Your name: " + inputRef.current.value);
  };

  return (
    <div>
      <input type="text" ref={inputRef} />
      <button onClick={handleSubmit}>Submit</button>
    </div>
  );
}
```

**Example:**

```javascript
<>
  <h1 />
  <p />
</>
```

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 11. What is State?

State is a React object that stores dynamic data in a component. When the state changes, the component re-renders to reflect the updated data.

**Key Points About State**

- Each component can have its own state.
- Updating state re-renders the component automatically.
- In functional components, we use useState hook to manage state.
- In class components, state is managed using this.state and updated with this.setState().

**Example:**

```javascript
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </>
  );
}
```

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 12. What is Props?

Props(short for properties) are read-only inputs passed from a parent component to a child component, allowing data to flow and making components reusable.

**Key Points About Props**

- Read-only → Child cannot modify them.
- Used to pass data or functions from parent to child.
- Helps create reusable components.
- Works in both functional and class components.

**Example:**

```javascript
function Welcome(props) {
  return <h1>Hello, {props.name}!</h1>;
}

// Usage
<Welcome name="John" />;
```

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 713. What is Prop Drilling?

Prop drilling happens when props are passed through multiple component levels just to reach a deeply nested child.

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 814. Differences Between State and Props?

| Feature                 | **State**                                          | **Props**                                        |
| ----------------------- | -------------------------------------------------- | ------------------------------------------------ |
| **Definition**          | An object that stores dynamic data of a component. | Read-only inputs passed from parent to child.    |
| **Mutability**          | **Mutable** – can be updated within the component. | **Immutable** – cannot be changed by the child.  |
| **Purpose**             | Stores data that can change over time.             | Passes data or functions to child components.    |
| **Component Control**   | Controlled by the component itself.                | Controlled by the parent component.              |
| **Usage**               | Managed via `this.state`/`useState()`.             | Accessed via `props`.                            |
| **Effect on Rendering** | Changing state triggers a re-render.               | Changing props also triggers re-render of child. |
| **Scope**               | Local to the component.                            | Can be passed from parent to multiple children.  |

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 15. What is hooks and how many types are there?

Hooks are special functions in React that let functional components use state, lifecycle methods, and other features.

**Types of Hooks:** `useState`, `useEffect`, `useReducer`, `useLayoutEffect`,`useMemo`, `useCallback`,`useRef`, `useImperativeHandle`,`useContext`, `useId` and custom hooks.

**Quick Rule of Thumb**

- **State:** `useState`, `useReducer`.
- **Effects:** `useEffect`, `useLayoutEffect`.
- **Performance Optimization:** `useMemo`, `useCallback`.
- **Refs & DOM Access:** `useRef`, `useImperativeHandle`.
- **Global Data:** `useContext`, `useId`.

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 16. What are the Rules of Hooks?

- Only call hooks at the top level.
- Only call hooks inside React functions.
- Never call hooks conditionally.

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 17. Can we call hooks inside loops or conditions?

No. That breaks hook order consistency.

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 18. Why does `useEffect` run twice in development?

Because React Strict Mode intentionally runs effects twice in development to detect side-effect bugs.
It does not happen in production.

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 19. Why does an object in dependency array cause re-renders?

Because objects are compared by reference, not value.
New object = new reference = effect runs again.

Fix using `useMemo`.

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 20. Why is hook order important internally?

React keeps hooks in an internal array. Changing order breaks state mapping.

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 21. Does updating state immediately change the value?

No. State updates are asynchronous and batched.

```javaScript
setCount(count + 1);
console.log(count); // old value
```

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 22. What are common mistakes in `useEffect`?

- Missing dependency array
- Wrong dependencies
- Causing infinite loops
- Updating state without condition

```javaScript
useEffect(() => {
  setCount(count + 1);
}); // This creates infinite render.
```

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 23. What is `useState`?

`useState` is a hook that allows functional components to have state and it returns the current state and a function to update it.

**When to use:** To store dynamic data in a functional component (form inputs, toggles, counters).

```javaScript
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);
  return (
    <>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </>
  );
}
```

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 24. What is `useEffect`?

`useEffect` allows functional components to perform side effects, like data fetching, subscriptions, or manually updating the DOM.

**When to use:** To store dynamic data in a functional component (form inputs, toggles, counters).

```javaScript
import { useEffect, useState } from "react";

function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => setSeconds(s => s + 1), 1000);
    return () => clearInterval(interval); // cleanup
  }, []);

  return <p>Seconds: {seconds}</p>;
}
```

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 25. What is `useContext`?

`useContext` allows a functional component to consume context values without prop drilling.

**When to use:** When multiple components need access to shared data (theme, user info, settings)..

```javaScript
import { createContext, useContext } from "react";

const ThemeContext = createContext("light");

function ThemedText() {
  const theme = useContext(ThemeContext);
  return <p>Current Theme: {theme}</p>;
}
```

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 26. What is `useReducer`?

`useReducer` manages complex state logic using a reducer function (like Redux but local to a component).

**When to use:** Managing complex state logic or multiple related state variables..

```javaScript
import { useReducer } from "react";

function reducer(state, action) {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };
    default:
      return state;
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: "increment" })}>Increment</button>
    </>
  );
}
```

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 27. What is `useRef`?

`useRef` Can be used to access DOM nodes or store values without re-rendering and returns a mutable object whose `.current` property persists across renders.

**When to use:** Accessing DOM elements, storing mutable values that don’t trigger re-render.

```javaScript
import { useRef } from "react";

function InputFocus() {
  const inputRef = useRef(null);

  return (
    <>
      <input ref={inputRef} type="text" />
      <button onClick={() => inputRef.current.focus()}>Focus Input</button>
    </>
  );
}
```

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 28. What is `useMemo`?

`useMemo` memoizes expensive calculations and returns a cached value to optimize performance.

**When to use:** To avoid recalculating expensive operations on every render..

```javaScript
import { useMemo, useState } from "react";

function ExpensiveCalculation({ number }) {
  const result = useMemo(() => {
    console.log("Calculating...");
    return number * 2; // expensive calculation
  }, [number]);

  return <p>Result: {result}</p>;
}
```

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 29. What is `useCallback`?

`useCallback` memoizes functions to prevent unnecessary re-creations, which can improve performance when passing functions to child components.

**When to use:** When passing functions as props to prevent unnecessary re-renders of child components..

```javaScript
import { useCallback, useState } from "react";

function Button({ onClick }) {
  return <button onClick={onClick}>Click Me</button>;
}

function App() {
  const [count, setCount] = useState(0);
  const increment = useCallback(() => setCount(c => c + 1), []);

  return (
    <>
      <p>Count: {count}</p>
      <Button onClick={increment} />
    </>
  );
}
```

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 30. What is `useLayoutEffect`?

`useLayoutEffect` is similar to useEffect but runs synchronously after DOM mutations and before the browser paints.

**When to use:** When you need to measure or modify the DOM before it is painted to the screen.

```javaScript
import { useLayoutEffect, useRef } from "react";

function Box() {
  const boxRef = useRef(null);

  useLayoutEffect(() => {
    console.log("Width:", boxRef.current.offsetWidth);
  });

  return <div ref={boxRef}>Hello</div>;
}
```

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 31. What is `useImperativeHandle`?

`useImperativeHandle` customizes the instance value exposed to parent components when using `ref`.

**When to use:** When the parent needs controlled access to a child component’s methods or DOM..

```javaScript
import { forwardRef, useImperativeHandle, useRef } from "react";

const Input = forwardRef((props, ref) => {
  const inputRef = useRef();
  useImperativeHandle(ref, () => ({
    focus: () => inputRef.current.focus()
  }));
  return <input ref={inputRef} />;
});

function App() {
  const inputRef = useRef();
  return <button onClick={() => inputRef.current.focus()}>Focus Input</button>;
}
```

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 32. What is `useId`?

`useId` generates a unique ID that is stable across server and client renders, preventing collisions.

**When to use:** When you need unique IDs for forms, accessibility, or SSR..

```javaScript
import { useId } from "react";

function TextInput() {
  const id = useId();
  return (
    <div>
      <label htmlFor={id}>Name:</label>
      <input id={id} type="text" />
    </div>
  );
}
```

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 33. What are custom hooks?

Custom hooks are reusable functions that use other hooks. They start with use.

```javaScript
function useFetch(url) {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch(url).then(res => res.json()).then(setData);
  }, [url]);

  return data;
}
```

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 34. What is the difference between `useState` vs `useReducer`?

`useState` is used for simple state management, while `useReducer` is preferred for complex state logic involving multiple related state variables or actions.

| Feature        | useState                    | useReducer                    |
| -------------- | --------------------------- | ----------------------------- |
| Complexity     | Simple state                | Complex state logic           |
| Best For       | Counters, inputs, toggles   | Multiple related state values |
| Logic Handling | Direct state update         | Uses reducer function         |
| Scalability    | Less scalable for big logic | Better for complex flows      |

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 35. What is the difference between `useEffect` vs `useLayoutEffect`?

`useEffect` runs after the screen updates, while `useLayoutEffect` runs synchronously before the browser paints. `useLayoutEffect` is used when we need to measure or modify the DOM before the user sees it.

| Feature        | useEffect                | useLayoutEffect                      |
| -------------- | ------------------------ | ------------------------------------ |
| Execution Time | After browser paint      | Before browser paint                 |
| Blocking       | Non-blocking             | Blocks painting                      |
| Use Case       | API calls, subscriptions | DOM measurements, layout adjustments |

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 36. What is the difference between `useMemo` vs `useCallback`?

`useMemo` memoizes a calculated value, whereas `useCallback` memoizes a function to prevent unnecessary re-renders.

| Feature  | useMemo                         | useCallback                           |
| -------- | ------------------------------- | ------------------------------------- |
| Returns  | Memoized value                  | Memoized function                     |
| Purpose  | Optimize expensive calculations | Prevent function recreation           |
| Use Case | Heavy computations              | Passing functions to child components |

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 37. What is the difference between `useRef` vs `useState`?

`useState` triggers a re-render when updated, but `useRef` does not. `useRef` is mainly used for DOM access or storing values that shouldn't cause re-renders.

| Feature           | useRef                             | useState                |
| ----------------- | ---------------------------------- | ----------------------- |
| Re-render Trigger | ❌ No                              | ✅ Yes                  |
| Purpose           | Store mutable values or access DOM | Store reactive UI state |
| Persistence       | Persists across renders            | Persists across renders |

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 38. Why dependency array in `useEffect`?

The dependency array in `useEffect` determines when the effect should run. If it is empty, the effect runs only once. If it contains values, the effect runs whenever those values change. Without it, the effect runs after every render, which may cause performance issues or infinite loops.

### 🎯 Different Dependency Cases

- **No Dependency Array**

  ✔ Runs after every render

  ```javaScript
  useEffect(() => {
    console.log("Runs on every render");
  });
  ```

- **Empty Dependency Array []**

  ✔ Runs only once (like componentDidMount)

  ✔ Used for:
  - Initial API calls
  - Setting up subscriptions

  ```javaScript
  useEffect(() => {
    console.log("Runs only once");
  }, []);
  ```

- **With Dependencies [value]**

  ✔ Runs:
  - On first render
  - Whenever count changes

  ```javaScript
  useEffect(() => {
    console.log("Runs when count changes");
  }, [count]);
  ```

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 39. What is React Fiber?

React Fiber is the internal reconciliation engine introduced in React 16. It breaks rendering work into small units called fibers, allowing React to pause, prioritize, and resume work. This enables concurrent rendering and improves performance by preventing UI blocking.

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 40. What is Virtual DOM?

The Virtual DOM is a lightweight copy of the real DOM. React updates the virtual DOM first, compares it with the previous version, and then updates only the changed parts in the real DOM for better performance.

**_How It Works_**

**1️⃣ Initial render:** React creates a Virtual DOM tree.

**2️⃣ State changes:** A new Virtual DOM is created.

**3️⃣ Diffing (Reconciliation):** React compares old and new Virtual DOM.

**4️⃣ Update real DOM:** Only changed nodes are updated.

This process is called **Reconciliation**.

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 41. What is Unidirectional Data Flow?

Unidirectional data flow in React is a design pattern where data flows in one direction only, from parent to child via props. Children cannot directly modify props; they can request changes by calling functions passed from the parent.

```javaScript
function Parent() {
  const [count, setCount] = React.useState(0);

  return (
    <div>
      <ChildDisplay count={count} />
      <ChildButton onIncrement={() => setCount(count + 1)} />
    </div>
  );
}

function ChildDisplay({ count }) {
  return <p>Count: {count}</p>;
}

function ChildButton({ onIncrement }) {
  return <button onClick={onIncrement}>Increment</button>;
}
```

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 42. What is Suspense?

Suspense is a React feature that lets you delay rendering a component until some asynchronous operation (like code or data loading) is complete. You provide a fallback UI, such as a spinner, that displays while waiting, improving the user experience..

```javaScript
import React, { Suspense } from "react";

const LazyComponent = React.lazy(() => import("./LazyComponent"));

function App() {
  return (
    <div>
      <h1>My App</h1>
      <Suspense fallback={<p>Loading...</p>}>
        <LazyComponent />
      </Suspense>
    </div>
  );
}

export default App;
```

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 43. What is Lazy Loading?

Lazy loading is a technique to load components only when they are needed, instead of loading everything upfront.

Lazy loading is a technique to load components only when they are needed. It reduces the initial bundle size, improves performance, and is usually implemented using `React.lazy` and `Suspense` with a fallback UI.

```javaScript
import React, { Suspense } from "react";

const HeavyComponent = React.lazy(() => import("./HeavyComponent"));

function App() {
  return (
    <Suspense fallback={<p>Loading...</p>}>
      <HeavyComponent />
    </Suspense>
  );
}
```

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 44. What are Error Boundaries?

An Error Boundary is a React component that catches errors in its child components, logs them, and displays a fallback UI instead of crashing the entire app. It helps make applications more resilient and improves user experience.

```javaScript
import React, { Component } from "react";

// Error Boundary
class ErrorBoundary extends Component {
  state = { hasError: false };

  static getDerivedStateFromError() {
    return { hasError: true };
  }

  render() {
    if (this.state.hasError) return <h2>Something went wrong!</h2>;
    return this.props.children;
  }
}

// Buggy Component
function Buggy() {
  throw new Error("Oops!");
  return <p>Hello</p>;
}

// Usage
function App() {
  return (
    <ErrorBoundary>
      <Buggy />
    </ErrorBoundary>
  );
}

export default App;
```

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 45. How to pass data between react components?

**1. Parent → Child (Using Props)**

Data flows from parent to child using props (unidirectional).

```javaScript
function Child({ message }) {
  return <p>Message: {message}</p>;
}

function Parent() {
  const msg = "Hello from Parent";
  return <Child message={msg} />;
}
```

- Props are read-only for the child
- Unidirectional flow ensures predictability

**2. Child → Parent (Using Callbacks)**

Pass a function from parent to child as a prop. Child calls it to send data upwards.

```javaScript
function Child({ onSend }) {
  return <button onClick={() => onSend("Data from Child")}>Send</button>;
}

function Parent() {
  const handleData = (data) => alert(data);
  return <Child onSend={handleData} />;
}
```

- This is how children communicate with parents in React

**3. Sibling → Sibling (Via Parent)**

Siblings cannot communicate directly. Use the common parent to share data.

```javaScript
function SiblingA({ sendData }) {
  return <button onClick={() => sendData("Hello Sibling B")}>Send</button>;
}

function SiblingB({ message }) {
  return <p>Message: {message}</p>;
}

function Parent() {
  const [msg, setMsg] = React.useState("");
  return (
    <>
      <SiblingA sendData={setMsg} />
      <SiblingB message={msg} />
    </>
  );
}
```

**4. Global State (Context API / Redux)**

For deeply nested or widely shared state, use Context API or Redux.

```javaScript
import { createContext, useContext, useState } from "react";

const DataContext = createContext();

function Provider({ children }) {
  const [data, setData] = useState("Global Data");
  return <DataContext.Provider value={{ data, setData }}>{children}</DataContext.Provider>;
}

function ComponentA() {
  const { setData } = useContext(DataContext);
  return <button onClick={() => setData("Updated!")}>Update</button>;
}

function ComponentB() {
  const { data } = useContext(DataContext);
  return <p>{data}</p>;
}
```

- Works across any component tree level
- Great for large apps

**5. Parent acts as the state holder**

Data can also be passed via URL parameters or query strings using react-router-dom.

```javaScript
// Route: /user/123
<Link to="/user/123">Go to User</Link>

function UserPage({ params }) {
  const { id } = useParams();
  return <p>User ID: {id}</p>;
}
```

```javaScript

```

```javaScript

```

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 46. How do you optimize performance?

- Use `React.memo` and `PureComponent` to avoid unnecessary re-renders
- Use `useCallback` and `useMemo` for functions and expensive calculations
- Implement lazy loading with React.lazy and Suspense
  - ```javaScript
      const LazyComponent = React.lazy(() => import("./LazyComponent"));
      <Suspense fallback={<p>Loading...</p>}><LazyComponent /></Suspense>
    ```
- Avoid anonymous functions/objects in JSX.
  - ```javaScript
      <Button onClick={() => handleClick()} />
    ```
- Use keys properly in lists and immutable state updates
  - ```javaScript
      {items.map(item => <li key={item.id}>{item.name}</li>)}
    ```
- Code splitting
  - ```javaScript
      import("./HeavyComponent").then(module => { ... });
    ```
- Virtualize long lists and profile with React DevTools

```javaScript
{items.map(item => <li key={item.id}>{item.name}</li>)}
```

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 47. How do you structure a React app?

```javaScript
my-app/
│
├── public/                 # Static files (index.html, favicon, images)
│
├── src/
│   ├── assets/             # Images, fonts, icons, styles
│   │
│   ├── components/         # Reusable UI components
│   │   ├── Button/
│   │   │   ├── Button.jsx
│   │   │   └── Button.css
│   │   └── ...
│   │
│   ├── features/           # Feature-wise modules
│   │   ├── dashboard/
│   │   │   ├── components/   # Feature-specific components
│   │   │   ├── pages/        # Dashboard pages
│   │   │   │   └── DashboardPage.jsx
│   │   │   ├── dashboardContext.jsx
│   │   │   └── index.jsx
│   │   │
│   │   └── profile/
│   │       ├── components/
│   │       ├── pages/
│   │       │   └── ProfilePage.jsx
│   │       └── index.jsx
│   │
│   ├── hooks/              # Custom hooks
│   │   └── useFetch.js
│   │
│   ├── context/            # Global contexts
│   │   └── AuthContext.js
│   │
│   ├── services/           # API calls, axios setup, utilities
│   │   └── api.js
│   │
│   ├── utils/              # Helper functions
│   │   └── formatDate.js
│   │
│   ├── routes/             # Centralized routing
│   │   └── AppRoutes.jsx
│   │
│   ├── App.jsx             # Main app component
│   └── index.js            # Entry point
│
└── package.json
```

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 48. How do you handle authentication?

I handle authentication by storing JWT in a secure place (localStorage or cookies), maintaining auth state in context, protecting routes with a wrapper component, and attaching tokens in API headers. I also handle unauthorized responses globally.

**1️⃣ Key Steps**

- Login API → Get JWT or token from backend
- Store token → LocalStorage, SessionStorage, or HttpOnly Cookie
- Provide auth state → Using React Context or Redux
- Protect routes → Redirect unauthenticated users
- Logout → Clear token and auth state

**2️⃣ Using Context for Auth**

```javaScript
// src/context/AuthContext.js
import React, { createContext, useState, useContext, useEffect } from "react";

const AuthContext = createContext();

export const AuthProvider = ({ children }) => {
  const [user, setUser] = useState(null);

  // On mount, check for token
  useEffect(() => {
    const token = localStorage.getItem("token");
    if (token) {
      setUser({ token }); // optionally fetch user info
    }
  }, []);

  const login = (token) => {
    localStorage.setItem("token", token);
    setUser({ token });
  };

  const logout = () => {
    localStorage.removeItem("token");
    setUser(null);
  };

  return (
    <AuthContext.Provider value={{ user, login, logout }}>
      {children}
    </AuthContext.Provider>
  );
};

export const useAuth = () => useContext(AuthContext);
```

**3️⃣ Protecting Routes**

```javaScript
// src/routes/ProtectedRoute.jsx
import { Navigate } from "react-router-dom";
import { useAuth } from "../context/AuthContext";

const ProtectedRoute = ({ children }) => {
  const { user } = useAuth();
  if (!user) {
    return <Navigate to="/login" />;
  }
  return children;
};

export default ProtectedRoute;
```

Usage

```javaScript
<Route
  path="/dashboard"
  element={
    <ProtectedRoute>
      <DashboardPage />
    </ProtectedRoute>
  }
/>
```

**4️⃣ Handling API Calls with Token**

```javaScript
// src/services/api.js
import axios from "axios";

const api = axios.create({
  baseURL: "https://api.example.com",
});

api.interceptors.request.use((config) => {
  const token = localStorage.getItem("token");
  if (token) config.headers.Authorization = `Bearer ${token}`;
  return config;
});

api.interceptors.response.use(
  (response) => response,
  (error) => {
    if (error.response.status === 401) {
      // Handle unauthorized globally
      localStorage.removeItem("token");
      window.location.href = "/login";
    }
    return Promise.reject(error);
  }
);

export default api;
```

**5️⃣ Notes / Best Practices**

- Use HttpOnly cookies for better security (prevents XSS)
- Use context or Redux for managing auth state globally
- Protect routes both in frontend and backend
- Refresh tokens for long sessions (optional)

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 49. What is Redux?

Redux is a state management library that stores all app state in a single store, updates it via actions and reducers, and provides predictable and debuggable state for large or complex applications.

**Redux Flow**

- **Action:** An object describing what happened
- **Reducer:** A pure function that updates state based on the action
- **Store:** Holds the state
- **View/Component:** Dispatches actions and reads state

**Simple Example: Counter**

```javaScript
// store.js
import { createStore } from "redux";

const initialState = { count: 0 };

function counterReducer(state = initialState, action) {
  switch(action.type) {
    case "INCREMENT": return { count: state.count + 1 };
    case "DECREMENT": return { count: state.count - 1 };
    default: return state;
  }
}

const store = createStore(counterReducer);
export default store;
```

```javaScript
// Counter.jsx
import React from "react";
import { useSelector, useDispatch } from "react-redux";

function Counter() {
  const count = useSelector(state => state.count);
  const dispatch = useDispatch();

  return (
    <div>
      <button onClick={() => dispatch({ type: "DECREMENT" })}>-</button>
      {count}
      <button onClick={() => dispatch({ type: "INCREMENT" })}>+</button>
    </div>
  );
}
export default Counter;
```

```javaScript
// App.jsx
import React from "react";
import { Provider } from "react-redux";
import store from "./store";
import Counter from "./Counter";

function App() {
  return (
    <Provider store={store}>
      <Counter />
    </Provider>
  );
}
export default App;
```

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 50. What is tanstack query?

TanStack Query is a library for managing server state in React apps. It handles fetching, caching, syncing, and updating data automatically, reducing boilerplate and improving performance.

**🔹 Key Features**

- **Data Fetching & Caching:** Automatically caches API responses
- **Automatic Refetching:** Refetch data when component mounts or network reconnects
- **Loading & Error States:** Built-in support for isLoading, isError
- **Pagination & Infinite Queries:** Built-in support for pages
- **Mutations:** Handle POST, PUT, DELETE requests easily
- **Query Invalidation:** Keep data fresh after updates

```javaScript
import { useQuery } from '@tanstack/react-query';
import axios from 'axios';

function fetchTodos() {
  return axios.get('https://jsonplaceholder.typicode.com/todos');
}

function TodoList() {
  const { data, isLoading, isError, error } = useQuery(['todos'], fetchTodos);

  if (isLoading) return <div>Loading...</div>;
  if (isError) return <div>Error: {error.message}</div>;

  return (
    <ul>
      {data.data.map(todo => (
        <li key={todo.id}>{todo.title}</li>
      ))}
    </ul>
  );
}
```

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 51. What is Form Hook?

React Hook Form simplifies form handling by using hooks, reduces unnecessary re-renders, and provides built-in validation. It’s preferred for large or dynamic forms over traditional controlled components.

```javaScript
import React, { useState } from "react";
import { useForm } from "react-hook-form";
import { z } from "zod";
import { zodResolver } from "@hookform/resolvers/zod";
import axios from "axios";

// 1️⃣ Define Zod validation schema
const signupSchema = z.object({
  username: z.string().min(3, "Username must be at least 3 characters"),
  email: z.string().email("Invalid email address"),
  password: z.string().min(6, "Password must be at least 6 characters"),
});

// 2️⃣ SignupForm Component
function SignupForm() {
  const [apiError, setApiError] = useState("");
  const [isSubmitting, setIsSubmitting] = useState(false);

  const {
    register,
    handleSubmit,
    formState: { errors },
    reset,
  } = useForm({
    resolver: zodResolver(signupSchema),
  });

  // 3️⃣ Form submission
  const onSubmit = async (data) => {
    setApiError("");
    setIsSubmitting(true);
    try {
      // Replace with your real API endpoint
      const response = await axios.post("https://example.com/api/signup", data);

      alert("Signup successful!");
      reset(); // Reset form
    } catch (error) {
      if (error.response && error.response.data?.message) {
        setApiError(error.response.data.message);
      } else {
        setApiError("Something went wrong. Please try again.");
      }
    } finally {
      setIsSubmitting(false);
    }
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)} style={{ maxWidth: "400px", margin: "auto" }}>
      <h2>Signup</h2>

      {/* Username */}
      <div>
        <label>Username:</label>
        <input type="text" {...register("username")} placeholder="Enter username" />
        {errors.username && <p style={{ color: "red" }}>{errors.username.message}</p>}
      </div>

      {/* Email */}
      <div>
        <label>Email:</label>
        <input type="email" {...register("email")} placeholder="Enter email" />
        {errors.email && <p style={{ color: "red" }}>{errors.email.message}</p>}
      </div>

      {/* Password */}
      <div>
        <label>Password:</label>
        <input type="password" {...register("password")} placeholder="Enter password" />
        {errors.password && <p style={{ color: "red" }}>{errors.password.message}</p>}
      </div>

      {/* API Error */}
      {apiError && <p style={{ color: "red" }}>{apiError}</p>}

      {/* Submit Button */}
      <button type="submit" disabled={isSubmitting}>
        {isSubmitting ? "Signing up..." : "Signup"}
      </button>
    </form>
  );
}

export default SignupForm;
```

**How it Works:**

- Zod validation:
  - `username` ≥ 3 characters
  - `email` must be valid
  - `password` ≥ 6 characters
- React Hook Form:
  - Handles input registration, validation, errors, and submission
  - Minimal re-renders
- API Submission & Error Handling:
  - `axios.post` sends data
  - Catch errors from server and display to user
- Form Reset:
- `reset()` clears the form after successful submission

<div align="right"><b><a href="#react-interview-question-and-answers">↥ Back to top</a></b></div>

### Q 50. Question?

```javaScript

```

<div align="right"><b><a href="#table-of-contents">↥ Back to top</a></b></div>

##
