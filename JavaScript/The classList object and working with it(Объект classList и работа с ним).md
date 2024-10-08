Вот, например, у нас есть элемент на странице, мы видим у него за раз аж четыре CSS-class.
```html
<p class="top name gerb grid">text</p>
```

Мы будем обращаться к нему через `classList`, это некий специальный массив, опять же массивоподобная история, называется он `DOMTokenList`, и он содержит здесь все эти элементы.
```js
const p = document.querySelector('p');
p.classList.add('active');
```
Так как это специальный массив, мы можем с ним работать через определенные методы. Во-первых, мы можем в любой момент добавлять туда
новые классы, используя метод `add`.

Раз я могу что-то добавлять, я могу это обязательно и удалять.
```js
p.classList.remove('active');
```

Можем добавлять, можем удалять, а значит, можем еще и проверять, есть ли там что-то уже.
Допустим, проверить, а есть ли у тебя
`class active` или нет?
```js
p.classList.contains('active');
```
Он мне вернет false или true. Соответственно, false, если чего-то нету.

Бывает так, что нам нужно что-то включать и выключать, и проверять, есть сейчас
этот class или нет, чтобы потом включить
или выключить, соответственно. 

Поэтому для нас предусмотрена очень удобная штука, называется она toggle. Toggle делает следующую вещь. Он сам проверяет, есть ли
на нашем элементе этот class уже, если он есть, он его снимает, то бишь удаляет, если его нету, он наоборот его добавляет.
```js
p.classList.toggle('active');
```
Такой своеобразный переключатель: вкл./выкл.




