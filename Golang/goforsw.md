# Цикл for

В go решили не заморачиваться и в go есть один единственный цикл for

```go
package main

import "fmt"

func main() {
  /*
  for init; condition; post {
    init - блок инициализации переменных цикла
    condition - условие ( если верно то тело цикла выполняется, если нет - то цикл завершается)
    post - изменения переменной цикла ( инкрементарное действие, декрементарное действие )
  }
  */

  for i := 0; i <= 5; i++ {
    fmt.Printf("Current value: %d\n", i)
  }

  // Важно в качестве init может быть использовано выражение присваивания только через :=

  // break - команда, прерывающая текущее выполнение тела цикла и передающая управление инструкциям следующим за циклом.
  for i := 0; i <= 15; i++ {
    if i > 12 {
      break
    }
    fmt.Printf("Current value: %d\n", i)
  }
  fmt.Println("After for loop with BREAK")

  // continue - команда, прерывающая текущее выполнение тела цикла и передающая управление СЛЕДУЮЩЕЙ ЭТЫРАЦИИ ЦИКЛА
  for i := 0; i <= 20; i++ {
    if i > 10 && i <= 15 {
      continue
    }
    fmt.Printf("Current value: %d\n", i)
  }
  fmt.Println("After for loop with CONTINUE")
}
```

```go
func main() {
  // Вложенные циклы и лейблы
  for i := 0; i < 10; i++ {
    for j := 0; j <= i; j++ {
      fmt.Print("*")
    }
    fmt.Println()
  }
  fmt.Println("По идеи выше треуголиник")

  // Иногда  бывает плохо, С лейблами по лучще. Лейблы - это синтаксический сахар.
  outer:
    for i := 0; i <= 2; i++ {
      for j := 1; j <= 3; j++ {
        fmt.Printf("i:%d and j:%d and sum i+j", i, j, i+j)
        if i == j {
          break outer // Хочу чтобы вообще все циклы ( внешнии тоже остановились )
        }
      }
    }
}
```

```go
import (
 "fmt"
 "strings"
)

func main () {
  // Модификации цикла for
  // 1. Классический цикл while do
  var loopVar int = 0
  /*
  while (loopVar < 10) {
    ....
    loopVar++
  }
  */
  for loopVar < 10 {
    fmt.Printf("In while like loop %d\n", loopVar)
    loopVar++
  }

  // 2. Классический бесконечный цикл
 outer:
  var password string
  for {
    fmt.Print("Insert password: ")
    fmt.Scan(&password)
    if strings.Contains(password, "1234") {
      fmt.Println("Weak password. Try again")
    } else {
      fmt.Println("Password Accepted")
      break outer
    }
  }

  // 3. Цикл с множественными переменными цикла
  for x,y := 0, 1; x <= 10 && y <= 12; x,y = x + 1, y + 2 {
    fmt.Printf("%d + %d = %d\n", x, y, x+y)
  }
}
```

```go
package main

import "fmt"

func main() {
  // Switch
  var price int
  fmt.Scan(&price)

  // В switch-case запрещены дублируещиеся условия в case"ах
  switch price {
    case 100:
      fmt.Println("Firset case")
    case 110:
      fmt.Println("Second case")
    case 120:
      fmt.Println("Third case")
    case 130:
      fmt.Println("Another case")
    default:
      // Отрабатывает только в том случае, если не один из выше перечисленных кейсов - не сработает
      fmt.Println("Default case")
  }

  // Case с множеством вариантов
  var ageGroup string = "b" // Возрастные группы: "a", "b", "c", "d", "e"
  switch ageGroup {
    case "a", "b", "c":
      fmt.Println("AgeGroup 10-40")
    case "d", "e":
      fmt.Println("AgeGroup 50-70")
    default:
      fmt.Println("You are too yong/old")
  }

  // Case с выражениями
  var age int
  fmt.Scan(&age)

  switch {
    case age <= 18:
      fmt.Println("Too yong")
    case age > 18 && age <= 30:
      fmt.Println("Second case")
    case age > 30 && age <= 100:
      fmt.Println("Too old")
    default:
      fmt.Println("Who are you")
  }

  // Case с проваливаниями. Проваливание выполняют ДАЖЕ ЛОЖНЫЕ КЕЙСЫ
  // В момент выполнения fallthrough у следующего кейса не проверяется условие, а сразу выполняет тело.
  var number int
  fmt.Scan(&number)
  switch {
    case number < 100:
      fmt.Printf("%d is less then 100\n", number)
      fallthrough
    case number < 200:
      fmt.Printf("%d less then 200\n", number)
  }

  // Гадость с терсмнацией цикла for из switch
  var i int
 uberloop:
  for {
    fmt.Scan(&i)
    switch {
      case i%2 == 0:
        fmt.Printf("Value is %d and it's even\n", i)
        break uberloop
    }
  }
  fmt.Println("END")
}
```
