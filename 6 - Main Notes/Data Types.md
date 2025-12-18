2025-12-17 15:45

Status: 

Tags: [[Rust]], [[Programming]]


# Data Types


Rust is a statically typed language that means it needs to know the types of all variables at compile time. usually the compiler knows it from the value we stored. But if we have many different types for example, if we parse the type, we must add a type annotation. 

```rust
let guess: u32 = "42".parse().expect("Not a number!");
```

In this case we parse the original string to a u32 aka unassigned integer 32 bit. 
If we wouldn't add the u32 annotation it would result into a compile error. Because the compiler needs to know what type we want to parse into.

```bash
$ cargo build
   Compiling no_type_annotations v0.1.0 (file:///projects/no_type_annotations)
error[E0284]: type annotations needed
 --> src/main.rs:2:9
  |
2 |     let guess = "42".parse().expect("Not a number!");
  |         ^^^^^        ----- type must be known at this point
  |
  = note: cannot satisfy `<_ as FromStr>::Err == _`
help: consider giving `guess` an explicit type
  |
2 |     let guess: /* Type */ = "42".parse().expect("Not a number!");
  |              ++++++++++++

For more information about this error, try `rustc --explain E0284`.
error: could not compile `no_type_annotations` (bin "no_type_annotations") due to 1 previous error

```




### Scalar Types

A scalar type represents a single value, Rust has 4 primary scalar types. Integers,floats,boolean's and characters.


### Integer Type

A integer is a number without a fractional component.


![[Pasted image 20251217155429.png]]

Each integer has a specific bit size and therefor can store a different max number. Signed just means it can be negative and positive, unsigned can only be positive. 

Each signed variant can store numbers from −(2n − 1) to (2n − 1) − 1, where n is the number of bits getting used so for 8-bit it would be 8. Unsigned can't go into the minus so their formula is a bit different, 0 to 2 hoch 8 − 1.


The i-size and u-size depends on the computer system you use, there is 32bit systems and 64 ones. 


You can write integers in many different forms, as shown below.

![[Pasted image 20251217160205.png]]

So which size should we default to? Rust takes i32 as a default, which is good so usually can't get integer overflow.


Whats a integer overflow?

Lets imagine you have a i8 integer, that has valid 0 - 255 values. And you try to store a number with the value 258, a integer overflow will occur. That can result in one of two behaviors. 

When you are compiling in debug mode, Rust includes check for integers that causes your program to panic.  Rust uses the term panicking when a program exists with an error. 

On the other hand if you put the --release flag, rust does not include checks for integer overflow so it doesn't panic. Instead what happens is that rust wraps it around so if we have a i8 and we get a 300, it counts to 256 and starts from 0 again, resulting in a 44. 

To explicitly handle the possibility of a integer overflow we can use the provided methods. 

- Wrap in all modes with the `wrapping_*` methods, such as `wrapping_add`.
- Return the `None` value if there is overflow with the `checked_*` methods.
- Return the value and a Boolean indicating whether there was overflow with the `overflowing_*` methods.
- Saturate at the value’s minimum or maximum values with the `saturating_*` methods.



### Floating-Point Types

Rust also has two primitive types for floating-point numbers, which are numbers with decimal points. Rust floating-point types are f32 and 64, which are 32 and 64 bits in size,respectively. The default type is f64 because on modern CPUs, its roughly the same speed as f32 but is capable of more precision. All floating points are always signed. 

```rust
fn main() {
    let x = 2.0; // f64

    let y: f32 = 3.0; // f32
}
```



### Numeric Operations

Rust supports all the basic mathematical operations you would expect for all the number types. Addition, subtraction,multiplication,division and remainder. Integer division truncates towards zero to the nearest integer. 

```rust
fn main() {
    // addition
    let sum = 5 + 10;

    // subtraction
    let difference = 95.5 - 4.3;

    // multiplication
    let product = 4 * 30;

    // division
    let quotient = 56.7 / 32.2;
    let truncated = -5 / 3; // Results in -1

    // remainder
    let remainder = 43 % 5;
}
```



### Boolean Type

As in most other programming languages, Rust has two boolean types, true and false. Boolean are one byte in size. The boolean type in Rust is specified using bool. 

```Rust
fn main() {
    let t = true;

    let f: bool = false; // with explicit type annotation
}
```




### The Character Type

Rust's char type is the language's most primitive alphabetic type. 

```rust
fn main() {
    let c = 'z';
    let z: char = 'ℤ'; // with explicit type annotation
    let heart_eyed_cat = '😻';
}
```

In rust we specify chars with single quotes, as opposed to string literals,which use double quotes. Rust's char type is 4 bytes in size and represents a Unicode scalar value, which means it can represent a lot more than ASCII.Accented letters; Chinese, Japanese, and Korean characters; emoji; and zero-width spaces are all valid `char` values in Rust. A character isn't really a concept in Unicode, so our "feeling" to what a character is might not match with what a char is in Rust. 


### Compound Types

Compound types can group multiple values into one type. Rust has two primitive compound types, arrays and tuples. 


#### The Tuple Type

A tuple is a general way to group together a number of values with a variety of types into one compound type. Tuples have a fixed length: once declared and cannot grow or shrink in size. 

We create a tuple by writing a coma separated list inside parenthesis, each position in the tuple has a type and they don't need to match.


```rust
fn main() {
    let tup: (i32, f64, u8) = (500, 6.4, 1);
}
```
optional type annotation. 


The variable tup binds to the entire tuple because a tuple is considered a single compound type. To get individual values of a tuple, we can use pattern matching to destructure a tuple value.

```rust
fn main() {
    let tup = (500, 6.4, 1);

    let (x, y, z) = tup;

    println!("The value of y is: {y}");
}
```

This program first creates a tuple and binds it to tup. In then uses a pattern with let and turns it into three separate variables,x,y and z. This called destructuring because it breaks a single tuple into three parts. 

We can also access a tuple element directly b using a period followed by the index of the value we want to access.

```rust
fn main() {
    let x: (i32, f64, u8) = (500, 6.4, 1);

    let five_hundred = x.0;

    let six_point_four = x.1;

    let one = x.2;
}
```

This program creates a tuple x and assign each index value to a variable using the indexes. 
A tuple without any value has a special name, its called a unit. This value and its corresponding type are both written () and represent a empty return value. Expressions implicitly return the until value, if they don't return any other. 

We can also make a tuple mutable for some reason and directly change the value of the indexes like this:

```rust
fn main() {
    let mut x: (i32, i32) = (1, 2);
    x.0 = 0;
    x.1 += 5;
}
```

### The Array Type

The other way of having a collection of multiple values is an array, unlike a tuple the values in a array have to have the same type. A array in Rust has a fixed size. 

```rust
fn main() {
    let a = [1, 2, 3, 4, 5];
}
```

Arrays are useful when you want your data allocated on the stack, the same as the other types we have seen so far, rather than the heap(comes in chapter 4) or when you always want a fixed number of elements. An array isn't as flexible as a vector type, though. A vector is a similar collection type provided by the standard library that is allowed to grow or shrink in size because it contents live on the heap. If you are unsure if you should use a array or a vector, you probably should use a vector. 

Arrays are useful when you know you are dealing with a fixed size, like the months in a year.

```rust
let months = ["January", "February", "March", "April", "May", "June", "July",
              "August", "September", "October", "November", "December"];

```


You write an arrays type in square brackets writing the type, following the number of elements in the array. Like so:

```rust
let a: [i32; 5] = [1, 2, 3, 4, 5];
```

Here the type is i32 and the size of the array is 5 elements. 

You can also initialize an array to contain the same value of each element by specifying the initial value, followed by a semicolon, and then the length of the array as shown here:

```rust
let a = [3; 5];
```


The array named a will contain 5 elements that will all be set to the value 3 initially. This is the same as writing let a = [3, 3, 3, 3, 3]; but in a more concise way.


```rust
fn main() {
    let a = [1, 2, 3, 4, 5];

    let first = a[0];
    let second = a[1];
}
```

This is how we access indexes from a array. 


#### Invalid Array Element Access 

We can by accident try to access a invalid element of an array that is past the end of the array. 


```rust
use std::io;

fn main() {
    let a = [1, 2, 3, 4, 5];

    println!("Please enter an array index.");

    let mut index = String::new();

    io::stdin()
        .read_line(&mut index)
        .expect("Failed to read line");

    let index: usize = index
        .trim()
        .parse()
        .expect("Index entered was not a number");

    let element = a[index];

    println!("The value of the element at index {index} is: {element}");
}
```

This code will compile successfully. If we run this code using cargo run and enter 0-4 the program will print out the corresponding value at that index. If we enter a value past the end of the array as 10 for example, we will see a output like this:

```bash
thread 'main' panicked at src/main.rs:19:19:
index out of bounds: the len is 5 but the index is 10
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace

```

The program resulted in a runtime error at the point of using a invalid value in the indexing operation. The program exited with a error message and didn't execute the println! statement.  When we try to access a index Rust will check if that index is less than the length of the array. This can only happen at runtime, because the compiler cant possibly know what value we would enter when running the code.

Rust protects us against accessing incorrect indexes, in other languages invalid memory could be accessed. 









# References

https://rust-book.cs.brown.edu/ch03-02-data-types.html
