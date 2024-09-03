# Интерфейсы в GO

```go
package main

import "fmt"

// 0. Структура - это явно деклариванный заименованный набор СОСТОЯНИЙ.
// Структура исходя из своего описания, отвечает на вопрос - из чего я должен состоять,
// чтобы считаться тем ТИПОМ, который декларируется структурой
// Структура описывает ПАТТЕРН СОСТОЯНИЯ.

// 1. Интерфейсы - явно декларируемый набор сигнатур ПОВЕДЕНИЙ (чаще всего в виде набора методов), удовлетворив который
// можно считаться типом, который декларирует интерфей.
// Интерфесы в Go декларируют ПОЛУ-АБСТРАКТНЫЙ тип.
// Отвечает на вопрос что я должен УМЕТЬ ДЕЛАТЬ, чтобы считаться тем ТИПОМ, который декларирует интерфейс.
// Интерфейс - описывает ПАТТЕРН ПОВЕДЕНИЯ.

// 2. Обьявление интерфейса
type FigureBuilder interface {
  // Набор сигнатур методов, которые необходимо реализовать в структуре-претенденте
  // Во-первых, у предендента должен быть метод Area() возвращающий int
  Area() int
  // Во-вторых, у преденденте должен быть метод Perimeter() возвращающий int
  Perimeter() int
}

// 3. Декларируем претендентов
// 3.1 Первый претендент - это прямоугольник
// У него есть два метода -
// Area() int
// Perimeter() int
// Когда эти методы реализованы, говорят, что RECTANGLE УДОВЛЕТВОРЯЕТ УСЛОВИЯ ИНТЕРФЕЙСА FigureBuilder
// RECTANGLE РЕАЛИЗУЕТ ИНТЕРФЕЙС FigureBuilder
type Rectangle struct {
    length, width int
}

func (r Rectangle) Area() int{
    return r.length * r.width
}

func (r Rectangle) Perimeter() int{
    return 2 * (r.length + r.width)
}

// 3.2 Второй претендент - это окружность
// У неe есть два метода -
// Area() int
// Perimeter() int
// Когда эти методы реализованы, говорят, что CIRCLE УДОВЛЕТВОРЯЕТ УСЛОВИЯ ИНТЕРФЕЙСА FigureBuilder
// CIRCLE РЕАЛИЗУЕТ ИНТЕРФЕЙС FigureBuilder
type Circle struct {
    radius int
}

func (c Circle) Area() int{
    return 3 * c.radius * c.radius
}

func (c Circle) Perimeter() int {
    return 2 * 3 * c.radius
}

func main() {
    // 4. Создадим по 3 экземпляра
    r1 := Rectangle{10, 20}
    r2 := Rectangle{30, 50}
    r3 := Rectangle{1, 1}
    c1 := Circle{5}
    c2 := Circle{10}
    c3 := Circle{15}

    // 5. Пдсчитаем общую площадь этих фигур
    rectangles := []Rectangle{r1, r2, r3}
    totalSumAreaOfRectangles := 0
    for _, rect := range rectangles {
        totalSumAreaOfRectangles += rect.Area()
    }

    circles := []Circle{c1, c2, c3}
    totalSumAreaOfCircles := 0
    for _, circ := range circles {
        totalSumAreaOfCircles += circ.Area()
    }

    fmt.Println("Total area is:", totalSumAreaOfRectangles + totalSumAreaOfCircles)

    // 6. Теперь воспользуемся интерфейсом указанным выше
    figures := []FigureBuilder{r1, r2, r3, c1, c2, c3} // Обьявляю слайс экземпляров, удовлетворяющих интерфейсу FigureBuilder
    // C другой стороны, кажется, что это слайс - каких-то определенных типов

    // 7. Подсчитаем общую площадь
    total := 0
    for _, fig := range figures {
        total += fig.Area()
    }
    fmt.Println("Total area:", total)
    // 8. Пояснение - так как каждый экземпляр удовлетворяет интерфейсу FigureBuilder (обьявляющий пол-абстрактный тип)
    // у каждого из слайса figures можно 100% вызвать метод Area() (который точно вернет int), или Perimeter()
    // который тоже 100% вернет int
}
```

## Более детально

```go
package main

import (
    "fmt"
    "unicode/utf8"
)

// 1. Описание интерфейса (описание того что должен уметь претендент)
type BigWord interface {
    IsBig() bool
}
// 2. Наш претендент которого надо научить делать IsBig() bool
type MySuperString string

// 3. Реализация IsBig() у претендента MySuperString
func (mss MySuperString) IsBig() bool {
    if utf8.RuneCountInString(string(mss)) > 10 {
        return true
    }
    return false
}

func main() {
    sample := MySuperString{"fgdfgsgvbdfg"}
    var interfaceSample BigWord // Обьявление переменной, типа интерфейса BigWord
    interfaceSample = sample // Присваивание значения для переменной типа BigWord возможно,
    // потому что sample (типа MySuperString) удовлетворяет интерфейсу BigWord
    fmt.Println("IsBig?", interfaceSample.IsBig()) // true

    // 4. Попытка присвоить значение с типажом, неудовлетворяющим интерфейсу
    //var interfaceBadSample BigWord
    //interfaceBadSample = "asdsce" // Тип string не имеет реализации метода IsBig, поэтому не удовлетворяет интерфейсу
}
```

```go
package main

import (
    "fmt"
)

// 1. Обьявляем интерфейс, декларирующий поведенчиский -паттерн (набор методов под реализацию)
type Worker interface {
    Work()
}

// 2. Обьявляем структуру. Данная структура - претендент на удовлетворение интерфейса Worker
type Employee struct {
    name string
    age int
}

// 3. Реализуем метод Work(), чтобы структура Employee удовлетворяла интерфейсу Worker
func (e Employee) Work() {
    fmt.Println("Now Employee with name", e.name, "is working!")
}

// 4. A давайте создадим функцию, которая будет принемать аргументы типа Worker и что-то с ними делать
func Describer(w Worker) {
    fmt.Printf("Interface with type %T and value %v\n", w, w)
}

// 6. Обьявление структуры. Данная структура - второй претендент на удовлетворение интерфейса Worker
type Student struct {
    name string
    coursNumber int
}

func (s Student) WantToEat() {
    fmt.Println("Student with name", s.name, "want to eat!")
}

func (s Student) Work() {
    fmt.Println("Student with name", s.name, "isworking")
}

func main() {
    // 5. Создадим экземпляр Employee
    emp := Employee{"Bob", 34}
    var workerEmployee Worker = emp // Присвоение в переменную типа Worker
    workerEmployee.Work() //Bob
    // В результате видим, что тип интерфейса определяется структурой его реализующей,
    // а значение интерфейса - это соответственно значение состояний структуры
    Describer(workerEmployee) // main.Employee {Bob 34}

    // 7. Создадим экземпляр Student
    std := Student{"Mike", 19}
    var workerStudent Worker = std
    workerStudent.Work()
    Describer(workerStudent) // Принял внутренний тип Student, а значение - равно значению полей экземпляра

    // 8. Создадим набор тех кто уже умеет Work(
    var workers []Worker - []Worker{workerStudent, workerEmployee}
    for _, worker := range workers {
        Describer(worker) // Данная функция вызывается у разных экземпляров благодаря тому, кто для ее вызова
        // экземпляру нужно удовлетворить некому контракту (поведеннческому патерну) если структура экземпляра поддерживает
        // данный параметр - то у экземпляра 100% можно вызвать все необходымые для этого метода
    }
    )
}
```

```go
package main

import "fmt"

// 1. А что если создать интерфейс, в котором в принципе нет никаких требований к поведению
type Empty interface {
}

// 2. Вопрос - кто удовлетворяет этому интерфейсу? Если интерфейс пустой - то ему удовлетворяет вообще кто угодно

// 3. Реализуем функцию, которая может принемать кого угодно
func Describer(pretendent interface{}) {
    fmt.Printf("Type = %T and value %v\n", pretendent, pretendent)
}

type Student struct {
    name string
}

// 4. Type Assertion
func SemiGeneric(pretendent interface{}) {
    val, ok := pretendent.(int) // Пытаюсь проверить что претендент типа int
    fmt.Println("Value:", val, "OK:", ok)
}

func main() {
    strSample := "Hello word"
    // 4. Передача параметра без присваивания в промежуточную переменную
    Describer(strSample)

    intSample := 200
    Describer(intSample)

    Describer(Student{"Vova"})

    // 5. Работа с полу-джинериком
    SemiGeneric(10)
    SemiGeneric(Student{"Feday"})
    SemiGeneric("Hello world")
}
```

## Свитч

```go
package main

import "fmt"

func DoSomething(pretendent interface{}) {
    switch pretendent.(type) { // Пытаемся извлечь нижележащий тип
    case string:
        fmt.Println("This is string")
    case int:
        fmt.Println("This is int")
    default:
        fmt.Println("Unknow type But i'm working!")

    }
}

func main() {
    DoSomething(10)
    DoSomething("Hello world")
    DoSomething(func(a, b int) int {return a + b})
}
```

## Next interface in Go

```go
package main

import "fmt"

//INTERFACE
type Describer interface {
    Describe()
}

//STRUCT
type Student struct{
    name string
    age int
}

//METHOD
func (std Student) Describe() {
    fmt.Printf("%s and %d y.o.\n", std.name, std.age)
}

func TypeFinder(i interface{}) {
    switch v := i.(type) { // Присвоим переменной v значение лежащие под предпологаемым интерфейсом
    case string:
        fmt.Println("This is string")
    case int:
        fmt.Println("This is int")
    case Describer: // Вывод - с типом интерфейса можно сравниватся точно также как и с любым другим типажем языка
        // это как раз и говорит о том что интерфейсы - полу-абстрактные типы.
        fmt.Println("I'm describer")
        v.Describe()
    default:
        fmt.Println("Unknow type")
    }
}

func main() {
    std := Student{"Alex", 23}
    TypeFinder(10)
    TypeFinder("Hello")
    TypeFinder(nil)
    TypeFinder(std)
}
```

## Чуствительны ли интерфейсы к valueType and pointerType in methods

```go
package main

import "fmt"

// 0. В Go принято называть интерфейсы с окончанием на 'er' (Describer, Worker, Pooler ...)
type Describer interface {
    Describe()
}

// STRUCT
type Student struct {
    name string
    age int
}
//METHOD
func (std Student) Describe() {
    fmt.Printf("Student name: %s and age %d\n", std.name, std.age)
}

// STRUCT
type Professor struct {
    name string
    age int
}
//METHOD
func (prof *Professor) Describe() {
    fmt.Printf("Professor name: %s and age %d\n", prof.name, prof.age)
}

func main(){
    var descr1 Describer
    stud1 := Student{"Alex", 23}
    descr1 = stud1 //Student реализует интерфейс Describer
    descr1.Describe()

    stud2 := &Student{"Bob, 21"} // Поскольку экземпляр -ссылка, разыименовать ее  имеет право кто угодно (в том числе  и компелятор)
    descr1 = stud2
    descrl.Describe()

    var descr2 Describer
    prof1 := &Professor{"Viktor Wann", 72}
    descr2 = prof1 //&Professor реализует интерфейс Describer
    descr2.Describe()

    prof2 := Professor{"Bob Brown", 62}
    prof2.Describe() // Здесь ссылку на &prof2 берет компилятор
    descr2 = prof2 // Professor не реализует интерфейс Describer
    // Дело в том, что сам по себе интерфейс - не референсный тип
    // Выливается это в следующее следствие:
    // Когда мы работаем с обычным методом, то взять референс на экземпляр может компилятор
    // Но когда мы пытаемся сделать это через интерфейс - в нем в принципе компилятор не видит никаких ссылок
}
```

## Интерфейсы (с точки зрения ООП)

```go
package main

import "fmt"

// 0. Интерфейсы (с точки зрения ООП) -Увеличивают уровень абстракции вашего кода
// Засчет увеличения уровня абстракции - можно решать много сторонних проблем, связанных с поддержкой
// пониманием и реюзабельностью кода.
// С другой стороны добавление интерфейсов не решают проблему уменьшения обстракности.

// 1. Что делать, если хочется скестить 2 интерфейса и создать единый уровень абстракции в коде?
type PerimeterCalculator interface {
    Perimeter() int
}

type AreaCalculator interface {
    Area() int
}

// 2. Соберем новый инрефейс из двух старых
type FigureFeatureCalculator interface {
    // Встраеваим интерфейсы
    PerimeterCalculator
    AreaCalculator

    // Наслуедование интерфейсов
    // Perimeter() int
    // Area() int
}

//STRUCT
type Rectangle struct {
    a, b int
    color string
}

// 2. Реализуем интерфейс PerimeterCalculator
func (r Rectangle) Perimeter() int {
    return 2 * (r.a + r.b)
}

// 3. Реализуем второй интерфейс AreaCalculator
func (r Rectangle) Area() int {
    return r.a * r.b
}

func main() {
    var pCalc PerimeterCalculator
    var aCalc AreaCalculator
    rect := Rectangle{10, 20, "green"}
    pCalc = rect //Структура Rectangle удовлетворяет интерфейсу PerimeterCalculator
    fmt.Println("Perimeter:", pCalc.Perimeter())

    aCalc = rect  // Структура Rectangle удовлетворяет интерфейсу AreaCalculator
    fmt.Println("Area:", aCalc.Area())

    var ffcalc FigureFeatureCalculator
    ffcalc = rect // Структура Rectangle удовлетворяет FigureFeatureCalculator
    fmt.Println(ffcalc.Area())
    fmt.Println(ffcalc.Perimeter())
}
```

## zval

```go
package main

import "fmt"
// 0. Почему интерфейс - полу-абстрактный тип в Go?

// 1. Создадим интерффейс езделка
type Rider interface {
    Ride()
    Gas()
    Stop()
}

func main() {
    // 2. Создаю экземпляр ездилки.
    var r Rider // ZeroValue - nil, ZeroType - nil
    if r == nil { // Попробует сравнить с nil
        fmt.Printf("r is nil. Value %v and type %T\n", r, r)
    }

    r.Ride() // Здесь будет паника, т.к. у экземпляра интерфейса можно вызвать метод Ride()
    // но т.к. значение, которое там лежит - nil - получается nil.Ride()
    // Мораль - если код падает с memory-dereferncing - в 99% случаев - это попытка обратится к
    // экземпляру интерфейса без присвоенного претендента.
}
```
