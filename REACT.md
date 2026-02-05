React may delay updates and group them together for performance. So if you do:

`setCount(count + 1); setCount(count + 1);`

Both lines see the **same old `count`**, and you only get +1.

But if you do:

`setCount(prev => prev + 1); setCount(prev => prev + 1);`

Each update uses the **latest value**, so you get +2.

React gives you the function form to guarantee **correctness** when the next state depends on the previous one.


Think of state updates as:

> “I’m describing **how** to compute the next state, not setting it directly.”

That’s the mental model React wants.