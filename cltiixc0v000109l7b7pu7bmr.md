---
title: "Building rest API"
seoTitle: "Building rest API"
datePublished: Fri Mar 08 2024 10:38:33 GMT+0000 (Coordinated Universal Time)
cuid: cltiixc0v000109l7b7pu7bmr
slug: building-rest-api
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1709893942597/14d73a3b-7c86-4230-b13d-487e3ede5fd9.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1709894297958/36e74700-4430-4e7a-a05b-75bdb6914b7b.png
tags: apis, reactjs, delete, 2articles1week, learning-journey, data-access, learninpublic, building-rest-api, patch-request

---

## Introduction

In today's interconnected digital world, APIs (Application Programming Interfaces) play a vital role in enabling communication and data exchange between various software applications. Whether you're a developer looking to enhance your skills or a curious individual eager to understand the magic behind modern technology, this guide will demystify APIs and walk you through the process of building your very first API from scratch.

## What is an API?

Before diving into the technical details, let's clarify what an API actually is. Think of an API as a messenger that facilitates communication between different software systems. It defines a set of rules and protocols that allow one application to interact with another, accessing and sharing data seamlessly.

![How to Develop A Secure REST API in Node.js - Peerbits](https://www.peerbits.com/static/d0e6cd2765ae3b9f7d1a565a2f8c0125/0a779/rest-api-code-main.png align="center")

---

## Why are APIs important?

APIs are the backbone of modern software development, enabling developers to leverage existing functionality and integrate it into their own applications. They promote collaboration, efficiency, and innovation by providing standardized interfaces for accessing services and data.

---

## Example

```javascript
const express = require('express');
const app = express();
const PORT = 8000;
const users = require("./MOCK_DATA.json");


app.get("/users" , (req , res ) => {
  const html =  `
  <ul>
    ${users.map((user) => `<li>${user.first_name}</li>`).join("")}
  </ul>
  `;
  res.send(html)
})

app.get("/api/users" , (req, res ) => {
  return res.json(users);
})


app
.route("/api/users/:id")
.get((req , res) => {
  const id = Number(req.params.id);
  const user = users.find((user) => user.id === id);
  return res.json(user)
})

.patch((req, res) => {
 // edit user with id
  return res.json({ status : "pending "})
}) 

.delete((req , res ) => {
  //  delete user with id
  return res.json({status : "pending"})
})



app.post('/api/users' , (req, res) =>{
  res.json({status : "pending"})
})

app.listen(PORT , () => console.log(`Server started ${PORT}`))
```

### **1\. Setting Up The Project**

* `const express = require('express');`: This line imports the Express framework, which is a popular tool for building web applications and APIs in JavaScript. Essentially, it provides a structure for handling requests and sending responses.
    
* `const app = express();`: Here, we create an instance of the Express application. This will be the core object we use to define our API's functionalities.
    
* `const PORT = 8000;`: This line defines the port number (8000 in this case) on which our API will listen for incoming requests.
    

### **2\. Data Access**

* `const users = require("./MOCK_DATA.json");`: This line imports data from a file likely named `MOCK_DATA.json`. This file presumably contains an array of user objects, each with properties like `id` and `first_name`. This data will be used to populate the API responses.
    

### **3\. Defining API Endpoints**

The code defines several routes, which are essentially different paths within the API that users can access. Here's a breakdown of each route:

* `/users` (GET Request):
    
    * This responds to a GET request sent to the `/users` path.
        
    * It creates an HTML string with an unordered list (`<ul>`) containing list items (`<li>`) for each user's first name (`user.first_name`) retrieved from the `users` data.
        
    * The `map` function iterates through the `users` array and creates an `<li>` element for each user.
        
    * Finally, `res.send(html)` sends the generated HTML as the response to the user's request. This is a basic example and wouldn't typically be used for real APIs that provide JSON data.
        
* `/api/users` (GET Request):
    
    * This responds to a GET request sent to the `/api/users` path.
        
    * It directly sends the entire `users` data (presumably an array of user objects) as a JSON response using `res.json(users)`. This is a more standard way to provide data through an API.
        
* `/api/users/:id` (Multiple Methods):
    
    * This route pattern uses `:id` as a placeholder for a dynamic value. It can handle different HTTP methods (GET, PATCH, DELETE) depending on the request.
        
        * **GET Request:**
            
            * It retrieves the user object with the matching ID from the `users` data using [`req.params.id`](http://req.params.id) to access the ID value from the request URL.
                
            * It then sends the retrieved user object as a JSON response using `res.json(user)`.
                
        * **PATCH Request:**
            
            * This part of the code currently doesn't implement any logic for editing a user. It simply sends a JSON response with a status of "pending."
                
        * **DELETE Request:**
            
            * Similar to PATCH, this section lacks implementation for deleting users. It just sends a "pending" status response.
                
* `/api/users` (POST Request):
    
    * This route likely intends to handle creating new users, but currently, it just sends a "pending" status response using `res.json({status : "pending"})`.
        

### **4\. Starting the Server**

* `app.listen(PORT , () => console.log(`Server started on port ${PORT}`))`: This line tells the Express app to start listening for requests on the defined port (8000 in this case). When the server starts successfully, it logs a message to the console indicating the port on which it's listening.
    

Overall, this code provides a basic example of an API built with Express. It demonstrates how to define routes, access data, and send responses in different formats (HTML and JSON). However, some functionalities like user editing, deletion, and creation are not currently implemented.

### Output

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1709893390618/44ac0352-3562-4296-909d-f58740222baa.png align="center")

**By ID**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1709893404893/715b110c-ad66-4ae6-be26-7f1c72ffbd89.png align="center")

---

## Conclusion

APIs are the backbone of modern software development, enabling seamless communication and data exchange between different applications. By understanding the basics of APIs and following the steps outlined in this guide, you've taken the first step towards becoming a proficient API developer.

Building your own API from scratch may seem daunting at first, but with the right approach and mindset, it's entirely achievable. Remember to focus on clarity, consistency, and user experience throughout the development process. Document your API thoroughly to help other developers understand its functionality and unleash its full potential.

As you continue your journey in the world of APIs, don't hesitate to explore new technologies, experiment with different design patterns, and collaborate with fellow developers. The possibilities are endless, and by harnessing the power of APIs, you can create innovative solutions that drive progress and enhance the way we interact with technology.

Thank you for joining us on this journey to demystify APIs and learn how to build your first API from scratch. We hope this guide has provided you with valuable insights and practical knowledge that you can apply to your future projects.

**Connect with us:**

* Hashnode: [https://hashnode.com/@Nehal71](https://hashnode.com/@Nehal71)
    
* Twitter : [https://twitter.com/IngoleNehal](https://twitter.com/IngoleNehal)
    
* LinkedIn: [https://www.linkedin.com/in/nehal-ingole/](https://www.linkedin.com/in/nehal-ingole/)