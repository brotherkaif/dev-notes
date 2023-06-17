# RUST: Hello, World!

## Creating a Project Directory
Create the following file structure:

```
hello_world/
└── main.rs
```

**Note:** The convention in Rust is to use `snake_case` for filenames. (e.g. `hello_world.rs` as opposed to `helloworld.rs`)

## Writing and Running a Rust Program

In `main.rs`:

```rust
fn main() {
    println!("Hello, world!");
}
```

Compile and run:

```bash
$ rustc main.rs
$ ./main
Hello, world!
```

## Anatomy of a Rust Program

```rust
fn main() {

}
```

The `main` function is special: it is always the first code that runs in every executable Rust program.

The function body is wrapped in `{}`. Rust requires curly brackets around all function bodies.

The body of the `main` function holds the following code:

```rust
println!("Hello, world!");
```

This line does all the work in this little program: it prints text to the screen.

There are four important details to notice here:

1. Rust style is to indent with four spaces, not a tab.
2. `println!` calls a Rust macro. If it had called a function instead, it would be entered as `println` (without the `!`).
3. We see the `"Hello, world!"` string. We pass this string as an argument to `println!`, and the string is printed to the screen.
4. We end the line with a semicolon (`;`), which indicates that this expression is over and the next one is ready to begin. Most lines of Rust code end with a semicolon.

## Compiling and Running Rust Programs

Rust programs are compiled into binary executables before they can be run. The Rust compiler is called `rustc`.

To compile a Rust program, you run the `rustc` command and pass it the name of the source file. For example, to compile a program called `main.rs`, you would run the following command:

```bash
$ rustc main.rs
```

This will compile the program and output a binary executable called `main`.

To run the compiled program, you can run the `./main` command. For example, to run the program called `main`, you would run the following command:

```bash
$ ./main
```

Rust is an ahead-of-time compiled language, which means that the executable can be run without having Rust installed.
