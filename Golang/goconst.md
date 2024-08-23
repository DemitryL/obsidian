# Const in GO

```
package main

import "fmt"

// 1. Константы - это не изменяемые переменные которые служат для:
//  1) Более стогово понимания кода
//  2) Для того, чтобы случайно не поменять значение (предпологается что значение константы не изменно)
//  3) Для удобных преобразований

const (
  MAIN_PORT = "8001"
)

func main() {
  //2. Обьявление одной константы
  const a = 10
  fmt.Println(a)
  // 3. Обьявление блока констант с областью видимости внутри функции main
  const (
    ipAddress = "127.127.00.03"
    port = "8000"
    dbName = "postgres"
  )
  fmt.Println("ipAddress value:", ipAddress)

  // 4. Константу никак нельзя поменять в ходе работы программы
  const b = 200
  // b = 30 // err

  // 5. Значения константы ДОЛЖНЫ БЫТЬ ИЗВЕСТНЫ на момент компиляции
  const sqrt = math.Sqrt(25) // Нельзя присвоить в константу что-либо, что является результатом вызова функции, метода
  fmt.Println("Const sqrt:", sqrt)

  // 6. Типизированные и нетипизированные константы
  const ADMIN_EMAIL string = "admin@admin.com" // типизированная константа. Указание типа - повышение читабельности кода

  // 7. Нетипизированные константы и их профит
  const NUMERIC = 100
  var numInt = NUMERIC
  fmt.Printf("Value %v and Type %T\n", numInt, numInt)

  // При использовании нетипизированных констант мы разрешаем компилятору
  // использовать неявное приведение типов в момент присваивания значений констант в переменные
  var numInt8 int8 = NUMERIC
  var numInt32 int32 = NUMERIC
  var numInt64 int64 = NUMERIC
  var numFloat32 float32 = NUMERIC
  var numComplex complex64 = NUMERIC

  fmt.Printf("numInt8 value %v type %T\n", numInt8, numInt8)
  fmt.Printf("numInt32 value %v type %T\n", numInt32, numInt32)
  fmt.Printf("numInt64 value %v type %T\n", numInt64, numInt64)
  fmt.Printf("numFloat32 value %v type %T\n", numFloat32, numFloat32)
  fmt.Printf("numComplex value %v type %T\n", numComplex, numComplex)

  // 8. Константы в Go зашиваются в момент компиляции в RUNTIME программы и не выбрасываются до ее окончания

func checkPortIsValid() bool {
  if MAIN_PORT == "8001" {
    return true
  }
  return false
}
```
