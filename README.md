# Table of Contents
- [Cargo](#cargo)
- [Guessing Game](#guessing-game)
- [Variables](#variables)
  - [Constants](#constants)
- [Data Types](#data-types)
  - [Scalar Data Types](#scalar-data-types)
    - [Integers](#integers)
    - [Floating-point Numbers](#floating-point-numbers)
    - [Booleans](#booleans)
    - [Character (use single quotes)](#character-use-single-quotes)
  - [Compound Data Types](#compound-data-types)
    - [Tuple (0-indexed)](#tuple-0-indexed)
    - [Array (0-indexed, fixed length)](#array-0-indexed-fixed-length)
- [Functions](#functions)
- [Control Flow](#control-flow)
  - [If statements](#if-statements)
  - [Loops](#loops)
    - [`loop`](#loop)
    - [`while`](#while)
    - [`for`](#for)
  - [Comments](#comments)
- [Memory in Rust](#memory-in-rust)
  - [Pros and Cons of Different Ways of Handling Memory](#pros-and-cons-of-different-ways-of-handling-memory)
  - [Stack and Heap](#stack-and-heap)
    - [The Stack](#the-stack)
    - [The Heap](#the-heap)
    - [Stack vs. Heap](#stack-vs-heap)
    - [Example](#example)
  - [Ownership Rules -- 3 Rules in Rust](#ownership-rules----3-rules-in-rust)
  - [Copy, Move, Clone](#copy-move-clone)
- [References and Borrowing](#references-and-borrowing)
  - [Borrowing](#borrowing)
  - [Rules of References, Reference Rules](#rules-of-references-reference-rules)
    - [Mutable References](#mutable-references)
    - [Dangling References](#dangling-references)
  - [Slices](#slices)
- [Structs](#structs)
  - [Attributes of a Struct](#attributes-of-a-struct)
  - [Tuple Structs (anonymous structs)](#tuple-structs-anonymous-structs)
  - [Example to Show the Value of Structs](#example-to-show-the-value-of-structs)
  - [Derived Traits](#derived-traits)
  - [Methods](#methods)
  - [Associated Functions](#associated-functions)
- [Enums](#enums)
  - [Enum Methods](#enum-methods)
  - [Option Enum](#option-enum)
  - [Match Expression](#match-expression)
    - [`if let` syntax](#if-let-syntax)
- [Rust's Module System](#rusts-module-system)
  - [Crates](#crates)
    - [Rules around Crates:](#rules-around-crates)
  - [Modules](#modules)
    - [Paths and Module Privacy Rules](#paths-and-module-privacy-rules)
  - [Privacy Rules with Structs and Enums](#privacy-rules-with-structs-and-enums)
  - [`Use` keyword](#use-keyword)
    - [Re-Exporting](#re-exporting)
    - [External Dependencies](#external-dependencies)
    - [Nested Paths](#nested-paths)
    - [Glob Operator (`*`)](#glob-operator)
  - [Modules in Separate Files](#modules-in-separate-files)
  - [SUMMARY:](#summary)
- [Common Collections in Rust](#common-collections-in-rust)
  - [Vectors](#vectors)
    - [Initializing Vectors](#initializing-vectors)
    - [Accessing Values in Vectors](#accessing-values-in-vectors)
    - [Iterating Over Elements in a Vector](#iterating-over-elements-in-a-vector)
    - [Storing Different Types of Data in Vectors](#storing-different-types-of-data-in-vectors)
  - [Strings](#strings)
    - [Creating a New String](#creating-a-new-string)
    - [Appending to a String](#appending-to-a-string)
    - [Indexing into a String](#indexing-into-a-string)
  - [Hashmaps](#hashmaps)
    - [Creating a Hashmap](#creating-a-hashmap)
    - [Accessing Values in a Hashmap](#accessing-values-in-a-hashmap)
    - [Iterating Over the Elements in Hashmap](#iterating-over-the-elements-in-hashmap)
    - [Updating the Hashmap](#updating-the-hashmap)
- [Error Handling in Rust](#error-handling-in-rust)
  - [panic! Macro](#panic-macro)
  - [`Result` Enum](#result-enum)
    - [Useful Functions on the `Result` Enum](#useful-functions-on-the-result-enum)
    - [Error Propagation with the `Result` Enum](#error-propagation-with-the-result-enum)
    - [The `?` Operator with the `Result` Enum](#the--operator-with-the-result-enum)
  - [`panic!` vs. `Result`](#panic-vs-result)
  - [Custom Types](#custom-types)
- [Generics](#generics)
  - [Motivation](#motivation)
  - [Defining Generic Types](#defining-generic-types)
  - [Generics with Structs](#generics-with-structs)
  - [Generics with Enums](#generics-with-enums)
  - [Generics in Method Definitions](#generics-in-method-definitions)
  - [Performance Impact of Using Generics](#performance-impact-of-using-generics)
- [Traits](#traits)
  - [Default Implementations](#default-implementations)
  - [Trait Bounds](#trait-bounds)
    - [Returning Types that Implement Traits](#returning-types-that-implement-traits)
  - [Using Trait Bounds to Conditionally Implement Methods](#using-trait-bounds-to-conditionally-implement-methods)
  - [Blanket Implementations](#blanket-implementations)
- [Lifetimes](#lifetimes)
  - [Generic Lifetime Annotations](#generic-lifetime-annotations)
  - [Writing Generic Lifetime Annotations](#writing-generic-lifetime-annotations)
  - [Lifetime Annotations in Struct Definitions](#lifetime-annotations-in-struct-definitions)
  - [Lifetime Elision Rules](#lifetime-elision-rules)
  - [Lifetime Annotations Inside of Methods](#lifetime-annotations-inside-of-methods)
  - [Static Lifetimes](#static-lifetimes)
- [Generics, Traits, Trait Bounds, and Lifetimes All Together](#generics-traits-trait-bounds-and-lifetimes-all-together)
- [Testing](#testing)
  - [Why do we want to write Tests?](#why-do-we-want-to-write-tests)
  - [Writing Tests](#writing-tests)
    - [Adding a Test that Fails](#adding-a-test-that-fails)
  - [Testing Product Code](#testing-product-code)
  - [`assert_eq!` Macro](#assert_eq-macro)
    - [`assert_ne!` Macro](#assert_ne-macro)
  - [Custom Failure Messages](#custom-failure-messages)
  - [Asserting that a Function Fails](#asserting-that-a-function-fails)
  - [Tests that Return a `Result` Type](#tests-that-return-a-result-type)
    - [Why Tests that Return `Result` Are Useful...](#why-tests-that-return-result-are-useful)
    - [How the `?` Operator is Useful Here](#how-the--operator-is-useful-here)
    - [Examples](#examples)
  - [Controlling How Tests Run](#controlling-how-tests-run)
    - [Changing the Number of Threads](#changing-the-number-of-threads)
    - [Showing Output](#showing-output)
    - [Running a Subset of Tests](#running-a-subset-of-tests)
    - [Ignoring Tests](#ignoring-tests)
  - [Test Organization](#test-organization)
    - [Unit Tests](#unit-tests)
    - [Integration Tests](#integration-tests)
- [CLI Program](#cli-program)
- [Closures](#closures)
  - [Closure Environment Capturing](#closure-environment-capturing)
    - [Closure Environment Capturing Modes in Rust](#closure-environment-capturing-modes-in-rust)
  - [Closure Type Inference](#closure-type-inference)
  - [Closure Example Use Case](#closure-example-use-case)
- [Iterators](#iterators)
  - [How Iterators Work](#how-iterators-work)
  - [Additional Iterator Methods with Default Implementations](#additional-iterator-methods-with-default-implementations)
  - [Implementing Our Own Iterator](#implementing-our-own-iterator)
- [Iterators in Practice](#iterators-in-practice)
  - [Removing the Use of `clone()` by Using Iterators](#removing-the-use-of-clone-by-using-iterators)
  - [Simplifying `search()` Using Iterator Adaptor Functions](#simplifying-search-using-iterator-adaptor-functions)
  - [Should I Use Loops or Iterators?](#should-i-use-loops-or-iterators)
- [Publishing a Rust Crate](#publishing-a-rust-crate)
  - [Preparing Your Code for Public Consumption](#preparing-your-code-for-public-consumption)
  - [`//!` Comments](#-comments)
  - [Re-Exporting / Exporting a Public API](#re-exporting--exporting-a-public-api)
  - [Publishing to crates.io](#publishing-to-cratesio)
  - [Removing Versions from crates.io](#removing-versions-from-cratesio)
- [Cargo Workspaces](#cargo-workspaces)
  - [Installing Binaries from crates.io with `cargo install`](#installing-binaries-from-cratesio-with-cargo-install)
  - [Extending Cargo with Custom Commands](#extending-cargo-with-custom-commands)
- [Smart Pointers in Rust](#smart-pointers-in-rust)
  - [References](#references)
  - [Smart Pointers Introduction](#smart-pointers-introduction)
  - [Smart Pointer Summary (IMPORTANT!!!)](#smart-pointer-summary-important)
  - [IMPORTANT DISTINCTION: `Rc<RefCell<T>>` vs. `RefCell<Rc<T>>`](#important-distinction-rcrefcellt-vs-refcellrct)
  - [The `Box` Smart Pointer](#the-box-smart-pointer)
    - [`Box` Example](#box-example)
  - [`Deref` Trait](#deref-trait)
    - [Creating Our Own Smart Pointer that Implements the `Deref` Trait](#creating-our-own-smart-pointer-that-implements-the-deref-trait)
    - [Implicit Deref Coercion with Functions and Methods](#implicit-deref-coercion-with-functions-and-methods)
  - [The `Drop` Trait](#the-drop-trait)
  - [Reference Counting](#reference-counting)
    - [`Cons` List Example with `Rc`](#cons-list-example-with-rc)
  - [Interior Mutability](#interior-mutability)
    - [`RefCell` Smart Pointer](#refcell-smart-pointer)
    - [USE CASE for the Interior Mutability Pattern](#use-case-for-the-interior-mutability-pattern)
    - [Combining `Rc` with `RefCell` to Get Multiple Owners of Mutable Data](#combining-rc-with-refcell-to-get-multiple-owners-of-mutable-data)
    - [Panicking when breaking borrowing rules with `borrow_mut()`](#panicking-when-breaking-borrowing-rules-with-borrow_mut)
  - [Reference Cycles and Memory Leaks](#reference-cycles-and-memory-leaks)
    - [`Weak` Smart Pointer](#weak-smart-pointer)
    - [Rc smart pointer: `strong_count()` and `weak_count()` methods](#rc-smart-pointer-strong_count-and-weak_count-methods)
- [Concurrency in Rust](#concurrency-in-rust)
  - [Using Threads](#using-threads)
  - [Types of Threads](#types-of-threads)
  - [Creating New Threads in Rust](#creating-new-threads-in-rust)
    - [Join Handles](#join-handles)
    - [Using `move` Closures with Threads](#using-move-closures-with-threads)
  - [Message Passing](#message-passing)
    - [Channels](#channels)
    - [Creating Channels in Rust](#creating-channels-in-rust)
    - [Channels and Owner Transference](#channels-and-owner-transference)
    - [Sending Multiple Messages](#sending-multiple-messages)
    - [Creating Multiple Producers](#creating-multiple-producers)
  - [Sharing State](#sharing-state)
    - [The API of `Mutex`](#the-api-of-mutex)
    - [Using a Mutex in Rust](#using-a-mutex-in-rust)
    - [`Mutex` Interior Mutability with `Arc`](#mutex-interior-mutability-with-arc)
- [Object Oriented Programming in Rust](#object-oriented-programming-in-rust)
  - [1. **<ins>Objects</ins>**](#1-objects)
  - [2. **<ins>Encapsulation</ins>**](#2-encapsulation)
  - [3. **<ins>Inheritance</ins>**](#3-inheritance)
- [Trait Objects in Rust](#trait-objects-in-rust)
  - [Static vs. Dynamic Dispatch](#static-vs-dynamic-dispatch)
  - [Object Safety for Trait Objects](#object-safety-for-trait-objects)
- [State Design Pattern in Rust](#state-design-pattern-in-rust)
  - [Extensions to the State Pattern](#extensions-to-the-state-pattern)
    - [Add a method called `reject()` that takes a post that’s `PendingReview` and return in to `Draft`](#add-a-method-called-reject-that-takes-a-post-thats-pendingreview-and-return-in-to-draft)
    - [Require two approvals before a post is published](#require-two-approvals-before-a-post-is-published)
    - [Make it so that you can only add text to a post when it’s in `Draft` state](#make-it-so-that-you-can-only-add-text-to-a-post-when-its-in-draft-state)
  - [Downsides of the State Design Pattern:](#downsides-of-the-state-design-pattern)
  - [Encoding States and Behaviors as Types (MUCH BETTER !!!)](#encoding-states-and-behaviors-as-types-much-better)
- [Patterns](#patterns)
  - [Places where Patterns can be Used](#places-where-patterns-can-be-used)
    - [1. Inside the Arms of `match` expressions —](#1-inside-the-arms-of-match-expressions--)
    - [2. Conditional `if let` Expressions —](#2-conditional-if-let-expressions--)
    - [3. `While let` Syntax —](#3-while-let-syntax--)
    - [4. `for` Loops —](#4-for-loops--)
    - [5. `let` Statements —](#5-let-statements--)
    - [6. Function Parameters —](#6-function-parameters--)
  - [Irrefutable and Refutable Patterns](#irrefutable-and-refutable-patterns)
- [Pattern Syntax in Rust](#pattern-syntax-in-rust)
  - [Matching Against Literals:](#matching-against-literals)
  - [Matching Named Variables:](#matching-named-variables)
  - [Matching Multiple Patterns:](#matching-multiple-patterns)
  - [Matching Ranges of Values:](#matching-ranges-of-values)
  - [Patterns that Destructure Values (i.e, break apart values)](#patterns-that-destructure-values-ie-break-apart-values)
  - [Ignoring Values in Patterns:](#ignoring-values-in-patterns)
  - [Match Guards](#match-guards)
  - [`@` Operator](#-operator)
- [Writing Unsafe Rust](#writing-unsafe-rust)
  - [Raw Pointers in Rust](#raw-pointers-in-rust)
    - [Characteristics of Raw Pointers (as compared to references / smart pointers)](#characteristics-of-raw-pointers-as-compared-to-references--smart-pointers)
  - [Calling Unsafe Functions or Methods](#calling-unsafe-functions-or-methods)
  - [Creating a Safe Abstraction Over Unsafe Code](#creating-a-safe-abstraction-over-unsafe-code)
  - [Functions that Call External Code](#functions-that-call-external-code)
  - [Accessing or Modifying Mutable Static Variables](#accessing-or-modifying-mutable-static-variables)
  - [Implementing an Unsafe Trait](#implementing-an-unsafe-trait)
  - [Accessing Fields of a Union](#accessing-fields-of-a-union)
  - [Unsafe Rust TAKEWAY](#unsafe-rust-takeaway)
- [Advanced Traits in Rust](#advanced-traits-in-rust)
  - [Associated Types](#associated-types)
    - [Difference between Associated Types and Generics](#difference-between-associated-types-and-generics)
    - [When to Use Associated Types (One Trait Implementation Per Type) - IMPORTANT!!!!](#when-to-use-associated-types-one-trait-implementation-per-type---important)
    - [When to Use Generics (Multiple Trait Implementations Per Type) - IMPORTANT!!!!](#when-to-use-generics-multiple-trait-implementations-per-type---important)
  - [Default Generic Type Parameters and Operator Overloading](#default-generic-type-parameters-and-operator-overloading)
  - [Calling Methods with the Same Name](#calling-methods-with-the-same-name)
  - [Supertraits](#supertraits)
  - [Newtype Pattern](#newtype-pattern)
- [Advanced Types in Rust](#advanced-types-in-rust)
  - [Type Aliases](#type-aliases)
  - [Never Type](#never-type)
  - [Dynamically Sized Types and the `Sized` Trait](#dynamically-sized-types-and-the-sized-trait)
    - [`Sized` Trait](#sized-trait)
- [Advanced Functions and Closures](#advanced-functions-and-closures)
  - [Function Pointers](#function-pointers)
  - [Returning Closures from Functions](#returning-closures-from-functions)
- [Macros in Rust](#macros-in-rust)
  - [Macros vs. Functions](#macros-vs-functions)
  - [Declarative Macros](#declarative-macros)
  - [Procedural Macros](#procedural-macros)
    - [Creating our own Custom Derive Macro](#creating-our-own-custom-derive-macro)
    - [Attribute-like Macros](#attribute-like-macros)
    - [Function-like Macros:](#function-like-macros)

# Cargo
**cargo** = build system, package manager, important for managing dependencies (this is a pain point with other low-level programming languages so it is really nice that rust has it built in).

- **TO compile a project, installs dependencies and necessary things for the dependency:** `cargo build`. When you add dependencies, like in the below example, you have to run `cargo build`...

    [package]
    name = "guessing_game"
    version = "0.1.0"
    edition = "2024"

    [dependencies]
    rand = "0.5.5"  // added this dependency

- **TO make new project**: `cargo new {project_name}`

- **TO check code for errors without producing an executable:** `cargo check`

- **TO compile (if necessary) and run project:** `cargo run`

---

# Guessing Game

```rust
fn main() {
    println!("Guess the number!");

    let secret_number = rand::thread_rng().gen_range(1, 101);

    println!("The secret number is {}", secret_number);

    loop{
        println!("Please enter a number: ");

        // In rust, variables are immutable by default. 'mut' makes it mutable.
        //
        // new() returns an empty string we can use.
        //
        let mut guess = String::new();

        io::stdin()
            // No named parameters in rust so type in value then "param_name:" shows up.
            //

            // read_line takes in the user's input and appends it to the specified buffer.
            // We specify the buffer to be guess (which is initialized to '').
            // Specify the buffer as a mutable reference (here, to the guess string), so
            // it takes a reference to the guess string and modifies it without taking
            // ownership of it. Returns a result type that either returns 'Ok' holding
            // the return value (i.e., user input) or 'Err' holding an error object.
            //
            .read_line(&mut guess)

            // If an error is returned, probably a system error. If Ok is returned, then expect
            // returns the value stored in Ok. Otherwise panic with an error message.
            .expect("Failed to read line");

        // Convert user's input from String to unsigned 32-bit int
        // let guess: u32 = guess.trim().parse().expect("Please type a number as your guess");

        // Smarter way to convert user's input from String to unsigned 32-bit int
        // that also handles invalid input:
        //
        // let guess: u32 = ... - declares a variable of type u32
        //
        // guess.trim().parse() - takes string guess, removes whitespace, parse to #.
        //
        // parse() returns a Result enum, which is either:
        //      Ok(value) if parsing succeeded
        //      Err(error) if parsing failed
        //
        // match allows us to handle different cases based on the result:
        //     If parsing is successful (Ok(num)), it assigns the parsed number to guess
        //
        //     If parsing fails (Err(_)), the underscore means "ignore the specific error" 
        //          and continue skips to the next iteration of a loop
        //
        let guess: u32 = match guess.trim().parse() {
            Ok(val) => val, 
            Err(_) => continue,
        };

        println!("You guessed: {}", guess);

        match guess.cmp(&secret_number) {
            Ordering::Less => println!("{}", "Your guess was too small!".red()),
            Ordering::Greater => println!("{}", "Your guess was too large!".red()),
            Ordering::Equal => {
                println!("{}", "Your guess was correct!".green());
                break; // break the loop if they guess the number correctly
            }
        }
    }

}

```

---

# Variables

- **Variables in Rust are immutable by default**. You have to specify "mut" to make mutable.

```Rust
let mut x = 5;    // make `x` mutable with `mut`

println!("This is the value of my variable: {}", x);

x = 6;     // we can reassign `x` bc we marked it as mutable
println!("This is the new value of my variable after reassignment: {}", x);
```

## Constants
- Compared to immutable variables, **constants can't be made mutable with "mut"**.
- Define constants with all upper case and underscores for spaces
- Also, they have to be type annotated, like the 'u32' specified below.

```Rust
const SUBSCRIBER_COUNT: u32 = 1000;
```
- NOTE: **Constants can ONLY be set to constant expressions**, e.g., can't be set to return value of function or any value that's computed at runtime.

# Data Types

## Scalar Data Types

### Integers
- **i32** = signed 32-bit integer (signed = can be positive or negative)
- **u32** = unsigned 32-bit integer (unsigned = can only be positive)
```Rust
let a = 98332;
let b = 98_332;    // '_' is a visual separator, like a comma, so `b` is same as `a`
println!("My value: {}", b);

let f: u8 = 256; // this value is to big for u8 --> get error about overflow
```

### Floating-point Numbers
```Rust
let f = 5.0;

let sum = 5 + 10;
let difference = 98.3 - 4.2;
let product = 4 * 30;
let quotient = 9.3 / 2.9;
let remainder = 99 / 5;
```

### Booleans
```Rust
let t = true;
let f = false;
```

### Character (use single quotes)
```Rust
let c = 'k';
```


## Compound Data Types

### Tuple (0-indexed)
```Rust
let tup = ("kirin", 23);
let (name, age) = tup;     // destructing to access tuple values
let name = tup.0;          // dot notation to access tuple values
let age = tup.1;
```

### Array (0-indexed, fixed length)
```Rust
let error_codes = [200, 404, 500];
let not_found = error_codes[1];     // 404

let byte = [0; 8];     // create an array with 8 values all set to 0
```

---

# Functions
- The **naming convention** for functions in Rust is **all lowercase and underscores for spaces**.
- **Have to specify return type**, e.g., "-> i32".

```Rust
fn my_function(name: &str, age: i32, in_x_years: i32) -> i32{
    println!("{} is {} years old!", name, age);

    // By default, the last line in a function is returned and
    // doesn't require a semicolon. So, can replace the below...
    // let sum = age + in_x_years;
    // return sum
    age + in_x_years
}

fn main() {
    // Call the function in `main`
    let sum = my_function("Kirin", 23, 5);

    println!("In five years, he will be {}", sum)
}
```

---

# Control Flow

## If statements

- **Conditions** in the if statement must **explicitly** be **booleans**

```Rust
let number = 5;

// conditions in the if statement must explicitly be booleans
if number < 10 {
    println!("number is less than 10");
} else if number > 10 {
    println!("number is greater than 10");
} else {
    println!("number is equal to 10")
}
```

## Loops

### `loop`

- execute the code in the loop over and over again until we call 'break'

```Rust
loop {
    println!("again!");
    break;
}
```

- You can use `loop` to return a value...

```Rust
let mut counter = 0;
let result = loop {
    counter += 1;
    if counter == 10 {
        break counter;    // This returns `counter` when the loop breaks.
                          // Value is stored in `result`.
    }
};
println!("{}", result)
```

### `while`
```Rust
let mut number = 3;
while number != 0 {
    println!("{}", number);
    number -= 1;
}
println!("LIFTOFF!!!")
```

### `for`
```Rust
let a = [10, 20, 30, 40, 50];
for element in a.iter() {
    println!("{}", element);
}

// Just like Python range(), `..` doesn't include the upper bound unless you use `..=`
for number in 1..4 {        
    println!{"{}", number};
}
```

## Comments

- Line comment:
```Rust
// Line comment
```

- Block comment:
```Rust
/*
	Block comment
*/
```

---

# Memory in Rust

## Pros and Cons of Different Ways of Handling Memory

<img width="503" alt="Image" src="https://github.com/user-attachments/assets/6851b889-f267-4c03-b8cd-1bdeb258a09f" />

## Stack and Heap
Rust is a systems programming language, so it is important to understand how our memory is laid out during runtime. 
- Rust makes certain decisions depending on whether our memory is stored on the stack or on the heap
- During runtime, our program has access to both the stack and the heap

### The Stack
- **Fixed size** **(can’t grow or shrink during runtime)**.
- Stores stack frames, which are created for every function that executes. 
- The stack frames store the local variables of the function being executed. 
- **The size of a stack frame is calculated at compile time, so the variables inside a stack frame must have a known, fixed size.**
- Variables inside of a stack frame only live as long as the stack frame lives.  

### The Heap
- The heap is less organized: **can grow or shrink at runtime**, the **data stored** in the heap **can be dynamic in size**, can be large amounts of data, and **we control the lifetime of the data**.

### Stack vs. Heap
- **Pushing to the stack is faster than allocating memory on the heap**, because the heap has to spend time looking for a place to store the new data.
- **Accessing data on the stack is faster than accessing data on the heap**, because with heap you have to follow the pointer in the stack frame. 

### Example
<img width="697" alt="Image" src="https://github.com/user-attachments/assets/fd055671-7f3f-4e69-b306-623f990556a4" />
Looking at the above code, the following happens in order…

1. The function a() is executed first because it comes first. So, we add a stack frame for a() to the stack. a() initializes the variable `x`, which is a string literal (`&str`, fixed size, stored in our binary), and `y` (`i32` - signed 32 bit integer, fixed size). In the stack frame, `x` is a reference to the string literal in our binary and `y` is stored directly in the stack frame because it is fixed size.

2. The function b() is executed (it is called in a). This creates a new stack frame that is added to the top of the stack. b() creates its own variable `x`, which is of type `String`. As a `String`, `x` can be dynamic in size, so can’t store it directly in the stack frame; instead, we ask the heap to allocate memory for `x`. The heap does this and passes back a pointer which is what we store in the stack frame. 

## Ownership Rules -- 3 Rules in Rust
1. **Each value in Rust has a variable that’s called its owner.**

2. **There can only be one owner at a time for a specific value (i.e., a value can’t have two owners at the same time).**
    - This rule ensures memory safety by preventing multiple concurrent mutable accesses.
    - Note on Shared Ownership: Types like **Rc<T>** (Reference Counter) and **Arc<T>** (Atomic Reference Counter) **allow multiple references to share ownership of a value.** The value is only dropped when the last Rc or Arc smart pointer goes out of scope. While multiple Rc/Arc pointers exist, they collectively manage the single underlying value.

3. **When the owner goes out of scope, the value will be dropped.**


<ins>Examples with a scope</ins> (we define a new scope here using curly brackets):
- Ex 1:
```Rust
{  // `s` is not valid here, it’s not yet declared

    let s = "hello"; 	// `s` is valid from this point forward.
			// `s` is a string literal stored directly in the binary, fixed size.

    // do stuff with `s`

}  // this scope is now over, and `s` is no longer valid
```

- Ex 2:
```Rust
{  // s is not valid here, it’s not yet declared

    let s = String::from("hello"); 	// `s` is valid from this point forward.
				    	// `s` is `String` type, dynamic in size, can be mutated, so it is automatically stored on the heap.
					// Rust automatically allocates memory on the heap for the `String`, and when the scope ends, Rust
					// drops the value and automatically deallocates memory on the heap.

    // do stuff with `s`

}  // this scope is now over, and `s` is no longer valid
```

## Copy, Move, Clone

- **Copy:** Simple types stored on the stack like integers, booleans, and characters implement the `Copy` trait which allows these types to be copied by default instead of moved.

```Rust
let x = 5;
let y = x; 	// Copy
```

- **Move:** In the below, Rust invalidates `s1` (called a "move"). Cloning s1 would be way too memory expensive (would create a new String on the heap). A shallow copy not as memory safe. Rust defaults to "move" unless `Copy` trait is implemented.

```Rust
let s1 = String::from("hello");
let s2 = s1; 	// Move (not shallow copy), invalidates s1
```

- **Clone:** More expensive, Rust defaults to "move".

```Rust
let s1 = String::from("hello");
let s2 = s1.clone(); 	// Clone
```

<ins>Example:</ins> Strings vs. Integers (Move vs. Copy)
```Rust
// Define a vector with two `String` types, "Kirin" and "Godhwani"
let vec_str = vec![String::from("Kirin"), String::from("Godhwani")];

// If we don't use `&` to take a reference, then the below errors: "cannot move out of index of `Vec<String>` ".
// A move occurs because the value is a `String` type, which does not implement the `Copy` trait.
let temp = &vec_str[0];		// HAVE to take a reference
```

However, we do not need to take a reference `&` when dealing with a vector of integers bc integers implement the `Copy` trait.

```Rust
// vector with two numbers, 0 and 1
let vec_num = vec![0, 1];

//  works without &, bc integers copy by default, they exist on the stack
let temp = vec_num[0];

println!("{}", temp);
println!("{:?}", vec_num);
```

---

# References and Borrowing

## Borrowing

- **Borrowing** — passing in references as function parameters. This is because we borrow the value and don’t actually take ownership of it. <ins>NOTE:</ins> references are immutable by default.

```Rust
fn main() {
    let s1 = String::from("hello");

    // We pass a reference to `s1` into calculate_length().
    let len = calculate_length(&s1);

    // In calculate_length() below, the `s` parameter is a reference to a string and references don't take
    // ownership of the underlying value, so `s1` keeps ownership in main and we can print it. 
    // i.e., calculate_length() borrows a reference to the data owned by `s1`.
    println!("The length of '{}' is {}.", s1, len);
}

fn calculate_length(s: &String) -> usize {
    let length = s.len(); // len() returns the length of a String
    length
}
```

## Rules of References, Reference Rules

1. **At any given time, you can either have one mutable reference OR any number of immutable references.** SO, you can’t have a mutable reference to a variable if an immutable reference already exists for it.

2. **References must always be valid** (i.e., the data they point to must be valid).

3. <ins>NOTE:</ins> **the scope of a reference starts when it is first introduced and ends when it is used for the last time.** As a result, in ex 5 below, we can declare a mutable reference to s after the println!() statement because the scopes of r1 and r2 end at this line (since it is the last time they are used.
```Rust
let mut s = String::from("hello");

let r1 = &s;
let r2 = &s;

println!("{}, {}", r1, r2);	// scopes of `r1` and `r2` end at this line (since it is the last time they are used.

let r3 = &mut s;	// can declare a mutable reference to `s` since no other references to `s` exist
```

### Mutable References
- References are immutable by default. **To modify the value without taking ownership of it**, we **use mutable references** as specified by **`&mut`**.

```Rust
fn main() {
    // make s1 a mutable variable
    let mut s1 = String::from("hello");

    // pass a mutable reference into change()
    change(&mut s1);
}

// With `&mut`, change() can mutate the value of the s1 string without taking ownership
// of the underlying value. 
fn change(some_string: &mut String) {
    some_string.push_str(", world");
}
```
- <ins>RESTRICTION 1 OF MUTABLE REFERENCES</ins>: **you can only have ONE mutable reference to a particular piece of data in a particular scope**. Prevents data races at compile time (data race = two pointers pointing to the same piece of data, one pointer is used to write to the data, no mechanism to synchronize data access between the pointers, e.g., one pointer will try to read the data in the middle of the other pointer writing to the data). To fix the below, make both references immutable (`&s`).

<img width="619" alt="Image" src="https://github.com/user-attachments/assets/5cfb5b31-3e63-4513-a731-2b43f50ad5a0" />

<br> - <ins>RESTRICTION 2 OF MUTABLE REFERENCES</ins>: **you can’t have a mutable reference to a variable if an immutable reference already exists for it.** This is because immutable references don’t expect the underlying value to change, which is problematic if you have a mutable reference. BUT, you can have multiple immutable references to the same variable, because the underlying data is not going to change.

<img width="531" alt="Image" src="https://github.com/user-attachments/assets/48bf94d4-42f3-434a-a361-9d2b09ac8076" />

### Dangling References

- References that **point to invalid data**.
```Rust
fn main() {
    let reference_to_nothing = dangle();
}

// dangle() defines a variable `s`, which is set to a string, and it returns a reference to `s`
// `s` is defined within the scope of the dangle() function, so when the function finishes
// executing, Rust drops `s` (i.e., deallocates it from the heap). Thus, the reference
// to `s` points to invalid memory. Rust prevents this as shown in the screenshow below...
fn dangle() -> &String {
    let s = String::from("hello");
    &s
}
```
“This function’s return type contains a borrowed value, but there is no value for it to be borrowed from”
<img width="711" alt="Image" src="https://github.com/user-attachments/assets/b2654965-7f5e-445b-8cb3-f9e9dc5b5439" />

## Slices

- Let you **reference a contiguous sequence of elements within a collection** instead of referencing the entire collection.
- **Do not take ownership of the underlying data**.

```Rust
let mut s = String::from("hello world");
let hello = &s[0..5];      // since 0 is start of string, can do &s[..5]
let world = &s[6..11];     // since 11 is end of string, can do &s[6..]
let all = &s[0..11];       // can do &s[..]
```

- <ins> Example 1: </ins> first_word() takes in the string slice `s2` (note that string literals are string slices, string literals are stored directly in the binary so s2 is a string slice to that location in the binary).

```Rust
fn main() {
    let s2 = "hello world";

    let word = first_word(s2);  // this would work even if s2 is a String bc it would be
				// automatically coerced into a string slice
}

// Returns a string slice. If the index of the first word is found, returns a slice containing
// the first word. If reaches the end of the input string without returning, then returns
// a slice containing the whole string (bc the whole string would be 1 word in this case). 
//
// Because first_word() accepts a string slice (&str), it borrows a reference to the
// data owned by s2. Therefore, the s parameter in first_word() does not take 
// ownership of the underlying value owned by s2, so the s2 variable in main() keeps
// ownership.
fn first_word(s: &str) -> &str {
    let bytes = s.as_bytes();

    for (i, &item) in bytes.iter().enumerate() {
        if item == b' ' {
            return &s[0..i];
        }
    }
    &s[..]
}
```

- <ins> Example 2: </ins> Slices on different types of collections.

```Rust
let a = [1, 2, 3, 4, 5];
let slice = &a[0..2];
```

---

# Structs
- Structs allow you to group related data together
- Enums and structs are the building blocks for creating new types in rust

## Attributes of a Struct
- Like a tuple, **Structs allows us to group related data of different types together**, but we get the **benefit of naming our structure and the data inside** the structure, so we can **reference data by name instead of index**.

```Rust
struct User {
    // Attributes of the struct
    username: String,
    email: String,
    sign_in_count: u64,
    active: bool,
}

fn main() {

    // Define a mutable instance of the `User` struct
    let mut user1 = User {
        email: String::from("kiringodhwani@gmail.com"),
         username: String::from("kirincg"),
         active: true,
         sign_in_count: 1
    };

    // Can get specific values from struct using dot notation
    let name = user1.username;

    // Can modify specific values in our struct using dot notation
    // NOTE: Must make sure to make the whole object mutable, can't just do a single attribute.
    user1.username = String::from("valgodhwani");

    // Can use functions to define new instances of Struct
    let user2 = build_user(
        String::from("kaig@gmail.com"), 
        String::from("kaig13"));
    
    // We can create new instances of a Struct using existing instances
    // In the below, we give `user3` a specific email address and username, 
    // and for the remaining attributes (active, sign_in_count) takes the
    // same values as `user2`. 
    let user3 = User {
        email: String::from("sgodhwani7@gmail.com"),
        username: String::from("sgod"),
        ..user2 // for the remaining fields, give us what user2 has
    };

}

// Function to create a new instance of the `User` struct.
fn build_user(email: String, username: String) -> User {
    User {
        email: email,
        username: username,
        active: true,
        sign_in_count: 1,
    }
}
```

## Tuple Structs (anonymous structs)

- We can create Structs without named fields.

- Tuple structs are useful when you want your entire tuple to have a name and be of different type then other tuples...

```Rust
// In the below, Color and Point have the same field/attribute types, which are three signed 32 bit integers.
// But, they are of different type: one is Color and one is Point. As a result, if a function expects a tuple
// struct of type Point, you cannot pass it Color.
struct Color(i32, i32, i32);
struct Point(i32, i32, i32);
```

## Example to Show the Value of Structs

**Code Before Using Structs:** works, but could be improved in terms of readability. Specifically, we are calculating the area of one rectangle, so the width and height are related; however, our program does not express that these two variables are related.
```Rust
fn main() {
    let width1 = 30;
    let height1 = 50;

    println!(
        "The area of the rectangle is {} square pixels.",
        area(width1, height1)
    );
}

fn area(width: u32, height:u32) -> u32 {
    width * height
}
```

**Improvement without Structs:** Group the weight and height variables together using tuples. This is better, but it is not clear what the fields in the tuple represent, because not named. Is the first variable the width or the height? 
```Rust
fn main() {
    let rect = (30, 50);

    println!(
        "The area of the rectangle is {} square pixels.",
        area(rect)
    );
}

fn area(dimensions: (u32, u32)) -> u32 {
    dimensions.0 * dimensions.1
}
```

**Major Improvement with Structs:** 
```Rust
struct Rectangle {
    width: u32,
    height: u32
}

fn main() {
    let rect = Rectangle {
        width: 30,
        height: 50,
    };

    println!(
        "The area of the rectangle is {} square pixels.",
        area(&rect)
    );
}

// Pass in a reference to the rectangle, because we don't want the function to take ownership of it.
fn area(rect: &Rectangle) -> u32 {
    rect.width * rect.height
}
```

## Derived Traits

**What if we want to print our Rectangle?? Our Rectangle struct does not implement the Display trait.** The Display trait specifies how something should be printed. Primitive types like integers implement this Display trait by default, since there is only one way to print an integer. But, for custom types like our structure, we have to implement it ourselves. 

<img width="583" alt="Image" src="https://github.com/user-attachments/assets/a0dd0851-987d-4dce-aa35-1c65f93c60fe" />

**SOLUTION:** 
```Rust
println!("rect: {:?}", rect);	// use the {:?}
```

<br>**New Error:** Now we see that our **Rectangle struct doesn’t implement the Debug trait**, which allows us to print out information useful for developers.

<img width="686" alt="Image" src="https://github.com/user-attachments/assets/d79412b6-756a-440e-b3d1-2ad4983c5cba" />

**SOLUTION:** use a **derived trait**...
- The hint in the above error tells us to add the `#[derive(Debug)]` text.
- **Debug is a trait** and **adding derive** here **allows the compiler to provide a basic implementation of the Debug trait**.
```Rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32
}
```
With our new modified code...
- `println!("rect: {:?}", rect);` => "rect: Rectangle { width: 30, height: 50 }"
- `println!("rect: {:#?}", rect);` =>  
"rect: Rectangle {  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;width: 30,  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;height: 50,  
}"

## Methods
- In our earlier code, we have related data grouped together under the Rectangle struct. However, our area() function to compute the area of the rectangle is defined separately from the Rectangle struct, even though it is very closely tied to our Rectangle struct. We can improve this by **grouping the area() function with our Rectangle struct by using the method syntax.**
- Methods are similar to functions, except that they are tied to an instance of a struct.
- The first argument in a method is always **self**, which is the instance of the struct that the method is being called on. Usually, you take a reference to self (`&self`). We could also take a mutable reference to self (`&mut self`), or, in rare cases, we could take ownership of the instance (`self`).
- A struct's methods are defined in **implementation blocks** for the struct. Implementation blocks house the functions and methods associated with the struct.

```Rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32
}

// Implementation block for the Rectangle struct
impl Rectangle {
    // Here, self is a reference to our current Rectangle instance.
    fn area(&self) -> u32 {
        self.width * self.height
    }
}

fn main() {
    let rect = Rectangle {
        width: 30,
        height: 50,
    };

    println!("rect: {:#?}", rect);

    println!(
        "The area of the rectangle is {} square pixels.",
        rect.area() 	// CALLING the area() method
    );
}
```
<br>

- <ins>Example:</ins> Method that takes in multiple parameters

```Rust
impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }

    // Method that takes in multiple parameters.
    // The bigger_area_than() method takes in a reference to another rectangle and determines
    // if the current rectangle instance has a bigger area than the passed in rectangle.
    fn bigger_area_than(&self, other_rect: &Rectangle) -> bool {
        let cur_area = self.area();
        let other_area = other_rect.area();
        if cur_area > other_area {
            return true;
        } else {
            return false;
        }
    }
}

fn main() {
    let rect = Rectangle {
        width: 30,
        height: 50,
    };
    let rect1 = Rectangle {
        width: 5,
        height: 10,
    };
    let rect2 = Rectangle {
        width: 100,
        height: 120,
    };
    println!("rect is bigger than rect1? {}", rect.bigger_area_than(&rect1));	// true
    println!("rect is bigger than rect2? {}", rect.bigger_area_than(&rect2));	// false
}
```

## Associated Functions
- Unlike methods, associated functions are **not tied to an instance of our struct** (i.e., **don't take self as a parameter**).

```Rust
impl Rectangle {
    // IMPORTANT: Bc this is an associated function, not a method, we don't get
    // passed in the self argument… 
    fn square(size: u32) -> Rectangle {
        Rectangle {
            width: size,
            height: size,
        }
    }
}

fn main() {
    let rect3 = Rectangle::square(25); // CALLING THE ASSOCIATED FUNCTION
    println!("Square: {:#?}", rect3);
}
```

---

# Enums
- Enums allow us to **enumerate a list of variants**.
- When is it appropriate to use enums over structs?
	- <ins>Example 1:</ins> Consider IP addresses. We can use enums to enumerate all of the variants — there are 2 variants, IPv4 and IPv6. An IP address can only be one of these 2 variants. Given these properties, if we wanted to express IP addresses in code, then using enums would make sense.

```Rust
enum IPAddressKind {
    // We can store data directly inside the enum variant by adding parenthesis after the
    // variant and specifying the type of data we want to store. In this case, we want to
    // store the string for the IP address. By doing this, we are able to group the the version
    // of the IP address with the actual IP address (grouping related data just like with structs).
    IPv6(String),

    IPv4(u8, u8, u8, u8),	// enum variants can store different types of data.
				// This variant stores four 8-bit integers.
}

fn main() {
    // Variants are namespaced under their identifier, so in this case, we use :: to specify each of our variants.
    let four = IPAddressKind::IPv4;
    let six = IPAddressKind::IPv6;

    // Storing the IP address inside the enum variant.
    let local_host = IPAddressKind::IPv4(127, 0, 0, 1);
    let kirin_yah = IPAddressKind::IPv6(String::from("127.0.0.1"));
}

// In main(), variables 'four' and 'six' are both variants of the IPAddressKind type, so we can
// define a function that takes in a parameter of type IPAddressKind (our enum).
fn route(ip_kind: IPAddressKind) {}
```

- <ins>Enum Example 2:</ins> **Enum variants can store a wide variety of types.** The Message enum below has four variants...
	1. The first variant stores no data
	2. The second variant stores an anonymous struct
	3. The third variant stores a single string
	4. The fourth variant stores three integers

^^^We **could define each of these variants as a separate struct; however these structs would all have different types. The benefit of an enum is that all of these variants are grouped under the Message type**...
```Rust
enum Message {
    Quit,
    Move { x : i32, y : i32 },
    Write(String),
    ChangeColor(i32, i32, i32),
}
```

## Enum Methods
- Just like structs, we **can define methods and associated functions on our enum type**. Just like structs, we use **implementation blocks** again.
```Rust
enum Message {
    Quit,
    Move { x : i32, y : i32 },
    Write(String),
    ChangeColor(i32, i32, i32),
}

impl Message {
    fn some_function(&self) {
        println!("Let's get Rusty!");
    }
}

fn main() {
    let kirins_message = Message::Move { x: 5, y: 2002 };
    kirins_message.some_function()
}
```

## Option Enum

Many languages have null values. **Null values represent a useful concept: a value could either exist or it could be null (i.e.,  there is no value)**. The problem with null values is that the type system can’t guarantee that if you use a value, it’s not null…

- **The type system doesn't differentiate between a value that can be null and a value that is guaranteed to exist**. If a variable is declared to be of a certain type (e.g., String, Integer, User), the type system often doesn't inherently know whether that variable might actually hold a null instead of a valid instance of that type.

- **This means you can try to perform operations on a potentially null value as if it were a valid value.** For example, if you have a variable of type String that might be null, you could try to call a method on it like .length() without first checking if it's actually a string.

- **If the variable is indeed null at runtime, this will lead to a "NullPointerException"** (or a similar error depending on the language). These errors often **crash the program or cause unexpected behavior**, and they can be difficult to track down because the type system didn't warn you about the possibility of a null value in the first place.

- **In Rust, there are no null values**. Instead, Rust uses the **<ins>Option</ins> enum** to explicitly represent the possibility of a **value being present (Some(value))** or **absent (None)**. The type system forces you to handle both cases, preventing null pointer exceptions. The Option enum and its variants are **included in program scope by default**. 

```Rust
enum Option<T> {
    Some(T),
    None,
}
```

- **If you have a value that could potentially be null or not exist, then you would wrap it in the Option enum**. This allows the type system to enforce that we handle the None case when a value doesn't exist, and guarantee in the Some case that our value is present.

- <ins>Example 1:</ins>
```Rust
// For some_number, some_string, and some_splice, we don't have to 
// annotate the type because Rust can infer the type from the values
// being passed in.
let some_number = Some(5);
let some_string = Some(String::from("a string"));
let some_splice = Some("a string");

// For the None case, no value is being passed in so we have to 
// annotate the type.
let absent_number: Option<i32> = None;
```

- <ins>Example 2:</ins> You can't add an optional integer to an integer because they are different types.

<img width="628" alt="Image" src="https://github.com/user-attachments/assets/a6c418f8-4edc-41cb-8089-9214eb8f5730" /> 

- ^^^In order to do this addition, we **have to extract our integer out of the Some variant**. In general, **to extract values out of the sum variant, we would write a `match` expression that handles all possible variants**: If the variant is None, then run this set of code. If the variant is Some, then we can safely use the value and run this set of code. Option enum also has very useful methods…
	- **unwrap_or**: In this case, if y (the optional integer) has a value (Some variant), then we’d like to use the value. But if it doesn’t have a value (None variant), we’d like to use a default value. To do this, we can call the unwrap_or method on our y variable.
```Rust
let x = 5;	     // integer
let y = Some(5);     // optional integer

let sum = x + y.unwrap_or(0);   // for unwrap_or(), default value = 0
```

## Match Expression

- The `match` expression allows you to **compare a value against a set of patterns**. These patterns could be literals, variables, wildcards, and many other types.

- The `match` expression is **exhaustive** — have to match all possible cases. This makes it very useful for enums.

<ins>Example 1:</ins>
```Rust
enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter,
}

fn value_in_cents(coin: Coin) -> u8 {
    // match expression on coin, matches all possible cases for all variants of Coin
    match coin {
         Coin::Penny => {
            println!("Lucky penny!");
            1
        },
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter => 25,
    }
}
```

<br>

<ins>Example 2:</ins> The **patterns in the match expression can also bind to values.**
```Rust
// enum representing the state minted on each quarter
#[derive(Debug)]
enum UsState {
    Alabama,
    Alaska,
    Arizona, 
    Arkansas,
    California,
    //...
}

enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter(UsState), 	// Quarter variant stores the UsState
}

fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => {
            println!("Lucky penny!");
            1
        },
        Coin::Nickel => 5,
        Coin::Dime => 10,

        // Match on the Quarter variant, `state` variable here binds to
        // the `UsState` stored inside the Quarter variant.
        Coin::Quarter(state) => {
            println!("State quarter from {:?}!", state);
            25
        },
    }
}

fn main() {
    // Passing in a Quarter that contains the US State "California"
    value_in_cents(Coin::Quarter(UsState::California));
}
```
<br>

**Using a `match` expression with an Option enum...**
```Rust
fn main() {
    let five = Some(5);

    let six = plus_one(five); // returns Some(6)
    let none = plus_one(None); // returns None
}

// Takes in an optional integer (x) and adds 1 to it. Also returns an 
// optional integer.
fn plus_one(x: Option<i32>) -> Option<i32> {
    match x {
        Some(i) => Some(i + 1),      // can't just return i + 1 bc plus_one()
                                     // return value is an optional integer
        None => None,
    }
}
```

- In our above case with the Option enum, we only have two possible variants/values to match. However, there are cases where we may have many different types of values to match. We can use the **underscore** placeholder to match all other patterns besides the ones we explicitly specify. The following `match` expression says to match x. If x matches Some, execute Some(i + 1). Otherwise, **if it’s any other pattern**, execute None.
```Rust
fn plus_one(x: Option<i32>) -> Option<i32> {
    match x {
        Some(i) => Some(i + 1), 
        _ => None,    // if it's any other pattern, return None variant
    }
}
```

### `if let` syntax

- Rare, but you can use the `if let` syntax when you are matching a value and you **only care about one condition / variant**...
```Rust
// Match on some_value. If some_value is exactly 3, then we print 'three'. Otherwise, we do nothing.
// In this case, we only care about one variant, Some(3), so it is verbose to write the entire match expression. 
match some_value {
    Some(3) => println!("three"),
    _ => (),
}

// More succinct way using 'if let'
if let Some(3) = some_value {
    println!("three");
}
```

---

# Rust's Module System
- Rust’s module system starts with a **package**. When you type in `cargo new` you create a new package. 
- A package stores **crates**. A crate could either be a binary crate (code you can execute) or a library crate (code that can be used by other programs). 
- Crates contain **modules**. Modules allow you to organize a chunk of code and control the privacy rules. 
    - E.g., suppose you have a library crate that contains an authentication module. You can make the code inside your authentication module private but expose one public login method. If we want code outside the authentication module to call the public login method, then we have specify a path to the login method. 
- **Workspaces** are meant for very large projects and allow you to store interrelated packages inside the workspace.

## Crates
- **Creating a new package:** `cargo new my-project`
<img width="231" alt="Image" src="https://github.com/user-attachments/assets/57e1cb62-c1b4-4ed4-9acc-f9ebb5493ccf" />

- Packages store crates, we can **define crates inside the Cargo.toml file**. **Even though we don’t have any crates defined in the above screenshot, our package starts with a binary crate (src/main.rs)**. Rust follows the convention that **if you have main.rs defined in your src directory, then a binary crate with the same name as your package will be automatically created and main.rs will be the crate root.**
	- The crate root is the src file that the Rust compiler starts at when building your crate. It also makes up the root module of your crate.

- Similarly, **if lib.rs is defined in the root of your src directory, then Rust will automatically create a library crate with the same name as your package and lib.rs will be the crate root.** THUS, even though we don’t have any crates defined in our Cargo.toml file, our package has two crates following the lib.rs and main.rs convention.

### Rules around Crates:
1. A package **must have at least one crate**
2. A package could have **either 0 library crates or 1 library crate**
3. A package could have **any number of binary crates**. If we wanted more binary crates in our example above, then we would create a folder called bin in the src directory, and each file in this folder would represent another binary crate.
<img width="207" alt="Image" src="https://github.com/user-attachments/assets/9a849043-978b-40a6-8bfb-6a546fb7597b" />

## Modules

- **Create new package with library crate:** `cargo new --lib restaurant`

<img width="210" alt="Image" src="https://github.com/user-attachments/assets/4f95e33f-d7d4-444d-8a45-7f26c8290c55" />

- <ins>Goal:</ins> Create a library that will help run a restaurant. Think about a restaurant as two parts: the front of the house (the area where the customers are) and the back of the house (where the food is being made, where dishes being washed, and where the manager would typically be).

- **Module tree** (for this goal):
	- crate is a module that gets created by default for our crate root (lib.rs)
	- Inside the crate module, we have the front_of_house module, which contains two modules, hosting and serving. Both hosting and serving have functions defined in them.

<img width="217" alt="Image" src="https://github.com/user-attachments/assets/b6f58dc2-043b-4833-8c1c-6528b7104fcb" />

- <ins>Defining this module tree in code...</ins> Structuring our code this way keeps it organized. If in the future, we wanted to add the ability to seat people at a VIP table, we know exactly where to put this option (in serving module). 

```Rust
// Module (mod keyword) called front_of_house
mod front_of_house {
    // front_of_house module contains two other modules: hosting and serving
    mod hosting {
        // hosting module has two functions related to hosting duties
        fn add_to_waitlist() {}

        fn seat_at_table() {}
    }

    mod serving {
        // serving module has three functions related to serving duties
        fn take_order() {}

        fn serve_order() {}

        fn take_payment() {}
    }
}
```
   
- **Modules can contain other modules inside of them, can also contain structs, enums, constants, traits, and so on.**

### Paths and Module Privacy Rules

- If you wanted to reference a file inside your directory tree, then you would need to specify a path to that file. In the same way, if you wanted to reference an item in your module tree, let’s say a function, then you would need to specify a path to that function. 

- By default, **a child module (like `hosting` below) and everything inside of it is private from the perspective of the parent module**. So, in this case, **`front_of_house` can't see `hosting` or anything inside of `hosting`**.

- However, **child modules are able to see anything that's defined in their parent modules**. This system allows us to hide implementation details by default and only expose the functions we need to to the outside world.
  
- In this case, <ins>we want to expose our add_to_waitlist() function. First, we expose the hosting module using the pub keyword</ins>…
```Rust
mod front_of_house {
    // Expose the hosting module using the pub keyword.
    pub mod hosting {
        // Expose the add_to_waitlist() function using the public keyword.
        pub fn add_to_waitlist() {}
    }
}
```
Inside the eat_at_restaurant() function below, we want to call the add_to_waitlist() function To do so, we need to specify the path to that function.
```Rust
pub fn eat_at_restaurant() {
    // Absolute path, starts at root of module tree (crate)
    crate::front_of_house::hosting::add_to_waitlist();

    // Relative path, starts from the current module (eat_at_restaurant() is
    // inside of the crate module, so can start from front_of_house.
    front_of_house::hosting::add_to_waitlist();
}
```

- <ins>Example 2:</ins> **super**
```Rust
// serve_order() function defined in top crate module.
fn serve_order() {}

// back_of_house module with two functions.
mod back_of_house {
    // In fix_incorrect_order(), we are able to call cook_order (since it's
    // defined in the same module), and we can call serve_order() by using
    // the relative path. We specify super, which allows us to reference the
    // parent module (crate).
    fn fix_incorrect_order() {
        cook_order();
        super::serve_order();
    }

    fn cook_order() {}
}
```

## Privacy Rules with Structs and Enums
<ins>Example 1: **Structs**</ins>
```Rust
// back_of_house module contains a struct called Breakfast, which contains two
// attributes (toast and seasonal_fruit) and an associated function called summer()
mod back_of_house {
    // Expose the Breakfast struct with the pub keyword
    pub struct Breakfast {
        pub toast: String, // explicitly mark toast as a public attribute
        seasonal_fruit: String,
    }

    impl Breakfast {
        // Expose the summer() associated function with the pub keyword.
	// summer() takes in a string called toast and creates a new Breakfast object with
	// toast=toast and seasonal_fruit="peaches".
        pub fn summer(toast: &str) -> Breakfast {
            // As an associated function of the `Breakfast` struct, summer() has full access to all of
            // the struct's fields, regardless of their pub or private status.
            Breakfast {
                toast: String::from(toast),
                seasonal_fruit: String::from("peaches"),
            }
        }
    }
}
// Calls the summer() associated function of Breakfast to create a new
// breakfast meal. But, Breakfast struct is private by default and the 
// summer() associated function is also private by default. Mark public above.
pub fn eat_at_restaurant() {
    let mut meal = back_of_house::Breakfast::summer("Rye");

    // In order to create a new Breakfast struct, we have to use the summer()
    // associated function, we can't create a Breakfast struct directly inside
    // eat_at_restaurant() because the Breakfast struct includes a private
    // attribute (seasonal_fruit). THE BELOW ERRORS !!!
    let meal2 = back_of_house::Breakfast {
        toast: String::from("white"),
        seasonal_fruit: String::from("apple"),
    };

    // Reassign the toast attribute in our meal variable. By default, the toast
    // attribute is private, even thought the Breakfast struct is public. 
    // NOTE: Even when the struct is public, by default, the fields within the
    // struct are private. The below only compiles after we make `toast` public.
    meal.toast = String::from("Wheat");
}
```
<br>

<ins>Example 2: **Enums**</ins>
```Rust
// back_of_house module contains Appetizer enum with two variants (Soup, Salad)
mod back_of_house {
    pub enum Appetizer {
        Soup,
        Salad,
    }
}

pub fn eat_at_restaurant() {
    // Create two orders, one of each variant of Appetizer.
    // Appetizer is private by default, have to add pub above. However, we
    // don't have to explicitly make each variant public. By default, if you
    // make an enum public, all of its variants become public as well.
    let order1 = back_of_house::Appetizer::Soup;
    let order2 = back_of_house::Appetizer::Salad;
}
```

## `Use` keyword

- When there are a lot of nested modules, specifying full paths to functions is not pretty. The use keyword allows you to bring a path into scope.

- **Before using `use` keyword...**
```Rust
mod front_of_house {
    pub mod hosting {
        pub fn add_to_waitlist() {}
    }
}
pub fn eat_at_restaurant() {
    // Specifying the full path isn't pretty... 
    front_of_house::hosting::add_to_waitlist();
    front_of_house::hosting::add_to_waitlist();
    front_of_house::hosting::add_to_waitlist();
}
```

- **After using `use` keyword...**
```Rust
// Bring the hosting module into scope
use crate::front_of_house::hosting;  
	// OR "use self::front_of_house::hosting" (relative path)

pub fn eat_at_restaurant() {
    hosting::add_to_waitlist();
    hosting::add_to_waitlist();
    hosting::add_to_waitlist();
}
```

- In the above example, we could have gone further and brought the add_to_waitlist() function into scope. However, **in Rust, the idiomatic way to bring functions into scope is to bring the function’s parent module into scope.** This makes it clear that the add_to_waitlist() function is not a local function, it’s actually defined inside of another module.

- **If you are bringing enums, structs, or other items into scope, it’s idiomatic to specify the full path (i.e., use with entire path to enum/struct/other item so you can just use the enum/struct/other item with no path)**.
	- However, if you have two structs from different modules with the same name, then bring the parents into scope so that the names don’t conflict. <ins>Ex</ins>:
```Rust
use std::fmt;
use std::io;

fn function1() -> fmt::Result {}

fn function2() -> io::Result<()> {}
```

### Re-Exporting
- Suppose that we want something that’s external to this file to also have access to the add_to_waitlist() function in the below. Currently, it would not have access. If we want external code to be able to call the add_to_waitlist() function directly, then we **need to re-export the hosting module**. To do so, we add pub in front of the use statement…
```Rust
mod front_of_house {
    pub mod hosting {
        pub fn add_to_waitlist() {}
    }
}

// We bring the hosting module into scope using the use keyword, and we mark this as
// public so external code could reference hosting as well. 
pub use crate::front_of_house::hosting;
```

### External Dependencies 

- **The use keyword allows us to bring items into scope within our program, and it also allows us to bring in items from external dependencies into scope.** <ins>Example:</ins>

<img width="357" alt="Image" src="https://github.com/user-attachments/assets/a6205b98-6215-4e33-9f3b-af3a020b60cd" />

```Rust
use rand::Rng;	// Bring the Rng trait into scope from the rand external dependency using `use`…
		// Now we can use it to create a random number…

pub fn eat_at_restaurant() {
    let secret_number = rand::thread_rng().gen_range(1, 101);
    //...
}
```

### Nested Paths

- <ins>Example:</ins>
```Rust
use rand::Rng;
use rand::ErrorKind::Transient;
use rand::CryptoRng;
```
—>    `use rand::{Rng, ErrorKind::Transient, CryptoRng};`

```Rust
use std::io;
use std::io::Write;
```
—>    `use std::io::{self, Write};`

### Glob Operator (`*`)
- Say we wanted to bring all of the public items underneath io into scope…

```Rust
use std::io::*;
```

## Modules in Separate Files

1. <ins>BEFORE:</ins> In **src/lib.rs**:

```Rust
mod front_of_house {
    pub mod hosting {
        pub fn add_to_waitlist() {}
    }
}
```
<br>

2. <ins>AFTER 1:</ins> Move the contents of our `front_of_house` module into a different file… So, in **src/front_of_house.rs** we have...

```Rust
pub mod hosting {
    pub fn add_to_waitlist() {}
}
```

In **lib.rs** we now only have...

```Rust
// This line tells Rust to define the front_of_house module here, but get
// the contents of the module from a DIFFERENT FILE with the SAME NAME as
// the module (i.e., src/front_of_house.rs).
mod front_of_house;
```
<br>

3. <ins>AFTER 2:</ins> Move the contents of the `hosting` module into a different file... So, we have...

<img width="201" alt="Image" src="https://github.com/user-attachments/assets/bc128981-b708-4614-9220-06cd16d055d7" />

**src/front_of_house/hosting.rs:**
```Rust
pub fn add_to_waitlist() {}
```

**src/front_of_house.rs:** 
```Rust
pub mod hosting;
```

**src/lib.rs:**
```Rust
mod front_of_house;
```

## SUMMARY:
- We can declare modules in Rust using the **`mod`** keyword.

- We can **define the contents of our module inline if we use curly brackets**.

- But, **if we want the contents of the module to be in a different file**, then we can just **use a semi colon** (mod module_name;) and **put the contents of the module in a file with the same name as the module**.

    - In our example, we declare mode front_of_house; in src/lib.rs and put the contents of the module in a file called src/front_of_house.rs.

- Similarly, we **can declare child modules and have their content live in a different file**. But, for child modules, we **need to have the corresponding file live in a directory with the same name as the parent module**.

    - In our example, the content of the child module (hosting) is stored in src/front_of_house/hosting.rs. This is because the parent module of hosting is called front_of_house, so hosting.rs must live in a directory called front_of_house.
 
---

# Common Collections in Rust

- Collections **allow you to store multiple values**.

- **Unlike arrays or tuples, collections are allocated on the heap**, meaning the **size of the collection could grow or shrink as needed**.

## Vectors
- **Arrays that can grow or shrink in size.**
- **Only store one type of data.**
- **Stored on the heap**, so just like any other type stored on the heap, will be dropped when they go out of scope. All of the values stored inside of the vector will also be dropped. 

### Initializing Vectors
1. Initialize empty Vector of unsigned 32-bit integers, push 3 values to it
```Rust
let mut v: Vec<i32> = Vec::new();    // make mutable bc we want to change it (add / remove values)
v.push(1);
v.push(2);
v.push(3);
```

2. Initialize vector with three unsigned 32-bit integers (1, 2, 3)
```Rust
let v2 = vec![1, 2, 3];
```

### Accessing Values in Vectors

```Rust
let v = vec![1, 2, 3, 4, 5];
```

1. **Directly reference an index in the vector.**

```Rust
let third_value = &v[2];	// THIS WOULD GET 3
```

- ^^^^^**PROBLEM WITH DIRECTLY REFERENCING AN INDEX**: **If we use an invalid index (e.g., index 20 for our vector), then we get a <ins>runtime</ins> error**. If this were an array and we used an invalid index, then we’d get a compile time error, so the program wouldn’t even run until we fixed the error. This is because arrays are fixed size (so we know array size at compile time), but with a vector, we don’t know the size at compile time (stored on the heap so could be of variable size). Thus, if you directly reference an element in a vector, then your program can crash at runtime if an invalid index is used. Solution (if don’t want program to crash if invalid index is used and instead want to handle that case gracefully)…

2. **The Get Method:** Returns an **Option** enum — Some(value) or None. **Use `match`** expression to handle both cases.

```Rust
match v.get(2) {
    Some(third_elem) => println!("The third element is {}", third_elem),
    None => println!("There is no third element"),
}
```


<ins>NOTE:</ins> **When we access elements in a vector, we are getting a reference to that element.** From our rules about references, you can’t have an immutable reference and a mutable reference to the same thing at the same time. The following code **ERRORS**...

```Rust
let mut v = vec![1, 2, 3, 4, 5];
let third_value = &v[2];
v.push(6);	// This borrows `v` as mutable, which is problematic since we took
		// an immutable reference in the previous line.
println!("The third element is {}", third_value);
```
<img width="516" alt="Image" src="https://github.com/user-attachments/assets/d5fe2415-75fb-4524-a453-1e48001e8f62" />
  
^^^^In our example, we take an **immutable reference** to a value in the vector when we do let **`third_value = &v[2]`**. Afterwards, we take a **mutable reference** to push a new element onto the vector **`v.push(6)`**. And then, we **use the immutable reference** that we created **in `println!("The third element is {}", third_value)`**. This is a problem, because when we take an immutable reference to something, we expect the underlying value to not change, but if we have a mutable reference to the same thing, then the underlying value could change. With vectors, when we push a new element onto the vector, then we may need to allocate more memory to make room for that new value, and when we do this, we need to move all of the elements in our vector to new memory locations. If this were to happen, then our variable we declared with let third_value = &v[2] would be pointing to something else.

### Iterating Over Elements in a Vector

- **`for in`**: **Loops through all of the elements in the `v` vector and takes an immutable reference to each element**. NOTE: must take some sort of reference to the vector or else the values will be moved.

```Rust
let v = vec![1, 2, 3, 4, 5];
for elem in &v {
	println!("{}", elem);
};
```

- Can also use **`for in`** to take **mutable reference** to each element and then modify the value...

```Rust
let mut v = vec![1, 2, 3, 4, 5];
for elem in &mut v {
	*elem += 50;  // use the dereference operator to get the underlying value and add 50 to it
 };

for elem in &v {
	println!("{}", elem)
 }
```

### Storing Different Types of Data in Vectors

- Vectors are designed to only store one type of data. However, you **can store different types of data in vectors using enum variants**.

- <ins>Example:</ins> We want our vector to represent a row of cells in a spreadsheet. Each cell can store either an integer, floating point number, or string. In order to represent this in a vector, we can **create an enum that represents the cell and variants within the enum for each type of data**. **Each of these variants are all under the same type** (the name of the enum)…

```Rust
enum SpreadsheetCell {
	Int(i32),
	Float(f64),
	Text(String),
}

let row = vec![
	SpreadsheetCell::Int(3),
	SpreadsheetCell::Text(String::from("blue")),
	SpreadsheetCell::Float(10.12),
];

// When you reference a specific element inside of the vector, you have
// to use a match expression to figure out which variant of the enum it is.
// This is because the vector is of type SpreadsheetCell.
match &row[1] {
	SpreadsheetCell::Int(i) => println!("{}", i),
	_ => println!("Not an integer!"),
}
```

## Strings

- **Strings are stored as a collection of UTF-8 encoded bytes** (so in memory, a string is just a collection of 1s and 0s). A program needs to interpret the 1s and 0s and print out the correct characters. This is where encoding comes into play.
-**UTF-8 Encoding:** 
    - Universal Character Set (UCS) (i.e., represents characters from all the well-known languages and also things like emojis). Backwards compatible with ASCII (first 128 symbols of unicode are ASCII characters). 
    - UTF-8: A variable-width character encoding for unicode. Variable-width because each character in UTF-8 could be represented as one byte, two bytes, three bytes, or four bytes. This is very important; in comparison, each character in ASCII is represented by one byte. In UTF-8, each character could be a different size in terms of bytes. The most popular encoding of unicode.
 
### Creating a New String

1. **Creating an empty string**

```Rust
let s1 = String::new();
```

2. **Creating a borrowed string slice / string literal (`&str`) and converting it to an owned string (`String`)**

```Rust
let s2 = "initial contents";
let s3 = s2.to_string();
```

3. **Creating an owned string (String) from a borrowed string slice (&str)**

```Rust
let s4 = String::from("initial contents");
```

### Appending to a String

**Just like a vector, a String can grow or shrink in size.**

```Rust
let mut s = String::from("foo");
```

1. **Append a borrowed string slice to the end of a String (don’t take ownership of string being passed in):**

```Rust
s.push_str("bar");
```

2. **Append a character to the end of a String**

```Rust
s.push('!');
```

At the end of the above two operations, we have "foo" —> “foobar!”  

3. **Combine / append strings using the ‘+’ operator**

```Rust
let s1 = String::from("Hello, ");
let s2 = String::from("world!");
let s3 = s1 + &s2;   // move ownership of s1’s value into s3, then take all the characters in s2 and
		     // append them to s3 without taking ownership of s2’s value. Saves memory 
		     // compared to copying both of them. Bc we move ownership of s1’s value into
		     // s3, we can’t use s1 after we’ve declared s3. 

// If we want to concatenate without taking ownership of s1 or s2…
let s3 = format!("{}{}", s1, s2);
```

### Indexing into a String

- **In Rust, Strings can’t be indexed by an integer.** This is because **Strings are a collection of bytes**.

	- UTF-8, as we explained before, is a variable-width character encoding, and each character in UTF-8 could be represented as one byte, two bytes, three bytes, or four bytes. Therefore, as an example, when we index into a String with an index of 0, we are specifying the first byte in our collection of bytes (the String), but the first character may be two bytes so we would be trying to get half of the first character. This is not what we want.

- **A word is represented in unicode in three different ways: bytes, scalar values** (building blocks in unicode, can represent a full character or parts of a character, what the char type refers to), and **grapheme cluster**s (what we consider a character). **When you index into a string with an integer**, **Rust doesn’t know which of these three** we want to receive.

```Rust
let hello = String::from("Hello");
```

1. **Access the bytes of a string:** the **bytes()** method returns a collection of bytes. In the below, we iterate over every byte and print it out.

```Rust
for b in hello.bytes() {
    println!("{}", b);  // 72 -> 101 -> 108 -> 108 -> 111
};
```

2. **Access the scalar values of a string:** The **chars()** method returns a collection of the string’s scalar values, we iterate over them below.

```Rust
for c in hello.chars() {
    println!("{}", c);	// H -> e -> l -> l -> o
};
```

3. **Access the grapheme clusters of a string:** The ability to iterate over grapheme clusters is not included by default. To iterate over grapheme clusters, we have to import a crate. **In dependencies in Cargo.toml, add unicode-segmentation = “1.7.1”**. Then, bring it into scope…

```Rust
use unicode_segmentation::UnicodeSegmentation;
							
// Call the graphemes() method on our string to get a collection of graphemes.
// Pass in true to get extended grapheme clusters.
for g in hello.graphemes(true) {
    println!("{}", g);	// H -> e -> l -> l -> o
}	
```

## Hashmaps
- Allow you to **store key-value pairs**
- The keys and values can be of any type
- Uses a hashing function to determine how to place the keys and values in memory

### Creating a Hashmap
- To create a new hashmap, we need to bring the hashmap type into scope from the standard library…

```Rust
use std::collections::HashMap;
```

<ins>Ex:</ins> In this example, we are tracking a game where keys = team name and the values = team’s score.

1. **Define the keys.**

```Rust
// Keys
let blue = String::from("Blue"); // team Blue
let yellow = String::from("Yellow"); // team Yellow
```

2. **Create the hashmap** (we name the hashmap “scores”)

```Rust
let mut scores = HashMap::new();
```

3. **Populate the hashmap with key-value pairs using the `insert(key, value)` method**

```Rust
scores.insert(blue, 10);	// “Blue”:10 (team Blue has a score of 10)
scores.insert(yellow, 50);}	// “Yellow”:50 (team Yellow has a score of 50)
```

^^^^<ins>NOTE:</ins> When we use `insert(key, value)`, we are **not passing in the “Blue” and “Yellow” strings by reference**. **Passing in the ‘blue’ and ‘yellow’ variables moves the ownership of the “Blue” and “Yellow” strings into the hashmap**. Therefore, after the insert() calls, the **‘blue’ and ‘yellow’ variables are dropped** and can’t be used. If we don’t want the hashmap to take ownership of the Strings, then we could pass references to the Strings, but this would require the use of lifetimes.

### Accessing Values in a Hashmap

- **Use the get() method and specify a key:** **get() method takes a reference to a key and returns an Optional value (Some(val) or None) that may contain a reference to the value corresponding to the key**. Returns an Option because we can’t guarantee that a value will be returned. For example, if you pass in an invalid key that doesn’t exist in the hashmap, then we want to return None.

```Rust
let team_name = String::from("Blue");	// the key of the value we want
let score = scores.get(&team_name);	// Returns an Optional value — Some(val) or None 
```

To access the value from the Option...
```Rust
let score = scores.get(&team_name).unwrap_or(&0);
```

OR

```Rust
let score = match scores.get(&team_name) {
    Some(val) => val,
    None => &0,
};
```

### Iterating Over the Elements in Hashmap

- Use a **`for in`** loop and **extract out a tuple that contains the key and value.**

```Rust
for (key, value) in &scores {
    println!("{}: {}", key, value);
}
```

### Updating the Hashmap

```Rust
// Create an empty HashMap
let mut scores = HashMap::new();
```

1. **Update a value by overwriting an existing key-value pair**

```Rust
scores.insert(String::from("Blue"), 10);        // Insert the key-value pair (“Blue”, 10) into hashmap
scores.insert(String::from("Blue"), 20);       // Overwrite the “Blue” key with the value 20
```

2. **If we don’t want to overwrite existing values**, use the below code. **`scores.entry(key)`** **gives us an Entry enum that tells us if the key already exists in the hashmap or not (Occupied or Vacant)**. In the below, the key is “Yellow”. Then, we **call the or_insert(val) method on this Entry enum**. What this code does is the following:

	-**If the key “Yellow” does not exist in the hashmap:** A new key-value pair (“Yellow”, val) is inserted into the hashmap.

	-**If the key “Yellow” already exists in the HashMap:** Do nothing, the existing value corresponding to the key “Yellow” remains unchanged.

```Rust
scores.entry(String::from("Yellow")).or_insert(30);	// Inserts the key-value pair (“Yellow”, 30) 
							// bc the key “Yellow” does not exist yet in the hashmap.

scores.entry(String::from("Yellow")).or_insert(40);	// Does nothing bc a key-value pair already
							// exists in the hashmap with key=“Yellow”.
```

- <ins>Updating a value in our hashmap based on an old value</ins>. In this example, we have a string of text and we want to populate a hashmap with (word, count) key-value pairs. The text is "hello world wonderful world”. One example key-value pair would be ("hello" : 1) because the word "hello" appears once in the string. Another example is ("world" : 2) because the word "world" appears twice in the string.

```Rust
let text = "hello world wonderful world";

let mut map = HashMap::new();

// split_whitespace() splits the text into a collection of words, split by spaces
// ["hello", "world", "wonderful", "world”]. We iterate over this collection of words.
//
for word in text.split_whitespace() {  

    // If word does not yet exist as a key in the hashmap, insert (word, 0) into the map.
    // If word already exists as a key in the hashmap, do nothing.
    // or_insert() returns a mutable reference to the key's corresponding value in the hashmap.
    //
    let count = map.entry(word).or_insert(0);

    // Dereference the mutable reference and increment it by 1. 
    *count += 1;
}
```

---

# Error Handling in Rust

## panic! Macro

- **If your program fails in a way that is unrecoverable or you can’t handle the error gracefully**, then you can call the **panic! macro** which will **immediately quit your program and print out an error message**.

- This crashes the program at **runtime**.

```Rust
panic!("crash and burn");
```

- Run with `RUST_BACKTRACE=1` environment variable to display a backtrace… `RUST_BACKTRACE=1 cargo run`

## `Result` Enum

- **For errors that are recoverable, we have the `Result` enum**… similar to the Option enum.

- Very common so brought into scope by default.

- Represents **Success (Ok variant)** or **Failure (Err variant)**

```Rust
pub enum Result<T, E> {
    Ok(T),	// Ok(T) represents the Success case and stores some generic value
    Err(E),	// Err(E) represents the Failure / Error case and stores some generic error value
}
```

- <ins>Example 1:</ins> Opening a file and panicking if we have the Err variant

```Rust
use std::fs::File;

fn main() {
    let f = File::open("hello.txt");

    // Use shadowing to redeclare f, 
    // If opening the file is successful, then the file is returned and stored in `f`
    // Otherwise, panic. 
    // 
    let f = match f {
        Ok(file) => file,
        Err(error) => panic!("Problem opening the file: {:?})", error),
    };
}
```

- <ins>Example 2:</ins> Opening a file, but instead of panicking if open fails, create a new file.

```Rust
use std::fs::File;
use std::io::ErrorKind;    // let’s us match on the type of error we get

fn main() {
    let f = File::open("hello.txt");

    let f = match f {
        // If opening the file is successful, then the file is returned and stored in f
        Ok(file) => file,

        // match on the type of error we get… error.kind() returns an enum representing the kind 
        // error we got
        Err(error) => match error.kind() {    
			
            // Handle the NotFound error case. If the file is not found, then we attempt to create the 
            // file. However, attempting to create a new file can fail, so we match on the result type 
            // returned from File::create(). If File::create() is successful (Ok), then we map the
            // created file to the fc variable and return it so that it is stored in f. If File::create() fails /
            // errors, then panic. 
            // 
            ErrorKind::NotFound => match File::create("hello.txt") { 
                Ok(fc) => fc,	// successful file creation
                Err(e) => panic!("Problem creating the file: {:?}", e),	// failure creating file
            },
			
            // If the error is not NotFound, bind the error to the other_error variable and then panic 
            // about there being a problem opening the file (include other_error in the message)
            //
            other_error => {
                panic!("Problem opening the file: {:?}", other_error)
            },
        }
    };
}
```

- <ins>Example 3:</ins>  It can be hard to read with all the nested match expressions —> use closures

```Rust
let f = File::open("hello.txt").unwrap_or_else(|error| {

    if error.kind() == ErrorKind::NotFound {

        File::create("hello.text").unwrap_or_else(|error| {
            panic!("Problem creating the file: {:?}", error);
        })

    } else {

        panic!("Problem opening the file: {:?}", error);

    }
});
```

### Useful Functions on the `Result` Enum

1. **unwrap()**: in the below example, unwrap() does the same thing as our match expression…
	- **In the success case (Ok)** , it **takes the thing stored in Ok(T)** (Ok(file) in this case) and **returns it**.
 	- **In the Error case, it panics** (panic!). 

<ins>Before</ins>:
```Rust
let f = File::open("hello.txt");
let f = match f {
    Ok(file) => file,
    Err(error) => panic!("Problem opening the file: {:?}", error),
};
```

<ins>After</ins>:
```Rust
let f = File::open("hello.txt").unwrap();
```
<br>

2. **expect()**: Same as unwrap() with the additional feature that it **allows you to specify the error message that gets sent to the panic! macro**.

```Rust
let f = File::open("hello.txt").expect("Failed to open hello.txt");
```

## Error Propagation with the `Result` Enum

- **When you have a function that calls something that may fail, then you want to return that error back to the caller instead of handling it within the function.**

- **This gives more control to the caller who can then decide what to do with the error.** This is called **<ins>error propagation</ins>**.

```Rust
use std::fs::File;
use std::io;
use std::io::Read;

// read_username_from_file() return a Result type (either a String (the username) or an error) 
fn read_username_from_file() -> Result<String, io::Error> {
    let f = File::open("hello.txt");

    // Opening the "hello.txt" file could fail...
    let mut f = match f {

        // If opening the file is successful, then the file is returned and stored in `f`
        Ok(file) => file,

        // If opening the file fails, then return the error to the caller (error propagation)
        Err(e) => return Err(e),
    };

    let mut s = String::new();

    // Calling read_to_string() on our file reads the contents of the file and 
    // stores it within the passed in String. read_to_string() returns a Result type.
    match f.read_to_string(&mut s) {

        // In the success case, return the string (contents of the file are stored in this string)
        Ok(_) => Ok(s),

        // In the error case, return the error to the caller (error propagation)
        Err(e) => Err(e), // specifying return not necessary bc last expression in fxn
    }
}
```

- By doing the error propagation in the above, the code calling the read_username_from_file() function is able to determine how best to handle the different errors.

## The `?` Operator with the `Result` Enum

- `?` does something very similar to the unwrap() or expect() methods.

- We can simplify the code in the previous example using the ? operator…

```Rust
fn read_username_from_file() -> Result<String, io::Error> {

    // If we succeed in opening the file, then the file is returned and stored in `f`.
    //
    // If we fail to open the file, then INSTEAD OF PANICKING, the read_username_from_file() function ends early and returns the error.
    //
    let mut f = File::open("hello.txt")?;

    let mut s = String::new();

    // If read_to_string() succeeds, then the contents of f are read and stored within s.
    //
    // If read_to_string() fails, then read_username_from_file() ends and returns the error. 
    //
    f.read_to_string(&mut s)?;
    Ok(s)	// If we get to this line in the function, then we know read_to_string()
		// succeeded, so we can return `s` (which contains the contents of f).
}
```

^^^We can simplify this code even more by **chaining** method calls...

```Rust
fn read_username_from_file() -> Result<String, io::Error> {
    let mut s = String::new();

    // We have two related method calls: opening the file and reading from the file.
    // Instead of creating an `f` variable when you read in the file, chain the method calls.
    File::open("hello.txt")?.read_to_string(&mut s)?;
    
    Ok(s)
}
```

^^^Technically, we can simplify even more using different built-ins...

```Rust
use std::fs::{self, File};
use std::io;
use std::io::Read;

fn read_username_from_file() -> Result<String, io::Error> {
    fs::read_to_string("hello.text")
}
```

- **NOTE:** The **`?`** operator **can only be used in a function that returns Result or Option.**

	- The main() function is special — it has restriction on what type it can return. It can return a Result type, which allows you to **use the ? operator in main()**…

 ```Rust
use std::error::Error;
use std::fs::File;

fn main() -> Result<(), Box<dyn Error>> {
    let f = File::open("hello.text")?;

    Ok(())
}
```

## `panic!` vs. `Result`
- In general, **the default should be using the Result enum and error propagation**, this **prevents your program from crashing**. Also, error propagation **allows the caller to decide how best to handle the error**.

- **Only use panic! in exceptional circumstances.**
    - These include **circumstances in which recovering from the error is not possible and your program cannot continue** because it’s in a bad state, so you must end the program. 
    - It is also appropriate to use panic! in **example code**. In example code, methods like unwrap() and expect() are used for brevity. Also, in example code, there’s no context for determining how to deal with errors. 
    - You **may** also **use unwrap() and expect() in prototype code**. If you are trying to get something out really quickly to see if it works and you don’t want to deal with error handling. However, if the code is moving past the prototype phase, you can find all the expect() and unwrap() statements and easily introduce error handling. 
    - **unwrap() and expect() can also be used in test code**. This is because in test code, you want your test to fail if something that you expect to succeed actually fails. 
    - You **may want to use unwrap() or expect() when you know a call to a function will succeed**. This allows you to easily get the result from the Option / Result enum. <ins>Example:</ins>

```Rust
use std::net::IpAddr;

fn main() {
    // Bc the String "127.0.0.1" is hardcoded here, we know the parse function will 
    // always succeed and convert it to an IP address. Thus, we can safely call unwrap()
    // without having to worry about the possibility of panicking.
    //
    // However, if the String were dynamic and came from something like user input, then
    // we wouldn’t want to call unwrap() bc may panic, so would want to handle the potential
    // error case.
    //
    let home: IpAddr = "127.0.0.1".parse().unwrap();    
}
```

## Custom Types

- **You can create custom types for validation.**

- <ins>Example:</ins> **In our guessing game, we can create a custom type for the user’s guess that validates that their guess is between 1 and 100.**

```Rust
pub struct Guess {
    value: i32, // store the integer (i.e., the guess)
}

impl Guess {
    // Associated function that takes in a value and validates that it's between 1 and 100.
    // If the value is between 1 and 100, then returns a new instance of the Guess struct with the value.
    pub fn new(value: i32) -> Guess {
        if value < 1 || value > 100 {
            panic!("Guess value must be between 1 and 100, got {}.", value);
        }

        Guess { value } // Same as Guess { value: value }
    }

    // Returns the value stored in the Guess struct.
    // We want this function because we don't want the value field to be manipulated directly (at all).
    pub fn value(&self) -> i32 {
        self.value
    }
}

fn main() { 
    // Defining a new guess 
    let my_guess = Guess::new(42);  // Creates a new Guess instance with the value 42 

    // Attempting to create an invalid guess will cause a panic
    let invalid_guess = Guess::new(150);   // This line would panic at runtime
}
```

^^^Now, our guessing game can use this new Guess type, and **any code dealing with Guess can be confident that the value stored inside of it is between 1 and 100.**

---

# Generics

## Motivation

```Rust
fn main() {
    let number_list: Vec<i32> = vec![34, 50, 25, 100, 65];

    let largest = get_largest(number_list);
    println!("The largest number is {}", largest);
}

fn get_largest(number_list: Vec<i32>) -> i32 {
    let mut largest = number_list[0];
    for number in number_list {
        if number > largest {
            largest = number
        }
    }
    largest
}
```
- In the above code, **the `get_largest()` function is tied to a concrete set of arguments: number_list, which has to be a vector of signed 32-bit integers.**

- **What happens if we want to use our same logic of finding the largest number on a slightly different set of arguments (e.g., the largest character in a vector)?** This will **ERROR** because get_largest expects a Vector of signed 32-bit integers but we are passing it a vector of characters.

- Possible Solution 1 (**BAD**): Duplicate the get_largest() function and change the type of number_list to Vec<char> and change the return type to char. This works, but we want to reduce duplication and only have one get_largest() function.

- <ins>Solution:</ins> **Generics** -- we can **use generics to modify our original get_largest() function to take in both sets of arguments (Vec<i32> and Vec<char>).**

## Defining Generic Types

- Generic types are **specified inside of angle brackets right after the function name**, like **`get_largest<T>`**. This specifies that we have a generic type called T.
  
    - If you have one generic type, you call it `T`.
      
    - To specify **multiple generic types**, use a comma to separate them in the angled brackets (e.g., **`get_largest<T, U>`**).
 
- Once we have our generic type defined, we can use it inside the function. In get_largest() below, we do the following…
  
    - FIRST, we **specify that number_list is a vector of a generic type T (`Vec<T>`) instead of a vector of integers (`Vec<i32>`)**
      
    - SECOND, we **change the return value**. Instead of returning an integer (`i32`), we **return `T`**.
 
- **Using traits:** As explained in the comment in the code below, to allow comparison, `T` can't be of any type; instead, `T` must be a type that can be compared. To enforce this, we use traits... `T: PartialOrd + Copy`. This says that our **type `T` has to be a type that can be ordered and copied** (primitive types like ints and chars). 

```Rust
fn get_largest<T: PartialOrd + Copy>(number_list: Vec<T>) -> T {
    let mut largest = number_list[0];
    for number in number_list {
        // We can't use the '>' operator on our type T because T is generic (i.e., it could be
        // anything, including something that we cannot compare). To fix this, we have to restrict
        // our generic type. Instead of saying T could be of any type, we want to say T could be of 
        // of any type that can be compared. To do this, we use traits, as explained above.
        // 
        if number > largest {
            largest = number
        }
    }
    largest
}

// Now, get_largest() can be used with characters and numbers...
fn main() {
    let number_list: Vec<i32> = vec![34, 50, 25, 100, 65];
    let largest = get_largest(number_list);
    println!("The largest number is {}", largest);

    let char_list: Vec<char> = vec!['y', 'm', 'a', 'q'];
    let largest = get_largest(char_list);
    println!("The largest char is {}", largest);
}
```

## Generics with Structs

- This `Point` struct has two attributes, `x` and `y`, and both are 32-bit integers…
```Rust
struct Point {
    x: i32,
    y: i32,
}

fn main() {
    let pl = Point { x: 5, y: 10, };
}
```

- **Use generics** if we want to allow a Point instance to have floating point numbers instead of integers...

```Rust {
struct Point<T> {
    x: T,
    y: T,
}

fn main() {
    let p1 = Point { x: 5, y: 10, };	// integers

    let p2 = Point { x: 5.0, y:10.0, };	// floating point numbers
}
```

- **In the example above, the `Point` struct says that both `x` and `y` are of type `T`**. So, `x` and `y` are **generic** **but** they have to **have the same type as each other**. To fix this, we can **define multiple generic types so we have another generic type besides `T`**…

```Rust
struct Point<T, U> {
    x: T,	// `x` is of a generic type `T`
    y: U,	// `y` is of another generic type `U`. This could be the same type as
		// type T, or it could be different
}

fn main() {
    let p1 = Point { x: 5, y: 10, };	// `x` and `y` could be the same type

    let p2 = Point { x: 5.0, y:10.0, };

    let p3 = Point { x: 5, y: 10.0, };	// `x` and `y` can now also be different types
}
```

## Generics with Enums

- We can use Generics inside of enum definitions… In fact, **both the Option enum and and Result enum use Generics**…

```Rust
// One generic, T. Used in the Some variant. So, if we get the Some variant, then something is returned, but we
// don’t want to specify the exact type of what that thing is. None case doesn’t return anything.
enum Option<T> {
    Some(T),
    None,
}

// Two generics, T and E.
// T specifies the type of the Ok value being returned, but doesn’t define an exact type of what the value is.
// E specifies the type of the error value in Err variant.
enum Result<T, E> {
    Ok(T),
    Err(E)
}
```

## Generics in Method Definitions

- In the below code, the **first implementation block is available to Point instances of any type**. As a result, the x() method in this implementation block is available to Point instances of any type. HOWEVER, the **second implementation block is only for Point instances where the type is f64**. As a result, the y() method in this implementation block is only available to points where the x and y values are f64.

```Rust
struct Point<T> {
    x: T,
    y: T,
}

// Want our implementation block to use generics, so add <T> or <U> or <S>, etc.
// We can use a different letter than T, like U, because the generic defined here is not tied to
// the generic specified above in our struct definition. 
//
// impl<U> says that we have an implementation block that uses a generic and we're going to call it U.
//
// Point<U> says that this implementation block is for a Point with a type parameter that is set to our generic.
//
impl<U> Point<U> {

    // x() takes a reference to self, which is the point instance we're operating on, and then
    // returns a reference to the `x` field, which is a generic type (so we return a reference to U).
    fn x(&self) -> &U {
        &self.x	
    }
}

// This implementation block is only for Point instances that have a type parameter f64 (64-bit floating point 
// number), and we define a function in it called y() which returns the y-value of the point. 
//
impl Point<f64> {
    fn y(&self) -> f64 {
        self.y
    }
}
```

- <ins>More Complex Example:</ins>

```Rust
// Two generics, T and U.
struct Point<T, U> {
    x: T,	// x is type T
    y: U,	// y is type U, which may be the same type as type T or different
}

// Implementation block with generics T and U. 
// Implementation block for our Point struct (Point<T, U>)
impl<T, U> Point<T, U> {

    // The mixup() method has its own set of generics, V and W. These generics are scoped
    // to the mixup() method.
    //
    // mixup() takes self as the first argument. The second argument, other, is another
    // Point instance, which is going to use the V and W generics defined in mixup<V, W>. We
    // use V and W here instead of T and U, because the 'other' Point potentially has different
    // types than self (the point we're calling the function on).
    // 
    // The return type of mixup() is also a Point instance. The generics are T and W, Point<T,W>.
    // This is because the point instance returned by mixup() takes the x value of self (which has type T)
    // and the y value of other (which has type W).
    //
    fn mixup<V, W>(self, other: Point<V, W>) -> Point<T, W> {
        Point {
            x: self.x,
            y: other.y,
        }
    }
}

fn main() {
    let p1 = Point { x: 5, y: 10.4, };     // Point<i32, f64>
    let p2 = Point { x : "Hello", y: 'c', };    // Point<&str, char>

    let p3 = p1.mixup(p2); // Point<i32, char>

    println!("p3.x = {}, p3.y = {}", p3.x, p3.y) // 5, c
}
```

## Performance Impact of Using Generics

- Generics are great because they allow us to **reduce duplication**: Instead of having to define multiple functions / structs / enums to allow for different types, we can use generics and define one function / structure / enum that serves all of the types we want. Example:

```Rust
enum Option<T> {
    Some(T),
    None,
}
fn main() {
    let integer = Option::Some(5);
    let float = Option::Some(5.0);
}
```

- **This does not incur a performance hit**. This is because, for the above example WLOG, at compile time, Rust turns the Option enum into two Option enums, one for 32-bit integers and one for 64-bit floating point numbers. This is called **monomorphization**.

---

# Traits

- **Traits allow you to define shared behavior across multiple types**.

- <ins>Example:</ins> Say we have a program which aggregates different types of text content. In this example, we have a news article and a tweet. The news article has author, headline, and content. The tweet has a username, content, and two booleans, reply and retweet, that indicate whether the tweet is a reply or a retweet.

```Rust
pub struct NewsArticle {
    pub author: String,
    pub headline: String,
    pub content: String,
}

pub struct Tweet {
    pub username: String,
    pub content: String,
    pub reply: bool,
    pub retweet: bool,
}
```

- We want the ability to summarize a news article and the ability to summarize a tweet… **we can use a <ins>trait</ins> to define this shared behavior between a news article and a tweet**. In this case, the shared behavior is summarization.

- **By shared behavior, we mean <ins>methods</ins>**… **<ins>traits allow us to define a set of methods that are shared across different types.</ins>**

```Rust
pub struct NewsArticle {
    pub author: String,
    pub headline: String,
    pub content: String,
}
// Implement the Summary trait for our NewsArticle type
impl Summary for NewsArticle {
    // For a NewsArticle, summarize() returns a String that contains the headline of the news
    // article and the author.
    fn summarize(&self) -> String {
        format!("{}, by {}", self.headline, self.author)
    }
}

pub struct Tweet {
    pub username: String,
    pub content: String,
    pub reply: bool,
    pub retweet: bool,
}
// Implement the Summary trait for our Tweet type
impl Summary for Tweet {
    // For a Tweet, summarize() returns a String that contains the username and the content of
    // the tweet (bc tweet content <280 characters). 
    fn summarize(&self) -> String {
        format!("{}: {}", self.username, self.content)
    }
}

// use pub to make the trait public
pub trait Summary {

    // Inside the curly brackets, we can define the shared methods under this trait
    //
    // We only specify the method signature, we don't actually have a method body, because we don't want
    // to dictate the implementation. We only want to say that for every type that implements the Summary trait,
    // they should have this summarize() method that returns a String.
    fn summarize(&self) -> String;
}

fn main() {
    let tweet = Tweet {
        username: String::from("@johndoe"),
        content: String::from("Hello World!"),
        reply: false,
        retweet: false,
    };
    let article = NewsArticle {
        author: String::from("John Doe"),
        headline: String::from("The Sky is Falling!"),
        content: String::from("The sky is not actually falling.")
    };
    println!("Tweet summary: {}", tweet.summarize());
    println!("Article summary: {}", article.summarize());
}
```

## Default Implementations

- In our example above, **instead of specifying the summarize() method signature inside of the Summary trait and expecting every type that implements the Summary trait to specify the body of summarize(), we may want a default implementation of summarize()**… 

```Rust
pub trait Summary {
    // To add a default implementation of summarize(), we can simply add a method body.
    //
    // Here we are saying that our Summary trait has a summarize() method and its default implementation
    // is to return this "(Read more...)" string. 
    //
    fn summarize(&self) -> String {
        String::from("(Read more...)")
    }
}
```

- NOTE: as we showed previously, **the NewsArticle and Tweet structs both specify their own custom implementation of summarize(), which overrides the default implementation.** However, **if we remove the custom implementation of summarize() from NewsArticle, like below, then NewsArticle will use this default summarize() implementation...**
  
```Rust
// This line of code is necessary to implement the Summary trait for the NewsArticle type.
// Bc Summary is implemented for NewsArticle, and NewsArticle doesn't override the default summarize() implementation,
// calling summarize() on a NewsArticle instance will call the default implementation.
impl Summary for NewsArticle { }
```

- **Default implementations can call other methods inside our trait definition:**

```Rust
pub struct NewsArticle {
    pub author: String,
    pub headline: String,
    pub content: String,
}
// Implement the Summary trait for our NewsArticle type
impl Summary for NewsArticle {
    // summarize_author() has no default implementation, so we must specify a custom implementation here.
    // Return the author (author field of NewsArticle struct).
    fn summarize_author(&self) -> String {
        format!("{}", self.author)
    }

    // Don't have to specify summarize() because it has a default implementation defined inside
    // the Summary trait block.
}

pub struct Tweet {
    pub username: String,
    pub content: String,
    pub reply: bool,
    pub retweet: bool,
}
// Implement the Summary trait for our Tweet type
impl Summary for Tweet {
    // summarize_author() has no default implementation, so we must specify custom installation here.
    // Return the username because the author of the tweet is the Twitter user.
    fn summarize_author(&self) -> String {
        format!("@{}", self.username)
    }
	
    // custom summarize() implementation that overrides the default implementation.
    fn summarize(&self) -> String {
        format!("{}: {}", self.username, self.content)
    }
}

pub trait Summary {
    // summarize_author() returns the name of the author, has no default implementation.
    fn summarize_author(&self) -> String;

    // summarize() has a default implementation, which uses the summarize_author() method.
    fn summarize(&self) -> String {
        format!("(Read more from {}...)", self.summarize_author())
    }
}

fn main() {
    let tweet = Tweet {
        username: String::from("@johndoe"),
        content: String::from("Hello World!"),
        reply: false,
        retweet: false,
    };
    let article = NewsArticle {
        author: String::from("John Doe"),
        headline: String::from("The Sky is Falling!"),
        content: String::from("The sky is not actually falling.")
    };
    println!("Tweet summary: {}", tweet.summarize());
    println!("Article summary: {}", article.summarize());
}
```

## Trait Bounds

- **Traits as parameters**

- We can **use generics with traits to create trait bounds**, which **allow us to use a generic type that specifies some set of functionality** (instead of using concrete types).

- <ins>Example:</ins>
	- **notify() uses a generic type T**
 	- **<T: Summary>** says that the **generic type T is limited to types that implement the Summary trait.**
  	- Then **use the generic type T in the parameter definition**… (item: &T)
```Rust
pub fn notify<T: Summary>(item: &T) {
    println!("Breaking news! {}", item.summarize());
}
```

- <ins>Example 2:</ins> **Force two parameters to be the same generic type that implements a specific trait**.

```Rust
// With the trait bound syntax, we can make `item1` and `item2` be the exact same type that implements 
// the Summary trait. This is because the generic type `T` is ONE type, and both `item1` and `item2` are type `T`.
pub fn notify<T: Summary>(item1: &T, item2: &T) { {
    //
}
```

- <ins>Example 3:</ins> **Specifying a trait bound with multiple traits**.

```Rust
// The type T has to implement both the Summary and Display traits
pub fn notify<T: Summary + Display>(item1: &T, item2: &T) { {
    //
}
```

- <ins>Example 4:</ins> **Specifying multiple trait bounds using a `where` clause**
  
```Rust
// Generic type T that implements the Display and Clone traits
// Generic type U that implements the Clone and Debug traits
fn some_function<T: Display + Clone, U: Clone + Debug>(t: &T, u: &U) -> i32 {
    //
}

// MORE READABLE with the where clause
fn some_function<T, U>(t: &T, u: &U) -> i32
    where 
        T: Display + Clone,
        U: Clone + Debug,
{
    //
}
```

### Returning Types that Implement Traits

- **See the trait objects section later... command-f**

## Using Trait Bounds to Conditionally Implement Methods

- **We use two implementation blocks in the below (one with trait bounds) to conditionally implement methods**.

- **In the first implementation block**, we **make it so that every Pair instance, regardless of what type T is, has the new() method.**

- However, **in the second implementation block**, we **use trait bounds to restrict to Pair instances where T implements the Display and PartialOrd traits**. As a result, the **cmp_display() method in this second implementation block is only available to Pair instances where T implements the Display and PartialOrd traits**. This is necessary because the cmp_display() method only works when x and y have these two traits implemented.

```Rust
use std::fmt::Display;

// The Pair struct has two fields, x and y. Both take the generic type T.
struct Pair<T> {
    x: T,
    y: T,
}

// This implementation block is on the Pair struct with generic type T (i.e., for any Pair struct).
// Contains new() method that creates a new instance of Pair.
impl<T> Pair<T> {
    fn new(x: T, y: T) -> Self {
        Self { x, y }
    }
}

// This implementation block uses trait bounds to say that T has to implement the Display and
// PartialOrd traits. So this implementation block only applies to Pair instances where the
// type T (i.e., the type of fields x and y) implements the Display and PartialOrd traits.
impl<T: Display + PartialOrd> Pair<T> {
    // The cmp_display() method compares x and y. We can do this because know x and y implement
    // the Display and PartialOrder traits. 
    fn cmp_display(&self) {
        if self.x >= self.y {
            println!("The largest number is x = {}", self.x);
        } else {
            println!("The largest member is y = {}", self.y)
        }
    }
}
```

## Blanket Implementations

- We can implement a trait on a type that implements another trait.

- In the below, we **Implement the ToString trait on any type T that implements the Display trait**...

```Rust
impl<T: Display> ToString for T {
    //
}
```

---

# Lifetimes

- **Dangling References**: references that point to invalid data. Ex:

```Rust
let r;
{
    let x = 5;
    r = &x;

} // When this scope ends, `x` gets dropped. So `r` is pointing to
  // invalid data when print is called below.

println!("r: {}", r);
```

^^^Rust won’t let this code with a dangling reference compile…

<img width="607" alt="Image" src="https://github.com/user-attachments/assets/148e9021-e81e-4111-9775-5a00db39b5cd" />

^^^ Rust knows this at compile time, because of the **Borrow Checker**.

- **Borrow Checker** — Runs at compile time, checks to make sure that all borrowed values (references) are valid.

- **Lifetime of a variable** — **how long the variable lives for**

## Generic Lifetime Annotations

- **Generic Lifetime Annotations** — **Help the borrow checker understand the relationship between the lifetimes of multiple references**, which in turn, **helps the borrow checker identify dangling references**.

- There are situations in which we need to help the compiler using generic lifetime annotations. <ins>In the below example</ins>, how does the Borrow Checker know that ‘result’ in main() is not a dangling reference?

```Rust
fn main() {
    // Define two Strings
    let string1 = String::from("abcd");
    let string2 = String::from("xyz");

    // Call longest() to determine the longer String out of `string1` and `string2`.
    let result = longest(string1.as_str(), string2.as_str());
    println!("The longest string is {}", result);	// How would the borrow checker know that `result` 
							// (when we print it here) is not a dangling 
							// reference? What is the lifetime of `result`?
}

// Takes in two string slices, `x` and `y`. Returns the longest of the two string slices.
fn longest(x: &str, y: &str) -> &str {	// longest() returns a reference here, but we have no idea what the
					// lifetime of this reference is

    // We return either `x` or `y` based on which is longer. But, `x` could have a 
    // different lifetime than `y`… 
    if x.len() > y.len() {
        x
    } else {
        y
    }
}
```
^^^
In the above code…

- PROBLEM 1: **We don’t know if we are returning `x` or `y`, and they could have different lifetimes !**
 
- PROBLEM 2: **We don’t know the exact lifetime of `x` or `y` because they are placeholders in the function. If the function gets called in many places, then `x` and `y` will take many different values and thus have many different lifetimes.**
  
**THE BORROW CHECKER DOESN’T KNOW HOW TO HANDLE THIS AMBIGUITY…**

<img width="732" alt="Image" src="https://github.com/user-attachments/assets/57459e20-f27a-4257-a4b9-76c1dc87b995" />

^^^This error says that `x` and `y` could have different lifetimes, and the borrow checker needs to know which of these lifetimes is being used as the lifetime of the return value. To fix this, we have to use a generic lifetime annotation…

## Writing Generic Lifetime Annotations

- **Generic Lifetime Annotations**: **Describe the relationship between the lifetimes of multiple references and how they relate to each other.**

	- **DO NOT actually change the lifetime of a reference.** Rather, they just explain the relationship between different lifetimes.

 	- Most people just refer to Generic Lifetime Annotations as **Lifetimes**.
 
- **How you specify Generic Lifetime Annotations (lifetimes):**
	- **`&i32`** — a reference
	- **`&’a i32`** — a reference with an **explicit lifetime**
	- **`&’a mut i32`** — a mutable reference with an **explicit lifetime**

- <ins>Fixing the error code with a Generic Lifetime Annotation (Lifetime):</ins> In the below, we **declare a generic lifetime `a`**, then we **annotate `x`, `y`, and the return value with `a`**. This means that there is a relationship between `x`, `y`, and the return value. The relationship is the following: **the lifetime of the return reference will be the same as the smallest lifetime of the arguments (`x` and `y`)**. So, **if `x` has a smaller lifetime than `y`, then the lifetime of the return reference will be the same as `x`, and vice versa.**

```Rust
fn main() {
    let string1 = String::from("abcd");
    let string2 = String::from("xyz");

    let result = longest(string1.as_str(), string2.as_str());
    println!("The longest string is {}", result);
}


// Generic lifetime annotations in angled brackets. Start with an apostrophe followed by the name of the lifetime.
// `x` uses the lifetime - `x: &'a`
// `y` uses the lifetime - `y: &'a`
// the return type uses the same lifetime - `&'a`
//
// Result: the lifetime of the return reference will be the same as the smallest lifetime of the arguments (`x` and `y`).
//
fn longest<'a>(x: &'a str, y: &'a str) -> &'a str {
    if x.len() > y.len() {
        x
    } else {
        y
    }
}
```
^^^So, in the above, <ins>how does the borrow checker know that result is not a dangling reference?</ins> **By adding our generic lifetime annotations** in the above, we **told the borrow checker that whatever gets returned from longest() and saved in result will have the lifetime that is equal to the smallest lifetime being passed into longest()**. Then, **all the borrow checker has to do is determine the smallest lifetime being passed in: `string1`'s lifetime or `string2`’s? Then, when result is printed, is the smallest lifetime still valid?** If it is, then we’re good. In our example, `string1` and `string2` have the same lifetime, and both are valid when print is called with result. 

- <ins>Two examples with the above lifetime code:</ins>
```Rust
// Example 1: Different lifetimes but SUCCESS
fn main() {
    // `string1`'s lifetime is until the end of the main() function
    let string1 = String::from("abcd");

    {
        // `string2`’s lifetime is only until the end of the inner scope it is defined in
        let string2 = String::from("xyz");

        // `result`'s lifetime = smallest lifetime being passed into longest()
        // `string2` has the smallest lifetime being passed in, so `result`'s lifetime = `string2`'s lifetime
        let result = longest(string1.as_str(), string2.as_str());

        // The borrow checker says this print is valid because `string2` is still valid so result is valid
        println!("The longest string is {}", result)
    }
}

// Example 2: Different lifetimes and FAILURE
fn main() {
    // `string1`'s lifetime is until the end of the main() function
    let string1 = String::from("abcd");
    let result;

    {
        // `string2`’s lifetime is only until the end of the inner scope it is defined in
        let string2 = String::from("xyz");

        // `result`'s lifetime = smallest lifetime being passed into longest()
        // `string2` has the smallest lifetime being passed in, so `result`'s lifetime = `string2`'s lifetime
        result = longest(string1.as_str(), string2.as_str());
    }

    // The borrow checker says this print is INVALID because `string2` does not live to this point — it is
    // invalidated when the inner scope above ends. Thus, `result` does not live to this point.
    println!("The longest string is {}", result)
}
```

- **You can specify different lifetime annotations depending on what your function is doing**… Suppose we want the **longest() function to always return `x` no matter what**. In this case, we **don’t care about the lifetime of `y`**, so we can remove `‘a` from `y`.

```Rust
fn longest<'a>(x: &'a str, y: & str) -> &'a str {
    x
}
```

^^^Now the FAILURE example above is valid, because longest() is always going to return a reference that has the same lifetime as `x`.  `x` in this case is `string1`, and `string1` lives until the end of main(), so the print statement for result is valid. 

- <ins>NOTE:</ins> **If the return value is a reference, then the lifetime of the return value always has to be tied to the lifetime of one of our parameters.** This is because if we return a reference from a function, then it has to be a reference to something that is passed into the function. This is because we can’t return a reference to something created/declared inside the function, as this item would be dropped when the function ends. 
	- Of course, you can return an owned type from a function without worrying about this stuff (e.g., return a String). In this case, even though we create the the item inside of the function, ownership of the item transfers when it is returned.

## Lifetime Annotations in Struct Definitions

- Previously, **when we used structs, we always used owned data types**. But, **if we want to use a reference, then we have to specify lifetime annotations**.

```Rust
// The ImportantExcerpt struct has a reference to a string in its `part` field.
// For this to work, we have to specify a lifetime annotation.
struct ImportantExcerpt<'a> {
    part: &'a str,
}

fn main() {
    let novel = String::from("Call me Ishmael. Some years ago...");

    // first_sentence is a reference to a string slice that's the first sentence of the novel.
    let first_sentence = novel.split('.').next().expect("Could not find");

    // New instance of the struct, pass it first_sentence.
    // Our lifetime annotation in the Struct declaration says that the struct cannot outlive the reference
    // passed into the `part` field. So, if we tried to use 'i' (the instance of ImportantExcerpt) after first_sentence
    // goes out of scope, then we would get an error. 
    let i = ImportantExcerpt {
        part: first_sentence,
    };
}
```

## Lifetime Elision Rules

```Rust
// first_word() takes a reference to a string slice and returns the first word in it
fn first_word<'a>(s: &'a str) -> &'a str {
    let bytes = s.as_bytes();

    for (i, &item) in bytes.iter().enumerate() {
        if item == b' ' {
            return &s[0..i];
        }
    }
    &s[..]
}
```
^^^**The above function still works when you remove the lifetime annotation.** This is because **there are scenarios when the compiler can deterministically infer the lifetime annotations.** It does this by checking the **Three Lifetime Elision rules**.

<ins>Note before specifying the rules:</ins>
- **Input Lifetimes** = lifetimes of arguments being passed in   
- **Output Lifetimes** = lifetimes of return values 

**<ins>Three Lifetime Elision rules</ins>** -- the compiler will try to follow these three rules when assigning lifetimes. But **if at the end of these three rules, it still can’t figure out what the lifetimes are, then we have to manually specify them.** 

1. **Each parameter that is a reference gets its own lifetime parameter**. So, in first_word() above, `s` will get a lifetime parameter. 

2. **If there is exactly one input lifetime parameter, that lifetime is assigned to all output lifetime parameters.** So, in first_word(), because there is exactly one input lifetime parameter (`s` with `‘a`), the return type will get this lifetime parameter (`‘a`).

3. **If there are multiple input lifetime parameters, but one of them is &self or &mut self, then the lifetime of self is assigned to all output lifetime parameters.** This rule only applies to methods.

^^^We can see from rules 1 and 2 how the compiler is able to generate the lifetimes for first_word() on its own without us having to specify them. However, if we have multiple input lifetimes (like with longest() from earlier), then we have to specify the lifetimes manually because rule 2 is broken. 

## Lifetime Annotations Inside of Methods
- **Lifetime Annotations are a type of Generic**, so **just like with generics**, we have to **include the lifetime annotation inside of angle brackets after `impl` and after the name of our struct**.

```Rust
struct ImportantExcerpt<'a> {
    part: &'a str,
}

impl<'a> ImportantExcerpt<'a> {
    fn return_part(&self, announcement: &str) -> &str {	// We don’t need to specify lifetime annotations here
							// bc of rule 3 of our elision rules. I.e., we have two 
							// input lifetimes here but one of them is &self, so the
							// lifetime of self is assigned to all output lifetime parameters
        println!("Attention please: {}", announcement);
        self.part
    }
}
```

## Static Lifetimes

- **The static lifetime means that the reference could live as long as the duration of the program. All string literals have a static lifetime.** This is because string literals are stored in the program’s binary, so they live for the duration of the program. <ins>Ex:</ins>

```Rust
let s: &'static str = "I have a static lifetime.";
```

---

# Generics, Traits, Trait Bounds, and Lifetimes All Together

The longest_with_an_announcement() function below…
- **Takes two string references**, `x` and `y`.
- **Takes a generic type `T`**. The `ann` parameter, which is an announcement, has this type. 
- Prints the announcement and returns the longest string slice out of `x` and `y`.
- **Use of Generics and Trait Bounds:** The parameter `ann` is of type T, so it is a generic type. But, we use a trait bound in the `where` clause to limit `T` to any type that implements the `Display` trait (i.e., types that can be printed to the screen).
- **Use of Lifetime Annotations:** We take in two parameters `x` and `y`, which are both references to string slices (`&str`), and we return a reference to a string slice (`&str`). Bc we have two references and no self, the compiler can’t do automatic lifetime elision, so we have to manually specify the lifetime. In this case, the lifetime we specify is `‘a` on `x`, `y`, and the return value. Therefore, the lifetime of the return value is equal to the smallest lifetime being passed in out of `x` and `y`.

```Rust
use std::fmt::Display;

fn longest_with_an_announcement<'a, T>(
    x:&'a str,
    y:&'a str,
    ann: T,
) -> &'a str
where 
    T: Display,
{
    println!("Announcement! {}", ann);
    if x.len() > y.len() {
        x
    } else {
        y
    }
}
```

---

# Testing

## Why do we want to write Tests? 

- Rust does a great job making sure our program is correct with a powerful type system and things like the borrow checker — so **Rust checks that we’re passing around the right types and we’re not mismanaging memory.**
 
- But, **Rust doesn’t really check that our functions are doing the right thing — can’t check our business logic, intent of our code.**

## Writing Tests
1. **Create a new library** called ‘adder’: `cargo new adder --lib` 
	- **Test module and a test already created and written for us in `lib.rs`**
<img width="681" alt="Image" src="https://github.com/user-attachments/assets/ded72e5e-ddbf-4f8f-bc64-85ea129afc09" />
<br>

```Rust
mod tests {	// Test Module
    use super::*;

    #[test]	// the function has its own attribute called test. In Rust, functions are tests 
		// if they have this #[test] attribute. We could have other helper functions in this
		// test module that are not tests and they wouldn’t have the #[test] 
  
    fn it_works() {	// This test is called it_works.
        let result = add(2, 2);
        assert_eq!(result, 4);	// the function asserts that 2 + 2 = 4
    }
}
```

2. **To run the tests in lib.rs:** `cargo test`
<img width="696" alt="Image" src="https://github.com/user-attachments/assets/cf3ed6f3-31d1-488f-8926-a9c3aa76b0e8" />
  
^^^To summarize the screenshot above:

1. First, we see each test that Rust ran. In this case, there is only one test called it_works, which we discussed above. The status of the it_works test is ok, meaning it was successful.

2. Next, the first “test result” section gives a summary of all the tests that were run. In this case, we only had one test, so the status is ok because this one test passed. 
    - “measured” tests are performance tests

3. The next section (after the full summary of all tests) is similar to parts 1 and 2, but it’s specific to document tests. In Rust, you can write tests in your documentation. Currently, we don’t have any documentation or tests in our documentation, so we can 0 documentation tests, no individual documentation test results show up, and the summary of documentation tests contains all 0s. 

### Adding a Test that Fails

- **In Rust, a test fails if something inside the test function <ins>panics</ins>.** Each test is ran in a new thread, and if the main thread sees that the test thread has died, then it fails the test.

- In the below, we add a failing test called `failing_test`.
```Rust
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn it_works() {
        let result = add(2, 2);
        assert_eq!(result, 4);
    }
    #[test]
    fn failing_test() {
        panic!("Make this test fail.”)      // a test fails is something inside the test function panics
    }
}
```
^^^^^
<img width="697" alt="Image" src="https://github.com/user-attachments/assets/df2489f7-e024-4b30-a519-6670f3a18ae2" />

## Testing Product Code

```Rust
#[derive(Debug)]
struct Rectangle {    // Rectangle struct that stores the `width` and `height` of a rectangle.
    width: u32,
    height: u32,
}

impl Rectangle {
    // can_hold() takes in another Rectangle and returns true if the current Rectangle can hold the
    // passed in Rectangle inside itself (i.e., wider and taller).
    fn can_hold(&self, other: &Rectangle) -> bool {
        self.width > other.width && self.height > other.height
    }
}

#[cfg(test)]
mod tests {
    // Our product code is in the default module.
    // Our tests are in the tests module.
    // Thus, to test our product code, we have to bring it into scope. 
    // We use the 'use' keyword and a relative path with 'super' to reference the parent module.
    use super::*;

    // TEST 1: test that larger_can_hold_smaller() correctly shows that a larger Rectangle CAN
    // hold a smaller Rectangle
    #[test]
    fn larger_can_hold_smaller() {          
        let larger = Rectangle {
            width: 8,
            height: 7
        };
	// smaller Rectangle has smaller width and height than larger Rectangle
        let smaller = Rectangle {
            width: 5,
            height: 1,
        };
        // assert!() asserts that a given expression evaluates to true.
        // larger.can_hold(&smaller) should return true, so...
        assert!(larger.can_hold(&smaller));
    }

    // TEST 2: test that larger_can_hold_smaller() correctly shows that a smaller Rectangle CANNOT hold
    //  a larger Rectangle.
    fn smaller_cannot_hold_larger() {
        let larger = Rectangle {
            width: 8,
            height: 7,
        };
        let smaller = Rectangle {
            width: 5,
            height: 1,
        };

        // smaller.can_hold(&larger) should evaluate to false bc a smaller Rectangle should not be able to hold 
        // a larger Rectangle. To verify this, we add ! (negate) before smaller.can_hold(&larger) so that the expression 
        // evaluates to true when false is returned from can_hold(). Necessary bc assert!() asserts that a given
        // expression evaluates to true. 
        assert!(!smaller.can_hold(&larger));
    } 
}
```
<img width="682" alt="Image" src="https://github.com/user-attachments/assets/b34c9f73-ee81-45fd-a91b-790750ebabd4" />

<br><ins>IF we add a bug to the above product code:</ins>
```Rust
impl Rectangle {
    fn can_hold(&self, other: &Rectangle) -> bool {
	// flipped the first `>` to `<`. 
        self.width < other.width && self.height > other.height
    }
}
```

<img width="694" alt="Image" src="https://github.com/user-attachments/assets/89c5d435-88a1-45d3-9759-52893c013faa" />

^^^^Our test suite caught the bug. The `larger_can_hold_smaller` test panicked because the `assert!()` macro panics when the expression passed into it evaluates to false: "assertion failed: larger.can_hold(&smaller)".

## `assert_eq!` Macro

- The **`assert_eq!` macro allows you to compare two values.**

```Rust
// add_two() takes in an integer, adds 2 to it, and then returns the result. 
pub fn add_two(a: i32) -> i32 {
    a + 2
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn it_adds_two() {
        assert_eq!(4, add_two(2));	// asserts that if we pass 2 into add_two(), like add_two(2), then
					// it returns 4. 
	}
}
```
<img width="670" alt="Image" src="https://github.com/user-attachments/assets/6fd2deaa-293d-4131-a859-4b67507ee9ce" />

<br><ins>We can make the above test fail...</ins>

```Rust
pub fn add_two(a: i32) -> i32 {
    a + 3	// changed this to add 3 instead of 2
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn it_adds_two() {
        assert_eq!(4, add_two(2));
    }
}
```
<img width="692" alt="Image" src="https://github.com/user-attachments/assets/57add128-159a-4423-be09-5ddd33554bc4" />

^^^As is shown in the test output, **our test failed because assert_eq!() panics because left (4) is not equal to right (add_two(2)=5).**

### `assert_ne!` Macro

- assert_ne!() does the opposite of `assert_eq!()` and **asserts that the two parameters passed into it are not equal**.

- **In the failure example just above**, **changing to `assert_ne!()`** instead of `assert_eq!()`, would give **`assert_ne!(4, add_two(2)=5)`** which evaluates to **true** and **doesn't panic.**

- **<ins>IMPORTANT NOTE:</ins>** **Both parameters passed into assert_eq! and assert_ne!() must implement the PartialEq and Debug traits**. **All of the primitive values and most of the standard library implement these two traits.** However, if we create our own structs and enums, then we will have to implement them ourselves.

## Custom Failure Messages
```Rust
// greeting() takes in a name that's a string slice and prints "Hello {name}!"
pub fn greeting(name: &str) -> String {
    //format!("Hello {}!", name)
    format!("Hello!")	// modify greeting() to make it fail test
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    // Calls greeting() with the name "Carol" and asserts that the returned string contains "Carol".
    fn greeting_contains_name() {
        let result = greeting("Carol");
        assert!(result.contains("Carol"));
    }
}
```

<img width="697" alt="Image" src="https://github.com/user-attachments/assets/d8d684ac-8b9b-4d28-be22-aa559fff1fb2" />

^^^ The test thread panicked because assertion failed at `result.contains(“Carol”)`, which is as expected. It also gives us the line number for this (line 15). This is okay, but it’s <ins>not the most useful failure message</ins>. 

<br>

**We can improve this by adding our own custom failure message in the `greeting_contains_name` test**.

```Rust
#[test]
// Calls greeting() with the name "Carol" and asserts that the returned string contains "Carol".
fn greeting_contains_name() {
    let result = greeting("Carol");

    // assert!() takes a custom failure message as the 2nd parameter.
    // The remaining parameters in `assert` fill in the	placeholders in the custom failure message.
    assert!(
        result.contains("Carol"),
        "Greeting did not contain name, value was '{}'",	
	result,							
    );
}
```
<img width="696" alt="Image" src="https://github.com/user-attachments/assets/3239ae97-bba3-4433-a15a-37f6d01cd1a5" />
^^^We can see our custom failure message in the test output.

## Asserting that a Function Fails
```Rust
// Guess struct holds a value
pub struct Guess {
    value: i32,
}
impl Guess {
    pub fn new(value: i32) -> Guess {
        // The user must give a value between 1 and 100. If the value is less than 1 or greater than
        // 100, then panic.
        if value < 1 || value > 100 {
            panic!("Guess value must be between 1 and 100, got {}", value);
        }
        Guess { value }
    }
}
```
^^^**Test that the new() method above correctly panics when the value is greater than 100…**

```Rust
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    #[should_panic]		// the should_panic attribute asserts that the code
				// inside of the function body panics.
    fn greater_than_100() {
        Guess::new(200);	// we pass in 200, which is greater than 100, so new() should panic 
    }
}
```
<img width="668" alt="Image" src="https://github.com/user-attachments/assets/aa063345-4694-427a-a7af-4d2ae54c6c72" />
^^^The test passes!!

<br>**If we modify the new() method to not panic when the value is greater than 100, then the test fails** bc the method does not panic when you run Guess::new(200):
<img width="699" alt="Image" src="https://github.com/user-attachments/assets/35be9b8d-65fc-4f5b-9e17-0f31b39b548a" />

^^^Testing that a function panics in this way works but is **imprecise**. All our test with **#[should_panic]** is saying is that the **function we call should panic, but it could panic for any reason**. We need to make our assertion more precise:

1. **First, modify new() to have two different calls to panic with two different failure messages depending on if the value is greater than 100 or less than 1.**
```Rust
pub struct Guess {
    value: i32,
}
impl Guess {
    pub fn new(value: i32) -> Guess {
        if value < 1 {
            panic!(
                "Guess value must be greater than or equal to 1, got {}.",
                value,
            );
        } else if value > 100 {
            panic!(
                "Guess value must be less than or equal to 100, got {}.",
                value,
            );
        }
        Guess { value }
    }
}
```

2. Now, we can **modify our #[should_panic] attribute to only panic for a specific failure message…**

```Rust
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    // The below change to the should_panic attribute says: assert that the code in this test function panics
    // and the failure message contains “Guess value must be less than or equal to 100”	
    #[should_panic(expected = "Guess value must be less than or equal to 100”)].   
    fn greater_than_100() {
        Guess::new(200);
    }
}
```
<img width="682" alt="Image" src="https://github.com/user-attachments/assets/4f1b0db2-f92f-40b9-bba4-06ff25761a12" />

<br>If we change the value in new() to -2, then the **test fails because the panic message we got does not contain “Guess value must be less than or equal to 100”**...
<img width="702" alt="Image" src="https://github.com/user-attachments/assets/c499ade7-da2c-4281-beeb-0aa562d3043b" />

## Tests that Return a `Result` Type
- **Tests that return a `Result` type allow you to use the ? operator**, which can be **convenient if you have multiple operations within the test that could return an error type and <ins>you want the test to fail if any of those return an error type.</ins>**
```Rust
#[cfg(test)]
mod tests {
    // The it_works() test function returns a Result type:
    //     - The success case is a unit type (basically nothing)
    //     - The error case is a String
    #[test]
    fn it_works() -> Result<(), String> {
        if 2 + 2 == 4 {
            Ok(())
        } else {
            Err(String::from("two plus two does not equal four"))
        }
    }
}
```

### Why Tests that Return `Result` Are Useful...

**Normally, a Rust test function has a `()` return type, and it passes if it runs to completion without panicking.** If it panics (e.g., via assert!, panic!, or an uncaught unwrap/expect), it fails.

**<ins>When a test function returns a `Result<(), E>` (where `E` is some error type), the test passes if it returns `Ok(())` and fails if it returns `Err(e)`</ins>**. This is **incredibly useful for**:

1. **Explicit Error Reporting:** The Err variant allows you to return a specific error value, which can provide more detailed information about why a test failed compared to just a generic panic message. This makes debugging much easier.

2. **Testing Fallible Operations:** Many Rust functions return Result (e.g., file I/O, network requests, parsing). When testing these functions, returning Result from your test allows you to directly use the return values without extra unwrap() or expect() calls that might obscure the actual failure.

3. **Chaining Fallible Operations:** This is where the `?` operator shines. If you have a sequence of operations, any one of which could return an Err, the ? operator provides a compact way to stop the test early if an error occurs.

### How the `?` Operator is Useful Here

The `?` operator is syntactic sugar for error propagation. When you use **`some_fallible_expression?`**, it does the following:

1. If some_fallible_expression evaluates to `Ok(value)`: It unwraps the Ok variant and `value` becomes the result of the expression. The execution continues normally.

2. If some_fallible_expression evaluates to `Err(error)`: It immediately returns that `Err(error)` from the current function. This is why the function using `?` must have a `Result` return type that is compatible with the error type being propagated.

- <ins>In the context of tests returning `Result`:</ins> **When you use `?` in such a test, if an operation inside the test returns an Err, that Err is automatically returned from the test function itself. The Rust test runner then interprets this Err return as a test failure.**

- <ins>Why it's useful:</ins> **Without `?`, you'd have to write `match` statements** or unwrap()/expect() calls for every fallible operation.

### Examples

**Example without a `Result` Return Type:**

```Rust
fn safe_divide(numerator: i32, denominator: i32) -> i32 {
    if denominator == 0 {
        panic!("Cannot divide by zero!"); // panicking is bad if the error is recoverable
    }
    numerator / denominator
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_valid_division() {
        let result = safe_divide(10, 2);
        assert_eq!(result, 5); // Test passes
    }

    #[test]
    #[should_panic(expected = "Cannot divide by zero!")]	// *expect* a panic
    fn test_divide_by_zero_panics() {
        safe_divide(10, 0); 
    }
}
```
<img width="658" alt="Image" src="https://github.com/user-attachments/assets/483a35bb-9711-404e-aa8b-f60ecf608322" />

<br>**Example with a `Result` Return Type — Rust-idiomatic way to handle recoverable errors.**

```Rust
fn safe_divide_result(numerator: i32, denominator: i32) -> Result<i32, String> {
    if denominator == 0 {
        // We return an Err here instead of panicking, MUCH BETTER
        // Rust-idiomatic way to handle recoverable errors.
        Err(String::from("Cannot divide by zero"))
    } else {
        Ok(numerator / denominator)
    }
}

#[cfg(test)]
mod tests {
    use super::*;


    // 1. TEST THAT PASSES BC NO ERROR RETURNED FROM safe_divide_result

    #[test]
    // This test now returns Result<(), String>
    // It passes if it returns Ok(()) and fails if it returns Err(some_string)
    //
    fn test_valid_division_with_result() -> Result<(), String> {

        // Below, safe_divide_result returns Ok(5)
        // The `?` unwraps the Ok(5), so `result` becomes 5.
        // Execution continues.
        //
        let result = safe_divide_result(10, 2)?; 
        assert_eq!(result, 5);
        Ok(()) // Test passes by returning Ok(())
    }


    // 2. TEST FAILS BC ERROR RETURNED FROM safe_divide_result

    #[test]
    fn test_divide_by_zero_with_result() -> Result<(), String> {

        // Below, safe_divide_result returns Err("Cannot divide by zero")
        // The `?` sees the Err, and immediately returns it from `test_divide_by_zero_with_result`.
        // The test runner sees this Err and marks the test as failed.
        //
        let result = safe_divide_result(10, 0)?;	// The test stops here and fails.

        // This line will NEVER be reached if the `safe_divide_result` returns an error
        Ok(())
    }


    // 3. TEST TO MAKE SURE safe_divide_result RETURNS CORRECT ERROR IN ERROR CASE

    #[test]
    fn test_divide_by_zero_and_check_error_message() -> Result<(), String> {
        let division_result = safe_divide_result(10, 0);

        // Instead of `?`, we're explicitly checking the error.
        // We expect it to be an Err, and we want to check its message.
        assert!(division_result.is_err());	// Assert that it's indeed an error
        assert_eq!(division_result.unwrap_err(), "Cannot divide by zero");	// Get the error and check its content

        Ok(())	// If we reach here, it means we handled the error correctly, so the test passes.
    }
}
```
<img width="690" alt="Image" src="https://github.com/user-attachments/assets/6988e50a-c4c5-443e-9585-3c1922762f38" />

## Controlling How Tests Run

```Rust
#[cfg(test)]
mod tests {
    // This test returns a Result type and tests that 2 + 2 = 4
    #[test]
    fn it_works() -> Result<(), String> {
        if 2 + 2 == 4 {
            Ok(())
        } else {
            Err(String::from("two plus two does not equal four"))
        }
    }

    // This tests that 2 + 2 = 4 using assert_eq!()
    #[test]
    fn it_works2() {
        assert_eq!(2 + 2, 4);
    }
}
```
<img width="670" alt="Image" src="https://github.com/user-attachments/assets/75066d00-d5d7-4947-aa68-9ce36d2b04cf" />

^^^**`cargo test`** compiles your code in test mode and runs the resulting test binary. 

So far, we’ve just been running `cargo tests` but we could specify command line options to change some of the defaults…
- **By default, all tests get run in parallel in a separate thread**
- **By default, all generated output is captured and not printed to the screen.** So, for example, in our test **if we had a print statement, then this print statement would not actually get printed out when we do `cargo test`**. 

**There are two sets of command line options…**
1. **One set goes to the `cargo test` command**
2. **The other set goes to the resulting test binary**

These two sets of command line options are separated by two dashes. For example…
1. If we want to figure out which **options we could pass to the `cargo test`** command: **`cargo test --help`**
2. If we want to figure out which **commands we could pass to the resulting test binary**: **`cargo test -- --help`**

### Changing the Number of Threads
The **`--test-threads`** command line option **allows you to set the number of threads used when running tests in parallel**. **By default, every test gets its own thread**. But, if we wanted to run tests serially, then we can set test-threads equal to 1…

<ins>Example:</ins> In the below, we are using the command line options for the resulting test binary…

**`cargo test -- --test-threads=1`**
 
^^^Generally, you wouldn’t want to do something like this because your tests would run slower, but may be useful in some cases. For example, you might have some tests that modify a file on disk and it happens to be the same file. If the tests run in parallel, then they’ll modify the file at the same time, which will cause tests to fail. You can solve this issue by having each test modify a different file, or you can run the tests serially instead of in parallel. 

### Showing Output
```Rust
fn prints_and_returns_10(a: i32) -> i32 {
    println!("I got the value {}", a);	// prints an integer, we want this output to show in the tests
    10
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn this_test_will_pass() {
        let value = prints_and_returns_10(4);
        assert_eq!(10, value);	// passes bc prints_and_returns_10() always returns 10
    }

    #[test]
    fn this_test_will_fail() {
        let value = prints_and_returns_10(8);
        assert_eq!(5, value);	// fails bc prints_and_returns_10() always returns 10
    }
}
```
^^^
When we run `cargo test`, we **only see the print statement for the failing test.**
<img width="689" alt="Image" src="https://github.com/user-attachments/assets/87926b7a-c56b-4779-b2f0-3a0cea1b0b7a" />
^^^BUT, **for the test that succeeded, we don’t see the print statement.** This is because **by default, standard output is captured for passing tests and we don’t see it on the screen**. We can change this with command line options.

We can fix this by giving an argument to the resulting test binary called `show-output`:

**`cargo test -- --show-output`**

<img width="689" alt="Image" src="https://github.com/user-attachments/assets/827cb294-e190-4957-8dbd-afba92fe2f57" />

^^^**Now, we also see the print statement for the passing test.**

### Running a Subset of Tests 
— We can **run a subset of tests using the test name**
```Rust
pub fn add_two(a: i32) -> i32 {
    a + 2
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn add_two_and_two() {
        assert_eq!(4, add_two(2)); // test that if you pass in 2, you get 4
    }

    #[test]
    fn add_three_and_two() {
        assert_eq!(5, add_two(3)); // test that if you pass in 3, you get 5
    }

    #[test]
    fn one_hundred() {
        assert_eq!(102, add_two(100)); // test that if you pass in 100, you get 102
    }
}
```
- If we only want to run the test called `one_hundred`: **`cargo test one_hundred`**

- If we want to run the two tests that start with “add”: **`cargo test add`**

- If we want to run tests based on the module (e.g., those in the “tests” module): **`cargo test tests::`**

### Ignoring Tests
```Rust
#[cfg(test)]
mod tests {
    #[test]
    fn it_works() {
        assert_eq!(2 + 2, 4);
    }

    #[test]
    #[ignore]			// the ignore attribute ignores the test 
    fn expensive_test() {
        // code that takes an hour to run
    }
}
 ```

<br><ins>When you run</ins> `cargo test`</ins>:
<img width="670" alt="Image" src="https://github.com/user-attachments/assets/1beff9c4-602c-463d-9f41-7ddb893d61ea" />

<br>**To run ONLY the tests that have the `#[ignore]` attribute:** 

**`cargo test -- --ignored`**

<img width="674" alt="Image" src="https://github.com/user-attachments/assets/ce0f2f74-22f1-4a34-a60e-a06289eef130" />
^^^<ins>The filtered out test is the one test we have without #[ignore]</ins>

## Test Organization

The Rust community thinks about tests as falling into two main categories: **unit tests** and **integration tests**

### Unit Tests

- **small, focused, test one module in isolation, and could test private interfaces.**
  
- We **have only been writing unit tests thus far.**
  
- In Rust, unit tests **live in the same file as our product code**
 
<ins>**lib.rs file**</ins> — 
```Rust
// %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
// OUR PRODUCT CODE

// add_two() is a public function that calls the private internal_adder() function to add 2 to the passed in num.
pub fn add_two(a: i32) -> i32 {
    internal_adder(a, 2)
}

// internal_adder() is a private function that adds two numbers together.
fn internal_adder(a: i32, b: i32) -> i32 {
    a + b
}
// %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%



// %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
// OUR TESTS -- In Rust, it's convention that in the same file as your product code, you have
// a module called `tests` which holds your tests for the product code. 

#[cfg(test)]	// this attribute says the configuration of the module is test, meaning
		// cargo only compiles the code in this module when we run `cargo test`.
mod tests {
    use super::*;   // import everything from the parent module

    // test function to call and test the private internal_adder() function
    // NOTE: internal_adder() is private but we can call it in our test module because child modules in Rust
    //       are able to access anything in their parent module (even private fields).
    #[test]
    fn internal() {
        assert_eq!(4, internal_adder(2, 2));
    }
}
// %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
```

### Integration Tests

- **Completely external to your library and thus test the public interface of your library.**

- **Live in a folder called `tests` at the root of your project.**
<img width="206" alt="Image" src="https://github.com/user-attachments/assets/724a1a0c-d074-4d9f-ac37-ca961b5268d8" />

- **Cargo knows to look for integration tests inside the ‘tests’ directory at the root of our project.** **Cargo will turn each of the files in the ‘tests’ directory into a crate.**

<ins>**integration_test.rs file**</ins>

```Rust
// At the top of our integration_test.rs file, we have to bring our adder library into scope (see lib.rs
// file above which contains our product code, i.e., the adder library). This is because every
// file in the ‘tests’ directory is going to be a new crate.
use adder;

#[test]	// write a test function, don’t need module with config annotation bc 
	// cargo knows that all files in the ‘tests’ directory are tests 
fn it_adds_two() {
    assert_eq!(4, adder::add_two(2));	// have to call the public add_two(), can’t call private internal_adder()
} 
```

**`cargo run`** => 
<img width="696" alt="Image" src="https://github.com/user-attachments/assets/149696de-1c86-41bb-b43f-261c4e23c813" />
^^^We now have three sections
1. The first section is for our unit tests (currently we just have the test called internal, which is shown earlier in the unit tests section.
2. The second section is for our integration tests
3. The third section is for our document tests

<br>**If we want to run JUST our integration tests:** 

**`cargo test --test integration_test`**

<br><ins>Defining Shared Code Amongst Our Integration Tests</ins>

- <ins>NOTE:</ins> Because every file in the ’tests’ directory is treated as a separate crate, this could lead to unexpected behavior. For example, if you have multiple integration test files and you want to share some code between those files.

- To do so, create a new folder in our `tests` directory called `common`, and create a new file called `mod.rs` in common.

- Then, add the shared code to `mod.rs`.
<img width="254" alt="Image" src="https://github.com/user-attachments/assets/d2f644b3-9a40-4d25-ba1d-b173ffdfd5ea" />

<br>In the below, when we run `cargo test`, we DON'T get a separate section of tests for the folder with the shared code. **This is because files in subdirectories of the ‘tests’ folder do not get compiled as crates.**

<img width="683" alt="Image" src="https://github.com/user-attachments/assets/11b70db3-ecf9-44d3-b556-b3d9beba749c" />

<br>Also, **because we put our code into a file called mod.rs, our code is now in a module that can be used by our other integration test files**...

```Rust
use adder;

mod common;	// This is a module declaration and it will look for the contents of the module in either a file
		// called common.rs or a **folder called common with a file called mod.rs**

#[test]
fn it_adds_two() {
    common::setup();	// We can call the function defined in our module
    assert_eq!(4, adder::add_two(2));
}
```

NOTE: we have a lib.rs file in our src directory, which means we have a library crate. If we had a main.rs file instead, then we would have a binary crate. **We can’t directly test binary crates with integration tests.** This is why **it’s common to see a binary crate that’s a thin wrapper around a library crate. This way, you can test the library crate with integration tests.**

---

# CLI Program

**<ins>lib.rs</ins>**

```Rust
use std::error::Error;
use std::fs;
use std::env; // import the environment module

// Box<dyn Error> essentially represents any type of error
pub fn run(config: Config) -> Result<(), Box<dyn Error>> {
    // With ?, if read_to_string() returns an Error type, then that Error type will automatically be
    // returned from the function.
    let contents = fs::read_to_string(config.filename)?;

    if config.case_sensitive {
        for line in search(&config.query, &contents) {
            println!("{}", line);
        }
    } else {
        for line in search_case_insensitive(&config.query, &contents) {
            println!("{}", line);
        }
    }
    // OR CAN DO:
    // let results = if config.case_sensitive {
    //     search(&config.query, &contents) 
    // } else {
    //     search_case_insensitive(&config.query, &contents)
    // };
    // for line in results {
    //     println!("{}", line);
    // }

    Ok(())  // In Ok() case, we return unit type
}

fn search<'a> (query: &str, contents: &'a str) -> Vec<&'a str> {
    let mut matches = Vec::new();
    for line in contents.lines() {
        if line.contains(query) {
            matches.push(line);
        }
    }
    matches
}

fn search_case_insensitive<'a> (query: &str, contents: &'a str) -> Vec<&'a str> {
    
    let mut matches = Vec::new();
    let query = query.to_lowercase();

    for line in contents.lines() {
        if line.to_lowercase().contains(&query) {
            matches.push(line);
        }
    }
    matches
}

pub struct Config {
    pub query: String,
    pub filename: String,
    pub case_sensitive: bool,
}
impl Config {
    pub fn new(args: &[String]) -> Result<Config, &str> {
        if args.len() < 3 {
            return Err("Not enough arguments");
        }
        let query = args[1].clone();
        let filename = args[2].clone();

        // We use environment variables to determine if we want to do regular case sensitive
        // search or case insensitive search. 
        // We call the var() function in the environment module which takes in a key to an 
        // environment variable and returns a Result type if the key exists. If the environment
        // variable is set, then the Result will be Ok() containing the set value. Otherwise, it
        // will be Error. Then, we call is_err() which returns a boolean that is equal to True if
        // var() errors. 
        //     Thus, if "CASE_INSENSITIVE" is not set, then var() will return Error, so is_err() will return True.
        //                  so case_sensitive will be True
        //           if "CASE_INSENSITIVE" is set, then var() will NOT return Error, so is_err() will return False.
        //                  so case_sensitive will be False
        //
        // Can set environment variable: export CASE_INSENSITIVE=true
        // Unset environment variable: unset CASE_INSENSITIVE
        let case_sensitive = env::var("CASE_INSENSITIVE").is_err();

        Ok(Config { query, filename, case_sensitive})
    }
}

#[cfg(test)]
mod tests {
    use super::*;   

    #[test]
    fn case_sensitive() {
        let query = "duct";
        let contents = "\
Rust:
safe, fast, productive.
Pick three.
Duct tape.";
        assert_eq!(vec!["safe, fast, productive."], search(query, contents));
    }

    #[test]
    fn case_insensitive() {
        let query = "rUsT";
        let contents = "\
Rust:
safe, fast, productive.
Pick three.
Trust me.";
        assert_eq!(
            vec!["Rust:", "Trust me."], 
            search_case_insensitive(query, contents)
        );
    }
}
```

**<ins>main.rs</ins>**

```Rust
use std::env;
use std::process; // allow us to exit the program without panicking

use minigrep::Config; // import the Config struct from our library crate 

fn main() {
    let args: Vec<String> = env::args().collect();

    // unwrap_or_else() takes in a closure containing the error variant. It
    // either returns the Ok value or computes it from the closure.
    let config = Config::new(&args).unwrap_or_else(|err| {
        eprintln!("Problem parsing arguments: {}", err); // print error to the standard error stream
        process::exit(1);  // terminates the program with the status code passed in
    });
    // Could also use a match like the below...
    // let config = match Config::new(&args) {
    //     Ok(val) => val,
    //     Err(err) => {
    //         eprintln!("Problem parsing arguments: {}", err);
    //         process::exit(1);
    //     }
    // };

    println!("Query: {}", config.query);
    println!("Filename: {}", config.filename);

    match minigrep::run(config) {
        Ok(_) => (), // in Ok case we do nothing
        Err(err) => {
            eprintln!("Application Error: {}", err); // print error to the standard error stream
            process::exit(1);
        }
    };

    // Could also use if let syntax because we only care about one case (i.e., the error variant in this example)...
    // if let Err(err) = run(config) {
    //     eprintln!("Application Error: {}", err);
    //     process::exit(1);
    // } 

}
```

---

# Closures

Closures are **anonymous functions** (i.e., no name), like lambda functions in Python. 
- They **could be stored as variables and passed around.** 
- They **could** even **be passed in as input parameters to a function.**
- They **capture the variables inside the scope in which they are defined.**

1. **Closure with <ins>no parameters</ins> and <ins>performs one action (doesn't return anything) </ins> —  printing specific text**

```Rust
let print_text = || println!("Defining Closure");	// store closure in a variable so can call it 

print_text();	// call the closure
```

2. **Closure with <ins>1 parameter</ins> and <ins>returns a value</ins> — adding 1 to a passed in integer**

```Rust
let add_one = |x: i32| x + 1;	// store closure in a variable so can call it 

add_one(2);	// call the closure with value 2
```

3. **Closure with <ins>multiple parameters</ins> and <ins>multiple lines</ins> — return the squared sum of two parameters**

```Rust
let squared_sum = |x: i32, y: i32| {

    let mut sum: i32 = x + y;	// find the sum of two parameters

    let mut result: i32 = sum * sum;	// find the squared value of the sum

    return result;
};

let result = squared_sum(5, 3);	// call the closure
```

## Closure Environment Capturing

Closure has a unique feature that allows it to capture the environment. This means the **closure can use the values in its scope**. <ins>For example, in the below,</ins> t**he closure bound to `print_num` uses the variable `num` which was not defined in it…**

```Rust
fn main() {
    let num = 100;

    // A closure that captures the `num` variable
    let print_num = || println!("Number = {}", num);

    print_num(); 
}
```

### Closure Environment Capturing Modes in Rust

1. **<ins>Capture by Immutable Borrow (`&T`):</ins>** **Variable is not modified inside the closure.** In the below, the variable **`word` is not modified inside the closure `print_str`**. **As the variable is immutable by default, we can make any number of immutable references of `word` inside the closure.** Notice that the closure variable `print_str` is also immutable.

	- **<ins>When a closure captures a variable by immutable borrow</ins>** (which **happens when the variable is only read inside the closure**, as `word` is in `println!("word = {}", word)`), **<ins>the closure essentially takes an immutable reference to that variable.</ins>** The core rule is that **you can have any number of _immutable references_ to a piece of data simultaneously.** Because the closure `print_str` only holds an immutable borrow of `word`, and `println!("length of word = {}", word.len());` also takes an immutable borrow of `word`, these operations can coexist.

 	- **Encoded in the `Fn` function trait** — **`Fn` immutably borrows values**

```Rust
fn main() {
    let word = String::from("Hello");

    // immutable closure — all we do is print the word, don’t modify it 
    let print_str = || println!("word = {}", word); 

    // now we CAN still do an immutable borrow outside the closure, can do as many immutable 
    // references to `word` as we want, as explained above
    println!("length of word = {}", word.len());

    print_str();
}
```

2. **<ins>Capture by Mutable Borrow (`&mut T`):</ins>** **Variable is modified inside the closure.** In the below example, the variable **`word` is modified inside the closure `print_str` with `word.push_str("World!");`**. Thus, we **have to make the variable `word` mutable as well as the closure variable `print_str`**. This means **<ins>no other references of the `word` variable can exist unless the closure is used</ins>, since the closure takes a mutable reference to the piece of data.**
	- **Encoded in the `FnMut` function trait** — **`FnMut` mutably borrows values**

```Rust
fn main() {
    let mut word = String::from("Hello");

    // mutable closure — we modify the value of `word`, so closure borrows the variable as mutable
    let mut print_str = || {
        word.push_str(" World!");
        println!("word = {}", word);
    };

    // NOTE: CANNOT immutable borrow here because the variable is borrowed as mutable inside the
    // closure, see screenshot below…
    // println!("length of word = {}", word.len());

    print_str();

    // BUT, can immutable borrow here because the closure has been already used
    println!("length of word = {}", word.len());
}
```

- <ins>To elaborate on why we have to make the `print_str` variable mutable in the above even though it just stores the closure…</ins>

    - **`FnMut`** **requires `&mut` self on the closure itself.**

    - Because the **closure in the above example captures `word` by mutable reference**, its **type automatically becomes `FnMut`.**

    - A **closure** of type **`FnMut`** **has a `fn call_mut(&mut self)` method (or similar) that takes `&mut self`**. This means that **whenever you call `print_str()`**, you are effectively **calling a method on the `print_str` variable that requires `print_str` itself to be mutable.**

    - **<ins>BEST ANALOGY:</ins>** **Think of `print_str` as a struct that internally holds a `&mut String` to `word`.** **When you call `print_str()`**, you're essentially saying **"I want to use the mutable reference stored within `print_str`." To allow that usage, `print_str` itself must also be mutable.**

<br>

3. **<ins>Capture by Move (i.e., Capture by value, Taking Ownership) (`T`):</ins>** **Variable is moved inside closure.** Here, we move the value in the `word` variable to a new variable `new_word` inside the closure. As the variable is moved, we cannot use it anywhere else except for inside the closure.

	- **Encoded in the `FnOnce` function trait** — **`FnOnce` takes ownership of the variables inside the closure’s environment.** The “Once” part of the name represents the fact that closures can’t take ownership of the same variables more than once. So, these closures can only be called once. 

```Rust
fn main() {
    let word = String::from("Hello");

    // `word` is moved into the closure — value in `word` variable is moved to a new variable in the closure
    let print_str = || {
        let new_word = word;
        println!("word = {}", new_word);
    };

    print_str();

    // CANNOT immutable borrow here because word variable has moved inside closure
    // see screenshot below…
    // println!("length of word = {}", word.len());
}
```

<br>

**When you create a closure, Rust infers which of the traits to use (`FnOnce`, `FnMut`, `Fn`) based on how you use the values inside the closure’s environment.** 

- You can **force the closure to take ownership of the values it uses inside its environment by using the `move` keyword in front of the closure.** Mostly **useful when you’re passing a closure from one thread to another thread** so you can also pass the ownership of the variables from one thread to the other thread. Ex:

```Rust
fn main() {
    let x = vec![1,2,3];

    // Inside this closure, we just evaluate `z == x`, so we don't take ownership of `x` inside our closure.
    // However, we can force the closure to take ownership of `x` by specifying `move`.
    //
    let equal_to_x = move |z| z == x;

    println!("can't use x here {:?}", x);	// this errors (red squiggly under `x`) bc the closure now takes
    						// ownership of `x` so we can't use `x` after it’s been moved.
```

NOTE: **Because closures capture their environment, they have to use extra memory to store that context**. Functions, on the other hand, don’t capture their environment, so they don’t incur the same overhead. 

## Closure Type Inference

**You don’t have to annotate the type of your closure’s input parameter nor do you have to annotate your closure’s return value.** For regular functions, you would have to specify the type of the input parameters and the type of the return value. 

- **Functions** are part of an explicit interface exposed to users, so agreeing on the types being passed in and returned is important.

- **Closures** are usually short and only relevant within a narrow context, so the **compiler is able to determine the input parameter types and the return types**. This is similar to how the compiler is able to determine the types of most variables. 

<ins>Example:</ins> You **can make the types explicit in a closure**…
```Rust
let expensive_closure = |num: u32| -> u32 {
	…
}
```

<ins>NOTE:</ins> **Closure definitions can only have one concrete type inferred for each input parameter**…

```Rust
let example_closure = |x| x;
	
let s = example_closure(String::from(“hello”));	// here, the compiler infers that `x` in the closure is a `String`

let n = example_closure(5);	// this fails bc the compiler expects from previous line that 
				// `x` is a String
```

^^^**The first type passed into our closure will be the concrete type of our input parameters.**

## Closure Example Use Case

Imagine you are building a back end for a fitness app, and the backend is built in Rust. The fitness app will generate customized workouts for a user based on various factors like their age, body mass index, workout preference, and intensity level. **Part of this algorithm runs a calculation that is expensive and takes a few seconds to run. We want to perform this expensive calculation as few times as possible, so we <ins>cache results of the calculation</ins>. CACHER IMPLEMENTATION**

```Rust
use std::collections::HashMap; // Import HashMap
use std::thread;
use std::time::Duration;

fn main() {
    let simulated_intensity = 10;
    let simulated_random_number = 7;

    generate_workout(simulated_intensity, simulated_random_number);
}

// In order to define structs, enums, or even function parameters that use closures, we need to
// use generics and trait bounds. Here, we have a generic called `T` and we define a trait bound
// for the generic with the `Fn` trait (function, capture by immutable borrow). All closures implement
// one of the three fn traits `Fn`, `FnMut`, `FnOnce`. Regular functions also implement these three fn traits.
//
struct Cacher<T>
where
    T: Fn(u32) -> u32,	// For a `Cacher` to exist, `T` must be a function (specifically, `T` must implement the `Fn` trait).
{
    calculation: T,	// calculation can be any closure that meets the trait bound
    	
    value: HashMap<u32, u32>,	// `value` is a HashMap to store results for different arguments.
				// The key will be the `u32` argument, and the value will be the `u32` result.
}

// The implementation block for `Cacher` has the same generic and trait bound as the `Cacher` struct
//
impl<T> Cacher<T>
where
    T: Fn(u32) -> u32,	// For the methods within this specific implementation of
			// `Cacher` (`new` and `value`), `T` is a function (implements the `Fn` trait).
{
    fn new(calculation: T) -> Cacher<T> {	// Constructor. Takes in a calculation of type `T` (our closure), and
						// creates a new `Cacher`, passing in the calculation and initializing an
						// empty HashMap.
        Cacher {
            calculation,
            value: HashMap::new(),	// Initialize an empty HashMap when the `Cacher` is created.
        }
    }

    // `value()` method, method bc first param is reference to `self`
    fn value(&mut self, arg: u32) -> u32 {

        // Check if the result for the given `arg` already exists in the HashMap.
        // `entry(arg)` gets an Entry enum, which can be `Occupied` or `Vacant`.
        // `or_insert_with` allows us to insert a value if the key is vacant, 
        // using the result of a closure (in this case, calling `self.calculation`).
        //
        *self.value.entry(arg).or_insert_with(|| {

            // If the `arg` is NOT in the HashMap, execute the expensive calculation and store its result.
            let v = (self.calculation)(arg);
            println!("Caching result for argument: {}", arg);	// Added for clarity, see print output below
            v
        })
        // `or_insert_with` returns a mutable reference to the value.
        // We dereference it (`*self.value...`) to get the owned `u32` value.
    }
}

fn generate_workout(intensity: u32, random_number: u32) {
    // Call the `new()` function in our `Cacher` struct on our closure for the expensive calculation
    // Make variable mutable bc we will be calling the `value` method which mutates the `Cacher` instance
    //
    let mut cached_result = Cacher::new(|num| {
        println!("calculating slowly...");
        thread::sleep(Duration::from_secs(2));	// this is the expensive calculation
        num
    });

    if intensity < 25 {
        println!(
            "Today, do {} pushups!",
            cached_result.value(intensity),	// The 1st call with intensity 10 will calculate and cache the result.
        );
        println!(
            "Next, do {} situps!",
            cached_result.value(intensity),	// The 2nd call with intensity 10 will retrieve the cached result. 
        );
        println!(
            "How about some jumping jacks? {} of them!",
            cached_result.value(15),	// This is a new argument (15), so it will calculate and cache this result.
        );
        println!(
            "And back to pushups: {} of them!",
            cached_result.value(intensity),	// This will again retrieve the cached result for 10.
        );
    } else {
        if random_number == 3 {
            println!("Take a break today! Remember to stay hydrated!");
        } else {
            println!( 
                "Today, run for {} minutes!",
                cached_result.value(intensity),
            )
        }
    }
}
```

---

# Iterators

- The **iterator pattern** allows you to **iterate over a sequence of elements regardless of how the elements are stored** (e.g., an array, a hashmap, a graph, a custom data structure, etc.)

- **Iterators encapsulate the logic for iterating over these different data structures**, whether its an array (simple just incrementing the index, or a hashmap which is more complicated). **This allows you to iterate over various data structures in a uniform way.**

- <ins>Example:</ins>

```Rust
let v1 = vec![1, 2, 3];

let v1_iter = v1.iter();	// create an iterator over the vector
```

- <ins>NOTE:</ins> **In Rust, iterators are lazy.** When we do `let v1_iter = v1.iter();`, **nothing special happens until we actually use the iterator**…

```Rust
for value in v1_iter {
    println!("Got: {}", value);
}
```

## How Iterators Work

- All iterators in Rust implement the **`Iterator` trait** which is defined in Rust standard library. Looks something like the below... 

	- As you can see, **iterators are very simple** — there’s **only one method you have to implement which is the <ins>next()</ins> method**. All the other methods have default implementations. 

	- The **<ins>next()</ins> method** **returns the next item in the iteration wrapped in Some() and when we get to the end of the iteration, it returns None.**

```Rust
pub trait Iterator {
    type Item;	// when implementing the iterator, you also have to define the `Item` type, which
		// is the type returned from the `next()` method.

    fn next(&mut self) -> Option<Self::Item>;	// we also need a mutable reference to `self` bc
						// calling `next()` changes the internal state of the
						// iterator used to track where it is in the sequence.

    // methods with default implementations elided
}
```

<br>

<ins>Example showing iterator in action with next():</ins>

```Rust
fn iterator_demonstration() {
    let v1 = vec![1, 2, 3]; 

    let mut v1_iter = v1.iter();	// mutable variable to store iterator, must
					// be mutable bc we're calling next() and next()
					// needs a mutable reference to the iterator

    assert_eq!(v1_iter.next(), Some(&1));	// First call, get reference to first elem in iterator wrapped in Some()
    assert_eq!(v1_iter.next(), Some(&2));	// Second call, get reference to second elem in iterator wrapped in Some()
    assert_eq!(v1_iter.next(), Some(&3));	// Third call, get reference to third elem in iterator wrapped in Some()
    assert_eq!(v1_iter.next(), None);		// Fourth call, get None bc at the end of vector
}
```

<ins>^^^^NOTE:</ins> Our **iterator returns immutable references when we use `iter()`…**

- **`iter()`**  —  **immutable references**

- **`iter_mut()`**  —  **mutable references**

- **`into_iter()`**  —   **own types**
	- <ins>Example with</ins> `into_iter`:

```Rust
#[test]
fn iterator_demonstration() {
    let v1 = vec![1, 2, 3]; 

    let mut v1_iter = v1.into_iter();   

    // You can see in these `assert_eq!()` calls that the value stored in `Some` is
    // an own type, not a reference like we had with `iter()`.
    assert_eq!(v1_iter.next(), Some(1)); 
    assert_eq!(v1_iter.next(), Some(2)); 
    assert_eq!(v1_iter.next(), Some(3));  
    assert_eq!(v1_iter.next(), None);   
}
```

## Additional Iterator Methods with Default Implementations

The **`Iterator` trait** has **various methods which have default implementations provided by the standard library**. There are <ins>two broad categories of methods</ins>:

1. **<ins>Adapters</ins>** — **Take in an iterator and return another iterator.**

- **`.map(closure)`** — Takes a closure and creates an iterator which calls that closure on each element in the sequence. <ins>Example:</ins>
	
```Rust
let v1 = vec![1, 2, 3];

// map() returns an iterator and iterators in Rust are lazy. So it doesn't do anything until we
// use a consumer method. We use collect() to transform it into a collection.
//
let v2: Vec<i32> = v1.iter().map(|x| x + 1).collect(); // [1, 2, 3] -> [2, 3, 4]
```

- **`.filter(closure)`** — Accepts a closure and creates an iterator which uses the closure to determine if an element should be included in the new iterator or not. Given an element the closure must return true or false. The returned iterator will yield only the elements for which the closure returns true. <ins>Example:</ins>

```Rust
#[derive(PartialEq, Debug)]
struct Shoe {	// shoe struct that represents a single shoe 
    size: u32,	// size of the shoe
    style: String,	// style of the shoe
}

// Takes a vector of shoes (not a reference so takes ownership of the vector) and a shoe size
// Filters the shoes in the vector to only shoes that have the specified size
//
fn shoes_in_my_size(shoes: Vec<Shoe>, shoe_size: u32) -> Vec<Shoe> {

    // into_iter() creates an iterator that takes ownership of the shoes vector.
    // 
    // Call the filter() method to create an iterator that only includes shoes with size equal to the
    // passed in shoe_size. This is an example of closures capturing their environment, as shoe_size 
    // is not defined in the closure but the closure has access to it.
    // 
    // Call collect() to convert the iterator returned from filter into a collection (vector of shoes)
    // 
    shoes.into_iter().filter(|s| s.size == shoe_size).collect()
}
```

- **`.zip(other iterator)`** — takes in another iterator and ‘zips up' the two iterators into a single iterator of pairs. Just like zip() in Python. <ins>Example:</ins>

```Rust
let a1 = [1, 2, 3];
let a2 = [4, 5, 6];

let mut iter = a1.iter().zip(a2.iter());    // —> [ Some((&1, &4)), Some((&2, &5)), Some((&3, &6)) ]
```
			
- **`.skip(n)`** — creates an iterator that skips the first n elements. skip(n) skips elements until n elements are skipped or the end of the iterator is reached (whichever happens first). After that, all the remaining elements are yielded. In particular, if the original iterator is too short, then the returned iterator is empty. <ins>Example:</ins>

```Rust
let a = [1, 2, 3];

let mut iter = a.iter().skip(2);    // skip 1 and 2 so the next element is 3

assert_eq!(iter.next(), Some(&3));       
assert_eq!(iter.next(), None);
```

<br>

2. **<ins>Consumers</ins>** — **Take in an iterator and return some other type such as an integer, collection, or any other type.**

- **`.sum()`** — `sum()` will repeatedly call the `next()` method to get each element in the sequence and then add those elements up and return the sum. <ins>Example:</ins>

```Rust
let v1 = vec![1, 2, 3];

let total: i32 = v1.iter().sum();	// requires type annotation 
					// `total` = 6
```

- **`.collect()`** — transform the iterator into a collection


## Implementing Our Own Iterator

<ins>Example:</ins> Here, we create an iterator that counts from 1 to 5...

```Rust

struct Counter {
    count: u32,	// `count` field keeps track of where we are in the process of iterating from 1 to 5.
    		// Private bc we want the field to only be accessed by our implementation block.
}

impl Counter {
    fn new() -> Counter {	// Constructor to create a new `Counter` with a `count` set to 0. This enforces that
    				// every time a new `Counter` is created, `count` gets initialized to 0 (bc `count` field
				// is private, so `Counter`'s can only be instantiated with this `new()` associated function).
        Counter { count: 0 }
    }
}

// Implement the `Iterator` trait for `Counter`
// 
impl Iterator for Counter {
    type Item = u32;	// `Item` associated type set to unsigned 32-bit int. Says that our `Iterator` is
    			// going to return items of type u32. 

    // `next()` is the only method we're required to implement for the `Iterator` trait...
    //   - takes a mutable reference to `self`
    //   - returns an `Option` enum which holds the next item or None if reaches the end
    //
    fn next(&mut self) -> Option<Self::Item> { 
        if self.count < 5 {	// If `self.count < 5`, then we increment `self.count` and return it (bc not at 5 yet).
            self.count += 1;
            Some(self.count)
        } else {	// If `self.count >=5`, then return None bc we're at the end of our iteration.
            None
        }
    }
}

#[test]
fn calling_next_directly() {
    let mut counter = Counter::new();

    // call `next()` six times, first five calls expect to get a number in the sequence bc iterating from 0 -> 5
    assert_eq!(counter.next(), Some(1));
    assert_eq!(counter.next(), Some(2));
    assert_eq!(counter.next(), Some(3));
    assert_eq!(counter.next(), Some(4));
    assert_eq!(counter.next(), Some(5));
    assert_eq!(counter.next(), None);	// sequence is over
}

// The standard library provides default implementations for a lot of other methods on our `Iterator`…
// Example test using these default implementations…
//
#[test]
fn using_other_iterator_trait_methods() {
    // Create a variable called `sum` which is an integer equal to this long expression...
    let sum: u32 = Counter::new()	// Create a new `Counter`.

        .zip(Counter::new().skip(1))	// Zip up the `Counter` we created with another `Counter` that 
					// skips the first element.

        .map(|(a, b)| a * b)		// Call `map` on the zipped up `Iterator` to multiply each pair (tuple) 
					// of values together then return the `Iterator` with these products.

        .filter(|x| x % 3 == 0)		// Filter the `Iterator` to only items that are divisible by 3.

        .sum();				// Sum the items in the `Iterator`.

    assert_eq!(18, sum);
}
```

^^^This example shows that simply implementing the `next()` method gives us access to all these other methods that have default implementations in the standard library.

# Iterators in Practice

- Improving our minigrep (CLI) project with iterators.

### Removing the Use of `clone()` by Using Iterators

- **<ins>OLD CODE:</ins>** We **`clone()`** strings in `Config::new()` which is **inefficient**, but we have no choice… as explained below…

<ins>main.rs</ins>
```Rust
fn main() {
    let args: Vec<String> = env::args().collect();	// `args()` returns an iterator over our command line
							// arguments, but we call `collect()` to turn it into a
							// a vector of `Strings`.

    let config = Config::new(&args).unwrap_or_else(|err| {	// We pass a reference to our vector
								// of Strings into `Config::new()`.

        eprintln!("Problem parsing arguments: {}", err); 
        process::exit(1); 
    });

    …
    …
    …
}
```

<ins>lib.rs</ins>
```Rust
pub struct Config {
    pub query: String,
    pub filename: String,
    pub case_sensitive: bool,
}
impl Config {
    pub fn new(args: &[String]) -> Result<Config, &str> {
        if args.len() < 3 {
            return Err("Not enough arguments");
        }
        // PROBLEM: cloning the strings here is inefficient, but we have to do this because `args` above is
        //          a reference to an array, so we can’t take ownership of the strings. TO FIX THIS, instead
        //	    of taking an array reference / slice for `args`, let’s take in an iterator, which we have 
        //	    ownership over, which also means that we have ownership over its contents. This way
        //          we can remove the `clone()` operation here. 
        // 
        let query = args[1].clone();
        let filename = args[2].clone();

        let case_sensitive = env::var("CASE_INSENSITIVE").is_err();

        Ok(Config { query, filename, case_sensitive})
    }
}
```

- **<ins>NEW CODE:</ins>** **Don’t have to call `clone()` in `Config::new()` because we pass in an iterator for `args`**. When we call `args.next()`, we get a `Some()` variant and the `String` inside `Some()` is an own `String`, and we then pass this own `String` into a `query` variable, so the `query` variable is now taking ownership of the `String`. The same goes for `filename` — the `filename` variable is taking ownership of its `String`. We then pass the `query` and `filename` variables into a `Config` instance, so the `Config` instance takes ownership of the `query` and `filename` strings.

<ins>main.rs</ins>
```Rust
fn main() {
    let config = Config::new(env::args()).unwrap_or_else(|err| {	//  Pass the iterator returned from `args()`
 									//  straight into `Config::new()`
        eprintln!("Problem parsing arguments: {}", err); 
        process::exit(1); 
    });

    …
    …
    …
}
```

<ins>lib.rs</ins>
```Rust
pub struct Config {
    pub query: String,
    pub filename: String,
    pub case_sensitive: bool,
}
impl Config {

    // `new()` now takes in the `args` iterator (type is `env::Args`)
    // Also, make `args` mutable because we iterate over the iterator using `next()`
    //
    // We know from the lifetime elision rules that each parameter that is a reference gets its own lifetime  
    // parameter. Before, we had one parameter (a reference to an array), so this will get a lifetime parameter
    // since it's a reference. We also know from the elision rules that if there is exactly one input lifetime 
    // parameter, that lifetime is assigned to all output lifetime parameters. Thus, the lifetime of the array 
    // reference (`args`) was assigned to all the output lifetime parameters, so we didn't have to specify 
    // lifetime annotations. Now, though, `args` is an own type (we changed it to an iterator), so it doesn't get a 
    // lifetime parameter, but we are still returning a string slice for the error part of the `Result` enum. As a 
    // result, we have to specify the lifetime of the string slice. Here, we set our lifetime to a `static` lifetime, 
    // which makes sense because the string slice we return in the `Error` variant is the error message which 
    // will live for the duration of the program, hence the `static` lifetime. 
    //
    pub fn new(mut args: env::Args) -> Result<Config, &'static str> {	

        args.next();	// the first command line argument is the path to our program, which we don't care
			// about, so essentially just discard / skip it here.

        // `next()` returns an `Option` enum, which we match over.
        //     - If we have a valid argument in `next()`, then we extract it from `Some()` and return it
        //     - Otherwise, return an error specifying that we didn't get the `query` string
        //
        let query = match args.next() {               
            Some(arg) => arg,                        
            None => return Err("Didn't get a query string”),
        };

	let filename = match args.next() {
            Some(filename) => filename,
            None => return Err("Didn't get a filename")
        };

        let case_sensitive = env::var("CASE_INSENSITIVE").is_err();

        Ok(Config { query, filename, case_sensitive})
    }
}
```

### Simplifying `search()` Using Iterator Adaptor Functions

**<ins>OLD CODE:</ins>**
```Rust    
fn search<'a> (query: &str, contents: &'a str) -> Vec<&'a str> {
    let mut matches = Vec::new();
    for line in contents.lines() {
        if line.contains(query) {
            matches.push(line);
        }
    }
    matches
}
```

**<ins>NEW CODE:</ins>**
```Rust
fn search<'a> (query: &str, contents: &'a str) -> Vec<&'a str> {
    contents 
        .lines()	// `.lines()` creates an iterator over all the lines in our `contents` string

        .filter(|line| line.contains(query))	// filter to only lines that contain the `query` string

        .collect()	// `collect()` consumer method turns the iterator returned from `filter()` into a collection.
			// Here, Rust knows what type of collection we want bc it's specified as the return type  
}
```

### Should I Use Loops or Iterators?

- **There is no added performance hit for using iterators.** Rust follows the zero cost abstraction principle which means that using higher level abstractions like iterators over loops doesn’t have a meaningful impact in terms of performance. So, **using loops or using iterators is about the same in terms of speed.**

- **Comes down to preference.** **Rust engineers tend to prefer iterators**, because it’s a higher level of abstraction and you get access to all of the nice default standard library methods like map() and filter(). 

---

# Publishing a Rust Crate

**Release Profiles** -- Allow you to configure how your code is compiled. Cargo has two main profiles:

1. **Dev:** Defined with good defaults for development.
    - The dev build is optimized and contains debug information
    - If we run `cargo build`, then our code will compile with the dev profile

<img width="521" alt="Image" src="https://github.com/user-attachments/assets/13c3ef58-e1c2-446e-957c-0351eae19fb8" />

<br>2. **Release:** Defined with good defaults for a release build
    - The release build is **optimized**
    - If we want to compile our code with the release profile, then we’ll type in `cargo build --release`

<img width="527" alt="Image" src="https://github.com/user-attachments/assets/9525f3cb-b292-4121-9889-22e711fcc323" />

<br>**We can also customize the settings in the Cargo.toml file…** In the below, we add two sections for the dev and release profiles. We also add the `opt-level` setting, which stands for optimization level. The optimization level can be 0, 1, 2, or 3. 0 being no optimizations and 3 being the highest number of optimizations. In the below, we keep the default settings…

- **Dev**: The dev profile will have an `opt-level` of 0 because we are going to be compiling a lot so we want our compilation speed to be fast, and that trades off the runtime speed —> **fast compile time but slower runtime.**

- **Release**: The release profile will have an `opt-level` of 3 because we are only going to be compiling once and running the program many times. So, we’ll **exchange a slower compile time for a faster runtime.** 

^^^But these `opt-level` settings are customizable in the below…

**<ins>cargo.toml</ins>**
```Rust
[package]
name = "my_crate"
version = "0.1.0"
edition = "2024"

[dependencies]

[profile.dev]
opt-level = 0	// can change this to set `opt-level` to something else, like 1, for the dev profile

[profile.release]
opt-level = 3
```

^^^NOTE: to get a full list of settings beyond just `opt-level`, see cargo’s documentation

## Preparing Your Code for Public Consumption

1. **Writing Useful Documentation Comments** — comments are useful when documenting your public API so that others know how to use your code.

    - **Regular comments** start with two slashes  `//` 

    - **Documentation comments** start with three slashes  `///`  and **use markdown for formatting**. Rust also turns your documentation into an HTML format that’s easy to read.
   
         - Example: We have a function called add1() which takes in an integer and adds 1 to it, then returns the new integer…. **Right above the function, we have a documentation comment**… this is defined in **lib.rs** :
     
```Rust
/// Adds one to the number given. -> (at the top of the documentation, explain what the function does)
/// 
/// # Examples -> (example section which gives an example of how to use the function)
/// 
/// ```
/// let arg = 5; -> (code block to show how to call the function, incl. line below)
/// let answer = my_crate::add_one(arg);
/// 
/// assert_eq!(6, answer); -> (assert statement that asserts that we get back the correct value. Bc we
///			       have this assert_eq!() statement, Rust runs this documentation
///			       comment as a documentation test when you run “cargo test”, as shown
///			       below… of course, we delete all these parenthesis comments b4 running)
/// ```
pub fn add_one(x: i32) -> i32 {
    x + 1
}
```
**Running `cargo test` to see the result of the Documentation test**… this feature is great because **it forces the documentation to be in sync with the code**! If, for example, we changed our function to add 2 instead of 1, then our documentation test fails. 

<img width="670" alt="Image" src="https://github.com/user-attachments/assets/43d641ed-683a-4c53-bbc8-0ea4bb36362f" />

<br>**In order to build the HTML documentation for our crate…   `cargo doc --open`**
- NOTE: `--open` is not required, it just opens a web browser with our documentation which is convenient
- <ins>Result of running `cargo doc —open` with the above example with `add_one()`…</ins>

<img width="618" alt="Image" src="https://github.com/user-attachments/assets/edf0ff41-0f1c-4514-b74c-0c9be2a10b23" />

<br>**Below, we have the web page Rust generated.** It **shows the name of our crate (“my_crate”) and then a list of functions in our crate**, which is currently just `add_one()`. NOTE: I deleted all of the parenthesis comments before opening this…

<img width="726" alt="Image" src="https://github.com/user-attachments/assets/1004022d-03c8-4b4e-931b-9110bcabb2e8" />

**If we click into the add_one() function on the web page, then we can see the function signature and the "Examples" section…**

<img width="731" alt="Image" src="https://github.com/user-attachments/assets/feda7f3c-8767-4cd1-bc86-3b49d72edcf6" />

<br>**Besides “Examples”, there are a few other commonly used sections…**

1. **Panics** — describes scenarios in which the function being documented could panic. Callers of the function who don’t want their programs to panic should make sure they don’t call the function in these situations. 

2. **Errors** — if the function returns a Result type. Use to describe the kinds of errors that might occur and what conditions might cause those errors to be returned. Helpful to callers so they can write code to handle the different kinds of errors in different ways. 

3. **Safety** — if the function is “unsafe” to call, there should be a section explaining why the function is unsafe and covering the invariants that the function expects callers to uphold.

## `//!` Comments

This style of comment **documents the item containing the comment** instead of documenting the item following the comment. 

- <ins>Example:</ins> The `//!` is inside of **lib.rs**, so it is **documenting our library crate.**

```Rust
//! # My Crate
//! 
//! `my_crate` is a collection of utilities to make performing certain
//! calculations more convenient.

/// Adds one to the number given.   (This and below is the same as our earlier documentation) 
/// 
/// # Examples
/// ...
```

**`cargo doc --open`** => 
<img width="714" alt="Image" src="https://github.com/user-attachments/assets/bb731f59-7a87-405e-9473-da8087f4cb62" />

## Re-Exporting / Exporting a Public API

**<ins>lib.rs</ins>** 
```Rust
//! # Art
//!
//! A library for modeling artistic concepts.

pub mod kinds {
    /// The primary colors according to the RYB color model.
    pub enum PrimaryColor {
        Red,
        Yellow,
        Blue
    }

    /// The secondary colors according the RYB color model.
    pub enum SecondaryColor {
        Orange,
        Green,
        Purple,
    }
}

pub mod utils {
    use crate::kinds::*;

    /// Combines two primary colors in equal amounts to create
    /// a secondary color.
    pub fn mix(c1: PrimaryColor, c2: PrimaryColor) -> SecondaryColor {
        // --snip--
        // ANCHOR_END: here
        SecondaryColor::Orange
        // ANCHOR: here
    }
}
```

**<ins>main.rs</ins>**
```Rust
use my_crate::kinds::PrimaryColor;	// PROBLEM: We want users to have access to the enums (`PrimaryColor`
					// and `SecondaryColor`) and the `mix()` function at the top level without
					// having to reference their respective modules —> re-export
use my_crate::utils::mix;

fn main() {
    let red = PrimaryColor::Red;
    let yellow = PrimaryColor::Yellow;
    mix(red, yellow);
}
```


<br>**<ins>IMPROVED CODE:</ins>**

**<ins>lib.rs</ins>** — Add the following to **re-export** the **enums (`PrimaryColor` and `SecondaryColor`) and the `mix()` function.** 

```Rust
pub use self::kinds::PrimaryColor;
pub use self::kinds::SecondaryColor;
pub use self::utils::mix;
```

^^^Now, **`PrimaryColor`, `SecondaryColor`, and `mix` will be exported from the top level of our library.** This means that **`PrimaryColor`, `SecondaryColor`, and `mix` are directly accessible via `use my_crate::...`**. So, instead of having to write `use my_crate::kinds::PrimaryColor;`, we can now simply write **`use my_crate::PrimaryColor;`. No need for `::kinds`**. 

**<ins>main.rs</ins>** 
```Rust
use my_crate::PrimaryColor;	// Now, we can import our items from the top level of our library.
use my_crate::mix;
```

Also, **when we look at the docs now, we can see the re-exports…**

<img width="399" alt="Image" src="https://github.com/user-attachments/assets/af78140a-b5c5-4f8c-b50c-ef05014eb8ff" />

Takeaway: pub use statements allow you to make your public API different from the internal structure of your program, which could be very useful for people consuming your library.

## Publishing to crates.io

1. Login to **crates.io** with GitHub account, verify email address.

2. Click dropdown next to your profile icon and go to account settings. Then, go to API tokens and generate a new API token. <ins>Copy the API token:</ins> **`cio79T7s4n0CSnlgmj863r9GIgoiMhBrgWg`**.

3. Run **`cargo login`** and **paste the key when prompted**.

<img width="436" alt="Image" src="https://github.com/user-attachments/assets/106243e5-0b2c-4ffe-a67c-3aca8261826f" />

4. Double-check the metadata, which is located in cargo.toml.
   
    - **name**: when you develop locally the name doesn’t matter, but when you publish to crates.io, the **name must be unique**. So, go to crates.io, and check if your desired name has already been taken. <ins>SO, in our example</ins>, I changed the name from "my_crate" to "kirin_art".
      
    - **Add description and license**

```Rust
[package]
name = "kirin_art"
version = "0.1.0"
edition = "2024"
description = "A library for modeling artistic concepts."
license = "MIT"
```

5. Add and commit changes (`git add .` and `git commit -m ""`)

6. **`cargo publish`**

<img width="740" alt="Image" src="https://github.com/user-attachments/assets/2f0c94bd-2096-4831-a38f-b4cacc2ec228" />

<img width="733" alt="Image" src="https://github.com/user-attachments/assets/51bf601b-ad4b-4391-82ca-fe5321d987ca" />

^^^NOTE: **Publishing to crates.io is permanent** — now that this **code is published, it cannot be deleted.** I can publish new versions, but the code as it is right now will be forever on crates.io. 
- crates.io does it this way because others may rely on your library and we don’t want to break them by deleting or modifying the code.

**When you want to upload a new version of your library to crates.io, simply change the version number in cargo.toml using the semantic versioning rules, and run `cargo publish` again**.

## Removing Versions from crates.io 
You can’t delete or modify your code once it’s up on crates.io, but **you can stop specific versions from continuing to be downloaded**. You can do this using the **`cargo yank`** command. For example, **if we didn’t want version “0.1.0” to be downloaded anymore**, then we would type in **`cargo yank --vers 0.1.0`**.

- What this does it for **anyone with this version in their `Cargo.lock`**, they **can continue to keep downloading this version**; however, **those downloading our library for the first time won’t be allowed to download this specific version.**
  
- If you’ve yanked a specific version and you want to **undo** it: **`cargo yank --vers 0.1.0 --undo`**.

---

# Cargo Workspaces

**What happens if a project grows beyond just one binary crate and one library crate to include multiple library crates?** In this case, **cargo workspaces** help you organize your project. 
- **Workspaces help you manage multiple related packages that are developed in tandem.**
- **Packages in a workspace share common dependency resolution by having one `Cargo.lock` file**.
- **Packages in a workspace share one output directory and various settings such as profiles.**

<br><ins>Example:</ins> **Create a workspace with 1 binary (`main.rs`) that depends on two libraries.** The first library will have an `add_one()` function and the second library will have an `add_two()` function. 
	
1. **Create a new `add` directory and `cd` into it**. Open in VSCode.

**`mkdir add`**

**`cd add`**

**`code .`**
	
2. Add a **`Cargo.toml`** file which **will configure the entire workspace…**
    - Instead of having a package section like usual, we **create a `workspace` section**. 
    - Also, we have a **workspace `members`** section to specify the packages in our workspace (i.e., we specify the paths to our packages in this section). 

<img width="404" alt="Image" src="https://github.com/user-attachments/assets/1ec62971-b6a3-41df-8553-1e7fb276f66b" />

3. **Create our binary, called `adder` here**. Thus, we specify its path as `adder` in the members section.

**`cargo new adder`**

<img width="406" alt="Image" src="https://github.com/user-attachments/assets/4b1d7d50-a47d-4d99-a9b0-092780ff34ac" />

4. **Build our workspace by running `cargo build` from the `add` directory (the root of our workspace**, this is the original directory we created). This will **generate `Cargo.lock` and the `target` directory in `add`**. Also, when we look at the `adder` directory containing our binary (we created this in the previous step), we will see that it doesn’t have a `Cargo.lock` file or a target directory. 

**`cargo build`**

<img width="211" alt="Image" src="https://github.com/user-attachments/assets/0d63b29e-1096-41f2-b276-f1f5525b3527" />

^^^^Even if we ran `cargo build` from the `adder` directory, we would still see the output in the top level target directory. Cargo uses this structure because packages in a workspace are meant to depend on each other. If each package had its own target directory, then when you compile a package, you would have to also compile all its dependencies — so this reduces the amount of recompilation you have to do. 

5. **Add a second package (or member) to our workspace called `add-one`**. This is a **library** so we have to specify `--lib` when we create it.
	
**`cargo new add-one --lib`**

<img width="406" alt="Image" src="https://github.com/user-attachments/assets/d9445d20-e471-4692-80eb-5bb87367f6b0" />

6. **Add a public `add_one()` function to the `src/lib.rs` file in `add-one`.**

```Rust
pub fn add_one(x: i32) -> i32 {
    x + 1
}
```

7. We **can now use the public `add_one()` function from the `add-one` library from within the `adder` binary we created in step 3**. To do so, we need **go to the `Cargo.toml` file within the `adder` directory and specify that our `adder` binary depends on our `add-one` library**. So, we **specify the `add-one` library as a dependency in the `adder` binary’s `Cargo.toml` file**. Cargo doesn’t assume that crates within a workspace depend on each other, so we have to make this relationship explicit.

```Rust
[dependencies]
add-one = { path = "../add-one" }
```

<img width="566" alt="Image" src="https://github.com/user-attachments/assets/1ee231b3-38d6-4d86-a4d2-82dd5586b733" />

8. **Use the public `add_one()` function from the `add-one` library in `src/main.rs` in the `adder` binary.**

<img width="689" alt="Image" src="https://github.com/user-attachments/assets/10e2271f-e393-4f05-b419-e7a611425b6c" />

9. **Build our workspace by running `cargo build`** at the root of our workspace (within `add`). Then, **run the `adder` binary from the root of our workspace**… use `-p` to specify the package we want to run

`cargo run -p adder` —> Hello, world! 10 plus one is 11!

10. **<ins>External Dependencies</ins>** — We have `Cargo.toml` files for both the `add-one` library and the `adder` binary. This can be seen in the screenshot for step 7. However, we only have one `Cargo.lock` file in the root of our workspace. This ensures that all of our crates are using the same version of all dependencies. So, if we add a dependency to our `add-one` package and we add the same dependency to our `adder` package, they will both resolve to the same version. Making all packages in a workspace use the same dependencies ensures that the packages are compatible with each other.

	- <ins>Example</ins> — we **add `rand` as a dependency to `add-one`**

<img width="210" alt="Image" src="https://github.com/user-attachments/assets/691efb89-7040-47f8-be64-c0547223e484" />

Then, after we run **`cargo build`**, this will **bring in and compile the `rand` crate**, and we **can see the `rand` crate as a dependency in `Cargo.lock` at the root of our workspace.**
<img width="631" alt="Image" src="https://github.com/user-attachments/assets/39f0b7a7-d735-4c3a-9683-eeaa37b6849c" />

NOTE: We can’t yet, though, use `rand` in any other package in the workspace. For example, we can’t use it in `adder`. We have to add `rand` as a dependency of the `adder` package in its `Cargo.toml` file. 

11. **<ins>Adding a Test to a Workspace</ins>** — We now **add a test module and one test in `lib.rs` in the `add-one` library.**

<img width="665" alt="Image" src="https://github.com/user-attachments/assets/b363f4df-4cf4-499c-8719-30aa8c96a1a3" />

To run the test, we run **`cargo test`** from the **root of our workspace** (`add` folder). 

<img width="729" alt="Image" src="https://github.com/user-attachments/assets/d541ef85-f1ef-41ea-b63c-1171c0f82308" />

^^^ **Running `cargo test` at the root of our workspace will run tests for all the projects within that workspace**. If we want to **run tests for a specific project**, we can do that by specifying **`-p`**. 

**`cargo test -p add-one`**

<br>12. **Add another library: `add-two`**

- Create the `add-two` library by running this command at the root of the workspace: **`cargo new add-two --lib`**

- Add a public `add_two()` function to `src/lib.rs` in the `add-two` library.
  
<img width="551" alt="Image" src="https://github.com/user-attachments/assets/7475bad2-116b-4559-b492-974bbe134a55" />

- Add the `add-two` library as a dependency in the `Cargo.toml` file of the `adder` binary:

<img width="537" alt="Image" src="https://github.com/user-attachments/assets/d6a25b90-43b2-4155-8992-4d25d647dd1d" />

- Use the public `add_two()` function from the `add-two` library in `src/main.rs` in the `adder` binary.

<img width="614" alt="Image" src="https://github.com/user-attachments/assets/b64d66f7-4962-4f87-9a66-3950074bd28e" />

- **Build our workspace by running `cargo build` at the root of our workspace** (within `add`). **Run the whole workspace with `cargo run` or just the binary with `cargo run -p adder`**.

<img width="558" alt="Image" src="https://github.com/user-attachments/assets/d52849a1-286b-4a3e-9aad-e1b064eb8add" />

- Can also add tests to `src/lib.rs` in the `add-two` library

<ins>NOTE:</ins> **If you want to publish the packages within a workspace, you have to publish them individually**. Meaning you’ll have to `cd` into each package (e.g., `adder`, `add-one`, `add-two`) and then run `cargo publish` from their respective directories. 

## Installing Binaries from crates.io with `cargo install`

This **isn’t meant to be a replacement for system packages or package managers such as homebrew**. Rather, it’s a **convenient way for Rust developers to use tools built by other Rust developers and publish to crates.io.**

- <ins>NOTE:</ins> you **can only install packages that have a binary target** bc you need something you can actually execute (remember packages can have binary targets and library targets)
  
- All binaries installed using the **`cargo install`** command are **stored inside the installation route’s bin directory**. Need to **add path to bin directory** `$HOME/.cargo/bin` **inside path environment variable**.

- <ins>Example:</ins> Rust installation of `grep` called `ripgrep`

	- Install `ripgrep` using **`cargo install ripgrep`**

<img width="566" alt="Image" src="https://github.com/user-attachments/assets/508b72a6-7051-4e49-b880-b66258b7e382" />

 ^^^Highlighted line shows where the binary is installed

 - To use the tool, **`rg --help`**.

## Extending Cargo with Custom Commands

You can **use the binaries installed with `cargo install` to extend cargo with custom commands…**

- If you have a **binary in your path that’s prefixed with `cargo`** (e.g., **`cargo-something`**), then you **can run this as a sub command of cargo by typing `cargo something`**. Cargo is designed this way so you can extend cargo without actually modifying cargo’s code.

---

# Smart Pointers in Rust

**<ins>Pointer</ins>** — **a pointer is a general concept for a variable that stores a memory address. The memory address refers to (or points to) some other data in memory.** You can think about pointers as an arrow pointing to a value stored in somewhere in memory. 

## References

**The most common pointer in Rust** is a **<ins>Reference</ins>**. 

- **References simply borrow the values they point to, meaning that they don’t have ownership over the values.**

- References don’t have any special capabilities, which also means they don’t have much overhead, unlike smart pointers

## Smart Pointers Introduction

**<ins>Smart Pointers</ins>** are **data structures that act like a pointer but have metadata and extra capabilities tacked on.**

- <ins>Ex:</ins> <ins>reference counting smart pointer</ins> — allows a piece of data to have multiple owners by keeping track of the owners, and once there are no more owners, cleaning up the data.

- **In many cases, smart pointers own the data that they point to**, unlike references which simply borrow the values.

- We’ve already encountered smart pointers — **`Strings`** and **`Vectors`**. **Both of these types are smart pointers because they own some data and allow you to manipulate it, they store extra metadata such as the capacity, and they have extra capabilities** (e.g., the String type ensures that the data is valid UTF-8).

- **Smart pointers are usually implemented using structs**. BUT, unlike regular structs, they implement the **`Deref`** and **`Drop`** traits.

    - **`Deref` trait:** Allows instances of your smart pointer struct to be treated like references. So, you can write code which works with both references and smart pointers. 
    - **`Drop` trait**: Allows you to customize the code that is run when an instance of your smart pointer goes out of scope.
 
- Smart pointers are a general design pattern used frequently in Rust.

- Many libraries implement their own smart pointers, so we won’t be covering every single smart pointer out there; instead, we’ll be covering the most common smart pointers used within the Rust standard library.

## Smart Pointer Summary (IMPORTANT!!!)

**<ins>Reference Counting smart pointer</ins>:**   **`Rc<T>`**

- **Heap-allocated type**. **Similar to `Box`, but the `T` value allocated on the heap is accompanied by two reference counts**. They allow value sharing, which can be an effective way to reduce memory usage.
  
- Enables **multiple owners (shared ownership) of the same data.**

	- **Create a new owner using** **`Rc::clone()`**. **When you clone an `Rc<T>`, the reference count increases. The data is only dropped when the last `Rc<T>` pointing to it is dropped.**
  
- Allows **only immutable borrows checked at compile time**.
  
- Internally stores a **strong count** (# references that have ownership of the data) and **weak count** (# references that don’t have ownership. A **value is dropped when its strong count is 0**, the weak count has no influence over whether the underlying value is dropped or not.
  
- <ins>NOTE:</ins> The **`Weak`** smart pointer is a version of the Reference Counting smart pointer (`Rc`) that holds a non-owning reference to the managed allocation. For more information see later section.

<br>**<ins>Box smart pointer</ins>**:   **`Box<T>`**

- **Heap-allocated type**. A `Box<T>` value is a `T` value that is allocated on the heap. So, allocates memory on the heap.
  
- Allows **single ownership** to a piece of data
  
- Allows **immutable or mutable borrows checked at <ins>compile time</ins>** (i.e., enforces the borrowing rules at compile time). This means that if you want the value inside of a `Box` smart pointer to be mutable, then the `Box` smart pointer itself has to be mutable (see below how this is different for `RefCell`).

<br>**<ins>RefCell smart pointer</ins>:**   **`RefCell<T>`**

- Allows **single ownership** to a piece of data
  
- Allows **immutable (`.borrow()`) or mutable borrows (`.borrow_mut()`) checked at <ins>runtime</ins>** (i.e., enforces the borrowing rules at runtime). Because `RefCell<T>` allows mutable borrows checked at runtime, **you can mutate the value inside the `RefCell<T>` even when the `RefCell<T>` smart pointer itself is immutable (i.e., provides interior mutability).**
  
- `RefCell` itself **does not allocate any memory on the heap**. It's a **mechanism for mutability within a type that is otherwise immutable**, and it works without requiring heap allocation. If you put a `RefCell` inside a `Rc` or `Box`, then the `Rc` or `Box` will allocate on the heap, but the `RefCell` itself doesn't (i.e., If you put a `RefCell` inside another heap-allocated type, like `Box<RefCell<T>>` or `Rc<RefCell<T>>`, then the `RefCell` (and its contents) will reside on the heap as part of that larger allocation). 

## IMPORTANT DISTINCTION: `Rc<RefCell<T>>` vs. `RefCell<Rc<T>>`

**`Rc<RefCell<T>>`** **(The Common Pattern for Shared, Mutable Data)** — example above uses this.

- When you see `Rc<RefCell<T>>`, it signifies that **the entire structure `RefCell<T>` is shared among multiple owners**.

- The **outer `Rc` (Reference Counter) enables multiple parts of your program to hold shared ownership of the same `RefCell<T>`**. You can clone this `Rc` to create more pointers, all referencing (sharing ownership of) the exact same internal `RefCell` instance.

- The **inner `RefCell<T>` provides interior mutability**. **While `Rc` itself, by default, provides only shared and immutable access to its contents, the `RefCell` allows any of the `Rc` owners to obtain a mutable borrow of the contained `T` at runtime.**

    - `RefCell` still enforces Rust's core borrowing rules at runtime: you can have either one mutable borrow OR any number of immutable borrows, but never both simultaneously. If you attempt to violate this rule (e.g., by calling `borrow_mut()` twice, or `borrow_mut()` while a `borrow()` is active), the program will panic at runtime.

- <ins>Summary in simple terms:</ins> **Usually, you use `Rc<RefCell<T>>`**; the **whole thing is shared and each shared owner gets to mutate the contents `T`**. The **effect of mutating the contents will be seen by all of the shared owners of the outer `Rc` because the inner data is shared.**

<br>**`RefCell<Rc<T>>` (less useful, rarely used)**
- The **outer `RefCell` means that you have a single `RefCell` that you can mutably borrow from**. In this way, you **have `&mut Rc<T>`, so you can change the `Rc<T>` itself**. **HOWEVER**, You **cannot directly change the `T` that the `Rc` points to** (unless `T` itself uses interior mutability). So, while you can "change the inside value" of a `RefCell<Rc<T>>`, what you're changing is the `Rc<T>` itself (the shared pointer), not the data `T` that the `Rc` points to.

- **The `RefCell` cannot inherently be shared among multiple owners** (shared ownership) in the same way `Rc` allows; you'd **need to wrap this entire structure in an `Rc`** if you wanted to share it (i.e., `Rc<RefCell<Rc<T>>>`), which gets overly complex.

- The **inner `Rc<T>` is a shared pointer to some data `T`**.

- <ins>Summary in simple terms:</ins> You **can't share a `RefCell<Rc<T>>` except by reference**, so this configuration is more **limited** in how it can be used. In order to mutate the inner data, you would need to mutably borrow from the outer RefCell, but then you'd have access to an immutable Rc. **The only way to mutate it would be to replace it with a completely different Rc.** Far less useful.


## The `Box` Smart Pointer

**`Box`**: **A smart pointer that allows you to allocate values on the heap.**

- <ins>Example:</ins> **Pass the value we want to store on the heap into** the **`Box::new()`** function…

```Rust
let b = Box::new(5);	// Here, we store 5 on the heap. On the stack, we store a pointer (memory address)
			// to the location of 5 on the heap. This pointer is stored in the `b` variable here.

println!("b = {}", b);	// can simply use the `Box` value as if it were a value on the stack
```
^^^THIS IS A CONTRIVED EXAMPLE. Typically you won’t store a single value, like `5`, on the heap. In fact, in this case, storing `5` on the stack would be much more appropriate. So, **typically Boxes ARE NOT used by themselves.**

<br>**Boxes don’t have any overhead except storing the data on the heap**, but they also **don’t have many other capabilities**, so you would <ins>typically use them in the following situations</ins>…

1. **When you have a type whose exact size can’t be known at compile time (e.g., DST) and you want to use a value of that type in a context which requires knowing the exact size.**

2. When you have a **large amount of data and you want to transfer ownership of the data**, but you want to **make sure that the data isn’t copied** (bc it’s a large amount of data). 

3. **<ins>Trait object</ins>**: When you own a value and you only care that the value implements a specific trait, rather than it being a specific type.

Just like any other owned value, **when our `Box` goes out of scope, it will be deallocated**, meaning that the `Box` smart pointer on the stack will be deallocated AND the underlying data on the heap will also be deallocated.

### `Box` Example

<ins>SIDE NOTE TO INTRODUCE EXAMPLE:</ins> **How Rust computes the size of non-recursive enums.**

```Rust
enum Message {
    Quit,
    Move { x : i32, y : 132 },
    Write(String),
    ChangeColor(i32, i32, i32)
}
```
^^^The way Rust will figure out the size needed to store a variant of `Message` is by going through each variant (`Quit`, `Move`, `Write`, `ChangeColor`) and seeing how much size each variant needs (`Quit` doesn’t need any space, `Move` is a struct with two values, `Write` is tuple with one `String`, `ChangeColor` is tuple with three integers). **Rust figures out which variant needs the most amount of space.** Because we **can only use one variant of the `Message` enum at a time, the most space `Message` is going to take up is equal to the space the largest variant takes up.**

<ins>Example where Boxes are actually useful</ins>: **Enabling Recursive Types with Boxes**

- **Rust needs to know how much space a type takes up at compile time**. BUT, <ins>in the below example</ins>, and **in general with recursive enums**, we **don't know how much space the enum could take up**. This is because, in theory, we **could recurse forever**…

```Rust
// Recursive enum called `List` with two variants: `Cons` and `Nil`. In our earlier example about how Rust figures out 
// the size needed to store a variant of the `Message` enum, we looked at the space needed for each variant and 
// took the space the largest variant takes up. To determine the size needed to store a variant of `List`, we have… 
// 	
//	`Cons` takes up some space — it stores a tuple containing a value (`i32`) and a `List`.
//	`Nil` variant takes up no space.
//
// We see now that `Cons` is the variant that takes up the most space, and Rust must determine how much space
// this is. To do so, Rust must now determine how much space `List` takes up — so we’re back again to 
// determining the size needed to store a variant of `List`… recurse infinitely —> no way to tell how big our
// `List` is going to be. TO FIX THIS, we wrap `List` in a `Box` smart pointer, as shown below…
//
enum List {
    Cons(i32, Box<List>),	// `Cons`: Tuple that contains an element and a pointer to the
				// next node (see full explanation below).
				//
				// Recursive type with infinite size. This is bc in the `Cons` variant, the `List` value in
				// the tuple is recursive without indirection bc we could recurse forever. To add
				// indirection, we wrap `List` inside the `Box` smart pointer: `Box<List>`. Indirection
				// here means that instead of storing the `List` value directly, we store a pointer to the
				// `List` value.
				//
				// FURTHER EXPLANATION OF WHY `Box` FIXES THIS ERROR: let’s try to figure out the
				// size of `List` again… look at each variant and see how much space each takes up:
				//
				// 	`Cons` variant takes up some space — it stores a tuple containing a value (i32)
				//		and it now stores a `Box` smart pointer. The `Box` smart pointer is going to be
				// 		a fixed size pointer (so it is fixed size on the stack), and it’s going to point
				//		to some arbitrary amount of data on the heap.  THUS, we now know
				// 		exactly how much space we need for the `Cons` variant — Prob solved!
				//
				// 	`Nil` takes up no space again

        Nil,	// `Nil` denotes end of the list (i.e., last node's next pointer points to Null)
}

use List::{Cons, Nil}; // bring the variants of `List` into scope

fn main() {
    let list = Cons(1, Box::new(Cons(2, Box::new(Cons(3, Box::new(Nil))))));
}
```
^^^THIS specific enum is called a **`Cons` List**. The `Cons` List is a data structure that comes from the programming language Lisp and its dialects. 

- In these Lisp languages, pairs (nodes of linked lists) are used as the fundamental building blocks of data structures. Here is one way to create the 1,2,3 list in Common Lisp: `(cons 1 (cons 2 (cons 3 nil)))`.

- In Rust, `Cons` is a variant of the `List` enum. **The `Cons` variant represents a non-empty node in a linked list and holds two pieces of data: a `u32` and a `Box<List>`**. **The `u32` is the value stored in the node (e.g., 5) and the `Box<List>` is a “next” pointer to the next node in the linked list.** Note that we could have the value be a generic type instead of a `u32`. The `Nil` variant represents Null (i.e., last node in the linked list points to None). Image of this:

<img width="212" alt="Image" src="https://github.com/user-attachments/assets/3a3a14e6-70a2-4cbf-8458-e85fb5471fd5" />

<ins>First node above:</ins> `Cons(42, next pointer to the next node in the linked list which contains 69)`

<ins>Second node above:</ins> `Cons(69, next pointer to the next node in the linked list which contains 613)`

<ins>Third node above:</ins> `Cons(613, Nil)`   —> `Nil` bc this is the last node in the linked list so next is None 

^^^**writing the full linked list out, we have**:   `Cons(42, Cons(69, Cons(613, Nil) ) )`

- Although functional programming languages use `Cons` lists (linked lists) frequently, it’s **not a data structure that’s commonly used in Rust**. Most of the time, when you have a list of items in Rust, it’s **better to use a Vector**.
  
    - Other more complex recursive data types are useful in Rust in various situations, so using the `Cons` list as an example helps us understand how Boxes allow for recursive data types. 

## `Deref` Trait

As explained in the last section introducing smart pointers, smart pointers are structs that implement the `Deref` trait and the `Drop` trait. 

- The **`Deref trait` allows you to treat pointers like regular references.**
  
- **Without the `Deref` trait, the compiler only knows how to dereference references.**

- The **`Deref` trait allows the Rust compiler to take any value that implements `Deref` and call the `deref()` method to get a reference**, which the **compiler then knows how to dereference.**

- The `Deref` trait allows you to **customize the behavior of the dereference operator `*`.**

<ins>Example 1:</ins> How the dereference operator `*` works with with references...
```Rust
let x = 5;
let y = &x;	// `y` is a reference to `x`, `y` is a memory address (or pointer) that
		// points to the location where `5` is stored.

assert_eq!(5, x);
assert_eq!(5, *y);	// Assert that dereferencing `y` is equal to `5`. The dereference operator
			// follows the memory address stored in `y` to the actual value.

assert_eq!(5, y);	// ERRORS, can't compare an integer to a reference to an integer bc different types.
```

^^^<ins>Example 2:</ins> modifying the above example to use smart pointers (the `Box` smart pointer) instead of references...

```Rust
let x = 5;
let y = Box::new(x);	// `Box` points to the value `5` stored in memory. HOWEVER, this is a copy
			// of `5`, bc when primitives like ints get passed into functions, the value
			// is copied instead of ownership being transferred.

assert_eq!(5, x);
assert_eq!(5, *y);	// We can use the dereference operator `*` the same way bc `Box` is a smart pointer that
			// implements the `Deref` trait, which allows the dereference operator to work the same
			// as if it were a reference
```

### Creating Our Own Smart Pointer that Implements the `Deref` Trait

- We base our smart pointer on `Box`

```Rust
// `Box` is implemented as a tuple struct (i.e., an anonymous struct without named fields) that holds one generic 
// value. The big difference between the `Box` smart pointer in the Rust standard library and `MyBox` is that `x` in 
// `MyBox` is not stored on the heap. This is just for the sake of this example focusing on `Deref`.
//
struct MyBox<T>(T);

impl<T> MyBox<T> {
    fn new(x: T) -> MyBox<T> {
        MyBox(x)
    }
}

use std::ops::Deref;	// bring the `Deref` trait into scope

// Implement the`Deref` trait for `MyBox` so that it can use `*` like a reference.
impl<T> Deref for MyBox<T> {

    type Target = T;	// Associated type called `Target` which is equal to our generic `T`. Associated types are a
			// slightly different way of declaring a generic parameter. See later section (chapter 19).

    // The `Deref` trait requires that we implement one method called `deref()` which takes a reference to `self` and returns a 
    // reference to the inner data, which in this case is going to be `&Self::Target` (or `&T`).
    //
    // In summary, this function's purpose: when the the deference operator `*` is used, we return a reference 
    // to the first and only item stored in our `MyBox` tuple struct. 
    //
    // `deref()` returns a reference instead of the value itself for ownership reasons. If `deref()` returned the 
    // value directly, then Rust would move ownership of the value outside of the smart pointer, and in most 
    // cases when using the dereference operator `*`, we don't want this.
    //
    fn deref(&self) -> &Self::Target { 
        &self.0    // `MyBox` is a tuple struct, so we return `&self.0`, which is a reference to the first item in the tuple.
    }
}

fn main() {
    let x = 5;
    let y = MyBox::new(x);  

    assert_eq!(5, x);
    assert_eq!(5, *y);	// When we use the deference operator on `y`, Rust actually calls: `*(y.deref())`. This
			// code first calls `deref()` on `y` to get a reference, and it then uses the dereference 
			// operator `*` on the reference.
			//
			// ^^^Bc Rust does this automatically, we don't have to think about when we have to
			// use the `deref()` method, so we can treat regular references and types that
			// implement `Deref` the same.
}
```

### Implicit Deref Coercion with Functions and Methods

**<ins>Deref Coercion</ins>** — a convenience feature in Rust that happens automatically for types that implement the `Deref` trait.

- **Deref Coercion will convert <ins>a reference to one type</ins> (A REFERENCE!!! CANT JUST BE AN OWNED TYPE) to <ins>a reference to a different type</ins>.**

- <ins>Example</ins>:

```Rust

fn hello(name: &str) {
    println!("Hello, {}!", name);
}

fn main() {
    let m = MyBox::new(String::from("Rust"));
    hello(&m)	// have to pass `&m` and not `m` because Deref Coercion
		// converts one reference to another reference! Rust will
		// not automatically coerce an owned value
		// (`MyBox<String>`) into a reference (`&str`). Deref coercion
		// only works on references (`&T` to `&U`)
}
```
^^^The above code **works even though we pass `&MyBox<String>` into `hello()` which expects `&str`**.

<ins>In the above example, how do we get from `&MyBox<String>` to `&str` ???</ins>

1. `MyBox<String>` implements `Deref`. If we call `.deref()` on `m`, then we get `&String`. `&MyBox<String>` —> `&String`.

2. The `String` type in Rust standard library also implements `Deref`. If we call `.deref()` on a String, then we get will get back a string slice (`&str`). `&String` —> `&Str`.

3. Rust sees that the type being passed to `hello()` is different than the type expected by the function signature, so it automatically performs these chained `.deref()` calls at compile time to get the correct type.
 
    - If Rust didn’t have automatic deref coercion, then to call `hello()` with `m`, we’d have to write the below code which is harder to read and longer and harder to write…
```Rust
hello(&(*m)[..])   // 1. Dereference `m` to a `String`
		   // 2. Take a reference to a string slice (`&str`) that is the full range of the `String` (`[..]`)
```

<ins>Rust performs deref coercion when it finds types and trait implementations in three cases</ins>:

1. From `&T` to `&U` when `T: Deref<Target=U>` — When going from an immutable reference to another immutable reference.

2. From `&mut T` to `&mut U` when `T: DerefMut<Target=U>` — When going from a mutable reference to another mutable reference

3. From `&mut T` to `&U` when `T: Deref<Target=U>` — When going from a mutable reference to an immutable reference.

	- NOTE: **RUST cannot perform deref coercion when going from an immutable reference to a mutable reference**. This has to do with borrowing rules. See the borrowing rules from earlier. The borrowing rules state that you can either have one mutable reference or any number of immutable references, so you can’t have a mutable reference to a variable if an immutable reference already exists for it. Converting a mutable reference to an immutable reference won’t break that rule (bc go from 1 mutable to 1 immutable). HOWEVER, **converting an immutable reference to a mutable reference would require that the initial immutable reference is the only immutable reference to that piece of data** (otherwise you may end up with mutable reference and immutable 	reference/s), which is something the **borrowing rules cannot guarantee**.

- **Similar to how you use the `Deref` trait to override the dereference operator `*` for immutable references, you can use the `DerefMut` trait to override the dereference operator for mutable references.**

## The `Drop` Trait

- Can be implemented on any type.

- Allows you to **customize the code that is run when a value goes out of scope**.

- **Almost always used when implementing smart pointers.**

    - <ins>For example</ins>, with the `Box` smart pointer, the custom behavior we want when a `Box` goes out of scope is to deallocate the data stored on the heap.
  
    - In some languages, you have to manually free memory or resources when you’re done using an instance of a smart pointer. BUT, **with the `Drop` trait**, this **cleanup happens automatically when a value goes out of scope.** So, you **don’t have to worry about manually cleaning up resources.**

- **<ins>SUMMARY:</ins> The `Drop` trait combined with Rust’s ownership system means that you don’t have to worry about cleaning up resources and memory because Rust will do it automatically.**

- <ins>Example:</ins>
```Rust
// struct which represents a smart pointer that stores a `String`
struct CustomSmartPointer {
    data: String,
}

// Implement the `Drop` trait for our struct — NOTE: unlike `Deref`, the `Drop` trait is included in the prelude so already in scope.
//
// The `Drop` trait requires that we implement one method called `drop()` which takes a mutable reference to
// `self`. Inside the method is the cleanup code that runs when an instance of `CustomSmartPointer` goes out
// of scope - here this is just printing something out.
// 	
impl Drop for CustomSmartPointer {
    fn drop(&mut self) {
        println!("Dropping CustomSmartPointer with data `{}`!", self.data);
    }
}

fn main() {
    let c = CustomSmartPointer {
        data: String::from("my stuff"),
    };
    let d = CustomSmartPointer {
        data: String::from("other stuff"),
    };
    println!("CustomSmartPointers created.");

    // At the end of `main`, both of the `CustomSmartPointers` go out of scope and Rust will automatically
    // call the `drop()` method for both. 
    // NOTE: variables will be dropped in the reverse order of their creation, so first `d` is dropped and
    // then `c` (because `c` was created first and then `d`)
}
```
**`cargo run`** —>  
	CustomSmartPointers created.  
	Dropping CustomSmartPointer with data `other stuff`!  
	Dropping CustomSmartPointer with data `my stuff`!  

<ins>What happens if you want to customize this cleanup behavior so you can manually clean up values early?</ins>

- **In most cases, this isn’t necessary.**

- However, in **some cases, you might want to clean up a value early.** For example, **when using smart pointers to manage locks.** In this case, you **might want to call the `drop()` method to release a lock so other code in the same scope could acquire the lock.**

- **Rust doesn’t allow you to call the `drop()` method directly/manually** — “explicit destructor calls not allowed”. Rust doesn’t allow us to call `drop()` manually because when our variable goes out of scope, Rust will still automatically call `drop()` which would result in a **double free** (i.e., potentially calling free on memory that’s already been freed).
 
- **<ins>TO MANUALLY CLEAN UP A VALUE EARLY:</ins>** Instead of calling the `drop()` method on the value, we **call the `drop()` function provided by Rust standard library and pass in the value we want to drop.**

    - EXAMPLE:

```Rust
struct CustomSmartPointer {
    data: String,
}

impl Drop for CustomSmartPointer {
    fn drop(&mut self) {
        println!("Dropping CustomSmartPointer with data `{}`!", self.data);
    }
}

fn main() {
    let c = CustomSmartPointer {
        data: String::from("some data"),
    };
    println!("CustomSmartPointer created.");

    drop(c);	// call the `drop()` function provided by Rust standard library and pass in `c`. It is
		// included in the prelude so we don't have to bring it into scope manually.

    println!("CustomSmartPointer dropped before the end of main.");
}
```
**`cargo run`** —>  
	CustomSmartPointer created.  
	Dropping CustomSmartPointer with data `some data`!    <— we can see that our smart pointer was
 								 successfully dropped / cleaned up
	  							 early before main() ends   						         
		   
`CustomSmartPointer` dropped before the end of main.

## Reference Counting

**The Reference Counting smart pointer allows us to share ownership of some data.**

- In the majority of cases, ownership is clear; you know exactly which variable owns a specific value.

- However, **there are cases where a single value has multiple owners**. For example, if you have a graph with multiple edges that point to the same node. Conceptually, this node is owned by all of the edges. In this case, a node should not cleaned up unless it doesn’t have any edges pointing to it. 

- **To enable multiple ownership of a value, we can use a Reference Counting smart pointer, which will <ins>keep track of the number of references to a value, and when there are no more references, the value will get cleaned up</ins>.**

    - <ins>An analogy would be a tv in a living room.</ins> When a person walks into the living room, they turn on the tv. As more people walk into the room, they start watching the tv. Then, people start to leave, and the last person to leave is the one who turns off the tv. If the tv turned off while there were multiple people in the living room, there would be panic. 

- The Reference Counting smart pointer is **<ins>used when we want to allocate a value on the heap and have multiple parts of our program read that value, and we don’t know at compile time which part of our program is going to finish using that value last (who should be the owner???)</ins>**. **If we knew which part was going to finish using the data last, we can simply make that part the data’s owner** and then create regular references referencing that owner and ownership rules would be enforced. However, if we don’t know who the owner is, then the owner may go out of scope and we’d have dangling references.

<ins>NOTE:</ins> The Reference Counting smart pointer we use here in this section is only useful in single threaded programs. 

### `Cons` List Example with `Rc`

**Suppose we create two lists that both share ownership of a third list**, like the below… In this case, we have a list called `b` and a list called `c`, and they both point to a list called `a`.

<img width="732" alt="Image" src="https://github.com/user-attachments/assets/d80e7935-dc42-493a-9124-cf52c245379c" />

<ins>Here is this example in code…</ins>
```Rust
// See my detailed explanation of a `Cons` List in previous section
enum List {
    Cons(i32, Box<List>),
    Nil,
}

use crate::List::{Cons, Nil};

fn main() {
    let a = Cons(5, Box::new(Cons(10, Box::new(Nil))));

    // Both lists `b` and `c` point to list `a`
    let b = Cons(3, Box::new(a));
    let c = Cons(4, Box::new(a));
}
```
^^^**HOWEVER, this code errors**, as shown below. The error states that we are attempting to use a value that has already been moved. **A `Cons` variant owns the data that it holds**. So, **when we do let `b = Cons(3, Box::new(a));` we are moving `a` into `b`**, so **`b` now owns `a`**. For this reason, we **can’t use `a` in the next line when defining `c`, which causes the below error.**

<img width="729" alt="Image" src="https://github.com/user-attachments/assets/067be855-c9f7-4dc3-bfa7-83d1fb14d411" />

We **could solve this by changing the definition of the `Cons` variant to hold references instead of owned value, but that would require the use of lifetimes.** By **using lifetime parameters**, we would be **specifying that every element in `List` has to live at least as long as the `List` itself.** **Otherwise**, we would have **dangling references** where the `List` points to elements that don’t exist. In other words, if the data that a `Cons` variant points to goes out of scope and is dropped before the `Cons` variant itself, then the `Cons` variant would be left with a hanging reference to invalid memory.

**<ins>Solution: Use a Reference Counting smart pointer</ins>**

<ins>NOTE:</ins> **to get the reference counts** in the below, we use **`Rc::strong_count()`** instead of `Rc::weak_count()`. There is no plain count only these two options… (we explain them in detail in a later section)

```Rust
use std::rc::Rc; // bring the Reference Counting smart pointer into scope

enum List {
    Cons(i32, Rc<List>),
    Nil,
}

use crate::List::{Cons, Nil};

fn main() {
    // Replace `Box` with `Rc` in the below.
    // Also, wrap List `a` inside a Reference Counting smart pointer because we are passing it into List `b` and 
    // List `c`. Creating List `a` increases reference count for `a` from 0 to 1.
    //
    let a = Rc::new(Cons(5, Rc::new(Cons(10, Rc::new(Nil))))); 

    println!("count after creating a = {}", Rc::strong_count(&a));

    // To pass List `a` into List `b` and List `c` (so that `b` and `c` both point to List `a`), call `Rc::clone()` and pass it a
    // reference to `a`. `Rc::clone()` doesn't make deep copies of the data it is passed, unlike most clone 
    // implementations. Instead, calling `Rc::clone()` here only increments the reference count. NOTE: another
    // way to do this is replacing `Rc::clone(&a)` with `a.clone()`. What clone does is the following: `a` owns one `Rc`
    // smart pointer to the data `(Cons(5, Rc::new(Cons(10, Rc::new(Nil)))))`, and `b` receives a new `Rc` smart 
    // pointer (returned by `clone()`) that also points to and shares ownership of the same underlying data.
    // They both hold separate `Rc` instances that refer to the same allocated content.
    // 
    // To summarize, we want both List `b` and List `c` to point to List `a`. We can't just pass in a reference to `a` for
    // the `Rc<List>` value in the tuple because what it expects is an owned type -> mismatched types error. We
    // also can't pass List `a` in directly because it would move ownership of `a` into `b` (as it is passed into `b` 
    // first). So, the solution here is to use the `clone()` method of `Rc`, which will give us back an owned value; 
    // however, in this case, `clone()` does not deep copy the data; instead, it just increases the reference count.	
    //
    // Creating List `b`, which points to List `a`, increases the reference count for `a` from 1 to 2.
    //
    let b = Cons(3, Rc::clone(&a))
    println!("count after creating b = {}", Rc::strong_count(&a));

    {
        // creating List `c`, which points to List `a`, increases the reference count for `a` from 2 to 3. 
        // Done in this inner scope
        let c = Cons(4, Rc::clone(&a)); 
        println!("count after creating c = {}", Rc::strong_count(&a)); 
    } 
    // when the inner scope ends, `c` is dropped, so the reference count for List `a` will decrease from 3 to 2

    println!("count after c goes out of scope = {}", Rc::strong_count(&a));
}
// NOTE: when we get to the end of `main()`, both `a` and `b` will also now be out of scope, so the reference count
// for list `a` is 0. THUS, the Reference Counting smart pointer will be cleaned up.
```

**<ins>NOTE:</ins>** **the Reference Counting smart pointer only allows multiple parts of your program to <ins>read the same data not modify it.</ins>** If the Reference Counting smart pointer allowed multiple mutable references, then we would be violating the borrowing rules: either have 1 mutable reference of any number of immutable. **BUT, mutability is useful —> <ins>interior mutability pattern.</ins>**

## Interior Mutability

A design pattern in Rust that **allows you to mutate data even when there are immutable references to that data**, which is typically disallowed by the borrowing rules. 

- To mutate data, this pattern **uses unsafe code** inside a data structure to bypass the typical rules around mutation and borrowing. 

- **Unsafe code:** code that is not checked at compile time for memory safety.

    - Even though the borrowing rules are not enforced at compile time, we can still enforce them at runtime.
  
    - You may ask: **why would you want to enforce the borrowing rules at runtime instead of compile time?** <ins>See below example</ins>.
 
### `RefCell` Smart Pointer

**The `RefCell` smart pointer represents single ownership over the data it holds**, much like the `Box` smart pointer. The difference is the **`Box` smart pointer enforces the borrowing rules at <ins>compile time</ins>**, whereas the **`RefCell` smart pointer enforces the borrowing rules at <ins>runtime</ins>**. As a result, with `RefCell`, if you break the borrowing rules at runtime, then your program will panic and exit. 

- **Because `RefCell<T>` allows mutable borrows checked at <ins>runtime</ins>, you can <ins>mutate the value inside</ins> the `RefCell<T>` <ins>even when</ins> the `RefCell<T>` <ins>smart pointer itself is immutable.</ins>**

    - Mutating a value inside an immutable value is called the **interior mutability pattern**.

- The **advantage `Box` has with checking the borrowing rules at compile time is that errors will be caught sooner** in the development cycle and there’s no runtime performance cost. For these reasons, checking borrowing rules at compile time is the default in Rust. 

- The **advantage of checking the borrowing rules at runtime is that certain memory safe scenarios are allowed, whereas they would be disallowed at compile time.** This is because certain properties of a program are impossible to detect using static analysis. 
    - Example: The most famous example of this is the halting problem. 

- The **`RefCell` smart pointer is useful when you’re sure that your code is following the borrowing rules, but the compiler can’t understand or guarantee that.**

- <ins>NOTE:</ins> you **can only use the `RefCell` smart pointer in single-threaded programs**.

- <ins>Example Below:</ins> We get **ERRORS** when **trying to use the interior mutability pattern w/ borrowing rules being checked at compile time.**

 ```Rust
// NOT ALLOWED to have a mutable reference to data that is declared as immutable...
//
let a = 5;		// Immutable variable `a` that is set to 5.
let b = &mut a;		// `b` is a mutable borrow to `a`, ERROR: "cannot borrow `a` as mutable
                        // bc it's not declared as mutable".

// IF we have an immutable reference to some data, then we can't change the underlying value of that data even if the data itself is mutable...
//
let mut c = 10;		// Mutable variable `c` that is set to 10
let d = &c;		// `d` is an immutable borrow to `c`
*d = 20;		// Use dereference to change underlying value from 10 to 20. ERROR: `d` is an
                        // immutable reference, so the data it refers to cannot be written.
```
**POSSIBLE SOLUTION WITH INDIRECTION:**
- Imagine we have a data structure that stores some value, and inside the data structure, that val is mutable.

- But, when we get a reference to the data structure, the reference itself is immutable. As a result, **code outside the data structure** would **not be able to mutate the value stored within the data structure directly.**

- HOWEVER, outside the data structure, we could **call** some **public methods that would mutate the inner value.** —> <ins>THIS is called the interior mutability pattern</ins> and it is **essentially what the `RefCell<T>` smart pointer does.**

- HOWEVER, the **`RefCell<T>` smart pointer is a little fancier** bc **instead of calling methods to mutate the data, we <ins>can call methods to get an immutable or mutable reference to the data</ins>**. This works because the **`RefCell<T>` smart pointer checks that the references are valid at runtime**.


### USE CASE for the Interior Mutability Pattern

We have a library that tracks a value against a maximum value and sends messages depending on how close the value is to the maximum value. This library could keep track of the quota for how many API calls a user is able to make. This library only provides the functionality to track how close a value is to the maximum value and what messages to send at what times. Applications implementing the library are expected to implement the mechanism for actually sending the message (whether through email, text, or something else). 

```Rust
// `Messenger` trait with one method called `send()` that takes an immutable reference to `self` and a message
// to send (string slice)
pub trait Messenger {
    fn send(&self, msg: &str);
}

// `LimitTracker` struct with three fields.
pub struct LimitTracker<'a, T: Messenger> {
    messenger: &'a T,	// `messenger` field is a reference to a generic type that implements the `Messenger` trait.
			// Bc we're borrowing `T` here, we have to add a lifetime annotation.

    value:usize,	// `value` field represents the current value
    max:usize,		// `max` field represents the max value
}

// In the implementation block, we have to specify our lifetime and generic again (with the trait bound)
impl <'a, T> LimitTracker<'a, T>
where
    T: Messenger,
{
    // Constructor
    pub fn new(messenger: &T, max: usize) -> LimitTracker<T> {
        LimitTracker {
            messenger,
            value: 0,
            max,
        }
    }
    // Pass in mutable reference to `self` and the `value` we want to set.
    pub fn set_value(&mut self, value: usize) {
        self.value = value;

        let percentage_of_max = self.value as f64 / self.max as f64;

        if percentage_of_max >= 1.0 {
            self.messenger.send("Error: You are over your quota!");
        } else if percentage_of_max >= 0.9 {
            self.messenger.send("Urgent warning: You've used over 90% of your quota!");
        } else if percentage_of_max >= 0.75 {
            self.messenger.send("Warning: You've used up over 75% of your quota!");
        }
    }
}

#[cfg(test)]
mod tests {
    use super::*;
    use std::cell::RefCell;	// bring the `RefCell` smart pointer into scope

    // `MockMessenger` struct with one field called `sent_messages` which will store a vector of 
    // messages that have been sent (the messages sent from `LimitTracker::set_value()` with .`send()`). 
    struct MockMessenger {
        sent_messages: RefCell<Vec<String>>,	// This vector is a mutable value, but the `send()` method
						// below accepts an immutable reference to `self`. As a result,
						// in `send()`, we can't edit the mutable `sent_messages` value
						// unless we use a `RefCell` smart pointer.
						//
						// SOLUTION: we wrap the vector of `Strings` in a `RefCell`
						// smart pointer, bc `RefCell<T>` allows mutable borrows
						// checked at runtime. Thus, we can mutate the value inside
						// the `RefCell<T>` even when the `RefCell<T>` smart pointer
						// itself is immutable.
   		}
    impl MockMessenger {
        fn new() -> MockMessenger {
            MockMessenger {
                sent_messages: RefCell::new(vec![]),	// construct a new `RefCell` smart pointer and
							// pass in an empty vector.
            }
        }
    }
    // Implement the `Messenger` trait for the `MockMessenger` struct. We make it so that when a `MockMessenger`
    // calls the `.send()` method, it pushes the message as a `String` onto the `sent_messages` vector. In this way,
    // the `MockMessenger` accumulates all of the messages sent in its `sent_messages` vector.
    impl Messenger for MockMessenger {
        fn send(&self, message: &str) {
            // self.sent_messages.push(String::from(message));	// Without `RefCell`, this ERRORS, because we
								// can't borrow the `sent_messages` vector
								// as mutable to push a value when we have
								// an immutable reference to the current
								// `MockMessenger` instance (`&self`). Bc we
								// take an immutable reference, all fields
								// inside the struct are also immutable.
								//
								// If instead of `RefCell`, we were to try to fix
								// this by taking a mutable reference to `self`
								// (`&mut self`), this would also ERROR bc the
								// `Messenger` trait expects a `send()`
								// method that accepts an immutable
								// reference to `self`.														

            // NOW, after applying our solution, `sent_messages` is our `RefCell` smart pointer and it is
            // immutable bc we have `&self` (an immutable reference to `self`). Bc we have `&self`, all of the 
            // fields inside the current `MockMessenger` instance are immutable. BUT, bc `sent_messages` 
            // is a `RefCell` smart pointer, we can can get a mutable reference to the values stored inside 
            // the smart pointer by calling `.borrow_mut()`... then we can call the `.push()` method on 
            // our mutable reference and append the message.
            //
            self.sent_messages.borrow_mut().push(String::from(message));
        }
    }

    #[test]
    fn it_sends_an_over_75_percent_warning_message() {
        let mock_messenger = MockMessenger::new();
        let mut limit_tracker = LimitTracker::new(&mock_messenger, 100);

        limit_tracker.set_value(80); // should send the "Warning" message for >= 75%

        // `sent_messages` is our `RefCell` smart pointer, but we want to get the length of the vector stored
        // inside of our smart pointer. In this case, we don't need a mutable reference. We can simply get
        // an immutable reference using `.borrow()`
        //
        assert_eq!(mock_messenger.sent_messages.borrow().len(), 1);
    }

}
```

As we explained, `RefCell` smart pointer checks the borrowing rules at runtime. **One of the borrowing rules is that we can’t have two mutable references at the same time. What happens when this is the case?**

```Rust
fn send(&self, message: &str) {
    // Two variables that take a mutable reference to `sent_messages`.
    let mut one_borrow = self.sent_messages.borrow_mut();
    let mut two_borrow = self.sent_messages.borrow_mut();
            
    // Push the passed in message using the first mutable reference and then the second.
    one_borrow.push(String::from(message));
    two_borrow.push(String::from(message));

}
```
^^^**NO COMPILE TIME ERRORS, bc `RefCell` checks borrowing rules at runtime**, **BUT when we run `cargo test`, the program <ins>panics at runtime</ins>…**

<img width="650" alt="Image" src="https://github.com/user-attachments/assets/a43001ce-7a56-46fc-bbd1-fee95e46fe6a" />

^^^<ins>LESSON:</ins> the interior mutability pattern gives flexibility but **we have to be careful and make sure that our code abides by the borrowing rules**. Also note that **bc we are checking the borrowing rules at runtime, this does results in a small runtime performance hit.**

### Combining `Rc` with `RefCell` to Get Multiple Owners of Mutable Data

In our previous section on the reference counting smart pointer (`Rc`), we talked about how we couldn’t change the values inside our `Cons` Lists once they were created bc **`Rc` only stores immutable values**. In the below example, we **use the `RefCell` smart pointer so that we can update the values inside our lists after they have been created.**

```Rust
#[derive(Debug)]
enum List {
    Cons(Rc<RefCell<i32>>, Rc<List>),	// Both the integer (first elem in tuple) and the list (second elem
					// in tuple) are wrapped in the `Rc` smart pointer bc we want them
					// to have multiple owners.
					//
					// Interior mutability —
					// The integer value is additionally wrapped in the `RefCell` smart
					// pointer so that it can be mutable even though the `Rc`
					// smart pointer doesn’t allow mutable references.

    Nil,
}

use crate::List::{Cons, Nil};
use std::cell::RefCell;
use std::rc::Rc;

fn main() {
    let value = Rc::new(RefCell::new(5));	// create an integer of 5 that is wrapped in `RefCell` smart pointer and
						// then an `Rc` smart pointer. This way it can be mutated and have
						// multiple owners.

    let a = Rc::new(Cons(Rc::clone(&value), Rc::new(Nil)));	// Create the first `Cons` List `a`, which has a single
								// node. For the value, we clone the `value`
								// variable defined in the previous line. The
								// `clone()` method of `Rc` gives us back an owned
								// value, but makes is so that the `value` variable
								// and the `a` list share ownership of the same
								// underlying value. `clone()` does not deep copy
								// the data; instead, it just increases the reference
								// count.
								// Also store the `a` `Cons` List in an `Rc` smart
								// pointer bc we want lists `b` and `c` to share ownership.

    // Create lists `b` and `c`, which store the values 3 and 4, respectively, and point to list `a`. We use `clone()` to 
    // ensure `b` and `c` share ownership of `a`'s underlying value with `a`.
    // We also make it so that the integers can be mutated with `RefCell` and can have multiple owners with `Rc`.
    //
    let b = Cons(Rc::new(RefCell::new(3)), Rc::clone(&a));
    let c = Cons(Rc::new(RefCell::new(4)), Rc::clone(&a));

    *value.borrow_mut() += 10;	// We use the automatic dereferencing feature to automatically 
                                // dereference `Rc<RefCell<5>>` to `RefCell<5>`, then call 
                                // `.borrow_mut()` to take a mutable reference to the value in the
				// `RefCell` smart pointer, then use `*` to modify the underlying value of
				// the mutable reference.

    println!("a after = {:?}", a);
    println!("b after = {:?}", b);
    println!("c after = {:?}", c);
}
```

<img width="515" alt="Image" src="https://github.com/user-attachments/assets/97593b11-0647-4da5-ae5e-f2b1151e406b" />

### Panicking when breaking borrowing rules with `borrow_mut()`

```Rust
use std::rc::Rc;
use std::cell::RefCell;

#[derive(Debug)]
struct MyData {
    value: i32,
}

fn main() {
    // --- Example 1: Multiple `borrow_mut()` at the same time ---
    //
    // Create an `Rc<RefCell<MyData>>`
    let shared_data_rc = Rc::new(RefCell::new(MyData { value: 10 }));

    // Clone the `Rc` to simulate multiple owners/references
    let shared_data_rc_clone1 = Rc::clone(&shared_data_rc);
    let shared_data_rc_clone2 = Rc::clone(&shared_data_rc);

    // First mutable borrow
    let mut_borrow_1 = shared_data_rc.borrow_mut();
    println!("Successfully obtained first mutable borrow: {:?}", mut_borrow_1);
	
    // ATTEMPT TO GET A SECOND MUTABLE BORROW - THIS WILL PANIC!!!!
    // The program will crash here because `RefCell` only allows one mutable borrow at a time.
    println!("\nAttempting to get a second mutable borrow...");
    let mut_borrow_2 = shared_data_rc_clone1.borrow_mut();
    // ERROR MESSAGE: thread 'main' panicked at src/main.rs:25:46:
    // already borrowed: BorrowMutError
    // note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace


    // --- Example 2: `borrow_mut()` while `borrow()` is active---
    //
    // Reset or create new shared data for this example
    let shared_data_rc_2 = Rc::new(RefCell::new(MyData { value: 20 }));
    let shared_data_rc_2_clone = Rc::clone(&shared_data_rc_2);

    // Get an immutable borrow
    let imm_borrow = shared_data_rc_2.borrow();
    println!("Successfully obtained immutable borrow: {:?}", imm_borrow);

    // ATTEMPT TO GET A MUTABLE BORROW WHILE IMMUTABLE BORROW IS ACTIVE - THIS WILL PANIC!!!!
    let mut_borrow = shared_data_rc_2_clone.borrow_mut();
    // ERROR MESSAGE: thread 'main' panicked at src/main.rs:40:45:
    // already borrowed: BorrowMutError
    //note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace
}
```

## Reference Cycles and Memory Leaks

Rust is known for being a memory safe language, so it provides certain guarantees (e.g., you can’t have data races). However, it does not provide the same guarantee for memory leaks. **Rust makes it difficult, but not impossible, to create memory that is never cleaned up.** We **can create a memory leak by using the `Rc` smart pointer and the `RefCell` smart pointer**. Using these two smart pointers, we can **create references where items reference each other in a cycle**, which will create a memory leak. 

<ins>EXAMPLE:</ins> In the below, we create a reference cycle where list `a` references list `b` and list `b` references list `a`.

<img width="438" alt="Image" src="https://github.com/user-attachments/assets/d1b973ee-bb40-4ce3-92ce-acfe6ac3e78c" />

```Rust
use crate::List::{Cons, Nil};
use std::cell::RefCell;
use std::rc::Rc;

#[derive(Debug)]
enum List {
    Cons(i32, RefCell<Rc<List>>),	// Store 32bit int and `List` wrapped in `Rc` (can have multiple owners).
					// Wrap whole thing in `RefCell`, so you can change the `Rc<List>` but not
					// the `List` (due to the order being `RefCell<Rc` and not `Rc<RefCell. This
					// is fine bc all we want to do is change which shared `List` is the next
					// pointer not actually change the contents of the `List`. 
    Nil,
}

impl List {
    // Returns the next value. If `self` is a `Cons` variant, then returns value in next pointer. If `self` is `Nil`, returns None.
    fn tail(&self) -> Option<&RefCell<Rc<List>>> {
        match self {
            Cons(_, item) => Some(item),	// If the variant is `Cons`, then return the `List` stored in `Cons`
						// wrapped in `Some`.
            Nil => None,
        }
    }
}

fn main() {
    // list `a` is a `Cons` variant wrapped in `Rc` (so can have multiple owners), stores
    // the number 5 and points to `Nil` (so just one node)
    let a = Rc::new(Cons(5, RefCell::new(Rc::new(Nil))));

    // Print out the initial reference count of list `a` using strong_count(): 1
    println!("a initial rc count = {}", Rc::strong_count(&a));
    // Print out the next item in `a` using `tail()`, it is `Nil`.
    println!("a next item = {:?}", a.tail()); 

    // list `b` is a `Cons` variant wrapped in `Rc` (so can have multiple owners), stores
    // the number 10 and points to a clone of list `a`, so `a` and `b` share the underlying value
    // stored in `a`.
    let b = Rc::new(Cons(10, RefCell::new(Rc::clone(&a))));

    // Print out the new reference count of list `a`: 2
    println!("a rc count after b creation = {}", Rc::strong_count(&a));
    // Print list `b`'s initial reference count: 1
    println!("b initial rc count = {}", Rc::strong_count(&b));
    // Print the next item in list `b`: list `a` whose value is 5
    println!("b next item = {:?}", b.tail());

    // Modifying list `a` to point to a clone of list `b`, call `tail()` to get next item in list `a`, use `if let` bc only care about 
    // `Some` variant. At this point, `a` is a `Cons` variant so when we call `tail()` we match into the Cons part and 
    // return `Some(RefCell::new(Rc::new(Nil)))` bc next pointer in `a` is `RefCell::new(Rc::new(Nil))`. We then change 
    // the next pointer of `a` to be a reference to list `b`. To do so, use `.borrow_mut()` to get a mutable reference to the 
    // data at `a` and then dereference it to change the data to a reference to list `b` (using `clone()`) so `a` shares 
    // ownership of `b`'s underlying value.
    if let Some(link) = a.tail() {
        *link.borrow_mut() = Rc::clone(&b);
    }

    // Print out `b`'s new reference count: 2
    println!("b rc count after changing a = {}", Rc::strong_count(&b));
    // Print out `a`'s new reference count: 2
    println!("a rc count after changing a = {}", Rc::strong_count(&a));

    // The below line gives a stack overflow. This is bc when we try to print the next item in list `a`, it will be a 
    // reference to list `b`,  which stores a reference to list `a`, which stores a reference to list `b`, and this goes on 
    // infinitely!!!
    println!("a next item = {:?}", a.tail());
}
```
^^^ **THIS circular dependency also causes a <ins>memory leak</ins>…**

When `b` gets cleaned up, the memory on the stack gets cleaned up; however, the memory on the heap will not get cleaned up bc this memory is still referenced inside of list `a` with its `Rc` smart pointer in next.

<img width="476" alt="Image" src="https://github.com/user-attachments/assets/0f345f82-6d0d-4399-b3e4-1faa474daa86" />

Then, `a` gets cleaned up. Again, the stack memory gets cleaned up; however, the memory on the heap does not get cleaned up bc this memory location is still being referenced by the heap memory for list `b`. 

<img width="489" alt="Image" src="https://github.com/user-attachments/assets/94f97174-8997-49a0-8822-9c6e02941bb0" />

^^^NOW, we have a situation where we have two lists allocated on the heap but we don’t have any stack variables pointing to them. This means they are orphaned and won’t get cleaned up. 

<ins>LESSON:</ins> **Reference cycles aren’t easy to create, but they are not impossible to create.** If mixing referencing counting (`Rc`) with interior mutability (`RefCell`), then you need to make sure that reference cycles aren’t being created. Creating reference cycles is a logical bug in your code that should be **prevented using automated tests, code reviews, and other SWE best practices**. 

- So far, we’ve been using smart pointers that own the data they point to, but **if you’re in a situation where you can get away with using pointers that don’t own the data they point to** (i.e., **`Weak` smart pointers**), **then you can prevent reference cycles.**

### `Weak` Smart Pointer

**A version of the Reference Counting smart pointer (`Rc`) that <ins>holds a non-owning (weak) reference to the data managed by an `Rc<T>`</ins>**. Bc they are Non-Owning, a **`Weak<T>` pointer doesn't increase the strong reference count of the `Rc<T>` it points to**. This means that **if all `Rc<T>` instances pointing to a value are dropped, the value itself will be dropped, regardless of any existing `Weak<T>` pointers.** Because `Weak` pointers don't prevent the underlying value from being dropped, a **`Weak` pointer has no way of knowing at compile time whether the value it used to point to still exists**. It's an observer, not an owner.

- Convert (**downgrade**) a **`Rc`** smart pointer **to** a **`Weak`** smart pointer using **`Rc::downgrade()`**.

- Convert (**upgrade**) a **`Weak`** smart pointer to a **`Rc`** smart pointer using the **`.upgrade()` method**, which returns an `Option`. Returns an `Option` bc the underlying value in the pointer may have been dropped and in that case we want to get back `None` variant. If hasn’t been dropped, then get a `Some` variant containing the `Rc` smart pointer.

- **<ins>Whenever we want to see or mutate the value inside a `Weak` smart pointer, we have to call upgrade to upgrade it to an `Rc` smart pointer.</ins>** This is because the `Weak` smart pointer has no idea if the inner value has been dropped or not.

<ins>How `Weak<T>` Solves Reference Cycles:</ins>
- Non-owning
- Does not increment the reference count
- Cannot directly access the data
- Returns None if the `Rc<T>` is dropped

<ins>When to Use `Weak<T>`:</ins>

- **`Weak<T>` is inherently tied to `Rc<T>`. It exists to solve the specific problem of reference cycles that arise from Rc<T>'s shared ownership model.**

- You **use Weak<T> specifically when you have a parent-child or peer-to-peer relationship where**:
	- You **need shared ownership** (`Rc<T>`).
	- **One part of the relationship** (e.g., a child pointing back to its parent, or two peers pointing to each other) **should not prevent the other part from being dropped.**
	- You want to avoid memory leaks due to reference cycles.

- <ins>Common Scenarios:</ins>
	- **Doubly Linked Lists**: In a doubly linked list where each node has `Rc` pointers to its next and prev nodes, the prev pointer is often `Weak` to prevent cycles.
	- **Graph Structures**: Similar to linked lists, if nodes in a graph have `Rc` pointers to their neighbors, using `Weak` for back-references can prevent cycles.
	- **Parent-Child Relationships**: If a child holds an `Rc` to its parent, and the parent also holds an `Rc` to its children (e.g., in a tree structure), the child's reference back to the parent should be `Weak`. This way, dropping the parent (and its `Rc` to children) will eventually allow the children to be dropped, and the parent can be dropped even if children still exist.

    - <ins>Example:</ins>

```Rust
use std::cell::RefCell;
use std::rc::{Rc, Weak};

// Tree structure with nodes that know about their child nodes.
#[derive(Debug)]
struct Node {
    value: i32,
    children: RefCell<Vec<Rc<Node>>>,	// Vector of children, node wrapped in `Rc` bc we want variables
					// outside of this tree to be able to point to node so we can traverse
					// the tree. Wrap vector in `RefCell`, bc want to be able to modify a
					// node's children, i.e., modify `Vec<Rc<Node>>` as a whole with
					// push pop.


    // Without a `parent` field, a parent node can access its children using `self.children`, but children don't have a
    // reference to their parent.
    parent: RefCell<Weak<Node>>,	// we want to be able to modify which `Weak<Node>` is the parent node
					// so wrap whole thing in `RefCell`. We also want the ability for variables
					// outside the tree to reference our parent
					// (multiple ownership), but we can't use `Rc` due to creating reference
					// cycles with children. Luckily, we don't need an `Rc` smart pointer bc
					// children don't need to own their parent, when a child is dropped, the
					// parent shouldn't also be dropped. So can use the `Weak` smart
					// pointer here.
}

fn main() {
    // Create a node that stores integer 3 and has no children
    let leaf = Rc::new(Node {
        value: 3,
        parent: RefCell::new(Weak::new()),	// leaf node has no parent at this point
        children: RefCell::new(vec![]),
    });

    // Print leaf's parent. The parent is `RefCell<Weak<Node>>`. To immutably borrow the value in
    // `RefCell`, we use `borrow`. Then, we attempt to convert the `Weak` smart pointer to an `Rc` smart
    // pointer using `upgrade()` which returns an `Option`. As I explained, we have to do this conversion
    // bc the `Weak` pointer doesn't know if the value got dropped.
    //
    println!("leaf parent = {:?}", leaf.parent.borrow().upgrade());

    // Create another node that stores integer 5 and has one child: the leaf node we just defined. 
    // We call `clone()` to get back an owned value but have shared ownership.
    let branch = Rc::new(Node {
        value: 5,
        parent: RefCell::new(Weak::new()), // branch node has no parent
        children: RefCell::new(vec![Rc::clone(&leaf)]),
    });

    // modify leaf's parent to be branch
    // `leaf.parent` gives `RefCell<Weak<Node>>`, use `borrow_mut()` to mutably borrow the value stored in the
    // `RefCell`, use `*` to modify the underlying value.
    // branch is a `Rc` smart pointer, but parent expects a `Weak` smart pointer. To transform a `Rc` smart pointer
    // to a `Weak` smart pointer, call `Rc::downgrade()` and pass in the `Rc` smart pointer. 
    //
    *leaf.parent.borrow_mut() = Rc::downgrade(&branch);

    println!("leaf parent = {:?}", leaf.parent.borrow().upgrade());
}
```

### Rc smart pointer: `strong_count()` and `weak_count()` methods

**Internally, the Rc smart pointer stores two counts**…

- **Strong count** — the **number of references which have ownership** of the data, **`Rc::strong_count()`**

    - A **value is dropped when its strong count is 0**

- **Weak count** — the **number of references that don’t have ownership of the data**, **`Rc::weak_count()`**

    - The weak count **has no influence over whether the underlying value is dropped or not.**
 

---

# Concurrency in Rust
 
One of the goals of the Rust language is handling concurrent programming safely and efficiently.

- **Concurrent programming** — when different parts of your program execute independently.

- **Parallel programming** — when different parts of your program execute at the same time.

By leveraging Rust’s type system and powerful ownership model, a lot of concurrency errors are able to be caught at compile time. Bc of this, you’re able to write code that is free of subtle bugs and is easy to refactor without introducing new bugs, which is why Rust uses the term **fearless concurrency**. 

Bc Rust is a low-level programming language, it has various solutions to handle concurrency problems. <ins>See below</ins>.

## Using Threads

- In most current operating systems, an executed program’s code is ran within a process and the operating system manages running multiple processes at once.

- Within a program, you can have independent parts that run simultaneously and the features that run these independent parts are called **threads**.

- **Splitting your program’s computation into multiple threads can improve performance**, **because multiple parts of your program are running at the same time. BUT, this also increases complexity.** 

- **Because threads run simultaneously, you don’t have control over the order in which different parts of your program are executed**, which leads to **challenges** including the below:

    - **Race Conditions:** Threads are accessing data or resources in an inconsistent order

    - **Deadlocks:** Two threads that are both waiting for a resource that the other thread has, thus making both threads wait indefinitely.

    - Because execution order is non-deterministic, bugs can appear that only happen in certain situations and are hard to reproduce and fix reliably.

- Rust attempts to mitigate the negative effects of using threads; however, it’s on the programmer to be thoughtful when designing their program for a multi-threaded context.

## Types of Threads

Many operating systems provide an API to create new threads. There are two main types of threads:

1. **One-to-One Threads** (also called OS threads, native threads, system threads, etc.) — **when you create a thread in your program, it maps to an operating system thread**, so there’s a **one-to-one mapping**.

2. **Green Threads** (also called user threads or program threads) — Many programming languages provide their own special implementation of threads. These are called green threads. **DO NOT have a one-to-one mapping with operating system threads**, so you can have 20 green threads that map to only 5 operating system threads. This is why the green thread model is called an **`m` to `n` model (`m` green threads that map to `n` operating system threads).** 

The tradeoff between these two types of threads that is most important to Rust is **runtime support**. **By runtime, we mean the code that’s included by the programming language in every single binary**. **Rust aims to have an extremely small runtime**; in fact, almost no runtime at all. The tradeoff with this is sacrificing features, because the more features we include out of the box, the larger the runtime will be. **Because green threads would require a larger language runtime, Rust ONLY included one-to-one threads in its standard library**. However, if you would like to use green threads with the tradeoff of having a larger binary, then you could use crates that provide such functionality. 

## Creating New Threads in Rust

```Rust
use std::{thread, time::Duration};	// import `thread` from the standard library

fn main() {
    // In order to create a new thread, we call `thread::spawn()` and pass in a closure.
    thread::spawn(|| {
        // Inside of our spawned thread, we will loop through a range of integers.
        for i in 1..10 {
            println!("hi number {} from the spawned thread!", i);
            thread::sleep(Duration::from_millis(1))	// `thread::sleep()` pauses execution of the thread
							// for a specified amount of time. In this case, we
							// have the thread sleep for 1 millisecond.
        }
    });

    // By default, every program has one main thread.
    // In our main thread, loop through a range, print the number and let the main thread sleep for 1 millisecond.
    for i in 1..5 {
        println!("hi number {} from the main thread!", i);
        thread::sleep(Duration::from_millis(1));
    }
}
```

**`cargo run`** -->

<img width="475" alt="Image" src="https://github.com/user-attachments/assets/943c1466-0fb8-419c-954c-fb1e255093b5" />

<ins>^^^Observations in the above:</ins>
- **We can see that the spawned thread and the main thread run concurrently and in parallel (i.e, at the same time)**, as the printed values appear to alternate between threads as opposed to us getting all of the printouts from the main thread first and then all of the printouts from the spawned thread after, or vice versa.

-  **The main thread finishes printing its entire range (1-4) but the spawned thread does not finish printing all of its numbers (range is 1-9 but only got to 1-4).** This is because **<ins>when the main thread ends, the spawned is stopped no matter if it finishes executing or not</ins>**. We solve this next using **Join Handles**…

### Join Handles

- **Modifying our code above to allow the spawned thread to finish execution.**

```Rust
use std::{thread, time::Duration};

fn main() {
    // Store the return value of the `spawn()` function, which is a `JoinHandle` type.
    let handle = thread::spawn(|| {
        for i in 1..10 {
            println!("hi number {} from the spawned thread!", i);
            thread::sleep(Duration::from_millis(1));
        }
    });

    for i in 1..5 {
        println!("hi number {} from the main thread!", i);
        thread::sleep(Duration::from_millis(1));
    }

    // Call `handle.join()` which will wait for the spawned thread to finish executing. 
    //
    // 	- Calling `.join()` blocks the thread currently running (which in this case is the main thread) until the
    // 	  thread associated with the `handle` (in this case the spawned thread) terminates / finishes exec.
    //
    // 	- Blocking a thread means that the thread is prevented from doing any further work or exiting. 
    //
    // We have to call `.unwrap()` bc `.join()` returns a `Result` type.
    //
    handle.join().unwrap();
}
```

**`cargo run`** --> 
<img width="424" alt="Image" src="https://github.com/user-attachments/assets/b417ebab-cab5-4fc6-bc31-3503fbaca033" />

^^^Once again, the threads alternate in execution and **NOW, we can see that the spawned thread finishes executing and prints its entire range (1-9).**

**As expected if we move the `handle.join()` call before the printing in the main thread, then the spawned thread will finish printing its entire range (1 - 9) before any of the printing in main even starts**. This is because the **main thread will be blocked from running until the spawned thread terminates / finishes execution…**

```Rust
fn main() {
    let handle = thread::spawn(|| {
        for i in 1..10 {
            println!("hi number {} from the spawned thread!", i);
            thread::sleep(Duration::from_millis(1));
        }
    });
    handle.join().unwrap();

    for i in 1..5 {
        println!("hi number {} from the main thread!", i);
        thread::sleep(Duration::from_millis(1));
    }
}
```

**`cargo run`** —> 
<img width="391" alt="Image" src="https://github.com/user-attachments/assets/b45c5ed5-913a-4e30-942b-82076219f3d3" />

^^^<ins>LESSON:</ins> small details, such as where the `.join()` method is called, can affect whether or not your threads run at the same time.

### Using `move` Closures with Threads

Up until this point, when we spawned a thread, the thread didn’t depend on any variables outside of the thread. <ins>This is not the case in the below example:</ins>

```Rust
use std::thread;

fn main() {
    // Create a vector called `v` in the main thread
    let v = vec![1, 2, 3]; 

    // We spawn a new thread. Inside the new thread, we use the `v` Vector that we created above in the 
    // main thread.
    let handle = thread::spawn(|| {
        println!("Here's a vector: {:?}", v);  
    });

	// drop(v);	// BADDD!!!!!!

	// Block the main thread from terminating until the spawned thread finishes execution
	handle.join().unwrap();  
}

```
^^**THIS ERRORS because...**

- “The closure may outlive the current function, but it borrows `v`, which is owned by the current function” 

- **<ins>ISSUE EXPLAINED:</ins>** **Rust sees `v` is being used inside our closure but it’s being declared outside our closure, so Rust will infer how to capture `v`**. **Bc `v` is only being used inside the `println!()` statement in the closure, Rust will infer that we only need a reference to `v`**. However, **this is a problem** because **Rust doesn’t know how long the spawn thread will run for so it doesn’t know if `v` will always be a valid reference**. Imagine if after spawning the new thread, we called the `drop` function on `v`. See this code above. If we were allowed to write this code, then there is a possibility that when we run it: we **spawn the thread, immediately switch back to the main thread, drop the value `v`, then switch back to the spawned thread at which point `v` would be invalid**. **Because Rust doesn’t know how long our thread will run for, Rust doesn’t allow us to take a reference to `v` inside the closure.**
    - In other words, **if the closure were to borrow data from the main thread (e.g., `v`), there would be a problem: the main thread might finish or drop `v` while the new thread is still trying to access it.** This would lead to a use-after-free error, which Rust's ownership system is designed to prevent.

- Rust gives us the hint to **force the closure to take ownership of `v` using `move`**.

<img width="730" alt="Image" src="https://github.com/user-attachments/assets/4235ec97-5fe9-4c72-b671-6941aa519cfb" />

**`move` keyword:** By default, **closures in Rust typically capture variables by borrowing when possible**. However, you can **force a closure to take ownership of the values it uses inside its environment by using the `move` keyword in front of the closure**. This is **,<ins>most useful when you’re passing a closure from one thread to another thread as it ensures that we also pass the ownership of the variables / values (captured data) from one thread to the other thread.</ins>**

- <ins>How this solves the earlier problem:</ins> **By using `move`, we ensure that the ownership of `v` is transferred from the main thread into the closure's environment.** This means `v` now "belongs" to the new thread's execution context, and the **new thread can safely use it without worrying about the main thread dropping it prematurely.**

- <ins>Solution to our earlier error with `move`</ins>:

```Rust
use std::thread;

fn main() {
    let v = vec![1, 2, 3]; 

    // When we add the `move` keyword in front of our closure, we are telling Rust: don't infer that
    // the values inside our closure are borrowed. Instead, what we explicitly want is to move values
    // inside the closure (i.e., have the closure take ownership of the values). 
    //
    // Now, `v` is moved inside of the spawned thread, so it can longer be used inside of main().
    //
    let handle = thread::spawn(move || {
        println!("Here's a vector: {:?}", v);  
    });

    handle.join().unwrap();
}
```

## Message Passing

**Using messages to pass data between threads.**

- One increasingly popular approach to ensuring **safe concurrency** is **message passing**, where you have **threads** (or actors) **passing messages to each other which contain data.**

- Go programming language slogan: “do not communicate by sharing memory; instead, share memory by communicating”

### Channels

One tool Rust provides to enable message passing concurrency is a **<ins>channel</ins>**, included in standard library.

- **Channels are analogous to a channel of water** (like a river or stream). If you put something like a rubber duck on the stream, then the duck will travel downstream to the end of the waterway.

- **A channel in program has two halves**: the **transmitter** and the **receiver**.

    - **Transmitter** —  the upstream location where you would place the rubber duck
  
    - **Receiver** — the downstream location where the rubber duck will end up

- <ins>How we use a channel to perform message passing:</ins>

    1. **One part of your code calls methods on the transmitter, passing in the data you want to send.**
  
    2. **Another part of your code is listening to the receiver for arriving messages.**

- The channel is said to be **closed** if either the transmitter or the receiver half is dropped.

- <ins>Example use cases:</ins> Once you are familiar with channels, you can implement things like a chat system, or a program in which many threads perform part of a calculation and one thread aggregates the results. 

### Creating Channels in Rust

- <ins>Create a channel:</ins> **`let (tx, rx) = mpsc::channel();`**

	- Where **`tx` is the sender / transmitter**, and **`rx` is the receiver**. Traditionally, `tx` is used for the sender / transmitter, and `rx` is used for the receiver.
  
	- **`mpsc::channel()` returns a tuple `(Sender<T>, Receiver<T>)`** which **contains the sender and receiver**.

- <ins>Use the sender to send a message:</ins> **`tx.send(msg).unwrap();`**

    - **`send()` attempts to send a value on the channel, returning it back if it could not be sent.**
  
    - The **value** being sent (i.e., `msg`) does not have to be a String, it **can be any type** we want.
  
    - A **successful send** occurs when it is determined that the **other end of the channel has not hung up** (i.e., **been dropped**) **already**. An **unsuccessful send** would be one where the **corresponding receiver has already been deallocated.**
  
    - **Returns a `Result` type - `Result<T, SendError>`**. **`Ok(T)` indicates the value was successfully placed on the channel**, but it **doesn't guarantee the receiver will process it before hanging up**. This is bc it is **possible for the corresponding receiver to hang up** (i.e., get dropped, go out of scope) **immediately after this function returns `[Ok]`**. **`Err(SendError)` means that the data will never be received bc the receiver has already hung up** (i.e., been dropped, gone out of scope) and the value couldn't be sent.  We **use `.unwrap()` to extract the `Ok` value or panic if an `Err` occurs.**

- <ins>Use the receiver to receive the message:</ins>   **`let received = rx.recv().unwrap();`**

    - **`recv()` attempts to wait for a value on the receiver (`rx`), returning an error if the corresponding channel has hung up** (i.e., all the senders (transmitters) corresponding to that receiver have been dropped or have gone out of scope.)
    - **Returns a `Result` type - `Result<T, RecvError>`**. **`Ok(T)` contains the received value and `Err(RecvError)` signifies the channel has hung up / closed**. `Err` essentially indicates that no more values are coming. We **use`.unwrap()` to extract the `Ok` value or panic if an `Err` occurs.**
  
    - **`recv()` will always block the current/local thread if there is no data available and it's possible for more data to be sent (at least one sender still exists)**. i.e., it blocks the current thread's execution while it waits for a message to be sent down the channel.
  
        -  **If** we **don't want to block the current/local thread's execution, use `try_recv()` which returns a Result type immediately: `Ok` containing the received value if a value is available, or `Err` if no values are available at the time.**
  
        - **`try_recv()` is useful when you want your thread to do other work.** For example, we can have a **loop where every so often we call `try_recv()` to see if there are any new messages**; **otherwise, we keep looping and let the thread do other work.**

- <ins>EXAMPLE:</ins>

```Rust
use std::sync::mpsc;	// Bring `mpsc` module into scope. `mpsc` stands for multi-producer, single-
			// consumer. In Rust, the way channels are implemented you can have multiple
			// producers of messages but only one receiver of messages.
use std::thread;

fn main() {

    // Create a channel and store the sender / transmitter and the receiver
    let (tx, rx) = mpsc::channel();

    // Spawn a thread and use our sender (`tx`) to send a message
    thread::spawn(move || {	// To use our sender (`tx`) to send a message, we HAVE TO `move` `tx` into
				// the closure. If we remove `move`, ERROR: "Sender cannot be shared
				// between threads safely"

        let msg = String::from("hi");
        tx.send(msg).unwrap();	// send the message from the sender with `send()`
    });

    // Use the receiver in the main thread to receive a message
    let received = rx.recv().unwrap();      

    println!("Got: {}", received);
}
```

### Channels and Owner Transference

- **Ownership rules help us prevent errors in our concurrent code.**

- <ins>Example:</ins> Trying to use `msg` after we’ve already sent it down the channel to a different thread...

```Rust
thread::spawn(move || { 
    let msg = String::from("hi");
    tx.send(msg).unwrap(); 
    println!("msg is {}", msg);    // if we were allowed to do this, it would be problematic, bc we would send a
				   // message to another thread and then afterwards potentially modify or
				   // drop the variable. BUT THIS ERRORS 
});
```
<img width="605" alt="Image" src="https://github.com/user-attachments/assets/f482ffb4-b01b-4af9-b894-8be50b74a2a0" />

^^^**When we call `send()` and pass in a value, <ins>`send()` takes ownership of the value.</ins>** So, in the above code, the ownership rules prevent us from doing something dangerous, which is modifying or dropping a value after is has been passed to another thread. 

### Sending Multiple Messages

**This is to prove our code is running concurrently...**

```Rust
use std::sync::mpsc; 
use std::thread;
use std::time::Duration;

fn main() {
    let (tx, rx) = mpsc::channel();

    thread::spawn(move || { 
        let vals = vec![
            String::from("hi"),
            String::from("from"),
            String::from("the"),
            String::from("thread"),
        ];
        // Loop through the vector of values and send each value down the channel, also let
        // the thread sleep for 1 second after each call to `send()`.
        for val in vals {
            tx.send(val).unwrap(); 
            thread::sleep(Duration::from_secs(1));
        }
    });

    // Instead of calling `recv()` on our receiver once, use a `for` loop to get all the messages
    // passed down the channel.
    for received in rx {	// we are not calling `recv()` anymore; instead, we
				// treat the receiver (`rx`) as an iterator. Every iteration
				// will have a value that we pass down the channel. When the
				// channel closes, the iteration will end.
        println!("Got: {}", received);
    }
}
```
**`cargo run`** —>    
	Got: hi  
 	Got: from  
	Got: the  
 	Got: thread

^^^**We get each of these printouts with a one second delay between them (bc of `thread::sleep()`) which shows that the spawned thread and the main thread are running concurrently**. This is because the **main thread doesn't wait for the spawned thread to finish sending all its messages before it starts printing**. If it did, then instead of seeing each message with a 1 second delay between them, we would see nothing for 4 seconds and then all of the messages at once. Instead, **as soon as the spawned thread sends a message, the main thread's `for received in rx` loop receives it and prints it**. When the spawned thread finishes its loop and `tx` (the sender) is dropped, the channel "hangs up," and the `for` loop on `rx` naturally concludes. This confirms that both threads are running in parallel, **exchanging messages as they become available.**

### Creating Multiple Producers

In our current examples, we have one thread that sends messages. However, **let’s say we want to have two threads that send messages**…

```Rust
use std::sync::mpsc; 
use std::thread;
use std::time::Duration;

fn main() {
    let (tx, rx) = mpsc::channel();

    let tx2 = tx.clone();    // get a new sending handle to use in our second spawned thread

    // Below, we have two threads that are passing messages down the channel to the main thread.
    // Spawned Thread 1
    thread::spawn(move || { 
        let vals = vec![
            String::from("hi"),
            String::from("from"),
            String::from("the"),
            String::from("thread"),
        ];
        for val in vals {
            tx.send(val).unwrap(); 
            thread::sleep(Duration::from_secs(1));
        }
    });

    // Spawned Thread 2
    thread::spawn(move || { 
        let vals = vec![
            String::from("more"),
            String::from("message"),
            String::from("for"),
            String::from("you"),
        ];
        for val in vals {
            tx2.send(val).unwrap(); 
            thread::sleep(Duration::from_secs(1));
        }
    });

    // Receiver in main thread receives messages from both spawned threads
    for received in rx {
        println!("Got: {}", received);
    }
}
```

**`cargo run`** —>   
	Got: hi  
	Got: more  
	Got: message  
	Got: from   
	Got: the   
	Got: for   
	Got: thread   
	Got: you   

^^^**We can see that the messages from each thread are being sent non-deterministically** (i.e., alternating between messages from each thread — `hi` from first thread, `more` from second thread, `message` from second thread,`from` from first thread…)

## Sharing State

- We can **transfer data using shared state.**

- Think about **<ins>message passing</ins> as <ins>one-way data flow</ins> — one thread passes a message to another thread and then that receiving thread now owns the data.** 

- On the other hand, with **<ins>shared state concurrency</ins>**, we have **some piece of data in memory that multiple threads can read and write to.**

### The API of `Mutex`
- **<ins>`Mutex`</ins>** — An abbreviation for **mutual exclusion**. Mutual exclusion means that you **have some piece of data and only one thread could access that piece of data at any given time.** 

- To achieve this, Mutexes use a **<ins>locking system</ins>** — **<ins>when a thread wants access to a piece of data behind a `Mutex`, it will signal that it wants access to that data and acquire the Mutex’s lock.</ins>**

    - The **lock** is a data structure that **keeps track of which thread has exclusive access to the piece of data.**

    - **Once a thread has acquired a lock on a particular piece of data, no other thread can access that data.**

    - **Once the thread is done with the piece of data, it can unlock the data and allow other threads to have access to it.**

- **Mutexes** have a **reputation for being hard to manage**, because you have to remember **two rules**:

    1. **You have to acquire a lock before you have access to data.**

    2. **You have to release the lock when you’re done with the data, so that other threads can have access.** 

^^^^This is a **pain point** that may lead people away from using Mutexes, but **Rust’s type system and ownership rules guarantee that you can’t get locking and unlocking wrong!!!!**

### Using a `Mutex` in Rust:

```Rust
use std::sync::Mutex;	// import `Mutex` from the standard library

fn main() {
    let m = Mutex::new(5);	// create a new `Mutex` that holds the integer 5
				// `new()` creates the new `Mutex` in an unlocked state ready for use.

    // Access the data in our Mutex in an inner scope 
    {
        let mut num = m.lock().unwrap();    // Call the `lock()` method to acquire a lock on the `Mutex`.	
					    //
					    // `lock()` blocks the current/local thread until it successfully
				            // acquires the lock.
					    //
					    // `lock()` returns a `Result` type --
					    //	    `Result<MutexGuard<T>, PoisonError<MutexGuard<T>>>`.
					    //
					    //  `Ok(MutexGuard<T>)` means the lock was successfully
					    //   acquired, and `MutexGuard` is a smart pointer that provides
					    //   mutable access to the inner data (`T`). The `Deref` trait of the
					    //   `MutexGuard` smart pointer points to the inner data of the
					    //    `Mutex`. Also, `MutexGuard` implements the `Drop` trait, such that
					    //    when `MutexGuard` goes out of scope, it automatically
					    //    releases the lock to the data. This means that releasing the
					    //    lock is done for you so you don't have to remember.
					    //
					    //  `Err(PoisonError)` occurs if another thread that previously
					    //   held the lock **panicked** while it held the lock. In other
					    //   words, suppose you have a `Mutex` protecting some shared
					    //   data. Suppose one thread acquires the lock, starts modifying the
					    //   data, and then, before releasing the lock, that thread
					    //   experiences a panic. A panic in Rust means the thread
					    //   immediately unwinds its stack and exits. If this happens while a
					    //   `Mutex` lock is held, the data protected by that `Mutex` might be
					    //   left in an inconsistent or partially modified state. For example,
					    //   if it was incrementing a counter, it might have only partially
					    //   completed the operation, or if it was reordering a list, it might
					    //   have left the list in a broken state. This "poisons" the `Mutex`,
					    //   indicating the inner data might be in an inconsistent state. To
					    //   indicate this, `lock()` returns `Err(PoisonError)`, which is designed
					    //   to prevent other threads from unknowingly operating on
					    //   potentially corrupt data. Calling `.unwrap()` here will panic if
					    //   such an error occurs.
					    //
					    // Once `lock()` returns, the current thread is guaranteed to be
					    // the sole holder of the lock.
        
        // Use the mutable `MutexGuard` to manipulate the underlying data with the dereference operator *
        *num = 6;

    }   // inner scope ends so the `MutexGuard` goes out of scope and the lock is released.

    println!("m = {:?}", m);

}
```
### `Mutex` Interior Mutability with `Arc`

- **<ins>`Mutex` uses interior mutability</ins>** — i**n the same way that a `RefCell` smart pointer allows you to mutate a value that’s inside a `Rc` smart pointer (`Rc<RefCell<T>>`), the `Mutex` smart pointer allows you to mutate a value that's inside an `Arc` smart pointer (`Arc<Mutex<T>>`)**.

    - The `RefCell` smart pointer comes with the risk of creating circular dependencies, the **`Mutex` smart pointer comes with the risk of creating deadlocks.** 
    - <ins>See the example below…</ins>

- **<ins>Sharing `Mutex` Between Multiple Threads:</ins>** We create a new `Mutex` that holds the integer 0. Then, we will spin up 10 threads that each increment the `Mutex` value by 1. At the end, the `Mutex` value should be 10. <ins>See below:</ins>

```Rust
use std::sync::{Arc, Mutex};	// import the Atomic Rc (`Arc`) smart pointer, provides the same functionality as the
				// the `Rc` smart pointer of allowing multiple owners (shared ownership) but it
				// thread safe! See below comments for more info.

use std::thread;
use std::rc::Rc;	// this doesn't work for us bc not thread safe :(, but we need its exact
			// functionality, which Atomic Rc gives us.

fn main() {
    //let counter = Rc::new(Mutex::new(0));	// use `Rc` so the counter can have multiple owners, BUT NOT THREAD SAFE SO CAN'T USE!!

    let counter = Arc::new(Mutex::new(0)); 	// use `Arc` so that the counter can have multiple owners and bc `Arc` is
						// thread safe, unlike `Rc`.
						// As explained above, `Mutex` uses interior mutability, so it allows
						// us to mutate the count inside the `Arc` smart pointer even though
						// the `Arc` itself provides only shared, immutable access to its contents.


    // Create a mutable vector that stores all 10 threads.
    mut handles = vec![];

    for _ in 0..10 {

        // Important notes about `Arc`:
        // Just like `Rc`, `Arc::clone` increases the reference count of the `counter` variable, which stores `Arc<Mutex<i32>>`.
        // It creates a new `Arc` pointer that points to and shares ownership of the same underlying data as the 
        // original `counter`. Each spawned thread will then take ownership of one of these cloned `Arc` 
        // pointers, allowing multiple threads to share ownership of the same `Mutex` (and thus the same
	// `i32` counter) safely.
        //
        let counter = Arc::clone(&counter);

        // `handle` contains the new spawn thread
        let handle = thread::spawn(move || {	// use `move` to move the `counter` variable into the thread.
						// ERROR: "cannot move counter bc it was already moved into
						// the closure in the previous iteration of the for loop"
						//
						//  ^^^SOLUTION 1: we allow `counter` to have multiple owners
						// with the `Rc` smart pointer above
						//
						// ^^^ERROR 2: "`Rc<Mutex<i32>>` cannot be sent between
						// threads safely" -- the `Rc` smart pointer gives us the
						// functionality we want, but unfortunately, it's not thread safe.
						// We want something that's exactly like `Rc`, but thread safe.
						//
						//  ^^^SOLUTION 2: Rust standard library has the Atomic Rc (`Arc`)
						// smart pointer. Same functionality as `Rc` but thread safe!
						// Atomics are a concurrency primitive. They are like primitive
						// types except that they can be shared across threads.

	    // The `Arc` smart pointer automatically dereferences to the `Mutex<i32>` inside it when we call
            // `.lock()` to acquire a lock on the `Mutex`. The `.lock()` method returns a
	    // `Result` type that, if successful, contains a `MutexGuard<i32>` in the `Ok` variant.
  	    // We use `.unwrap()` to extract this `MutexGuard`. The `MutexGuard` itself acts as
	    // a smart pointer and we can use `*` to access the inner i32 in the `MutexGuard` and mutate it.
            let mut num = counter.lock().unwrap();
            *num += 1;
	    //^^^
	    // The way the above code works is the following...
	    //    1. One Thread Acquires the Lock: Only one thread at a time can successfully acquire the
	    //       `Mutex` lock. Whichever thread's `counter.lock()` call happens to execute first will
	    //       find the lock available and obtain it.
	    //       
	    //    2. Other Threads Wait: If a thread calls `counter.lock()` and the `Mutex` is already locked
	    //       by another thread, that calling thread will block (pause its execution) until the lock is released.
	    //
	    //    3. The thread that successfully acquired the lock will increment the count.
	    //
	    //    4. `MutexGuard` is dropped and the lock is automatically released. 
	    //
	    //    5. Another Thread Acquires the Lock: Once the lock is released by the previous
	    //       thread, one of the waiting threads (the order is not guaranteed and depends
	    //       on the operating system's scheduler) will be unblocked and will then acquire the lock.

        });
        handles.push(handle);	// after the new spawn thread is created, append it to the vector of threads
    }

    // After acquiring the threads, join them all to the main thread, meaning that we block the main thread 
    // from terminating until all of the spawned threads finish execution.
    for handle in handles {
        handle.join().unwrap();
    }
    println!("Result: {}", *counter.lock().unwrap())	// have to acquire lock, unwrap to get the `MutexGuard`,
							// and dereference to get int.
}
```

**The Rust language itself provides few concurrency features**, but it does give you the building blocks to create your own concurrency features or use concurrency features written by others. 

- Two basic concurrency concepts provided to you as building blocks by the standard library are the `Send` and `Sync` traits.

---

# Object Oriented Programming in Rust

- There are many different competing definitions describing what object-oriented programming is. Some of these definitions would classify Rust as an object-oriented programming language and others would not. 

<br>There are arguably <ins>3 characteristics that most object-oriented programming languages share</ins>:

### 1. **<ins>Objects</ins>**

- Made out of **data and methods that operate on that data.**
   
- In Rust, **Structs** and **Enums** hold data and you can use implementation blocks to create methods on the structs and enums.
   
	- So, Structs and Enums provide the **same functionality as Objects**.

### 2. **<ins>Encapsulation</ins>**

- Means that **implementation details of an Object are hidden from the code using that object.**
   
- **Instead of changing the internals directly, the code outside of the object is limited to interacting with the object through its public API (i.e., public methods).** This enables the programmer to change the internals of an object without changing code which uses that object.
   
- **In Rust, everything is private by default**, but you can use the **`pub`** keyword to **decide which modules, types, functions, and methods are public.**
   
- <ins>Example</ins>:

```Rust

// struct is public so code outside of this library can use our struct.
pub struct AveragedCollection { 

    // BUT, the fields are private, so outside code can't manipulate these fields directly. Instead, they  
    // have to use the methods in the implementation block below which modify the internal state.
    list: Vec<i32>,
    average: f64,	// average of the numbers in the list
}

impl AveragedCollection {

    // Add a new value to the list and update the average of the list accordingly.
    pub fn add(&mut self, value: i32) {
        self.list.push(value);
        self.update_average();
    }

    // Remove the last element from the list (if the list is not empty) and update the list accordingly.
    pub fn remove(&mut self) -> Option<i32> {
        let result = self.list.pop();	// `pop()` removes the last element from a vector and return it in
					// `Some`, or None if the vector is empty.
        match result {
            Some(value) => {
                self.update_average();
                Some(value)
            }
            None => None
        }
    }

    // Return the current average of the list (stored in the `average` field)
    // We don't have to do any extra work here bc the `add()` and `remove()` methods that modify the list
    // make sure to update the average of the accordingly. 
    //
    pub fn average(&self) -> f64 {
        self.average
    }

    // Updates the average of the list in the 'average' field
    // Private method, bc code outside the struct doesn’t needed to call it
    fn update_average(&mut self) {
        let total: i32 = self.list.iter().sum();
        self.average = total as f64 / self.list.len() as f64;
    }
}
```
^^^^IN THE ABOVE, **we encapsulate the internals of the struct** (i.e., we **make the fields of the struct private**) so **code outside of the struct can’t change the internals directly and is limited to interacting with it through its public API**. 

BC WE DO THIS, **we can change the internals without changing code that uses our structure**. **For example, we can switch from storing our list of numbers in a Vector and use a Hashset**. We would **then** need to **change** the **`add()` and `remove()` methods** to add and remove numbers from the hashset, BUT **as long as our public `add()` and `remove()` methods have the same signature, code using our struct doesn’t have to change.**

- <ins>LESSON:</ins> **In Rust, the fact that everything is private by default but you can use the `pub` keyword to make things public, gives you the ability to encapsulate implementation details in Rust.**

### 3. **<ins>Inheritance</ins>**

- **Inheritance is the ability for an object to inherit from another object’s definition, gaining the data and behavior of that other object without having to define the data and behavior itself.**

- **Rust does not have this ability**; specifically, you can’t define a structure that inherits fields and methods from another struct.

- **However**, **Rust does have some other tools you can use depending on why you’re reaching for inheritance**. There are <ins>two main reasons for using inheritance</ins>:

	1. **<ins>Code Sharing</ins>** — you can implement behavior on one type and then all the other types that inherit from it can reuse that behavior.  
		
  		- In **Rust**, you can accomplish the same thing by using **default trait method implementations**. <ins>NOTE:</ins> there is a limitation, as of this video, traits can only define methods, not fields.

	2. **<ins>Polymorphism</ins>** — **allows you to substitute multiple objects for each other at runtime if they share certain characteristics.** In classical inheritance, this shared characteristic is a parent class. For example, you could have a **base class called vehicle and then subclasses that inherit from vehicle such as truck, motorcycle, or car**. Then, you can **define a function which takes in a vehicle and then at runtime you can pass in a truck, motorcycle, or car into the function.**

		- **Rust takes a MUCH different approach**. In Rust, you can use **generics** to abstract away concrete types and you can use **trait bounds** to restrict the characteristics of the generics (e.g., the generic type has to implement the Debug trait). 

		- In addition, Rust provides **trait objects**, which are similar to generics except they use dynamic dispatch, whereas generics use static dispatch. See next section for more info on trait objects.

---

# Trait Objects in Rust

 As explained in the previous section, Rust doesn’t support classical inheritance; however, **Rust achieves polymorphism**, which is the **ability for code to work on multiple types of data through trait objects.**

<ins>Example:</ins> Imagine you are building a GUI (graphical user interface) library. The goal of this library is to take in a list of visual elements, such as buttons, text boxes, sliders, etc., and be able to draw them to the screen. In addition, we would like users of our library to be able to extend our library, meaning they could create their own visual components that are able to be drawn to the screen. This means that **at compile time, we won’t know the full breadth of objects that are going to be used; however, we do know that all of these visual objects are going to have a method called `draw()` which we can execute.**

- **Classical Inheritance:** If we were using a language with classical inheritance, then we might create a base class called visual component, which has a `draw()` method. Then, other visual components, such as buttons, text boxes, and sliders, can inherit from the visual component base class and thus inherit the `draw()` method. They could also overwrite the `draw()` method with their own implementation.

- **Trait Objects in Rust:** **In Rust, we define shared behavior using traits**. We create a trait called `Draw` which has one method called `draw()`… <ins>see this below</ins>

**<ins>lib.rs</ins>**
```Rust
// Define a public trait called `Draw`
pub trait Draw {
    fn draw(&self);	// The `Draw` trait requires that we implement one method 
    			// called `draw(&self)` which takes a reference to `self`.
}

// Define a struct called `Screen` which holds a public list of drawable components.
pub struct Screen {
    pub components: Vec<Box<dyn Draw>>,    // Public field called `components` which is a Vector of 
					   // `Box` smart pointers, where each `Box` contains any type
					   // that implements the `Draw` trait. 
					   //
					   // `components` = Vector of trait objects `Box<dyn Draw>`
					   //
					   //  - We define a trait object by first specifying some sort 
					   //     of pointer, such as a reference or a `Box` smart pointer, 
					   //     and then using the `dyn` keyword followed by the 
					   //     relevant trait.
					   //
					   //  - Because we use trait objects `Box<dyn Draw>`, Rust
					   //     will ensure at compile time that any type in the 
					   //     `components` Vector implements the `Draw` trait.
					   //
					   //  - NOTE: we discuss why trait objects need to use some 
					   //     sort of pointer in a later section.
					   // 
					   //  - The `dyn` keyword stands for dynamic dispatch.
					   //
					   // Why not use generics instead of trait objects? like the
					   // below...
					   //      pub struct Screen<T:Draw> {
					   //          pub components: Vec<T>,   // Vector of components 
					   //                                    // where each component 												   //                                    // is of generic type `T`. `T`
					   //                                    // must implement the
					   //                                    // `Draw` trait.
					   //      }
					   //  ^^^THE CRUCIAL DIFFERENCE with the above 
					   // compared to our trait object implementation is that
					   // it limits the `components` Vector to items of one type 
					   // (e.g., just buttons, just sliders,  just text input fields, 
					   // etc.) -- the `components` vector has to be 
					   // homogenous. `components` can't store a mixture of 
					   // types that implement the `Draw` trait, which is what we 
					   // want and what the trait object implementation gives us 
					   // (e.g., a list of buttons, sliders, and text input fields mixed 
					   // together). 
					   //      
					   // LESSON: If you want the list to be homogenous, then 
					   // you should use Generics with trait bounds as there is no 
					   // runtime cost. However, if you need the flexibility to store 
					   // any type that implements a certain trait, then use trait 
					   // objects, which do have a performance cost.
}

impl Screen {
    // `run()` iterates through the `components` vector and draws the items to the screen
    pub fn run(&self) {
        for component in self.components.iter() {	// we have to use `.iter()` otherwise if we 
							// do `for component in self.components`, then Rust would try 
       							// to take ownership of the `self.components` vector 
	      						// and then move each `Box<dyn Draw>` out of the vector 
	     						// and into the `component` variable during each 
	    						// iteration. Bc `self` is an immutable reference (`&self`), 
	   						// we can't move `self.components` out of it bc you 
	  						// can't move data out of something you only have an 
							// immutable reference to. As a result, without `.iter()`, 
       							// we get the compile-time error "cannot move out of 
	      						// self.components because it is behind an & reference".
            component.draw()
        }
    }
}
```

<ins>Implementing drawable components…</ins> **i.e., implementing structs that implement the `Draw` trait…**

- **Each drawable component can have whatever fields are relevant to that component, there is no set template or required set of fields.**
	- For example, a `Button` component may have just `width` and `height` fields, whereas a `TextInput` component may have a `text` field.

- **Each drawable component can have custom functionality**. They **all have to implement the `Draw` trait with its `draw(&self)` method, but they can have other methods defined as well that are unique to them.**
	- For example, the `Button` component might have an `on-click handler` which is a function that does something when the user clicks a button. Other components may not have this function.

**<ins>lib.rs continued</ins>**

```Rust
// `Button` component
pub struct Button {
    // These are the fields relevant to a `Button` component, but a `TextInput` component might
    // have different fields.
    pub width: u32,
    pub height: u32,
    pub label: String,
}
// Implement the `Draw` trait for our `Button` component. `Draw` trait requires that we implement one method  
// called `draw(&self)` which takes a reference to `self`.
impl Draw for Button {
    fn draw(&self) {
        // draw button
    }
}
```

<ins>How do consumers of our library define their own drawable components?</ins>

**<ins>main.rs</ins>**

```Rust

// Import the `Draw` trait from our GUI library (lib.rs), as well as `Screen` and `Button`.
use gui_lib::{Draw, Screen, Button};

// With the `Draw` trait in scope, define another drawable component called `SelectBox`.
struct SelectBox {
    width: u32,
    height: u32,
    options: Vec<String>,
}
// Implement the `Draw` trait for the `SelectBox` component. `Draw` trait requires that we implement one 
// method called `draw(&self)` which takes a reference to `self`.
impl Draw for SelectBox {
    fn draw(&self) {
        // draw select box
    }
}

// Use our GUI library inside of `main`
fn main() {
    // Create an instance of our `Screen` struct. `components` field stores a Vector of `Box` smart pointers, 
    // where each `Box` contains any type that implements the `Draw` trait.
    let screen = Screen {
        components: vec![
            // The first drawable component is a `SelectBox`
            Box::new(SelectBox {
                width: 100,
                height: 100,
                options: vec![String::from("yes"), String::from("no"), String::from("maybe")],
            }),
            // The second drawable component is a `Button`
            Box::new(Button {
                width: 100,
                height: 100,
                label: String::from("ok"),
            })
        ],
    };

    // `run()` iterates through the `components` vector and draws the items to the screen
    screen.run();
}
```
^^^**<ins>NOTE:</ins>** IN THE ABOVE, if we tried to **add an object to the `components` vector that DOES NOT implement the `Draw` trait…**	

<img width="739" alt="Image" src="https://github.com/user-attachments/assets/2558bd84-5e8c-47eb-8b75-223e1dbae0f1" />

^^^THIS is a **very helpful error message** that even tells us which types implement `Draw` and are thus eligible to be added to the `components` vector.

## Static vs. Dynamic Dispatch

**Monomorphization** (<ins>see earlier explanation/example of this using command-f</ins>) 

- **Happens when we use generics and trait bounds**.

- A process where the **compiler will generate non-generic implementations of functions based on the concrete types used in place of generic types.**

- For example, **suppose you have a generic `add<T>(x: T, y: T)` function that takes two generic parameters and adds them**. **Suppose the function is used with both `f64` (floating-point) and `i32` (integer) types**. The **compiler will generate separate, optimized versions of `add` like `add_f64(x: f64, y: f64)` and `add_i32(x: i32, y: i32)`**. It then **replaces each call to the generic `add` function with the appropriate specialized versio**n. This essentially means **we get a specific, non-generic implementation of the `add` function for each concrete usage.**

- **This is called <ins>static dispatch</ins>** — static dispatch is **when the compiler knows the concrete functions you’re calling at compile time.**

<br>The opposite is **<ins>dynamic dispatch</ins>** — happens **when the compiler DOES NOT know the concrete functions you’re calling at compile time**. INSTEAD, it **figures out the concrete functions you’re calling at runtime**. 

- When using **trait objects**, the **Rust compiler must use dynamic dispatch**, because, at compile time, the compiler doesn’t know all of the concrete objects that are going to be used. 

- INSTEAD, the **compiler will add code to figure out the correct method to call at runtime, which means there is a runtime performance cost**. The **upside is you get to write flexible code that can accept any object that implements a certain trait.**

## Object Safety for Trait Objects

- **ONLY traits that are <ins>object safe</ins> can be used to create trait objects.**

- What does it mean for a **trait** to be **object safe**? **A trait is object safe when all of the methods implemented on that trait have these two properties…**
	1. **The return type is not `self`**
	2. **There are no generic parameters**

- If a trait DOES NOT have the above two properties, then the Rust compiler can’t figure out the concrete type of that trait and therefore doesn’t know the correct method to call.

---

# State Design Pattern in Rust

Implementing the state object oriented pattern using Rust.

- **In the state pattern, we have some value which has internal state, and that internal state is represented by state objects.**

    - **<ins>Each state object is responsible for its own behavior and deciding when to transition into another state.</ins>**
 
    - **<ins>The value that holds the state objects knows nothing about the different behaviors of states or when to transition to different states.</ins>**

-  The benefits of using the state pattern is that when business requirements change, we don’t need to change the code which uses the value; instead, we simply need to change code inside one of the state objects or perhaps add new state objects.

<ins>Example:</ins> **Implementing a Blog post workflow in Rust…**

1. A Blog post **starts off as an empty draft**.

2. Once the draft is done, **then a review of the post is required.**

    - Make sure that changes to the blog post follow a specific sequence: If somebody attempts to review a blog post before a review is requested, then that blog post should remain in a draft state. 

4. **Once the post is approved, it gets published**. **Only published posts return content for print** (i.e., unpublished blog posts cannot be printed).

**<ins>main.rs</ins>**
```Rust
use blog::Post;

fn main() {
    let mut post = Post::new();    // create a new `Blog` post, in `Draft` state 

    post.add_text("I ate a salad for lunch today");     // call `add_text()` method to populate the post with text.
    
    assert_eq!("", post.content());    // assert that calling `post.content()` returns an empty string bc the post
				       // is in a `Draft` state, not a `Published` state, and only `Published` posts 
	   			       // return content for print.

    post.request_review();	// call `request_review()` to move the `Blog` from `Draft` state to being in review
    assert_eq!("", post.content());    // assert that `post.content()` still returns an empty string bc has not
                                       // yet been approved so it is not in a `Published` state, and only `Published`
				       // posts return content for print.


    post.approve();	// use `approve()` method to approve the post, moving it to a `Published` state.
    assert_eq!("I ate a salad for lunch today", post.content());    // `post` is in a `Published` state so it can 
    								    // return content for print.
}
```

^^^**IN THE ABOVE, we only interact with the `Post` type...**

- The **`Post` type will store a value representing the state of the post**, which could be either **`Draft`, `PendingReview`, or `Published`.**

- **The state will change in response to methods being called on the `Post` type, BUT, `Post` type doesn't know the logic about when to transition to different states and what states to transition to, THIS is defined in the state objects.** 

- Users won't be allowed to make a mistake such as publishing a `Post` before it has been reviewed.

<ins>Defining the `Post` type in lib.rs according to the above notes:</ins>

**<ins>lib.rs</ins>**
```Rust
pub struct Post {
    state: Option<Box<dyn State>>,    // `state`` is an optional `State` trait object wrapped in a `Box`
    content: String,
}
impl Post {
    // Because the fields of the `Post` struct are private, the only way to create a new `Post` instance
    // is using the below constructor. This constructor, called `new()` creates a new `Post` with the state
    // set to the `Draft` state, which ensures that when a `Post` is created, it's always going to start
    // off in a `Draft` state. 
    //
    pub fn new() -> Post {
        Post {
            state: Some(Box::new(Draft {})),    // the initial state is the `Draft` state
            content: String::new(),
        }
    }

    // The `content` field is private so outside code can't modify it directly. As a result, we add
    // a public method that allows user's to modify the internal `content` field in order to add/append
    // text to the `Post`. 
    // This `add_text()` functionality doesn't depend on the state the post is in, so it is not part of
    // the state pattern. You can see this from the fact that the `add_text()` method doesn't interact
    // with the `state` field. 
    //
    pub fn add_text(&mut self, text: &str) {
        self.content.push_str(text);
    }

    // Once again, `content` field is private so we must add a public method that allows outside code
    // to return its value.
    //
    // `content()` is part of our state pattern: it returns an empty string if the post is not in a 
    // `Published` state. If the post is in a `Published` state, then it returns the contents of the `Post`. 
    // The goal is to keep all of the rules like this within the `State` trait objects and not in this 
    // `Post` class, so the rules are not in this `Post.content()` method and instead in the State trait
    // object implementations. 
    //
    pub fn content(&self) -> &str { 

        // self.state is an `Optional` that owns the `State` trait object wrapped in a `Box`. We want a reference to
        // the State trait object so call `as_ref()`. We know that there is always going to be a valid state object,
        // so we can call `unwrap` to get the value in `Some` without having to worry about it panicking. Then, we
        // have `&Box<dyn State>` (`State` trait object wrapped in `Box`) which calls its `content()` method passing 
        // in the current `Post`. We can call `content()` even though we have `&Box<dyn State>` instead of `&dyn State`
        // (reference to a `State` trait object) bc of Deref coercion.
        //
        // `Option<Box<dyn State>>`     —>     `Option<&Box<dyn State>>`     —>     `&Box<dyn State>`
        // then call `.content(self)` on `&Box<dyn State>` to return `&str`
        //
        // The `content()` method of the `State` trait objects takes a reference to the current `Post` (`self`) so 
        // that it has access to the `content` field.
        //
        self.state.as_ref().unwrap().content(self)
    }

    // Public `request_review()` method that modifies the `state` field.
    // We can see some of the advantages of the state design pattern: The `request_review()` method on 
    // the `Post` struct is the same no matter what state we’re in (just like the `content` method above).
    // Instead, each state is responsible for its 
    // own rules that govern what happens when we call the `request_review()` trait method on that 
    // particular `State` trait object. 
    //
    pub fn request_review(&mut self) {

        // `self.state` contains an `Option`. `take()` takes the value out of the `Option`, leaving a `[None]` in
        // its place. SO we are moving the value inside our `Option` (i.e., the state) outside of the `Option`
        // and into the `state` variable here which gains ownership of the value. This is why we needed to 
        // make the `state` field on the `Post` struct optional, bc in this case, we move the state out of our 
        // `Post` instance but Rust doesn't allow unpopulated struct fields. BUT, with an optional value we're 
        // able to call `take()` which will give us ownership of the `state` field and in its place it's going to leave 
        // the `None` variant. 
        // 
        match self.state.take() {        

            // If the state exists, call `.request_review()` on it to get the new state
            // After calling `take()`, the value in `self.state` is moved into the `state` variable, so the 
            // `state` variable has ownership of the value and `self.state` is `None` here when we do 
            // `self.state =`. We then reassign `self.state` to a `Some` variant and inside we call the 
            // `request_review()` method on `state`. `request_review()` consumes the current state in 
            // `state`, invalidates it, and returns a new state (`PendingReview` if the current state is `Draft`, 
            // `PendingReview` if the current state is `PendingReview`, `self` if `Published`).
            //
            Some(state) => self.state = Some(state.request_review()),

            // If the state doesn't exit, do nothing.
            None => ()
        };
    }

    // Public `approve()` method that modifies the `state` field. Very similar to `request_review()`
    pub fn approve(&mut self) {
        match self.state.take() {        
            Some(state) => self.state = Some(state.approve()),
            None => ()
        };
    }
}

// `State` trait, defines shared behavior between the various states of a `Post` (i.e., the `State`
// trait objects: `Draft`, `PendingReview`, and `Published`).
trait State {

    // `request_review()` takes ownership of a `Box` containing `Self` (bc no `&`). `Self` contains the current
    // state (i.e., `dyn State` like `Draft`) bc this method is defined with structs implementing the `State` trait, like `Draft` and 
    // `PendingReview`.
    //
    // Why Not Just Use `Self` Instead of `Box<Self>`? We call `request_review()` on a 
    // `Box<dyn State>`, but the main reason is because `Self` can be any of the concrete types (`Draft`, 
    // `PendingReview`, `Published`) so it is a dynamically sized type (DST), and Rust needs to know the size of a 
    // type at compile time to move it by value. As a result, we take ownership of the fixed-size pointer (`Box`) 
    // that manages the dynamically sized data.
    //
    // `request_review()` returns a `State` trait object (i.e., any type that implements the `State` trait, wrapped in 
    // a `Box`). Doesn't have a default implementation, so requires a custom implementation for each type /
    // struct that implements the `State` trait.
    //
    fn request_review(self: Box<Self>) -> Box<dyn State>;

    // `approve()` method just like `request_review` (same param and same return type)
    fn approve(self: Box<Self>) -> Box<dyn State>;

    // `content()` takes `&self`, which for a trait method defined on the `State` trait, means `&dyn State`.
    // Has a default implementation which returns an empty string. The `Draft` and `PendingReview` `State`
    // objects use this default because we return an empty string if the `Post` is not `Published`. 
    //
    fn content<'a>(&self, post: &'a Post) -> &'a str {    // see reason for lifetimes in the custom
							  // implementation in `Published`
        ""
    }
}

// The different `State` trait objects...

// `Draft` state
struct Draft {}
impl State for Draft {

    // As noted previously, `request_review()` takes ownership of a `Box` containing `Self` (bc no `&`) and `Self`
    // contains the current state (`dyn State`). In this custom implementation of `request_review()` for `Draft`, we don't
    // use `self` within the function, so we are essentially invalidating the current state (`Draft`) and then
    // returning a new state (`PendingReview`) that is used in its place.
    //
    fn request_review(self: Box<Self>) -> Box<dyn State> {
        Box::new(PendingReview {})
    }

    // A `Draft` state object can't be approved because it is not yet in review. So return `self`.
    fn approve(self: Box<Self>) -> Box<dyn State> {
        self
    }
}

// `PendingReview` state
struct PendingReview {}
impl State for PendingReview {

    // If we call `request_review()` on a `PendingReview` `State` object, then we don't want to invalidate the current
    // state (`PendingReview`), because the `Post` is already in review, so we return the current state in `self`.
    fn request_review(self: Box<Self>) -> Box<dyn State> {
        self
    }

    // If we call `approve()` on a `PendingReview` `State` object, then we transition into a `Published` state by
    // taking ownership of the current state in `self` and returning a new state (`Published`) that is used in its 
    // place.
    fn approve(self: Box<Self>) -> Box<dyn State> {
        Box::new(Published {})
    }
}

// `Published` state 
struct Published {}
impl State for Published {

    // If we call `request_review()` on a `Published` `State` object, it doesn't need to be reviewed bc it was already
    // reviewed and approved. So just return the current `Published` state.
    fn request_review(self: Box<Self>) -> Box<dyn State> {
        self
    }

    // If we call `approve()` on a `Published` `State` object, return `self` because it was already published.
    fn approve(self: Box<Self>) -> Box<dyn State> {
        self
    }

    // If the post is `Published`, then return a reference to the post's `content` field.
    fn content<'a>(&self, post: &'a Post) -> &'a str {
        &post.content    // the lifetime of the return type is tied to the lifetime of the post bc we return 
			 // `post.content`.
    }
}
```

## Extensions to the State Pattern

### Add a method called `reject()` that takes a post that’s `PendingReview` and return in to `Draft`

- This would be almost the same as `approve()`: `Draft`’s implementation would return `self`, `Published`’s implementation returns `self`, and `PendingReview`’s implementation returns a `Box::new(Draft {})` (i.e., `Draft` instance wrapped in `Box`).


### Require two approvals before a post is published

Introduce a new state and modify the `PendingReview` state's `approve` logic.

1. **Introduce a new state**: Let's call it `PendingSecondReview` or `AwaitingSecondApproval`. This state will represent the post after the first approval but before the second and final one. When `approve` is called on a `PendingSecondReview` post, it finally transitions to the `Published` state.

```Rust
struct PendingSecondReview {}

impl State for PendingSecondReview {
    fn request_review(self: Box<Self>) -> Box<dyn State> {
        self	// if we are already in `SecondReview`, don’t need to request review, return `self`
    }

    fn approve(self: Box<Self>) -> Box<dyn State> {
        Box::new(Published {})    // if call for approval when state = `PendingSecondReview`, then this is the second
				  // approval so we can publish and move to `Published` state!
    }
}
```

2. **Modify `PendingReview`'s `approve` method**: When `approve` is called on a `PendingReview` post, it should transition to the new `PendingSecondReview` state, not directly to `Published`.

```Rust

impl State for PendingReview {
    fn request_review(self: Box<Self>) -> Box<dyn State> {
        self
    }

    fn approve(self: Box<Self>) -> Box<dyn State> {
        Box::new(PendingSecondReview {})    // first approval → `PendingSecondReview`
    }
}
```

### Make it so that you can only add text to a post when it’s in `Draft` state

To only allow text to be added in the `Draft` state, you need to delegate the decision to the current state — just like with `content()`. 

1. **Add a method to the `State` trait to control adding text:**

```Rust
trait State {
    fn request_review(self: Box<Self>) -> Box<dyn State>;
    fn approve(self: Box<Self>) -> Box<dyn State>;
    fn content<'a>(&self, post: &'a Post) -> &'a str {
        ""
    }

    // Whether text can be added in the current state. By default, it can’t be added (Applies to `Published` and
    // `PendingReview` `State` trait objects so they use the default implementation).
    fn can_add_text(&self) -> bool {
        false
    }
}
```

2. **Override `can_add_text` in `Draft` so that we can add text in `Draft` —> `can_add_text` return True**:

```Rust
impl State for Draft {
    fn request_review(self: Box<Self>) -> Box<dyn State> {
        Box::new(PendingReview {})
    }

    fn approve(self: Box<Self>) -> Box<dyn State> {
        self
    }

    fn can_add_text(&self) -> bool {
        true
    }
}
```

**3. Update `Post::add_text` to check the current state:**

```Rust
impl Post {
    pub fn add_text(&mut self, text: &str) {
        if self.state.as_ref().unwrap().can_add_text() {    // same method call in `pub content()`, see explan.
            self.content.push_str(text);
        } else {
            println!("Cannot add text unless the post is in Draft state.");
        }
    }
}
```

## Downsides of the State Design Pattern:

- **Some states are coupled to each other**
    - For example, if we wanted to add a state between `PendingReview` and `Published`. This state is going to be called `Scheduled`. After adding the `Scheduled` state, we would need to edit the `PendingReview` state such that when `approve()` is called it would transition to the `Scheduled` state instead of the Published state. 

- **Duplication:** For example, in `Post`, we have very similar implementations of the `request_review()` method and the `approve()` method. If we had many more methods with similar code, then we can consider using macros to reduce some of the repetition.

## Encoding States and Behaviors as Types (MUCH BETTER !!!)

By implementing the state pattern exactly as we would in an object oriented programming language, we’re **not taking full advantage of Rust’s strengths**. 

- We can **<ins>modify our library such that invalid states and transitions are compile time errors.</ins>**

- Rather than encapsulating states and transitions completely so that outside code has no knowledge of them, we’ll **encode different states as different types.**

- **Don’t use the `state` field anymore because we’re moving the encoding of state to the Type of the Struct.**

**<ins>lib.rs</ins>**
```Rust

use std::future::Pending;

// `Published` state
pub struct Post {
    content: String,    // private `content` field
}
impl Post {
    // The `new()` function in `Post` returns a `DraftPost`.
    // HERE, WE ENFORCE that all posts start in `Draft` state:  Bc the `content` field is private for `Post`, `DraftPost`,
    // and `PendingReviewPost`, AND this is the only constructor, the ONLY WAY to create new posts is via 
    // `Post::new()`, so all new posts must begin as a `DraftPost`.
    //
    pub fn new() -> DraftPost {
        DraftPost {
            content: String::new(),
        }
    }
    // HERE, WE ENFORCE that ONLY `Published` posts return content for print: Both `DraftPost` and
    // `PendingReviewPost` don't have `content()` methods and `content` field is private for all of the structs, so 
    // we can't get the `content` of a post when it is in the `Draft` or `PendingReview` states. THE ONLY WAY to 
    // get the `content` of the post is through the `content()` method in the `Published` state HERE. This matches 
    // our requirement that only `Published` posts return content for print.
    //
    pub fn content(&self) -> &str {
        &self.content
    }
}

// `Draft` state
pub struct DraftPost {
    content: String,    // private `content` field. `DraftPost` doesn't have its own `content()` method, so `DraftPosts`
                        // can’t print their `content`. This ensures we can only get `content` when `Published`.
}
impl DraftPost {
	
    // HERE, WE ENFORCE that you can ONLY add text to the post when its in the `Draft` state: The only type/struct that has a
    // method to modify `content` is the `Draft` state, which makes sense bc we require that you can only add 
    // text to the post in the `Draft` state.
    //
    pub fn add_text(&mut self, text: &str) {
        self.content.push_str(text);
    }

    // Method to get from the `DraftPost` state to the `PendingReviewPost` state
    // Takes ownership of `self` (no `&`), meaning that it consumes and invalidates the current state and  
    // returns the new state (`PendingReviewPost`).
    //
    // HERE, WE ENFORCE that you can ONLY get to `PendingReview` state from `Draft` state: This method is the only way to 
    // get a `PendingReviewPost` instance, so you can only get to the `PendingReview` state by calling 
    // `request_review()` on a post in the `Draft` state (`DraftPost`). 
    //
    pub fn request_review(self) -> PendingReviewPost {
        PendingReviewPost {
            content: self.content,
        }
    }
}

// `PendingReview` state
pub struct PendingReviewPost {
    content: String,    // private `content` field. `PendingReviewPost` doesn't have its own `content()` method, so
			// `PendingReviewPosts` can’t print their content. This ensures we can only get `content` when `Published`.
}
impl PendingReviewPost {

    // One method called `approve()` which returns an instance of `Post`, so you can get from the `PendingReview`
    // state to the `Published state` (`Post`). 
    // Takes ownership of `self` (no `&`), meaning that it consumes and invalidates the current state and  
    // returns the new state (`Post`).
    //
    // HERE, WE ENFORCE that you can ONLY get to `Published` state from the `PendingReview` state: This method is the 
    // only way to get a `Post` instance, so you can only get to the `Published` state by calling `approve()` on a post 
    // in the `PendingReview` state (`PendingReviewPost`)
    //
    pub fn approve(self) -> Post {
        Post {
            content: self.content,
        }
    }
}
```


**<ins>main.rs</ins>**
```Rust
use blog::Post;

fn main() {
    let mut post = Post::new();    // ONLY WAY to create new posts is via `Post::new()`, so all new posts
				   // must begin as a `DraftPost`.


    post.add_text("I ate a salad for lunch today");    // can ONLY add text to the `Post` in the `Draft` state
    // assert_eq!("", post.content())    // can't call `content()` until the post is `Published`, throws COMPILE TIME ERROR


    // NOTE: `request_review()` and `approve()` no longer change internal state, instead return a new post type, 
    // use shadowing

    let post = post.request_review();    // can ONLY get to the `PendingReview` state by calling
					 // `request_review()` on a post in the `Draft` state (`DraftPost`).
    // assert_eq!("", post.content())    // can't call `content()` until the post is `Published`, throws COMPILE TIME ERROR

    let post = post.approve();    // can ONLY get to the `Published` state by calling `approve()` on a
				  // post in the `PendingReview` state (`PendingReviewPost`)

    assert_eq!("I ate a salad for lunch today", post.content());  	// we are in `Published` state, ONLY `Published`
									// posts return content for print

}
```
**<ins>^^^^ THIS IMPLEMENTATION</ins> doesn’t quite follow the object oriented state pattern** anymore; however, the **advantage of it is that invalid states are impossible due to the type system and type checking.**

---

# Patterns

- **Patterns are a special syntax in Rust for matching against the structure of types**.

- **Patterns** consist of some combination of the following:
    - Literals
    - Destructed Arrays, Enums, Structs, or Tuples
    - Variables
    - Wildcards
    - Placeholders

^^^These components **describe the shape of the data we’re working with**, which we can then **match against values to determine whether our program has the correct data** to continue running a particular piece of code.

## Places where Patterns can be Used

### 1. Inside the Arms of `match` expressions — 

- **`match` arms consist of a pattern mapping to an expression:**

**`{pattern} => {expression}`**

- `match` expressions have to be **exhaustive** (i.e., every possible value for the variable we are matching on MUST be accounted for ). 

- If don’t want to individually specify every case, can use a **catch-all pattern**. I.e.,  if we go through all of the arms and none of them match the variable, then we execute this last catch-all arm. <ins>Examples of catch-all arms:</ins>

```Rust
_ => println!("Unsupported language :(“),    // In catch-all arm, if we DON’T want to bind to the
					     // variable we’re matching on, use  `_`

lang => println!(“Unsupported language! {:?}”, lang),	// If in the catch-all arm, we DO want to bind
							// to the variable we're matching on, specify a
							// variable name (e.g., `lang`) instead of `_`. 

```

- <ins>Example:</ins>

```Rust
#[derive(Debug)]
enum Language {
    English,
    Spanish,
    Russian,
    Japanese,
}
let language = Language::English;

// match on the value in `language`
match language {
    Language::English => println!("Hello World!"),
    Language::Spanish => println!("Hola Mundo!"),
    Language::Russian => println!("Hello World in Russian!"),
    _ => println!("Unsupported language :("),       	

    // lang: => println!(“Unsupported language! {}”, lang),
}
```

### 2. Conditional `if let` Expressions — 

- You can **use `if let` expressions if you want to match on some variable but you <ins>only care about one case.</ins>**

- **Downside of `if let` expressions**: the **compiler doesn’t enforce that they’re exhaustive**. For example, in the below, even if we delete the `else` block at the end, the code will still compile even though this might introduce a defect as we are not handling certain cases. 

- <ins>Example:</ins>

```Rust
let authorization_status: Option<&str> = None;
let is_admin = false;
let group_id: Result<u8, _> = "34".parse();

// If `authorization_status` is a `Some` variant, then store the string slice contained in `Some` in `status`
if let Some(status) = authorization_status {
    println!("Authorization status: {}", status);

// If `authorization_status` is a `None` variant, we enter this `else if` block.
// If `is_admin` is True, then print out "Authorization status: admin"
} else if is_admin {
    println!("Authorization status: admin")

// If `is_admin` is False, enter this `if let` expression.
// If `group_id` is an `Ok` variant, then store the integer contained in `Ok` in a new, shadowed `group_id` 
// variable and enter the `if else`.
} else if let Ok(group_id) = group_id {
    if group_id > 30 {
        println!("Authorization status: privileged");
    } else {
        println!("Authorization status: basic");
    }
} else {
    println!("Authorization status: guest");
}
```

### 3. `While let` Syntax — 

- `while let` syntax allows you to **run a loop as long as the pattern specified continues to match.**

- <ins>Example:</ins>

```Rust
let mut stack = Vec::new();
stack.push(1);
stack.push(2);
stack.push(3);

// `while let` matches on the return value of `stack.pop()`, which is an `Option`.
// If the `Option` variant returned is `Some`, then we store the value contained in `Some` in `top`.
// The loop keeps running while the `Option` variant returned from `stack.pop()` is `Some`, so the 
// loop exits when `stack.pop()` returns `None`, indicating that the stack is now empty.
//
while let Some(top) = stack.pop() {
    println!("{}", top);
}
```

### 4. `for` Loops — 

- <ins>Example:</ins>

```Rust
let v = vec!['a', 'b', 'c'];

// Call `for` on `v.iter().enumerate()`. `enumerate()` works just like Python returning
// tuples with (index in `v`, value in `v`). 
// We use the `(index, value)` pattern to destructure each tuple into two variables, `index` and `value`.
//
for (index, value) in v.iter().enumerate() {
    println!("{} is at index {}", value, index);
}
```

### 5. `let` Statements — 

- Surprisingly, patterns are used in `let` statements.

- <ins>Example 1:</ins>

```Rust
let x = 5;
```
^^^^^^^
- Here we declare a variable `x` and set it equal to 5
- More formally, it looks something like this: **`let PATTERN = EXPRESSION;`**
	- In our example, 
		- **`x` is an identifier pattern** (all identifier patterns are **irrefutable**), meaning it **matches any value and binds that value to the given identifier (`x`).**
		- The **expression (5)** is **matched against the pattern (`x`)**. **Since `x` is an identifier pattern, it successfully matches 5 and creates a new variable named `x` in the current scope, assigning the value 5 to it.**

- <ins>Example 2:</ins>

```Rust
let (x, y, z) = (1, 2, 3);
```
^^^^^
- Here, the **expression is the tuple `(1, 2, 3)`** which is **matched against the pattern `(x, y, z)`**, which **deconstructs the tuple.**

- Rust compares the tuple `(1, 2, 3)` to the pattern being used `(x, y, z)`, and in this case, they match because the **tuple has three elements** and the **pattern has three elements**. As a result, **1 binds to `x`, 2 binds to `y`, and 3 binds to `z`.**

- <ins>NOTE:</ins> **If the pattern DID NOT match (e.g., if the expression tuple had three elements and the pattern had two elements), then we would get a compile time error** (shown below). The error shows that we expect a tuple pattern that matches three integers, but we have a pattern `(x, y)` that only matches 2 values when the expression being evaluated has 3 values `(1, 2, 3)`.

<img width="665" alt="Image" src="https://github.com/user-attachments/assets/4dea6e4b-78d8-4499-b850-18ae19a95663" />

- <ins>NOTE:</ins> If we want to **ignore a value in the expression** being evaluated, **use an underscore `_`**:

```Rust
let (x, y, _) = (1, 2, 3);    //  bind 1 to `x`, bind 2 to `y`, and ignore the third value `3`
```

### 6. Function Parameters — 

- <ins>Example:</ins>
```Rust
fn main() {
    let point = (3, 5);
    print_coordinates(&point);    // call `print_coordinates()` passing in a reference to the `point` tuple `(3, 5)`.
}

// `print_coordinates()` deconstructs the passed in tuple into `x` and `y` using the pattern `(x, y)`.
//
fn print_coordinates(&(x, y): &(i32, i32)) {
    println!("Current location: ({}, {})", x, y);
}
```
^^^**THIS ALSO WORKS with closures**

## Irrefutable and Refutable Patterns

- **<ins>Irrefutable</ins>** — Irrefutable patterns are **patterns that will always match.**

	- <ins>Example:</ins> The **pattern `x` in the below example is irrefutable** because it will **always match no matter what the expression is**…

```Rust
let x = 5;
```

- **<ins>Refutable</ins>** — Refutable patterns are **patterns that might not match.**

	- <ins>Example:</ins>

```Rust
let x: Option<&str> = None;

if let Some(x) = x {    // Pattern matches the `Some` variant. If `x` is a `None` variant, which it is in
			// in this case, then this pattern will not match. 
    println!("{}", x);
}
```
	
- **The following can <ins>only accept irrefutable patterns</ins>:**
    1. **Function parameters**
    2. **`let` statements**
    3. **`for` loops**
  
^^^This is the bc the **program can’t do anything meaningful if the pattern fails to match.**

- **`if let` and `while let` expressions accept both irrefutable and refutable patterns**, but you’ll get a **compiler warning if you use an irrefutable pattern**, because by definition, **<ins>`if let` and `while let` are meant to handle matching failures</ins>**. For example, a **`while let` with a pattern that always matches will loop infinitely as opposed to stopping**, for example, when a list becomes empty or a counter reaches a particular point. 

- **<ins>IN GENERAL, you don’t need to worry about the distinction between refutable and irrefutable patterns.</ins>** However, you do **need to be familiar with the concept of refutability, so you can respond to compile time errors**… See two examples below...

<ins>Example 1 :</ins>
 
```Rust
let x: Option<&str> = None;
let Some(x) = x;    // `x` is a `None` variant, not `Some`, so this `let` never matches => ERROR
```

<img width="740" alt="Image" src="https://github.com/user-attachments/assets/9ab97073-50f9-4565-8d0d-a3c686b31b40" />

<ins>Example 2:</ins>

```Rust
let x: Option<&str> = None;

if let x = 5 {    // the pattern `x` will match any expression, so we will always enter this
		  // code block to print `x` making the `if let` useless. COMPILER WARNING
    println!("{}", x);
}
```

<img width="671" alt="Image" src="https://github.com/user-attachments/assets/5fab8079-325f-4e60-bf0c-9fcc921bef3c" />

---

# Pattern Syntax in Rust

This section discusses all the valid syntax you can use inside patterns and why you might want to use each one.

## Matching Against Literals:

- This pattern is **useful when you want your code to take action when it receives a concrete value.**

- <ins>Example:</ins>

```Rust
let x = 1;

// match on `x`, which is the integer 1
match x {
    // The pattern in the match arms is simply a literal (`1`, `2`, `3`, etc.)
    1 => println!("one"),
    2 => println!("two"),
    3 => println!("three"),
    _ => println!("anything"),
}
```

## Matching Named Variables:

- <ins>Example:</ins>

```Rust
let x = Some(5);    // `x` is a `Some` variant containing `5`
let y = 10;

// match on `x`, which is `Some(5)`
match x {
    // If `x` is a `Some` variant containing `50`...
    Some(50) => println!("Got 50"),

    // If `x` is a `Some` variant containing any other value, then bind that value to the local `y` variable…
    // 
    // This arm uses the named variable pattern, in this case `y` is the named variable.
    // 
    // NOTE: the match block creates a new scope, so variables defined within the match block shadow
    // variables defined outside. Specifically, in this case, the `y` defined inside the match block, will shadow 
    // the `y` defined earlier outside of the match block. As a result, in this `println!()` with `y`, the `y` that is 
    // printed contains the value stored in the `Some` variant. BUT, for the `x` println!() below in the catch-all
    // arm, this `x` is the same variable as defined above outside of the match block bc there's no variable 
    // named `x` defined inside this match block to shadow it.
    // 
    Some(y) => println!("Matched, y = {:?}", y),

    // Catch-all arm if previous two arms don't match
    _ => println!("Default case, x = {:?}", x),
}
```

## Matching Multiple Patterns:

- <ins>Example:</ins>

```Rust
let x = 1;

// match on `x`, which is the integer 1
match x {

    // `|` is an "or" operator, so here we say: if `x` is 1 or 2 or 3, then enter this arm...
    // 
    1 | 2 | 3 => println!("one or two or three"),

    4 => println!("four"),
    _ => println!("anything"),
}
```

## Matching Ranges of Values:

- <ins>NOTE:</ins> **the range operator only works on numeric values and characters**

- <ins>Example 1:</ins>

```Rust
let x = 5;

// match on `x`, which is the integer `5`
match x {

    // match the inclusive range of values [1, 5], so if `1 <= x <= 5`, then enter this arm...
    //
    1..=5 => println!("one through five inclusive"),

    _ => println!("something else"),
}
```

- <ins>Example 2:</ins>

```Rust
let x = 'c';

// match on `x`, which is the character `c`
match x {

     // if `x` is a character between `a` and `j` inclusive, then enter this arm...
    //
    'a'..='j' => println!("early ASCII letter"),

    // if `x` is a character between `k` and `z` inclusive, then enter this arm...
    //
    'k'..='z' => println!("late ASCII letter"),

    _ => println!("something else"),
}
```

## Patterns that Destructure Values (i.e, break apart values)

- We **can destructure structs, enums, tuples, and references in order to use different parts of these values.**

- <ins>Example 1:</ins> **Destructing structs**

```Rust
struct Point {
    x: i32,
    y: i32,
}

fn main() {
    let p = Point { x: 0, y: 7};    // create a new `Point` stored in `p` with `x = 0` and `y = 7`

    // Deconstruct `p`, which is a `Point` instance with `x = 0` and `y = 7`.
    // We create two variables, `a` and `b`.
    // `a` is mapped to whatever value is inside of the `x` field of `p`, so `a = 0`.
    // `b` is mapped to whatever value is inside of the `y` field of `p`, so `b = 7`.
    //
    let Point { x: a, y: b} = p;    // if we wanted to bind the values to the variables `x` and `y` instead
				    // of `a` and `b`, we would do: `let Point { x, y } = p;`

    assert_eq!(0, a);
    assert_eq!(7, b);
}
```

- <ins>Example 2:</ins> **When we are destructing a struct, we can use named variables and literals…**

```Rust
struct Point {
    x: i32,
    y: i32,
}

fn main() {
    let p = Point { x: 0, y: 7};    // create a new `Point` stored in `p` with `x = 0` and `y = 7`

    // match on `p`
    match p {

        // Match any `Point` where the `y` field =0. Bind the value in the `x` field to the local `x` variable.
        //
        Point { x, y: 0 } => {
            println!("On the x-axis at {}", x)
        },

        // Match any `Point` where the `x` field =0. Bind the value in the `y` field to the local `y` variable.
        // NOTE: This arm is only reached if the Point's `y` field != 0, due to the order of match arms.
        //	
        Point { x: 0, y } => {
            println!("On the y axis at {}", y)
        },

        // Match any `Point` instance no matter the values in the `x` and `y` fields. Bind the values to
        // the local `x` and `y` variables, respectively.
        // NOTE: This arm is a catch-all for all Points where `y` field != 0 and `x` field` != 0.
        //
        Point { x, y } => {
            println!("On neither axis: ({}, {})", x, y)
        }
    }
} 
```

- <ins>Example 3:</ins> **Destructing enums**

```Rust
enum Message {
    Quit,                        // variant with no values
    Move { x: i32, y: i32 },     // struct variant with two integer fields
    Write(String),               // tuple variant with one String value
    ChangeColor(i32, i32, i32),  // tuple variant with three integer values
}

fn main() {
    let msg = Message::ChangeColor(0, 160, 25);

    // Match on the `msg` variable which contains a variant of the `Message` enum.
    match msg {

        // If the variant is `Quit`...
        //
        Message::Quit => {
            println!("Quit");
        },

        // If the variant is `Move`, then destruct the struct: bind the values in the `x` and `y` fields to
        // the local `x` and `y` variables, respectively...
        //
        Message::Move {x, y} => {
            println!(
                "Move to x: {} y: {}",
                x, y
            )
        },

        // If the variant is `Write`, then extract the `String` value from the tuple and bind it to the
        // local `text` variable...
        //
        Message::Write(text) => {
            println!("Text message: {}", text)
        },

        // If the variant is `ChangeColor`, then destruct the tuple: bind the three integer values to
        // the local `r`, `g`, and `b` variables, respectively...
        //
        Message::ChangeColor(r, g, b) => {
            println!(
                "Change color: red {}, green {}, and blue {}",
                r, g, b
            )
        }
    }
}
```

- <ins>Example 4:</ins> **Destructing nested enums and structs**

 ```Rust
enum Color {
    Rgb(i32, i32, i32),     // a tuple of three integers
    Hsv(i32, i32, i32),     // a tuple of three integers
}

enum Message {
    Quit,                      
    Move { x: i32, y: i32 },   
    Write(String),             
    ChangeColor(Color),         // stores a variant of the `Color` enum
}

fn main() {
    // `msg` stores a `ChangeColor` variant of `Message` that contains an `Hsv` variant of `Color`
    let msg = 
        Message::ChangeColor(
            Color::Hsv(0, 160, 255)
        );

    // Match on the `msg` variable
    match msg {

        // Match on a `ChangeColor` variant that contains an `Rgb` variant. Bind the values
        // inside the `Rgb` variant to the local `r`, `g`, and `b` variables.
        //
        Message::ChangeColor(Color::Rgb(r, g, b)) => {
            println!(
                "Change color: red {}, green {}, and blue {}",
                r, g, b
            );
        },

        // Match on a `ChangeColor` variant that contains an `Hsv` variant. Bind the values
        // inside the `Hsv` variant to the local `h`, `s`, and `v` variables.
        Message::ChangeColor(Color::Hsv(h, s, v)) => {
            println!(
                "Change color: hue {}, saturation {}, and value {}",
                h, s, v
            );
        },
        _ => (),
    }
}
```

- <ins>Example 5:</ins> **More complex destructuring**

```Rust
struct Point {
    x: i32,
    y: i32,
}

fn main() {
    // From (3, 10), bind `3` to `feet`, bind `10` to `inches`, 
    // From Point {x: 3, y: -10}, bind `3` to `x`, bind `-10` to `y`
    //
    let ((feet, inches), Point {x, y}) = ((3, 10), Point {x: 3, y: -10});
}
```

## Ignoring Values in Patterns:

- <ins>Example 1:</ins> **<ins>Ignoring function parameters</ins>** — This can be **useful when you need a function signature to be something specific (e.g., implementing a trait method for a specific struct), but you're not going to use all the arguments passed in**. This stops the compiler from throwing a warning ("unused arguments”).

```Rust
fn main() {
    foo(3, 4);
}

// We use `_` as an argument name to have the `foo()` function completely ignore the first
// parameter passed into it.
//
fn foo(_: i32, y: i32) {
    println!("This code only uses the y parameter: {}", y);
}
```


- <ins>Example 2:</ins> **Ignoring part of a value**

```Rust
// Here, we are managing some setting, and the business requirement is that if the setting has no
// value, then we can set a new value. However, if the setting already has a value, then we can't 
// modify it. 
let mut setting_value = Some(5);    // the current setting
let new_setting_value = Some(10);   // the potential new setting if the current setting has no value

// Match on a tuple containing the current setting value and the potential new setting value
match (setting_value, new_setting_value) {

    // Match a tuple with two `Some` variants, use `_` bc we don't care what's stored in the `Some` variants.
    // If both the current setting value and the new setting value are `Some` variants...
    //
    (Some(_), Some(_)) => {
        println!("Can't overwrite an existing customized value");
    }

    // Otherwise, bc setting does not have a value (None variant), set the value...
    _ => {
        setting_value = new_setting_value;
    }
}

println!("setting is {:?}", setting_value)
```

- <ins>Example 3:</ins> **Using `_` in multiple places in one pattern to ignore particular values**

```Rust
let numbers = (2, 4, 8, 16, 32);

match numbers {

    // Ignore the 2nd and 4th value in the tuple
    //
    (first, _, third, _, fifth) => {
        println!("Some numbers: {}, {}, {}", first, third, fifth);
    }
}
```

- <ins>Example 4:</ins> If you’re prototyping and have an **unused variable that you don’t want the Rust compiler to complain about, you can prefix the variable name with an `_`.**

    - <ins>NOTE:</ins> **Prefixing a variable name with an `_` is different than using just an `_`. Prefixing a variable name with an `_` still binds the value.** For example, **in the below, the value 5 is still bound to the `x` field even though we prefix it with an `_` like `_x`**. On the other hand,**`_` (bare underscore) is a wildcard pattern that does not create a binding**.
 
<img width="163" alt="Image" src="https://github.com/user-attachments/assets/6b8cdb9f-1ab8-49ca-86f1-6a86652e1557" />

^^^ `y` has a yellow squiggly but `x` doesn’t because we prefix it with an `_`

- <ins>Example 5:</ins> **If you only care about certain parts of a value and want to ignore all of the other parts, then you can use the range syntax.** 

```Rust
struct Point {
    x: i32,
    y: i32,
    z: i32,
}

let origin = Point { x: 0, y: 0, z: 0 };

match origin {

    // This pattern binds the value in the `x` field to the local `x` variable, then using
    // the range syntax (`..`) ignores all of the other fields of the `Point` struct.
    //
    Point { x, ..} => println!("x is {}", x)
}
```

- <ins>Example 5.2:</ins> **The range syntax expands to as many values as it needs to be…**

```Rust
let numbers = (2, 4, 8, 16, 32);

match numbers {

    // This pattern binds the first value in the `numbers` tuple to the local variable `first`, it binds
    // the last value in the tuple to the local variable `last`, and it ignores all of the values in between. 
    //
    (first, .., last) => {
        println!("Some numbers: {}, {}", first, last);
    } 
}
```
^^^<ins>NOTE:</ins> **Using the range syntax `..` must be unambiguous.** For example, if we change the pattern in Example 5.2 to `(.., second, ..)`, then we would get an error because we have the range syntax on both sides of the `second` variable. In this case, Rust can’t determine what value the `second` variable should bind to: the first value in the tuple? The second? The third? The fourth? The fifth?


## Match Guards

- A **<ins>match guard</ins>** is an **extra if condition you can add to a match arm**. **For that arm to be chosen, <ins>both the pattern must match AND the if condition must evaluate to true.</ins>**

- Useful for expressing complex ideas that patterns themselves cannot express.

- <ins>Example 1:</ins>

```Rust
let num = Some(4);

match num {

    // Match on any `Some` variant. Bind the value in `Some` to the local `x` variable AND
    // check if `x < 5`. If so, then enter this match arm.
    //
    Some(x) if x < 5 => println!("less than five: {}", x),

    // Enter this arm if we match on a `Some` variant but `x >= 5`...
    Some(x) => println!("{}", x),

    // Match on a `None` variant
    None => (),
}
```
^^^<ins>NOTE:</ins> In the above example, we **can’t express that we want `x < 5` using just patterns, so match guards are here to fulfill that role.**

- <ins>Example 2:</ins> **Match guards solve issues with shadowing inside the match block**

```Rust
let x = Some(5);
let y = 10;

match x {

    // Match on any `Some` variant and bind the value in `Some` to the local `n` variable.
    // Enter this arm if `n` is equal to `y` (as defined previously with `let y = 10`).
    //
    Some(n) if n == y => println!("Matched, n = {}", n),

    _ => println!("Default case, x = {:?}", x),
}
```
^^^<ins>NOTE:</ins> In the above, we can’t use the variable `y` inside of the pattern, like `Some(y)` to check if equal, because the `y` inside of the pattern would shadow the `y` defined outside of the match block with `let y = 10;`. However, we can solve this by just using `y` inside of the match guard.

- <ins>Example 3:</ins> **You can specify multiple patterns and have the match guard apply to each pattern**

```Rust
let x = 4;
let y = false;

match x {

    // If `x` is equal to 4, 5, or 6 AND `y` is true, then enter this arm...
    //
    // This match guard (`if y`) doesn't just apply to the last pattern (`6`), it applies to
    // each pattern (`4`, `5`, and `6`).  
    //
    4 | 5 | 6 if y => println!("yes"),

    _ => println!("no"),
}
```

## `@` Operator

- The **`@` Operator** allows us to **create a variable that holds a value at the same time we are testing that value to see whether it matches a pattern**.

- <ins>Example:</ins>

```Rust
enum Message {
    Hello { id: i32} ,
}

let msg = Message::Hello { id: 5 };

match msg {

    // Match a `Hello` variant where the value in the `id` field is in the range [3, 7]. Also, bind the value
    // in the `id` field to the local `id_variable` variable.
    //
    // In essence, the `@` operator allows us to test a value (e.g., if the value is in a certain range), while also
    // saving it to a variable.
    //
    Message::Hello { id: id_variable @3..=7, } => { 
        println!("Found an id in range: {}", id_variable)
    }

    // If we don't care about saving the `id` value in a variable, then we can just use the range
    // operator without `@`
    //
    Message::Hello { id: 10..=12 } => {             
        println!("Found an id in another range")
    }

    // If we want to bind the value in the `id` field to a local `id` variable without checking if it's in a
    // certain range, then we can just use a named variable like below...
    //
    Message::Hello { id } => {
        println!("Found some other id: {}", id)
    }
```

^^^^<ins>NOTE:</ins> **Can also do this with match guard**

```Rust
let msg = Message::Hello { id: 5 };

match msg {

    // Match a `Hello` variant, and if the `id` is within the range [3, 7].
    // The `id` field's value is bound to a local `id` variable here.
    //
    Message::Hello { id } if id >= 3 && id <= 7 => {
        println!("Found an id in range: {}", id)
    }

    // Match a Hello variant, and if the `id` is within the range [10, 12].
    //
    Message::Hello { id: other_id } if other_id >= 10 && other_id <= 12 => {
        println!("Found an id in another range")
    }

    // Catch-all for any other `Hello` variant.
    // The `id` field's value is bound to a local `id` variable.
    //
    Message::Hello { id } => {
        println!("Found some other id: {}", id) 
    }
 }
```

---

# Writing Unsafe Rust

- So far, **all of the code we have written has been enforced to follow Rust’s memory safety guarantees at compile time**.

- **If we want to opt out of the memory safety guarantees, then we can use unsafe Rust**. <ins>Unsafe Rust exists for two reasons:</ins>

    1. Static analysis is conservative by nature, so **Rust will reject a valid program if it can’t guarantee that the program is memory safe, even though you as the developer knows that the program is memory safe.**

    2. The underlying computer hardware is inherently unsafe. If Rust didn’t allow you to do unsafe operations, then you couldn’t do certain tasks.

- Rust is a systems programming language so it must allow you to do low-level systems programming, which sometimes requires unsafe code. 

- **TO write unsafe Rust, use the `unsafe` keyword**, which **gives you 5 abilities that you don’t have in the safe Rust world…**

    1. **Dereference a raw pointer**

    2. **Call an unsafe function or method**

    3. **Access or modify a mutable static variable** 

    4. **Implement an unsafe trait**

    5. **Access fields of unions**

- <ins>NOTE:</ins> The **`unsafe` keyword does not turn off the borrow checker and it does not disable Rust’s safety checks.**
    - So, unsafe code isn’t necessarily dangerous but the developer has to make sure that memory inside of unsafe blocks is handled appropriately.
 
## Raw Pointers in Rust

- The compiler will ensure references are valid (i.e., no dangling references pointing to invalid data)

**Unsafe Rust has two types of raw pointers that are similar to references:**

1. **<ins>Immutable Raw Pointer</ins>** — 

```Rust
let mut num = 5;

// Create an immutable reference to `num` (`&num`), then use `as` to cast the immutable reference to an 
// immutable raw pointer (`*const i32`).
//
let r1 = &num as *const i32;    // immutable raw pointers are written as `*const` followed
				// by the type the pointer points to.
```

2. **<ins>Mutable Raw Pointer</ins>** —
	- In the context of raw pointers, immutable means that the pointer can’t be directly assigned after it has been dereferenced. 

```Rust
let mut num = 5;

// Create a mutable reference to `num` (`&mut num`), then use `as` to cast the mutable reference to a 
// mutable raw pointer (`*mut i32`).
//
let r2 = &mut num as *mut i32;	// mutable raw pointers are written as `*mut` followed
				// by the type the pointer points to. 
```
^^^
<ins>NOTE 1:</ins> In the above two examples, because we create the raw pointers from references, we know that the memory they’re pointing to is valid, but in general, we can’t make that assumption for raw pointer types. 

<ins>NOTE 2:</ins> We **don’t see** the **`unsafe` keyword** anywhere, because **Rust allows us to create raw pointers outside of an `unsafe` block**, BUT **Rust doesn’t allow us to dereference the raw pointers unless it’s in an `unsafe` block.**

### Characteristics of Raw Pointers (as compared to references / smart pointers)

- **<ins>Allowed to ignore Rust’s borrowing rules by having mutable and immutable pointers to the same location in memory, or multiple mutable pointers to the same location in memory.</ins>**

	- Bypass Rust’s borrowing rules (bc this is not allowed for regular immutable and mutable references). However, we have to be careful bc this may create a data race. 

- **Not guaranteed to point to valid memory.**  

- Allowed to be **Null**

- **Do not implement any type of automatic cleanup**

- Especially useful when interfacing with C code or building up safe abstractions that the Borrow Checker doesn’t understand.

- <ins>Example 1:</ins> **Creating a raw pointer that points to an arbitrary memory address**

```Rust
let address = 0x012345usize;
let r3 = address as *const i32;	// Create an immutable raw pointer that points to the address, there might
				// be valid memory at that address or there might not be, we have no idea.
```

- <ins>Example 3:</ins> **Dereferencing raw pointers using an `unsafe` block**

```Rust
let mut num = 5;

// Use our same raw pointers from the previous example, see explanations above.
// We have an immutable raw pointer and a mutable raw pointer pointing to the same location in memory,
// and as mentioned in the characteristics above, this is allowed for raw pointers. 
//
let r1 = &num as *const i32;    
let r2 = &mut num as *mut i32;  

// Create an `unsafe` block
unsafe {

    // Use the dereference operator `*` to dereference `r1` and `r2` and print out the values.
    //
    println!("r1 is {}", *r1);
    println!("r2 is {}", *r2);
}
```

## Calling Unsafe Functions or Methods

- **Unsafe functions and methods look the same as regular functions and methods** **except** that they **have the `unsafe` keyword at the beginning of their definition.**

```Rust
unsafe fn dangerous() {}

// `unsafe` functions and methods can only be called inside of other `unsafe` functions or `unsafe` blocks.
unsafe {
    dangerous();
}
```

- The **`unsafe` keyword in this context means** that the function has requirements that we need to uphold when calling the function. More specifically, it means that **when calling the function, we need to give it the correct arguments. If we give it the incorrect arguments, then it could lead to undefined behavior.**

- **By calling an unsafe function, you’re saying that you’ve read the function’s documentation and you’re taking responsibility for upholding the function’s contract.**

- **Unsafe functions can only be called inside of other `unsafe` functions or `unsafe` blocks.** They can be called within `unsafe` functions because the bodies of `unsafe` functions are effectively `unsafe` blocks.


## Creating a Safe Abstraction Over Unsafe Code

- Just because a function contains unsafe code, doesn’t make it an unsafe function. In fact, **you can wrap unsafe code inside of a safe function.**

- <ins>Example:</ins> **`split_at_mut()` function from the standard library**. This function **implements some unsafe code**. It is a **safe method implemented on mutable slices which will split the slice into two slices along the passed-in index.**

```Rust
let mut v = vec![1, 2, 3, 4, 5, 6];

let r = &mut v[..];

// We have the vector `v` containing `[1,2,3,4,5,6]`, we create a mutable slice of the entire vector
// called `r`, and we then call `r.split_at_mut(3)` to get `[1, 2, 3]` and `[4, 5, 6]`.
//
let (a, b) = r.split_at_mut(3);

assert_eq!(a, &mut [1, 2, 3]);
assert_eq!(b, &mut [4, 5, 6]);
```


- <ins>If we tried to implement `split_at_mut()` using only safe Rust code</ins>… **ERROR** — 

```Rust
fn split_at_mut(slice: &mut [i32], mid: usize) -> (&mut [i32], &mut [i32]) {
    let len = slice.len();

    assert!(mid <= len);

    (&mut slice[..mid], &mut slice[mid..])	// This ERRORS bc we are breaking the borrowing rules: taking
						// two mutable references to the same piece of data within
						// the same scope.
						//
						// We know this code is ok, but the Borrow Checker can't
						// understand that we're borrowing different parts of the
						// slice.
}
```

<img width="725" alt="Image" src="https://github.com/user-attachments/assets/23b1c484-6dec-4d81-a424-c735755a26cb" />

- **Implementing `split_at_mut()` correctly using `unsafe` code:**

```Rust
fn split_at_mut(slice: &mut [i32], mid: usize) -> (&mut [i32], &mut [i32]) {
    
    // Slices are a pointer to some data and the length of that data...
    let len = slice.len();
    let ptr = slice.as_mut_ptr();    // returns a mutable raw pointer (unsafe) to the slice

    assert!(mid <= len);    // By doing this check, we know the midpoint is valid, so we know the raw
			    // pointers we use in the below `unsafe` block are also valid. Therefore, this is
			    // an appropriate use of `unsafe`.

    // Create an `unsafe` block within our safe `split_at_mut()` function.
    // This allows us to wrap unsafe code inside of a safe function, such that the function can be called from 
    // safe rust code - safe abstraction around unsafe code.
    //
    unsafe {
        // Create and return a tuple of two slices after the split
        (

            // `slice::from_raw_parts_mut()` takes in a pointer to some data and a length, and creates a new 
            // mutable slice.
            //
            // `slice::from_raw_parts_mut` is unsafe because it relies on the caller to ensure the pointer 
            // and length are valid and refer to unique memory.
            //
            // `add()` is also unsafe bc it must trust that the pointer it passes back at an offset is valid.			
            //
            // ^^^ in order to use these unsafe functions, we have to create this `unsafe` block.
            //

            // The first slice starts at the original `ptr` and has `mid` elements.
            //
            slice::from_raw_parts_mut(ptr, mid),

            // The second slice starts at `ptr` offset by `mid` elements and covers the
            // remaining `len - mid` elements.
            //
            slice::from_raw_parts_mut(ptr.add(mid), len - mid),    // `ptr.add()` moves a pointer forward
								   // by the passed in offset and returns it.
        )
    }
}
```

## Functions that Call External Code

- Sometimes your Rust code may need to **interact with code in a different language**. For this purpose, Rust has the **`extern`** keyword, which **facilitates the creation and use of a foreign function interface (FFI)**.

- A **foreign function interface (FFI)** is a **way for a programming language to define a function that another language,  or a foreign language, could call.**

- **Calling a function defined within an `extern` block is always unsafe**, because we **don’t know if the language we’re calling into has the same rules and guarantees as Rust.** It’s the **developer’s responsibility to make sure that the functions defined within an `extern` block are safe to call.** 

- <ins>Example:</ins> In the below, we have an **integration with the `abs()` function from the C standard library**

```Rust
// Within an `extern` block, we specify the name and signature of the foreign function we want to call.
//  
// `"C"` defines which application binary interface (ABI), the external function uses. The ABI defines how
// to call the function at the assembly level. The `"C"` ABI is the most common ABI and follows the C
// programming language's ABI.
//
unsafe extern "C" {
    fn abs(input: i32) -> i32;
}

fn main() {
    unsafe {
        println!("Absolute value of -3 according to C: {}", abs(-3));
    }
}
```

- We can **allow other languages to call our Rust functions by using the `extern` keyword in the function signature.**

```Rust
#[unsafe(no_mangle)]	// <— This `no_mangle` annotation let’s the Rust compiler know not to mangle the
			// name of our function (`call_from_c`). Mangling is when the compiler
			// changes the name of a function to give it more information for other parts
			// of the compilation process. Here, we want to prevent that behavior so that
			// external code knows exactly what the name of our function is.
pub extern "C" fn call_from_c() {
    println!("Just called a Rust function from C!")
}
```

## Accessing or Modifying Mutable Static Variables

- **Unsafe Rust gives us the ability to access and modify mutable static variables.**

- **Global variables are supported in Rust, but can be problematic with Rust’s ownership rules**. **If two threads are accessing the same mutable global state, then it could cause a data race.**

-  **In Rust, Global variables are called <ins>static variables.</ins>**

    - Static variables are similar to constants in that the convention for naming the variable is to use all upper case and underscores for spaces

    - They have to be **type annotated**. 

    - They **must have a static lifetime** (i.e., **valid for the entire duration of the program**).

    - <ins>Example:</ins> static variable called HELLO_WORLD…

```Rust
static HELLO_WORLD: &str = "Hello, world!";	// string literals have a static lifetime, but we don’t have
						// to specify it with `&'static` because Rust can infer that

fn main() {
    println!("name is: {}", HELLO_WORLD);
}
```

- You might think that constants and immutable static variables are similar, but there is a slight difference:

    - **static variables have a fixed address in memory**, meaning that you’re always accessing the same data.
  
    - **constants are allowed to duplicate their data whenever they’re used**. For example, if you’re referencing a constant throughout your code base, then the compiler can replace all of those instances of the constant with the concrete value. 

    - **constants can't be made mutable**
  
    - **<ins>static variables can be mutable, but accessing and modifying mutable static variables is unsafe.</ins>** <ins>Example:</ins>

```Rust
static mut COUNTER: u32 = 0;	// mutable static variable called `COUNTER`, which is an
				// integer initially set to `0`.

// `add_to_count()` takes in a number and increments `COUNTER` by that number inside an `unsafe` block.
fn add_to_count(inc: u32) {
    unsafe {
        COUNTER += inc;
    }
}

fn main() {
    // The `add_to_count()` function is safe so it can be used inside `main()` without an `unsafe` block
    add_to_count(3);

    // However, we still have to create an `unsafe` block when we access `COUNTER`.
    unsafe {
        println!("COUNTER: {}", COUNTER);
    }
}
```
^^^<ins>NOTE:</ins> THIS CODE DOESN’T RUN BC OF NEWER RUST VERSION

<img width="740" alt="Image" src="https://github.com/user-attachments/assets/8295cf87-3578-489e-a028-1a60b91a5e26" />

## Implementing an Unsafe Trait

- **A trait is unsafe when at least one of its methods is unsafe.**

- We can **mark a trait as unsafe by adding the `unsafe` keyword to its definition and also to its implementation blocks** (i.e., the implementation blocks where types implement the trait, `impl State for Draft {}`).

- <ins>Example:</ins>

```Rust
unsafe trait Foo {
    //
}

unsafe impl Foo for i32 {
    //
}
```

## Accessing Fields of a Union

- A **union** is similar to a structure but only one field is used for each instance. 

- Unions are primarily used to interface with C unions.

- It’s unsafe to access fields of a union, because Rust can’t guarantee what the type of data stored in the union is for a given instance. 


## Unsafe Rust TAKEWAY

**Using `unsafe` isn’t wrong or frowned upon.** When you have a use case for `unsafe`, use it, just make sure that you’re being safe with memory. 

---

# Advanced Traits in Rust

## Associated Types 

- **Associated types** are **placeholder types defined within a trait**. **When you implement the trait, you specify the concrete type for each of these placeholders.** This **allows the trait's methods to refer to a type that's specific to each implementation.**

- **Think of associated types as "blanks" within a trait definition. When you implement a trait, you don't just provide the methods; you also "fill in the blanks" by specifying concrete types for these associated types.** This lets the trait's methods operate on types that are unique to each specific implementation.

- <ins>For example:</ins> In the below, we’ve defined the **`Iterator` trait which has one associated type named `Item`.** We then **use `Item` in the `next()` method.** **`Item` is the thing we return.** 

```Rust
pub trait Iterator {
    type Item;	// associated type

    fn next(&mut self) -> Option<Self::Item>;
}
```
^^^^Then, **when we implement our `Iterator` trait, we have to specify a concrete type for `Item`.** This way, you can **define a trait which uses some type that’s unknown until we implement the trait.** <ins>In the above example</ins>, we have a **method called `next()`** which is going to **return the next item in an iteration**; however, we **don’t know what the type of that item is until the `Iterator` trait is implemented.** 

- **If the `Iterator` trait is implemented on a vector of integers, then `Item` will be an integer.**

- **If the `Iterator` trait is implemented on a String, then `Item` will be a character**

<ins>Here is an example where `Item` is an integer:</ins>
```Rust
struct Counter {}

impl Iterator for Counter {
    type Item = u32;    // specify a concrete type for the associated type

    fn next(&mut self) -> Option<Self::Item> {
        Some(0) // this is just an example
    }
}
```

### Difference between Associated Types and Generics

Both allow us to define a type without specifying the concrete value

<ins>Difference:</ins>

- **<ins>With associated types, a single type can only implement the trait once, and this implementation fixes the specific concrete type for each associated type.</ins>**

```Rust
// `Iterator` implementation for `Counter` where `Item` is a u32.
// KEY POINT: We can't have another implementation of `Iterator` for `Counter` where `Item` is something different.
//
impl Iterator for Counter {
    type Item = u32;

    fn next(&mut self) -> Option<Self::Item> {
        Some(0) // this is just an example
    }
}
```
^^^^
<ins>NOTE:</ins> **If we tried to have another implementation where `Item` is a different type… COMPILE TIME ERROR**, so we **can’t have two implementations of `Iterator` for `Counter` where `Item` is a different type.**
￼
- **<ins>With generics, a single type can have multiple implementations of the same trait, each specialized for a different generic type parameter (e.g., u32, u16, i32, etc.)</ins>**

```Rust
pub trait Iterator<T> {
    fn next(&mut self) -> Option<T>;
}

struct Counter {}

// In the 1st implementation of `Iterator` for `Counter`, we want our generic to be a concrete type of u32.
//
impl Iterator<u32> for Counter {
    fn next(&mut self) -> Option<u32> {
        Some(0)
    }
}

// In the 2nd implementation of `Iterator` for `Counter`, we want our generic to be a concrete type of u16.
//
impl Iterator<u16> for Counter {
    fn next(&mut self) -> Option<u16> {
        Some(0)
    }
}
```
		
^^^^
<ins>TAKEAWAY:</ins> **Generics allow us to have multiple implementations of the `Iterator` trait on a single type** (`Counter` in this case) **substituting the generic for different concrete types.**

<ins>So, when deciding between **generics** and **associated types**, the question is:</ins>

- **Does it make sense to have multiple implementations of a trait for a single type?** e.g., multiple implementations of the `Iterator` trait for the `Counter` type substituting the generic for different concrete types 

- **Does it make sense to have just one implementation of a trait for the type?** e.g., one implementation of the `Iterator` trait for the `Counter` type that uses one concrete type

### When to Use Associated Types (One Trait Implementation Per Type) - IMPORTANT!!!!

- **With associated types, a single type can only implement the trait once, and this implementation fixes the specific concrete type for each associated type.**(e.g., we implement the `Iterator` trait for the `Counter` type with an associated type of u32). 

- Associated types are **best when a trait's implementation for a given type has only one logical associated type** (whether it's an input, an output, or an internal type) that is inherently tied to that specific implementation.

- <ins>Example where Associated Types are Best:</ins> **In the case of the `Iterator` trait, it makes sense to use an associated type** because if a type implements the `Iterator` trait, then its `next()` method should always return the same concrete type. **<ins>Consider the type `Vec<i32>`. When we implement `Iterator` for this type, its `next()` method should always yield an `i32`<ins>**. It **<ins>doesn't make sense for `Vec<i32>` to have multiple, distinct `Iterator` implementations where one yields i32s and another yields Strings</ins>**. Therefore, the `Item` type returned by `next()` is fixed for that particular iterator.

### When to Use Generics (Multiple Trait Implementations Per Type) - IMPORTANT!!!!

- **With generics, a single type can have multiple implementations of the same trait, each specialized for a different generic type parameter** (e.g., we implement the `Iterator` trait for the `Counter` type once with our generic being u32 and another time with our generic being u16)

- **Generics are best when a single type can logically have multiple distinct implementations of a trait, where each implementation is specialized by a type parameter** (which could be an input, an output, or another related type).

- <ins>Example where Generics are Best:</ins> Consider a hypothetical **`ConvertTo` trait that defines how one type can be converted into another**. It **uses a generic type parameter (`T`) for the type it converts into, because a single source type might logically be convertible into many different destination types.** <ins>For example</ins>, a simple **`Number` struct might be convertible into both an i32 and a f64:**

```Rust
struct Number {
    value: i32,
}

// Hypothetical trait: defines how `Self` can be converted INTO `T`
trait ConvertTo<T> {
    fn convert(self) -> T;
}

// Implements converting `Number` INTO `i32`
impl ConvertTo<i32> for Number {
    fn convert(self) -> i32 {
        self.value
    }
}

// Implements converting `Number` INTO `f64`
impl ConvertTo<f64> for Number {
    fn convert(self) -> f64 {
        self.value as f64
    }
}

fn main() {
    let num = Number { value: 10 };

    // Here, `as_int` is declared as i32, so Rust infers `ConvertTo<i32>`
    let as_int: i32 = num.convert();
    println!("As integer: {}", as_int); // Output: As integer: 10


    let num = Number { value: 25 }; 

    // Here, `as_float` is declared as f64, so Rust infers `ConvertTo<f64>`
    let as_float: f64 = num.convert();
    println!("As float: {}", as_float); // Output: As float: 25
}
```
^^^^^^
<ins>NOTE:</ins> If `ConvertTo` had used an associated type for its destination (e.g., `type Destination;`), we would only be able to provide one implementation of `ConvertTo` for Number (e.g., either converting to i32 or to f64, but not both). Using a generic `T` allows us to provide multiple, distinct `ConvertTo` implementations for the `Number` type, each specific to the type it's being converted into.

## Default Generic Type Parameters and Operator Overloading

- **Generic Type Parameters can specify a default concrete type.** This allows implementers to not have to specify a concrete type unless it’s different than the default. 

- **A great use case for this is when customizing the behavior of an operator** (a.k.a., **<ins>Operator Overloading</ins>**)

	- **Rust allows you to customize the semantics of certain operators that have associated traits in the standard library `ops` module.** One of the operators you **can overload** is the **`Add` operator**. 

- <ins>Example:</ins> We can **overload the `Add` operator for our `Point` struct by implementing the `Add` trait for `Point`**… Here, **we <ins>use the default concrete type of the generic and don’t have to change it…</ins>**

```Rust
use std::ops::Add;

#[derive(Debug, PartialEq)]
struct Point {
    x: i32,
    y: i32,
}

impl Add for Point {
    type Output = Point;    // specify a concrete type for the associated type `Output` 

    // add() takes in another point (`rhs`) and returns a new point where the `x` field is equal to
    // the sum `self.x + rhs.x` and the `y` field is equal to the sum `self.y + rhs.y`.
    //
    // This is the default function contract of the add() method when you tab in vscode. 
    //
    fn add(self, rhs: Self) -> Self::Output {
        Point {
            x: self.x + rhs.x,
            y: self.y + rhs.y,
        }
    }
}

fn main() {
    assert_eq!(
        // Add two points together with our new overloaded `Add` operator
        Point { x: 1, y: 0 } + Point { x: 2, y: 3 },
        Point { x: 3, y: 3 }
    );
}


// This is the implementation of the `Add` trait in std::ops::Add.
//
// 'Add' trait has a generic called `Rhs`, which is the type passed into the add() method for the `rhs` 
// parameter. The `Rhs` generic has a default concrete type which is `Self` (i.e., the type that's 
// implementing the `Add` trait). This makes sense because when we want to add one type to another, typically 
// they are going to be the same type (i.e., two ints, two points, etc.). 
//
// Because `Rhs` has a default concrete type, in the above, we didn't need to specify a concrete type 
// when we implemented `Add` for `Point`. Otherwise, it would be `impl Add<Point> for Point {}` 
//
trait Add<Rhs=Self> {
    type Output;

    fn add(self, rhs: Rhs) -> Self::Output;
}
```

- <ins>Example 2:</ins> In this example, we **change the default concrete type of the generic, so we have to specify this change…**

```Rust
use std::ops::Add;

struct Millimeters(u32);
struct Meters(u32);

// Implement the `Add` trait for the `Millimeters` struct.
//
// If we didn't specify that the `Rhs` generic is `Meters`, then it would default to `Self`, which
// in this case is `Millimeters`. In the `add()` method, the `rhs` parameter takes the type `Rhs`, and
// because we want the type of `rhs` to be `Meters`, not `Millimeters`, we have to specify this in 
// `impl Add<Meters> for Millimeters` to overwrite the default generic type parameter.
//
impl Add<Meters> for Millimeters {
    type Output = Millimeters;    // we still want the return type of add() to be Millimeters

    // This is the default function contract of the `add()` method when you tab in vscode after specifying
    // the trait implementation above. `Meters` is automatically filled in here bc we specify it above.
    // 
    fn add(self, rhs: Meters) -> Self::Output {
        Millimeters(self.0 + (rhs.0 * 1000))
    }
}
```

- In general, <ins>you can use default generic type parameters for two reasons:</ins>

	1. **To extend a type without breaking existing code** (if you already have a type and you want to add a generic parameter without breaking existing code, then you have a default concrete type for the generic).

	2. **To allow customization for specific cases which most users won’t need** (the `Add` trait examples above are examples of this — most of the time we will always add two of the same type, but in certain situations, like the second example above, we may want to add different types).


## Calling Methods with the Same Name

- **Rust allows you to have two traits with the same method and implement both those traits on one type.** You **can also implement a method on the type itself with the same name as the methods inside of the traits.** In this situation, you **<ins>need to tell Rust which method you’d like to call</ins>**. <ins>Example:</ins>

```Rust
struct Human;
impl Human {

    // `Human` struct implements a method called `fly()`
    //
    fn fly(&self) {
        println!("*waving arms furiously*")
    }
}

// `Pilot` trait has a method called `fly()`, and we implement the `Pilot` trait for `Human`
trait Pilot {
    fn fly(&self);
}
impl Pilot for Human {
    fn fly(&self) {
        println!("This is your captain speaking.")
    }
}

// `Wizard` trait has a method called `fly()`, and we implement the `Wizard` trait for `Human`
trait Wizard {
    fn fly(&self);
}
impl Wizard for Human {
    fn fly(&self) {
        println!("Up!")
    }
}

fn main() {
    let person = Human;

    // By default, the method that gets called is the one implemented on the struct
    // itself, not the trait methods.
    person.fly();    —> *waving arms furiously*

    // If we want to call the `fly()` method defined on the Pilot trait...
    Pilot::fly(&person);    —> This is your captain speaking.

    // If we want to call the fly() method defined on the Wizard trait...
    Wizard::fly(&person);    —> Up!
}
  ```

- This gets **more complicated when we have associated functions instead of methods.** Imagine we had two different structs/types (`Tiger` and `Lion`) that both implement their own `fly()` associated function and implement the `Wizard` trait, which has its own `fly()` associated function. In this case, `Tiger::fly()` would call the associated function implemented on the `Tiger` structure. If we wanted to call the `fly()` associated function on the `Wizard` trait implemented for `Tiger`, we would try to do **`Wizard::fly()`**. **This is the problem**. Because **`fly()` is an associated function on the `Wizard` trait, it doesn’t take `self` as a parameter** so there is **no way for Rust to know if you are calling the implementation of `Wizard` for `Tiger` or for `Lion`**. <ins>Example:</ins>

```Rust
struct Human;
impl Human {

    // `Human` struct implements an associated function called `fly()`
    //
    fn fly() {
        println!("*waving arms furiously*")
    }
}

// `Pilot` trait has an associated function called `fly()`, and we implement the `Pilot` trait for `Human`
trait Pilot {
    fn fly();
}
impl Pilot for Human {
    fn fly() {
        println!("This is your captain speaking.")
    }
}

// `Wizard` trait has a associated function called `fly()`, and we implement the `Wizard` trait for `Human`
trait Wizard {
    fn fly();
}
impl Wizard for Human {
    fn fly() {
        println!("Up!")
    }
}

fn main() {
    Human::fly();    // By default, this calls the associated function `fly()` implemented on the `Human` 
                     // struct, not the ones implemented on the traits that `Human` implements. 

    // If we want to call the `fly()` associated function defined on the `Wizard` trait...
    <Human as Wizard>::fly();    // we have to use fully qualified syntax. This tells Rust that we want 
                                 // to call the `fly()` associated function on the `Wizard` trait as
				 // implemented for `Human`
}
```

## Supertraits

- You might have a **trait that’s dependent on functionality from another trait**. In this case, your **<ins>trait is dependent on the other trait being implemented</ins>**. The trait you rely on is called a **supertrait**. 

```Rust
use std::fmt;

trait OutlinePrint: fmt::Display {
    fn outline_print(&self) {
        let output = self.to_string();    // The `outline_print()` method in the `OutlinePrint` trait requires that
					  // `self` implements `to_string()`, which is defined in the `Display` trait.
					  //
					  // THUS, any type that implements the `OutlinePrint` trait must also
					  // implement the `Display` trait.
					  //
					  // To encode this, specify `OutlinePrint: fmt::Display` above.
					  //
					  // Because we have specified that our `OutlinePrint` trait depends on the
					  // `Display` trait, the `to_string()` method doesn't error here.
					  //
					  // If we try to implement `OutlinePrint` trait on a type that doesn't
					  // implement the `Display` trait, then we get an ERROR (like the below)

        let len = output.len();
        // etc...
    }
}
```

<img width="462" height="63" alt="Image" src="https://github.com/user-attachments/assets/53ae5e22-4f7f-4c3b-af55-0e3ac3b0cc9d" />

## Newtype Pattern

- **<ins>Orphan Rule:</ins>** We **can implement a trait on a given type if either the trait or the type is defined within our crate.**

- If you want **to implement a trait on a type where both the trait and the type are defined outside of our crate, then we can <ins>use the Newtype Pattern</ins>…**

	- We **do this by creating a tuple struct with one field, this field is going to be the type we are wrapping.**

	- **This thin wrapper around our type is local to our crate, so we can implement any trait we’d like for it.**

- <ins>Example:</ins> We want to **implement the `Display` trait on a `Vector` type**, but the **`Display` trait and the `Vector` type are both defined outside of our crate (breaks Orphan Rule)**

```Rust
use std::fmt;

// To get around the Orphan Rule, we create a new tuple struct called `Wrapper` which
// stores a `Vector` (this wrapper is the newtype).
//
struct Wrapper(Vec<String>);

// `Wrapper` is defined within our crate, so we can implement the `Display` trait for `Wrapper`.
//
impl fmt::Display for Wrapper {
    fn fmt(&self, f: &mut fmt::Formatter<'_>) -> fmt::Result {
        write!(f, "[{}]", self.0.join(", "))    // Inside the trait implementation, we can access the `Vector`
						// (i.e., the wrapped value in the newtype) by calling `self.0` since `Wrapper`
						//  is a tuple struct.
    }
}

fn main() {
    let w = Wrapper(
        vec![String::from("hello"), String::from("World")]
    );
    println!("w = {}", w);
}
```

^^^<ins>NOTE:</ins> The **downside** of this pattern is that **`Wrapper` is a newtype, so we can't call methods defined on the `Vector` type directly on `Wrapper`.**

- However, **if we did want our newtype to implement every method on the type it's holding, then we can implement the `Deref` trait such that dereferencing `Wrapper` would return the inner value.**

- However, **if we only want our newtype to have a subset of methods defined on the inner type, then we would have to implement each of those methods manually.**

<br>We can also **use the newtype pattern to increase type safety…**

- Imagine you had two functions, one function takes an age (u32) as a parameter, and the other function takes in an employee id (u32) as a parameter. So, **both take u32**. 

- If you want to **prevent the user from passing in the employee id instead of the age (or vice versa) to a function**, then you can **create a newtype which wraps a u32...**

```Rust
// Create tuple structs for `Age` and `ID`
struct Age(u32);
struct ID(u32);

// Now, instead of passing raw integers to functions that use `Age` or `ID`, we pass one of these structs.
```

<br>The **newtype pattern is also useful to abstract away implementation details**. In general, the newtype pattern is a **lightweight way to achieve encapsulation**. 

- <ins>Example:</ins> we **create a `People` type which wraps a hashmap of integers pointing to strings**. **Code using the `People` type will only be exposed to the public API of the `People` type and have no knowledge of the internal data structures being used.**

---

# Advanced Types in Rust

## Type Aliases 

- Rust allows you to create **<ins>type aliases</ins>** to **give existing types new names.**

- <ins>Example:</ins>

```Rust		
// Create the type alias `Kilometers` for i32
//
type Kilometers = i32;

let x: i32 = 5;
let y: Kilometers = 5;

println!("x + y = {}", x + y);    // `Kilometers` is not a new type, it is a synonym for an i32, so it is treated just
				  // like an i32. Here, for example, we can add an i32 and a `Kilometer` type bc they
				  // are technically the same type.
```

<br>**<ins>The main use case of type aliases is to reduce repetition.</ins>**

- <ins>Example:</ins> Here **we have a really long type that we don’t want to keep having to write out over and over again…**

```Rust
let f: Box<dyn Fn() + Send + 'static> = Box::new(|| println!("hi"));

fn takes_long_type(f: Box<dyn Fn() + Send + 'static>) {
    //
}

fn returns_long_type() -> Box<dyn Fn() + Send + 'static> {
    //
 }
```

^^^^<ins>We can make this code much more concise and reasable with type aliases:</ins>

```Rust

type Thunk = Box<dyn Fn() + Send + 'static>;

let f: Thunk = Box::new(|| println!("hi"));

fn takes_long_type(f: Thunk) {
    //
}

fn returns_long_type() -> Thunk {
    //
}
```

^^^^**Type aliases can also convey meaning**. In the above, “Thunk” is a word for code that will be evaluated at some later point in time. This is an appropriate name for a closure that gets stored.

## Never Type

- The **<ins>Never type</ins>** is a special type **denoted with an `!`**. 

- <ins>Example:</ins> **When used as the return type for a function, the <ins>Never type</ins> means that the function will never return.**

```Rust
fn bar() -> ! {
    // 
}
```

<br><ins>Why the Never type is useful: </ins>

```Rust
// When we built our guessing game, we had code which parsed user input into an integer. The code was 
// something like the below... `guess` contains the string of user input
//
while game_in_progress {

    // Notice that `guess` is type annotated as u32. However, the `Err` arm doesn't return a u32; instead, it 
    // uses `continue`. This works because `continue` has a Never type.
    //
    // Rust will look at both arms of the `match` expression, the first arm returns a u32 and the second arm 
    // returns a  Never type, so it can never return. Thus, Rust concludes that the return type of the `match`
    // expression is a u32. 
    //
    // We are allowed to write this code because if we get into the `Err` arm, `continue` will not return 
    // anything; instead, it will move control back to the top of the loop, meaning that `guess` will never 
    // be assigned (to something that is not u32). Thus, the only type `guess` will be assigned is u32 from 
    // the first arm. 
    //
    let guess: u32 = match guess.trim().parse() {
        Ok(num) => num,
        Err(_) => continue,
    };
}
```

<br>**The <ins>Never type</ins> is also useful with the `panic!` macro.**

```Rust
impl<T> Option<T> {
    pub fn unwrap(self) -> T {
        match self {

            // If `self` is a `Some` variant, return the value contained in `Some` 
            Some(val) => val, 

            // If `self` is a `None` variant, `panic!`
            // `panic!` returns a never type, so if we get in the `None` arm, then we won't be returning from 
            // `unwrap()`; instead we will exit the program. So, the return value of `unwrap()` is still `T`
	    // bc the first arm returns type `T` and the second arm will never return.
            //
            None => panic!(
                "called `Option::unwrap()` on a `None` value"
            ),
        }
    }
}
```

<br>**A loop has the <ins>Never type</ins>**

```Rust
print!("forever ");

// This loop never ends, so the value of the expression is the Never type.
// However, it wouldn't have the Never type if we added `break`
loop {
    print!("and ever ");
}
```

## Dynamically Sized Types and the `Sized` Trait

- **<ins>Dynamically Sized Types</ins> (DSTs, unsigned types)** are **types whose size we can only know at runtime.**

- <ins>Example of a dynamically sized type:<ins> The **`str`** type

```Rust
// Because Rust can't determine the size of these `str` types at compile time, if we
// try to write this code, we get a bunch of ERRORS (one is screenshotted below). 
//
let s1: str = "Hello there!";
let s2: str = "How's it going?";
```

<img width="658" height="104" alt="Image" src="https://github.com/user-attachments/assets/996d62e5-ebb7-46d3-b779-26c8298b4683" />

^^^^ TO FIX this error, **instead of using **`str`** directly, we have to use the borrowed version of `str` — `&str`**. This **string slice structure (`&str`) stores two values:**

1. **An address pointing to the location of the string in memory**

2. **The length of the string**

^^^**BOTH** **the address value and the length of the string have a type of `usize`, meaning that we know their size at compile time**, which is why the error is fixed by using `&str`. 

- In general, the above example is how dynamically sized types are used in Rust. They have an extra bit of metadata which stores the size of the dynamic information.

<br>**IMPORTANT:** **<ins>The golden rule for dynamically sized types is that we must always put them behind some sort of pointer.</ins>**

- In the above example, the `str` type is behind a reference (`&str`), but we can also put it behind a `Box` smart pointer or an `Rc` smart pointer. 

**<ins>Trait objects are also dynamically sized types</ins>** — trait objects **have to be behind some sort of pointer (e.g., `Box`)**.

### `Sized` Trait

**Rust has a special trait called the `Sized` trait to determine whether a type’s size can be known at compile time or not.**

- The `Sized` trait is **automatically implemented for every type whose size is known at compile time.**

- **Rust implicitly adds the `Sized` trait bound to every generic function**… 

```Rust
// This function takes a generic, and Rust will automatically add the `Sized` trait bound like so...
//
fn generic<T: Sized>(t: T) {
    //
}
```

^^^^So, **by default, generic functions will only work on types whose size is known at compile time.** To **relax this restriction**, you can use a **special syntax…**

```Rust
fn generic<T: ?Sized>(t: &T) {
    //
}
```

^^^^
Here, we’re saying **“T may be sized or not”**. <ins>NOTE</ins>: **This special syntax (`?`) is ONLY available for the `Sized` trait**. **After adding the `?`, type `T` can now potentially be a dynamically sized type, so we have to put it behind some sort of pointer (we chose a reference).**

---

# Advanced Functions and Closures

## Function Pointers

- Not only can you pass closures to functions, but **you can also pass functions to functions.**

- This is **useful when you want to pass in a function you’ve already defined instead of creating a new closure.** 

- **To pass in a function as an argument to another function**, use a **<ins>function pointer</ins>**, which is **specified with `fn`**. 

<img width="729" height="184" alt="Image" src="https://github.com/user-attachments/assets/2885b63c-0af5-4b59-82c7-3da2a0e271e2" />

- <ins>Example:</ins>

```Rust
fn add_one(x: i32) -> i32 {
    x + 1
}

// do_twice() takes in a parameter `f` which is a function pointer with the signature `fn(i32) -> i32`. This 
// means that the function `f` points to accepts an integer and returns an integer. 
//
fn do_twice(f: fn(i32) -> i32, arg: i32) -> i32 {

    f(arg) + f(arg)    // Function pointers are pointers that point to code, not data. 
                       // They can be called just like functions, so we call `f` here two times passing in the 
                       // `arg` parameter (which is an i32).
}

fn main() {
    let answer = do_twice(add_one, 5);    // We pass the `add_one()` function into `do_twice()` for the `f`
					  // parameter (function pointer). In this case, then, when we call
					  // `f(arg)` in do_twice(), we are calling `add_one(arg)`.

    println!("The answer is: {}", answer);
}
```

- One **case where you may only want to accept function pointers** **(instead of function pointers and closures)** is if you’re **interfacing with external code that does not support closures.** For example, C functions can accept functions as arguments, but the C programming does not support closures. 

- <ins>Example 2:</ins> **Closure OR Function Pointer in `.map()`**

```Rust
let list_of_numbers = vec![1, 2, 3];

// Convert vector of ints into vector of strings by creating an iterator over the vector, using `map` to call 
// `to_string()` on each element in the iterator, and then using `collect()` to transform the iterator into a
// collection (vector of strings). 
// 
let list_of_strings: Vec<String> = 
    list_of_numbers 
        .iter()
        .map(|i| i.to_string())    // `map()` takes in a closure OR a function pointer that's called
				   // on each element in the iterator. HERE, we use a closure !!!
        .collect();

println!("{:?}", list_of_strings);
```

^^^^^^
<ins>NOW, **the below uses a function pointer INSTEAD of a closure**…</ins>

```Rust
let list_of_numbers = vec![1, 2, 3];

let list_of_strings: Vec<String> = 
    list_of_numbers 
        .iter()
        .map(ToString::to_string)    // Pass in a function pointer INSTEAD of a closure
        .collect();

println!("{:?}", list_of_strings);
```

^^^^^
<ins>We can also **define our own function and pass that function in as a function pointer** in `map`…</ins>

```Rust
fn kirins_function(num: &i32) -> String {
    num.to_string()
}

fn main() {
    let list_of_numbers = vec![1, 2, 3];

    let list_of_strings: Vec<String> = 
        list_of_numbers 
            .iter()
            .map(kirins_function)    // Pass in a function pointer that points to the
				     // function we created
            .collect();

    println!("{:?}", list_of_strings);
}
```

<br><ins>Example 3:</ins> Useful pattern that exploits an implementation detail of tuple structs and tuple struct enum variants. 

```Rust
enum Status {
    Value(u32),    // Tuple structs use parenthesis () to initialize values contained inside the tuple struct,
		   // this looks like a function call. In fact, these initializers are implemented as functions
		   // that take in arguments and return an instance of the tuple struct.
		   //
		   // This means that we can use the initializers as function pointers, see below...
    Stop
}

// `(0u32..20)` represents a range of numbers. Specifically, `(0u32..20)` creates an iterator that yields numbers 
// from 0 up to (but not including) 20, as u32 type.
//
// The below code creates a Vector of `Status` enums by calling `map` on the range passing in the `Value` 
// variant to `map`. `map()` will treat `Value` like a function pointer, where the argument is a u32 and the return 
// value is a Value variant. As a result, `map()` will call `Status::Value` on each integer in the range `(0u32..20)`
// and then use `collect()` to convert the iterator returned from `map()` into a collection (Vector of `Status` 
// enums).
//
let list_of_statuses: Vec<Status> =
    (0u32..20).map(Status::Value).collect();
```

## Returning Closures from Functions

- **<ins>Closures are represented using traits</ins>**, so we **<ins>can’t return a concrete type from a function that returns a closure.</ins>**

- <ins>Example:</ins> To return a closure, we **can use the `impl {TRAIT}` syntax**…

```Rust
// `returns_closure()` has a return type of `impl Fn(i32) -> i32`
// This means that `returns_closure()` returns something that implements the `Fn` trait taking in an integer and 
// returning an integer.
//
fn returns_closure() -> impl Fn(i32) -> i32 {

    |x| x + 1   // IMPORTANT: `returns_closure()` always returns the same closure.

}
```

^^^^**<ins>NOTE: This syntax will not work in all situations:</ins>**

- <ins>For example</ins>, suppose `returns_closure()` takes in an argument `a` which is an integer, and we want to return a closure based on the value of `a`…

```Rust
fn returns_closure(a: i32) -> impl Fn(i32) -> i32 {

    // If `a > 0`, then return a closure that takes in an argument `b` (i32) and returns `a + b`. 
    if a > 0 {
        move |b| a + b

    // If `a <= 0`, then return a closure that takes in an argument `b` (i32) and returns `a - b`.
    } else {
        move |b| a - b
    }
}
```

^^^^<ins>**THIS code ERRORS…**</ins> **“No two closures, even if identical, have the same type.** **<ins>Consider boxing your closure and/or using it as a trait object.</ins>**”

<img width="743" height="286" alt="Image" src="https://github.com/user-attachments/assets/febdc39a-4674-41d3-aa24-397c3c4ec580" />

^^^^ As this error states, **each closure is a unique type**, **even if identical to another closure.**

- In the above example, **our two closures returned in `returns_closure()`** (`move |b| a + b` and `move |b| a - b`) **are different types**, but the **`impl {TRAIT}` syntax only works if we’re returning ONE TYPE.**

- In our example, **we’re returning one of two types** **(the type of `move |b| a + b` or the type of `move |b| a - b`)** **depending on the value of `a`.**

- As a result, **instead of using the `impl {TRAIT}` syntax, we <ins>must return a trait object…</ins>**

```Rust
// As we have discussed, trait objects are dynamically sized types, so trait objects
// have to be behind some sort of pointer (in this case, we use `Box`).
//
// “Return any type that implements this trait”
//
// Trait = `Fn` trait taking in an integer and returning an integer.
//
fn returns_closure(a: i32) -> Box<dyn Fn(i32) -> i32> {
    if a > 0 {
        Box::new(move |b| a + b)
    } else {
        Box::new(move |b| a - b)
    }
}
```

---

# Macros in Rust

- **Macros** allow you to write code which writes other code, known as meta programming.

- You can **think of macros like a function, where the input is code and the output is also code that is transformed in some way.**

- <ins>Examples of macros in Rust:</ins>

    - **`println!`** macro

    - **`vec!`** macro

^^^**Both of these macros expand to produce more code than the code you’ve written manually.**

- As a result, **writing macros allows you to reduce the amount of code you have to write and maintain**, which is similar to the role of functions. 

## Macros vs. Functions
- **Functions** must declare the number of parameters they can accept
- **Macros** **can accept a variable number of parameters**

- **Functions** are called at runtime
- **Macros** are **expanded before your program finishes compiling**

- **Macros** are a lot more powerful than functions; however, the downside is that **using macros introduces more complexity because you’re writing code that writes other code. As a result, macros are harder to read, understand, and maintain.**

## Declarative Macros

- **<ins>Declarative macros</ins>** are the most widely used form of macros in Rust.

- **Allow you to write something similar to a match expression** — they **<ins>match against patterns and replace code with other code.</ins>**

- <ins>Example:</ins> the **`vec!` macro is a declarative macro…**

    - **When using `vec!`** (the vec macro), we **specify `vec!` followed by square brackets `[]` containing the values we want in our vector.**

        - we **can pass in different types** when calling the `vec!` macro (e.g., ints, string slices).

        - we **can pass in a variable number of arguments** when calling the `vec!` macro (e.g., 3, 5)

```Rust
// Pass in 3 arguments that are integers.
let v1: Vec<u32> = vec![1, 2, 3];   

// Pass in 5 arguments that are string slices.
let v2: Vec<&str> = vec!["a", "b", "c", "d", "e"];
```
^^^**<ins>main.rs</ins>** — the entry point for our binary crate.

**<ins>How the `vec!` macro is implemented…</ins>** this is a simplified version of the `vec!` macro from the standard library.

**<ins>lib.rs</ins>** — the entry point for our library crate

```Rust
#[macro_export]    // this annotation means that whenever the crate in which this macro is defined in is
		   // brought into scope, this macro should be made available.

macro_rules! vec {	// define the declarative macro by starting off with `macro_rules!` followed by the
			// name of the macro, in this case `vec` (the exclamation point in `vec!` is not included in
			// the name). In the curly brackets, we put the body of the macro.

    // The body of the macro is similar to a `match` expression. In this case, a `match` expression with one 
    // arm.
    ( $( $x:expr ),* ) => {	// `( $( $x:expr ),* )` is the pattern to match on and in the brackets is the
				// code block associated with that pattern. If the inputs to the macro match
				// this pattern, then the code in the brackets will be emitted, otherwise an
				// error will be thrown bc we only have one arm (NOTE that macros could have
				// multiple arms).
				//
				// The pattern syntax used in macros is different than the pattern syntax used
				// in `match` expressions bc we're matching against actual code versus values.
				//
				// - The outer two parenthesis `()` encompass the entire pattern.
				// - Next, `$( PATTERN )` captures any values that match the pattern
				//   inside,  for use in the replacement code (i.e., the code block in the
				//    brackets)
				// - The interior pattern inside `$()` is `$x:expr`, which matches any Rust
				//    expression and assigns it to the variable `$x`.
				// - After `$( PATTERN )` is a comma `,` which means that a literal comma
				//    could appear after the code which matches `$x:expr`.
				// - The `*` means that the pattern can match 0 or more times.
				//
				// Example: Imagine we called the `vec!` macro with `[1, 2, 3]` as the input. The
				// pattern will match 3 times, once for every expression in the code we pass
				// in: it will first match `1` which is an expression that is assigned to `$x`, then
				// `2` which is assigned to `$x`, and then `3` which is assigned to `$x`….
		
        // The following code is then generated….
        {
            let mut temp_vec = Vec::new();    // First, a new vector is created.

	    // The code in `$( temp_vec.push($x); )*` says that we generate the line of code 
            // `temp_vec.push($x);` for every match that we get in the `$( PATTERN )`.
            //
            // The first match we get is a match against `1`, so `1` is assigned to `$x`  and then 
            // `temp_vec.push($x);` is emitted with `$x` being replaced with `1`.
            //
            // This is then repeated with `temp_vec.push($x);` being generated two more times for `$x` 
            // being equal to `2` and `3`. 
            //
            // So we can essentially replace `$( temp_vec.push($x); )*` with `temp_vec.push(1)` then 
            // `temp_vec.push(2)` and then `temp_vec.push(3)`.
            //
            $(
                temp_vec.push($x);
            )*

            temp_vec
        }
    };
}
```

## Procedural Macros

- **<ins>Procedural macros</ins> are like functions**: they **<ins>take code as input, operate on that code, and produce code as output.</ins>**

- This is **in contrast with declarative macros**, which match against patterns and replace code with other code. 

- <ins>There are 3 kinds of procedural macros:</ins> (they all work in a similar fashion)
    1. Custom Derive
    2. Attribute-like
    3. Function-like

- **Procedural macros must be defined in their own crate with a custom crate type.** The three kinds of procedural macros are all defined using a similar syntax: 

```Rust
use proc_macro;    // bring the `proc_macro` crate into scope, which defines `TokenStream`

// Define the procedural macro by defining a function where the name of the function is the name of our
// procedural macro, and the input is a `TokenStream`, which is the code we're operating on, and the output 
// is a `TokenStream`, which is the code we're producing.
//
// Tokens are the smallest individual elements of a program. They can represent keywords, identifiers, 
// operators, separators, or literals.
//
// The function must also have an attribute which specifies the kind of procedural macro that we're 
// creating. 
//
#[some_attribute]
pub fn some_name(input: TokenStream) -> TokenStream {
    //...
}
```

### Creating our own Custom Derive Macro

The custom derive macro we create is called `hello_macro()` and it will implement a trait called `HelloMacro`, which will have an associated function with a default implementation that prints out “hello macro”.

**<ins>main.rs</ins>** — code using our macro

```Rust
// Bring the macro into scope
use hello_macro::HelloMacro;
use hello_macro_derive::HelloMacro;

// Define a struct called `Pancakes` and have a `derive` attribute specifying our macro. 
// What this `derive` attribute does is implement our `HelloMacro` trait for the `Pancakes` struct.
#[derive(HelloMacro)]
struct Pancakes;

fn main() {
    // Bc the `derive` attribute above implements our `HelloMacro` trait for the `Pancakes` struct,
    // we can now call `hello_macro()` from the `Pancakes` struct.
    Pancakes::hello_macro();
}
```

**<ins>Implementing `HelloMacro`</ins>** — the procedural macro

1. Create a new library crate called “hello_macro”

**`cargo new hello_macro --lib`**
<img width="211" height="167" alt="Image" src="https://github.com/user-attachments/assets/e849c3c5-4dc3-46c4-9ae6-9681736ef20b" />

2. Define the `HelloMacro` trait in **lib.rs**

```Rust
pub trait HelloMacro {
    fn hello_macro();    // our macro has one associated function named `hello_macro()`
}
// We want to have a default implementation for `hello_macro()` that prints “hello macro” followed by the type 
// on which the trait is implemented on. However, Rust doesn’t have reflective capabilities, so we can’t look up 
// the name of the type at runtime here in a default implementation. Thus, we have to use our procedural 
// macro to generate the default implementation. 
```

3. Now that we have our trait defined, we need to define our procedural macro. As explained, **procedural macros have to be defined in their own crate. SO, we create a new library crate inside of the “hello_macro” crate…**

**`cargo new hello_macro_derive --lib`**

<img width="209" height="188" alt="Image" src="https://github.com/user-attachments/assets/0d9b3021-6880-4811-b902-18de0b769599" />

<ins>NOTE:</ins> There is a **naming convention when structuring crates and macro crates.** If you have a **custom derive macro**, then you’ll **name the crate whatever the crate’s name is (e.g., “hello_macro”) and append “_derive”. So, in this case, we get “hello_macro_derive”.**

<ins>NOTE:</ins> **Because the “hello_macro” crate and the “hello_macro_derive” crate are tightly coupled, we create the macro crate inside of the library crate.** Each crate still has to be published separately, and **code using the crates has to bring each crate into scope. THIS IS WHY there are two `use` statements in main.rs shown earlier.** 

4. Open **“cargo.toml”** file in the newly created “hello_macro_derive” crate. **Macro crates are a special type of crate**, so **to signify this**, we **add `proc-macro = true` in the “cargo.toml” file under the `[lib]` section**. We also **add the `syn` and `quote` crates as dependencies.**

```Rust
[package]
name = "hello_macro_derive"
version = "0.1.0"
edition = "2018”

[lib]
proc-macro = true

[dependencies]
syn = "1.0"
quote = "1.0"
```

5. **Implement our macro in the lib.rs file of the “hello_macro_derive” crate.**

```Rust
extern crate proc_macro;    // `proc_macro` is a crate that comes with Rust, so don't have to declare it in
			    // dependencies section. However, to import, we have to write `extern crate`.
			    // The `proc_macro` crate allows us to read and manipulate Rust code.

use proc_macro::TokenStream;	// `TokenStream` is the type of the code we're operating on and the code we're producing
use syn;	// allows us to take a string of Rust code and turn it into a syntax tree data structure, which
		// we can operate on.

use quote::quote;    // can take the syntax tree data structure and turn it back into Rust code.

// Define our custom derive macro called `HelloMacro`
#[proc_macro_derive(HelloMacro)]    // annotated with `proc_macro_derive` to indicate that this
				    // a custom derive macro with the name `HelloMacro`

pub fn hello_macro_derive(input: TokenStream) -> TokenStream {
	
    // Use the `syn` crate to parse the `input` `TokenStream` (the Rust code we're operating on) into a  
    // syntax tree that we can manipulate.
    // Use `unwrap()` so that the function panics if parsing fails. Appropriate bc not returning a `Result` type and  
    // this function is called at compile time not runtime.
    //
    let ast = syn::parse(input).unwrap();

    // Pass the syntax tree into `impl_hello_macro()` to build the trait implementation
    impl_hello_macro(&ast)
}

fn impl_hello_macro(ast: &syn::DeriveInput) -> TokenStream {
    let name = &ast.ident;    // Extract out the name of the type we're working on

    // Use the `quote!` macro to output some Rust code. In this case, we implement the `HelloMacro` trait  
    // on our type. The `quote!` macro has templating abilities so this pound `#name` will be replaced by the 
    // `name` variable containing our type. Then, we provide a custom implementation of the `hello_macro` 
    // associated function, which, in this case, prints a message containing the name of the type we're 
    // working on.
    //
    let gen = quote! {
        impl HelloMacro for #name {
            fn hello_macro() {
                println!(
                    "Hello, Macro! My name is {}!",
                    stringify!(#name)    // `stringify!` macro takes an expression and turns it into a
					 // string without evaluating the expression like the `format!`
					 // macro would.
                );
            }
        }
    };
    gen.into()    // Take the output of the `quote!` macro which is saved in a variable called `gen`, and turn
		  // it  into a `TokenStream` using the `.into()` method.
}
```

5. **Build the “hello_macro_derive” crate — `cargo build`** in this directory

6. **Build the “hello_macro” crate — `cargo build`** in this directory

7. **Go back to the project with main.rs that uses our macro. Add the “hello_macro” crate and “hello_macro_derive” crate as dependencies in cargo.toml**…

```Rust
[package]
name = "procedural_macros"
version = "0.1.0"
edition = "2018"

[dependencies]
hello_macro = { path = "../hello_macro" }
hello_macro_derive = { path = "../hello_macro/hello_macro_derive" }
```

8. **We can now run main.rs …**

```Rust
// Bring the macro into scope
use hello_macro::HelloMacro;
use hello_macro_derive::HelloMacro;

// Define a struct called `Pancakes` and have a `derive` attribute specifying our macro. 
// What this `derive` attribute does is implement our `HelloMacro` trait for the `Pancakes` struct.
#[derive(HelloMacro)]
struct Pancakes;

fn main() {
    // Bc the `derive` attribute above implements our `HelloMacro` trait for the `Pancakes` struct,
    // we can now call `hello_macro()` from the `Pancakes` struct.
    Pancakes::hello_macro();
}
```
**`cargo run` —>** 
<img width="647" height="92" alt="Image" src="https://github.com/user-attachments/assets/d1f7b93b-ef62-4e4e-af89-819327119667" />

^^^^The associated function works as we want: it prints the message with the name of the type that the trait is implemented on.

### Attribute-like Macros

- Similar to custom derive macros, except instead of generating code for the derive attribute, we can create a custom attribute. 

- **Custom derive macros only work on structs and enums, whereas attribute-like macros work on other types such as functions.**

- <ins>Example:</ins>

```Rust
// Imagine you are building a new web framework and you want to create a new attribute
// called `route()` which takes in an HTTP method and a route. This macro will generate code
// which will map a specific HTTP request to a given function. In this case, we're mapping
// a GET request on the root path to the index function. 
#[route(Get, "/")]
fn index() {
    //...
}

// We define our attribute-like macro by specifying a function annotated with `#[proc_macro_attribute]`.
// Our function would take in two arguments. The first argument, `attr` contains the contents of the
// attribute, which in this case is the HTTP method and the path. The second argument is going to contain
// the contents of the item the attribute is attached to, in this case the `index()` function. 
//
// Other than this, attribute-like macros work just like custom derive macros.
//
#[proc_macro_attribute]
pub fn route(
    attr: TokenStream, // GET, "/"
    item: TokenStream  // fn index() {}
) -> TokenStream {
    //...
}
```

### Function-like Macros:

- **Look like function calls however they are more flexible.**

- They **can take a variable number of arguments, and they operate on Rust code.**

- <ins>Example:</ins> We **want to generate a function-like macro called `sql` that takes a SQL statement as an argument, validates that the SQL statement has the correct syntax, and then generates code that will allow you to execute the SQL statement.**

```Rust
let sql = sql!(SELECT * FROM POSTS WHERE id=1);

// The definition for a function-like macro is extremely similar to our custom derive macro, with the only 
// difference being that we annotate the function with `#[proc_macro]` instead of  `#[proc_macro_derive]`
#[proc_macro]
pub fn sql(input: TokenStream) -> TokenStream {
    //...
}
```


























