# Rectangle Struct Example

**Goal:** We want an area function to calc the area of a rectangle.

Three Implementation Comparisons:
```rust
// Rookie
fn area(width: u32, height: u32) -> u32 {
// Unclear!! width and height not related by structure

// Using tuple
fn area(dimensions: (u32, u32)) -> u32 {
// Bug-prone, need to memorize indexes

// Best: use struct to group related variables
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    println!(
        "The area of the rectangle is {} square pixels.",
        area(&rect1)
    );
}

fn area(rectangle: &Rectangle) -> u32 {
    rectangle.width * rectangle.height
}
```

## Debuging Tips for Struct

**Notes:** 

- `struct` type does not implement `std::fmt::Display` therefore cannot use println!() with it.
- We can use the `debug` functionality to print helpful struct information
- Add the outer attribute starting with # just before struct definition

Now we can use the `:?` formatter with println!:
```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    println!("rect1 is {:?}", rect1);
}
```

Run above code:
```shell
$ cargo run
   Compiling rectangles v0.1.0 (file:///projects/rectangles)
    Finished dev [unoptimized + debuginfo] target(s) in 0.48s
     Running `target/debug/rectangles`
rect1 is Rectangle { width: 30, height: 50 }
```

We can also use the `dbg!` macro:
```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let scale = 2;
    let rect1 = Rectangle {
        width: dbg!(30 * scale), // dbg takes ownership whereas println! takes reference
        height: 50,
    };

    dbg!(&rect1); // We use reference here to prevent dbg taking ownership
}

Run above code:
```shell
$ cargo run
   Compiling rectangles v0.1.0 (file:///projects/rectangles)
    Finished dev [unoptimized + debuginfo] target(s) in 0.61s
     Running `target/debug/rectangles`
[src/main.rs:10] 30 * scale = 60
[src/main.rs:14] &rect1 = Rectangle {
    width: 60,
    height: 50,
}
```

## Reference

[See the original chapter in the Rust Book](https://doc.rust-lang.org/stable/book/ch05-02-example-structs.html)


