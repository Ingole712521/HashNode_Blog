---
title: "My Rust Learning Journey (From Basics to Traits & Generics)"
seoTitle: "Rust Learning Journey Week 1 "
seoDescription: "Rust isn't really hard – it's just strict. Like that one teacher who had all those rules but actually made you a better student"
datePublished: Sun Feb 15 2026 14:29:53 GMT+0000 (Coordinated Universal Time)
cuid: cmlnudsw5000m02jm2mowfs71
slug: my-rust-learning-journey-from-basics-to-traits-and-generics
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1771165128924/ef00c9a7-ea21-452e-b21f-22dfd45f646f.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1771165768128/70825694-22bd-4982-b087-52e80cedc072.png
tags: learning, rust, learn, learn-to-code, web3, learning-in-public, rust-solana-web3, rust-lang, rustseries, rust-programming

---

# What is Rust 🦀

I've been diving into Rust lately, and it has been quite an adventure. Rust runs as fast as C/C++ but catches many bugs before your code even runs.

When I first started, something clicked for me pretty quickly:

> Rust isn't really hard – it's just strict. Like that one teacher who had all those rules but actually made you a better student.

And that strictness is actually Rust's superpower. Let me walk through everything I've picked up so far, using plain English and examples that actually make sense.

---

## 1\. Getting Rust on Your Machine

Before doing anything fun, we need Rust installed. The Rust folks made this simple with a tool called **rustup**.

### Installing Rust

If you're on Linux or Mac, open your terminal and paste this:

```sh
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Windows users can grab the installer straight from the official Rust website.

Once it's done, double-check everything worked:

```sh
rustc --version
cargo --version
```

---

## Meet Cargo – Your New Best Friend

Cargo is Rust's build system and package manager rolled into one. Think of it as a personal assistant that handles all the boring stuff so you can focus on coding.

Starting a new project is as simple as:

```sh
cargo new my_project
cd my_project
cargo run
```

And just like that, you've got a Rust project up and running.

---

## 2\. The Basics

### Hello World

```rust
fn main() {
    println!("Hello, Rust!");
}
```

### What's happening here?

* `fn main()` – every Rust program starts here. It's like the front door to your code.
    
* `println!()` – that exclamation mark means it's a macro (think of it as Rust's way of printing with superpowers).
    

---

## 3\. Variables – The "Write in Pen vs Pencil" Thing

Here's something that tripped me up at first: Rust variables don't like to change. They are **immutable by default**.

```rust
fn main() {
    let x = 10;
    x = 20; // This won't work!
    println!("{}", x);
}
```

If you want a variable that can change, you have to explicitly say so with `mut`:

```rust
fn main() {
    let mut x = 10;
    x = 20; // Now it works!
    println!("{}", x);
}
```

**Think of it this way:** A normal `let` is like writing with permanent ink. Once it's down, it's down. `mut` is like using a pencil – you can erase and change things whenever you need.

---

## 4\. Making Decisions and Repeating Stuff

### If-Else

```rust
fn main() {
    let age = 18;

    if age >= 18 {
        println!("You're an adult – congratulations!");
    } else {
        println!("Still got some time before adulthood");
    }
}
```

### For Loops

```rust
fn main() {
    for i in 1..6 {  // This goes 1, 2, 3, 4, 5
        println!("Number: {}", i);
    }
}
```

---

## 5\. Functions – Your Code's Building Blocks

Functions let you write code once and use it everywhere. Here's a simple one:

```rust
fn add(a: i32, b: i32) -> i32 {
    a + b  // Notice there's no semicolon? That means "return this"
}

fn main() {
    let result = add(5, 10);
    println!("Result: {}", result);
}
```

**Quick tip:** In Rust, the last line of a function automatically becomes the return value if you don't put a semicolon.

---

## 6\. Structs – Grouping Related Stuff Together

Think of structs as custom data containers. They let you bundle related information:

```rust
struct Student {
    name: String,
    age: u32,
}

fn main() {
    let s1 = Student {
        name: String::from("Rohan"),
        age: 20,
    };

    println!("Student name: {}", s1.name);
    println!("Student age: {}", s1.age);
}
```

**Imagine it like this:** A struct is like a student ID card – it holds all the important details about someone in one place.

---

## 7\. Ownership – Rust's Secret Sauce (And Why It Matters)

This is the big one. The concept that makes Rust special.

### The Three Rules of Ownership:

1. Every piece of data has one owner (and only one)
    
2. When the owner goes away, the data goes with it
    
3. You can't have two owners at once
    

### Seeing Ownership in Action

```rust
fn main() {
    let s1 = String::from("Rust");
    let s2 = s1;  // Ownership moves from s1 to s2 here

    println!("{}", s2);
    // println!("{}", s1); // This would crash
}
```

### Why does that last line crash?

Because when we did `let s2 = s1`, Rust said "okay, s1 is done with this string, it's yours now s2." Try to use s1 after that, and Rust shuts it down.

**Here's a way to think about it:** Imagine you lend your favorite book to a friend. You don't have it anymore, right? If someone asks you for that book, you can't give it to them – it's not in your hands. That's ownership in Rust.

---

## 8\. Cloning – When You Actually Want Copies

Sometimes you genuinely need two copies of something. That's where `.clone()` comes in:

```rust
fn main() {
    let s1 = String::from("Rust");
    let s2 = s1.clone();  // Makes a whole new copy

    println!("{}", s1);  // Both work now
    println!("{}", s2);
}
```

**Think photocopy machine:** You've got your original document, you make a copy, and now you have two separate documents. Change one, the other stays the same.

---

## 9\. Borrowing – Using Things Without Owning Them

What if you want to let someone use your data without giving it away forever? That's borrowing:

```rust
fn print_length(s: &String) {  // The & means "borrowing"
    println!("Length: {}", s.len());
}

fn main() {
    let name = String::from("Rust");

    print_length(&name);  // Lending it out temporarily

    println!("Still have it: {}", name);  // Still mine
}
```

**Like lending your bike:** Your friend can ride it, but at the end of the day, it's still your bike.

---

## 10\. Mutable Borrowing – When Your Friend Can Modify Your Stuff

Sometimes you want to let someone not just use your data, but change it too:

```rust
fn add_word(s: &mut String) {
    s.push_str(" Language");
}

fn main() {
    let mut name = String::from("Rust");

    add_word(&mut name);

    println!("{}", name);  // Prints "Rust Languge"
}
```

### But here's the catch – Rust has a strict rule:

You can only have **one mutable borrow at a time**.

**Why?** Imagine two people editing the same Google Doc simultaneously, making conflicting changes. Chaos, right? Rust prevents that chaos by saying "only one editor at a time, please."

---

## 11\. Match – Like Switch Statements on Steroids

Rust's `match` is incredibly powerful. It's like a supercharged switch statement:

```rust
fn main() {
    let num = 2;

    match num {
        1 => println!("It's one"),
        2 => println!("It's two"),
        3 => println!("It's three"),
        _ => println!("Something else entirely"),
    }
}
```

The `_` at the end is like "everything else" – Rust's way of making sure you cover all possibilities.

---

## 12\. Option – Rust's Smarter Way to Handle "Nothing"

Here's something cool: Rust doesn't have `null`. No null pointer exceptions! Instead, it uses `Option`, which can be either:

* `Some(value)` – there's something here
    
* `None` – nothing to see here
    

### Option in Action

```rust
fn get_name(flag: bool) -> Option<String> {
    if flag {
        Some(String::from("Rust"))
    } else {
        None
    }
}

fn main() {
    let name = get_name(true);

    match name {
        Some(n) => println!("Found a name: {}", n),
        None => println!("No name found"),
    }
}
```

**Picture it like this:** Option is a gift box. Sometimes you open it and there's a present inside (`Some`). Sometimes it's empty (`None`). The key is – Rust makes you check before opening.

---

## 13\. Result – Handling Errors the Rust Way

When things can go wrong, Rust uses `Result`. It's either:

* `Ok(value)` – everything worked!
    
* `Err(error)` – something went wrong
    

### Result Example

```rust
fn divide(a: i32, b: i32) -> Result<i32, String> {
    if b == 0 {
        Err(String::from("Can't divide by zero – nice try!"))
    } else {
        Ok(a / b)
    }
}

fn main() {
    let result = divide(10, 2);

    match result {
        Ok(val) => println!("Answer: {}", val),
        Err(err) => println!("Oops: {}", err),
    }
}
```

**Think of it like a test result:** You either pass (`Ok`) or fail with a reason (`Err`). The best part? Rust won't let you ignore the possibility of failure – you have to handle it.

---

## 14\. Traits – Defining What Things Can Do

Traits are Rust's way of saying "anything that wants to be this kind of thing must be able to do these things." Sort of like interfaces in other languages:

```rust
trait Animal {
    fn sound(&self);
}

struct Dog;
struct Cat;

impl Animal for Dog {
    fn sound(&self) {
        println!("Woof!");
    }
}

impl Animal for Cat {
    fn sound(&self) {
        println!("Meow...");
    }
}

fn main() {
    let d = Dog;
    let c = Cat;

    d.sound();
    c.sound();
}
```

**Here's the analogy:** A trait is like a job description. It says "whoever takes this job must know how to do X." Then Dog and Cat apply for the job and show they can do it.

---

## 15\. impl – Adding Methods to Your Structs

The `impl` keyword lets you attach functions to your structs:

```rust
struct Student {
    name: String,
    age: u32,
}

impl Student {
    fn display(&self) {
        println!("Name: {}", self.name);
        println!("Age: {}", self.age);
    }
}

fn main() {
    let s1 = Student {
        name: String::from("Rohan"),
        age: 20,
    };

    s1.display();  // Calling our method
}
```

**Think of it this way:** Your struct is the phone hardware. `impl` adds the apps and features that make the phone useful.

---

## 16\. Generics – Write Once, Work Everywhere

Generics let you write functions that work with multiple types:

```rust
fn print_value<T>(value: T)
where
    T: std::fmt::Debug,  // T must be printable
{
    println!("{:?}", value);
}

fn main() {
    print_value(10);        // Works with number
    print_value("Rust");     // Works wit text
    print_value(3.14);       // Works with decmals
}
```

That `<T>` is saying "T can be any type." It's like telling Rust "trust me, whatever type shows up, we'll handle it."

**The best analogy:** Generics are like a universal adapter. Same plug, works with different devices.

---

## Wrapping Up (What I've Learned So Far)

Looking back, here's what I've covered:

* Getting Rust set up with rustup
    
* Using Cargo to manage projects
    
* Variables, functions, and all the usual programming stuff
    
* Structs for grouping data
    
* **Ownership** – the thing that makes Rust Rust
    
* Borrowing (both regular and mutable)
    
* Pattern matching with match
    
* Option for handling missing values
    
* Result for dealing with errors
    
* Traits for defining shared behavior
    
* impl for adding methods
    
* Generics for writing flexible code
    

Rust feels strict at first because it cares. It cares about memory safety, about preventing bugs, about making you write better code. Once you stop fighting that strictness and start working with it, everything clicks.

The journey's just beginning. If you're learning Rust too,stick with it – that initial "why won't this compile" frustration turns into "oh, that's actually really smart" pretty quickly.

**Connect with :**

* Hashnode: [**hashnode.com/@Nehal71**](http://hashnode.com/@Nehal71)
    
* Twitter : [**twitter.com/IngoleNehal**](http://twitter.com/IngoleNehal)
    
* LinkedIn: [**linkedin.com/in/nehal-ingole**](http://linkedin.com/in/nehal-ingole)
    
* GitHub : [**github.com/Ingole712521**](http://github.com/Ingole712521)