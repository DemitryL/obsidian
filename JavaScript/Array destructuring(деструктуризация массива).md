Мы подошли к такой интересной теме
как `Destructuring`.  Иногда ее называют
деструктурирующее присваивание или завлекающее присваивание. 

Она есть не только в JavaScript, в других языках тоже. Появилась она относительно недавно.
```js
const cities = ['Madrid', 'Amsterdam', 'Paris', 'Berlin', 'Kiev'];

const [madrid, amst, paris] = cities;
console.log(madrid, amst, paris); // Madrid Amsterdam Paris
```
Просто привыкаем к тому, что мы после объявления либо константы, либо через let-переменные, пишем не сразу имя, потом равно, а пишем сначала квадратные скобки и уже внутри мы пишем имена переменных.

Что ожидаю, что внутри квадратных скобок я создал переменную `madrid`, и значением этой переменной однозначно стал нулевой индекс, значение нулевого индекса от массива, который стоит у меня справа от знака равенства.

------
Во-первых, мы можем захотеть что-то пропустить, сказать, окей, мне нужен только первый и третий элемент или, может, первый, третий и пятый,
мне не нужен Amsterdam и Berlin.

Как мне быть в данном случае?
Ничего страшного, я каждый раз, когда мне нужно что-то пропустить, просто беру и ставлю лишнюю запятую, и у меня будет пропуск.
```js
const [madrid, , paris, , kiev] = cities;
console.log(madrid, paris, kiev); // Madrid Paris Kiev
```
И видим, что действительно содержимое пропустило Amsterdam, пропустило Berlin, но другие города попали в соответствующие переменные ровно в том порядке, который я задал.

Здесь же мы можем использовать такую же штуку, которую мы смотрели с вами в прошлый раз, связанную с rest-оператором.

Мы можем сказать, что создай две переменные, а третью назови хвост-tail, это распространенное название, и сохрани в нее всё то, что ты
не положил в эти две переменные, в те переменные, которые идут до этого.
```js
const [madrid, ams, ...tail] = cities;
console.log(madrid, tail); // Madrid [ 'Paris', 'Berlin', 'Kiev' ]
```
Причем мы гарантировано получаем здесь массив, Опять же, если мы выбрали все элементы из массива, этот массив будет просто-напросто пустым, и мы обязательно должны писать его последним.

То мы не можем написать его в начале, в середине, 
обязательно должны написать его последним. 

На самом деле в функции то же самое. Если мы используем оператор остатка функции, там тоже он должен идти последним, после всех аргументов.

Здесь есть следующий нюанс, заключающийся в том, что мы можем всю эту историю писать очень аккуратно, разнося по строчкам, так чаще всего
оно на самом деле и бывает. 
```js
const [
 madrid,
 ams,
 ...tail
] = cities;
```
Но хочу сказать о другом, у нас здесь идут запятые, и современный JavaScript позволяет нам
после последнего элемента массива или объекта ставить запятую, это не является ошибкой, это нормально.

Но если мы используем `Destructuring` и последний метод используется у нас как некая такая собирательная единица, то после нее запятая не ставится, запятая в данном случае может рассматриваться как ошибка.

-----
Зачем разносить по строчкам. Нам может понадобиться написать какие-то значения по умолчанию. 
```js
const [
 madrid = '',
 ams = '',
 ...tail
] = cities;
```
Почему так может происходить? Зачастую, работая с данными, в нашем приложении мы не знаем, что будет внутри. Что-то приходит с сервера, что-то зависит от того, какие действия воспроизводит пользователь у нас на сайте.

Что если вдруг `cities` по какой-то причине пришел, допустим, сервер со значением `null`, по какой-то причине, неизвестно, вот такой у нас `cities`, у нас, по сути, без вот этой части
JavaScript, приложение упадет.

Он скажет: невозможно сделать `Destructuring` из `null`, такого не бывает. 
```js
const cities = null;

const [
 madrid = '',
 ams = '',
 ...tail
] = cities || [];
```
Ежели мы гарантируем, что если здесь у нас undefined либо null, то мы пойдем по умолчанию
пойдем по ветке или и присвоим `Destructuring` от пустого массива. 

-----
Окей, у нас могут быть вложенные массивы. Допустим, здесь у нас есть некий numbers, и в numbers может быть какая-то вложенная штука.
```js
const numbers = [1, 2, [3, 4], 10, 12, 23];
const [a, b, c] = numbers; // 1 2 [3, 4]
```
Это нормально, мы можем захотеть и его тоже как-то деструктурировать. Тогда мы можем сделать
вложенную историю. 
```js
const [
 a,
 b,
 [c, d]
] = numbers;
console.log(a, b, c, d); // 1 2 3 4
```

Разумеется, в данной истории мы тоже можем захотеть иметь, значение по умолчанию, поэтому
в некоторых случаях мы можем сделать себе вот такую защиту.
```js
const [
 a = 0,
 b = 0,
 [c = 1, d = 1] = [],
] = numbers || [];
```
Мы говорим, если не существуют нулевого индекса, пускай по умолчанию он будет ноль,
если не существует второго, пускай по умолчанию он будет ноль. Если не существует третьего индекса, пускай по умолчанию он будет
пустой массив. 

Если же мы хотим поменять что-то местами, ничего страшного, мы используем уже
существующие переменные, здесь мы не создаем новую, здесь у нас не используются
готовые значения, мы точно также, как в случае
`Destructuring` говорим:
```js
let x = 10;
let y = 20;
[y, x] = [x, y];

console.log(y, x); // 10 20
```
Скажем, console.log у, х. "y" будет 10, "х" будет 20. 10, 20 было. "y" был 20, теперь "y" 10. "х" был 10, теперь "х" 20. 

Вот так вот взяли их и поменяли местами. 