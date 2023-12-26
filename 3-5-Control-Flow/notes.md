# Rust Control Flow

**Goal:** Learn how to control the flow of execution of Rust code with ifs and loops.


## `if` Expressions

**Notes:** 

- Condition code should evaluate to `bool`, integers don't work in Rust.
- Using too many else if will cluster your code, chapter 6 will introduce `match`.
Example:
```rust
fn main() {
    let number = 6;

    if number % 4 == 0 {
        println!("number is divisible by 4");
    } else if number % 3 == 0 {
        println!("number is divisible by 3");
    } else if number % 2 == 0 {
        println!("number is divisible by 2");
    } else {
        println!("number is not divisible by 4, 3, or 2");
    }
}
```

## Conditional Assignment

Use `if` in a `let` statement to conditionally assign value to a variable.

However, the `if` and `else` arms must have the same value type.

```rust
fn main() {
    let condition = true;
    let number = if condition { 5 } else { 6 };

    println!("The value of number is: {number}");
}
```

## Repetition with Loops

Rust offers 3 types of loops: `loop`, `while`, and `for`.

### Repeating code with `loop`

**Notes:**

- `loop` keyword tells Rust to execute loop body forever until you stop it.
- `break` keyword will terminate the loop.
- `continue` keyword skip to the next iteration.
- _loop label_ must begin with a single quote.

Example:
```rust
fn main() {
    let mut counter = 0;

    let result = loop {
        counter += 1;

        if counter == 10 {
            break counter * 2;
        }
    };

    println!("The result is {result}"); // result is 20
}
```

Use loop labels to break specific loop:
```rust
fn main() {
    let mut count = 0;
    'counting_up: loop {
        println!("count = {count}");
        let mut remaining = 10;

        loop {
            println!("remaining = {remaining}");
            if remaining == 9 {
                break;
            }
            if count == 2 {
                break 'counting_up;
            }
            remaining -= 1;
        }

        count += 1;
    }
    println!("End count = {count}");
}
// Numbers printed would be 0 10 9 1 10 9 2
```

### Conditional Loops with `while`

**Notes:**

- While the condition is true, the loop will run, else it will break.
- `while` is a combination of `loop`, `if`, `else`, and `break`.

Example:
```rust
fn main() {
    let mut number = 3;

    while number != 0 {
        println!("{number}!");

        number -= 1;
    }

    println!("LIFTOFF!!!");
}
```

### Looping through a Collection with `for`

**Notes:**

- Using `for` loops for arrays is safe without invalid accesses or missing values.
- `for` is also very concise when used to count items.

An array is an iterable collection:
```rust
fn main() {
    let arr = [1, 2, 3, 4, 5];
    for elem in arr {
        println!("The value is: {elem});
    }
}
```

Use `rev` method to countdown:
```rust
fn main() {
    for number in (1..4).rev() {
        println!("{number}!");
    }
    println!("LIFTOFF!!!");
}
```
