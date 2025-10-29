# 🐹 Go (Golang) Basics — Println vs Printf

---

**Link:** [Go Essential Training (LinkedIn Learning)](https://www.linkedin.com/learning/go-essential-training-2018/challenge-server-kill?autoplay=true&resume=false)  
**IDE:** [Atom.io](https://atom.io/)

**Scheduling in Go:** [ArdanLabs Blog — Scheduling in Go](https://www.ardanlabs.com/blog/2018/08/scheduling-in-go-part1.html)

---

## 🖨️ Println vs Printf

- `fmt.Print` and `fmt.Println` print raw strings (`fmt.Println` appends a newline).  
- `fmt.Printf` does **not** print a newline automatically — you must add `\n` manually.  
- `fmt.Printf` works by supplying a **format string** with symbols that are replaced by arguments.  

Example:
```go
fmt.Printf("%s is cool", "Bob")
```
- In this case, `%s` represents a **string**.  
- `%T` prints the **type** of a variable.

---

### Example

```go
fmt.Println("Value of Pi :", math.Pi)
fmt.Printf("Value of Pi : %g", math.Pi)
```

**Expected Output:**

```
Value of Pi : 3.141592653589793
Value of Pi : 3.141592653589793
```

---

## 🧠 Things to Remember

- In Go, **identifiers that start with an uppercase letter** are **exported** (accessible from other packages).  
- Identifiers that start with a **lowercase letter** are **package-private** — only accessible within the current package.

---
