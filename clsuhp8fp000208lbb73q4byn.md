---
title: "Day 4 of React Mastery"
seoTitle: "Day 4 of React Mastery"
datePublished: Tue Feb 20 2024 14:57:47 GMT+0000 (Coordinated Universal Time)
cuid: clsuhp8fp000208lbb73q4byn
slug: day-4-of-react-mastery
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1708440645033/16d8ee4e-a1ed-4b98-952a-c582d26bb662.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1708440949174/f57156fd-f55f-4d1f-ab7e-80fd8ebf38ea.png
tags: javascript, router, reactjs, typescript, state-management, 2articles1week, reacthooks, react-usestate-state-management-hooks-components-javascript-front-end-development-web-development-code-examples-step-by-step-guide-user-interfaces-programming-tutorial-web-development-tutorial-javascript-development-react-development-reactjs-state-hook-state-management-in-react-frontend-development, mastery, functional-components, react-component-state

---

## Introduction

Welcome to the world of React! In this comprehensive blog post, we'll delve into essential concepts like routers, state management, and component styling to help you become a proficient React developer. We'll cover popular router libraries like Reach Router and React Router, explore state management techniques Additionally, we'll discuss the differences between class components and functional components, providing code examples and explanations along the way. Let's get started!

![A Comprehensive Guide to React Router: Types and Implementation Methods —  PART 1 | by Dev Balaji | Medium](https://miro.medium.com/v2/resize:fit:1400/1*ETRkggvBtYQVWm_NAelkwg.png align="left")

## Routers in React

Routers are essential tools in React for building single-page applications (SPAs) where different components are rendered based on the URL or route. They facilitate navigation between different views or pages within the application without requiring a full page reload. Two popular router libraries in the React ecosystem are Reach Router and React Router.

### Reach Router

Reach Router is a simple, accessible router library for React. It provides a declarative way to define routes and handle navigation in your application. Reach Router emphasizes accessibility and focuses on providing a straightforward API for defining and managing routes.

To use Reach Router, you first need to install it in your project:

```bash
npm install @reach/router
```

Once installed, you can define routes and navigate between them using Reach Router's components and hooks.

### Example of Reach Router

```jsx
import React from 'react';
import { Router, Link } from '@reach/router';

const Home = () => <div>Home</div>;
const About = () => <div>About</div>;

const App = () => (
  <Router>
    <Home path="/" />
    <About path="/about" />
  </Router>
);

export default App;
```

In this example, we import the `Router` and `Link` components from Reach Router. We define two components, `Home` and `About`, each rendering a simple `<div>` element with the respective content. We then use the `Router` component to define routes for these components. The `path` prop specifies the URL path at which each component should be rendered.

We can navigate between these routes using the `Link` component, which creates accessible links for navigating to different routes within the application.

---

### React Router

React Router is another popular routing library for React applications. It provides a more feature-rich and flexible routing solution compared to Reach Router. React Router supports advanced features like nested routes, route parameters, and programmatic navigation.

To use React Router, you need to install it in your project:

```bash
npm install react-router-dom
```

Once installed, you can define routes and navigate between them using React Router's components and hooks.

### Example of React Router

```jsx
import React from 'react';
import { BrowserRouter as Router, Route, Link } from 'react-router-dom';

const Home = () => <div>Home</div>;
const About = () => <div>About</div>;

const App = () => (
  <Router>
    <Link to="/">Home</Link>
    <Link to="/about">About</Link>
    <Route exact path="/" component={Home} />
    <Route path="/about" component={About} />
  </Router>
);

export default App;
```

In this example, we import the `BrowserRouter`, `Route`, and `Link` components from React Router. We define two components, `Home` and `About`, similar to the Reach Router example. We then use the `Router` component to wrap our application and define routes for the `Home` and `About` components using the `Route` component. The `exact` prop ensures that the `Home` component is only rendered when the URL path exactly matches "/".

We can navigate between these routes using the `Link` component, which generates HTML anchor tags (`<a>`) with the specified URLs.

---

## State management

State management in React refers to the process of managing and updating the state of your application. The state represents the data that determines the behavior and appearance of your components. In React, there are various approaches to manage state, each suited for different use cases and application requirements.

### React Component State

React components have their own local state, which can be managed using the `useState` hook for functional components or by extending the `Component` class and using `this.state` for class components. This approach is suitable for managing simple, component-specific state that doesn't need to be shared with other components.

### Example

```jsx
import React, { useState } from 'react';

const Counter = () => {
  const [count, setCount] = useState(0);

  const increment = () => {
    setCount(count + 1);
  };

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
};

export default Counter;
```

### React Context API

The React Context API provides a way to share data between components without having to pass props through every level of the component tree. It's useful for providing global state that multiple components need access to. You can create a context using `React.createContext()` and then use `Context.Provider` and `Context.Consumer` to provide and consume the context values.

### Example of React Context API

```jsx
import React, { createContext, useContext, useState } from 'react';

const CounterContext = createContext();
const CounterProvider = ({ children }) => {
  const [count, setCount] = useState(0);

  const increment = () => {
    setCount(count + 1);
  };

  return (
    <CounterContext.Provider value={{ count, increment }}>
      {children}
    </CounterContext.Provider>
  );
};

const useCounter = () => useContext(CounterContext);

export { CounterProvider, useCounter };
```

### Usage

```jsx
import React from 'react';
import { CounterProvider, useCounter } from './CounterContext';

const Counter = () => {
  const { count, increment } = useCounter();

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
};

const App = () => (
  <CounterProvider>
    <Counter />
  </CounterProvider>
);

export default App;
```

### Redux

Redux is a predictable state container for JavaScript apps, often used with React for managing complex application state. It provides a centralized store that holds the entire state of the application, and state mutations are made by dispatching actions to reducers.

### Example of Redux

```jsx
// TODO: Add Redux
```

### MobX

MobX is another state management library that makes state management simple and scalable by transparently applying functional reactive programming (TFRP) principles. It allows you to define observable state, which automatically tracks and updates the components that depend on it.

### Example of MobX

```jsx
// TODO
```

---

## Functional Components

Functional components are a simpler and more concise way to define React components. They are JavaScript functions that return React elements. Functional components have become more popular with the introduction of React hooks, which allow them to have state and lifecycle methods. Functional components are easier to read, write, and test compared to class components.

### Example

```jsx
import React, { useState } from 'react';

const Counter = () => {
  const [count, setCount] = useState(0);
  const incrementCount = () => {
    setCount(prevCount => prevCount + 1);
  };

  return (
    <div>
      <h1>Counter</h1>
      <p>Count: {count}</p>
      <button onClick={incrementCount}>Increment</button>
    </div>
  );
};

export default Counter;
```

### Explanation

In this example, we define a functional component called `Counter`. Let's break down the key parts of the code:

1. `import React, { useState } from 'react';`: We import the `React` library and the `useState` hook from the `react` package. The `useState` hook allows us to add state to functional components.
    
2. `const Counter = () => { ... };`: We define the `Counter` component using an arrow function syntax. This is a functional component.
    
3. `const [count, setCount] = useState(0);`: We use the `useState` hook to declare a state variable called `count` with an initial value of `0`. The `useState` hook returns an array with two elements: the current state value (`count`) and a function (`setCount`) to update the state value.
    
4. `const incrementCount = () => { ... };`: We define a function called `incrementCount` that updates the `count` state by incrementing its value by 1. We use the functional form of `setCount` to update the state based on the previous state value.
    
5. `<div>...</div>`: Inside the JSX code, we return a `<div>` element containing the counter UI. It displays the current count value (`{count}`) and a button that calls the `incrementCount` function when clicked.
    
6. `export default Counter;`: Finally, we export the `Counter` component as the default export, making it available for use in other parts of our application.
    

Overall, this example demonstrates how to create a simple counter component using a functional component in React. The component uses the `useState` hook to manage state and updates the UI dynamically based on the state changes.

---

## Class Components

Class components are the traditional way of defining React components using ES6 classes. They extend from the `React.Component` class and have a `render()` method that returns React elements. Class components are still widely used, especially in legacy codebases, but functional components with hooks have become the preferred choice for new development.

### Example of a Class Component

```jsx
import React, { Component } from 'react';

class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }

  incrementCount = () => {
    this.setState(prevState => ({
      count: prevState.count + 1
    }));
  };

  render() {
    return (
      <div>
        <h1>Counter: {this.state.count}</h1>
        <button onClick={this.incrementCount}>Increment</button>
      </div>
    );
  }
}

export default Counter;
```

### Explanation

1. Import React and Component: We start by importing the `React` and `Component` objects from the `react` module. The `Component` object is used to create class components in React.
    
2. Define the Counter class: We define a class called `Counter` that extends the `Component` class provided by React.
    
3. Constructor method: Inside the class, we define a constructor method to initialize the component's state. In this example, we set the initial state of the `count` property to `0`.
    
4. IncrementCount method: We define a custom method called `incrementCount` that updates the `count` state by incrementing it by 1 whenever the button is clicked. We use the `setState` method to update the state, passing in a function that receives the previous state as an argument and returns the updated state.
    
5. Render method: The `render` method is a required method in class components that returns the JSX to be rendered to the DOM. In this example, we render a heading element (`<h1>`) displaying the current count value and a button element (`<button>`) with an `onClick` event handler that calls the `incrementCount` method when clicked.
    
6. Export the Counter component: Finally, we export the `Counter` component so that it can be imported and used in other parts of the application.
    

This class component represents a simple counter that allows users to increment the count value by clicking a button. It demonstrates the basic structure of a class component in React, including state management and event handling.

---

## Comparison

* Functional components are simpler and more lightweight compared to class components.
    
* Functional components can use React hooks, allowing them to have state and lifecycle methods.
    
* Class components have access to lifecycle methods like `componentDidMount`, `componentDidUpdate`, etc., while functional components can use the `useEffect` hook for similar functionality.
    
* Functional components with hooks are the recommended approach for new development in React, but class components may still be necessary in certain cases, such as when working with legacy code or integrating with third-party libraries that rely on class components.
    

Overall, the choice between functional and class components depends on your project requirements and personal preference. However, functional components with hooks are becoming increasingly popular due to their simplicity, readability, and ability to handle complex state and side effects.

---

## Conclusion

we've explored a wide array of fundamental concepts in React, ranging from routers and state management to component styling and the differences between functional and class components.

* Routers, exemplified by Reach Router and React Router, offer powerful tools for navigating between different views in a React application, enhancing user experience and facilitating seamless navigation.
    
* State management is essential for managing data within a React application, with options like local component state, React Context API, Redux, and MobX offering varying degrees of complexity and flexibility to suit different project needs.
    
* Component styling is made more intuitive with libraries like styled-components, allowing for the creation of dynamic and reusable styled components directly within React applications.
    
* We've also compared and contrasted functional components with hooks and class components, showcasing the simplicity and versatility of functional components with hooks, while also acknowledging the continued relevance of class components in certain scenarios.
    

By mastering these foundational concepts, you're equipped with the knowledge and skills to build robust and scalable React applications. Whether you're embarking on a new project or refining your existing ones, understanding routers, state management, component styling, and component types is crucial for developing modern and efficient web applications with React. Keep experimenting, exploring, and pushing the boundaries of what you can achieve with React!

Thank you for joining me on this journey I hope you found this blog insightful and empowering as you continue to dive deeper into the world of React development. Remember, learning is a continuous process, and I'm here to support you every step of the way

Connection :- [Twitter](https://twitter.com/IngoleNehal) or [LinkedIn](https://www.linkedin.com/in/nehal-ingole/)