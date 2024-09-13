# Структуры в Go

```go
package main

import (
  "fmt"
)

// 1. Структура - заименованный набор полей (состояний), определяющий новый тип данных.

// 2. Определение структуры (явное определение)
type Student struct {
  firstName string
  lastName  string
  age       int
}

// 3. Если имеется ряд состояний одного типа, то можно сделать так
type AnotherStudent struct {
  firstName, lastName, groupName string
  age, coureNumber               int
}

func PrintStudent(std Student) {
  fmt.Println("=============")
  fmt.Println("FirstName:", std.firstName)
  fmt.Println("LastName:", std.lastName)
  fmt.Println("Age:", std.age)
}

func main() {
  // 4. Создание представителей структуры
  stud1 := Student{
    firstName: "Fedya",
    lastName:  "Petrov",
    age:       21,
  }
  //fmt.Println("Student 1:", stud1) // Student 1: {Fedya Petrov 21}
  PrintStudent(stud1)

  stud2 := Student{"Petya", "Ivanov", 19} // Порядок указания свойств такой же как в структуре
  PrintStudent(stud2)

  // 5. Что если не все поля сруктуры определить? Будут подствлены zeroValue по типам
  stud3 := Student{
    firstName: "Vasya",
  }
  PrintStudent(stud3)

  // 6. Анонимные структуры (структура без имени)
  anonStudent := struct {
    age    int
    groupID  int
    proffesorName  string
  }{
    age:  23,
    groupID: 2,
    proffesorName: "Alexeev",
  }
  fmt.Println("AnonStudent:", anonStudent) // AnonStudent: {23 2 Alexeev}

  // 7. Доступ к состояниям и их модификации
  studVova := Student{"Vova", "Ivanov", 19}
  fmt.Println("firstName:", studVova.firstName)
  studVova.age += 2
  fmt.Println("New age:", studVova.age)

  // 8. Инициализация пустой строки
  emptyStudent1 := Student{}
  var emptyStudent2 Student
  PrintStudent(emptyStudent1)
  PrintStudent(emptyStudent2)

  // 9. Указатели на экземпляры структур
  studPointer := &Student{
    firstName: "Igor",
    lastName: "Sidorov",
    age:   22,
  }
  fmt.Println("Value studPointer:", studPointer) // Value studPointer: &{Igor Sidorov 22}

  secondPointer := studPointer
  (*secondPointer).age += 20
  fmt.Println("Value afterPointerModify:", studPointer)

  studPointerNew := new(Student)
  fmt.Println(studPointerNew) // &{ 0}

  // 10. Работа с доступом к полям структур через указатель
  fmt.Println("Age via (*...).age:", (*studPointer).age) // 42
  fmt.Println("Age via .age:", studPointer.age) // происходит разыменовангие указателя studPointer и запрос соответствующего поля

  // 11. Структура с анонимными полями
  type Human struct {
    firstName string
    lastName string
    string
    int
    bool
  }

  // 12. Создание экземпляра с анонимными полями
  human := &Human{
    firstName: "Bob",
    lastName: "Johnson",
    string: "Additional info",
    int:   -1,
    bool: true,
  }
  fmt.Println(human)  // &{Bob Johnson Additional info -1 true}
}
```

## Настраеваемые и вложенные структуры

```go
// 1. Вложенные структуры (вложение структур). Этоиспользование одной структуры, как тип поля
// в другой структуре
type University struct {
  yearBased int
  infoShort string
  infoLong  string
}

type Student struct {
  firstName string
  lastName string
  university University
}

// 4. Встроенные структуры (когда мы добовляем поля одной структуры к другой)
type Professor struct {
  firstName string
  lastName string
  age int
  greatWork string
  // papers map[string]string - добавление этого поля делает структуры несравнимой
  University // В этом месте происходит добавление всех полей University в Professor
}


func main() {
  // 2. Создание экземпляра структур с вложением
  stud := Student{
    firstName: "Fedya",
    lastName: "Petrov",
    university: University{
      yearBased: 1991,
      infoShort: "cool University",
      infoLong: "very cool University",
    },
  }

  // 3. Получение доступа к вложенным полям структур
  fmt.Println("FirstName:", stud.firstName)
  fmt.Println("LastName:", stud.lastName)
  fmt.Println("Year Based Uni:", stud.university.yearBased)

  // 5. Получение доступа к встраеваемым структурам
  prof := Professor {
    firstName: "Anatoly",
    lastName: "Smirnov",
    age: 120,
    greatWork: "Ultimate c programming",
    University: University {
      yearBased:  1829,
      infoShort: "short info",
      age:  243,
    },
  }

  // 6. Обращение к полям с встроенной структурой
  fmt.Println("FirstName:", prof.firstName)
  fmt.Println("Year based:", prof.yearBased)
  fmt.Println("Info short:", prof.infoShort)
  fmt.Println("Age:", prof.University.age) // prof.age - Получим доступ к полю ВЫШЕЛЕЖАЩЕЙ СТРУКТУРЫ

  // 7. Сравнение экземпляров ==
  // При сравнении экземпляров происходит сравнение всех их полей друг с другом
  profLeft := Professor{}
  profRight := Professor{}

  fmt.Println(profLeft == profRight) // true

  // 8. Если ХОТЯБЫ ОДНО ИЗ ПОЛЕЙ СТРУКТУР - НЕ СРАВНИМО - то и вся структура несравнима
}
```
