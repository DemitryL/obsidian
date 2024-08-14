# Project Витрина

## Обзор API что доступно как использовать.

API от сайта [fortniteapi.io](https://fortniteapi.io/)

Postman -> Headers -> Authorization - key 

## Подготовка проэкта шапка футер 

index.css
```css
body {
 margin: 0;
 font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', 'Oxygen', 'Ubuntu', 'Cantarell', 'Fira Sans', 'Droid Sans', 'Helvetica Neue', sans-serif;
 -webkit-font-smoothing: antialiased;
 -moz-osx-font-smoothing: grayscale;
}

nav {
 padding: 0 1rem;
}

.content {
 min-height: calc(100vh - 70px - 64px);
 padding: 1.5rem 0;
}

.goods {
 display: grid;
 grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
 gap: 1rem;
}
```

public -> index.html
```html
<meta
 name="description"
 content="React Shop"
/>

<title>React Shop</title>

 <!-- Compiled and minified CSS -->
 <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0/css/materialize.min.css">
    
 <!-- Icons materialize CSS -->
 <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
```

public -> manifest.json
```json
{
 "short_name": "React Shope",
 "name": "React Shope",
}
```

components

Header.jsx
```jsx
function Header() {
 return <nav className="green darken-1">
  <div className="nav-wrapper">
   <a href="#" className="brand-logo">React Shope</a>
   <ul id="nav-mobile" className="right hide-on-med-and-down">
    <li><a href="!#">Repo</a></li>
   </ul>
  </div>
 </nav>
}

export {Header}
```

Footer.jsx
```jsx
function Footer() {
 return <footer className="page-footer green lighten-4">
  <div className="footer-copyright">
   <div className="container">
    @ {new Date().getFullYear()} Copyright Text
    <a className="grey-text text-lighten-4 right" href="#!">Repo</a>
   </div>
  </div>
 </footer>
}

export {Footer}
```

Для работы с локальными переменными
.env.local
```
REACT_APP_API_KEY=b1034aaa-fe54e979-f85a8fe6-9d3c4535
```

src -> config.js
```js
const API_KEY = process.env.REACT_APP_API_KEY;

// Get daily shop
const API_URL = 'https://fortniteapi.io/v2/shop?lang=ru';

export {
 API_KEY,
 API_URL,
}
```

App.js
```js
import {Header} from './components/Header';
import {Shope} from './components/Shope';
import {Footer} from './components/Footer';

function App() {
 return (
  <>
   <Header />
   <Shope />
   <Footer />
  </>
 )
}

export default App;
```

Shope.jsx
```jsx
function Shope() {
 return <main className="container content">Shope main</main>
}

export {Shope}
```

## Вывод списка товаров

Shope.jsx
```jsx
import { useState, useEffect } from 'react';
import { API_KEY, API_URL } from '../config';

import {Preloader} from './Preloader';
import {GoodsList} from "./GoodsList";

function Shope() {
 const [goods, setGoods] = useState([]);
 const [loading, setLoading] = useState(true);
 const [order, setOrder] = useState([]);
 
 useEffect(function getGoods() {
  fetch(API_URL, {
   headers: {
    'Authorization': API_KEY,
   }
  }).then(response => response.json()).then(data => {
   data.featured && setGoods(data.featured);
   setLoading(false);
  })
 }, []);
 
 return <main className="container content">
  {
   loading ? <Preloader /> : <GoodsList goods={goods} />
  }
 </main>
}

export {Shope}
```

components -> Preloader.jsx
```jsx
function Preloader() {
 return <div className="progress">
  <div classNam="indeterminate"></div>
 </div>
}

export { Preloader }
```

Список товаров
GoodsList.jsx
```jsx
import {GoodsItem} from "./GoodsItem";

funtion GoodsList(props) {
 const {goods = []} = props;
 
 if (!goods.length) {
  return <h3>Nothing here</h3>
 }
 
 return <div className="goods">
  {goods.map(item => (
   <GoodsItem key={item.id} {...item} />
  )}
 </div>
}

export { GoodsList }
```

Разметка одна карточка товара
GoodsItem.jsx
```jsx
function GoodsItem(props) {
 const {
  id,
  name,
  description,
  price,
  full_background,
 } = props;
 
 return <div className="card" id={id}>
  <div className="card-image">
   <img src={full_background} alt={name} />
  </div>
  <div className="card-content">
   <span className="card-title">{name}</span>
   <p> {description} </p>
  </div>
  <div className="card-action">
   <button className="btn">This is a link</button>
   <span className="right" style={{fontSize: '1.8rem'}}>{price}</span>
  </div>
 </div>
}

export { GoodsItem }
```

index.css
```css
.card {
 display: flex;
 flex-direction: column;
}

.card-content {
 flex-grow: 1;
}
```

## Состояние заказа, иконка корзины

Cart.jsx
```jsx
function Cart(props) {
 const {quantity = 0} = props;
 
 return <div className="cart blue darken-4 white-text">
  <i className="material-icons">shopping_cart</i>
  {quantity ? <span className="cart-quantity">{quantity}</span> : null}
 </div>
}

export {Cart};
```

Add in Shop

Shop.jsx
```jsx
import {Cart} from "./Cart";

return <main className="container content">
 <Cart quantity={order.length} />

  {
   loading ? <Preloader /> : <GoodsList goods={goods} />
  }
 </main>
```

index.css
```css
.cart {
  position: fixed;
  bottom: 2rem;
  right: 2rem;
  cursor: pointer;
  z-index: 5;
  padding: 1rem;
}

@media (min-width: 767px) {
 .cart {
  top: 5rem;
  bottom: unset;
 }
}
```

## Функция добовления товара в корзину


