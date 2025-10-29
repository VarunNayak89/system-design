# 🧩 Go (Golang) — Functions and Interfaces

---

## 🧠 Function Basics

Functions in Go are defined using the **`func`** keyword followed by the function name, parameters, and return type.

### ✳️ Basic Function Definition

```go
func add(a int, b int) int {
    return a + b
}
```
Usage:
```go
val := add(1, 2)
```

---

## 🔁 Multiple Return Values

Go functions can return **more than one value**.

```go
func divmod(a int, b int) (int, int) {
    return a / b, a % b
}
```
Usage:
```go
div, mod := divmod(7, 2)
```

---

## 🧷 Pass by Reference (Pointers)

- Go passes **integers by value** (a copy).  
- To pass a value **by reference**, use a **pointer (`*`)**.

Example:
```go
func doubleptr(n *int) {
    *n *= 2
}
```
Usage:
```go
doubleptr(&val) // pass address of value
```

---

## ⚠️ Returning Errors from Functions

Go can return **multiple values**, which allows returning both a result and an **error**.

Example:
```go
func sqrt(n float64) (float64, error) {
    if n < 0 {
        return 0.0, fmt.Errorf("sqrt of negative number %f", n)
    }
    return math.Sqrt(n), nil
}
```

Usage:
```go
s1, err := sqrt(2.0)
if err != nil {
    fmt.Println(err)
}
```

---

## 🧹 Memory Management and `defer`

Go has a **garbage collector**, so you don’t need to manually manage memory.  
However, for **resource cleanup**, Go provides the **`defer`** keyword.

### 🔑 Defer Usage
- Runs **after** the surrounding function completes.  
- Used to **release resources** like files, connections, etc.  
- `defer` statements are executed in **LIFO order (last-in-first-out)**.

Example:
```go
func cleanup(name string) {
    fmt.Printf("Cleaning up %s\n", name)
}

func worker() {
    defer cleanup("A") // executed last
    defer cleanup("B") // executed first
    fmt.Println("Start running worker")
}
```

Output:
```
Start running worker
Cleaning up B
Cleaning up A
```

---

## 🧩 Interface in Go

An **interface** is a collection of method signatures.  
A type satisfies an interface **implicitly** if it implements **all methods** with matching names, parameters, and return types.

Example:
```go
type Shape interface {
    Area() float64
    Perimeter() float64
}

type Circle struct {
    Radius float64
}

func (c Circle) Area() float64 {
    return math.Pi * c.Radius * c.Radius
}

func (c Circle) Perimeter() float64 {
    return 2 * math.Pi * c.Radius
}

// Usage
func printShapeInfo(s Shape) {
    fmt.Printf("Area: %.2f, Perimeter: %.2f\n", s.Area(), s.Perimeter())
}
```

---
