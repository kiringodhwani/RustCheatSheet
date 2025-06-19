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

## Ownership -- 3 Rules in Rust
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

## Rules of References

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

### Enum Methods
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

### If let syntax

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

## Use keyword

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

## Re-Exporting
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

- <ins>Example 2:</ins> Nested Paths
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

### Glob Operator (*)
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

## Result Enum

- **For errors that are recoverable, we have the Result enum**… similar to the Option enum.

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

### Useful Functions on the Result Enum

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

## Error Propagation

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

## The `?` Operator

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

## Tests that Return a Result Type — 
- **Tests that return a Result type allow you to use the ? operator**, which can be **convenient if you have multiple operations within the test that could return an error type and <ins>you want the test to fail if any of those return an error type.</ins>**
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

### Why Tests that Return Result Are Useful...

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

1. **<ins>Capture by Immutable Borrow (&T):</ins>** **Variable is not modified inside the closure.** In the below, the variable **`word` is not modified inside the closure `print_str`**. **As the variable is immutable by default, we can make any number of immutable references of `word` inside the closure.** Notice that the closure variable print_str is also immutable.

	- **<ins>When a closure captures a variable by immutable borrow</ins>** (which **happens when the variable is only read inside the closure**, as word is in `println!("word = {}", word)`), **<ins>the closure essentially takes an immutable reference to that variable.</ins>** The core rule is that **you can have any number of _immutable references_ to a piece of data simultaneously.** Because the closure `print_str` only holds an immutable borrow of `word`, and `println!("length of word = {}", word.len());` also takes an immutable borrow of `word`, these operations can coexist.

 	- **Encoded in the `Fn` function trait** — `Fn` immutably borrows values**

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

2. **<ins>Capture by Mutable Borrow (&mut T):</ins>** **Variable is modified inside the closure.** In the below example, the variable **`word` is modified inside the closure `print_str` with `word.push_str("World!");`**. Thus, we **have to make the variable `word` mutable as well as the closure variable `print_str`**. This means **<ins>no other references of the `word` variable can exist unless the closure is used</ins>, since the closure takes a mutable reference to the piece of data.**
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

    - **`FnMut`** **requires &mut self on the closure itself.**

    - Because the **closure in the above example captures `word` by mutable reference**, its **type automatically becomes `FnMut`.**

    - A **closure** of type **`FnMut`** **has a `fn call_mut(&mut self)` method (or similar) that takes `&mut self`**. This means that **whenever you call `print_str()`**, you are effectively **calling a method on the `print_str` variable that requires `print_str` itself to be mutable.**

    - **<ins>BEST ANALOGY:</ins>** **Think of `print_str` as a struct that internally holds a `&mut String` to `word`.** **When you call `print_str()`**, you're essentially saying **"I want to use the mutable reference stored within `print_str`." To allow that usage, print_str itself must also be mutable.**
 
  3. **<ins>Capture by Move (i.e., Capture by value, Taking Ownership) (T):</ins>** **Variable is moved inside closure.** Here, we move the value in the `word` variable to a new variable `new_word` inside the closure. As the variable is moved, we cannot use it anywhere else except for inside the closure.

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

**When you create a closure, Rust infers which of the traits to use (FnOnce, FnMut, Fn) based on how you use the values in inside the closure’s environment.** 

- You can **force the closure to take ownership of the values it uses inside its environment by using the `move` keyword in front of the closure.** Mostly **useful when you’re passing a closure from one thread to another thread** so you can also pass the ownership of the variables from one thread to the other thread. Ex:

```Rust
fn main() {
    let x = vec![1,2,3];

    // Inside this closure, we just evaluate z == x, so we don't take ownership of x inside our closure.
    // However, we can force the closure to take ownership of x by specifying "move".
    //
    let equal_to_x = move |z| z == x;

    println!("can't use x here {:?}", x);	// this errors (red squiggly under x) bc the closure now takes
    						// ownership of x so we can't use x after it’s been moved.
```

NOTE: **Because closures capture their environment, they have to use extra memory to store that context**. Functions, on the other hand, don’t capture their environment, so they don’t incur the same overhead. 

## Closure Type Inference







