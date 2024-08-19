# Functions in GO

```
package main

import "fmt"

// 1. Явная функция - локально-определенный блок кода, имеющий имя (ЯВНОЕ ОПРЕДЕЛЕНИЕ)
// Фунецию необходимо определить + Функцию необходимо вызвать
// 2. Сигнатура фунеций и их определение
// func functionName(params type) typeReturnValue {
// //body
// }

func main() {
  fmt.Println("Hello world")
  // 4. Вызов простейшей функции
  res := add(10, 20)
  fmt.Println("Result of add(10, 20):", res)
  fmt.Println("Result of mult(1,2,3,4):", mult(1,2,3,4))
  per, area := rectangleParameters(10.5, 10.5)
  fmt.Println("Area of rect(10.5, 10.5):", area)
  fmt.Println("Perimeter of rect(10.5, 10.5):", per)

  secondPer, secondArea := namedReturn(10, 20)
  fmt.Println(secondArea, secondPer)

  emptyReturn(10)

  helloVaridic(10, 20, 30, 40, 50, 60)

  someStrings(2,3, "Bob", "Alex", "Vito")

  sum1 : sumVariadic(10, 20, 30, 40, 50, 60)
  sliceNumber := []int{10, 20, 30}
  sum2 := sumVariadic(sliceNumber...)
  fmt.Println(sum1, sum2)

  // 12. Анонимная функция (синтаксис)
  anon := func(a, b int) int {
    return a + b
  }
  fmt.Println("Anon:", anon(20, 30))
}

// 3. Простейшая функция (определить функцию можно как до момента ее вызова в функции main,
// так и в любом месте пакетаб главное чтобы она была определена в принципе где-нибудь)
func add(a int, b int) int {
  result := a + b
  return result
}

// 4. Функция с однотипными параметрами
func mult(a, b, c, d int) int {
  result := a * b * c * d
  return result
}

// 5. Возврат больше чем одного значения (returnType1, returnType2.....)
func rectangleParameters(length, width float64) (float64, float64) {
  var perimeter = 2 * (length + width)
  var area = length * width

 return perimeter, area
}

// 6. Именованный возврат значений
func namedReturn(a, b int) (perimeter, area int) {
  perimeter = 2 * (a + b)
  atea = a * b
  return // Не нужно указывать возвращаемые переменные
}

// 7. При вызове оператора return фукция прекрощает свое выполнение и возврацает что-то
func funcWithReturn(a, b int) int {
  if a > b {
    return a - b
  }

  if a == b {
    return a
  }

  return b
}

// 8. Что вернется в случаеб если return в принципе не указан (или он пустой)
func emptyReturn(a int) {
  fmt.Println("I'm emptyReturn with parameter:", a)
  return
}

// 9. (*args, **kwargs) Variadic parameters (континуальные параметры)
func helloVaridic(a ...int) {
  fmt.Println(a)
}

// 10. Смешение параметров с variadic (
//  1.Континуальный параметр всегда самый последний
//  2.Variadic параметр - на всю функцию один (для удобочитаемости)
//)
func someStrings(a, b int, words ...string) {
  fmt.Println("Parameter:", a)
  fmt.Println("Parameter:", b)
  var result string
  for _, word := range words {
    result += word
  }
  fmt.Println("Result concat:", result)
}

// 11. Передача слайса или использование variadic parameters?
func sumVariadic(nums ...int) int {
  var sum int
  for _, val := range nums {
    sum += val
  }
  return sum
}

// 13. Анонимная функция внутри явной
func bigFunction(aArg, bArg int) int {
  return func(a, b int) int { return a + b + 1}(aArg, bArg)
}
```
