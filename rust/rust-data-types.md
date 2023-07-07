# RUST: Data Types

## Scalar types

Represent a single value. Rust has four primary scalar types:

    * **Integers** represent whole numbers. Rust has a variety of integer types, each with a different size and range of values.
    * **Floating-point numbers** represent numbers with decimal points. Rust has two floating-point types: `f32` and `f64`.
    * **Booleans** represent logical values: `true` or `false`.
    * **Characters** represent a single Unicode character.

## Compound types

Represent a collection of values. Rust has two primary compound types:

    * **Arrays** are fixed-size collections of values of the same type.
    * **Strings** are variable-size collections of characters.

## Other types

    * **Tuples** are fixed-size collections of values of different types.
    * **References** are pointers to other values.
    * **Enums** are a way of representing a finite set of values.

Data types are an important part of Rust programming. They determine the size and layout of variables in memory, the range of values that can be stored in variables, and the set of operations that can be performed on variables.

* The type of a variable is declared when the variable is created.
* The type of a value can be inferred by the compiler, but it is often helpful to explicitly declare the type.
* Rust is a statically typed language, which means that the types of all variables and values must be known at compile time.
* Type safety is an important feature of Rust. It helps to prevent errors and makes Rust code more reliable.

## Examples

**Integers**

```rust
let number: i32 = 100;
let another_number: u32 = 1000000;
```

**Floating-point numbers**

```rust
let float_number: f32 = 3.14159;
let another_float_number: f64 = 2.71828;
```

**Booleans**

```rust
let is_true: bool = true;
let is_false: bool = false;
```

**Characters**

```rust
let character: char = 'A';
let another_character: char = 'a';
```

**Arrays**

```rust
let array: [i32; 5] = [1, 2, 3, 4, 5];
```

**Strings**

```rust
let string: String = "This is a string".to_string();
```

**Tuples**

```rust
let tuple: (i32, String, bool) = (100, "This is a tuple", true);
```

**References**

```rust
let number: i32 = 100;
let reference = &number;
```

**Enums**

```rust
enum Color {
    Red,
    Green,
    Blue,
}

let color: Color = Color::Red;
```
