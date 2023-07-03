# RUST: Variables and Mutability

## Mutability

* By default, variables in Rust are immutable. This means that once a value is bound to a name, you cannot change that value.
* If you want to change the value of a variable, you need to make it mutable by adding the `mut` keyword before the variable name.
* Mutability can be useful for making code more convenient to write, but it can also lead to bugs if not used carefully.
* Ultimately, the decision of whether to use mutability or not depends on what you think is clearest in that particular situation.

### Notes

* Rust's emphasis on immutability makes it a good choice for writing concurrent code, as it helps to prevent race conditions.
* Immutable variables are also easier to reason about, as you don't have to worry about the value of the variable changing unexpectedly.
* However, mutability can be useful in some cases, such as when you need to update a value in a loop or when you need to pass a variable to a function that needs to be able to change its value.

### Example

The following will result in a compiler error:

```rust
fn main() {
    let x = 5;
    println!("The value of x is: {x}");
    x = 6;
    println!("The value of x is: {x}");
}
```

```bash
$ cargo run
   Compiling variables v0.1.0 (file:///projects/variables)
error[E0384]: cannot assign twice to immutable variable `x`
 --> src/main.rs:4:5
  |
2 |     let x = 5;
  |         -
  |         |
  |         first assignment to `x`
  |         help: consider making this binding mutable: `mut x`
3 |     println!("The value of x is: {x}");
4 |     x = 6;
  |     ^^^^^ cannot assign twice to immutable variable

For more information about this error, try `rustc --explain E0384`.
error: could not compile `variables` due to previous error
```

This can be resolved by adding `mut` to the variable declaration:

```rust
fn main() {
    let mut x = 5;
    println!("The value of x is: {x}");
    x = 6;
    println!("The value of x is: {x}");
}
```

```bash
$ cargo run
   Compiling variables v0.1.0 (file:///projects/variables)
    Finished dev [unoptimized + debuginfo] target(s) in 0.30s
     Running `target/debug/variables`
The value of x is: 5
The value of x is: 6
```

## Constants

* Constants are values that are bound to a name and are not allowed to change.
* Constants are declared using the `const` keyword instead of the `let` keyword.
* The type of the value must be annotated when declaring a constant.
* Constants can be declared in any scope, including the global scope.
* Constants may be set only to a constant expression, not the result of a value that could only be computed at runtime.
* Constants are valid for the entire time a program runs, within the scope in which they were declared.
* Naming hardcoded values used throughout your program as constants is useful in conveying the meaning of that value to future maintainers of the code.
* It also helps to have only one place in your code you would need to change if the hardcoded value needed to be updated in the future.

### Notes

* Constants are a good way to represent values that are not likely to change, such as the speed of light or the number of seconds in a minute.
* Constants can also be used to make your code more readable and maintainable.
* For example, if you have a constant for the maximum number of points a player can earn in a game, you can use that constant throughout your code instead of having to hard-code the value in multiple places.

### Example

Below shows a constant declaration:

```rust
const THREE_HOURS_IN_SECONDS: u32 = 60 * 60 * 3;
```

A few things to note:

* The right hand side assignment of `60 * 60 * 3` is a "constant expression", i.e. it is not the result of a value that could only be computed at runtime.
* Notice the convention of using `UPPER_SNAKE_CASE` for the name.

## Shadowing

* Shadowing is a technique where a new variable with the same name as a previous variable is declared.
* The new variable shadows the previous variable, and the compiler will see the new variable when the name is used.
* Shadowing can be used to change the type of a variable, but it cannot be used to mutate the type of a variable.

### Example

The code below demonstrates shadowing:

```rust
fn main() {
    let x = 5;

    let x = x + 1;

    {
        let x = x * 2;
        println!("The value of x in the inner scope is: {x}");
    }

    println!("The value of x is: {x}");
}
```

This results in the following output:

```bash
$ cargo run
   Compiling variables v0.1.0 (file:///projects/variables)
    Finished dev [unoptimized + debuginfo] target(s) in 0.31s
     Running `target/debug/variables`
The value of x in the inner scope is: 12
The value of x is: 6
```

This is useful in situations where you want to change the type of a variable, preserve the immutability at the end of your transformations and avoid having to create a separate variable with a different name (e.g. `something` and `something_str`).

```rust
    let spaces = "   ";
    let spaces = spaces.len();
```

Shadowing is different to marking a variable with `mut`. Whilst `mut` will let you reassign the variable, it does not allow you to change it's type.

The following example demonstrates this:

```rust
    let mut spaces = "   ";
    spaces = spaces.len();
```

When compiled, the following error occurs:


```bash
$ cargo run
   Compiling variables v0.1.0 (file:///projects/variables)
error[E0308]: mismatched types
 --> src/main.rs:3:14
  |
2 |     let mut spaces = "   ";
  |                      ----- expected due to this value
3 |     spaces = spaces.len();
  |              ^^^^^^^^^^^^ expected `&str`, found `usize`

For more information about this error, try `rustc --explain E0308`.
error: could not compile `variables` due to previous error
```
