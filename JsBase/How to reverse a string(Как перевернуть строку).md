
3 способа перевернуть строку в js

## Способ 1: Использование метода массива reverse()

Для того, чтобы перевернуть строку в обратном направлении нам понадобиться:

1. Преобразуем строку в массив с помощью метода `split('')`, передав в качестве аргумента пустую строку, чтобы каждый символ строки был отдельным элементом массива.
2. Далее используем метод `reverse()`, который меняет порядок элементов массива в обратном направлении.
3. И последним действием собираем из массива строку с помощью метода `join('')`.
```javascript
const str = 'строка';

// Преобразуем строку в массив
const strToArr = str.split(''); // ['с', 'т', 'р', 'о', 'к', 'а']

// Разворачиваем элементы массива
strToArr.reverse(); // ['а', 'к', 'о', 'р', 'т', 'с']

// Преобразуем массив в строку
const newStr = strToArr.join(''); // акортс
```

Также этот способ можно записать в одну строку:
```javascript
const str = 'строка';
const newStr = str.split('').reverse().join(''); // акортс
```

## Способ 2: Использование цикла for

Во втором способе мы воспользуемся циклом `for` и пройдемся по строке начиная с конца, добавляя символы строки в новую переменную.

```javascript
function reverseString(str) {
    let reversed = '';
    for (let i = str.length - 1; i >= 0; i--) {
        reversed += str[i];
    }
    return reversed;
}

const newStr = reverseString('строка'); // акортс
```

## Способ 3: Использование рекурсии

Третий метод использует рекурсию для разделения строки на подстроку без первого символа и добавления этого символа в конец развернутой подстроки.

```javascript
function reverseString(str) {
    if (str === '') { return '' }
    return reverseString(str.substring(1)) + str[0];
}

const newStr = reverseString('строка'); // акортс
```