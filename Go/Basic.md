# 🧮 Go (Golang) — Numbers, Conditions, Loops, Strings, Arrays & Maps

---

## 🔢 Numbers

- Go doesn’t allow adding **int** with **float**.  
- If not initialized, int variables have a **zero value (0)**.  
- Two floating-point types: **float32** and **float64**.  
- `%v` shows the value, `%T` shows the type.  
  Example:  
  ```go
  fmt.Printf("x=%v type of %T\n", x, x)
  ```  
- Variable declaration can be done in two ways:
  - `var x float64`
  - `x := 1.0`  
- Assign two variables in a single line:  
  ```go
  x, y := 1.0, 2.0
  ```
- Declaring a variable but not using it causes a **compile-time error**.

---

## ⚙️ Condition: if & switch case

- No parentheses needed around conditions (e.g., `if x > 5`).  
- Logical AND: `&&`, Logical OR: `||`.  
- Use `;` to separate multiple statements in one line:  
  ```go
  if frac := a / b; fac > 5 {
  }
  ```
- Switch cases don’t require `break`. Case values can be **strings** or **integers**.  
- Switch without a condition — conditions inside `case` blocks.  

Example 1:
```go
switch x {
case 1:
  fmt.Println("One")
case 2:
  fmt.Println("Two")
}
```

Example 2:
```go
switch {
case x > 100:
  fmt.Println("Large")
case x > 10:
  fmt.Println("Medium")
}
```

---

## 🔁 For Loop

- No parentheses for `for` loops (`for i := 0; i < 3; i++ {}`).  
- `break` and `continue` work as in C#.  

### Example 1: For with condition (same as `while`)
```go
a := 0
for a < 3 {
  fmt.Println(a)
  a++
}
```

### Example 2: Infinite for (like `while true`)
```go
b := 0
for {
  if b > 2 {
    break
  }
  fmt.Println(b)
  b++
}
```

---

## 🔤 String

- Example:  
  ```go
  book := "The Colour of Magic"
  ```  
- `len(book)` → returns string length.  
- Access individual character → `book[0]`.  
- Strings are **immutable** — can’t be changed after creation (`book[0] = 119` gives error).  
- Slicing strings:  
  ```go
  book[4:11]  // "colour"
  book[4:]    // "colour of magic"
  book[:4]    // "The "
  ```  
- Concatenate using `+`: `"T" + book[1:]`  
- Multiline string with backticks:  
  ```go
  `This
  is
  multiline`
  ```  
- Convert number to string:  
  ```go
  s := fmt.Sprintf("%d", n)
  ```  
- Print string with type:  
  ```go
  fmt.Printf("s=%s (type %T)\n", s, s)
  ```

---

## 🧱 Array & Slice

- Go has **arrays**, but **slices** are more commonly used.  
- Slice = sequence of items of the same type.  

### Example:
```go
loons := []string{"bugs", "daffy", "taz"}
fmt.Println(len(loons)) // 3
fmt.Println(loons[1])   // "daffy"
fmt.Println(loons[1:])  // from index 1 to end
```

### Iteration examples:

**Without range:**
```go
for i := 0; i < len(loons); i++ {
  fmt.Println(loons[i])
}
```

**With range (just value):**
```go
for _, name := range loons {
  fmt.Println(name)
}
```

**With index and value:**
```go
for i, name := range loons {
  fmt.Printf("%s at %d\n", name, i)
}
```

**Append to slice:**
```go
loons = append(loons, "elmer")
```

---

## 🗺️ Map (Key-Value Pairs)

- All keys must have the same data type; all values must have the same type.  

### Example:
```go
stocks := map[string]float64{
  "AMZN": 1699.8,
  "GOOG": 1129.19,
  "MSFT": 98.61, // trailing comma required in multi-line
}
```

### Map Operations:
```go
len(stocks)          // get total keys
stocks["MSFT"]       // get a value
stocks["TSLA"]       // returns 0 if key not found

value, ok := stocks["TSLA"]
if !ok {
  fmt.Println("Key not found")
}

stocks["TSLA"] = 322.12   // set a new value
delete(stocks, "AMZN")    // delete a key

for key := range stocks {
  fmt.Println(key)
}

for key, value := range stocks {
  fmt.Printf("%s -> %.2f\n", key, value)
}
```

### Create Empty Map:
```go
count := map[string]int{}
```

### String Split Example:
```go
words := strings.Fields(text) // ignores whitespace and splits string
```

---

## 💻 Example Code: Numbers.go

```go
package main

import "fmt"

func main() {
  x, y := 1.0, 2.0  // declare variables
  fmt.Printf("x=%v type of %T\n", x, x)
  fmt.Printf("y=%v type of %T\n", y, y)

  var mean float64
  mean = (x + y) / 2  // convert to float
  fmt.Printf("result: %v, type of %T\n", mean, mean)
}
```

---
