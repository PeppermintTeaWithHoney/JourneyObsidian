2025-12-27 16:30

Status:

Tags: [[Rust]],[[Programming]]

# Comments in Rust


We all should strive to make our code easy to understand, but sometimes some extra explaining is needed, that's what comments are there for. The compiler will ignore all comments. We use the following format for comments in Rust:

```rust
// hello, world
```

It starts with where the // are and end after the line finishes. 

```rust
// So we're doing something complicated here, long enough that we need
// multiple lines of comments to do it! Whew! Hopefully, this comment will
// explain what's going on.
```

There is also the multi-line syntax that starts with  /*  and ends with   * /

```rust
/* So we’re doing something complicated here, long enough that we need
   multiple lines of comments to do it! Whew! Hopefully, this comment will
   explain what’s going on. */
```

We can also place them at the end of a line containing code.

```rust
fn main() {
    let lucky_number = 7; // I'm feeling lucky today
}
```


But we will see them often like this:

```rust
fn main() {
    // I'm feeling lucky today
    let lucky_number = 7;
}
```

















# References

https://rust-book.cs.brown.edu/ch03-04-comments.html