# The Slice Type

In simple words, a Slice type is a contiguous portion of a collection of elements, such as part of a String.

For example, if we want to find the first word in a long string of words separated by spaces:

```rust
// Return the length of first word in s
fn first_word(s: &String) -> usize {
    let bytes = s.as_bytes();

    for (i, &item) in bytes.iter().enumerate() {
        // The method returns a tuple pair, the 1st is index, 2nd reference to item
        if item == b' ' {
            return i;
        }
    }
    // No space found, return the length of the string
    s.len()
}

However, keeping track of indexes of words is very error-prone, especially when strings mutate.

Therefore, we should use **Slices** instead!!!

## String Slices `&str`

A `String` slice is a part of a `String`, for example:
```rust
let s = String::from("hello world");
let hello = &s[0..5];
let world = &s[6..11];
// There are also short hands

let hello = &s[..5];
let world = &s[6..];
let hello_world = &s[..];
```

**Note:** String slice range indices must occur at valid UTF-8 character boundaries.

Let's rewrite the first_word function using Slice:
```rust
fn first_word(s: &String) -> &str {
    let bytes = s.as_bytes();

    for (i, &item) in bytes.iter().enumerate() {
        if item == b' ' {
            return &s[0..i]; // Return a slice
        }
    }

    &s[..] // Return reference to the whole string
}
```

Using Slice will expose the invalid reference error much sooner:
```rust
fn main() {
    let mut s = String::from("hello world");

    let word = first_word(&s);

    s.clear(); // error!

    println!("the first word is: {}", word);
}
```

Here's the compiler error:

```shell
$ cargo run
   Compiling ownership v0.1.0 (file:///projects/ownership)
error[E0502]: cannot borrow `s` as mutable because it is also borrowed as immutable
  --> src/main.rs:18:5
   |
16 |     let word = first_word(&s);
   |                           -- immutable borrow occurs here
17 |
18 |     s.clear(); // error!
   |     ^^^^^^^^^ mutable borrow occurs here
19 |
20 |     println!("the first word is: {}", word);
   |                                       ---- immutable borrow later used here

For more information about this error, try `rustc --explain E0502`.
error: could not compile `ownership` due to previous error
```

## String Literals Are Slices

This is why string literals are immutable:
```rust
let s = "Hello, world!"; // the type of s is &str
```

## String Slices as Parameters

A experienced Rustacian would modify first_word function:

```rust
fn first_word(s: &str) -> &str {
```

In this case, the parameter can take `&str`, `&String`, and string literals:
```rust
fn main() {
    let my_string = String::from("hello world");

    // `first_word` works on slices of `String`s, whether partial or whole
    let word = first_word(&my_string[0..6]);
    let word = first_word(&my_string[..]);
    // `first_word` also works on references to `String`s, which are equivalent
    // to whole slices of `String`s
    let word = first_word(&my_string);

    let my_string_literal = "hello world";

    // `first_word` works on slices of string literals, whether partial or whole
    let word = first_word(&my_string_literal[0..6]);
    let word = first_word(&my_string_literal[..]);

    // Because string literals *are* string slices already,
    // this works too, without the slice syntax!
    let word = first_word(my_string_literal);
}
```

## Arrary Slices

Example:
```rust
let a = [1, 2, 3, 4, 5];

let slice = &a[1..3];

assert_eq!(slice, &[2, 3]);
```
In this case, the type of slice is `&[i32]`. More details will be introduced in chapter 8.

## Reference

[See the original chapter in the Rust Book](https://doc.rust-lang.org/stable/book/ch04-03-slices.html)




