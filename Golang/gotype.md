# Какие есть встроенные типы

### Логический тип или по другому булевый (boolean)

```go
package main

import "fmt"

func main() {
  // Boolean => default false
  var firstBoolean bool
  fmt.Println(fistBoolean) // false

  // Boolean operands
  aBoolean, bBoolean := true, false
  fmt.Println("AND", aBoolean && bBoolean) // false
  // Операция логического "и" - называется еще логическим умножением.

  // Второй вариант логическое "или" - или как его еще называют сложением
  fmt.Println("OR", aBoolean || bBoolean) // true

  // Логическое отрицание "NOT" !
  fmt.Println("NOT", !aBooean) // false
}
```

### Множество целых чисел.

```go
func main() {
  // Numerics, Integers
  // int8, int16, int32, int64, int
  // int - платформо зависимый в зависимости от разрядности вашей операционной системы.
  // uint8, uint16, uint32, uint64, uint
  var a int = 32
  b := 92
  fmt.Println("Value of a:", a, "Value of b:", b, "Sum of a+b:", a+b) // Value of a: 32 Value of b: 92 Sum of a+b: 124

  // Вывод типа через %T форматирование
  fmt.Println("Type is %T\n", a) // Type is int
  // Узнаем, сколько байт занимает переменная типа int
  fmt.Println("Type %T size of %d bytes\n", a, unsafe.Sizeof(a)) // Type int size of 8 bytes
  // 1 byte = 8 bit

   // Эксперимент. При использовании короткого обьявления - тип для целого числа - int платформо-зависимый.
  fmt.Println("Type %T size of %d bytes\n", b, unsafe.Sizeof(b)) // Type int size of 8 bytes

  // Эксперимент 2.
  var first32 int32 = 12
  var second64 int64 = 13
  fmt.Println(first32 + second64)
  //  Это код вызовет ошибку несмотряна то что мы складываем два числа, но разрядность этих чисел разная. Для решения Используете явное приведение типов при необходимости если уверены что не произойдет коллизии
  fmt.Println(int64(first32) + second64)

  // Эксперимент 3. Если проводятсяарифметические операции
  // над int и intX, то обязательно нужно использовать механизм приведения. Т.к. int != int64.
  var third64 int64 = 16123414
  var fourtInt int = 15623
  fmt.Println(third64 + fourtInt) // Вызовет ошибку - конфликт
  fmt.Println(third64 + int64(fourtInt))

  // Аналагичным образом устроены uint8, uint16, uint32, uint64, uint - только нужно помнить что они хранят только положительные значения.
  var varA uint = 10

  // Numerics, Float
  // float32, float64
  floatFirst, floatSecond := 5.67, 12.54
  fmt.Printf("type of a %T and type of %T\n", floatFirst, floatSecond) // type of a float64 and type of float64

  sum := floatFirst + floatSecond
  sub := floatFirst - floatSecond
  fmt.Println("Sum:", sum, "Sub", sub) // Sum: 18.21 Sub: -6.86999999999999
  // Лучше всего использовать Printf()
  fmt.Printf("Sum: %.3f and Sub: %.3f\n", sum, sub) // Sum: 18.210 Sub: -6.870

  // Numerics, Complex
  c1 := complex(5, 7)
  c2 := 12 + 32i
  fmt.Println(c1 + c2) //(17 + 39i)
  fmt.Println(c1 * c2) // (-164+244i)
}
```

### Strings - Строки

```go
func main() {
  // Strings. Строка - это набор БАЙТ
  name := "Fedya"
  lastname := "Pupkin"
  concat := name + " " + lastname
  fmt.Println("Full name:", concat) // Full name: Fedya Pupkin

  fmt.Println("Length of string:", name, len(name)) // Length of string: Fedya 5
  // Функция len() - возвращает количество элементов в наборе

  nameC := "Федя"
  fmt.Println("Amount of chars:", nameC,  utf8.RuneCountInString(nameC)) // Amount of chars: Федя 4

  В Go для хранения utf символов используется такое понятие как руна(Rune). Руна - это один utf символ.

  // Содержится ли подстрока в строке
  totalString, subString := "ABCDEDFG", "CDE"
  fmt.Println(strings.Contains(totladString, subString)) // true

  // rune -> alias int32
  var sampleRune rune
  fmt.Println(sampleRune) // 0
  fmt.Printf("Rune as char %c\n", samplrRune)

  var anotherRune rune = 'Q' // Для инициализации руны символьным значением - используйте ''
  fmt.Printf("Rune as char %c\n", anotherRune) // Rune as char Q

  var thirdRune rune = 234
  fmt.Printf("Rune as char %c\n", thirdRune) // Rune as char e

  // "A" < "abcd"
/*
  -1 if first < second,
   0 if first == second,
   1 if first > second
*/
  fmt.Println(strings.Compare("abcd", "def")) // -1 - обозначает что левая строка меньше правой.
  fmt.Println(strings.Compare("abcd", "abcd")) // 0 - обозначает что равны.
  fmt.Println(strings.Compare("abcd", "a")) // 1 - обозначает что левая сторона больше правой.

  var aByte byte // alias uint8
  fmt.Println("Byte:", aByte) // 0
}
```
