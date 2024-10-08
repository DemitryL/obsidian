Выбирать все элементы страницы для работы бывает иногда избыточно. Порой, имея ссылку на какой-то один элемент, мы можем дальше
использовать навигацию относительно этого элемента.

Мы можем получить его родителя, можем получить дочерние элементы, можем получить соседние элементы. 
```html
<header>
 <a><span></span></a>
 <button></button>
 <div></div>
</header>
```
Вот, в частности у меня есть какая-то ссылка, рядом с этой ссылкой ее соседний элемент, у меня является button-ссылка. У кнопки и у ссылки есть общий родитель, у ссылки есть еще и дочерний элемент, это некий span-элемент.

Давайте попробуем поработать, я возьму эту ссылку, положу ее в переменную.
```js
const anchor = document.querySelector('a');
anchor.parentElement
```
Обращаясь к anchor, я могу получить его родителя. Обратиться по методу, соответственно, `parentElement`. 

И он мне говорит, что родителем является вот эта штука, причем не просто является это тоже объект. Мы можем в этом убедиться, распечатав его в console, через `console.dir`.
```js
console.log(anchor.parentElement);
```
Мы можем всю эту историю распечатать и убедиться, что это действительно объект, к которому мы можем обратиться как к объекту и получать доступ к его атрибутам, и прочим историям, с которыми нам еще предстоит познакомиться.

Раз есть родитель, есть и дети. Соответственно, мы должны общаться к... Либо мы можем посчитать
количество элементов. `ChildElementCount` считает
количество элементов, либо через `children` мы можем получить коллекцию элементов.
```js
anchor.children
anchor.children[0]
```
Раз это коллекция, мы можем, обращаться по индексу вполне конкретному и сказать, допустим, по нулевому индексу я получу нулевой элемент.

Если у меня там много элементов к каждому могу обратиться по индексу. 

Либо я могу использовать другую штуку, я всегда могу обратиться к первому ребенку, `firstElementChild`. То же самое я могу сделать
с последним `lastElementChild`.
```js
anchor.firstElementChild
anchor.lastElementChild
```
В данной, конкретной ситуации они совпадают, это одни и те же объекты. Опять же важно везде здесь
писать именно элемент.

Но и мы можем хотеть получит не только детей и родителей, мы можем хотеть получить
соседний элемент.
```js
anchor.nextElementSibling
```
В данном случае это кнопка button. Если нам нужен следующий div, то мы можем делать:
```js
anchor.nextElementSibling.nextElementSibling
```
Либо мы могли бы положить сначала эту кнопку в отдельную переменную, потом еще для нее снова
получить следующий элемент.

У нас есть некая кнопка button, и чтобы получить предыдущего соседа, мы говорим: `previousElementSibling`.
```js
const btn = anchor.nextElementSibling;
btn.previousElementSibling
```
Мы снова получаем нашу ссылку, от которой мы до этого начинали наше движение по разным самым сторонам.