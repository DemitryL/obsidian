Зададим простой список дел, но для этого нам понадобится научиться динамически добавлять или удалять элементы со страницы.
```html
<body>
 <h1>DOM API</h1>
 <div>
  <input type="text" placeholder="todo">
  <button>Add Task</button>
 </div>
 <ul id="todos"></ul>
</body>
```

У меня на страничке есть поле для ввода, кнопка и место, куда я планирую вводить элементы
списка дел.

В данном случае я планирую, что я буду забивать какой-то текст, нажимать на клавишу, и этот текст
будет добавляться в этот список, потом при необходимости по клику на элемент я смогу его удалять.

```js
const list = document.getElementById('todos');
document.querySelector('button').addEventListener('click', handleClick);

function handleClick() {
 const newTodo = this.previousElementSibling.value.trim();

 if(newTodo) {
  // add todo
  createTodo(newTodo);
  this.previousElementSibling.value = '';
 } else {
  alert('input field is empty');
 }
}

function createTodo(text) {
 const li = document.createElement('li');
 li.innerText = text;
 li.className = 'todo-item';
 li.addEventListener('click', removeTodo);

 list.append(li); 
}
```
Мы помним, что когда мы работаем с объектами, если у объектов есть метод, то этот метод имеет встроенный this. Этот this однозначно указывает
на сам объект.

Если наша функция вызывается при клике на кнопку, this будет указывать на кнопку. Если функция вызовется при клике на список, this будет ссылаться на список, на элемент списка.

Таким образом мы можем создавать абсолютно любые элементы и очень удобно оборачивать
эту логику в отдельные функции.

Естественно, раз мы можем создавать элементы,
мы можем их и удалять.
```js
function removTodo() {
 this.removeEventListener('click', removeTodo);
 this.remove();
}
```
Для удаления у нас тоже есть отдельный метод.