# Обработка ошибок / паники

## DEFER

//main.go

```go
package main

import "fmt"

//1. DEFER - оператор отложенного ВЫЗОВА функции/метода.

//2. Создадим отложенную функцию

//3. С выходными параметрами

func CheckDBCloseConnection(a int) {
    fmt.Println("Check started......Value:", a)
    fmt.Println("Check done! Connection refused")
}

//4. Если функция принемает входные параметры и данная функция используется в связке с defer
// то:
// параметры расчитываются в момент передачи их в функцию
// А вызов функции с уже давно рассчитаным параметром осуществляется в момент
// завершения выше лежащей функции.

// В какой момент defer вызывается?
func OuterFunc() int{
    defer fmt.Println("I'm defered print function") // 3
    fmt.Println("OuterFunc started!") // 1
    var result = 10
    fmt.Println("OuterFunc finished. Ready to return value") // 2
    return result
}

func main() {
    defer fmt.Println("Step 1 defer") // 4
    defer fmt.Println("Step 2 defer") // 3
    defer fmt.Println("Step 3 defer") // 2
    defer fmt.Println("Step 4 defer") // 1

    var namIP = 10
    p := &namIP
    defer CheckDBCloseConnection(namIP) // defer означает что данная функция будет вызвана при завершении main() с параметром,
    //значение которого расчитывается на момент 31-ой строки
    *p++
    fmt.Println("Value namIP in main():", namIP)
    fmt.Println("Main function started")
    fmt.Println("Main function ended")
    fmt.Println("Value from OuterFunc on main side is:", OuterFunc()) // 4
}
```

## ERROR

// main.go

```go
// В Go существует 2 механизма сигнализирования аномального поведения
// 1-ый механизм это ошибки Error (ЯВЛЯЕТСЯ КАНОНИЧНЫМ ИСПОЛНЕНИЕМ НА СЛУЧАЙ НЕНОРМАЛЬНОГО ПОВЕДЕНИЯ)
// 2-ой механизм - это паника (не лучший вариант так как приводит сразу к аварийному завершению, и в принципе
// мог быть обычной ошибкой)

//Error
package main

import (
    "errors"
    "fmt"
    "runtime/debug"
    "log"
    "strconv"
)

func funcWithError(a int) (string, error) {
    if a % 2 == 0 {
        return "Even", nil
    }
    return "", errors.New("THIS IS ERROR!")
}

// Panic
func PanicRecover() {
    if r := recover(); r != nil {
        fmt.Println("Panic satisfied:", r)
        debug.PrintStack()
    }
}

func panicExample(firstName *string, lastName *string) {
    defer PanicRecover() // Даже в случае возникновения паники - первым делом будут вызваны все deferred функции.
    if firstName == nil {
        panic("runtime error: fistname can not be nil")
    }

    if lastName == nil {
        panic("runtime error: lastname can not be nil")
    }

    fmt.Println("Full name:", *firstName, *lastName)
}

func main() {
    numLiteral := "12"
    num, err := strconv.Atoi(numLiteral)
    if err != nil {
        log.Fatal("Can not convert this value to int:", err)
        return
    }
    fmt.Println("Convertion Done:", num)

    ans, err := funcWithError(5)
    if err != nil {
        fmt.Println("not use odd values", err)
        return
    }
    fmt.Println(ans)

    var name = "Bob"
    panicExample(&name, nil)
}
```
