## map()

```go
package main

import "fmt"

func main() {
  // 1. Map - это набор пар ключ:значение. Инициализация пустой мап
  mapper := make(map[string]int)
  fmt.Println("Empty map:", mapper) // Empty map: map[]

  // 2. Добавление пар в существующую мапу
  mapper["Alice"] = 24
  mapper["Bob"] = 25
  fmt.Println("Mapper after adding pairs:", mapper) // map[Alice:24 Bob:25]

  // 3. Инициализация мапы с указанием пар
  newMapper := map[string]int{
    "Alice":1000,
    "Bob":1000,
  }
  newMapper["Jo"] = 3000
  fmt.Println("New Mapper:", newMapper) // New Mapper: map[Alice:1000 Bob:1000]

  // 4. Что может быть ключом в мапе?
  // 4.1 ВАЖНО: Мапа НЕ УПОРЯДОЧНА В GO
  // 4.2 КЛЮЧАМИ В МАПЕ МОЖЕТ БЫТЬ ТОЛЬКО СРАВНИМЫЙ ТИП (==, !=)

  // 5. Нулевое значение для map
  // var mapZiroValue map[string]int  // mapZiroValue == nil
  // mapZiroValue["Alice"] = 12

  // 6. Получение элементов из map
  // 6.1 Получение элемента, который представлен в мапе
  testPerson := "Alice"
  fmt.Println("Salary of testPerson:", newMapper[testPerson]) // Salary of testPerson: 1000
  // 6.2 Получение элемента который НЕ представлен в мапе
  testPerson = "Derek"
  fmt.Println("Salary of new testPerson:", newMapper[testPerson]) //Salary of new testPerson: 0
  // При обращении к несуществующему ключу - новая пара не добавляется
  fmt.Println(newMapper) // map[Alice:1000 Bob:1000 Jo:3000]

  // 7. Проверка вхождения ключа
  employee := map[string]int{
    "Den": 0,
    "Alice": 0,
    "Bob": 0,
  }
  fmt.Println("Den and Value:", employee["Den"]) // Den and Value: 0
  fmt.Println("Jo and Value:", employee["Jo"]) // Jo and Value: 0

  // 7.1 При обращении по ключу - возвращается два значения
  if value, ok := employee["Den"]; ok {
    fmt.Println("Den and Value:", value)
  } else {
    fmt.Println("Den does not exists in map")
  }
  if value, ok := employee["Jo"]; ok {
    fmt.Println("Jo and Value:", value)
  } else {
    fmt.Println("Jo does not exists in map")
  }

  // 8. Перебор элементов мапы
  for key, value := range employee {
    fmt.Printf("%s and value %d\n", key, value)
  }

  // 9. Как удалять пары
  // 9.1 Удаление существующей пары
  fmt.Println("Before deleting:", employee) // Before deleting: map[Alice:0 Bob:0 Den:0]
  delete(employee, "Den")
  fmt.Println("After deleting:", employee) // After deleting: map[ALice:0 Bob:0]

  // 9.2 Удаление не существующей пары
  if _, ok := employee["Anna"]; ok {
    delete(employee, "Anna") // ОЧЕНЬ ДОРОГАЯ ОПЕРАЦИЯ
  }
  fmt.Println("After second del:", employee) After second del: map[ALice:0 Bob:0]

  // 10. Количество пар == длина мапы
  fmt.Println("Pair amount in map:", len(employee)) // Pair amount in map: 2

  // 11. Мапа (как и слайс) ссылочный тип
  words := map[string]string{
    "One": "Один",
    "Two": "Два",
  }

  newWords := words
  newWords["Three"] = "Три"
  delete(newWords, "One")
  fmt.Println("words map:", words) // words map: map[Three:Три Two:Два]
  fmt.Println("newWords map:", newWords) // newWords map: map[Three:Три Two:Два]

  // 12. Сравнение мап
  // 12.1 Сравнение массивов (массив можно использовать как ключ в мапе)
  if [3]int{1, 2, 3} == [3]int{3, 4, 5} {
    fmt.Println("Equal")
  } else {
    fmt.Println("Not equal")
  }

  // 12.2 Сравнение слайсов. Слайсы (из-за того что тип ссылочный - можно сравнить только с nil)
  //if []int{1,2,3} == []int{1,2,3} {
    //fmt.Println()
  //}

  // 12.3 Сравнение мап. Мапа (из-за того что тип ссылочный - можно сравнить только с nil)
  aMap := map[string]int{
    "a": 1,
  }
  var bMap map[string]int

  if aMap == nil {
    fmt.Println("Zero value map")
  }

  if bMap == nil {
    fmt.Println("Zero value of map bMap")
  }

  // 13. Грустные следствичя
  // Если мапа/слайс являются составляющими какой-либо структуры - структура автоматичестки не сравнима
}
```
