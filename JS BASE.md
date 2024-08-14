1. __[[#Типы данных]]__
2. __[[#Приведение типов]]__
3. __[[#Сравнение == и ===]]__
4. __[[#Переменные var, let, const]]__
5. __[[#Функции]]__
6. __[[#Что такое контекст]]__
7. __[[#Прототипы. Prototype]]__
8. __[[#Promise]]__
9. **[[#Async Await]]**
10. **[[#Замыкания в JS]]**
11. **[[#Класс в JS]]**
12. **[[#Методы Массивов]]**

Изучение на сайте [Codewars](https://www.codewars.com/)
Также практикуйся на сайте [Learn javascript](https://learn.javascript.ru/)

- **[[callback-function in JS]]**
- **[[Возврат функций из функций]]**
- **[[Шпаргалка по js]]**
- **[[Как преобразовать строку в массив js]]**
- **[[How to reverse a string(Как перевернуть строку)]]**
- **[[JSON]]**

# top

###  Типы данных 
~~~javascript
// number, string, boolean, object, null, undefined, Symbol

// typeof
console.log(typeof(0)); //number
console.log(typeof('qwe')); //string
console.log(typeof({cat: 1})); //object
console.log(typeof(null)); //object
console.log(typeof(undefined)); //undefined
console.log(typeof(Symbol(description: 1))); //symbol
console.log(typeof(function() {})); //function
console.log(typeof(false)); // boolean
~~~

### Приведение типов

Все что будет переконвертировано в false
~~~javascript
// 0, '', null, undefined, false
~~~
Остальное будет тру. Еще один способ узнать тип данных:
~~~javascript
// Boolean(<name>);
console.log(Boolean('qaw')); //true
console.log(Boolean(0)); //false
console.log(Boolean({})); //true
~~~
При конкатинации идет неявное приведение к строке:
~~~javascript
console.log('1' + 3); // 13
console.log('1' + 3 + 5); // 135
~~~
При арефметических вычислениях идет неявное приведение строк к числу:
~~~javascript
console.log('7' - 3); //4
console.log('9' - 4 - 1); //4
console.log('7' * '3'); //21
console.log('9' / '3'); //3
~~~
Так же :
~~~javascript
// Null преобразуется в 0 и выполняется вычисление 0 + 2
console.log(null + 2); //2
console.log(undefined + 3); //NaN
~~~
##### Особенность типа NaN:
~~~javascript
console.log(typeof(NaN)); //number
~~~

### Сравнение == и ===

== Сравнение по значению, приводит к одному типу: 
~~~javascript
console.log('1' == 1); //true
~~~
=== Строгое сравнение типов:
~~~javascript
console.log('1' === 1); //false
~~~
##### Запомнить:
~~~javascript
console.log(null == undefined); //true
console.log(null === undefined); //false

console.log('0' == false); //true
console.log('0' === false); //false

console.log('0' == 0); //true
console.log('0' === 0); //false

console.log(false == []); //true
console.log(false == {}); //false

console.log('' == 0); //true
console.log('' == []); //true
console.log('' == {}); //false

console.log([] == 0); //true
console.log({} == 0); //false
console.log(null == 0); //false
~~~
### Переменные var, let, const
#### LET
~~~javascript
// Завели переменную а
let a = 10;
// Скопировали значение пременной а в переменную б
let b = a;
// Уменьшили на 1 значение переменной б
b--;
console.log(a, b); // 10 9
~~~
Создание массива
~~~javascript
let a = [1,2,3];
// Присваиваем ссылку на один и тот же массив
let b = a;
b.push(5);
console.log(a, b); // [1,2,3,5]  [1,2,3,5]
~~~
массив и боъект это ссылочные типы данных, при присваивание переменные ссылаются на один и тотже массив, так как копируется лишь ссылка на один и тотже обьект. В иттоге при изменении по переменным меняется сам первоночальный обьект.
#### CONST
~~~javascript
const a = 1;
a = 5; // Выдаст ошибку так как переменную обьявленную с помощьб const изменять нельзя

// Можно изменять массив и обьект обьявленный при помощи const методами
const a = [1, 2];
a.push(7);
console.log(a); // [1,2,7]
// Но переприсваивать переменную напремую через знак равенства нельзя
a = [1,2,3,4];

const b = {
  cat: '1'
};
// удалим свойство у обьекта
delete b.cat;
console.log(b); // {} получаем пустой обьект
~~~
#### VAR
~~~javascript
// Здесь происходит такое понятие как всплытие, этим var отличается от const , let
console.log(a); // undefined

var a = 1;
a = 3;
console.log(a); //3

// при токой запись мы получим ошибку, мы пытаемся обратится к переменной которая еще не была иницилизирована. У let, const видимость только после обьявления.
console.log(c);
console.log(b);
let c = 3;
const b = 1;
~~~
У let, const видимость блочная :
~~~javascript
let a = 1;
let b = 2;

if (true){
  a = 7;
  // К переменной объявленной внутри блока есть доступ только внутри этого блока.
  let b = 9;
  console.log('b', b);
}

console.log(a, b);
~~~

### Функции

Функции задаются следующим образом:
~~~javascript
// a, b, c - аргументы
function sum(a, b, c){ 
  return a + b + c;
}
console.log(sum(1, 2, 3)); // 6
~~~

Задать функцию можно другим способом, присвоев ее переменной:
~~~javascript
const sum = function(a, b, c){
  return a + b + c;
}

console.log(sum(1, 2, 3));
~~~

Функции объявленные таким способом, мы к ним имеем доступ только после объявления. В ином случае мы получим ошибку:
~~~javascript
console.log(sum(1, 2, 3)); // ReferenceError: Cannot access 'sum'

const sum = function(a, b, c){
  return a + b + c;
}
~~~
В случае первого варианта при обьявлении функции заранее, мы ошибки не увидим. Называется это понятие хоистинг (всплытие - поднятие переменных)

~~~javascript
console.log(sum(1, 2, 3)); // 6

function sum(a, b, c){ 
  return a + b + c;
}
console.log(sum(1, 2, 3)); // 6
~~~

Javascript - при нахождении данных конструкций он их выносит наверх документа и мы имеем доступ к ним в любом месте файла.


### Что такое контекст

Контекст this :
~~~javascript
let user = {
  name: 'John',
  age: 35,

  sayHello() {
   console.log('Hi');
  }
}

user.sayHello(); // Hi
~~~

Обращение к полю объекта: 
~~~javascript
let user = {
  name: 'John',
  age: 35,

  sayHello() {
   console.log(this.name);
  }
}

user.sayHello(); // John
~~~

```javascript
let user = {
 name: 'John',
 age: 35,
}

let animal = {
 name: 'rabbit',
 age: 5,
}

function sayHello() {
 console.log(this.name);
}

user.f = sayHello;
animal.f = sayHello;

// Обращаемся к метадам этих объектов
user.f(); // John
animal.f(); // rabbit
// Правельная установка this происходит только при таком вызове объекта
```

~~~javascript
let hi = user.f;
// метод hi() вызывается без привязки к этому объекту, поэтому выдаст undefind
hi(); // undefind
~~~

Стрелочные функции и this :
```javascript
let user = {
 name: 'John',
 age: 35,

 sayHi() {
  let arrowFunc = () => {
   console.log(this.name);
  }
  // Сразу же вызываем функцию
  arrowFunc();
 }
}

// Вызываем метод sayHi
user.sayHi(); // John
```

Это работает потому что у стрелочной функции нет собственного this, и если мы используем this внутри стрелочной функции, то его значение будет браться из внешней нормальной функции, тоесть из sayHi . Не зависимо от вложенности стрелочных функций даже если бы их было 10 вложенных друг в друга , то значение this все равно в итоге бралось из нормальной функции.

Привязка контекста :
```javascript
let user = {
 name: 'John',
 age: 35,

 sayHi(hiWord) {
  console.log(`${hiWord} ${this.name}`)
 }
}

let animal = {
 name: 'rabbit',
}

// Вызываем метод sayHi получая имя из другого объекта
// Используем для этого 3 способа

// Первый call, (первый аргумент - объект который станет в итоге this, далее передаем аргументы через запятую столько сколько нужно)
user.sayHi.call(animal, 'Heeey'); // Heeey rabbit

// Второй похожий метод apply, делает он все тоже самое
// (первый аргумент - объект который станет в итоге this, далее передаем аргументы в массиве через запятую столько сколько нужно)
user.sayHi.apply(animal, ['Heeeey']); // Heeeey rabbit

// Третий bind, здесь есть особенность bind возвращает новую функцию и ее необзодимо принудительно еще вызвать
user.sayHi.bind(animal, 'hihi')(); // hihi rabbit

```

### Прототипы. Prototype

Прототипная модель в JS :
~~~javascript
let animal = {
 eats: true,
};

let rabbit = {
 jumps: true,
};

// получаем доступ к animal через объект rabbit, данной записью мы говорим что для объекта rabbit прототипом является объект animal:
rabbit.__proto__ = animal;

console.log(rabbit.eats); //true
~~~

  Еще один способ создания прототипа :
~~~javascript
let animal = {
 eats: true,
 name: 'animal',
 walk() {
  console.log(this.name);
 }
};

function Rabbit(name) {
 this.name = name
}

// Добавляем свойство прототайп 
Rabbit.prototype = animal;

// Создали новый инстанс с помощью ключевого свойства new
let rabbit = new Rabbit('Igor');

console.log(rabbit.walk()); // Igor
console.log(animal.walk()); // animal
~~~
    В качестве this при вызове метода объекта, устанавливается        объет стоящий перед точкой

Пройтись по свойствам объекта : 
~~~javascript
// for in
// Выведим свойства объекта rabbit
for (let prop in rabbit){
 // выедем ключи свойств
 console.log(prop); // name, eats, walk
}
// eats, walk свойства которые пришли благодаря прототипному наследованию
~~~
Ну что если нам нужно получить свойста конкретно самого объекта rabbit, а не его прототипов :
~~~javascript
for (let prop in rabbit){
 // воспользоваться встроенным методом объекта hasOwnProperty()
 if (rabbit.hasOwnProperty(prop)){
  console.log(prop); // name
 }
}
~~~
Второй способ:
~~~javascript
console.log(Object.keys(rabbit)); // ['name']
console.log(Object.values(rabbit)); // ['Igor']

// Метод который возвращает массив массивов, где внутренний элемент состоит из ключа и значения
console.log(Object.entries(rabbit)); // [ ['name','Igor'] ]
~~~
### Promise
Promise in JS
~~~javascript
const promise = new Promise(function(resolve, reject){
 setTimeout( () => {
  resolve('success');
 }, 2000)
});

promise.then(response => {
 console.log(response); // success
})

////////

const promise = new Promise(function(resolve, reject){
 setTimeout( () => {
  reject(new Error('error'));
 }, 2000)
});

promise
 .then(response => {
  console.log(response); // success
 })
 .catch(error => {
  console.log(error); //Error: error
 })
~~~

**Встроенные методы promise :**
resolve - вызывается в случае успеха
reject - в случае ошибки

~~~javascript
const url1 = 'https://yandex.ru';

const promise = fetch(url1);

promise
 .then(response => response.json())
 .then(response => {
  console.log(response);
 })
 .catch(error => {
  console.log(error);
 });
~~~
В итоге при битой  ссылке менуем блоки then и выводится блок с ошибкой catch

Несколько запросов к серверу одновремменно
Цепочки промисов :
~~~javascript
const url2 = 'https://api.github.com/users';

const promise = fetch(url2);

promise
 .then(response => response.json())
 .then(commits => {
  console.log(commits);

  const login = commits[0].author.login;
  return fetch(`${url2}/${login}`)
 })
 .then(user => user.json())
 .then(user => {
  console.log(user);
 })
 .catch(error => {
  console.log(error);
 });
~~~
В итоге получаем данные о пользователе.

Также у промиса ест ь еще один метод который вызывается всега пр и завершении промися, не зависимо от того с каким результатом завершился промис
~~~javascript
.finally(() => {
  console.log('finally'); // finally
})
~~~

Метод обрабатывающий промися последовательно
~~~javascript
const promise = fetch(url1);
const promise2 = fetch(url2);

Promise
 .all([promise, promise2])
 .then(result => {
  console.log(result);
 }, error => {
  console.log(error);
 })
~~~
Метод all будет ожидать пока каждый из промисов не выполница, выполнится корректно,  в случае если при выполнении хотябы у одного из промисов произошда ошибка, то мы поподем уже во второй колбек и в данном случае мы увидем ошибку с которой этот запрос упал 

Еще один из методов __race__, он выводит результат наиболее быстро выполнившегося промися и не важно что это ошибка или результат
~~~javascript
Promise
 .race([promise, promise2])
 .then(result => {
  console.log(result);
 }, error => {
  console.log(error);
 })
~~~
### Async Await
Async & await in JS
Решаем задачу с двумя последователями запросами к серверу с помощью  промисов 

Получение коммитов из репозитория
~~~javascript
const url1 = 'https://api.github.com/commits';
~~~
Получение логина
~~~javascript
const url2 = 'https://api.github.com/users';
~~~
~~~javascript
const promise = fetch(url1);

promise
 .then(response => response.json())
 .then(commits => {
  console.log(commits);

  const login = commits[0].author.login;
  return fetch(`${url2}/${login}`);
 })
 .then(response2 => response2.json())
 .then(user => {
  console.log(user);
 })
 .catch(error => {
  console.log(error);
 })
~~~

Тотже запрос при помощи Async & Await
~~~javascript
async function getUser() {
 try{
  // Получили тело ответа
  let commits = await fetch(url1);
  // Преобразовали его
  commits = await commits.json();

  console.log(commits);

  const login = commits[0].author.login;
  let user = await fetch(`${url2}/${login}`);
  user = await user.json();

  console.log(user);
 } catch(e) {
  // Вывод ошибок
   console.log(e);
 } finally {
  // Finally выполняется всегда
   console.log('finally');
 }
}

getUser();
~~~

### Замыкания в JS
"Замыкание" - это способность функции запоминать переменные, которые были определены внутри родительской функции, даже после того, как родительская функция была выполнена. Подробнее можно почитать по **[ссылке](https://itchief.ru/javascript/closure)**

1 -  Task 
~~~javascript
function makeCounter() {
 let count = 0;

 return function () {
  count++;
  console.log(count);
 }
}

// При каждом новом вызове майкКоунтер мы создаем новоем лексическое окружение для внутренней функции. Поэтому переменная сounter при инициализации будет равна нулю.
let counter = makeCounter();
let counter2 = makeCounter();

counter(); // 1
counter(); // 2

counter2(); // 1
counter2(); // 2
~~~
В этом примере мы создали функцию `makeCounter()`, которая создает другую функцию `()`. Внутри функции мы создали переменную `count`, которая была определена внутри родительской функции. Функция `()` возвращает значение `count`, увеличивая его на `1`. Когда мы вызываем `makeCounter()`, она возвращает функцию `()`, которая имеет доступ к `count` благодаря замыканию. Каждый раз, когда мы вызываем `counter()`,

Если мы создадим новый счетчик с помощью функции `makeCounter()`, то отсчет для него начнется заново.


2 - Task 
~~~javascript
// sum(2)(4) = 6 Функция которая будет возвращать сумму

// переменная а которая является замыканием
function sum(a) {
 return function (b) {
  return a + b;
 }
}

console.log(sum(2)(5));  // 7
~~~

~~~javascript
// Функция которая будет прибавлять 2 к кокомуто числу
const plusTwo = sum(2);

console.log(plusTwo(6));
~~~
3 - Task
~~~javascript
let garage = [
 {
  car: 'mazda',
  count: 3
 },
 {
  car: 'porsche',
  count: 1
 },
 {
  car: 'nissan',
  count: 4
 }
];

// Отсортировать массив по ключам
let sortedByCar = [...garage.sort((a, b) => a['car'] > b['car'] ? 1 : -1)];
console.log(sortedByCar); // {car: 'mazda'},{car: 'nissan'},{car: 'porsche'}

let sortedByCount = [...garage.sort((a, b) => a['count'] > b['count'] ? 1 : -1)];
console.log(sortedByCount); // {count: 1}, {count: 3}, {count: 4}
~~~

~~~javascript
function byField(field) {
 return (a, b) => a[field] > b[field] ? 1 : -1;
}

function byField(field) {
 return function(a, b) {
  return a[field] > b[field] ? 1 : -1;
 };
}

let sortedByCar = [...garage.sort(byField('car')];
console.log(sortedByCar);

let sortedByCount = [...garage.sort(byField('count')];
console.log(sortedByCar);
~~~
### Класс в JS
> В объектно-ориентированном программировании _класс_ – это расширяемый шаблон кода для создания объектов, который устанавливает в них начальные значения (свойства) и реализацию поведения (методы).

**[Классы](https://learn.javascript.ru/classes)** появились в Es6, Нужны они для более удобной реализации объекьно оренторованного подхода. Изначально в Js ООП реализуется с помощью прототипов и прототипного наследования. Классы нам предоставляют немного другой синтаксис более удобный. Сам механизм реализации очень схож с прототипным ООП, но есть ряд важных отличий.

Для того чтобы реализовать класс пишем:
~~~javascript
class CoffeeMachine {
// constructor в который передаем параметры которые будут переданы в свойства данного обьекта
 constructor(coffee) {
 // присваеваем это переданное значение
  this.coffee = coffee;
 }

// метод класса 
 addCoffee(amount = 10){
  // this.coffee += amount ? amount : 10;
  this.coffee += amount;
 }
}

// Создаем экземпляр нашего класса
let cm1 = new CoffeeMachine(25);
cm1.addCoffee(); // 35
~~~
Свойства которые мы создаем в конструкторе они добавляются как  свойства обьекта. Все методы класса в итоге добавляются в прототип.

Иногда нам необходимо контролировать доступ к свойствам класса для этого использую гетторы и сетторы. Например для того чтобы валидировать значение и не допускать записи невалидного значения.
~~~javascript
class CoffeeMachine {
// Метод constructor — специальный метод, необходимый для создания и инициализации объектов, созданных, с помощью класса. В классе может быть только один метод с именем `constructor`. Исключение типа SyntaxError будет выброшено, если класс содержит более одного вхождения метода constructor.

 constructor(coffee) {
  this.coffee = coffee;
 }

 get coffee() {
  return this._coffee;
 }

 set coffee(value) {
  if (value < 5) {
   alert('Error, value < 5');
   return;
  }
  this._coffee = value;
 }

 addCoffee(amout = 10) {
  this.coffee += amout;
 }
}

let cm1 = new CoffeeMachine(25);
~~~
Статические методы.
~~~javascript
// метод который будет сравнивать по количеству кофя
static compareByCoffeeAmount(c1, c2) {
 return c1.coffee - c2.coffee;
}

let cm1 = new CoffeeMachine(15);
let cm2 = new CoffeeMachine(11);
let cm3 = new CoffeeMachine(25);

const sorted = [cm1, cm2, cm3]
 .sort(CoffeeMachine.compareByCoffeeAmount);
console.log(sorted);
~~~
Статические свойства.
~~~javascript
static power = 100;
~~~
Суть статических методов и свойств, что они относятся конткретно к классу, а не к инстансу, тоесть в нутри инстансов cm1, cm2, cm3 этих свойств не будет, эти свойства нужны конкретно с целым классом сущностей.

Приватные свойства: 
~~~javascript
#madeIn = 'China';
~~~
Суть приватных свойств заключается в том что они доступны только в нутри класса и не доступны из вне, тоесть в экземпляре нашего класса мы уже доступ к данному свойству мы иметь не будем.

## Методы Массивов

~~~javascript
const blogComments = [
 {userId: 10, text: 'Text 1', likes: 23, retweets: 9, tag: 'food'},
 {userId: 11, text: 'Text 2', likes: 31, retweets: 14, tag: 'new'},
 {userId: 12, text: 'Text 3', likes: 14, retweets: 6, tag: 'sport'},
 {userId: 13, text: 'Text 4', likes: 2, retweets: 0, tag: 'economy'},
 {userId: 14, text: 'Text 5', likes: 15, retweets: 3, tag: 'new'},
 {userId: 15, text: 'Text 6', likes: 33, retweets: 11, tag: 'food'},
 {userId: 16, text: 'Text 7', likes: 53, retweets: 19, tag: 'sport'},
 {userId: 17, text: 'Text 8', likes: 1, retweets: 1, tag: 'food'},
 {userId: 18, text: 'Text 9', likes: 0, retweets: 0, tag: 'economy'},
];
~~~
	Проход по массиву простым способом:
~~~javascript
for (let i = 0; i < blogComments.length; i++) {
 // выводим в консоль все элементы
 console.log(blogComments[i]);
}
~~~
##### 1.  Перебор элементов массив. 1. forEach :
~~~javascript
// forEach принемает в себя функцию, которая в свою очередь принемает три арумента( текущий элемент массива, индекс этого элемента, сам исходный массив)
blogComments.forEach((item, index, array) {
 // выводим элементы по которым идем
 console.log(item)
});
// Как правило третий аргумент используется крайне редко, обходимся первыми двумя.
// Метод forEach ничего не возвращает даже если использовать return. Этот медод нужен для того чтобы просто пройтись по элементам массива
~~~
Перепишем внутрению функцию на стрелочную и в дальнейшем используем стрелочные функции.
~~~javascript
blogComments.forEach((item, index) => {
 console.log(item);
});
~~~
##### 2. Методы для поиска элементов массива : 2. filter / every / some  // 3. find / findIndex :

Method **filter** :
~~~javascript
const filtered = blogComments.filter((item) => {
 // выборка элементов по условию
 return item.likes >= 15;

 // вывод элементов в которых есть буква 'w'
 return item.tag.indexOf('w') > -1;
});
console.log(filtered);
~~~
Method **every** : работает следующим образом возвращает булевые значения
~~~javascript
const filtered = blogComments.every((item) => {
 // соотвествует условию если так то вернет true иначе false
 return item.likes >= 0; 
});
console.log(filtered); // true
~~~
Method **some** : проверяет соответствует ли хотябы один элемент заданному условию, если это так то вернет true, если же не один элемент не соответствует то вернет false :
~~~javascript
const filtered = blogComments.some((itme) => {
 return item.retweets >= 19;
});
console.log(filtered); // true
~~~
Method **find** : возвращает первый элемент который удовлетворяет условию:
~~~javascript
const found = blogComments.find((item) => {
 // количество ретвитов больше или рано 12
 return item.retweets >= 12;
});
console.log(found);
~~~
Method **findIndex** : возвращает индекс элемента который удовлетворяет условию :
~~~javascript
const found = blogComments.findIndex((item) => {
 return item.retweets >= 12;
});
console.log(found); // 1
~~~
##### 3. Методы преобразования массива : 4. map /  5. sort  / 6. reduce

Method **map** : возвращает нам новый массив из элементов из условий  записаных в теле функции
~~~javascript
const mappedArray = blogComments.map((item) => {
// создаем обьект с сохранением поля userId и добавлением поля суммой лайков и ретвитов
 const changedElement = {
  userId: item.userId,
  actions: item.likes + item.retweets
 };
 // на выходе ожидаем получить массив с данными полями остальные нас не интересуют
 return changedElement;
});
~~~
Method **sort** : для сортировке массива по каким либо критериям. Устроен следующим образом принемает в себя функцию которая принемает в себя два аргумента (item1, item2) между которыми происходит какоето сранение.
~~~javascript
// method sort изменяет сам массив blogComments
blogComments.sort((item1, item2) => {
 // сортировка по возрастанию
 return item1.likes - item2.likes;
});
console.log(blogComments);
~~~

~~~javascript
blogComments.sort((item1, item2) => {
 if (item1.tag > item2.tag) {
  return 1;
 }

 if (item1.tag < item2.tag) {
  return -1;
 }

 return 0;
});
console.log(blogComments);
~~~
Method **reduce** : метод полезен когда нужно сагрегировать информацию из массива и вернуть кокоето значение. Принемает данный метод функцию которая принемает в себе четыре аргумента ( аккумулятор, текущее значение(текущий элемент), индекс текущего элемента, сам массив с которым работаем ), последние два аргумента являются необязательными.
~~~javascript
// const reduced = blogComments.reduce((acc, current, index, array) => {})

const reduced = blogComments.reduce((acc, current) => {
 // складываем лайки
 acc += current.likes;
 return acc;
}, 0); // изначальное значение acc = 0
console.log(reduced); // 172
~~~
###### Выполнение методов друг за другом последовательно.
~~~javascript
const reduced = blogComments.map((item) => {
 const changedElement = {
  userId: item.userId,
  actions: item.likes + item.retweets
 };

 return changedElement;
}).reduce((acc, item) => {
 acc += item.actions;
 return acc;
}, 0);
console.log(reduced);
~~~

## Event Loop
( Асинхронность )



[[#top]]
-----
