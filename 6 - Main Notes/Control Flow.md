2025-12-27 16:39

Status:

Tags: [[Rust]], [[Programming]]

# Control Flow

The ability to run some code depending on some conditions, or the ability to have a program run while a certain condition is true are basic building blocks in most programming languages. The most common constructs that we control the flow with in Rust are if conditions and loops.


## if Expressions

An if Expression allows us to branch our code depending on the conditions. We provide a condition and than a state, "if this condition is met, do this. If the condition isn't don't run this code."

```rust
fn main() {
    let number = 3;

    if number < 5 {
        println!("condition was true");
    } else {
        println!("condition was false");
    }
}
```


All if Expression start with the keyword if, followed by a condition. In our case the condition checks if the number is smaller than 5. If yes it prints condition was true, if not it prints condition was false.  In our case we provided a else statement. If we don't add this, the program just skips the if expression. 

```shell
$ cargo run
   Compiling branches v0.1.0 (file:///projects/branches)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.31s
     Running `target/debug/branches`
condition was true
```

Its also good to note, that the condition has to be a boolean. If it isn't it will cause a error. 

```rust
fn main() {
    let number = 3;

    if number {
        println!("number was three");
    }
}
```

```bash
$ cargo run
   Compiling branches v0.1.0 (file:///projects/branches)
error[E0308]: mismatched types
 --> src/main.rs:4:8
  |
4 |     if number {
  |        ^^^^^^ expected `bool`, found integer

For more information about this error, try `rustc --explain E0308`.
error: could not compile `branches` (bin "branches") due to 1 previous error
```



### Handling Multiple Conditions with if else

We can use multiple conditions by combining them with if else else if expressions. For example:

```rust
fn main() {
    let number = 6;

    if number % 4 == 0 {
        println!("number is divisible by 4");
    } else if number % 3 == 0 {
        println!("number is divisible by 3");
    } else if number % 2 == 0 {
        println!("number is divisible by 2");
    } else {
        println!("number is not divisible by 4, 3, or 2");
    }
}
```

This program has four possible paths it can take.

```bash
$ cargo run
   Compiling branches v0.1.0 (file:///projects/branches)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.31s
     Running `target/debug/branches`
number is divisible by 3
```

When the program executes it checks each body until one of them evaluates to true and executes that block.  As we can see even if 6 is divisible by 2 it doesn't show nor does the else condition show, because the 3 was executed earlier. Too many else if expressions can clutter our code, so if we have more than one we might want to refactor our code. 



### Using if in a let Statement

Because if is a expression we can write it on the right side of a let statement and assign it to a variable. 

```rust
fn main() {
    let condition = true;
    let number = if condition { 5 } else { 6 };

    println!("The value of number is: {number}");
}
```

The number variable will be bound depending on the outcome of the if block.

```bash
$ cargo run
   Compiling branches v0.1.0 (file:///projects/branches)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.30s
     Running `target/debug/branches`
The value of number is: 5
```

Code of blocks evaluate to the last expression in them. Numbers by them self are also Expressions. In this case the value of the if expression depends on which code block executes. So the value has the potential to be either of them, so it must be the same type. 
If they are mismatched we get an error like the following:

```rust
fn main() {
    let condition = true;

    let number = if condition { 5 } else { "six" };

    println!("The value of number is: {number}");
}
```

```bash
$ cargo run
   Compiling branches v0.1.0 (file:///projects/branches)
error[E0308]: `if` and `else` have incompatible types
 --> src/main.rs:4:44
  |
4 |     let number = if condition { 5 } else { "six" };
  |                                 -          ^^^^^ expected integer, found `&str`
  |                                 |
  |                                 expected because of this

For more information about this error, try `rustc --explain E0308`.
error: could not compile `branches` (bin "branches") due to 1 previous error
```

We get the Error because the if block evaluates to a integer and else block to a string, resulting in a mismatch. This will never work because variables must have a single type and rust needs to know at compile time which one it is. Knowing the type of the variable number lets the compiler verify the type is valid where ever we use it. Rust wouldn't be able to do that if the type of number would only be determined at runtime. The compiler would have to be way more complex and would make fewer guarantees about the code if it had to track multiple hypothetical types for any variable.



### Repetition with loops

Its often really useful to execute a code of block more than once. Rust provides several loops, that will run through the code inside the body and at the end start immediately again at the start. 

Rust has 3 different kind of loops. For, while and loop.


#### Repeating Code with loop

The code keyword tells rust to execute a code of block over and over again forever until you explicitly tell it to stop. 

```rust
fn main() {
    loop {
        println!("again!");
    }
}
```

It won't stop to print rust until we stop it, in our case with control + c.

```rust
$ cargo run
   Compiling loops v0.1.0 (file:///projects/loops)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.08s
     Running `target/debug/loops`
again!
again!
again!
again!
^Cagain!
```


Fortunately, Rust also provides a signal to stop and break out of a loop using code. We can use the break keyword within the loop of the program to tell it to stop. There is also the continue keyword in Rust, that tells the loop to skip over the remaining code in this loop.


### Return Values from Loops

One of uses of loop is to retry an operation that you know might fail, such as checking whether a thread completed its job.  We also might want to pass the result of that loop to the outside of the loop. To do this, we can add the value we want returned after the break expression you use to stop the loop; that value will be returned out of the loop so you can use it, as it shown in the following example:

```rust
fn main() {
    let mut counter = 0;

    let result = loop {
        counter += 1;

        if counter == 10 {
            break counter * 2;
        }
    };

    println!("The result is {result}");
}
```

So in the code snippet we make a mutable variable counter and initialize it to 0.
Than we declare a variable result that holds the value returned from the loop. On every iteration of the loop we add one to the counter variable and then check if the counter variable is equal to 10. When it is , we use the break keyword with the value counter * 2 and eat the end we use a semicolon to end the statement that assigns the value to result. And at the end we use the print macro and print the result, which in our case is 20.

We can also return from inside a loop. While break only exits the current loop, return always exists the current function. 

### Loop Labels to Disambiguate Between Multiple Loops



If we have loops within loops, break and continue apply to the innermost loop at that point. We can optional specify a loop label on a loop that you can then use with break or continue to specify that those keywords apply to the labeled loop instead of the innermost loop. Loop labels must begin with a single quote.

```rust
fn main() {
    let mut count = 0;
    'counting_up: loop {
        println!("count = {count}");
        let mut remaining = 10;

        loop {
            println!("remaining = {remaining}");
            if remaining == 9 {
                break;
            }
            if count == 2 {
                break 'counting_up;
            }
            remaining -= 1;
        }

        count += 1;
    }
    println!("End count = {count}");
}
```



The outer loop has the label 'counting_up, and it will count up from 0 to 2.
The inner loop without a label counts down from 10 to 9. The first break that doesn't specify a label will exist the inner loop only. The break 'counting_up; statement will exit the outer loop. 



### Conditional Loops with while 

A program will often need to evaluate a condition within a loop. While the condition is true, the loop runs. When the conditions ceases to be true, the program calls break, stopping the loop. It's possible to implement behavior like this using a combination of loop,if,else and break; we could try that right now, but this pattern is so common that rust has its own built-in language construct for it called while loop. 

```rust
fn main() {
    let mut number = 3;

    while number != 0 {
        println!("{number}!");

        number -= 1;
    }

    println!("LIFTOFF!!!");
}
```


This makes it way simpler and clearer. This program will go on until the number is 0. 


### Looping through a collection with for

We could use the while construct to loop over a elements of a collection, such as an array. For example:

```rust
fn main() {
    let a = [10, 20, 30, 40, 50];
    let mut index = 0;

    while index < 5 {
        println!("the value is: {}", a[index]);

        index += 1;
    }
}
```


The code here prints every loop the value of the index in the array a until index reaches 5.

But this approach is very error prone; we could cause the program to panic if we would for example set while index < 6, or we change the array to have 4 elements only. Its also slower because, the compiler adds runtime code to perform conditional checks of whatever the index is withing the bounds of the array on every iteration. 

That's why we can use the for loop. 

```rust
fn main() {
    let a = [10, 20, 30, 40, 50];

    for element in a {
        println!("the value is: {element}");
    }
}
```

This code will have the same output as the other code example, but we increased the safety of our code and eliminated the chance of bugs in our code. Because there is no chance that the for loop would beyond the end of the array or not going far enough and missing some items. Its also more efficient, because the index doesn't have to get compared to the length of the array at every iteration. 

Also we wouldn't need to remember if we changed the number of elements in a array.

The safety and conciseness of for loops makes them the most used ones in Rust.

Even in code we wrote earlier most rustaceans would use a for loop with in range.


```rust
fn main() {
    for number in (1..4).rev() {
        println!("{number}!");
    }
    println!("LIFTOFF!!!");
}
```







# References
https://rust-book.cs.brown.edu/ch03-05-control-flow.html