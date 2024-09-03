# Конструктор в Go

```go
package main

import (
    "fmt"
)

// 1. Создадим структуру Rectangle
type Rectangle struct {
    length, width int
}

// 2. Создадим конструктор для Rectangle
// Для имен конструкторов в Go договорились использовать функцию с следующим названием:
// * New() если данный конструктор на файл один (в файле присутствует описание только одной структуры)
// * New<StructName>() - если в файле присутствуют еще какие-то структуры

// 3. В Go принято возвращать из конструктора не сам экземпляр, а ссылку на него
func New(newLength, newWidth int) *Rectangle {
    return &Rectangle{newLength, newWidth}
}

// 4. Добавим два метода
func (r *Rectangle) Perimeter() int {
    return 2 * (r.length + r.width)
}

func (r *Rectangle) Area() int {
    return r.length * r.width
}

func main() {
    r := New(10,20)
    fmt.Printf("Type as %T and Value %v\n", r, r) // Type as main.Rectangle and value {10,20}
    fmt.Println("Perimeter:", r.Perimeter()) // Perimeter: 60
    fmt.Println("Area:", r.Area()) // Area: 200
}
```
