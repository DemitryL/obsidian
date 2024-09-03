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

## Получение ресивера по значению или по указателю

```go
package main

import (
    "fmt"
)

type Employee struct {
    name string
    salary int
}

// 1. Метод в котором получатель копируется и в его теле происходит работа с локальной копией
func (e Employee) SetName(newName string) {
    e.name = newName
}

// 2. Метод в котором получатель передается по ссылке (в теле метода работаем с ссылкой на экземпляр)
func (e *Employee) SetSalary(newSalary int) {
    e.salary = newSalary
}

// 4. Используйте методы с PointerReciever'ом в ситуациях когда:
//   1) Изменения в работе метода над экземпляром должны быть видны на вызывающей стороне
//   2) Когда экземпляр достаточно "увесистый", то есть копировать его дорого с точки зрения расходов ресурсов
//   3) С ними может рабртать любой вид экземпляра


func main() {
  e := Employee{"Alex", 3000}
  fmt.Println("Before setting parameters:", e)
  e.SetName("Bob")
  fmt.Println("After SetName call:", e)
  e.SetSalary(4500) // 3. Вызов метода у ссылки на сотрудника
  // 5. Аналогично явному вызову (&e).SetSalary(4500)
  fmt.Println("After SetSalary call:", e)
}
```

## Перенос методов | ООП - метод наследования

```go
package main

import (
    "fmt"
)

type University struct {
    city string
    name string
}

// 1. Данный метод явно связан только с структурой University
func (u *University) FullInfoUniversity() {
    fmt.Printf("Uni name: %s and City: %s\n", u.name, u.city)
}

// 2. В структуру Professor встоены поля структуры University (переходят все методы тоже)
type Professor struct {
    fullName string
    age int
    University
}

func main() {
  p := Professor{
        fullName: "Boris Bobroff",
        age: 150,
        University: University{
            city: "Moscow",
            name: "BMSTU",
        }
    }
    // 3. Вызываем метод структуры University через экземпляр профессора
    p.FullInfoUniversity()  // Uni name: BMSTU and City: Moscow
}
```

## Передоча параметров по ссылкам и по значению с точки зрения сравнения методов

```go
package main

import (
    "fmt"
)

type Rectangle struct {
    length, width int
}

// 1. Реализуем функцию и метод для подсчета периметра прямоугольника
// ВАЖНО: все параметры передаем как копии

// 4. При вызове этого метода неважно, будет ли он вызваться у экземпляра или у его ссылки
// METHOD
func (r Rectangle) Perimeter() int {
    return 2 * (r.length + r.width)
}

// 5. Данную функцию можно вызвать ТОЛЬКО у копии прямоугольника (но не у его ссылки)
// FUNCTION
func (r Rectangle) int {
    return 2 * (r.length + r.width)
}

// 6. Допустим будет метод который меняет значение состояния структуры на новое, но этот метод - Value Reciever
func (r Rectangle) SetLength(newLegth int) {
    r.length = newLegth
}

func main() {
  // 2. Создаем экземпляр прямоугольника
  rectangleAsValue := Rectangle{10, 10}
  fmt.Println("Call function for rectangleAsValue:", Perimeter(rectangleAsValue)) // 40
  fmt.Println("Call method for rectangleAsValue:", rectangleAsValue.Perimeter())  // 40

  // 3. Создадим указатель на прямоугольник
  rectangleAsPointer := &rectangleAsValue
  fmt.Println("Call method for rectangleAsPointer:", rectangleAsPointer.Perimeter()) // 40
  // Perimeter(rectangleAsPointer) - Иллюстрация к пункту 5

  // 7. Вызываем метод SetLength у экземпляра rectangleAsValue
  fmt.Println("Before call method SetLength:", rectangleAsValue) // {10, 10}
  rectangleAsValue.SetLength(9999)
  fmt.Println("After call method SetLength:", rectangleAsValue) // {10, 10}

  // 8. Вызываем метод SetLength у ссылки на rectangleAsValue
  rectangleAsPointer.SetLength(999999)
  fmt.Println("After call method SetLength for &rectangle:", *rectangleAsPointer) // {10, 10}
}
```

## Передоча параметров по ссылкам и по значению с точки зрения сравнения методов. ЧАСТЬ 2

```go
package main

import "fmt"

type Rectangle struct {
    length, width int
}

// METHOD
func (r *Rectangle) Area() int {
    return r.length * r.width
}

//FUNTION
func Area(r *Rectangle) int {
    return r.length * r.width
}

//METHOD
func (r *Rectangle) SetWidth(newWidth int) {
    r.width = newWidth
}

func main() {
  // Значение исходное
  rectangleAsValue := Rectangle{10, 10}
  // Ссылка на исходное значение
  rectangleAsPointer := &rectangleAsValue
  fmt.Println("Call Area function for &rectangle:", Area(rectangleAsPointer)) //100
  fmt.Println("Call Area method for &rectangle:", rectangleAsPointer.Area())  //100
  // 1. Вызов метод у value - исходного значения
  fmt.Println("Call Area method for rectangle:", rectangleAsValue.Area())  //100

  // 2. Вызываем функцию с параметром value - исходное значение
  //Area(rectangleAsValue)

  // 3. Распичатаем исходный прямоугольник
  fmt.Println("Before changing width:", rectangleAsValue) // {10, 10}

  // 4. Вызываем метод SetWidth у &rectangle
  rectangleAsPointer.SetWidth(999)
  fmt.Println("After change via method SetWidth for &rectangle:", rectangleAsValue) // {10, 999}

  // 5. Вывод метода SetWidth у rectangle
  rectangleAsValue.SetWidth(888)
  fmt.Println("After change via method SetWidth for rectangle:", rectangleAsValue) // {10, 888}
}
```

## Методы для стандартных типов

```go
package main

import "fmt"

// 1. Методы для стандартных типов
// В Go встроено куча приметивов (int, int32, string, bool...)
// Что если хочется дописать к стандартному типу какой-то метод?

// 2. Наивная попытка. Это невыполнимо. Компилятор запрещает добавление новых методов к существующим базовым типам
//func (a *int) IsEven() bool {
    //if *a % 2 == 0 {
        //return true
    //}
    //return false
//}

// 3. Но мне очень хочется, что делать?
// Создайте новый тип - ваш int и делайте с ним что хотите!
// Для создания нового типа используют конструкцию 
type MySuperDuperInt int 

// METHOD
func (msdi *MySuperDuperInt) IsEven() bool {
    if *msdi % 2 == 0 {
        return true
    }
    return false
}


func main() {
    num1 := MySuperDuperInt(202)
    num2 := MySuperDuperInt(201)
    fmt.Println(num1.IsEven())  // true
    fmt.Println(num2.IsEven())  // false
    // 4. Внутренние преобразования
    // var num3 MySuperDuperInt = MySuperDuperInt(10)
    // var num4 int = int(num3)
}
```
