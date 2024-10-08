Нас может интересовать не просто какое-то действие, нас может интересовать само событие.

Мы можем захотеть проверить, а что произошло, где произошло, при каких обстоятельствах произошло. Для этого у нас тоже есть
определенный инструмент.

У меня на странице есть кнопка, есть поле для ввода.
```html
<body>
<button>Click</button>
<input />
```

Они у меня уже выбраны в мой JavaScript-код, и даже на них я навесил по обработчику.
```js
const btn = document.querySelector('button');
const input = document.querySelector('input');

btn.addEventListener('click', handleEvent);
input.addEventListener('keypress', handleEvent);

function handleEvent(event) {
 console.log(event);
}
```
В случае с кнопкой у меня будет обрабатываться клик. В случае с input будет обрабатываться
нажатие клавиши любой, соответственно, будет вызываться некая функция.

Давайте посмотрим, что же это такой за event и что есть внутри? Часто он называется просто `"e"`,
иногда `evt`, иногда `event`, то есть здесь опять же
это просто название. 

Что там внутри? Когда я кликаю, я вижу, что у меня в качестве event приходит некий объект, причем этот объект является `MouseEvent (событие мышки)`.

У этого события есть определенный набор самых разных вещей. Есть информация о том, в какую
координату был совершен клик. Есть информация о том, что это действительно событие типа клик. 

То есть я могу прям четко понимать, в какую область экрана я кликнул.

Кроме того, если я буду работать теперь с другим элементом. Если я буду работать с клавиатурой и, допустим, нажму на клавиатуре английскую букву A. У меня случится событие клавиатуры.

Кроме того я могу проверить, окей, клавиша A была нажата сама по себе, или она была нажата
с некими спецклавишами. Мне здесь отображается,
нажата ли клавиша Alt, нажата ли клавиша Ctrl,
и нажата ли клавиша Shift.

Опять же я могу на сочетание клавиш какие-то дополнительные проверки делать и всё это дело использовать.

Другая важная штука, с которой мы можем работать, когда дело заходит о событии, это то, что было общего и в `MouseEvent`, и в `Event`, который нашего input касался, эта штука называется `target`.
```js
console.log(event.target);
```

Event target – это наиболее часто используемая штука в связке как раз с Event.

Допустим, у меня есть один input, и я хочу рядышком еще один сделать Мой `querySelector` выберет первый из них, и, допустим, я хочу сделать проверку, что как только я нажимаю
Enter на клавише, я хочу, чтобы фокус переставился
на следующий элемент. 
```js
if (event.key === 'Enter') {
 event.target.nextElementSibling.focus();
}
```

Допустим, у меня могли бы быть, здесь много могло бы быть у меня input.
```html
<div>
 <input />
 <input />
 <input />
 <input />
 <input />
 <button>click me</button>
</div>
```
`querySelectorAll`, я выбрал все input.
```js
const inputs = document.querySelectorAll('input');

inputs.forEach(input => input.addEventListener('keypress', handleEvent));

function handleEvent(event) {
 console.log(event);
 console.log(event.target);

 if(event.key === 'Enter') {
  event.target.nextElementSibling.focus();
 }
}
```
У каждого input будет обрабатываться Enter, и будет делаться focus на следующем элементе. Что получается, я что-то печатаю, нажимаю на Enter, focus сместился. 

Но форма такая хитрая, что если мы обернем наш набор inputs в форму, то здесь может всё пойти
немножко не так. 
```html
<form>
 <input />
 <input />
 <input />
 <input />
 <button>click me</button>
</form>
```
Мы можем нажать на Enter и у нас вроде бы focus переключился, но у нас произошла перезагрузка страницы, потому что форма, она по умолчанию берет и отправляет эту форму, а нам это было не нужно.

Поэтому одна из особенностей этого самого event, как раз связанная с работой, с формой заключается в том, что у любого event, есть также еще штука, связанная с дефолтным поведением браузера. 