# RUST: Functions

## Functions

* Functions are a way to group together related code.
* They can be used to encapsulate logic and make code more readable and reusable.
* Functions are declared using the `fn` keyword.
* The function name, parameters, and return type are specified after the `fn` keyword.
* The body of the function is enclosed in curly braces.

## Parameters

* Parameters are the values that are passed to a function when it is called.
* They are declared in the function signature, after the function name.
* The type of each parameter must be specified.
* Parameters can be passed by value or by reference.

## Statements and Expressions

* Statements are instructions that perform some action.
* Expressions evaluate to a value.
* The body of a function is made up of statements and expressions.
* The last expression in the body of a function is the return value of the function.

## Functions with Return Values

* Functions can have a return value.
* The return value is the value that is returned to the caller of the function.
* The return value is specified after the function name, in the function signature.
* The return value of a function can be any type.

## Other Notes

* Functions can be nested.
* Functions can be recursive.
* Functions can be called from other functions.
* Functions can be passed as parameters to other functions.

## Examples

**Example 1: A function that adds two numbers**

```rust
fn add_numbers(x: i32, y: i32) -> i32 {
  x + y
}

fn main() {
  let sum = add_numbers(5, 10);
  println!("The sum is {}", sum);
}
```

**Example 2: A function that prints a greeting**

```rust
fn greet(name: &str) {
  println!("Hello, {}!", name);
}

fn main() {
  greet("Bard");
}
```

**Example 3: A function that returns the factorial of a number**

```rust
fn factorial(n: i32) -> i32 {
  if n == 0 {
    return 1;
  } else {
    return n * factorial(n - 1);
  }
}

fn main() {
  let factorial_of_5 = factorial(5);
  println!("The factorial of 5 is {}", factorial_of_5);
}
```
