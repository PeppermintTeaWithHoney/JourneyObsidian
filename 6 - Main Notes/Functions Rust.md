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





### Statements and Expressions

Function bodies are made up of series of statements optionally ending in a expression. 
So far do the functions we have covered not included a ending expression but we had expressions as part of statements.  Because Rust is a expression based languages its important to understand. 

Statements are instructions that perform some action and do nut return a value.

Expressions evaluate to a resultant value.



Lets look at examples:

```rust
fn main() {
    let y = 6;
}
```

Creating a variable and assigning a value to it with the let keyword is a statement. 

Function definitions are also statements, the entire preceding example is a statement in itself.(As we’ll see below, _calling_ a function is not a statement, though.)

Statements don't return any value, so we can't assign them to another variable. 
If we try that in the following code:

```rust
fn main() {
    let x = (let y = 6);
}
```

we will get the following error:

```bash
$ cargo run
   Compiling functions v0.1.0 (file:///projects/functions)
error: expected expression, found `let` statement
 --> src/main.rs:2:14
  |
2 |     let x = (let y = 6);
  |              ^^^
  |
  = note: only supported directly in conditions of `if` and `while` expressions

warning: unnecessary parentheses around assigned value
 --> src/main.rs:2:13
  |
2 |     let x = (let y = 6);
  |             ^         ^
  |
  = note: `#[warn(unused_parens)]` on by default
help: remove these parentheses
  |
2 -     let x = (let y = 6);
2 +     let x = let y = 6;
  |

warning: `functions` (bin "functions") generated 1 warning
error: could not compile `functions` (bin "functions") due to 1 previous error; 1 warning emitted

```

The let y = 6 statement doesn't return a value so we cant bind it to x.
Expressions evaluate to a value and make up most of the rest of code i'll write in Rust.
Consider a simple math operation such as 5+6, is a expression that evaluate to 11. 
Expressions can be part of a statement, like in the earlier example let y = 6, the 6 is a expression that evaluates to the value 6. Calling a function is a expression and calling a macro is too. A new scope block with curly brackets is an expression. 

```rust
fn main() {
    let y = {
        let x = 3;
        x + 1
    };

    println!("The value of y is: {y}");
}
```

This expression 

```rust
{
    let x = 3;
    x + 1
}
```

is a block, that in this case evaluates to 4 and the value gets bound to y as part of the let statement. Note that the x + 1 line doesn't have a semicolon at the end, which is unlike the lines we saw before. Expressions do not include semicolons. If we add a semicolon to the end of a expression, we turn it into a statement and it wont return a value.





### Functions with return values


Functions can return values to the code that calls them, but we must declare their type after an arrow -->. In Rust, the return value of a function is synonymous with the value of the final expression in the code of the body of a function. We can return early using the return keyword and specifying a value. But most functions return the last expression implicitly.
Here is an example of a function that returns a value:

```rust
fn five() -> i32 {
    5
}

fn main() {
    let x = five();

    println!("The value of x is: {x}");
}
```


As we can see there is no function calls,macros or even let statements in the five function, just the number itself. That's a perfectly valid function in Rust. And we specified the return type too with i32.

```bash
$ cargo run
   Compiling functions v0.1.0 (file:///projects/functions)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.30s
     Running `target/debug/functions`
The value of x is: 5
```

The return value of the five functions is 5 and its i32. The line let x = five() assigns x to the return value of the five function. So this would evaluate to let x = 5. 

Also the five functions has no parameter and defines the type of the return value already. 
The body of the function is a expression without ;  and we want to return the value. 

```rust
fn main() {
    let x = plus_one(5);

    println!("The value of x is: {x}");
}

fn plus_one(x: i32) -> i32 {
    x + 1
}
```
This will print The value of x is: 6
If we would remove the semicolon from it we would get the following error:

```bash
$ cargo run
   Compiling functions v0.1.0 (file:///projects/functions)
error[E0308]: mismatched types
 --> src/main.rs:7:24
  |
7 | fn plus_one(x: i32) -> i32 {
  |    --------            ^^^ expected `i32`, found `()`
  |    |
  |    implicitly returns `()` as its body has no tail or `return` expression
8 |     x + 1;
  |          - help: remove this semicolon to return this value

For more information about this error, try `rustc --explain E0308`.
error: could not compile `functions` (bin "functions") due to 1 previous error
```

















# References


https://rust-book.cs.brown.edu/ch03-03-how-functions-work.html