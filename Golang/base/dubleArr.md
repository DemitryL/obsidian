# Чтобы решить эту проблему, нам нужно объединить два отсортированных массива (arr1 и arr2) и убедиться, что полученный массив также отсортирован в порядке возрастания, без каких-либо повторяющихся элементов.

План:
- Мы возьмем на себя слияние двух отсортированных массивов.
- Используйте набор (или карту) для отслеживания уникальных элементов и удаления любых дубликатов во время объединения.
- Наконец, мы преобразуем набор/карту обратно в список и вернем его, убедившись, что он отсортирован в порядке возрастания.

```go
package main

import "fmt"

func mergeArrays(arr1, arr2 []int) []int {
    // Create a set (map) to store unique elements
    uniqueElements := make(map[int]bool)

    // Add elements from arr1 to the map (set)
    for _, num := range arr1 {
        uniqueElements[num] = true
    }

    // Add elements from arr2 to the map (set)
    for _, num := range arr2 {
        uniqueElements[num] = true
    }

    // Create a slice to store the merged and unique elements
    result := make([]int, 0, len(uniqueElements))

    // Extract the unique elements from the map into a slice
    for num := range uniqueElements {
        result = append(result, num)
    }

    // Sort the resulting slice
    sort.Ints(result)

    return result
}

func main() {
    arr1 := []int{1, 5, 9, 4, 2}
    arr2 := []int{3, 9, 2, 7, 4}
    
    merged := mergeArrays(arr1, arr2)
    fmt.Println("Merged and sorted array:", merged)
}

```

Объяснение:
Создадим карту (uniqueElements): На этой карте будут только уникальные элементы. Ключи — это целые числа из входных массивов, а значения устанавливаются в true (для обеспечения уникальности).

Добавьте элементы на карту: Мы проходим по arr1 и arr2, добавляя каждый элемент на карту. Если элемент уже существует, он будет проигнорирован, чтобы не было дубликатов.

Извлекайте уникальные элементы: После обработки обоих массивов мы извлекаем все ключи из карты в срез под названием result.

Отсортируйте результат: Мы используем сортировку. Функция ints из пакета сортировки для сортировки результирующего среза в порядке возрастания.

Return the sorted slice.Верните отсортированный ломтик.


### Пример удаления одинаковых элементов из слайса:
```go
package main

import "fmt"

func removeDuplicates(nums []int) []int {
    uniqueMap := make(map[int]bool)
    result := []int{}

    for _, num := range nums {
        if !uniqueMap[num] {
            uniqueMap[num] = true
            result = append(result, num)
        }
    }

    return result
}

func main() {
    nums := []int{1, 2, 3, 4, 4, 5, 2, 1}
    fmt.Println("Original array:", nums)

    result := removeDuplicates(nums)
    fmt.Println("Array without duplicates:", result)
}

```
Объяснение:
- Создается пустая мапа uniqueMap, где ключами будут уникальные элементы слайса.
- Проходим по всем элементам слайса. Если элемент еще не встречался (его нет в мапе), добавляем его в результат и помечаем как встреченный в мапе.
- Возвращаем новый слайс без дубликатов.

Описание:
Время работы этого решения: O(n), где n — это количество элементов в исходном слайсе, поскольку добавление элементов в мапу и проверка их наличия происходит за O(1) для каждого элемента.
Пространственная сложность: O(n) для хранения уникальных элементов в мапе.
Таким образом, с помощью мапы можно эффективно удалить одинаковые элементы из слайса в Go.
