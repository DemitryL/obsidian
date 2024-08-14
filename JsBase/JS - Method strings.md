**Первый метод - `at`**

Позволяет использовать отрицательный индекс строк и получать элемент с конца строки.

```js
const name = "Alexandr";

console.log(name.at(0)); // A
console.log(name.at(1)); // l

console.log(name.at(-1)); // r
console.log(name.at(-2)); // d
```

Тот же способ получение элемента с конца используя длину строки:
```js
console.log(name[name.length - 1]); //r
console.log(name[name.length - 2]); // d
```

## Методы изменения регистров строк

```js
const text = "КаКоЙтОтЕкСт";
// Изменение к нижнему регистру
console.log(text.toLowerCase());

// Изменения строки к верхнему регистру
console.log(text.toUpperCase());
```

## Методы избовление строки от пробелов вначеле и в конце строки.

```js
const message = " Hello ";

console.log(`Message "${message}" have length ${message.length}`)
```

```js
const messageFormatted = message.trim()

console.log(`Message "${messageFormatted} have lenth ${messageFormatted.length} works`)
```

## Метод получения индекса начала строки indexOf().

```js
const message = "Пробуем найти это выражение"

console.log(
 message.indexOf('это выражение'); // 14
 // Если строки или буквы нет то получаем -1 
 // Обычно такие проверки делают так !== -1
)
```

## Метод получения булевого значения true / false - includes().

```js
const message = "Пробуем найти это выражение"

console.log(
 message.includes('это выражение'); // true
)
```

## Методы  которые проверяют начинается или окончиваетя строка на данные слова - startWith() / endWith().

```js
const message = "Пробуем найти это выражение"

console.log(
 message.startWith('Про'); // true
)
console.log(
 message.endWith('ние'); // true
)
```

### Каждому из последних 4 методов можно передать второй аргумент index с которого будет начинатся поиск.

```js
const message = "Привет"

console.log(message.indexOf('ив', 4)) // -1
console.log(message.includes('ив',  4)) // false
console.log(message.startWith('Пр', 0)) // true
console.log(message.endWith('ет', 3)) // false
```

### Способы обрезки строки или способы получить подстроку из строки.

```js
const str = "JavaScript"

// first method substring() принемает два аргумента начальный и конечный индекс
console.log(str.substring(0, 4)) // "Java"

// Еще один метод который выполняет точно такую же задача - slice()
console.log(str.slice(0, 4)) // "Java"
console.log(str.slice(-6, -3)) // "Scr"
```

### Method repeat() - Возвращает строку указанное количество раз.

```js
const str = "JavaScript"

console.log(str.repeat(3)) // "JavaScriptJavaScriptJavaScript"
```

### Methods для замены построки в строке.

```js
const message = "Я изучаю бэкенд"

// replace() -заменяет первую обнаруженную подстроку, не меняет последующие вхождения
console.log(message.replace("бэкенд", "фронтенд")) // "Я изучаю фронтенд"

// replaceAll() - заменяет все вхождения соотвествующие условию.
console.log(message.replaceAll("бэкенд", "фронтенд"))
```

### Method split() - позваляет разбить строку на массив по указаннаму разделителю.

```js
const str = "Hello, world!"

console.log(str.split(", ")) // ["Hello", "world!"]

console.log(str.split("")) // ["H", "e", "l", "l", "o", ",", " ", "w", "o", "r", "l", "d", "!"]
```



