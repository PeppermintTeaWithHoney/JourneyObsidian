2025-12-26 20:25

Status:

Tags: [[Rust]], [[Programming]]

# Functions Rust

Functions are everywhere in Rust, like in most other programming languages too.
One of the most important ones is the main function, which is the entry point of many programs. We use the fn keyword to declare a function and use snake case as the conventional style for function and variable names. 

```rust
fn main() {
    println!("Hello, world!");

    another_function();
}

fn another_function() {
    println!("Another function.");
}
```


We define a function in Rust using the fn keyword followed by the function name and the curly brackets.  Because we defined the function in the program, we can call it from inside the main function. As we can see we defined the function after the main, but we can still call it. Rust doesn't care about where we define the functions, just that it is defined somewhere in a scope that the caller can see. 

```bash
$ cargo run
   Compiling functions v0.1.0 (file:///projects/functions)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.28s
     Running `target/debug/functions`
Hello, world!
Another function.

```




### Parameters

We can define functions to have parameter, which are special variables that are part of the functions signature. When a function has parameters you can provide it with the correct values of these parameters. 

```rust
fn main() {
    another_function(5);
}

fn another_function(x: i32) {
    println!("The value of x is: {x}");
}
```


```bash
$ cargo run
   Compiling functions v0.1.0 (file:///projects/functions)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 1.21s
     Running `target/debug/functions`
The value of x is: 5
```

The declaration of another_function has 1 parameter named x. The type of x is specified as i32. When we pass 5 into the another function, the print macro puts 5 where the pair of curly brackets is.

In rust functions you must declare the type of each parameter. This is a deliberate decision made by the rust team. Requiring the type here, means we don't need it in other parts of the code. Also the compiler gives better error messages if it knows what type it needs. 

If we have more than 1 parameter we use a comma to split them like here:
```rust
fn main() {
    print_labeled_measurement(5, 'h');
}

fn print_labeled_measurement(value: i32, unit_label: char) {
    println!("The measurement is: {value}{unit_label}");
}
```

```bash
$ cargo run
   Compiling functions v0.1.0 (file:///projects/functions)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.31s
     Running `target/debug/functions`
The measurement is: 5h
```





# References


https://rust-book.cs.brown.edu/ch03-03-how-functions-work.html