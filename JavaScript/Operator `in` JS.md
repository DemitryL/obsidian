Работая с объектами иногда нужно проверить есть ли какойто ключ в данном обьекте
```js
const developer = {
  name: "Jeck",
}

console.log('name' in developer); // true
```

Если же ключа нет, то получаем false
```js
console.log('fullname' in developer); // false
```