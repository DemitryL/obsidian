Мы уже познакомились с такими классными методами массивов как `map` и `filter`. Они позволяют нам получать новые оригинальные массивы, при этом не меняя старого массива.

Если `map` у нас берет и создает такое же количество массивов, в новом массиве просто преобразуя, каждый элемент массива в что-то новое. 

`Filter` у нас берет и создает новый массив, но усечённый по определенным условиям.

`Reduce` – это нечто, которое может вообще, что угодно. Оно может внутри себя взять
и скомбинировать `map` и `filter`  за одну операцию, за один обход, может нам, обойдя определенную структуру данных, выдать вообще что-то новое, может выдать какой-то объект, может выдать просто число, может выдать просто строку.
На самом деле всё, что угодно, всё, что мы захотим.

Давайте попробуем с ним поработать.
```js
// Reduce
const staff = [
 {
  id: 1,
  name: 'John Doe',
  salary: 1000,
 },
 {
  id: 2,
  name: 'Sara Smith',
  salary: 900,
 },
 {
  id: 3,
  name: 'Elton John',
  salary: 1100,
 },
 {
  id: 4,
  name: 'Mo Williams',
  salary: 1000,
 },
];

const budget = staff.reduce((acc, user) => {
 return acc + user.salary;
}, 0);
console.log(burget);
```
У каждого опять же есть уникальный идентификатор, имя и некая зарплата. Я хочу посчитать некий бюджет. 

Первый параметр будет некий аккумулятор у нас. Он может называться по-разному. 
Я хочу работать с числами, поэтому исходное значение у меня будет 0.  По сути, то, что я передам сюда изначально при первом вызове этой функции, относительно моего нулевого элемента,
метода staff, соответственно, аккумулятор,
мой аккумулятор будет иметь это значение – 0.

Если бы я передал сюда пустой массив,
это был бы пустой массив.

Если бы передал сюда пустой объект,
это был бы пустой объект.

Соответственно, второй, это наш текущий элемент, `user`.  Здесь история такая, что сам по себе `reduce` может быть достаточно сложный по логике. Нам важно, чтобы он всегда нам что-то возвращал. Даже если у нас какие-то условия есть, нам важно, чтобы он что-то возвращал. 
```js
const budgetForSmallPersonal = staff.reduce((acc, user) => {
 if (user.salary < 1000) {
  return acc + user.salary;
 }

 return acc;
}, 0);
console.log(budgetForSmallPersonal);
```
То есть, по сути, в момент первого вызова этого колбэка аккумулятор будет равен 0, в момент второго вызова  этот аккумулятор может измениться, я могу сказать, что аккумулятор плюс текущий user.salary. 

Допустим, у юзера зарплата тысяча, я беру свой ноль, прибавляю к нему тысячу. Для второго элемента моего массива с индексом 1, соответственно, у него аккумулятор придет
уже видоизменённый, здесь уже будет лежать тысяча. 

Нежели я не хочу ничего менять, у меня зарплата,
соответственно, маленькая, я не хочу никак видоизменять общее это значение, я просто его же должен вернуть, то есть аккумулятор всё время
будет присутствовать в нашей логике.

```js
const salaries = staff.reduce((acc, user) => {
 return [...acc, user.salary]
}, []);
console.log(salaries); // [1000, 900, 1100, 1000]
```
Окей, аккумулятором теперь будет такая сущность как массив. Дальше текущий элемент, я буду возвращать, по сути, каждый раз новый массив, это важно для иммутабельности и буду использовать как раз user.salary.  Тем самым у меня будет отдельная сущность, в которой будут просто отдельно, независимо лежать зарплаты, если вдруг это для чего-то требуется.

