# What is Ownership

Some lanuages has a garbage collector, others require the programmer to explicitly allocate and free memories.

Rust uses the third approach, the **ownership system** to efficiently manage heap data.

**Ownership** is a set of rules, when violated, the program won't compile.

Mastering it will make it super easy to write safe and efficient Rust code.

## Ownership Rules

1. Each value in Rust has an _owner_.
2. Only one owner at a time.
3. When the owner goes out of scope, the value will be dropped.

## Variable Scope

**Scope:** the range within a program for which an item is valid.

Example:
```rust
    {                      // s is not valid here, it’s not yet declared
        let s = "hello";   // s is valid from this point forward

        // do stuff with s
    }                      // this scope is now over, and s is no longer valid
```

## The `String` Type

- `String` is a heap datatype.
- `String` doesn't have a known size (except for `string` literals).
- `String` can't be trivially copied to make a new, independent instance when used in a different scope.

Construct a `String` variable from a `String` literal:
```rust
    let mut s = String::from("hello"); // without the mut keyword, s is immutable

    s.push_str(", world!"); // push_str() appends a literal to a String

    println!("{}", s); // This will print `hello, world!`
```

## Memory and Allocation

Why can `String` be mutated while `String` literals cannot?

We know the content and size of `string` literals at compile time, which is why they are fast and efficient.

However, to support a mutable piece of text, whose size is unknown at compile time, we must use heap memory.

Rust doesn't require explicit `free`, the memory is automatically returned or dropped once the variable that owns it goes out of scope.

When a variable goes out of scope, Rust calls a special function called `drop`.

The ownership system is safe and efficient as there won't be missing `free` or double `free`.


## Variables and Data Interacting with Move

The transfer of ownership of heap data is called a move.
What accutally happen is: B points to the location A points to, and A gets dropped.

Example:
```rust
    let s1 = String::from("hello");
    let s2 = s1;

    println!("{}, world!", s1); // Error, s1 no longer valid
```

If run above code:
```shell
$ cargo run
   Compiling ownership v0.1.0 (file:///projects/ownership)
error[E0382]: borrow of moved value: `s1`
 --> src/main.rs:5:28
  |
2 |     let s1 = String::from("hello");
  |         -- move occurs because `s1` has type `String`, which does not implement the `Copy` trait
3 |     let s2 = s1;
  |              -- value moved here
4 |
5 |     println!("{}, world!", s1);
  |                            ^^ value borrowed here after move
  |
  = note: this error originates in the macro `$crate::format_args_nl` which comes from the expansion of the macro `println` (in Nightly builds, run with -Z macro-backtrace for more info)
help: consider cloning the value if the performance cost is acceptable
  |
3 |     let s2 = s1.clone();
  |                ++++++++

For more information about this error, try `rustc --explain E0382`.
error: could not compile `ownership` due to previous error
```

## Variables and Data Interacting with Clone

Obtain deep copy with `clone`:
```rust
    let s1 = String::from("hello");
    let s2 = s1.clone();

    println!("s1 = {}, s2 = {}", s1, s2); // Will compile without error
```

## The `Copy` trait for stack-only data

Rust has a special annotation called the `Copy` trait that we can place on types that are stored on the stack.

Rust won’t let us annotate a type with `Copy` if the type, or any of its parts, has implemented the `Drop` trait.

Here are some types that implement the `Copy` trait:

- All the integer types
- The Boolean type
- All the floating-point types
- The character type, `char`.
- Tuples, if they only contain types that also implement Copy. (`i32`, `i32`) works fine but (`i32`, `String`) does not.

## Ownership and Functions

**Notes:** 

- Passing variables to function will either copy or move.

- Returning value from a function is a copy or move, too.

Return value and Scope:
```rust
fn main() {
    let s1 = gives_ownership();         // gives_ownership moves its return
                                        // value into s1

    let s2 = String::from("hello");     // s2 comes into scope

    let s3 = takes_and_gives_back(s2);  // s2 is moved into
                                        // takes_and_gives_back, which also
                                        // moves its return value into s3
} // Here, s3 goes out of scope and is dropped. s2 was moved, so nothing
  // happens. s1 goes out of scope and is dropped.

fn gives_ownership() -> String {             // gives_ownership will move its
                                             // return value into the function
                                             // that calls it

    let some_string = String::from("yours"); // some_string comes into scope

    some_string                              // some_string is returned and
                                             // moves out to the calling
                                             // function
}

// This function takes a String and returns one
fn takes_and_gives_back(a_string: String) -> String { // a_string comes into
                                                      // scope

    a_string  // a_string is returned and moves out to the calling function
}
```

Return multiple values using a tuple:
```rust
fn main() {
    let s1 = String::from("hello");

    let (s2, len) = calculate_length(s1);

    println!("The length of '{}' is {}.", s2, len);
}

fn calculate_length(s: String) -> (String, usize) {
    let length = s.len(); // len() returns the length of a String

    (s, length)
}
```

## Reference

[See the original chapter in the Rust Book](https://doc.rust-lang.org/stable/book/ch04-01-what-is-ownership.html)
