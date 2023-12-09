# Hello, World!

**Goal:** After installing rust, it's time to write the famous hello_world program!

**Prerequisites:**
- Basic familiarity with the [command line](https://tutorial.djangogirls.org/en/intro_to_command_line/)
- Have [VSCode](https://code.visualstudio.com/download) or other editing tools/IDEs installed

## Create a Project Directory

For Linux, macOS, and PowerShell on Windows, enter this:
```
$ mkdir ~/projects
$ cd ~/projects
$ mkdir hello_world
$ cd hello_world
```
For Windows CMD, enter this:
```
> mkdir "%USERPROFILE%\projects"
> cd /d "%USERPROFILE%\projects"
> mkdir hello_world
> cd hello_world
```

## Writing Your First Rust Program

Create a new source file called **main.rs** inside hello_world directory.

Open **main.rs** and enter this:
```rust
fn main() {
    println!("Hello, world!");
}
```

## Running Your First Rust Program

On Linux or macOS, enter:
```
$ rustc main.rs
$ ./main
Hello, world!
```
On Windows, enter:
```
> rustc main.rs
> .\main.exe
Hello, world!
```

## Real-world Rust Programs

Right now just using [rustc](https://doc.rust-lang.org/rustc/what-is-rustc.html) may seem good enough for simple programs like hello_world. 

In the future, you will learn how to use [Cargo](https://doc.rust-lang.org/cargo/), the Rust package manager, for larger programs.

## Reference

[See the original chapter in the official Rust Book](https://doc.rust-lang.org/book/ch01-02-hello-world.html)
