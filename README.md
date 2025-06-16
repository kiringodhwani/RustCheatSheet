# Cargo
**cargo** = build system, package manager, important for managing dependencies (this is a pain point with other low-level programming languages so it is really nice that rust has it built in).

- **TO compile a project, installs dependencies and necessary things for the dependency:** `cargo build`. When you add dependencies, like in the below example, you have to run `cargo build`...

    [package]
    name = "guessing_game"
    version = "0.1.0"
    edition = "2024"

    [dependencies]
    rand = "0.5.5"  // added this dependency

- **TO make new project**: cargo new {project_name}

- **TO check code for errors without producing an executable:** cargo check

- **TO compile (if necessary) and run project:** cargo run

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

	let s = "hello";  // `s` is valid from this point forward.
			  // `s` is a string literal stored directly in the binary, fixed size.

	// do stuff with `s`

}  // this scope is now over, and `s` is no longer valid
```

- Ex 2:
```Rust
{  // s is not valid here, it’s not yet declared

	let s = String::from("hello");  // `s` is valid from this point forward.
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
  
- <ins>RESTRICTION 2 OF MUTABLE REFERENCES</ins>: **you can’t have a mutable reference to a variable if an immutable reference already exists for it.** This is because immutable references don’t expect the underlying value to change, which is problematic if you have a mutable reference. BUT, you can have multiple immutable references to the same variable, because the underlying data is not going to change.

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

### Attributes of a Struct
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

### Tuple Structs (anonymous structs)

- We can create Structs without named fields.

- Tuple structs are useful when you want your entire tuple to have a name and be of different type then other tuples...

```Rust
// In the below, Color and Point have the same field/attribute types, which are three signed 32 bit integers.
// But, they are of different type: one is Color and one is Point. As a result, if a function expects a tuple
// struct of type Point, you cannot pass it Color.
struct Color(i32, i32, i32);
struct Point(i32, i32, i32);
```

### Example to Show the Value of Structs

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

### Derived Traits

**What if we want to print our rectangle?? Our Rectangle struct does not implement the Display trait.** The Display trait specifies how something should be printed. Primitive types like integers implement this Display trait by default, since there is only one way to print an integer. But, for custom types like our structure, we have to implement it ourselves. 

<img width="583" alt="Image" src="https://github.com/user-attachments/assets/a0dd0851-987d-4dce-aa35-1c65f93c60fe" />

SOLUTION: `println!("rect: {:?}", rect);	// use the {:?}`

**New Error:** Now we see that our **Rectangle struct doesn’t implement the Debug trait**, which allows us to print out information useful for developers.

<img width="686" alt="Image" src="https://github.com/user-attachments/assets/d79412b6-756a-440e-b3d1-2ad4983c5cba" />

SOLUTION: use a **derived trait**...
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

### Methods
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

### Associated Functions
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
We **could define each of these variants as a separate struct; however these structs would all have different types. The benefit of an enum is that all of these variants are grouped under the Message type.**
```Rust
enum Message {
    Quit,
    Move { x : i32, y : i32 },
    Write(String),
    ChangeColor(i32, i32, i32),
}
```




