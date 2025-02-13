---
title: "TypeScript Interface and Types"
seoTitle: "TypeScript Interface and Types"
seoDescription: "An interface in TypeScript is a syntactical contract that an entity must adhere to. "
datePublished: Thu Feb 13 2025 08:38:10 GMT+0000 (Coordinated Universal Time)
cuid: cm7337ukw000r09kz3ohe99pl
slug: typescript-interface-and-types
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1739435791533/a0c3e74f-5b57-47f9-bb56-87dd099266df.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1739435860476/60d540c1-bcdd-44af-9994-a1ef8a96a139.jpeg
tags: typescript, interface, types, learninpublic

---

## Introduction

Creating and using functions is a fundamental aspect of any programming language, and TypeScript is no different. Today, we are going to explore **Interfaces** and **Types** in TypeScript. While TypeScript shares a similar syntax with JavaScript, it introduces type safety and additional features that improve code maintainability and readability.

---

## **Interfaces in TypeScript**

An **interface** in TypeScript is a syntactical contract that an entity must adhere to. It defines a standard structure that implementing classes or objects must follow. However, it does not contain any implementation details.

### **Key Features of Interfaces:**

* Defines the structure of an object.
    
* Only contains property and method declarations, without implementations.
    
* Can be implemented by classes or extended by other interfaces.
    

### **Example of an Interface:**

```typescript
interface User {
    name: string;
    age: number;
}

interface Manager {
    department: string;
}
```

In the above example, we have two interfaces: `User` and `Manager`, defining the required properties.

### **Implementing Interfaces in Objects:**

```typescript
let employee: User = {
    name: "John Doe",
    age: 30
};
```

The `employee` object strictly follows the `User` interface, ensuring type safety.

### **Extending Interfaces:**

Interfaces can be extended to create new interfaces with additional properties.

```typescript
interface TeamLead extends User, Manager {}

let teamLead: TeamLead = {
    name: "Alice",
    age: 35,
    department: "Engineering"
};
```

Here, `TeamLead` extends both `User` and `Manager`, so any object following `TeamLead` must include properties from both.

---

## **Types in TypeScript**

The **Type System** in TypeScript describes the various types used in the language. These types can be categorized into three main sections:

### **1\. Any Type**

The `any` type allows a variable to hold values of any type. While it provides flexibility, it negates TypeScript's type-checking benefits.

```typescript
let randomValue: any = "Hello";
randomValue = 42;
randomValue = true;
```

### **2\. Built-In Types**

TypeScript includes built-in types such as:

* `string`
    
* `number`
    
* `boolean`
    
* `null`
    
* `undefined`
    
* `void`
    

Example:

```typescript
let username: string = "Nehal";
let userAge: number = 24;
let isActive: boolean = true;
```

### **3\. User-Defined Types**

Apart from built-in types, TypeScript allows defining custom types using `type` aliases.

#### **Using Type Aliases:**

```typescript
type Employee = {
    name: string;
    age: number;
    position: string;
};

let dev: Employee = {
    name: "Nehal",
    age: 24,
    position: "Software Developer"
};
```

#### **Combining Types (Union & Intersection):**

* **Union Types:** A variable can hold multiple types.
    

```typescript
let id: string | number;
id = 101;
id = "A102";
```

* **Intersection Types:** Combines multiple types.
    

```typescript
type Manager = {
    department: string;
};

type TeamLead = User & Manager;

let lead: TeamLead = {
    name: "Sophia",
    age: 40,
    department: "IT"
};
```

---

## **Conclusion**

Understanding **Interfaces** and **Types** in TypeScript is crucial for writing clean, maintainable, and scalable code.

* **Interfaces** define object structure and can be extended or implemented.
    
* **Types** allow flexibility in defining custom types, including unions and intersections.
    

By leveraging TypeScript’s powerful type system, developers can improve code quality and prevent potential runtime errors. Happy coding!