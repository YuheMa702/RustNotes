# References and Borrowing

**Goal:** Learn the concept of reference in Rust to use variables without owning them.

Unlike a pointer, a reference is gauranteed to point to a valid value during its life.



Example:
```rust
fn main() {
    let s1 = String::from("hello");

    let len = calculate_length(&s1); // don't need to return s1 as we never had ownership

    println!("The length of '{}' is {}.", s1, len);
}

fn calculate_length(s: &String) -> usize {
    s.len()
}
```

Just like variables, references are immutable by default.

## Mutable References

We can create mutable reference with `&mut` keyword. However there could be only one mutable reference at a time.

Example:
```rust
fn main() {
    let mut s = String::from("hello");

    change(&mut s);
}

fn change(some_string: &mut String) {
    some_string.push_str(", world");
}
```

You can't have more than one mutable reference at a time:
```rust
    let mut s = String::from("hello");

    {
        let r1 = &mut s;
    } // r1 goes out of scope here, so we can make a new reference with no problems.

    let r2 = &mut s;
```

You can't have both mutable and immutable reference to the same variable:
```rust
    let mut s = String::from("hello");

    let r1 = &s; // no problem
    let r2 = &s; // no problem
    let r3 = &mut s; // BIG PROBLEM

    println!("{}, {}, and {}", r1, r2, r3);
```

## Dangling References

Rust compiler will prevent dangling references, pointers to locations that are freed or owned by someone else.

Example:
```rust
fn main() {
    let reference_to_nothing = dangle();
}

fn dangle() -> &String { // dangle returns a reference to a String

    let s = String::from("hello"); // s is a new String

    &s // we return a reference to the String, s
} // Here, s goes out of scope, and is dropped. Its memory goes away.
  // Danger!
```

If we run above code:
```shell
$ cargo run
   Compiling ownership v0.1.0 (file:///projects/ownership)
error[E0106]: missing lifetime specifier
 --> src/main.rs:5:16
  |
5 | fn dangle() -> &String {
  |                ^ expected named lifetime parameter
  |
  = help: this function's return type contains a borrowed value, but there is no value for it to be borrowed from
help: consider using the `'static` lifetime
  |
5 | fn dangle() -> &'static String {
  |                 +++++++

For more information about this error, try `rustc --explain E0106`.
error: could not compile `ownership` due to previous error
```

The solution is to return the string directly. We will cover the concept of lifetimes in Chapter 10!!

## Reference

[See the original chapter in the Rust Book](https://doc.rust-lang.org/stable/book/ch04-02-references-and-borrowing.html)



