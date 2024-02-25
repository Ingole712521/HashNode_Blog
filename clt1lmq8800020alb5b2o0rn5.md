---
title: "Hooks React"
datePublished: Sun Feb 25 2024 14:22:12 GMT+0000 (Coordinated Universal Time)
cuid: clt1lmq8800020alb5b2o0rn5
slug: hooks-react
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1708870837097/79f45d73-a6e3-4e99-99f4-cd82fc0c3d9e.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1708870890762/2a902531-946a-40fe-b6ec-a14f502a7522.jpeg
tags: web-development, reactjs, coding, hooks, coding-challenge, coding-journey, learn-in-public

---

In today's installment of our Learning React Series, we're diving deep into one of the fundamental concepts of React: Hooks. Specifically, we'll be exploring the `useState` hook, `setCounter`, and the `counter` state variable in detail with examples to give you a solid understanding.

## Understanding Hooks in React

### What are Hooks?

Hooks are functions that let you use state and other React features without writing a class. They allow you to reuse stateful logic without changing your component hierarchy.

## UseState Hook

The `useState` hook is a function that allows functional components in React to have state. It returns a stateful value and a function to update that value, much like `this.setState` in a class component.

```jsx
import React, { useState } from 'react';

function Counter() {
  const [counter, setCounter] = useState(0);

  return (
    <div>
      <p>Count: {counter}</p>
      <button onClick={() => setCounter(counter + 1)}>Increment</button>
      <button onClick={() => setCounter(counter - 1)}>Decrement</button>
    </div>
  );
}

export default Counter;
```

In the above example, `useState(0)` initializes the state variable `counter` with a default value of `0`. The `setCounter` function allows us to update the `counter` state.

## SetCounter and UseState

`setCounter` is a function returned by `useState` that allows you to update the state value. When invoked, it re-renders the component with the updated state.

`counter` is the state variable itself. It holds the current value of the state.

### Example Usage

```jsx
import React from 'react';
import Counter from './Counter';

function App() {
  return (
    <div>
      <h1>Welcome to the Learning React Series: Day 8</h1>
      <Counter />
    </div>
  );
}

export default App;
```

In the above example, we've created an `App` component that renders the `Counter` component. This `Counter` component utilizes the `useState` hook to manage its state.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708870604066/a61d3af3-f770-4430-b71b-9a73a3fdf9b8.png align="center")

### Conclusion

Understanding hooks like `useState` is crucial for building powerful and dynamic React applications. By leveraging hooks, you can simplify your code, improve its readability, and enhance the overall developer experience.

Stay tuned for more insights and practical examples as we continue our journey of learning React!

Happy coding! 🚀✨