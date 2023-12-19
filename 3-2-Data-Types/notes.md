# Data Types!

**Goal:** Learn the basic data types in Rust.

**Notes:**

- Rust is statically typed!
- Rust must know the types of all variables at compile time!
- Data types can be scalar or compound!

## Scalar Types

- Represents a single value.
- integers, floating-point numbers, Booleans, and characters.

### Integer Types

Table 1: Integer Types in Rust

| Length | Signed | Unsigned |
|:------:|:------:|:--------:|
| 8-bit  | `i8`   | `u8`     |
| 16-bit | `i16`  | `u16`    |
| 32-bit | `i32`  | `u32`    |
| 64-bit | `i64`  | `u64`    |
| 128-bit| `i128` | `u128`   |
| arch   | `isize`| `usize`  |


**Note:** `isize` and `usize` types depend on the architecture, can be either 32 or 64 bits.

Table 2: Integer Literals in Rust

| Number Literals   | Example     |
|:-----------------:|:-----------:|
| Decimanl          | `15_213`    |
| Hex               | `0x15213`   |
| Octal             | `0o77`      |
| Binary            | `0b111_010` |
| Byte (`u8` only)  | `b'A'`      |

**Note:** If unsure which int type to use, `i32` the Rust defult is a good place to start.

### Floating-Point Types

**Notes:**

- Rust's floating-point types are `f32` and `f64`.
- The default type is `f64`.

Example:
``` rust
fn main() {
    let x = 2.0; // f64
    let y: f32 = 3.0 // f32
}
```

### Numeric Operations

The basic mathematical operations are:
- addition (+)
- subtraction (-)
- multiplication (*)
- division (/) **Integer division rounding towards zero**
- remainder (%)

### The Boolean Type

Example:
```rust
fn main() {
    let t = true;

    let f: bool = false; // with explicit type annotation
}
```

### The Character Type

Example:
```rust
fn main() {
    let c = 'z';
    let z: char = 'ℤ'; // with explicit type annotation
    let heart_eyed_cat = '😻';
}
```

**Notes:**

- `char` literals use single quotes.
- `char` type is 32-bit long
- `char` can represent Unicode Scalar Values.


## Compound Types
Compound types can group multiple values into one type: tuples and arrays.

## The Tuple Type

**Notes:**

- Group various values with various types into one type.
- Has fixed length.
- Can add optional type annotations.

Example:
```rust
fn main() {
    let tup: (i32, f64, u8) = (500, 6.4, 1);
}
```

Use pattern matching to destructure a tuple:
```rust
fn main() {
    let tup = (500, 6.4, 1);

    let (x, y, z) = tup;

    println!("The value of y is: {y}");
}
```

Access tuple element directly with a period (.) followed by index number:
```rust
fn main() {
    let x: (i32, f64, u8) = (500, 6.4, 1);

    let five_hundred = x.0;

    let six_point_four = x.1;

    let one = x.2;
}
```

**Notes:** 

- The tuple without any values is called _unit_.
- Both the value and type of _unit_ are written `()`.
- `()` represents an empty value or an empty return type.


### The Array Type

Unlike tuple, every element inside an array must have the same type! Array in rust has a fixed length.

Example:
```rust
fn main() {
    let a = [1, 2, 3, 4, 5];
    let a: [i32; 5] = [1, 2, 3, 4, 5]; // Short hand
    let a = [3; 5] // [3, 3, 3, 3, 3]
}
```

**Notes:** Use array when you for stack-allocated variables and fixed length variables.

Access Array Elements using indexing:
```rust
fn main() {
    let a = [1, 2, 3, 4, 5];

    let first = a[0];
    let second = a[1];
}
```

Rust will panic at invalid array access:
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
If you run `cargo run` and enter 10:
```
thread 'main' panicked at 'index out of bounds: the len is 5 but the index is 10', src/main.rs:19:19
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace
```

## Reference

[See the original chapter in the Rust Book](https://doc.rust-lang.org/stable/book/ch03-02-data-types.html)