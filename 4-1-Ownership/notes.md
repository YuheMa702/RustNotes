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
