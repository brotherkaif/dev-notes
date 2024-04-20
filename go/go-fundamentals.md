# GO: Fundamentals

## Getting Up and Running

### Installing Go

* Use the [Download and Install](https://go.dev/doc/install) steps.

### Creating a Basic Program

#### Enable Dependency Tracking

To enable dependency tracking for your code by creating a `go.mod` file, run the `go mod init` command, giving it the name of the module your code will be in.

```bash
$ go mod init example/hello
go: creating new go.mod: module example/hello
```

#### Write Code

Write a `hello.go` file with the following code:

```go
// declare a main package
package main

// import the popular fmt package
import "fmt"

// implement a main function to print a message to the console
// a main function executes by default when you run the main package
func main() {
    fmt.Println("Hello, World!")
}
```

#### Run Code

```bash
$ go run .
Hello, World!
```

#### Importing Packages

In your Go code, import the `rsc.io/quote` package and add a call to its Go function.

```go
package main

import "fmt"

import "rsc.io/quote"

func main() {
    fmt.Println(quote.Go())
}

```

Add new module requirements and sums.

```bash
$ go mod tidy
go: finding module for package rsc.io/quote
go: found rsc.io/quote in rsc.io/quote v1.5.2
```

The `go mod tidy` command will locate and download the `rsc.io/quote` module. Run the code.

```bash
$ go run .
Don't communicate by sharing memory, share memory by communicating.
```

## Variables and Simple Data Types

### Simple Data Types

Data types that contain one and only one value.

- Strings
- Numbers
- Booleans
- Errors

### Strings

Strings in Go represent a collection of one or more UTF8 codepoints. They come in two flavours, **Interpreted Strings** and **Raw Strings**.

```go
"this is a string" // interpred string (double quotes)

`this is also a string` // raw string (backticks)

"this is an escape character: \n it creates a newline"
this is an escape character:
 it creates a newline

`this is an escape character: \n it creates a newline`
this is an escape character: \n it creates a newline

`raw strings
ignore new lines`
raw strings
ignore new lines
```

### Numbers

**Signed Integers:**
`int`: Whole numbers can represent both positive and negative values. For example, `99`, `0`, `937`.

**Unsigned Integers:**
- `uint`: Whole numbers and can only represent positive values. For example, `0`, `15`, `7329`.

**Floating Point Numbers:**
- `float32`: A 32-bit floating point number. For example, `6.02e23`, `3.1415`, `0.25`.
- `float64`: A 64-bit floating point number. It is the default floating point number type. For example, `6.02e23`, `3.1415`, `0.25`.

- **Complex Numbers:**
- `complex64`: A 64-bit complex number and comprises of a "real" component and an "imaginary" component. For example, `1 + 2i`, `0.833i`, `6.02e23 + 3.1415i`.
- `complex128`: A 128-bit complex number. It is the default complex number type. For example, `1 + 2i`, `0.833i`, `6.02e23 + 3.1415i`.

### Booleans

The simplest data type in programming, it represents `true` or `false`.

### Error

The `error` built-in interface type is the conventional interface for representing an error condition, with the `nil` value representing no error.

```go
type error interface {
    Error() string
}
```

### Finding Documentation for Built-in Types

- [Standard Library](https://pkg.go.dev/std): Documentation on all of the packages available in the Go Standard Library
- [builtin Documentation](https://pkg.go.dev/builtin): Documentation only package (as builtins do not need to be imported like other packages)

### Declaring Variables

There are 3 different ways to declare variables in Go:

```go
var myName string                   // declare variable
var myName string = "Samus Aran"    // declare and initialize

var myName = "Samus Aran"           // initialise with inferred type (rarely used, see below)
myName := "Mike"                    // short declaration syntax (more commonly used)
```

### Type Conversions

Go has a founding priciple of _being clear over being clever_.

```go
var i int = 32
var f float32

f = i           // error! - Go doesn't support implicit conversions
f = float32(i)  // type conversions allow explicit conversion
```
