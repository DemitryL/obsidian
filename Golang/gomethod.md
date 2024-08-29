# Methods in Go

```go
package main

import (
  "fmt"
  "math"
)

type Employee struct {
  name string
  position string
  salary int
  currency string
}

// 1. Методы - функции, привязанные к определенном структурам
// func (s Struct) MethodName(parameters type) type {}
//      Resiever - получатель метода
func (e Employee) DisplayInfo(){
  fmt.Println("Name:", e.name)
  fmt.Println("Position:", e.position)
  fmt.Printf("Salary : %d %s\n", e.salary, e.currency)
}

func main() {
  emp := Employee{
    name: "Bob",
    position: "Middle Golang developer",
    salary: 3000,
    currency: "USD",
  }
  // 2. Вызов метода
  emp.DisplayInfo()
}
```

# 3. В чем преимущество методов над функциями

```go
// Во-первых: наличие методов улучшает "консистеность" кода, т.к. напрямую влияет на его понимание.
// Во-вторых: в Go запрещается создавать функции с одинаковыми названиями, в то время как методы для разных стуктур,
// с одинаковыми названиями - разрешины.

type Circle struct {
  radius float64
}

type Rectangle struct {
  length, width int
}

// 4. Создадим функцию и метод Perimeter для структуры Circle
func Perimeter(c Circle) float64 {
  return c.radius * 2 * math.Pi
}

func (c Circle) Perimeter() float64 {
  return c.radius * 2 * math.Pi
}

// 5. Создадим фукцию и метод Perimeter для структуры Rectangle
func (r Rectangle) Perimeter() int {
  return 2 * (r.length + r.width)
}

// 6. В Go разрешено создавать методы с одинаковыми именами в пределах одной структуры. Главное чтобы
// получатель метода в разных структурах (где реализован метод со схожим именем) отличался.
func PerimeterRectangle(r Rectangle) int {
    return 2 * (r.length + r.width)
}

func main() {
  c := Circle{10.5}
  fmt.Println("Call function:", Perimeter(c))
  fmt.Println("Call Method:", c.Perimeter())

  r := Rectangle{10,20}
  fmt.Println("Call function for rectangle:", PerimeterRectangle(r))
  fmt.Println("Call method for rectangle:", r.Perimeter())
}
```
