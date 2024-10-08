Методов в массивах очень много.
Мы знаем с вами метод `pop`, эта штука удаляет у нас
из массива последний элемент.

Мы знаем метод `push`. Он, соответственно, добавляет элементы в конец массива.

Точно также у нас есть методы `shift` и `unshift`
Они делают то же самое, только наоборот. Соответственно, добавляют в начало или удаляют из начала.

Из того, что нам будет часто пригождаться, это тот же самый метод `includes`.
```js
const numbers = [1, 2, 3, 4, 5];
numbers.includes(4); // true
```
Вот он будет смотреть, если это значение есть, он нам будет возвращать истину (true).

```js
console.log(numbers.indexOf(2)); // 1
```
Индекс of опять же – это поиск элементов,  поиск его индекса.  Если мы индекс найдем, мы получим,
соответственно, номер индекса. В данном случае это будет 1.

Если мы индекс не найдем, мы получим -1.

Да, если мы  будем искать число 9, мы получим -1, потому что такого индекса не существует.
```js
console.log(numbers.indexOf(9)); // -1
```

Точно также, как и в строках. У нас есть метод,
который называется `slice`.
То же самое он делает, это срез.
```js 
console.log(numbers.slice(0, 2)); // [1, 2]
```
Соответственно, нулевой, первый, второй, второй мы не включаем, хочу два значения. Получается, я здесь ожидаю получить новый массив, соответственно, один и два значения. 

Старый массив останется таким же, каким был изначально.
Новый массив – новая область памяти.

Никакого сохранения по ссылке не происходит. В данном случае мы просто создаем новую область памяти. Соответственно, эту сущность можно сохранить в другую переменную, а эта новая переменная никак не будет связана со старой.

Часто бывает, можно создать новый массив, например, `nums 2`, и мы можем использовать метод `concat`.
```js 
const num2 = numbers.concat([6, 7, 8]);

console.log(num2); // [1, 2, 3, 4, 5, 6, 7, 8]
```
`Concat` – это та же самая конкатенация. Здесь мы можем к исходному массиву сконкатенировать какой-нибудь
новый массив.
Мы сюда можем передать либо как переменную дополнительный массив, либо прям вот так вот просто
дать ему еще какой-то массив.

При этом, если мы посмотрим оригинальный тип numbers,
в нем как было четыре числа, так и осталось.

Соответственно, методом `join` мы получаем строку с каким-то разделителем.
```js
console.log(numbers.join(', ')); // 1, 2, 3, 4
```
Я получу строку со всеми моими элементами массива, разделенными, соответственно, запятой и пробелом.











 



