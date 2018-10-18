# Chapter 1
## Anatomy of a Rust Program
- `fm main() { /* */}` - defines a function in Rust
  - `main` function is special. It's the first code that gets run in an executable
  - `{}` are required around function bodies
- `println!("Hello, World);`
  - Rust style is to indent with 4 spaces, not a tab
  - `println!` calls a macro. Function names do not include the `!`
  - Takes a string as an argument
  - the line ends with a semicolon
- Use `rustfmt` to convert file to idiomatic style

## Compiling and Running are Separate Steps
- before running a program use `rustc` to compile it
- this will create an executable in the same directory
- Rust is a n ahead of time compile language. Yuo can coompile a program and hand off the executable to someone else to run.
- `rustc` is fine for simple programs. For bigger projects, use `cargo`

## Hello, Cargo!
- Cargo is Rust's build system and package manager
- Bigger projects will have dependencies and `cargo` makes them easier to manage.
- The rest of this book assumes you are using `cargo`

## Creating a Project with Cargo
``` bash
$ cargo new hello_cargo --bin
```
- creates an executable called _hello_cargo_
- `--bin` creates an executable application as opposed to a library
- creates a src folder
- creats Cargo.toml
  - TOML is Cargo's configuration format
  - `[package]` indicates the following lines are for configuring a package
  - name
  - version
  - authors
  the last line `[dependencies]` is the start of the section where you define what crates you need.

## Building and Running a Cargo Project
Run:
``` bash
cargo build
```
from the root of your cargo project to compile.

- creates a `target` folder containing the compiled executables
- creates a `Cargo.lock` file at the top directory
  - keeps track of exact dependency versions
- you can run `cargo run` to copile the code and then run the executable in a singel step
- run `cargo check` to see if your code copiles without producing an executable
  - Why? Faster.

## Building for Release
Run:
``` bash
cargo build --release
```
from the root of your cargo project to compile a release version of your code.

- This will build to `target/release` instead of `target/debug`
- optimizations make the resulting executable run faster but compilation is slower


## Cargo as Convention
Even though we didn't get a lot of the benefits of cargo in this project we have learned a major part of the toolchain we will be using to work in larger and more complex Rust codebases.