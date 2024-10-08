# Карты Go в действии

## Введение

Одной из самых полезных структур данных в информатике является хеш-таблица. Существует множество реализаций хеш-таблиц с различными свойствами, но в целом они предлагают быстрый поиск, добавление и удаление. Go предоставляет встроенный тип карты, который реализует хеш-таблицу.

## Объявление и инициализация

Тип карты Go выглядит следующим образом:
```
map[KeyType]ValueType
```

где KeyType может быть любым типом, который можно сравнить (подробнее об этом позже), а ValueType может быть вообще любым типом, включая другую карту!

Эта переменная m представляет собой сопоставление строковых ключей со значениями int:
```
var m map[string]int
```

Типы карт являются ссылочными типами, такими как указатели или срезы, поэтому значение m выше равно нулю; Он не указывает на инициализированную карту. Карта nil ведет себя как пустая карта при чтении, но попытки записи в карту nil приведут к панике во время выполнения; Не делайте этого. Чтобы инициализировать карту, используйте встроенную функцию make:
```
m = make(map[string]int)
```

Функция make выделяет и инициализирует структуру данных хеш-карты и возвращает значение карты, указывающее на нее. Специфика этой структуры данных является деталью реализации среды выполнения и не определяется самим языком. В этой статье мы сосредоточимся на использовании карт, а не на их реализации.

## Работа с maps

Go предоставляет знакомый синтаксис для работы с картами. Этот оператор устанавливает ключ "route" в значение 66:
```
m["route"] = 66
```
Этот оператор извлекает значение, хранящееся в ключе "route", и присваивает его новой переменной i:
```
i := m["route"]
```

Если запрошенный ключ не существует, мы получаем нулевое значение типа value. В этом случае тип значения — int, поэтому нулевое значение равно 0:
```
j := m["root"]
// j == 0
```
Встроенная функция len возвращает количество элементов на карте:

```
n := len(m)
```
Встроенная функция delete удаляет запись с карты:
```
delete(m, "route")
```

Функция delete ничего не возвращает и ничего не сделает, если указанный ключ не существует.

Присваивание двух значений проверяет существование ключа:

```
i, ok := m["route"]
```

В этом операторе первому значению (i) присваивается значение, хранящееся под ключом "route". Если этот ключ не существует, i — это нулевое значение типа значения (0). Второе значение (ok) — это логическое значение, которое имеет значение true, если ключ существует в карте, и false, если его нет.

Чтобы проверить ключ без извлечения значения, используйте символ подчеркивания вместо первого значения:
```
_, ok := m["route"]
```

Чтобы перебрать содержимое карты, используйте ключевое слово range:
```
for key, value := range m {
    fmt.Println("Key:", key, "Value:", value)
}
```

Чтобы инициализировать карту какими-либо данными, используйте литерал map:
```
commits := map[string]int{
    "rsc": 3711,
    "r":   2138,
    "gri": 1908,
    "adg": 912,
}
```

Тот же синтаксис может быть использован для инициализации пустой карты, что функционально идентично использованию функции make:
```
m = map[string]int{}
```

### Эксплуатация нулевых значений

Может быть удобно, что при извлечении карты возвращается нулевое значение, когда ключ отсутствует.

Например, карту логических значений можно использовать в качестве структуры данных, подобной множеству (напомним, что нулевое значение для логического типа равно false). В этом примере выполняется обход связанного списка узлов и вывод их значений. Он использует карту указателей узлов для обнаружения циклов в списке.
```
 type Node struct {
        Next  *Node
        Value interface{}
    }
    var first *Node

    visited := make(map[*Node]bool)
    for n := first; n != nil; n = n.Next {
        if visited[n] {
            fmt.Println("cycle detected")
            break
        }
        visited[n] = true
        fmt.Println(n.Value)
    }
```

Выражение visited[n] истинно, если было посещено n, или ложно, если n отсутствует. Нет необходимости использовать двузначную форму для проверки наличия n в карте; Нулевое значение по умолчанию делает это за нас.

Еще одним примером полезных нулевых значений является карта срезов. При добавлении к нулевому срезу просто выделяется новый срез, поэтому добавление значения к карте срезов — это всего лишь одна строка; Нет необходимости проверять, существует ли ключ. В следующем примере срез people заполняется значениями Person. У каждого человека есть имя и количество лайков. В примере создается карта, связывающая каждую отметку «Нравится» с группой людей, которым она нравится.

```
    type Person struct {
        Name  string
        Likes []string
    }
    var people []*Person

    likes := make(map[string][]*Person)
    for _, p := range people {
        for _, l := range p.Likes {
            likes[l] = append(likes[l], p)
        }
    }
```

Чтобы распечатать список людей, которые любят сыр:
```
    for _, p := range likes["cheese"] {
        fmt.Println(p.Name, "likes cheese.")
    }
```

Чтобы распечатать количество людей, которым нравится бекон:
```
    fmt.Println(len(likes["bacon"]), "people like bacon.")
```

Обратите внимание, что поскольку и range, и len рассматривают нулевой ломтик как ломтик нулевой длины, эти последние два примера будут работать, даже если никто не любит сыр или бекон (как бы маловероятно это ни было).

### Типы ключей

Как упоминалось ранее, ключи карты могут быть любого типа, который можно сравнить. Спецификация языка точно определяет это, но вкратце, сопоставимыми типами являются булевы, числовые, строковые, указательные, канальные и интерфейсные типы, а также структуры или массивы, которые содержат только эти типы. Примечательно, что в списке отсутствуют срезы, карты и функции; Эти типы не могут быть сравнены с помощью == и не могут быть использованы в качестве ключей карты.

Очевидно, что строки, целые числа и другие базовые типы должны быть доступны в виде ключей карты, но, возможно, неожиданными являются ключи структуры. Struct можно использовать для ключевых данных по нескольким измерениям. Например, эта карта карт может быть использована для подсчета посещений веб-страниц по странам:
```
hits := make(map[string]map[string]int)
```

Это отображение строки в (map of string to int). Каждый ключ внешней карты — это путь к веб-странице со своей внутренней картой. Каждый внутренний ключ карты представляет собой двухбуквенный код страны. Это выражение возвращает информацию о том, сколько раз австралиец загрузил страницу документации:
```
n := hits["/doc/"]["au"]
```

К сожалению, такой подход становится громоздким при добавлении данных, так как для любого заданного внешнего ключа необходимо проверить, существует ли внутренняя карта, и при необходимости создать ее:
```
func add(m map[string]map[string]int, path, country string) {
    mm, ok := m[path]
    if !ok {
        mm = make(map[string]int)
        m[path] = mm
    }
    mm[country]++
}
add(hits, "/doc/", "au")
```

С другой стороны, дизайн, использующий одну карту с ключом структуры, избавляет от всей этой сложности:
```
type Key struct {
    Path, Country string
}
hits := make(map[Key]int)
```

Когда вьетнамец заходит на домашнюю страницу, увеличение (и, возможно, создание) соответствующего счетчика состоит из одной строки:
```
hits[Key{"/", "vn"}]++
```

И точно так же легко увидеть, сколько швейцарцев прочитали спецификацию:
```
n := hits[Key{"/ref/spec", "ch"}]
```

### Параллелизм

Карты небезопасны для одновременного использования: не определено, что происходит, когда вы читаете и записываете в них одновременно. Если вам нужно читать и записывать в карту из одновременно выполняющихся горутин, доступ должен быть опосредован каким-либо механизмом синхронизации. Одним из распространенных способов защиты карт является синхронизация. RWMutex.

Этот оператор объявляет переменную счетчика, которая является анонимной структурой, содержащей карту и встроенную синхронизацию. RWMutex.
```
var counter = struct{
    sync.RWMutex
    m map[string]int
}{m: make(map[string]int)}
```

Чтобы прочитать со счетчика, возьмите блокировку чтения:
```
counter.RLock()
n := counter.m["some_key"]
counter.RUnlock()
fmt.Println("some_key:", n)
```

Чтобы записать на счетчик, возьмите блокировку записи:
```
counter.Lock()
counter.m["some_key"]++
counter.Unlock()
```

### Порядок итераций

При итерации по карте с циклом диапазона порядок итераций не указывается и не гарантируется, что он будет одинаковым от одной итерации к другой. Если требуется стабильный порядок итераций, необходимо поддерживать отдельную структуру данных, определяющую этот порядок. В этом примере используется отдельный отсортированный срез ключей для вывода строки map[int] в порядке ключей:
```
import "sort"

var m map[int]string
var keys []int
for k := range m {
    keys = append(keys, k)
}
sort.Ints(keys)
for _, k := range keys {
    fmt.Println("Key:", k, "Value:", m[k])
}
```
