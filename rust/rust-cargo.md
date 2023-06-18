# RUST: Cargo

- Cargo is Rust's build system and package manager.
- Cargo handles a lot of tasks for you, such as building your code, downloading the libraries your code depends on, and building those libraries.
- The simplest Rust programs don't have any dependencies, but as you write more complex Rust programs, you'll add dependencies.
- If you start a project using Cargo, adding dependencies will be much easier to do.
- Cargo comes installed with Rust if you used the official installers.
- If you installed Rust through some other means, you can check whether Cargo is installed by entering `cargo --version` in your terminal.

## Creating a Project with Cargo

To create a new project:

```
$ cargo new hello_cargo
```

This will create the following project structure:

```
hello_cargo/
├── Cargo.toml
├── .git
│   └── ...
├── .gitignore
└── src
    └── main.rs
```

- Cargo creates a new directory and project called `hello_cargo`
- The directory contains two files: `Cargo.toml` and `src/main.rs`
- The directory is also set up as a GIt repository
  - If you run `cargo new` within an existing Git repository, the Git files will not be generated
  - You can use the `--vcs` flag to change the version control system that Cargo uses (see `cargo --help` for more info)

`Cago.toml` contents:

```toml
[package]
name = "hello_cargo"
version = "0.1.0"
edition = "2021"

# See more keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html

[dependencies]
```

- The `Cargo.toml` file is a manifest file that contains information about the project, such as its name, version, and dependencies.
- The `name`, `version`, and `edition` keys are required in the `[package]` section.
- The `[dependencies]` section is optional.
- If the `[dependencies]` section is empty, the package does not depend on any other packages.

`src/main.rs` contents:

```rust
fn main() {
    println!("Hello, world!");
}
```

- Cargo has generated a `src/main.rs` file for us, which contains the `Hello, world!` program
- Cargo expects source files to live inside the `src` directory
- The top-level project directory is just for README files, license information, configuration files, and anything else not related to your code
- Using Cargo helps you organize your projects
- If you started a projectthat doesn't use Cargo, you can convert it to a project that does use Cargo by moving the project code into the `src` directory and creating an appropriate `Cargo.toml` file

## Building and Running a Cargo Project

- We can create a project using `cargo new`
- We can build a project using `cargo build`
- We can build and run a project in one step using `cargo run`
- We can build a project without producing a binary to check for errors using `cargo check`
- Instead of saving the result of the build in the same directory as our code, Cargo stores it in the `target/debug` directory

## Building for Release

- Cargo has two profiles: `dev` and `release`
- The `dev` profile is used for development, when you want to rebuild quickly and often
- The `release` profile is used for building the final program, which will run as fast as possible
- To build your project with optimizations, you can use the `cargo build --release` command
- This will create an executable in the `target/release` directory
- If you are benchmarking your code's running time, be sure to run `cargo build --release` and benchmark with the executable in `target/release`

## Cargo as Convention

- Cargo is a build system and package manager for Rust.
- Cargo is not necessary for simple projects, but it becomes more valuable as projects become more complex.
- Cargo helps to coordinate the build process and manage dependencies.
- To work on an existing Rust project, you can use the following commands:

```bash
$ git clone example.org/someproject
$ cd someproject
$ cargo build
```
