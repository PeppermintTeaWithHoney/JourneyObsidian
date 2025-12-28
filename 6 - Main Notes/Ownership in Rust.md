2025-12-28 13:16

Status:

Tags: [[Programming]], [[Rust]]

# Ownership in Rust


Ownership is a unique feature in Rust and has deep implications with the rest of the language. It gives Rust the ability to be memory safe without using a garbage collector. 
So its really important to understand how this works.

#### What is safety?
Its the absence of undefined behavior.

For example a safe program:

```rust
fn read(y: bool) {
    if y {
        println!("y is true!");
    }
}

fn main() {
    let x = true;
    read(x);
}
```

We could make the program unsafe:

```rust
fn read(y: bool) {
    if y {
        println!("y is true!");
    }
}

fn main() {
    read(x); // oh no! x isn't defined!
    let x = true;
}
```

Because we moved the call to read before defining x. 
read(x) expects to have a value of boolean, but x doesn't have a value yet.
Whenever this program gets executed by a interpreter, reading x before defining would raise an exception such as Pythons NameError. But these come at a cost. Each time a interpreted program reads a variable. then the interpreter must check whenever that variable is defined. 

Rust goal is to compile programs into efficient binaries that require as few runtime checks as possible. So Rust does not check at runtime if a variable is defined before being used.
That happens at compile time with the borrow-checker.

```bash
error[E0425]: cannot find value `x` in this scope
 --> src/main.rs:8:10
  |
8 |     read(x); // oh no! x isn't defined!
  |          ^ not found in this scope
```

Everyone probably would assume that it's good that Rust checks that variables are defined before they are used. But why? What would happen if we would use a variable before assigning it?

On a computer using x86 architecture the assembly would probably look like this:

```asm
main:
    ; ...
    mov     edi, 1
    call    read
    ; ...
```


The assembly code will do the following:

Move the number 1 into a register called edi

Call the read function, which expects the first argument y to be in the edi register.

If we would allow the unsafe function do compile, its assembly would look like this:

```asm
main:
    ; ...
    call    read
    mov     edi, 1    ; mov is after call
    ; ...
```

This program is unsafe because we call read on something that we expect to be a boolean, but it could be literally everything because we didn't define it before. It could be 2,100, or even `0x1337BEEF`. When read wants to use its argument y for any purpose, undefined behavior will happen. 

Rust doesn't specify what happens if you try to run where y {...} isn't true or false. That behavior or what happens after the execution is undefined. Something will happen for example:

The code will execute without crashing and no one will notice a problem.
The code will immediately crash due to a segmentation fault or another kind of operating system error.
The code continues to run without crashing until a bad actor finds out about this vulnerability and could delete our whole production database.  


One of the foundational goals of rust is to ensure no undefined behavior is happening.
That is the meaning of  "safety". Undefined behavior is especially dangerous with low-level programs that have direct access to memory. About 70% of all reported security vulnerabilities are caused from memory corruption, which is one form of undefined behavior.

A secondary goal of Rust is to catch all forms of undefined behavior at compile-time and not at run-time. This goal has two motivations:

1.  Catching bugs at run-time is better than catching them at production-time. Which improves the reliability of your programs.\
2. Catching bugs at compile-time means fewer run-time checks which improves the speed of our program.

Even then Rust can't prevent all bugs from happening. If an application exposes a public unauthenticated /delete-production-database endpoint, then someone doesn't need a suspicious if statement to delete the database. But Rust protections are likely still better than a language without the safety measures as shown by the Google's Android team.



### Ownership as a discipline for memory safety

Since safety is the absence of undefined behavior and ownership is for safety we need to understand ownership in terms of undefined behavior it prevents. The Rust Reference maintains a large list of undefined behavior, but for now we focus on the operations in memory. 

Memory is where data is stored while the execution of a program. There are many ways to think about memory. 

- If we are unfamiliar with system programming, you might think about memory on a high level like, memory is the ram in my computer. Or memory is the thing that runs out if use too much data. 
- If someone is familiar with system programming they might think of it like memory is a array of bytes or memory is the pointers i get back from malloc\\


Both of these two forms are valid but not useful ways to think about how Rust works.
The high level example is too abstract to get to know how memory works using Rust. 
You will need to understand the concept of a pointer for example. The low level example is too concrete to understand how Rust works. Rust does not allow you to interpret memory as an array of bytes for example. 

Rust providers a particular way of thinking about memory. Ownership is a discipline of safely using memory within this way of thinking.















# References

https://rust-book.cs.brown.edu/ch04-01-what-is-ownership.html