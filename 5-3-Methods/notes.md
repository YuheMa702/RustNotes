# Struct Functions

**Goal:** Group associated function inside `impl` blocks for better structure and readability

**Notes:** 

- All functions inside `impl` blocks are called _associated functions_.
- Methods are the ones with Self as a parameter, use dot operator.
- Use double colons for non-method associated functions.


Example:
```rust
impl Rectangle {
    fn area(&self) -> u32 { // method
        self.width * self.height
    }

    fn can_hold(&self, other: &Rectangle) -> bool { // method
        self.width > other.width && self.height > other.height
    }
    fn square(size: u32) -> Self { // non-method use :: to call
        Self {
            width: size,
            height: size,
        }
    }
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };
    let rect2 = Rectangle {
        width: 10,
        height: 40,
    };
    let rect3 = Rectangle {
        width: 60,
        height: 45,
    };
    let sq = Rectangle::square(30); // Use double colon here

    println!("Can rect1 hold rect2? {}", rect1.can_hold(&rect2));
    println!("Can rect1 hold rect3? {}", rect1.can_hold(&rect3));
    println!("Can rect1 hold sq? {}", rect1.can_hold(&sq));
}
```

## Reference

[See the original chapter in the Rust Book](https://doc.rust-lang.org/stable/book/ch05-03-method-syntax.html)
