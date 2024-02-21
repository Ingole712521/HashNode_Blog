---
title: "Day 5 pf Mastering React Context API"
seoTitle: "Day 5 pf Mastering React Context API"
datePublished: Wed Feb 21 2024 05:26:55 GMT+0000 (Coordinated Universal Time)
cuid: clsvcqyax000409l6hda30g29
slug: day-5-pf-mastering-react-context-api
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1708492263885/578c62dc-f1c7-49c8-80e2-abbd73d5e815.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1708493154327/5dc68c25-9cc8-4b2c-abe8-80692541db7b.png
tags: javascript, react-native, reactjs, context-api, reacthooks, learn-in-public

---

## Introduction

In the realm of React development, managing state across components efficiently is crucial for building scalable and maintainable applications. While props drilling and state lifting have been traditional solutions, React Context API offers a more elegant and streamlined approach to sharing state across components without the need for prop drilling.

In this comprehensive guide, we'll delve into the nuances of React Context API, exploring its core concepts, implementation details, and best practices. Additionally, we'll take it a step further by integrating local storage with Context API to persist state across page reloads, enhancing the user experience and application robustness.

![Overview of React.js](https://www.patterns.dev/img/reactjs/react-logo@3x.svg align="left")

## Understanding React Context API

React Context API provides a way to pass data through the component tree without having to pass props down manually at every level. It consists of three main components:

1. **Provider:** It allows consuming components to subscribe to context changes.
    
2. **Consumer:** It enables consuming components to subscribe to context changes.
    
3. **Context:** It's the object created with React.createContext(). It represents the data that will be shared across the component tree.
    

Let's start by creating a simple example to demonstrate how Context API works:

```jsx
import React from 'react';
const ThemeContext = React.createContext('light');
export default ThemeContext;
```

```jsx
// App.js
import React from 'react';
import ThemeContext from './ThemeContext';
import Toolbar from './Toolbar';
function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Toolbar />
    </ThemeContext.Provider>
  );
}

export default App;
```

```jsx
// Toolbar.js
import React from 'react';
import ThemeContext from './ThemeContext';
function Toolbar() {
  return (
    <ThemeContext.Consumer>
      {theme => <div>The current theme is: {theme}</div>}
    </ThemeContext.Consumer>
  );
}

export default Toolbar;
```

In this example, `App` component wraps `Toolbar` component with `ThemeContext.Provider`, and `Toolbar` component consumes the value provided by `ThemeContext.Provider` using `ThemeContext.Consumer`.

## Integrating Local Storage with React Context API

Integrating local storage with React Context API allows us to persist state even when the user refreshes the page or navigates away. This is particularly useful for preserving user preferences or application settings.

Let's extend our previous example to include local storage integration:

```jsx
import React, { useState, useEffect } from 'react';
const ThemeContext = React.createContext();
export const ThemeProvider = ({ children }) => {
  const [theme, setTheme] = useState('light');

  useEffect(() => {
    const savedTheme = localStorage.getItem('theme');
    if (savedTheme) {
      setTheme(savedTheme);
    }
  }, []);

  const toggleTheme = () => {
    const newTheme = theme === 'light' ? 'dark' : 'light';
    setTheme(newTheme);
    localStorage.setItem('theme', newTheme);
  };

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
};

export default ThemeContext;
```

```jsx
// App.js
import React from 'react';
import { ThemeProvider } from './ThemeContext';
import Toolbar from './Toolbar';
function App() {
  return (
    <ThemeProvider>
      <Toolbar />
    </ThemeProvider>
  );
}

export default App;
```

In this updated example, we've created a `ThemeProvider` component that wraps the entire application. It manages the theme state using `useState` hook and syncs it with local storage using `useEffect`. The `toggleTheme` function allows toggling between light and dark themes, updating both state and local storage accordingly.

### Conclusion

React Context API provides a powerful mechanism for managing global state in React applications, reducing the need for prop drilling and making state management more intuitive. By integrating local storage, we can further enhance the capabilities of Context API, enabling seamless persistence of state across page reloads and enhancing the user experience. With this newfound knowledge, you're well-equipped to leverage React Context API and local storage in your projects to build more robust and user-friendly applications.

Thank you for joining me on this journey I hope you found this blog insightful and empowering as you continue to dive deeper into the world of React development. Remember, learning is a continuous process, and I'm here to support you every step of the way

Connection :- [Twitter](https://twitter.com/IngoleNehal) or [LinkedIn](https://www.linkedin.com/in/nehal-ingole/)