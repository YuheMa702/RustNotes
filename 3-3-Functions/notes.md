# Functions

**Goals:** Learn the basic anatomy of Rust functions and tell the differences between statements and expressions.

## Overview

- Rust uses _snake_ style for functions: lower-case with underscore separating words. 

- Rust doesn't care where you define functions, as long as they can be seen by the caller.

Example:
```rust
fn main() {
    println!("Main function.");

    another_function();
}

fn another_function() {
    println!("Another function.");
}
```

## Parameters

- Concrete value parameters are called arguments.

- Type annotation is required for function signatures.

Example:
```rust
fn main() {
    print_labeled_measurement(5, 'h');
}

fn print_labeled_measurement(value: i32, unit_label: char) {
    println!("The measurement is: {value}{unit_label}");
}
```

## Statements and Expressions

Statement: Perform some action but does not return any value. Ends with a semicolon.

Expression: Evaluates to a resultant value. No semicolon at the end.

Example with scope block:
```rust
fn main() {
    let y = { // Starting the scope block
        let x = 3; // A statement
        x + 1 // An expression
    }; // The scope block returns 4

    println!("The value of y is: {y}");
}
```

## Functions with non-empty return values

- Must specify return type after an arrow.
- The function implicitly returns the last expression.
- Rust will err if there is a type mismatch of return type.

Example:
```rust
fn main() {
    let x = plus_one(5);

    println!("The value of x is: {x}");
}

fn plus_one(x: i32) -> i32 {
    x + 1
}
```

## Reference

[See the original chapter in the Rust Book](https://doc.rust-lang.org/stable/book/ch03-03-how-functions-work.html)





