Первый вариант, соответственно, у нас называется Function Declaration (декларация функции) либо просто объявление функции.
```js
// 1. Function Declaration
function sum(a, b) {
 return a + b;
}
```

Вторая штука, она как и первый вариант записи функции, существует достаточно давно, называется она Function Expression. Соответственно, эта штука называется
функциональным выражением.
```js
// 2. Function Expression
const sum = function (a, b) {
 return a + b;
}
```

Следующая штука, это даже не способ записи функций, это некий паторн, он называется IIFE. Опять же можем эту штуку расшифровать, она называется Immediately-invoked function expression.

По сути, это та же самая функция, но то же самое функциональное выражение, которое мы только что видели,
но с тем отличием, что она сразу же вызывается.
```js
// 3. IIFE(immediately-invoked function expression)
(function(a, b) {
 return a + b;
})(3, 6)
```

Четвертый вариант – это то, что появилось у нас в 2015 году. Это то, что у нас называется Arrow function.
```js 
// 4. Arrow function 
const sum = (a, b) => {
 return a + b;
}
////////
const sum = (a, b) => a + b;
```