# Hello, Cargo!
**Goal:** Now that you have written your first program, it's time to use Cargo to handle more complex projects!

## Creating a Project with Cargo

```
$ cargo new hello_cargo // create a new dir
$ cd hello_cargo        // will see a Cargo.toml and a src dir with a main.rs inside
```

**Notes:**
1. cargo also creates a new Git repo with a .gitignore file (use -vcs for no version control)
2. TOML stands for Tom's Obvious, Minimal Language = Cargo's configuration format
	- [package] : name, version, and edition of Rust are needed for Cargo to compile code
	- [dependencies] : packages of code in Rust are called crates
3. Cargo expect source files to live inside the src directory
	- top-level dir is for README, license info, config files, anything not related to code

## Build and Run a Cargo Project

```
$ cargo build                // generate an exe file in target/debug/hello_cargo
$ ./target/debug/hello_cargo // run the exe
$ cargo run                  // run the exe, would recompile if see changes
$ cargo check                // check if program compiles without creating an exe
```

**Notes:**
1. Run cargo build for the first time will gen a Cargo.lock file at top level
	- it keeps track of the exact versions of dependencies
2. cargo check much faster than cargo run
3. cargo is cross-platform, the commands are exact the same!

## Build for Release

```
$ cargo build --release // takes long time but optimize exe, in target/release
```

## Cargo as Convention

For any open-source Rust Project at GitHub, you can start working on it using Cargo:

```
$ git clone example.org/someproject
$ cd someproject
$ cargo build
```

## Reference

[See the original chapter in the official Rust Book](https://doc.rust-lang.org/book/ch01-03-hello-cargo.html)
