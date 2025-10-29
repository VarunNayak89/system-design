# 🧱 Go (Golang) — Structs and Interfaces

---

## 🧩 Structs in Go

Structs in Go are used to **group multiple fields into a single data type**.

### 🧠 Example: Defining a Struct

```go
type Trade struct {
    Symbol string   // Stock symbol
    Volume int      // Number of shares
    Price  float64  // Trade price
    Buy    bool     // true if buy trade, false if sell trade
}
```

### 🧩 Using Structs

```go
t1 := Trade{"MSFT", 10, 99.98, true}

t2 := Trade{
    Symbol: "MSFT",
    Volume: 10,
    Price:  99.98,
    Buy:    true,
}

t3 := Trade{} // defined struct with zero values

fmt.Println(t1.Symbol) // access field of struct by dot
```

---

## ⚙️ Methods in Structs

In Go, structs can have **methods**, but unlike C# or Java, methods are **declared outside the struct** with a **receiver**.

### 🧠 Example: Struct Method with Receiver

```go
func (t *Trade) Value() float64 {
    value := float64(t.Volume) * t.Price
    if t.Buy {
        value = -value
    }
    return value
}
```

Usage:

```go
fmt.Println(t2.Value())
```

---

## 🧭 Another Example: Struct with Method

```go
// Point is a 2D Point
type Point struct {
    X int
    Y int
}

// Move method modifies the Point coordinates
func (p *Point) Move(dx int, dy int) {
    p.X += dx
    p.Y += dy
}
```

Usage:

```go
p := Point{1, 2}
p.Move(5, 5)
fmt.Println(p.X, p.Y)
```

---

## 🧩 Interfaces in Go

An **interface** in Go is a **collection of method signatures**.  
A type satisfies an interface when it implements **all methods** declared in the interface — implicitly (no need to declare intent).

### 🧠 Example: Interface and Implementation

```go
type Shape interface {
    Area() float64
}

func sumAreas(shapes []Shape) float64 {
    total := 0.0
    for _, shape := range shapes {
        total += shape.Area()
    }
    return total
}

func main() {
    shape := []Shape{s, c}
    sa := sumAreas(shape)
    fmt.Println(sa)
}
```

> ✅ **Interfaces provide great abstraction** — they decouple behavior from implementation.

---

## 💡 Key Takeaways

- Structs combine fields into a single custom type.  
- Methods can be attached to structs using **receivers**.  
- Interfaces define behavior; any type that implements all interface methods satisfies it automatically.  
- Go achieves **polymorphism** without inheritance.

---
