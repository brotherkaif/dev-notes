# RUST: Control Flow

## `if` Expressions

* `if` expressions allow you to branch your code depending on conditions.
* The condition in an `if` expression must be a `bool`.
* If the condition is `true`, the block of code associated with the `if` expression will be executed.
* If the condition is `false`, the block of code associated with the `if` expression will be skipped.
* You can optionally include an `else` expression, which will be executed if the condition is `false`.
* The `if` expression can be nested, so you can have multiple levels of branching.

Here are some examples of `if` expressions:

```rust
if number < 5 {
  println!("The number is less than 5");
} else {
  println!("The number is not less than 5");
}

if number != 0 {
  println!("The number was something other than zero");
}
```

### Handling Multiple Conditions with `else if`

* You can use `else if` to check multiple conditions in a row.
* The `else if` conditions are evaluated in order, and the first condition that evaluates to `true` will be executed.
* If none of the `else if` conditions evaluate to `true`, the `else` block will be executed.

Here is an example of how to use `else if` to handle multiple conditions:

```rust
let number = 3;

if number < 0 {
  println!("The number is less than 0");
} else if number == 0 {
  println!("The number is equal to 0");
} else {
  println!("The number is greater than 0");
}
```

In this example, the first `else if` condition checks if the number is less than 0. If the condition evaluates to `true`, the `println!` statement will be executed. If the condition evaluates to `false`, the second `else if` condition will be checked. The second `else if` condition checks if the number is equal to 0. If the condition evaluates to `true`, the `println!` statement will be executed. If the condition evaluates to `false`, the `else` block will be executed.

The `else` block will only be executed if none of the `else if` conditions evaluate to `true`. In this example, the `else` block will be executed because the number is greater than 0.

### Using `if` in a `let` Statement

As `if` is an expression, we can use it on the right side of a `let` statement to assign the outcome to a variable:

```rust
fn main() {
    let condition = true;
    let number = if condition { 5 } else { 6 };

    println!("The value of number is: {number}");
}
```

In the example above, the value of `number` will be the value `5`.

The return value of each "arm" must be the same type. For example, the snippet below will result in an error:

```rust
fn main() {
    let condition = true;

    let number = if condition { 5 } else { "six" };

    println!("The value of number is: {number}");
}
```

## Repetition with loops

Rust has three kinds of loops: `loop`, `while`, and `for`.

### Repeating Code with `loop`

- The `loop` keyword tells Rust to execute a block of code forever, until you explicitly tell it to stop
- `break` within a `loop` will tell the program when to stop executing the loop
- `break` within a `loop` will tell the program to skip over the remaining code in the current iteration and move onto the next iteration

Example:

```rust
fn main() {
    loop {
        println!("again!");
    }
}
```

### Returning Values from Loops

- A common use-case of `loop` is to retry an operation you know might fail, such as checking whether a thread has completed its job
- The pattern below uses a `break` to return a value after stopping a `loop`

```rust
fn main() {
    let mut counter = 0;

    let result = loop {
        counter += 1;

        if counter == 10 {
            break counter * 2;
        }
    };

    // result should be 20 in this example
    println!("The result is {result}");
}
```

### Loop Labels to Disambiguate Between Multiple Loops

- For loops within loops, `break` and `continue` apply to the innermost loop at that point
- A "loop label" can be used in conjunction with `break` and `continue` to target a specific loop
- Loop labels must begin with a single quote

Example:

```rust
fn main() {
    let mut count = 0;
    // loop here is labelled 'counting_up
    'counting_up: loop {
        println!("count = {count}");
        let mut remaining = 10;

        loop {
            println!("remaining = {remaining}");
            if remaining == 9 {
                break;
            }
            if count == 2 {
                // the 'counting_up loop is specified
                break 'counting_up;
            }
            remaining -= 1;
        }

        count += 1;
    }
    println!("End count = {count}");
}
```

### Conditional Loops with `while`

A `while` loop will continue to run until a specified condition evaluates to `true`, at which point it will `break`.

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

The `while` construct removes the need to have a lot of nesting that would occur if you were to try and reimplement this logic using a combination of `loop`, `if`, `else`, and `break`.
