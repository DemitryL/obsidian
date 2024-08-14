Загадка
```html
<body>
 <h1>Угадай загадку</h1>
 <p id="riddle"></p>
 <p><small>Дайте 3 попытки.</small></p>
 <div>
   <input placeholder="ответ" autofocus>
   <button onclick="check()">Прверить</button>
 </div>

 <script src="main.js"></script>
</body>
```

```js
const riddle = {
 question: 'Висит груша нельзя скушать',
 currontAnswer: 'лампочка',
 hints: ['это съедобное', 'это фрукт'],
 tries: 3,
 checkAnswer() {},
}

window.onload = function() {
 document.getElementById('riddle').innerText = riddle.question;
}

function check() {
 const input = document.getElementsByTagName('input')[0];

 const guessedAnswer = input.value;

 if(guessedAnswer) {
   
 }
}
```