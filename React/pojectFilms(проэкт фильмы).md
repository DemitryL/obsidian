### Подготовка проэкта создание шапки и подвала

#### Библиотека [materializecss.com](https://materializecss.com/getting-started.html)

Мы будем работать со стилями и то не со всеми какието мы точечно будем дописывать самостоятельно

Настройка проэкта 
public -> index.html

```html
<meta 
 name=""
 content="React movies simple portfolio project"
/>

<title>React Movies</title>
<!-- Compiled and minified CSS -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0/css/materialize.min.css">
```

Так же правим файл manifest.json
public -> manifest.json

```json
{
 "short_name": "React Movies",
 "name": "React Movies App",
}
```

Структура создадим две папки components and layout
src -> components + layout

Далее 
layout -> Header.jsx
```jsx
function Header() {
 return <nav className="green darken-1">
    <div className="nav-wrapper">
      <a href="#" className="brand-logo">Logo</a>
      <ul id="nav-mobile" className="right hide-on-med-and-down">
        <li><a href="!#">Sass</a></li>
      </ul>
    </div>
  </nav>
}

export {Header}
```

Подключим к нашему приложению
App.js
```js
import React from 'react'
import {Header} from './layout/Header'
import {Footer} from './layout/Footer'
import {Main} from './layout/Main'

function App() {
 return (
  <>
   <Header />
   <Main />
   <Footer />
  </>
 )
}

export default App;
```
Добавляем свои стили в index.css
```css
nav {
 padding: 0 1rem;
}

.content {
 min-height: calc(100vh - 70px - 64px);
}
```

Add Footer.jsx
```jsx

function Footer() {
 return <footer className="page-footer">
          <div className="footer-copyright">
            <div className="container">
            © {new Date().getFullYear()} Copyright Text
            <a className="grey-text text-lighten-4 right" href="#!">More Links</a>
            </div>
          </div>
        </footer>
}

export {Footer}
```

Add Main.jsx
```jsx

function Main() {
 return <main className="content container">
        </main>
}

export {Main}
```

## Знакомства с API базой фильмов

Открытая база данных фильмов [omdbapi.com](https://omdbapi.com/)
Мы будем получать от туда постер название описания для фильмов

Для того чтоб это все посмотреть можно использовать приложение [postman](https://www.postman.com/downloads/) 


```
http://www.omdbapi.com/?apikey=[yourkey]&
```
После регистрации на omdbapi.com получаем свой apikey и ставим вместо [yourkey]


## Создание общего списка фильмов

components -> Movie.jsx + Movies.jsx
они оба будут получать пропсы и что то с ними делать

Movie.jsx
```jsx
funciton Movie (props) {
 const {
  Title: title,
  Year: year,
  imdbID: id,
  Type: type,
  Poster: poster,
 } = props;
 
 return <div id={id} className="card movie">
  <div className="card-image waves-effect waves-block waves-light">
   <img className="activator" src={} />
  </div>
  <div className="card-content">
   <span className="card-title activator grey-text text-darken-4">{title}</span>
   <p>{year} <span className="right">{type}</span></p>
  </div>
 </div>
}
export {Movie}
```

Movies.jsx
```jsx
import {Movie} from './Movie'

function Movies (props) {
 const {movies} = props;
 
 return <div className="movies">
  {movies.map(movie => (
   <Movie key={movie.imdbID} {...movie} />
  ))}
 </div>
}
export {Movies}
```

Main.jsx
```jsx
import React from 'react'
import {Movies} from '../components/Movies'
import {Search} from '../components/Search'
import {Preloader} from '../components/Preloader'

class Main extends React.Component {
 state = {
  movies: [],
 }
 
 componentDidMount() {
  fetch("url")
   .then(response => response.json())
   .then(data => this.setState({movies: data.Search}))
 }
 
 render() {
  const {movies} = this.state;
 
  return <main className="container content">
   <Search />
   {
    movies.lenght ? (<Movies movies={movies}/>) : <Preloader />
   }
  </main>
 }
}
```

Добавляем свои стили в index.css
```css
nav {
 padding: 0 1rem;
}

.content {
 min-height: calc(100vh - 70px - 64px);
}

.movies {
 display: grid;
 grid-template-colums: repeat(auto-fill, minmax(250px, 1fr));
 gep: 1rem;
}
```

## Добавление строки поиска

Создание прелоудера
components -> Preloader.jsx

Preloader.jsx
```jsx
function Preloader() {
 return <div className="progress">
  <div className="indeterminate"></div>
 </div>
}
export {Preloader}
```

Создаем компонент формы поиска
components -> Search.jsx

Search.jsx
```jsx
import React from 'react'

class Search extends React.Component {
 state = {
  search: '',
 }
 
 render() {
  return <div className="row">
    <div className="input-field inline">
     <input 
      placeholder="search" 
      type="search" 
      className="validate" 
      value={this.state.search}
      onChange={(e) => this.setState({search: e.target.value})}
     />
    </div>
  </div>
 }
}

export {Search}
```

## Практика по реализации поиска фильмов
Нужна фунция которая будет обновлять стайт и которую можно спустить в низ

Main.jsx
```jsx
import React from 'react'
import {Movies} from '../components/Movies'
import {Search} from '../components/Search'
import {Preloader} from '../components/Preloader'

class Main extends React.Component {
 state = {
  movies: [],
 }
 
 componentDidMount() {
  fetch("url")
   .then(response => response.json())
   .then(data => this.setState({movies: data.Search}))
 }
 
 searchMovies = (str) => {
  fetch(`url=${str}`)
   .then(response => response.json())
   .then(data => this.setState({movies: data.Search}))
 }
 
 render() {
  const {movies} = this.state;
 
  return <main className="container content">
   <Search searchMovies={this.searchMovies}/>
   {
    movies.lenght ? (<Movies movies={movies}/>) : <Preloader />
   }
  </main>
 }
}
```
Search.jsx
```jsx
import React from 'react'

class Search extends React.Component {
 state = {
  search: '',
 }
 
 handleKey = (event) => {
  if(event.key === 'Enter') {
   this.props.searchMovies(this.state.search);
  }
 }
 
 render() {
  return <div className="row">
    <div className="input-field inline">
     <input 
      placeholder="search" 
      type="search" 
      className="validate" 
      value={this.state.search}
      onChange={ (e) => this.setState({search: e.target.value}) }
      onKeyDown={this.handleKey}
     />
     <button className="btn search-btn" onClick={() => this.props.searchMovies(this.state.search) }>Search</button>
    </div>
  </div>
 }
}

export {Search}
```

Добавляем свои стили в index.css
```css
nav {
 padding: 0 1rem;
}

.content {
 min-height: calc(100vh - 70px - 64px);
}

.movies {
 display: grid;
 grid-template-colums: repeat(auto-fill, minmax(250px, 1fr));
 gep: 1rem;
}

.search-btn {
 position: absolute;
 top: 0;
 right: 1rem;
}
```

## Добавление фильтрации по категориям

Search.jsx
```jsx
import React from 'react'

class Search extends React.Component {
 state = {
  search: '',
  type: 'all',
 }
 
 handleKey = (event) => {
  if(event.key === 'Enter') {
   this.props.searchMovies(this.state.search, this.state.type);
  }
 }
 
 handleFilter = (event) => {
  this.setState(() => ({type: event.target.dataset.type}), () => {
   this.props.searchMovies(this.state.search, this.state.type)
  })
 } 
 
 render() {
  return <div className="row">
    <div className="input-field inline">
     <input 
      placeholder="search" 
      type="search" 
      className="validate" 
      value={this.state.search}
      onChange={ (e) => this.setState({search: e.target.value}) }
      onKeyDown={this.handleKey}
     />
     <button className="btn search-btn" onClick={() => this.props.searchMovies(this.state.search, this.state.type) }>Search</button>
    </div>
    
    <div>
     <label>
      <input 
       className="with-gap"
       name="type"
       type="radio"
       data-type="all"
       onChange={this.handleFilter}
       checked={this.state.type === 'all'}
      />
      <span>All</span>
     </label>
     <label>
      <input 
       className="with-gap"
       name="type"
       type="radio"
       data-type="movie"
       onChange={this.handleFilter}
       checked={this.state.type === 'movie'}
      />
      <span>Movies only</span>
     </label>
     <label>
      <input 
       className="with-gap"
       name="type"
       type="radio"
       data-type="series"
       onChange={this.handleFilter}
       checked={this.state.type === 'series'}
      />
      <span>Series only</span>
     </label>
    </div>
    
  </div>
 }
}

export {Search}
```

Добавляем свои стили в index.css
```css
label:not(:last-child) {
 margin-right: 1rem;
}
```

Main.jsx
```jsx
import React from 'react'
import {Movies} from '../components/Movies'
import {Search} from '../components/Search'
import {Preloader} from '../components/Preloader'

class Main extends React.Component {
 state = {
  movies: [],
 }
 
 componentDidMount() {
  fetch("url")
   .then(response => response.json())
   .then(data => this.setState({movies: data.Search}))
 }
 
 searchMovies = (str, type = 'all') => {
  fetch(`url=${str}${type !== 'all' ? `&type=${type}` : ''}`)
   .then(response => response.json())
   .then(data => this.setState({movies: data.Search}))
 }
 
 render() {
  const {movies} = this.state;
 
  return <main className="container content">
   <Search searchMovies={this.searchMovies}/>
   {
    movies.lenght ? (<Movies movies={movies}/>) : <Preloader />
   }
  </main>
 }
}
```

## Обработка неудачного поиска

Main.jsx
```jsx
import React from 'react'
import {Movies} from '../components/Movies'
import {Search} from '../components/Search'
import {Preloader} from '../components/Preloader'

class Main extends React.Component {
 state = {
  movies: [],
  loading: true,
 }
 
 componentDidMount() {
  fetch("url")
   .then(response => response.json())
   .then(data => this.setState({movies: data.Search, loading: false}))
 }
 
 searchMovies = (str, type = 'all') => {
  this.setState({loading: true})
 
  fetch(`url=${str}${type !== 'all' ? `&type=${type}` : ''}`)
   .then(response => response.json())
   .then(data => this.setState({movies: data.Search, loading: false}))
 }
 
 render() {
  const {movies, loading} = this.state;
 
  return <main className="container content">
   <Search searchMovies={this.searchMovies}/>
   {
    loading ? (<Preloader />) : (<Movies movies={movies}/>)
   }
  </main>
 }
}
```

Movies.jsx
```jsx
import {Movie} from './Movie'

function Movies (props) {
 const {movies = []} = props;
 
 return <div className="movies">
  {movies.length ? movies.map(movie => (
   <Movie key={movie.imdbID} {...movie} />
  )) : <h4>Nothing found</h4>
  
  }
 </div>
}
export {Movies}
```

## Безапасное хранение ключа API

Создаем файл с названием `.env.local`

Создаем локальную переменную
`
REACT_APP_API_KEY=78584b3c
`

Main.jsx
```jsx
import React from 'react'
import {Movies} from '../components/Movies'
import {Search} from '../components/Search'
import {Preloader} from '../components/Preloader'

const API_KEY = process.env.REACT_APP_API_KEY;

class Main extends React.Component {
 state = {
  movies: [],
  loading: true,
 }
 
 componentDidMount() {
  fetch(`https://www.omdbapi.com/?apikey=${API_KEY}&s=matrix`)
   .then(response => response.json())
   .then(data => this.setState({movies: data.Search, loading: false}))
 }
 
 searchMovies = (str, type = 'all') => {
  this.setState({loading: true})
 
  fetch(`https://www.omdbapi.com/?apikey=${API_KEY}&s=${str}${type !== 'all' ? `&type=${type}` : ''}`)
   .then(response => response.json())
   .then(data => this.setState({movies: data.Search, loading: false}))
 }
 
 render() {
  const {movies, loading} = this.state;
 
  return <main className="container content">
   <Search searchMovies={this.searchMovies}/>
   {
    loading ? (<Preloader />) : (<Movies movies={movies}/>)
   }
  </main>
 }
}
```
