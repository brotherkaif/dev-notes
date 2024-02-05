# GO: Getting Started

## Prerequisites

* Some programming experience, a text editor, and a command terminal.

## Install Go

* Use the [Download and Install](https://go.dev/doc/install) steps.

## Enable Dependency Tracking

To enable dependency tracking for your code by creating a `go.mod` file, run the `go mod init` command, giving it the name of the module your code will be in.

```bash
$ go mod init example/hello
go: creating new go.mod: module example/hello
```

## Write Code

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

## Run Code

```bash
$ go run .
Hello, World!
```

## Importing Packages

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

```go
$ go run .
Don't communicate by sharing memory, share memory by communicating.
```
