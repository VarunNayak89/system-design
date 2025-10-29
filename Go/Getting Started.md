# 🐹 Go — Basic Program Structure (`welcome.go`)

---

## 📘 Example Code

```go
// print a friendly greeting

package main  // allow team to work on part of

import (
    "fmt"  // package for printing functions
)

func main() {  // define functions
    fmt.Println("welcome Go phers ")  // function with library name
    // no semicolon at end of line
}
```

---

## 💡 Key Notes

- **Comments:** Single line `//` or multi-line `/* ... */`  
- **Go Code Organization:** Code in Go is organized into **packages**  
- **Main Package:**  
  - Has a special meaning — it allows your code to **compile and execute**.  
  - Other packages cannot run directly.

---

## ⚙️ Commands

| Command | Description |
|----------|--------------|
| `go run welcome.go` | Run the Go program |
| `go build welcome.go` | Build the Go program |
| `./welcome` | Execute the compiled binary |
| `go help` | List available Go commands |

---
