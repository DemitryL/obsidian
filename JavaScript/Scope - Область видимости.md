При работе с функциями одно из важных понятий называется область видимости. На английском звучит как Scope. 
```js
// Scope 
function isString(str) {
 const isValid = typeof str === "string";
 return isValid;
}
const res = isString('123');
```

То есть, по сути, все переменные, которые мы создаем внутри нашей функции, они являются локальными. 
Локальные переменные, которые мы создаем внутри либо через const, либо через let. Вне функции мы не можем к ним обратиться.

Мы не можем дважды объявить переменную с одним названием. Но внутри функции у нас есть отдельная память, локальная. В ней мы можем, что угодно, мы можем
создавать переменные с любыми названиями, некое такое замкнутое пространство.