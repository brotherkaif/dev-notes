# GO: Call Module Code

1. Create a `hello` directory for your Go module source code. You should have the following file structure:
```
.
├── greetings
└── hello

```

2. Enable depenendency tracking within the `hello` directory:
```bash
$ go mod init example.com/hello
go: creating new go.mod: module example.com/hello
```

3. Create a `hello.go` file with the following content:
```go
package main

import (
    "fmt"

    "example.com/greetings"
)

func main() {
    // Get a greeting message and print it.
    message := greetings.Hello("Gladys")
    fmt.Println(message)
}
```

---

#### References

- [Call your code from another module](https://go.dev/doc/tutorial/call-module-code)
