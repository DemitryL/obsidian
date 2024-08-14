У меня есть немножко стилей, есть просто кнопка,
и есть элемент на странице.
```html
<head>
<style>
button{
 padding: 0.5rem 0.8rem;
 font-size: 1.2rem;
}
.element {
 width: 100%;
 font-size: 1.2rem;
 padding: 50px 0;
 text-align: center;
 background-color: lightblue;
 margin-top: 20px;
}
.hide{
 display: none;
}
</style>
</head>
<body>

<button id="toggle-btn">Toggle visibility</button>

<div class="element">This is my DIV element</div>
<script src="main.js"></script>
</body>
```
Мне нужно в JavaScript выбрать оба этих элемента и привязать некую логику для работы с ними.

```js
const btn = document.getElementById('toggle-btn');
const div = document.querySelector('.element');
```
Мне нужен обработчик клика и здесь у меня опционально: либо я могу через объект стилей открывать эту сущность, говорить display none,
```js
function toggleDivVisibility() {
 if (div.style.display === 'none') {
  div.style.display = 'block';
 } else {
  div.style.display = 'none';
 }
}
```
либо я могу класс добавлять. Он будет либо добавлять наш class hide, либо будет его снимать.
```js
function toggleDivVisibility() {
 div.classList.toggle('hide')
}
```

И обработчик на саму кнопочку, я обращаюсь к моей кнопке, я говорю: `addEventListener`,
добавь на событие клика ту функцию, которую я только что написал.
```js
btn.addEventListener('click', toggleDivVisibility);
```
