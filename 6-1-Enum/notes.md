# Define An Enum

**Goals:** Learn how to define an `enum` type in Rust.


## `enum` vs `struct`

**Note:** `enum` fields can be accessed via `::`

Example:
```rust
enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
    ChangeColor(i32, i32, i32),
}

struct QuitMessage; // unit struct
struct MoveMessage {
    x: i32,
    y: i32,
}
struct WriteMessage(String); // tuple struct
struct ChangeColorMessage(i32, i32, i32); // tuple struct
```


## The `Option<T>` type in Rust

**Note:** There is no null in Rust, so we use Option type

Example:
```rust
enum Option<T> {
    None,
    Some(T),
}

let some_number = Some(5);
let some_char = Some('e');

// Need to specify type when the value is None or null
let absent_number: Option<i32> = None;

```

## Reference

[See the original chapter in the Rust Book](https://doc.rust-lang.org/stable/book/ch06-01-defining-an-enum.html)
