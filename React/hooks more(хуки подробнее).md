# Хуки более подробнее

## useState

App.js
```js
import {State} from './hooks/State'

function App() {
 return (
  <div className="App">
   <State />
  </div>
 )
}

export default App;
```

State.jsx
```jsx
import React, { useState } from 'react';

export const State = () => {
 const [value, setValue] = useState(initialValue);
 
 return <div>{}</div>;
}
```
Есть особенность что вместо initialValue мы можем передать функцию.

useState(() => {}) позволяет на передать функцую и он ее выполнит внутри себя.

```
setValue((prevValue) => {
 return prevValue + 1;
})
```

prevValue - получение предыдущего значения.

## useEffect

Effect.jsx
```jsx
import React, { useEffect } from 'react';

export const Effect = () => {

 // what effect does
 useEffect(() => {
  const handler = () => {}
  document.addEventListener('click', handler)
  
  return () => {document.removeEventListener('click', handler)
 }, [])
 
 useEffect(function initPlugin() {
  somePlugin.init();
  
  return () => {somePlugin.destroy()}
 }, [])

 return <div></div>;
}
```

## useContext

Один из самых возможно трудно понимаемых хуков. Но в то же время один из самых мощных.

В реакте нам постоянно нужно пробрасывать пропсы. Для того что бы облегчить этот процес и был придуман `useContext` .

Context.jsx
```jsx
import React, { createContext, useState } from 'react';

export const CustomContext = createContext();

// Компонент
export const Context = (props) => {
  const [books, setBooks] = useState([
  // Колекция книг
   {id: 1, title: 'JS'},
   {id: 2, title: 'React'},
   {id: 3, title: 'NodeJS'},
  ]);
  
  /* Метод добавить книгу, он будет принемать объект книги, и он будет говорить создай новый массив положи новую книгу первой и добавь туда все текущие книги */
  const addBook = (book) => {
   setBooks([book, ...books])
  }
  
  /* И тоже самое на удаление. Для удаления нам достаточно id. Сделаем фильтрацию и будем проверять каждую книгу точнее ее индификатор не равен индификатору который мы получили. */
  const removeBook = (id) => {
   setBooks(books.filter(book => book.id !== id))
  }
  
  /* Как любому компоненту дать доступ к этому компоненту вне зависимости от уровня вложености и здесь как раз нам напомощь приходит тот компоненты который мы создали.
  
  Этот компонент будет возвращать Контекст с провайдором и оборачивать им мы будем все то что придет нам через `props.children`. И все его дочерние компоненты будут иметь доступ к тому что мы положем в поле value. Мы можем в поле велью напрямую набрасать какой-то объект, но обычно этот объект можно создать снаруже или внутри.
   */
   const value = {
    // передаем все книги, метод добавления и удаления книг
    books,
    addBook,
    removeBook,
   }
   
   return <CustomContext.Provider value={value}>
    {props.children}
   </CustomContext.Provider>
}
```
На уровне нашего приложения мы импортируем наш Context.

App.js
```js
import {Context} from './hooks/Context'

function App() {
 return <Context>
  
 </Context>;
}

export default App;
```
Оформить можно вообще по разному, в официальной документации немного по другому. Но и этот вариант достаточно популярный.

/* Например импортируем из папки компонентов компонент Книги */

App.js
```js
import {Context} from './hooks/Context'
import {Books} from './components/Books'

function App() {
 return <Context>
  <Books />
 </Context>;
}

export default App;
```

Books.jsx
```jsx
import React, {useContext} from 'react'
// Импортируем сам контекст
import {CustomContext} from '../hooks/Context'

import {Book} from './Book'

export function Books() {
 /* Используем юсКонтекст мы можем сделать диструкторизацию он принемает то контекст который мы изночально создавали и здесь теперь мы можем вытащить любую сущьность которую мы передавали в провайдер. Вытащим книги и по умолчанию сделаем их массивом. */
 const { books = [] } = useContext(CustomContext);
 
 return <div className='books'>
  {
   books.map(book => {
   // Ну и мы передаем все что в этой книге есть это айди и тайтл
    return <Book key={book.id} {...book} />
   })
  }
 </div>
}
```

Book.jsx
```jsx
import React, { useContext } from 'react';
import { CustomContext } from '../hooks/Context';

// Простейший компонент книги он принемает пропсы и пропс тайтл пытается рапечатать.
export function Book(props) {
 // Вытаскиваем кастом контекст
 const { removeBook } = useContext(CustomContext);
 
 return <h2 onClick={() => removeBook(props.id)}>{props.title}</h2>;
}
```

## useLayoutEffect

useLayoutEffect - выполняется синхронно и он может немного затормозить все то что выводится у нас на странице.

В докумендации советуют лучше использовать useEffect нежеле useLayoutEffect, так как useEffect выполняется асинхронно.

По факту useLayoutEffect нужно использовать когда нам нужно принудительно лесть в дом чтото менять. Но как правило 99% случаев нужно использовать useEffect.


## useCallback, useMemo

useCallback - выглядит он следующим образом, мы в этот хук передаем некую функцию и некий набор зависимостей

```jsx
function useCallback (callback, deps) {}
```

Какие выводы из этого мы можем сделать?

Функция useCallback как и любая другая функция вызывается на каждый рендер и в качестве параметра callback каждый рендер приходит новая функция и новый массив зависимостей. Которые мы либо выбрасываем, если зависимости до и после совпадают, либо сохраняем в хранилище, для будущего использования.


useMemo - это хук, который сохраняет результат вызова функции (первый аргумент) и пересчитывает его только при изменении зависимостей (второй аргумент). useMemo возвращает результат вызова первого аргумента.

Выглядит использование так:
```
// Типизация
function useMemo<T>(factory: () => T, deps: any[] | undefined): T;

// 1
const memoResult = useMemo(() => funcResult, []);

// 2
let testString = 'test';
const { data } = useMemo<{ data: string }>(() => ({ data: testString }), [testString]);
```


## useImperativeHandle

Это один из наиболее редко используемых хуков.
Здесь история о том чтобы попробывать изменить направления движения пропросов. 

В рамках нашего приложения мы данные передаем снизу вверх.

```jsx
import React, {useState,useRef, useImperativeHandle} from 'react';

const TextInput = React.forwardRef((props, ref) => {
 const {hasError, placeholder, value, update} = props;
 console.log(update);
 const inputRef = useRef();

 useImperativeHandle(ref, () => {
  return {
   focus() {
    inputRef.current.focus();
   }
  }
 })

 return (
  <input
   ref={inputRef}
   value={value}
   onChange={(e) => update(e.target.value)}
   placeholder={placeholder}
   style={{borderColor: hasError ? "red" : "black"}}
  />
 )
})
```

```jsx
const Form = () => {
 const [card, setCard] = useState("");
 const [phone, setPhone] = useState("");
 const [error, setError] = useState("");

 const cardEl = useRef();
 const phoneEl = useRef();

 const validate = () => {
  if(card.length < 16) {
   setError("card");
   cardEl.current.focus();
   return;
  }

  if (phone.length < 11) {
   setError("phone");
   phoneEl.current.focus();
   return;
  }
  setError("");
 }

 return (
  <div>
   <h2>useImperativeHandle hook</h2>
   <TextInput
    hasError={error === "card"}
    placeholder={"Card"}
    value={card}
    update={setCard}
    ref={cardEl}
   />
   <TextInput
    hasError={error === "phone"}
    placeholder={"Phone"}
    value={phone}
    update={setPhone}
    ref={phoneEl}
   />
   <button onClick={validate}>Validate</button>
  </div>
 )
}
```

Это очень редко приходится использовать, чаще всего она используется под капотом библиотек по работе с формами.

## useReducer

Очень важный хук который может значительно облегчить некоторые вещи.

```jsx
import React, { useReducer } from "react";
import "./style.css";

const limitRGB = (num) => (num < 0 ? 0 : num > 255 ? 255 : num);
const step = 50;

const reducer = (state, action) => {
 switch (action.type) {
  case "INCTEMENT_R":
   return {
    ...state,
    r: limitRGB(state.r + step)
   };
  case "DECREMENT_R":
   return {
    ...state,
    r: limitRGB(state.r - step)
   };
  case "INCTEMENT_G":
   return {
    ...state,
    g: limitRGB(state.g + step)
   };
  case "DECREMENT_G":
   return {
    ...state,
    g: limitRGB(state.g - step)
   };
  case "INCTEMENT_B":
   return {
    ...state,
    b: limitRGB(state.b + step)
   };
  case "DECREMENT_B":
   return {
    ...state,
    b: limitRGB(state.b - step)
   };
  default:
   return state;
 }
};

export default function App() {
 // useReducer возвращает два состояния. Первое это некий стейт значение по умолчанию, чаще всего это некий обьект. Вторая вещь это некая функция обновления. Она как правило называется dispatch - это общее распространенное название.
 const [{r, g, b}, dispatch] = useReducer(reducer, {r: 0, g: 150, b: 200})

 return (
  <div className="App">
   <h1
    style={{
     color: `rgb(${r}, ${g}, ${b})`
    }}
   >
    Hello CodeSandbox
   </h1>
   <div>
    <span>r </span>
    <button onClick={() => dispatch({type: "INCREMENT_R"})}>+</button>
    <button onClick={() => dispatch({type: "DECREMENT_R"})}>-</button>
   </div>
   <div>
    <span>g </span>
    <button onClick={() => dispatch({type: "INCREMENT_G"})}>+</button>
    <button onClick={() => dispatch({type: "DECREMENT_G"})}>-</button>
   </div>
   <div>
    <span>b </span>
    <button onClick={() => dispatch({type: "INCREMENT_B"})}>+</button>
    <button onClick={() => dispatch({type: "DECREMENT_B"})}>-</button>
   </div>
  </div>
 )
}
```

Reducer - это просто обычная javascript функция которая принемает две вещи, она принемает текущее состояние нашего приложения, она принемает некое действие в зависимости от которого предпологается что фугкция вернет нам новое состояние приложения.

Эту штуку часто используют когда много у нас сущьностей.

## Пользовательские хуки

Кастомные хуки

App.js
```jsx
import React, { useState } from "react";
import { usePrevious } from "./hooks/usePrevious";

export default function App() {
 const [count, setCount] = useState(0);

 const prevCount = usePrevious(count);

 return (
  <div className="App">
   <button onClick={() => setCount(count + 1)}></button>
   <h2>Current: {count}</h2>
   <h2>Previous: {prevCount}</h2>
  </div>
 )
}
```

usePrevious.js - используй предыдущее значение.
```jsx
import React, { useRef, useEffect } from "react";

function usePrevious(value) {
 const ref = useRef(); // {current: null}
 
 useEffect(() => {
  ref.current = value;
 })
 
 return ref.current;
}

export { usePrevious };
```

Может использоватся в самых различных случаях, с анимацией чтобы запомник в каком состоянии она была в прошлый раз.

Второй хук это имитация работы с локал сторедж
useLocalStorage

useLocalStorage.js
```jsx
import { useEffect, useState } from "react";

function useLocalStorage(initialState, key) { 
 const get = () => {
  const storage = localStorage.getItem(key);

  return storage ? +storage : initialState;
 }

 const [value, setValue] = useState(get);

 useEffect(() => {
  localStorage.setItem(key, value);
 }, [value])

 return [value, setValue];
}

export { useLovalStorage };
```

App.js
```jsx
import React, { useState } from "react";
import { usePrevious, useLocalStorage } from "./hooks";

export default function App() {
 const [count, setCount] = useLocalStorage(0, 'count');

 const prevCount = usePrevious(count);

 return (
  <div className="App">
   <button onClick={() => setCount(count + 1)}></button>
   <h2>Current: {count}</h2>
   <h2>Previous: {prevCount}</h2>
  </div>
 )
}
```


## Правила использования хуков

Хуки - обычные JavaScript-функции.

1. Используйте хуки только на верхнем уровне.
 - Не используйте хуки внутри циклов, условных операторов или вложенных функций.
 
2. Вызывайте хуки только из React-функций 
 - Не вызывайте хуки из обычных функций JavaScript.
 - Вызывайте хуки из функционального компонента React
 - Вызывайте хуки из пользовательского хука.

