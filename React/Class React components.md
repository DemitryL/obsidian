### Разбор составляющих базового React-шаблона
```
> node_modules
> public
> src
.gitignore
package.json
README.md
yarn.lock
```

В папке public находятся файлы:
```
favicon.ico
index.html
logo.png
manifest.json
robots.txt
```

Файл `robots.txt` для `SEO`, файл `manifest.json` нужен для каких то методанных в первую очередь мобильные приложекия этим файлом пользуются.

В папке `src` находятся файлы:
```
App.css
App.js
App.test.js
index.css
index.js
logo.svg
reportWebVitals.js
setupTests.js
```

Файл `reportWebVitals.js` - это дополнительный некий сервис от гугла 

Файл `setupTests.js` для тестов кода

### Понятие React-компонента
На официальном сайте в разделе `Документация` есть раздел `Философия React` 

Посмотрим пример в классовом стиле, реакт развивался достаточно много лет изночально классовые компоненты были основным подходом, сейчас все чаще используют функции потомучто у них теперь есть ьак называемые хуки.

Но так или иначе мы будет встречать классовые компоненеты поэтому нужно их знать.

`App.js`
```jsx
import React from "react";

class App extends React.Component {
 constructor(props) {
  super(props);
 }
 
 render() {
  return (
   <div className="App">
    Hello form React
   </div>
  )
 }
}

export default App;
```

У класса на верхнем уровне должны быть различные методы и в частности метод который отправляет на отрисовку называется `render()` в нутри этого метода и должна происходить вся эта маги с `jsx`.

Метод `constructor()` принемает какието пропсы и с помощью метода `super()` передает их в родительский класс.

```jsx
import React, {Component} from "react";

class App extends Component {
 constructor(props) {
  super(props)
 }

 render() {
  return (
   <div>
   </div>
  )
 }
}

export default App;
```
Обычно классовый компонент выглядит так, это минимально.

### Состояние компонента и управление им

У любого приложения как правиоа есть различные состояния, как правила что то в нем меняется, пользователь делает какие то определенные действия и все что меняется мы как правило должны сохранять и вот в реакте есть такое понятие как стейт и если мы работаем с классовым компонентом то он хранится в такой переменной как `this.state = {}` как правило это обьект.

Напишем простой кликер:
```jsx
import React, {Component} from "react";

class App extends Component {
  state = {
   count: 0
 }

 handleClick = () => {
  this.setState({count: this.state.count + 1})
 }

 render() {
  return (
   <div>
    <button onClick={this.hendleClick}>{this.state.count}</button>
   </div>
  )
 }
}

export default App;
```

Запускаем проект и кликая на кнопку меняется состояние в консоле появились две дополнительные вкладки `Components and Profiler` мы работаем с вкладкой `Components` можем видеть какие пропсы были переданы и какой сейчас стейт.

Есть и другой вариант записи `state`:
```jsx
state = {
 count: 0
};
```

Как работает `setState()` 
```jsx
handleClick = () => {
 this.setState((prevState) => ({count: prevState.count + 1}))
 this.setState((prevState) => ({count: prevState.count + 1}))
 this.setState((prevState) => ({count: prevState.count + 1}))
}
```
В таком случае при нажатии `count` будет увеличиватся на 3.

Также `setState()` вторым параметром принемет колбек функцию:
```jsx
handleClick = () => {
 this.setState((prevState) => ({count: prevState.count + 1}), () => {
  console.log('setState complete')
 })
}
```

`setState()` - работает асинхронно , он выполняет все операции, после каких то синхронных операций.

Но все же наиболее распрастраненный сценарий работы:
```jsx
handleClick = () => {
 this.setState({count: this.state.count + 1})
}
```

### Нюансы создания методов в классовых компонентах

Как мы работаем с функциями, мы можем передовать работая с классовыми компонентами тремя разными способами:

Первый способ метод создания используя стрелочную функцию, но в документации реакта написано что они не рекомендуют так делать, хотя их же сборка поддерживает этот подход и он на самом деле самый локаничный.

Второй способ, обычный метод не используя стрелочную функцию. Он не очень популярен и его не очень любят потому что он занимает много места, но он вполне актуален

```jsx
import React, {Component} from "react";

class App extends Component {
 constructor(props) {
  super(props);
  this.state = {
   count: 0
  }
  this.handleClick = this.handleClick.bind(this);
 }

 handleClick() {
  this.setState({count: this.state.count + 1})
 }

 render() {
  return (
   <div>
    <button onClick={this.hendleClick}>{this.state.count}</button>
   </div>
  )
 }
}

export default App;
```

Ну и третий вариант это когда у нас есть что-то уникальное что-то небольшое, не обезательно создавать отдельный метод, мы можем напрямую написать стрелочную функцию.
```jsx
render() {
  return (
   <div>
    <button onClick={() => this.setState({count: this.state.count + 1})}>{this.state.count}</button>
   </div>
  )
 }
```

### Разбор практики с кликером
```jsx
import React, {Component} from "react";

class App extends Component {
  state = {
   count: 0
 }

 increment = () => {
  this.setState({count: this.state.count + 1})
 }

 decrement = () => {
  this.setState({count: this.state.count - 1})
 }

 render() {
  return (
   <div style={{margin: 'auto', width: '300px'}}>
    <button onClick={this.decrement}>-</button>
    <span style={countStyle}>{this.state.count}</span>
    <button onClick={this.increment}>+</button>
   </div>
  )
 }
}

export default App;

const countStyle = {
 margin: '0 0.75rem',
 display: 'inline-block'
}
```


### Понятие жизненного цикла React-компонента

Методы жизненного цикла:
```
# Монтирование
constructor
render
React обновляет DOM и рефы
componentDidMount

# Обновление
New props setState() forceUpdate()
render
React обновляет DOM и рефы
componentDidUpdate

# Размонтирование
componentWillUnmount
```

У нас есть наследуемый компонент из реакта:
```jsx
componentDidMount() {
 console.log('componentDidMount');
 fetch()
}
```

`componentDidMount()` - отрабатывает только один раз, можем использовать метод `fetch()` чаще всего так  и используется, подключать какиенибудь плагины для самых разных целей.

```jsx
componentDidUpdate() {
 console.log('componentDidUpdate');
}
```

`componentDidUpdate()` - отрабатывает при каждом изменении компонента.

```jsx
componentWillUnmount() {
 clearInterval(this.timerId);
}
```

### Cоздание таймерa

```jsx
import "./App.css";
import React, { Component } from "react";

class App extends Component {
  state = {
    count: 0,
    isCounting: false,
  };

  componentDidMount() {
    const userCount = localStorage.getItem("timer");
    if (userCount) {
      this.setState({ count: +userCount });
    }
  }

  componentDidUpdate() {
    localStorage.setItem("timer", this.state.count);
  }

  componentWillUnmount() {
    clearInterval(this.couterId);
  }

  handleStart = () => {
    this.setState({ isCounting: true });

    this.couterId = setInterval(() => {
      this.setState({ count: this.state.count + 1 });
    }, 1000);
  };

  handleStop = () => {
    this.setState({ isCounting: false });
    clearInterval(this.couterId);
  };

  handleReset = () => {
    this.setState({ isCounting: false, count: 0 });
    clearInterval(this.couterId);
  };

  render() {
    return (
      <div>
        <header className="App">
          <h1>React Timer</h1>
          <p>{this.state.count}</p>
          {/* Две кнопки сменяются в зависимости идет подсчет или нет */}
          {!this.state.isCounting ? (
            <button onClick={this.handleStart}>Start</button>
          ) : (
            <button onClick={this.handleStop}>Stop</button>
          )}
          <button onClick={this.handleReset}>Reset</button>
        </header>
      </div>
    );
  }
}

export default App;
```

### Работа с коллекциями и атрибутом key

```jsx
import React, {Component} from 'react'

class App extends Component {
 state = {
  posts: [
   {id: 'abc1', name: 'JS Basics'},
   {id: 'abc2', name: 'JS Advanced'},
   {id: 'abc3', name: 'React JS'},
  ],
 };
 
 render() {
  return (
   <div>
    {this.state.posts.map(post => (
     <h2 key={post.id}>{post.name}</h2>
    ))}
   </div>
  );
 }
```

Метод массива `map()` позволяет на пройтись по массиву и динамически выводить объекты на страницу.

Каждой статье нужен уникальный ключ `key={}`. Когда мы работаем  со списками и выводим типовой набор, реакту важно получить тот самый типовой набор, в каждом значении кей будет какаято уникальная стока, такой строкой чаще всего бывает айдишник.

### Однонаправленный поток данных и состояние

Наши компоненты могут вкладыватся в другие компоненты подобно тому как html теги могут вкладыватся в другие теги. И при этом мы можем в компоненты передовать какието пропсы.

Структура, некий список карточек
```
App.js

// Posts - отыечает за вывод списка
Posts.js

// Post - уникальный один пост как он должен выглядеть
Post.js
```

История заключается в том что мы не можем передавать попсы в обратном направлении

`
src -> components -> Posts.jsx -> Post.jsx 
`

App.js
```jsx
import {Posts} from './components/Posts'

class App extends Component {
 state = {
  posts: [
   {id: 'abc1', name: 'JS Basics'},
   {id: 'abc2', name: 'JS Advanced'},
   {id: 'abc3', name: 'React JS'},
  ]
 }
 
 {/* Чтобы вызвать это this.setState() на уровне поста или ниже мы должны пробросить ее вниз */}
 handleSomething = () => {
  {//this.setState({})}
  console.log('App.jsx setState update');
 }

render() {
 {/*Деструктуризация*/}
 const {posts} = this.state;
 return (
  <div className="App">
   <Posts posts={posts} cb={this.handleSomething}/>
  </div>
 )
}

}
```

Posts.js
```jsx
import {Post} from './Post';

export function Posts (props) {
 return <div>
  {
   props.posts.map(post => (
    <Post key={post.id} name={post.name} cb={props.cb}/>
   ))
  }
 </div>
}
```

Post.js
```jsx
{/*Деструктуризация*/}
const {name, cb} = props

export function Post (props) {
 return <h2 onClick={cb}>{name}</h2>
}
```

### Обновление состояния через дочернии елементы

App.js
```jsx
import {Posts} from './components/Posts'

class App extends Component {
 state = {
  posts: [
   {id: 'abc1', name: 'JS Basics'},
   {id: 'abc2', name: 'JS Advanced'},
   {id: 'abc3', name: 'React JS'},
  ]
 }

 removePost = (id) => {
  {/* Для обновления состояния мы всегда используем setState()*/}
  this.setState({posts: this.state.posts.filter(post => post.id !== id)})
 }

render() {
 {/*Деструктуризация*/}
 const {posts} = this.state;
 return (
  <div className="App">
   <Posts posts={posts} cb={this.handleSomething} removePost={this.removePost}/>
  </div>
 )
}

}
```

Posts.js
```jsx
import {Post} from './Post';

export function Posts (props) {
 return <div>
  {
   props.posts.map(post => (
    <Post key={post.id} id={post.id} name={post.name} cb={props.cb} removePost={props.removePost}/>
   ))
  }
 </div>
}
```

Post.js
```jsx
{/*Деструктуризация*/}
const {name, cb, removePost} = props

export function Post (props) {
 return <div> <h2 onClick={cb}>{name}</h2> <button onClick{() => removePost(id)}>Delete</button> </div>
}
```
