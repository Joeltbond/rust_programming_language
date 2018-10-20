# Chapter 2
Creating a guessing game

## Processing a Guess
- To optain user input we need `io` from the standard library (`std`)
  - `use std::io;`
- Rust brings a few types into scope in the _prelude_.
  - other types have tyo be brought into scoe explicitely with a `use` statement

## Storing Values with Variables

``` rust
let mut guess = String::new();
```

- `let` is used to create a variable
  - variables are immutable by default.
  - `mut` before the variabel name makess the variable mutable

``` rust
let foo = 5; // immutable
let mut bar = 5; // mutable
```

- `String::new()` is a function that returns a new instance of `String`
  - a growable, UTF-8 encoded bit of text
  `::` syntaxe indictes that `new` is an _associated_ function of the `String` type rather than on an instance.
  - other languages call this a _static method_

``` rust
io::stdin().read_line(&mut guess)
    .expect("Failed to read line);
```

- `stdin()` returns an instance of `std::io::Stdin`
- `read_line` takes whatever the user types and places it in a string.
  - the string passed in needs to be mutable so it can be changes by this method
  - `&` indictes that an argument is a reference
    - see chapter 4 for a more thorough explanation of refences

## Handling Potential Failure with the Result Type
``` rust
.expect("Failed to read line");
```
- break method chaining into multiple lines for readability
- `read_line` returns and `io::Result`
  - rust has a generic `Result` type as well as specific versions such as`io::Result`
  - `Result` is and _enum_ of `Ok` and `Err`
  - if `io::Result` is `Err`, `expect` will cause the program to crash with the message that you passed to it.
  - if you don't call `expect` you will get a warning about not handling potential errors.

## Using a Crate to Get More Functionality
- Rust doesn't come with a randome number generator for we ill need to add a crate
- Add the rand crate under dependencies in Cargo.toml
- install `rand` by adding it to your Cargo.toml and running `cargo` build.
- you can see the documentation for your dependencies by running `cargo doc --open`

## Comparing the guess to the Secret Number
- `std::cmp::Ordering` is an `enum` with the variants `Less`, `Greater` and `Equal`
    - These are the possible outcomes when comparing two values
- a `match` expression is made up of _arms_
- rust allows shadowing of variables which is useful for converting them to the approriate type
  - which we will need to compare stdin input to a random number

## Allowing after multiple guesses and quiting after a correct guess
- After generating the number wrap the rest of the program in a `loop {}` block to repeat the questions
- quit the game after a correct guess by adding a `break;` statement.

## Handling invalid input
- switch from `.expect` to a `match` statement to handle errors without panicking.
  - Our program will ignore the value and restart the loop on `Err`