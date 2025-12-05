2025-12-03 14:35

Status:

Tags: [[Programming]], [[Rust]]


# Rust Programming a Guessing Game

```rust
use std::io;

fn main() {
    println!("Guess the number!");

    println!("Please input your guess.");

    let mut guess = String::new();

    io::stdin()
        .read_line(&mut guess)
        .expect("Failed to read line");

    println!("You guessed: {guess}");
}
```





Rust has a standard of set items that it brings into every program, its called the prelude. If you want to bring something into the scope of the program that isn't in the prelude you have to use std::example. In the case above we bring the io library into the program.

The main function is the entry point to the program. 

```rust
fn main(){
}
```

The fn syntax declares a new function. Into the parentheses would go a parameter, in this case there are none. The curly brackets starts and end the body of the function.


```rust
    println!("Guess the number!");

    println!("Please input your guess.");

```

The println! macro just prints the string to the screen.


### Storing Values with Variables

```rust
    let mut guess = String::new();

```

There is a lot going on in this line. We use the let statement to define a variable, in this case guess.
In rust variables are immutable by default, meaning we cant change the value after defining it. 
In this case we used mut to make the variable mutable, aka we can change the value of it.

We set this variable to the result of String::new(), a function that returns a new instance of a string. String is a string type provided by the standard library that is grow-able, UTF-8 encoded bit of text.
The :: syntax in the ::new line indicates that new is associated function of the String type. And with that we created a variable and set it to a empty string. 



### Receiving User Input

```rust
    io::stdin()
        .read_line(&mut guess)

```


At the beginning we included the input/output with "use std::io;". Now we call the stdin function from the the io module which allows us to handle user input. 
If we hadn’t imported the `io` module with `use std::io;` at the beginning of the program, we could still use the function by writing this function call as `std::io::stdin`. The `stdin` function returns an instance of [`std::io::Stdin`](https://doc.rust-lang.org/std/io/struct.Stdin.html), which is a type that represents a handle to the standard input for your terminal.

Next, the line .read_line(&mut guess), calls the read_line method on the standard input handle to get input from the user.  We're also passing &mut guess as the argument to read_line to tell it where to store the user input in. So the full job for read_line is to take whatever the user types through standard input and append it to the strong we gave (without overwriting its contents), so therefor we pass the string as a argument. The strings argument needs to be mutable so the method can change the string's content. 

The & indicates that this argument is a reference, which gives you a way to let multiple parts of of your code access one piece of data without needing to copy the data into memory multiple times.  Like variables, references are mutable by default that's why we have to write &mut guess rather than &guess to make it mutable. 



## Handling Potential failure with Result

```rust
        .expect("Failed to read line");
```


Which could also had been written as:
```rust
io::stdin().read_line(&mut guess).expect("Failed to read line");
```

Which just prefer to split it over more than 1 line, to make it easier to read. So we try to split them when we use a new .method_name() syntax. 

So read_line puts whatever the user inputs into the string we passed to it. But it also returns a result value. Result is a enumeration, aka enum. Its a type that can be in one of multiple states, we call each possible state a variant. 

Results variants are Ok and Err. The Ok variant shows us that the operation was successful and it contains the successfully generated value. The Err variant means the operation failed, and it contains information on how the operation failed.

Values of the Result type, like value of any type, have methods defined to them. Result has the type .expect. It crashes the program and displays the message that we passed as an argument.

If the read_line method returns an Err, its most likely be coming from an error from the underlying operating system. 

If this instance of Result is an Ok value, expect will take the return value that Ok is holding and return just that value to you so you can use it. In this case it would be the bytes of the user input.

If we don't call except the program with compile, but we will get the following warning:

```cmd
$ cargo build
   Compiling guessing_game v0.1.0 (file:///projects/guessing_game)
warning: unused `Result` that must be used
  --> src/main.rs:10:5
   |
10 |     io::stdin().read_line(&mut guess);
   |     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
   |
   = note: this `Result` may be an `Err` variant, which should be handled
   = note: `#[warn(unused_must_use)]` on by default
help: use `let _ = ...` to ignore the resulting value
   |
10 |     let _ = io::stdin().read_line(&mut guess);
   |     +++++++

warning: `guessing_game` (bin "guessing_game") generated 1 warning
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.59s

```

In this case the compiler is warning us that Result may be an Err variant, which we should handle.

The right way to suppress this warning would be to write error handling code. Instead of writing expect. 

## Printing Values with println! Placeholders

That's the last line we have to discuss for now. 

```rust
    println!("You guessed: {guess}");
```

This line now prints the string that now contains our variable guess, aka the user input. The set of curly brackets is a placeholder: think of {} as little crab pincers that hold a value in place. When printing something we can use that to print the value of the variable when putting the name of it into the curly brackets. 

If we want to print the result of a evaluation we can put empty curly brackets and write a comma after the string with the thing we want to put into the brackets, which will evaluate. 

```rust
let x = 5;
let y = 10;

println!("x = {x} and y + 2 = {}", y + 2);
```
This code would print x = 5 and y+2 = 12



## Generating a secret number

Sadly rust doesn't provide anything in its standard library in terms of creating a random number, thankful there are crates out there that do, in this case rand. Its a library crate and its there to be used in more than one project. 


## Using a crate to get more functionality 

Our project is a binary crate, aka  executable. The rand crate is a library crate and it can't be executed on its own. Cargo's coordination of external crates is where it really shines. But before we can use the rand crate we have to edit our cargo.toml we to include it as a dependency. 

Anything that follows the header in the .toml file is part of it until another head comes. So we can write in dependencies what external crates we want to include. In our case we specify the rand crate and write the version behind it, with the semantic version specifier. We write 0.8.5 which means it will use a version not below 0.8.5 but anything up to 0.9. It does that because it considers any version up to the next bigger version has the same api, which cannot be guaranteed in the next bigger version anymore. 


```bash
$ cargo build
  Updating crates.io index
   Locking 15 packages to latest Rust 1.85.0 compatible versions
    Adding rand v0.8.5 (available: v0.9.0)
 Compiling proc-macro2 v1.0.93
 Compiling unicode-ident v1.0.17
 Compiling libc v0.2.170
 Compiling cfg-if v1.0.0
 Compiling byteorder v1.5.0
 Compiling getrandom v0.2.15
 Compiling rand_core v0.6.4
 Compiling quote v1.0.38
 Compiling syn v2.0.98
 Compiling zerocopy-derive v0.7.35
 Compiling zerocopy v0.7.35
 Compiling ppv-lite86 v0.2.20
 Compiling rand_chacha v0.3.1
 Compiling rand v0.8.5
 Compiling guessing_game v0.1.0 (file:///projects/guessing_game)
  Finished `dev` profile [unoptimized + debuginfo] target(s) in 2.48s

```

When we include a external dependency, Cargo fetches the latest version of everything it needs from the registry, which is a copy of data from Crates.io . Crates.io is where people in the rust ecosystem post their open source Rust projects for others to use. After updating the registry, Cargo checks all the dependencies section and downloads all crates listed that aren't already downloaded. In our case we only wrote rand, but it also downloads any dependencies that our dependency relies on. After downloading them rust compiles them and then compiles the project with the new dependencies available. If we now compile it again, it won't do anything because it knows that we already have everything included we wrote into the dependencies.




## Ensuring reproducible builds with cargo.lock

Cargo has a mechanism that ensures everyone can build the project the same way every time.  Cargo will use only the version of the dependencies we specified until we indicate otherwise. 
Lets use the following example, there is a new version for our rand crate, its 0.8.6 it brings a new bug fix with it, but also it breaks our program because it contains a regression. To handle this cargo creates the cargo.lock file the first time we use cargo build. 

So the first time we build cargo figures all versions of our dependencies out and stores them into the cargo.lock file, so now we can be sure we always build with the same versions, every time we build it. 


## Updating crates to a New Version 

When we do want to upgrade a crate, Cargo has the update command, which will ignore the cargo.lock file and figure out all the latest versions that fit our specifications in your cargo.toml file. 
Cargo then will write them to our cargo.lock file. In this case it will look for versions greater than 0.8.5 and smaller than 0.9.0.

If we wanted to have a major update, for example to 0.9.0 we would have to manually write that into the dependencies. The next time run cargo build, it will update the registry of crates available and reevaluate your rand requirements to the new version we have specified. 


## Generating a random number

```rust
use std::io;

use rand::Rng;

fn main() {
    println!("Guess the number!");

    let secret_number = rand::thread_rng().gen_range(1..=100);

    println!("The secret number is: {secret_number}");

    println!("Please input your guess.");

    let mut guess = String::new();

    io::stdin()
        .read_line(&mut guess)
        .expect("Failed to read line");

    println!("You guessed: {guess}");
}
```


First we import Rng method from the rand crate. Next, we're adding two lines in the middle. In the first line we call the rand::thread_rng() function that gives us the particular random number generator we want to use. One that is local to the current thread of operation and is seeded by the operating system. Then we call the .gen_range method on the random number generator. This method is defined by the rng trait we brand into scope. The gen_range lets us pick a range of numbers between the first and second number. The kind of range expression we use here takes the form start..=end and is inclusive of the lower and upper bounds.


Note: We can't just randomly know which traits to use and which methods and functions to call from a crate. So each crate comes with documentation with instructions for using it. The good thing about cargo is, we can write cargo doc --open and it will open a link and shows us all documentation provided by our dependencies. 




x















# References

https://rust-book.cs.brown.edu/ch02-00-guessing-game-tutorial.html