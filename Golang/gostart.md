# Вывод в консоль

```
packege main 

import "fmt"

func main() {
  // Простейший вывод в консоль. Println - это вывод аргумента + '\n'
  fmt.Println("Hello world")
  fmt.Println("Second line")
}
```
Результат:
```bash
Hello world
Second line
```
Соответственно функция Println() - выводит каждый аргумент с новой строки. Так же ее так сказать проотец фукция Print() - которая просто поочередно выводит аргуметы.

Пример функции Print() :
```
func main() {
  // Простой вывод в консоль.
  fmt.Print("First")
  fmt.Print("Second")
  fmt.Print("Third")
}
```
Результат:
```bash
FirstSecondThird
```

### Форматированный вывод -- Printf - стандартый вывод os.Stdout с флагом форматирования.

Пример функции Printf() :
```
func main() {
  fmt.Printf("Hello, my name is %s\n My age is %d", "Bob", 42)
}
```
Результат:
```bash
Hello, my name is Bob
My age is 42
```

### Деклорирование переменных

#### Какая типизация ?
***В языке Go*** принята полустрогая статическая типизация.

#### Способы деклорирования переменных.
**Декларирование** - это процесс связывание имени переменной с типом потенциального значения

Пример:
```
func main() {
  // Деклорирование
  var age int  // В начале идет ключевое слово, затем имя переменной и тип
  fmt.Println("My age is:", age)
}
```
Результат:
```bash
My age is: 0
```
**При деклорировании переменной** - автоматически происходит ее **инициализация** **НУЛЕВЫМ ЗНАЧЕНИЕМ ДЛЯ ЭТОГО ТИПА**

Присваивание значения:
```
func main() {
 age = 32 
 fmt.Println("Age after assigment:", age)
}
```
Результат:
```bash
Age after assigment: 32
```

### Деклорирование и инициализация пользоватедьских значений

```
func main() {
 var height int = 183 
 fmt.Println("My height is:", height)
}
```
Результат:
```bash
My height is: 183
```

### В чем **полустрогасть** типизации. Можно опускать тип переменной

```
func main() {
 var uid = 12345 
 fmt.Println("My uid:", uid)
 fmt.Println("%T\n", uid) // type 
}
```
Результат:
```bash
My uid: 12345
int
```

### Деклорирование и инициализация переменных одного типа (множественный случай)

```
func main() {
 var firstVar, secondVar int = 20, 30 
 fmt.Println("FirstVar:%d SecondVar:%d\n", firstVar, secondVar) 
}
```
Результат:
```bash
FirstVar: 20 SecondVar: 30
```

### Деклорирование блока переменных


```
func main() {
 var(
   personName string = "Bob"
   personAge int = 42
   personUID int
 )
 
 fmt.Println("Name: %s\nAge: %d\nUID: %d\n", personName, personAge, personUID)
}
```
Результат:
```bash
Name: Bob
Age: 42
UID: 0
```

**Немного странного**
```
func main() {
 var a, b = 30, "Vova"
 fmt.Println(a, b)
 
 // Немного хорошего. Повторное деклорирование переменной приводит к ошибке компиляции
 var a = 200 //previous declaration
}
```
Результат:
```bash
30 Vova
```

### Короткая деклорация (короткое обьявление)

```
func main() {
  count := 10
  fmt.Println("Count:", count)
  count = count + 1
  fmt.Println("Count:", count)
}
```
Результат:
```bash
Count: 10
Count: 11
```

### Множественное присваивание через :=

```
func main() {
  aArg, bArg := 10, 30
  fmt.Println(aArg, bArg)
}
```
Результат:
```bash
10 30
```
#### Короткое присваивание
Оператор ```:=``` слева от себя требует ***КАК МИНИМУМ ОДНУ НОВУЮ ПЕРЕМЕННУЮ*** 

```
func main() {
  aArg, bArg := 10, 30
  fmt.Println(aArg, bArg)
  aArg, bArg = 30, 40
  fmt.Println(aArg, bArg)
  // aArg, bArg := 10, 30
  // fmt.Println(aArg, bArg)
  
  // исключение из этого правила
  bArg, cArg := 300, 400
  fmt.Println(aArg, bArg, cArg)
}
```
Результат:
```bash
10 30
30 40 
30 300 400
```

**Пример:**
```
package main

import (
  "fmt"
  "math"
)

func main() {
  width, length := 20.5, 30.2
  fmt.Println("Min dimensional of rectangle is: %.3f\n", math.Min(width, length))
}
```
Результат:
```bash
Min dimensional of rectangle is: 20.500
```

#### Консольный ввод 

```
package main

import (
  "fmt"
)

func main() {
  var(
    age int
    name string
  )
  
  //fmt.Scan(&age)
  //fmt.Scan(&name)
  fmt.Scan(&age, &name)
  
  fmt.Printf("My name is: %s\nMy age is: %d\n", name, age)
  
  // Для ручного использованиея потока ввода
  fmt.Fscan(os.Stdin, &age)
  fmt.Println("New age:", age)
}
```
Результат:
```bash
12
Alica
My name is: Alica
My age is: 12
33
New age: 33
```
