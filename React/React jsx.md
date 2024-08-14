Написание jsx без каких либо шаблонизаторов пример:
```html
<!DOCTYPE html>
<html lang="en">
<head>
 <meta charset="UTF-8">
 <meta name="viewport" content="width=device-width, initial-scale=1.0">
 <title>Pure React</title>
</head>
<body>
 <div id="root"></div>
 <!-- React CDN -->
 <script crossorigin src="https://unpkg.com/react@18/umd/react.development.js"></script>
 <script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
 <!-- React jsx -->
 <script>
  const Book = (props) => {
   return React.createElement('div', {}, [
    React.createElement('h2', {}, props.name),
    React.createElement('p', {}, props.year),
    React.createElement('p', {}, props.price),
   ])
  }
  const App = () => {
   return React.createElement('div', {}, [
    React.createElement("h1", {id: 'hello', className: 'class1'}, 'Hello from React'),
    React.createElement(Book, {name: 'JS for beginners', year: 2018, price: 1000}),
    React.createElement(Book, {name: 'React', year: 2020, price: 1200}),
    React.createElement(Book, {name: 'Vue JS', year: 2019, price: 1100}),
   ])
  }
  ReactDOM.render(React.createElement(App), document.getElementById('root'));
 </script>
 
</body>
</html>
```

`React.createElement()` - принимает три параметра, первое это имя элемента, вторым параметром идет объект в этом объекте идут различные атрибуты, третья вещь это дочерние элементы.

`ReactDOM.render()` - рендер принимает два параметра, первым параметром он спрашивает что мы хотим отрисовать, вторым параметром куда.

Для работы с jsx нужно некое окружение, javascript не знает что такое jsx и его нужно особым образом преобразовывать к понятному для браузера интерфейсу

Преобразование приложения в jsx :
```jsx
const Book = (props) => {
 return <div>
  <h2>{props.name}</h2>
  <p>{props.year}</p>
  <p>{props.price}</p>
 </div>
}

const App = () => {
 return <div>
  <Book name="JS for beginners" year="2018" price="1000" />
  <Book name="React" year="2020" price="1200" />
  <Book name="Vue JS" year="2019" price="1100" />
 </div>
}

const roootElement = document.getElementById("root")
ReactDOM.render(
 <React.StrictMode>
  <App />
 </React.StrictMode>,
 rootElement
)
```

```jsx
const Book = (props) => {
 return (
  <div className={props.name} data-text="">
   <h2>Hello, {props.name ? <span>{props.name}</span> : 'default name'}</h2>
   <p>{props.year}</p>
   <p>{props.price}</p>
   <br />
  </div>
 )
}
```

Инструкции такие как `if(){}, switch ().., for/ while`  мы не можем использовать в нутри конструкии jsx. Но мы можем использовать любой вызов функции, тернарный оператор в котором допускается любой уровень вложенности.

Касаемо того что может быть атрибутом: мы не можем использовать `class` мы должны использовать `className` , мы не можем использовать `for` должны использовать `htmlFor`. Мы должны их писать через камелКейс  исключением будут только data- атрибуты, реакт нормально их кушает.

Использование коментариев в jsx:
```jsx
{ // coments }
{ /* coments */ }
```

Все непарные теги обезательно должны быть закрытыми:
```jsx
<br />
<img />
<meta />
```

Передаем дочерний элемент компаненту:
`props.children`
```jsx
const Book = (props) => {
 return <div>
  <h2>{props.name}</h2>
  <p>{props.year}</p>
  <p>{props.price}</p>
  <p>{props.children}</p>
 </div>
}

const App = () => {
 return <div>
  <Book name="JS for beginners" year="2018" price="1000" />
    Lorem ipsom
  </Book>
 </div>
}
```

