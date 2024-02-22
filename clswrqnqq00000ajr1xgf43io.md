---
title: "Mastering UI Flexibility"
datePublished: Thu Feb 22 2024 05:14:22 GMT+0000 (Coordinated Universal Time)
cuid: clswrqnqq00000ajr1xgf43io
slug: mastering-ui-flexibility
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1708578523836/1103c9a7-4572-44ac-8985-d60314beb6df.webp
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1708578643258/d8f2194e-626f-480c-ad33-dbd11e3c5ff0.webp
tags: props, tailwind-css, tailwind-css-tutorial, learning-in-public, props-in-reactjs

---

## **Introduction**

In the realm of modern web development, efficiency and flexibility are paramount. Tailwind CSS and React.js have emerged as two powerful tools that streamline development workflows and enhance code maintainability. In this comprehensive guide, we'll delve into the intricacies of Tailwind CSS and the concept of props in React. Additionally, we'll combine these concepts to create a Todo list practical implementation.

## **Tailwind CSS**

![Tailwind CSS: The Utility-First CSS Framework Powering Modern Web Design](https://balticanebula.com/content/images/2023/06/plus-tailwind.jpg align="left")

Tailwind CSS is a utility-first CSS framework that provides a comprehensive set of pre-defined utility classes to style your HTML elements. Unlike traditional CSS frameworks like Bootstrap or Foundation, which come with pre-designed components, Tailwind CSS focuses on providing low-level utility classes that can be composed to create custom designs quickly and efficiently.

## **Key Concepts of Tailwind CSS**

1. **Utility-First Approach:** Tailwind CSS adopts a utility-first approach, which means that styling is applied directly in HTML markup using classes like `bg-blue-500` for setting background color or `p-4` for adding padding. This approach promotes clarity and enables rapid prototyping without the need to write custom CSS.
    
2. **Responsive Design:** Tailwind CSS offers built-in support for creating responsive designs by providing responsive utility classes like `sm:`, `md:`, `lg:`, and `xl:`. These classes allow you to define different styles for various screen sizes, ensuring a consistent user experience across different devices.
    
3. **Customization:** Tailwind CSS is highly customizable, allowing developers to tailor the framework to suit their specific project requirements. You can customize everything from colors, fonts, spacing, breakpoints, and more by modifying the `tailwind.config.js` file.
    
4. **Just-in-Time (JIT) Mode:** Introduced in Tailwind CSS v2.1, the Just-in-Time (JIT) mode significantly improves build times by generating CSS on-demand as you use it in your HTML templates. This mode eliminates unused CSS and results in smaller bundle sizes, making Tailwind CSS even more efficient for production use.
    

### **Example**

Let's consider a scenario where we want to create a simple pricing component using Tailwind CSS. We'll define different pricing tiers with varying features and styles.

```html
<!-- Pricing Component -->
<div class="max-w-md mx-auto">
  <div class="bg-white shadow-lg rounded-lg overflow-hidden">
    <div class="px-4 py-5 sm:px-6">
      <h3 class="text-lg font-semibold leading-6 text-gray-900">Basic Plan</h3>
      <p class="mt-1 text-sm text-gray-500">Perfect for small teams or individuals.</p>
    </div>
    <div class="border-t border-gray-200 px-4 py-5 sm:p-6">
      <dl>
        <div class="mb-4">
          <dt class="text-sm font-medium text-gray-500">Features</dt>
          <dd class="mt-1 text-sm text-gray-900">
            <ul class="list-disc list-inside">
              <li>10 projects</li>
              <li>Basic analytics</li>
              <li>No support</li>
            </ul>
          </dd>
        </div>
        <div class="mb-4">
          <dt class="text-sm font-medium text-gray-500">Price</dt>
          <dd class="mt-1 text-lg font-semibold text-gray-900">$29 / month</dd>
        </div>
        <div>
          <a href="#" class="block w-full bg-gray-800 py-2 px-4 border border-transparent rounded-md text-center font-semibold text-white uppercase hover:bg-gray-700">Subscribe</a>
        </div>
      </dl>
    </div>
  </div>
</div>
```

In this example, we've used various Tailwind CSS utility classes to style different elements of the pricing component:

* `bg-white`, `shadow-lg`, `rounded-lg`: Styling the outer container with a white background, drop shadow, and rounded corners.
    
* `px-4`, `py-5`, `sm:px-6`, `sm:p-6`: Adding padding to different sections of the component, with increased padding on larger screens (responsive design).
    
* `text-lg`, `text-sm`, `font-semibold`: Setting text sizes and font weights for headings and paragraphs.
    
* `list-disc`, `list-inside`: Styling the list of features with disc bullets and placing them inside the list items.
    
* `bg-gray-800`, `py-2`, `px-4`, `border`, `rounded-md`, `text-white`, `uppercase`: Styling the subscribe button with a dark background, padding, border, rounded corners, and white text.
    

---

## **Props in React**

![An introduction to React component props](https://scrimba.com/articles/content/images/2022/10/Learn-React-props-in-one-tutorial-3.png align="left")

In React.js, props (short for properties) are a mechanism for passing data from parent to child components. Props allow components to be dynamic and reusable by enabling communication between them. Props are immutable and are passed down from parent components to child components.

## **Key Aspects of Props in React**

1. **Passing Data:** Props are passed from parent to child components as attributes similar to HTML attributes. Parent components can pass data, functions, or even other React components as props to their children.
    
2. **Immutable:** Props are read-only and cannot be modified by the child component. They are considered immutable data. This ensures that the data passed from the parent remains unchanged within the child component, preserving data integrity.
    
3. **Dynamic Rendering:** Props enable dynamic rendering of components based on the data passed from their parent components. By passing different props to the same component, you can customize its behavior and appearance dynamically.
    
4. **Component Composition:** Props facilitate component composition by allowing components to be configured and customized through the data passed via props. This promotes reusability and modularity in React applications, as components can be easily composed to build complex user interfaces.
    

### **Example**

Let's create a simple `Button` component in React that accepts props for styling and onClick functionality.

```jsx
// Button.js
import React from 'react';

const Button = ({ label, onClick, variant }) => {
  const buttonStyles = `py-2 px-4 rounded ${variant === 'primary' ? 'bg-blue-500 text-white' : 'bg-gray-300 text-gray-700'}`;

  return (
    <button className={buttonStyles} onClick={onClick}>
      {label}
    </button>
  );
};

export default Button;
```

In this example:

* We define a functional component called `Button`.
    
* The component accepts three props: `label` (the text displayed on the button), `onClick` (the function to be executed when the button is clicked), and `variant` (the styling variant of the button).
    
* We dynamically determine the button's styles based on the `variant` prop. If `variant` is `'primary'`, the button will have blue background and white text, otherwise, it will have gray background and dark gray text.
    
* When the button is clicked, the `onClick` function provided as a prop is executed.
    

Now, let's use the `Button` component in a parent component:

```jsx
// App.js
import React from 'react';
import Button from './Button';

const App = () => {
  const handleClick = () => {
    alert('Button clicked!');
  };

  return (
    <div className="container mx-auto mt-4">
      <Button label="Primary Button" onClick={handleClick} variant="primary" />
      <Button label="Secondary Button" onClick={handleClick} />
    </div>
  );
};

export default App;
```

In this example:

* We import the `Button` component and use it twice in the `App` component.
    
* Each `Button` instance receives different props: one with a `'primary'` variant and the other with the default variant.
    
* We pass the `handleClick` function as the `onClick` prop, which will be executed when the button is clicked.
    

This demonstrates how props enable communication between parent and child components in React, allowing for dynamic and reusable UI components.

---

## Todo List

![Premium Photo | To do list icon a notebook with a completed todo list 3d  render](https://img.freepik.com/premium-photo/list-icon-notebook-with-completed-todo-list-3d-render_471402-428.jpg align="center")

Integrating Tailwind CSS with React using props in a todo list application involves creating reusable components for tasks, passing task data via props, and dynamically styling the components based on the task status.

Below is an example of how you can implement a todo list using Tailwind CSS and React

### **Step 1: Create Task Component**

Create a `Task.js` component to represent individual tasks in the todo list. This component will receive task data via props and dynamically style the task based on its status.

```jsx
// Task.js
import React from 'react';

const Task = ({ task }) => {
  const taskClasses = `flex items-center justify-between px-4 py-2 border-b border-gray-200 ${task.completed ? 'bg-green-100' : 'bg-white'}`;

  return (
    <div className={taskClasses}>
      <span className="text-lg">{task.title}</span>
      <input type="checkbox" checked={task.completed} onChange={() => {}} />
    </div>
  );
};

export default Task;
```

### **Step 2: Create TodoList Component**

Create a `TodoList.js` component to display a list of tasks. This component will receive an array of tasks as props and render individual `Task` components for each task.

```jsx
// TodoList.js
import React from 'react';
import Task from './Task';

const TodoList = ({ tasks }) => {
  return (
    <div className="max-w-md mx-auto mt-8">
      {tasks.map(task => (
        <Task key={task.id} task={task} />
      ))}
    </div>
  );
};

export default TodoList;
```

### **Step 3: Create App Component**

Create the main `App.js` component to manage the state of the todo list and render the `TodoList` component.

```jsx
// App.js
import React, { useState } from 'react';
import TodoList from './TodoList';

const App = () => {
  const [tasks, setTasks] = useState([
    { id: 1, title: 'Create Blog', completed: false },
    { id: 2, title: 'Leetcode Question', completed: true },
    { id: 3, title: 'Project process', completed: false }
  ]);

  return (
    <div className="container mx-auto">
      <h1 className="text-3xl font-semibold text-center mt-8">Todo List</h1>
      <TodoList tasks={tasks} />
    </div>
  );
};

export default App;
```

### **Step 4: Styling with Tailwind CSS**

Ensure you have Tailwind CSS configured in your project. You can include Tailwind CSS in your project using various methods like CDN, npm, or yarn.

### **Step 5: Run the Application**

Run your React application using `npm start` or `yarn start` and navigate to the localhost address in your browser to see the todo list in action.

This setup creates a simple todo list application where tasks are represented as components, and their status is dynamically styled using Tailwind CSS classes based on the `completed` prop. You can expand this application by adding functionality to add, delete, or mark tasks as completed.

---

## Conclusion

**Tailwind CSS** empowers developers with a utility-first approach, offering a vast array of pre-defined classes that streamline the styling process. By leveraging Tailwind CSS, developers can rapidly prototype and customize UI components, ensuring flexibility and efficiency throughout the development cycle. With features like responsive design, customization options, and Just-in-Time mode, Tailwind CSS proves to be a versatile tool for creating modern and visually appealing web applications.

**Props in React** serve as a crucial mechanism for communication between components, enabling dynamic rendering and reusability. By passing data from parent to child components via props, React developers can build modular and scalable applications with ease. Whether it's configuring component behavior or customizing appearance, props facilitate seamless integration and composition of React components, enhancing code maintainability and extensibility.

Thank you for joining me on this journey I hope you found this blog insightful and empowering as you continue to dive deeper into the world of React development. Remember, learning is a continuous process, and I'm here to support you every step of the way

Connection :- [Twitter](https://twitter.com/IngoleNehal) or [LinkedIn](https://www.linkedin.com/in/nehal-ingole/)