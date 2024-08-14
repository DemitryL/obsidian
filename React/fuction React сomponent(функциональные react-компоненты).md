## Работа с состоянием в функциональном компоненте

Если мы хотим добавить в функциональный компонент все те возможности что и в классовам компоненте то мы будем использовать такую сущьность как хуки. 

Хуки это некая функциональность, у нас эта возможность сразу есть из коробки в REACT.

App.js
```js
function App() {
 return (
  <div className="App"></div>
 );
}

export default App;
```

Мы можем писать их через ключевое слово `function`, можем использовать стрелочные функции, здесь уже все зависит от предпочтения или договоренность с командой.

Для работы с состояниями нам обязательно нужно сделать импорт
```
import React, {useState} from 'react'
```

useState - используй состояние, работает он достаточно хитро мы должны создать новую переменную.

App.js
```js
function App() {
 const [] = useState();

 return (
  <div className="App"></div>
 );
}

export default App;
```

useState() - некая функция которая всегда возвращает нам некий массив и этот массив как правило мы должны через диструктурезацию   разобрать чтоб у нас были две разные сущности.

`
const [value, setValue] = useState();
`
Первым элементом массива нам придет некое значение, мы можем назвать его обсолютно как угодно. И второй сущностью нам приходит из хука Функция которая позволяет нам эту переменную все время обновлять.

`
const [value2, setValue2] = useState();
`
Каждый раз когда нам нужна новая переменная мы каждый раз создаем данную конструкцию. Отдельно приходит сама переменная в которую мы чтото положем, это может быть обьект массив и т.д. И вторым  параметром функция обновления которую мы тоже называем как угодно.

Ну и второй ньюанс мы передаем некое значение по умолчанию в качестве аргумента при работе с хуком. 

Допустим если мы работаем с числом, например передадим 0, изначально value будет равен нулю.
`
const [value, setValue] = useState(0);
`

#### Создание кликер через хуки

App.js
```jsx
function App() {
 const [count, setCount] = useState(0);
 
 const increment = () => {
  setCount(count + 1)
 }
 
 const decrement = () => {
  setCount(count - 1)
 }

 return (
  <div className="App">
   <button onClick={decrement}>-</button>
   <span style={{display: 'inline-block', margin: '0 0.5rem'}}>{count}</span>
   <button onClick={increment}>+</button>
  </div>
 );
}

export default App;
```

## Управление жизненым циклом через функциональный компоненет

Мы должы понять как работать с жизненым циклом используя функциональный компонент и хуки. Не все этапы жизненого цикла мы можем реализовать в функциональном компоненте. Но при этом мы можем использовать основные три, как раз те что мы использовали при классовом компоненте.


Выносим кликер в отдельный компонент

Clicker.jsx
```jsx
function Clicker() {
 const [count, setCount] = useState(0);
 
 const increment = () => {
  setCount(count + 1)
 }
 
 const decrement = () => {
  setCount(count - 1)
 }

 return (
  <div className="App">
   <button onClick={decrement}>-</button>
   <span style={{display: 'inline-block', margin: '0 0.5rem'}}>{count}</span>
   <button onClick={increment}>+</button>
  </div>
 );
}

export default Clicker;
```

App.js
```js
import React, {useState} from 'react';
import Clicker from './Clicker';

function App() {
 const [isClicker, setClicker] = useState(false);
 
 return (
  <div className="App">
   <h2>React App</h2>
   <button onClick={() => setClicker(!isClicker)}>Toggle clicker</button>
   {isClicker && <Clicker />}
  </div>
 )
}

export default App;
```

За работу с жизненым циклом отвечает один `useEffect`, он один содержит в себе функциональность всех трех этопов циклов.

Clicker.jsx
```jsx
import React, { useState, useEffect } from 'react';

function Clicker() {
 const [count, setCount] = useState(0);
 
 const increment = () => {
  setCount(count + 1)
 }
 
 const decrement = () => {
  setCount(count - 1)
 }

 return (
  <div className="App">
   <button onClick={decrement}>-</button>
   <span style={{display: 'inline-block', margin: '0 0.5rem'}}>{count}</span>
   <button onClick={increment}>+</button>
  </div>
 );
}

export default Clicker;
```

Так же как `useState` `useEffect` мы можем использовать любое количество раз.

`useEffect` - обычно пишут перед ретерном и он не к чему не присваевается, он существует сам по себе. ОН принемает две сущьности, первая это некая функция - как раз некие действия которые мы хотим сделать. Вторая это некий набор зависимостей, по хорошему эта штука должна быть всегда.

`useEffect(() => {}, [])`

Если мы хотим чтоб обновлялся то мы можем конкрето указывать 

```jsx
useEffect(() => {
 console.log('hello from clicker', count);
}, [count])
```

Возможность чтото размонтировать используется специальный ретерн в конце строки.

```jsx
useEffect(() => {
 console.log('hello from clicker', count);
 
 return () => console.log('goodbye clicker');
}, [count])
```

По факту функция-очистки срабатывает каждый раз при обновлении зависимости плюс при размонтировании.


## Использование рефов в функциональном компоненте

Ref.jsx
```jsx
import React, { useRef } from 'react';

const WithRef = () => {
 return (
  <div>
   <input placeholder="name" />
  </div>
 )
}

export default WithRef;
```

`useRef` это аналог `createRef` который мы используем в классовом компоненте.

Ref.jsx
```jsx
import React, { useRef } from 'react';

const WithRef = () => {
 const inputEl = useRef(null);
 console.log(inputEl);

 return (
  <div>
   <input placeholder="name" ref={inputEl} />
  </div>
 )
}

export default WithRef;
```

useRef возвращает изменяемый ref-объект, свойство .current которого инициализируется переданным аргументом (initialValue). Возвращённый объект будет сохраняться в течение всего времени жизни компонента.

По сути, useRef похож на «коробку», которая может содержать изменяемое значение в своём свойстве .current.

## Рефакторинг таймера в функциональном компоненте

Timer.jsx
```jsx
import React, {useState, useEffect, useRef} from 'react';

function setDefaultValue() {
 const userCount = localStorage.getItem('count');
 return userCount ? +userCount : 0;
}

export default function Timer() {
 const [count, setCount] = useState(setDefaultValue());
 const [isCounting, setIsCount] = useState(false);
 const timerIdRef = useRef(null);
 
 const handleReset = () => {
  setCount(0);
  setIsCount(false);
 }
 
 const handleStart = () => {
  setIsCount(true);
 }
 
 const handleStop = () => {
  setIsCount(false);
 }
 
 useEffect(() => {
  localStorage.setItem('count', count);
  
 }, [count])
 
 useEffect(() => {
  if(isCounting) {
   timerIdRef.current = setInterval(() => {
    setCount((prevCount) => prevCount + 1);
   }, 1000);
  }
  
  return () => {
   timerIdRef.current && clearInterval(timerIdRef.current)
   timerIdRef.current = null;
  }
 }, [isCounting])
 
 return (
  <div className='timer'>
   <h1>React Timer</h1>
   <h3>{count}</h3>
   {!isCounting ? (
    <button onClick={handleStart}>Start</button>
   ) : (
    <button onClick={handleStop}>Stop</button>
   )}
   <button onClick={handleReset}>Reset</button>
  </div>
 )
 
}
```

## Рефакторинг проекта с фильмами в функциональном компоненте





