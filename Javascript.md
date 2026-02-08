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

## Closure
A function which is bundled together with its lexical environment
When a function is returned, **its original lexical environment is preserved**, even after the outer function has finished executing.
## 📌 Example (Classic Closure)

`function outer() 
{   let x = 10;    
	function inner() {     
	console.log(x);  
} 
return inner; 
}  
const fn = outer(); 

fn();`

**A closure is a function + its backpack.  
The backpack contains all the variables from the scope where it was born.  
The backpack travels with the function everywhere it goes.

✔️ A closure packs _everything in the scope chain where it was defined_. from there to global -> null

It never “forgets” the environment from its birth.



##  Call stack,  callback queues, micro task queue, Event Loop
**Call Stack**

- Holds currently executing functions (LIFO).
    
- Only one function runs at a time.
    

**Task Queue (Macrotask Queue)**

- Stores callbacks from asynchronous sources like `setTimeout`, DOM events, HTTP responses.
    
- Lower priority than microtasks.
    

**Microtask Queue**

- Stores microtasks: **Promise callbacks**, queueMicrotask, MutationObserver, fetch().
    
- Runs **before** the task queue, after each execution frame.
    

**Event Loop**

- Checks if the call stack is empty.
    
- If empty → runs **all microtasks first**.
    
- If microtasks are done → takes one macrotask from task queue and executes it.
- Also, there is a risk of starvation in callback queue if a task in microtask queue, produces another microtask and event loop goes on pumping the call stack with this task, completely leaving callback queue, as its priority is less and microtask queue continues to fill.
    
- Repeats forever.
    

**Flow**

1. JS runs synchronous code.
    
2. Async operations schedule callbacks into **task queue** or **microtask queue**.
    
3. When stack is empty → event loop drains microtasks.
    
4. If microtask queue empty → runs one macrotask.
    
5. Cycle repeats


## 📘 PROMISES & .then() / .catch() — FINAL NOTES

---

### 1️⃣ What a Promise is

- A Promise represents one future result
    
- It has only two outcomes:
    

- ✅ resolved(value)
    
- ❌ rejected(error)
    

You cannot change how an API promise resolves/rejects.

---

### 2️⃣ What flows in a promise chain

❌ Promises do NOT flow forward  
✅ Resolved values or errors flow forward

.then() and .catch() receive values, not promises

---

### 3️⃣ Core invariant (MOST IMPORTANT)

Every .then() and .catch() returns a NEW promise

The state of that new promise depends ONLY on what you do inside.

---

### 4️⃣ The ONE rule to rule them all 🔒

### In both .then() and .catch():

- return → next .then()
    
- throw / Promise.reject() → next .catch()
    

No exceptions.

---

### 5️⃣ What return actually means

Copy codereturn value;

Internally becomes:

Copy codePromise.resolve(value)

✔️ Even if value is:

- number
    
- object
    
- Error object
    
- null
    

➡️ Chain is resolved

---

### 6️⃣ Returning an Error is NOT an error

Copy codereturnnewError("oops");

- This is just returning an object
    
- Promise treats it as success
    
- Next .then() WILL run
    

📌 Returning an error = fallback value

---

### 7️⃣ What actually causes rejection

Only these:

Copy codethrow error;

or

Copy codereturnPromise.reject(error);

➡️ Chain becomes rejected  
➡️ Control moves to next .catch()

---

### 8️⃣ When does .catch() run?

.catch() runs if:

- a promise was rejected
    
- a .then() threw
    
- a .then() returned a rejected promise
    

.catch() does NOT end the chain automatically.

---

### 9️⃣ Recovery behavior of .catch()

Copy code.catch(err => {  
    return fallbackValue;  
})

- Converts rejection → resolution
    
- Next .then() WILL run
    
- fallbackValue becomes the input
    

---

### 🔁 Truth table (memorize)

|Where|Action|Next handler|
|---|---|---|
|.then()|return value|.then()|
|.then()|return promise (resolved)|.then()|
|.then()|throw|.catch()|
|.then()|return rejected promise|.catch()|
|.catch()|return value|.then()|
|.catch()|return promise (resolved)|.then()|
|.catch()|throw|.catch()|
|.catch()|return rejected promise|.catch()|

---

### 🔟 Why .then() after .catch() runs

Because .catch() returned a value →  
which internally is Promise.resolve(value)

Both success path and error-recovery path end up resolved.

---

### 1️⃣1️⃣ How to STOP the chain

Returning values ❌ does NOT stop the chain

To stop:

Copy codethrow error;

or

Copy codereturnPromise.reject(error);

---

### 1️⃣2️⃣ One-line mental model (FINAL)

Promises don’t care WHERE you are — only whether you return or throw.

---
#  Async Await 

Async is a keyword for registering async functions, it always returns a promise.

await can only be used inside an async function. Use await in front of the promise in the async function to handle promises there and it **resolves promise

JS engine do not wait for promise to be resolved, just go to next line. 

await is like .then to the promise it carries and the js waits for that to be resolved until it executes the next line. 

The WAIT IS TRICKY:
	###
	A Promise starts running as soon as it’s created, not when you await it. For example, if p1 is declared at the start of the program with a 10-second timer, the countdown begins immediately. By the time execution reaches await p1, the promise has already been working in the background. The await doesn’t start the timer — it simply pauses execution until the promise resolves. Meanwhile, p2 also started its own timer when it was declared. If p2 has a 5-second timer, then 5 seconds later it’s already resolved — even if the code hasn’t reached await p2 yet. So, when execution finally reaches await p2, there’s no extra waiting. The promise is already settled, so JavaScript just grabs its value instantly and assigns it to val2.

	 

Promise.all - 
.race - 
.allsettled - 
.any -  waits for first resolved settled promise.



