# Structs in Rust

**Notes:**

- `struct` is immutable by default.
- You can only make the entire struct mutable with `mut` keyword.
- Access `struct` field using dot operator.

Define a User Struct:
```rust
struct User {
    active: bool,
    username: String,
    email: String,
    sign_in_count: u64,
}

fn main() {
    let mut user1 = User { // create a mutable instance
        active: true,
        username: String::from("someusername123"),
        email: String::from("someone@example.com"),
        sign_in_count: 1,
    };

    // modity struct field
    user1.email = String::from("anotheremail@example.com");
}
```

You can create a builder function for struct:
```rust
fn build_user(email: String, username: String) -> User {
    User {
        active: true,
        username, // shorthand when param name == field name
        email, // shorthand when param name == field name
        sign_in_count: 1,
    }
}
```

## Struct Update Syntax

Create a new instance using an old one:

```rust
fn main() {
    // --snip--

    let user2 = User {
        email: String::from("another@example.com"),
        ..user1 // Note update syntax must come last to set the remaining fields
    };
}
```

**Note:** The String field of user1 was moved to user2 so we can no longer use user1 as a whole!!!

## Using Tuple Struct without named fields

**Notes:**

- Can destructure them to their fields.
- Can use dot operator to access fields.

Example:
```rust
struct Color(i32, i32, i32);
struct Point(i32, i32, i32);

fn main() {
    let black = Color(0, 0, 0);
    let origin = Point(0, 0, 0);
}
```

## Unit-like Struct without Fields

Define a trait:
```rust
struct AlwaysEqual;

fn main() {
    let subject = AlwaysEqual;
}
```

More on how to define traits and implement them in chapter 10

## Reference

[See the original chapter in the Rust Book](https://doc.rust-lang.org/stable/book/ch05-01-defining-structs.html)



