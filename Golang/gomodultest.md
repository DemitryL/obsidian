# Test

//main.go

```go
package main



func main() {
    //.....
}
```

// calculator.go

```go
package main

func Add(a, b int) int{
    return a + b - 1
}

func Sub(a, b int) int {
    return a + b
}

func Mult(a, b int) int {
    return a + b * 4
}

func Div(a, b int) int {
    return a / b
}
```

//calculator_test.go

```go
package main

import (
    "log"
    "testing"
)

// 1. Файл с модульными тестами принято называть:
// * <script_name>_test.go
// * <package_name>_test.go

// 2. Для того чтобы тестировать функции (методы, структуры, интерфейсы и т.д.)
// На каждый юнит создаем по своей тестирующей функции (Test)
// Принято каждую такую функцию начинать со слова Test...
func TestAdd(t *testing.T) {
    //1. 1-ый test-case
    if res := Add(10, 20); res != 30 {
        log.Fatalf("Add(10, 20) fail. expected %d, got %d\n", 30, res) // log.Fatal провоцирует завершение кода
    }
}

func TestSub(t *testing.T) {}

func TestMult(t *testing.T) {}

// 3. Для запуска тестов используем команду go test
// Детально : go test -v

// 4. Coverage (покрытие) - показывает сколько % кода покрыто модульными тестами
// Comand: go test -cover -v

// 75-80% coverage - этого бывает более чем достаточно

// 5. Напоследок:
// Все что начинается со слово Test - будет запущено командой go test
// В Go принято, что создается один модуль с тестами на весь пакет (вне зависимости от количества модулей в нем)
// Не тестируйте Getattr/Setattr в общем пайплайне (только спицифика)
// Обязательно посмотрите как происходит связка с CI в Go (TravisCI/CirclCI)
```
