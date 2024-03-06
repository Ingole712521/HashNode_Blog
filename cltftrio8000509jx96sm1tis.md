---
title: "HTTP Methods"
seoTitle: "HTTP Methods"
datePublished: Wed Mar 06 2024 13:18:39 GMT+0000 (Coordinated Universal Time)
cuid: cltftrio8000509jx96sm1tis
slug: http-methods
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1709730342202/16005d6f-3df3-4cac-95ba-9e0a2cb35457.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1709731076314/1155eedf-f8cd-4318-b0cf-f7fa0fdaab7d.avif
tags: postman, twitter, nodejs, youtube, http-method, put-method, get-and-post, delete-method

---

## Introduction

In the vast world of web development, understanding HTTP methods is akin to mastering the language spoken between clients and servers. Every time you tweet on Twitter, upload a video on YouTube, or make any interaction on the web, HTTP methods are silently working behind the scenes to make it happen seamlessly.

Let's delve into the world of HTTP methods, exploring their types, functionalities, and real-world examples from platforms like YouTube and Twitter to solidify our understanding.

## **What are HTTP Methods?**

![What is HTTP: Components and Characteristics - Shiksha Online](https://images.shiksha.com/mediadata/ugcDocuments/images/wordpressImages/2022_11_MicrosoftTeams-image-83.jpg align="left")

HTTP (Hypertext Transfer Protocol) methods are a set of rules that dictate the types of actions that can be performed on the web. These methods define the operations that a client (such as a web browser) can perform on a web server. Each HTTP method has a specific purpose and usage, enabling various interactions between clients and servers.

---

## Commonly Used HTTP Methods

![HTTP Request Methods | GET, POST, PUT, DELETE - YouTube](https://i.ytimg.com/vi/tkfVQK6UxDI/hqdefault.jpg align="center")

1. GET: The GET method is used to retrieve data from a server. It requests a representation of the specified resource without altering it. GET requests are idempotent, meaning multiple identical requests will have the same effect as a single request. Example:
    
    ```javascript
    GET /articles HTTP/1.1
    Host: example.com
    ```
    
2. POST: POST is used to submit data to be processed to a specified resource. It often results in the creation of a new resource or the updating of an existing one. Unlike GET, POST requests are not idempotent, as each request may result in a different outcome. Example:
    
    ```javascript
    POST /articles HTTP/1.1
    Host: example.com
    Content-Type: application/json
    
    {
      "title": "New Article",
      "content": "Lorem ipsum dolor sit amet"
    }
    ```
    
3. PUT: PUT is used to update or replace the entire resource at a specific URL. It is idempotent, meaning that making the same PUT request multiple times will have the same effect as a single request. Example:
    
    ```javascript
    PUT /articles/123 HTTP/1.1
    Host: example.com
    Content-Type: application/json
    
    {
      "title": "Updated Title",
      "content": "Updated content"
    }
    ```
    
4. DELETE: DELETE is used to remove a specific resource from the server. It is also idempotent, as deleting a resource multiple times will have the same effect as a single deletion. Example:
    
    ```javascript
    DELETE /articles/123 HTTP/1.1
    Host: example.com
    ```
    
5. PATCH: PATCH is used to apply partial modifications to a resource. It is often used when you want to update only specific fields of a resource without affecting the rest. Example:
    
    ```javascript
    PATCH /articles/123 HTTP/1.1
    Host: example.com
    Content-Type: application/json
    
    {
      "title": "Updated Title"
    }
    ```
    

---

## **Real-world Examples**

1. **Twitter**: When you compose a tweet on Twitter and hit the 'Tweet' button, your browser sends a POST request to the Twitter server, containing the text of your tweet. Upon receiving this request, the server processes the tweet and adds it to your timeline.
    
2. **YouTube**: When you upload a video to YouTube, your browser sends a POST request to the YouTube server with the video file and metadata. The server then processes this request, stores the video on its servers, and makes it accessible to viewers.
    

---

## Example

```javascript
const fs = require('fs');
const http = require("http");
const url = require('url');
const myServer = http.createServer((req , res) => {
  if (req.url === "/favicon.ico")  
  return res.end;
  const log = `${Date.now()}: ${req.method} ${req.url }new Request received \n `;

const myUrl = url.parse(req.url, true);
console.log(myUrl);

  fs.appendFile("log.txt" , log, (err , data) => {
    switch (myUrl.pathname) {
      case "/":  if ( req.method === "GET") {  // get 
        res.end("Hello from server");            
      }     
        break;
      case "/about":
        const username = myUrl.query.myname;
        res.end(`Hi , ${username}`);
        break;
      case "/contact-us" : res.end("you can contact me ");
        break;
 
      case "/signup" :
        if (req.method === "GET")  {  // get request 
            res.end("This is signup form");
          
          }

         else if (req.method === "POST") {      // post request   
          res.end("Sucess");       
          
        };
        default : res.end("404 not found")

    }
  })

 
});

myServer.listen(8000 , ()  => console.log("server is listen"));
```

### Output of log file

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1709729872603/6189a832-c38b-45e1-b55c-ff4f47ccf0da.png align="center")

let's break down the code line by line:

```javascript
const fs = require('fs');
const http = require("http");
const url = require('url');
```

Here, we are importing necessary modules for our server. `fs` is used for file system operations, `http` is used to create an HTTP server, and `url` is used to parse URLs.

```javascript
const myServer = http.createServer((req , res) => {
```

This line creates an HTTP server using the `createServer()` method of the `http` module. It takes a callback function as an argument, which will be called whenever a request is made to the server. The `req` parameter represents the request object, and `res` represents the response object.

```javascript
  if (req.url === "/favicon.ico")  
  return res.end;
```

This line checks if the requested URL is for the favicon (icon displayed in the browser tab). If it is, it immediately ends the response without performing any further actions.

```javascript
  const log = `${Date.now()}: ${req.method} ${req.url }new Request received \n `;
```

This line constructs a log message containing the current timestamp, HTTP method, and requested URL. This log message will be appended to a file later.

```javascript
  const myUrl = url.parse(req.url, true);
```

Here, we parse the requested URL using the `url.parse()` method. This provides an object (`myUrl`) containing various components of the URL, such as pathname and query parameters.

```javascript
  fs.appendFile("log.txt" , log, (err , data) => {
```

This line appends the log message to a file named "log.txt" asynchronously. The callback function handles any errors that may occur during the file operation.

```javascript
    switch (myUrl.pathname) {
```

Here, we use a switch statement to handle different pathnames of the requested URL.

```javascript
      case "/":  if ( req.method === "GET") {  // get 
        res.end("Hello from server");            
      }     
        break;
```

If the pathname is "/", and the request method is GET, it sends a "Hello from server" message as the response and ends the response.

```javascript
      case "/about":
        const username = myUrl.query.myname;
        res.end(`Hi , ${username}`);
        break;
```

If the pathname is "/about", it extracts the value of the "myname" query parameter from the URL and sends a personalized greeting message as the response.

```javascript
      case "/contact-us" : res.end("you can contact me ");
        break;
```

If the pathname is "/contact-us", it sends a simple message indicating that you can contact the server.

```javascript
      case "/signup" :
        if (req.method === "GET")  {  // get request 
            res.end("This is signup form");
          
          }

         else if (req.method === "POST") {      // post request   
          res.end("Success");       
          
        };
```

If the pathname is "/signup", it checks if the request method is GET or POST. If it's GET, it sends a message indicating that it's a signup form. If it's POST, it sends a "Success" message.

```javascript
        default : res.end("404 not found")
```

If none of the above cases match, it sends a "404 not found" response.

```javascript
    }
  })
 
});

myServer.listen(8000 , ()  => console.log("server is listen"));
```

Finally, the server listens on port 8000, and a message is logged to the console once the server starts listening.

---

## Conclusion

HTTP methods form the backbone of communication in web development, providing a standardized set of actions for clients to interact with servers. By mastering these methods and understanding their nuances, developers can build efficient, scalable, and maintainable web applications. Whether you're retrieving data with GET, submitting forms with POST, updating resources with PUT or PATCH, or deleting items with DELETE, each HTTP method serves a specific purpose in shaping the web landscape.

As you continue your journey in web development, remember to leverage the power of HTTP methods effectively to design APIs and services that meet the needs of your users while adhering to best practices. Stay curious, experiment with different methods, and strive to create experiences that are both user-friendly and robust. With a solid understanding of HTTP methods, you'll be well-equipped to navigate the ever-evolving world of web development with confidence and creativity.

**Connect with us:**

* Hashnode: [https://hashnode.com/@Nehal71](https://hashnode.com/@Nehal71)
    
* Twitter : [https://twitter.com/IngoleNehal](https://twitter.com/IngoleNehal)
    
* LinkedIn: [https://www.linkedin.com/in/nehal-ingole/](https://www.linkedin.com/in/nehal-ingole/)