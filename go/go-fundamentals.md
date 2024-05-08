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
### Arithmetic

```go
a,b := 10, 5        // Go allows multiple variables to be initialized at once!

c := a + b          // 15 - addition
c := a - b          // 5 - subtraction
c := a * b          // 50 - multiplication
c := a / b          // 2 - division
c := a / 3          // 3 - integer division used for integers
c := a % 3          // 1 - modulus (remainder of integer division)
d := 7.0 / 2.0      // 3.5 - decimal results given for floating point numbers
```

### Comparisons

```go
a,b := 10, 5

c := a == b         // false - equality
c := a != b         // true - inequality
c := a < b          // false - less than
c := a <= b         // false - less than or equal to
c := a > b          // true - more than
c := a >= b         // true - more than or equal to
```

### Constants

```go
const a = 42                        // constant (implicitly typed)
const b string = "hello, world"     // constant (explicitly typed)
const c = a                         // one constant can be assigned to another

const (                             // group of constants
    d = true
    c = 3.14
)

const (
    a = "foo"
    b                               // "foo" - unassigned constants receive previous value
)

const c = 2 * 5                     // constant expression
const d = "hello, " + "world"       // must be calculable at compile time
const e = someFunction()            // this won't work - can't be evaluated at compile time
```

Constant expressions are often combined with something called `iota`:

```go
const a = iota      // 0 - iota is related to position in constant group

const (
    b = iota        // 0 - iota starts at zero on first line
    c               // 1 - constant expression copied, iota increments
    d = 3 * iota    // 6 - iota increments again
)

const (
    e = iota        // iota resets to zero with each group
)
```

### Pointers and Values

```go
a := "foo"          // create a string variable
b := &a             // address operator returns the address of a variable

*b = "bar"          // dereference a pointer with asterisk
c = new(int)        // built-in "new" funtion creates pointer to anonymous variable
```

- Pointers are primarily used to share memory
- **Use copies whenever possible**

## Creating and Debugging Programs

### CLI Tools

The following packages are present in the Go [Standard Library](https://pkg.go.dev/std) and are very useful when designing CLI applications:

- [`os`](https://pkg.go.dev/os): Package `os` provides a platform-independent interface to operating system functionality.
    - `Stdin`: Allows us to read input from the standard input source (by default, the keyboard)
    - `Stdout`: Allows us to write to the standard output device (typically a monitor)
    - `Stderr`: Similar to `Stdout`, but it is a special channel specifically for errors
- [`fmt`](https://pkg.go.dev/fmt): Package `fmt` implements formatted I/O with functions analogous to C's `printf` and `scanf`.
    - `Scan*`: Allows us to read information in from various sources (including `Stdin`)
    - `Print*`: Allows us to write information out to various destinations (including `Stdout`)
- [`bufio`](https://pkg.go.dev/bufio): Package `bufio` implements buffered I/O. It wraps an io.Reader or io.Writer object, creating another object (Reader or Writer) that also implements the interface but provides buffering and some help for textual I/O.

### Example: Buildin a CLI Application

The following is a simple CLI application that takes input from the user via `Stdin` and returns it to `Stdout` in uppercase format.

```go
package main

import (
	"bufio"
	"fmt"
	"os"
	"strings"
)

func main() {
	fmt.Println("What would you like to scream?")
	in := bufio.NewReader(os.Stdin)
	s, _ := in.ReadString('\n')
	s = strings.TrimSpace(s)
	s = strings.ToUpper(s)
	fmt.Println(s + "!")
}
```

```
$ go run main.go
What would you like to scream?
make it stop
MAKE IT STOP!
```

### Web Services

At a very high level, **clients** make requests to **servers**. The **front controller** of the client is responsible for recieving request from the client, routing the request to the appropriate back controller and then passing the response back to the original client.

```
                             +-------------------------+
                             |                   SERVER|
                             |                         |
+----------+     request     |                         |
|          +-----------------|--->+----------------+   |
|  CLIENT  |                 |    |FRONT CONTROLLER|   |
|          |<----------------|----+-----------+----+   |
+----------+    response     |          ^     |        |
                             |          |     |        |
                             |          |     v        |
                             |   +------+---------+    |
                             |   |+---------------++   |
                             |   +|BACK CONTROLLERS|   |
                             |    +----------------+   |
                             |                         |
                             +-------------------------+
```

### Building a Web Service

- Go provides the **front controller** for us
- We need to implement the **back controllers**
- This **back controller** is just a function

```go
package main

import (
    "io"
    "net/http"
    "os"
)

func main() {
    // register the handler function as the back controller to the base endpont
    http.HandleFunc("/", Handler)

    // start the server on localhost:3000 and use the default front controller
    http.ListenAndServe(":3000", nil)
}

func Handler(w http.ResponseWriter, r *http.Request){
    f, _ := os.Open("./menu.txt")
    io.Copy(w, f)
}
```

### Aggregate Data Types

#### Array Types

Basics:

```go
var arr [3]int          // array of 3 ints
fmt.Println(arr)        // [0 0 0]
arr = [3]int{1, 2, 3}   // array literal

fmt.Println(arr[2])     // 2
arr[1] = 99             // update value
fmt.Println(arr)        // [1 99 3]
fmt.Println(len(arr))   // 3
```

Assignation:

```go
arr := [3]string{"foo", "bar", "baz"}

arr2 := arr                             // ARRAYS ARE COPIED BY VALUE!
fmt.Println(arr)                        // {"foo" "bar" "baz"}

arr[0] = "quux"
fmt.Println(arr)                        // {"quux" "bar" "baz"}
fmt.Println(arr2)                       // {"foo" "bar" "baz"}

arr = arr2                              // false - arrays are comparable
```
