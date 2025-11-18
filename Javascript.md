
## 🔑 What is a Promise?

A **Promise** is an object representing a value that will be available in the future.  
It has two outcomes:

- ✅ `resolve(value)` → success
    
- ❌ `reject(error)` → failure
    

👉 Think of it like an **order ticket at a restaurant**:

- You place the order → you get a _promise_.
    
- When food is ready → promise is _resolved_.
    
- If something goes wrong → promise is _rejected_.
    

---

## ⏳ Why Promises (vs try...catch)?

- `try...catch` only handles **synchronous** errors.
    
- Promises handle **asynchronous** results (like API calls, DB queries, timers).
    
- With `async/await`, you can combine Promises + `try...catch` nicely.
    

Example:

```js
async function fetchUser() {
  try {
    const res = await fetch("/api/user");
    const data = await res.json();
    return data;
  } catch (err) {
    console.error("Error:", err);
  }
}
```

---

## 🖥️ Next.js & Promises as Props

In **Next.js (React Server Components)**:

- You can **pass a Promise as a prop**.
    
- React knows how to wait for the Promise (using **Suspense**) without blocking the whole page.
    

Example:

```jsx
async function getData() {
  return fetch("https://api.example.com/posts").then(r => r.json());
}

export default function Page() {
  const dataPromise = getData();  // 🍔 order ticket
  return <Posts data={dataPromise} />;  // give ticket to React
}
```

👉 Benefits:

- Parallel data fetching
    
- Streaming: render parts of UI while waiting for others
    

---

## 🌍 Real-Life Uses of Promises

1. **Fetching APIs**
    
    ```js
    fetch("/api/user")
      .then(res => res.json())
      .then(data => console.log(data));
    ```
    
2. **Database queries**
    
    ```js
    db.query("SELECT * FROM users").then(rows => console.log(rows));
    ```
    
3. **File system (Node.js)**
    
    ```js
    const fs = require("fs/promises");
    fs.readFile("data.txt", "utf8").then(console.log);
    ```
    
4. **Delays**
    
    ```js
    const delay = (ms) => new Promise(r => setTimeout(r, ms));
    delay(2000).then(() => console.log("2s later"));
    ```
    
5. **Multiple tasks in parallel**
    
    ```js
    Promise.all([fetch("/api/user"), fetch("/api/posts")]);
    ```
    

---

## 🧠 Key Takeaways

- Promises = _“I’ll give you the result later”_
    
- `try...catch` ≠ async → use Promises or `async/await`
    
- In Next.js, Promises as props → faster rendering + streaming
    
- Used everywhere async is needed (APIs, DB, files, timers)
    

##  Hoisting in JS

Execution context, has 2 parts, memory and code execution, vars, and functions code are stored in this context first before executing. and so if we do console log before we define the var, we get undefined, as memory is already allocated, and set to undefined. 

if this happens inside functions, the code execution searches lower/ parent stacks sequentially until it finds the var, if not found till the global, then return not defined.

let, const also do hoisting but after declaring with them, the elements are **NOT stored in global execution context memory window** and so they cannot be access when console log is executed before even declaring them. 
-##----------------------------------------------------------------------------------##


let and const are hoisted. we cant use them before initialization is result of "temporal dead zone". 
JS use diff memory than global execution context to store let and cost. which is reason behind "temporal dead zone" 

level of strictness ... var<<let<<const.

var  has no temporal dead zone, can redeclare and re-initialize, stored in GES 
**let use TDZ,** can't re-declare, can re-initialize, stored in separate memory
**const use TDZ**, can't re-declare, can't re-initialize, stored in separate memory 

syntax error is similar to compile error. while type and reference error falls under run time error. 
syntax error ... violation of JS syntax 

type error ... while trying to re-initialize const variable reference error ... while trying to access variable which is not there in global memory.