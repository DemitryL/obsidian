# String is working

```go
package main

import (
  "fmt"
  "unicode/utf8"
)

func main() {
  name := "Hello world"
  fmt.Println(name)

  // 1. Строка - это байтовый слайс со своими особенностями при обращении к нижележащему массиву
  word := "Sample word"
  fmtPrintf("string %s\n", word)
  // Какие значения байт сейчас находятся в слайсе word?
  fmt.Printf("Bytes: ")
  for i := 0; i < len(word); i++ {
    fmt.Printf("%x ", word[i] // %x - формат представления 16-тиричного байта
  }
  fmt.Println() // Bytes: 53 61 6d 70 6c 65 20 77 6f 72 64
  // Каким образом получать доступ к отдельно стоящим символам?
  for i : 0; i < len(word); i++ {
    fmt.Printf("%c ", word[i] // %c - формат предсталерия символа
  }
  fmt.Println() // Characters: S a m p l e  w o r d

  // 2. Строки в Go - хранятся как наборы UTF-8 символов. Каждый символ, вообще говоря, может занимать больше чем 1 байт

  // 3. Руна (Rune) - это стандартный встроенный тип в Go (alias над int32), позволяющий хранить единый неделимый UTF символ ВНЕ ЗАВИСИМОСТИ ОТ ТОГО сколько байт он занимает
  fmt.Printf("Runes: ")
  words := "Тестовая строка"
  runeSlice := []rune(words) // Преобразование слайса байт к слайсу рун / наоборот - []byte(sliceRune)
  for i := 0; i < len(runeSlice); i++ {
    fmt.Printf("%c ", runeSlice[i])
  }
  fmt.Println() // Runes: Т е с т о в а я  с т р о к а

  // 4. Итерирование по строке с использованием рун
  for id, runeVal := range words { // id - это индекс байта, с КОТОРОГО НАЧИНАЕТСЯ РУНА runeVal
    fmt.Printf("%c starts at position %d\n", runeVal, id)
  }

  // 5. Создание строки из слайса байт
  myByteSlice := []byte{0x40, 0x41, 0x42, 0x43} // Исходное представление байтов
  myStr := string(myByteSlice)
  fmt.Println(myStr) // @ABC

  myDecimalByteSlice := []byte{100, 101, 102, 103} // синтаксический сахар - можно использовать десятичное представление байтов
  myDecimalStr := string(myDecimalByteSlice)
  fmt.Println(myDecimalStr) // defg

  // 6. Создание строки из слайса рун
  // Руны как hex
  runeHexSlice := []rune{0x45, 0x46, 0x47, 0x48}
  myStrFromRune := string(runeHexSlice)
  fmt.Println("From Runes(hex):", myStrFromRune) // EFGH
  // Руны как литералы
  runeLiteralSlice := []rune{'v', 'a', 's', 'y', 'a'} // '' - таким образом обозначается руна
  myStrFromRuneLiterals := string(runeLiteralSlice)
  fmt.Println("From Runes(literals):", myStrFromRuneLiterals) // Vasya

  fmt.Printf("%s and %T\n", myStrFromRuneLiterals, myStrFromRuneLiterals) // Vasya and string

  // 7. Длина и емкость строки
  // Длина len() - количество байт в слайсе
  fmt.Println("Length of Вася:", len("Вася")) // Length of Вася: 8

  // Длина RuneCounter - количество !рун!
  fmt.Println("Length of Вася:", utf8.RuneCountInString("Вася")) // Length of Вася: 4

  // Вычисление емкости строки - бессмысленно, т.к. строка базовый тип
  fmt.Println(cap([]rune("Вася"))) // 4

  // 8. Сравнение строк  == и !=. Начиная с go 1.6
  word1, word2 := "Вася", "Петя"
  if word1 == word2 {
    fmt.Println("Equal")
  } else {
    fmt.Println("Not equal")
  }

  // 9. Конкатенация
  word3 := word1 + word2
  fmt.Println(word3) // ВасяПетя

  // 10. Строитель строк (java -> StringBuiler)
  firstName := "Alex"
  secondName := "Johnson"
  fullName := fmt.Sprintf("%s #### %s", firstName, secondName)
  fmt.Println("FullName:", fullName) // FullName: Alex #### Johnson

  // 11. Строки не изменяемые
  fullName[0] = "Q" // (strings are immutable)

  // 12. А слайсы изменяемые :)
  fullNameSlice := []rune(fullName)
  fullNameSlice[0] = 'F'
  fullName = string(fullNameSlice)
  fmt.Println("String mutation:", fullName) // String mutation: Flex #### Johnson

  // 13. Сравнение рун
  if 'Q' == 'q' {
    fmt.Println("Runes equal")
  } else {
    fmt.Println("Runes not equal")
  }

  // 14. Где живут полезные методы работы со строками?
  // import "strings"

}
```

## Работа с буфером

```go
package main

import (
  "bufio"
  "fmt"
  "os"
  "strconv"
)

func main() {
  var name string
  input := bufio.NewScanner(os.Stdin)
  if input.Scan() { // Команда захвата потока ввода и сохранения в буфер (захват идет до символа окончания строки)
  name = input.Text() // Команда вовращения элементов, помещенных в буфер (отдаст string)
  }
  fmt.Println(name)

  fmt.Println("For loop started:")
  for {
    if input.Scan() {
      result := input.Text()
      if result == "" {
       break
      }
      fmt.Println("Input string is:", result)
    }
  }

  // Преобразование строкого литерала к чему-нибудь числовому
  numStr := "10"
  numInt, _ := strconv.Atoi(numStr) // Atoi - Anything to Int (именно int)
  fmt.Printf("%d is %T\n", numInt, numInt) // 10 is int

  numInt64, _ := strconv.ParseInt(numStr, 10, 64)
  fmt.Printlln(numInt64 + numInt) // (mismatched type int64 and int)

  numFloat32, _ := strconv.ParseFloat(numStr, 32) //Но это 64-разрядное число будет без проблем ГАРАНТИРОВАНО ПРИВОДИТЬСЯ к 32
  fmt.Println(numInt64, numFloat32) // 10 10
  fmt.Printf("%.3f and %T\n, numFloat32, float32(numFloat32)) // 10.000 and float64

}
```
