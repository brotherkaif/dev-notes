# GO: Create Module

## Prerequisites

- Some programming experience, a text editor, and a command terminal.

## Start a module that others can use

- Go code is grouped into packages
- Packages are grouped into modules
- Modules specify dependencies and the Go runtime required (in the `go.mod` file)

Create a `greetings` module:

```bash
$ mkdir greetings
$ cd greetings
$ go mod init example.com/greetings
go: create new go.mod: module example.com/greetings
```

**Note:** If you publish a module, the module path _must_ be a path from which your module can be downloaded by Go tools (i.e. a location on the internet).

Create a `greetings.go` file:

```go
package greetings

import "fmt"

// Hello returns a greeting for the named person.
func Hello(name string) string {
    // Return a greeting that embeds the name in a message.
    message := fmt.Sprintf("Hi, %v. Welcome!", name)
    return message
}
```

The above code does the following:

- Declare a greetings package to collect related functions.
- Implement a Hello function to return the greeting:
    - This function takes a `name` parameter whose type is `string`.
    - The function also returns a `string`.
    - **Note:** A function which starts with a capital letter can be called by a function not in the same package (i.e. an "Exported Name").
- Declare a `message` variable to hold your greeting:
    - **Note:** The `:=` operator is a shortcut for declaring and initialising a variable in one line.
    - The long way would be:
        - `var message string`
        - `message = fmt.Sprintf("Hi, %v. Welcome!", name)`
- Use the `fmt` package's `Sprintf` function to create a greeting message.
    - The first argument is a format string, and `Sprintf` substitutes the name parameter's value for the `%v` format verb.
    - Inserting the value of the name parameter completes the greeting text.
- Return the formatted greeting text to the caller.

---

#### References

- [Tutorial: Create a Go module](https://go.dev/doc/tutorial/create-module)
