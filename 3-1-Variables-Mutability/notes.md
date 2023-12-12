# Variables and Mutability!

**Goal:** Understand variables and their traits unique to Rust!

## Immutable by Default

**Why:** Immutable variables can enhance safety and facilitate concurrency.

**Notes:**

1. For immutable variables, once it's bound to a name, you can't change it! Otherwise, you will get an immutability error during compilation.
2. The Rust compiler **gaurantees** that when you state a value won't change, it really won't change.

## Make Variables Mutable with `mut` Keyword

**Why:** Mutability is very useful in certain scenarios.

For example, enter the following in src/main.rs:
```rust
fn main() {
    let mut x = 5;
    println!("The value of x is: {x}");
    x = 6;
    println!("The value of x is: {x}");
}
```

When we run with Cargo, it will compile successfully:

```
$ cargo run
   Compiling variables v0.1.0 (file:///projects/variables)
    Finished dev [unoptimized + debuginfo] target(s) in 0.30s
     Running `target/debug/variables`
The value of x is: 5
The value of x is: 6
```

## Constants

Constants are immutable, you can declare a constant with the `const` keyword instead of the `let` keyword. Rust's naming convension for constants is UPPERCASE_WITH_UNDERSCORE.

For example:
```rust
let mut current_time = 0;
const ONE_HOUR_IN_SECONDS: u32 = 60 * 60;
```

There are a few differences between constants and variables:

| Constants       | Variables (default) |
|:----------------|:--------------------|
| Can't use `mut` | Can use `mut`       |
| Can be declared globally | Mutable variables can't be declared globally    |
| Can only be assigned to a constant expression | Can be assigned to dynamic expressions |
| Type annotation is mandatory | Type annotation may be optional |

## Shadowing

When you declare a new variable with the same name as the previous one, the previous one gets shadowed:

```rust
fn main() {
    let x = 5;      // 5 binds to x

    let x = x + 1;  // {x + 1} binds to x
                    // After old x exits the {x + 1} scope, it gets shadowed.

    {
        let x = x * 2;
        println!("The value of x in the inner scope is: {x}"); // 12
    }

    println!("The value of x is: {x}"); // 6
}
```

Shadowing is different from `mut`:

1. After using `let` to binds a new expression to an old name, the new variable is still immutable
2. With `let`, we can change variable types, but with `mut`, we cannot.

## Reference

[See the original chapter in the official Rust Book](https://doc.rust-lang.org/book/ch03-01-variables-and-mutability.html)
