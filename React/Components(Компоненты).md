Для работы с реактом практически всегда нельзя использовать один файл, поэтому мы будем разбивать на компоненты.

 Компонент `Book.jsx`
```jsx
import React from "react";

const Book = (props) => {
 return (
  <div className={props.name}>
   <h2>Hello, {props.name}</h2>
   <p>{props.year}</p>
   <p>{props.price}</p>
   <p>{props.children}</p>
  </div>
 )
}
export { Book }
```

Импортируем в файл `index.js`:
```js
import React from "react";
import ReactDOM from "react-dom";

import App from "./App";

const rootElement = document.getElementById("root");
ReactDOM.render(
 <React.StrictMode>
  <App />
 </React.StrictMode>
)
```

Компонент `App.jsx`
```jsx
import React from "react";
import { Book } from './Book';

const App = () => {
 return (
  <div>
   <Book name="JS for beginner" year="2018" price="1000">
    Text here
   </Book>
   <Book name="React" year="2020" price="1200"/>
  </div>
 )
}

export default App;
```

#### Условная отрисовка
```jsx
<h2>Hello, {props.name ? <span>{props.name}</span> : 'default name'}</h2>
```

Также можем использовать условия до return:
```jsx
const Book = (props) => {
 if(!props.name) {
  return null;
 }

 return (
  <div>
   <h2>{props.name}</h2>
   <p>{props.year}</p>
   <p>{props.price}</p>
  </div>
 )
}
```
Условие if если имя отсутствует то не отрисовывается ничего. Возвращается null

OR

```jsx
const Book = (props) => {
 return props.name ? (
  <div>
   <h2>{props.name}</h2>
   <p>{props.year}</p>
   <p>{props.price}</p>
  </div>
 ) : null;
}
```

#### Пример с прелоадером

Компонент `Preloader.jsx`:
```jsx
import React from "react";

const Preloader = () => {
 return <h3>Loader...</h3>
}

export { Preloader };
```

`App.jsx`
```jsx
import React from "react"

import {Preloader} from "./Preloader"

const App = (props) => {
 return props.isLoading ? (
  <Preloader />
 ) : (
 <div>
  <Book name="JS" year="2011" price="1000" />
 </div>
 )
}
```

`index.js`
```jsx
const isLoading = true;
```