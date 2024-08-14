# Массивы. Основа

```
package main

import "fmt"

func main() {
  // Arrays. Base
  // 1. Определение массива.
  // Создание массив под хранение 5-ти целочисленных элементов
  var arr [5]int // При инициализации массива важно передать информацию - сколько элементов в нем будет.
  fmt.Println("This is my array:", arr) // This is my array: [0 0 0 0 0]
  // 2. Определение элементов массива (после предворительной инициализации)
  // Необходимо обратится к элементу массива через синтаксис arr[i] = elem
  arr[0] = 10
  arr[1] = 20
  arr[3] = -500
  arr[4] = 720
  fmt.Println("After elements init:", arr) // After elements init: [10 20 0 -500 720]
  // 3. Определение массива с укозанием элементов на месте.
  newArr := [5]int{10, 20, 30, 40, 50}
  fmt.Println("Short declaration and init:", newArr) // Short declaration and init: [10, 20, 30, 40, 50]
  // Если при инициализации количество элементов меньше номинальной длины массива то недостоющие элементы инициализируются нулями.
  // nwArr := [5]{10, 20, 30} // [10, 20, 30, 0, 0]
  
  // 4. Создание массива через инициализацию переменных
  arrWithValues := [...]int{10, 20, 30, 40}
  fmt.Println("Arr declaration with [...]:", arrWithValues, "Length:", len(arrWithValues)) // [10, 20, 30, 40] Length: 4
  
  // 5. Массив - это набор ЗНАЧЕНИЙ. Тоесть при всех манипуляциях - массив копируется (жестко, на уровне компелятора.)
  first := [...]int{1,2,3}
  second := first 
  second[0] = 10000
  fmt.Println("First arr:", first) // First arr: [1, 2, 3]
  fmt.Println("Second arr:", second) // Second arr: [10000, 2, 3]
  
  //6. Массив и его размер - это две состовляющие одного типа (Размер массива - часть типа)
  var aArr [5]int
  var bArr [6]int
  aArr[0] = 100
  bArr = aArr // Error type
  
  // 7. Итерирование по массиву
  floatArr := [...]float64{12.5, 13.5, 15.2, 10.0, 12.0}
  for i := 0; i < len(floatArr); i++ {
    fmt.Printf("%d elemt of arr is %.2f\n", i, floatArr[i])
  }
  
  // 8. Итерирование по массиву через оператор range
  var sum float64
  for id, val := range floatArr {
    fmt.Printf("%d element of arr is %.2f\n", id, val)
    sum += val
  }
  fmt.Println("Total sum is:", sum)
  
  // 9. Игнорирование id в range base for цикле
  for _, val := range floatArr {
    fmt.Printf("%.2f value WO id\n", val)
  }
  
  // 10. Многомерные массивы
  words := [2][2]string{
    {"Bob", "Alice"},
    {"Victor", "Jo"},
  }
  
  fmt.Println("Multidimensional array:", words)
  
  // 11. Итерирование по многомерному массиву
  for _, val1 := range words {
    for _, val2 := range val1 {
      fmt.Printf("%s ", val2)
    }
    fmt.Println()
  }
  
  // 12. Общение со срезом == как массив, только без указания начального размера
  slice := []int{10, 20, 30}
  slice[0] = slice[0] * 10
  slice[1] = 200
  slice = append(slice, 200) // Добавление нового элемента
  for i, v := range slice {
    fmt.Println(i,v)
  }
  
  emptySlice := []int{}
  emptySlice = append(emptySlice, 200)
}
```

## Слайсы
```
package main

import "fmt"

func main() {
  // 1. Слайсы (они же срезы)
  // Слайс - это динамическая обвязка над массивами
  startArr := [4]int{10, 20, 30, 40}
  var startSlice []int = startArr[0:2] // Слайс инициализируется пустыми квадратными скобками
  fmt.Println("Slice[0:2]:", startSlice) // [10, 20]
  // Создали слайс, основываясь уже на существующем массиве
  
  // 2. Создание слайса без явной инициализации массива
  secondSlice := []int{13, 20, 30, 40}
  fmt.Println("SecondSlice:", secondSlice)
  
  // 3. Изменение элементов среза
  originArr := [...]int{30, 40, 50, 60, 70, 80}
  firstSlice := originArr[1:4] // Это набор ссылок на элементы нижележащего массива
  for i, _ := range firstSlice {
    firstSlice[i]++
  }
  fmt.Println("OriginArr:", originArr) // OriginArr: [30 41 51 61 70 80]
  fmt.Println("FirstSlice:", firstSlice) //FirstArr: [41 51 61]
  
  // 4. Один массив и два производных среза
  fSlice := originArr[:]
  sSlice := originArr[2:5]
  
  fmt.Println("Before modifications: Arr:", originArr, "fSlice:", fSlice, "sSlice:", sSlice)
  fSlice[3]++
  sSlice[1]++
  fmt.Println("Before modifications: Arr:", originArr, "fSlice:", fSlice, "sSlice:", sSlice)
  
  // 5. Срез как встроенный тип
  /*
  type slice struct {
    Length int
    Capacity int
    ZeroElement *byte
  }
  */
  
  // 6.Длина и еикость слайса
  wordsSlice := []string{"one", "two", "three"}
  fmt.Println("slice:", wordsSlice, "Length:", len(wordsSlice), "Capacity:", cap(wordsSlice))
  wordsSlice = append(wordSlice, "four")
  fmt.Println("slice:", wordsSlice, "Length:", len(wordsSlice), "Capacity:", cap(wordsSlice))
  // Capacity (cap) - или емкость слайса - это значение, показвающее СКОЛКО ЭЛЕМЕНТОВ В ПРИНЦИПЕ можно добавить в срез БЕЗ ВЫДЕЛЕНИЯ ДОПОЛНИТЕЛЬНОЙ ПАМЯТИ ПОД НИЗЛЕЖАЩИЙ МАССИВ.
  
  // Допустим у нас есть срез на 3 элемента (инициализировали без явного указания массива)
  // Компилятор при создании этого среза СНАЧАЛА создал массив ровно на 3 элемента
  // После этого компилятор вернул адрес, где массив живет
  // Срез запомнил этот адрес и теперь ссылается на него
  // Потом
  // Начинаем дефоромировать слайс (увеличим длину / увеличим количество элементов
  // Проблема - в ниже лежащем массиве (на котором основан слайс) все 3 ячейки. Что делать?
  // Компилятор ищет в памяти место для массива размером 3*2 (в общем случае n*2, где n - пероначальный размер)
  // После того как место найдено (в нашем случае найдено место для 6 элементов), в это место копируются 
  // старые 3 элемента на свои позиции. На 4-ую позицию мы добавляем новый элемент
  // После этого компилятор возвращает нашему слайсу новый адрес в памяти, где находится массив под 6 элементов.
  
  // Емкость всегда будет измерять как n*2
  numerics := []int{1,2}
  for i:=0; i < 200; i++ {
    if i % 10 == 0{
      fmt.Println("Current len:", len(numerics), "Current cap:", cap(numerics))
    }
    numerics = append(numerics, i)
  }
  
  // Важно: после выделения памяти под новый массив, ссылки со старым будут переписаны в новый
  // Пример
  numArr := [2]int{1,2}
  numSlice := numArr[:]
  
  numSlice = append(numSlice, 3) // В этот момент numSlice больше не ссылается на numArr
  numSlice[0] = 10
  fmt.Println(numArr) // [1 2]
  fmt.Println(numSlice) // [10 2 3]
  
  // 7. Как создавать слайсы наиболее эффективно?
  // make() - это фунция, позволяющая более детально создавать срезы 
  sl := make([]int, 10, 15)
  // []int - тип коллекции
  // 10 - длина
  // 15 - умкость
  // Сначала инициализируется arr = [15]int
  // Затем по нему делается срез arr[0:10]
  // После чего он возвращается
  fmt.Println(sl) // [0 0 0 0 0 0 0 0 0 0]
  
  // 8. Добавление элементов в СРЕЗ
  myWords := []string{"one", "two", "three"}
  fmt.Println("myWords:", myWords)
  anoherSlice := []string{"four", "five", "six"}
  myWords = append(myWords, anotherSlice...)
  myWords = append(myWords, "seven", "eight")
  mt.Println("myWords:", myWords)
  
  // 9. Многомерный срез
  mSlice := [][]int{
    {1, 2},
    {3, 4, 5, 6},
    {10, 20, 30},
    {} 
  }
  fmt.Println(mSlice)
}
```


