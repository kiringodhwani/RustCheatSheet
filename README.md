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
            // no named parameters in rust so type in value then "param_name:" shows up.
            //

            // read_line takes in the user's input and appends it to the specified buffer
            // we specify the buffer to be guess (which is initialized to '').
            // specify the buffer as a mutable reference (here, to the guess string), so
            // it takes a reference to the guess string and modifies it without taking
            // ownership of it. Returns a result type that either returns 'Ok' holding
            // the return value (i.e., user input) or 'Err' holding an error object.
            .read_line(&mut guess)

            // If an error is returned, probably a system error. If Ok is returned, then expect
            // returns the value stored in Ok. Otherwise error message.
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
