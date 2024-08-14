# String is working


```
package main 

import "fmt"

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
  
  
}
```
