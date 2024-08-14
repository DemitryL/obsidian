## Управляемые компоненты - принцып единой ответственности

App.js
```jsx
import {Form} form './components/Form'

function App() {
 return (
  <div className="App">
   <Form />
  </div>
 )
}

export default App;

```

components -> Form.jsx
```jsx
import React from 'react'

class Form extends React.Component {
 state = {
  firstName: '',
  email: '',
 }
 
 handleChange = (event) => {
  {/* name - прилетает динамически */}
  this.setState({[event.target.name]: event.target.value})
 }
 
 render() {
  {/* Деструктуризация */}
  const {firstName, email} = this.state;
 
  return <div>
   <input 
    type="text" 
    name="firstName"
    placeholder="firstName"
    value={firstName}
    onChange={this.handleChange}
   />
   <input 
    type="email" 
    name="email"
    placeholder="email"
    value={email}
    onChange={this.handleChange}
   />
  </div>
 }
}

export {Form}
```


## Валидация значений формы

Простой пример валидации на момент когда поле больше не активно

```jsx
validateName = () => {
 {/* проверяем firstName на количество символов */}
 if (this.state.firstName.length < 5) {
  alert('Your first name can\'t be less than 7 letters')
 }
}
```

```
 render() {
  {/* Деструктуризация */}
  const {firstName, email} = this.state;
 
  return <div>
   <input 
    type="text" 
    name="firstName"
    placeholder="firstName"
    value={firstName}
    onChange={this.handleChange}
    onBlur={this.validateName}
   />
  
  </div>
 }
```

#### Validate Email

```
validateEmail  = () => {
  if (!/^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(this.state.email))
  {
   alert('email is not valid')
  }
}
```

```
render() {
  {/* Деструктуризация */}
  const {firstName, email} = this.state;
 
  return <div>
   <input 
    type="email" 
    name="email"
    placeholder="email"
    value={email}
    onChange={this.handleChange}
    onBlur={this.validateEmail}
   />
  </div>
 }
```

## Элементы checkbox, radio button, select, textarea


#### Textarea
```jsx
import React from 'react'

class Form extends React.Component {
 state = {
  message: '',
 }
 
 handleChange = (event) => {
  {/* name - прилетает динамически */}
  this.setState({[event.target.name]: event.target.value})
 }
 
 render() {
  {/* Деструктуризация */}
  const {message} = this.state;
 
  return <div>
   <textarea name="message" value={message} onChange={this.handleChange} />
  </div>
 }
}

export {Form}
```

#### Select
```jsx
import React from 'react'

class Form extends React.Component {
 state = {
  select: '',
 }
 
 handleChange = (event) => {
  {/* name - прилетает динамически */}
  this.setState({[event.target.name]: event.target.value})
 }
 
 render() {
  {/* Деструктуризация */}
  const {select} = this.state;
 
  return <div>
   <select name="select" value={select} onChange={this.handleChange}>
    <option value="" disable></option>
    <option value="1">1</option>
    <option value="2">2</option>
    <option value="3">3</option>
   </select>
  </div>
 }
}

export {Form}
```

#### Checkbox
```jsx
import React from 'react'

class Form extends React.Component {
 state = {
  subscription: false,
 }
 
 handleCheckboxChange = (event) => {
  {/* name - прилетает динамически */}
  this.setState({[event.target.name]: event.target.checked})
 }
 
 render() {
  {/* Деструктуризация */}
  const {subscription} = this.state;
 
  return <div>
  <label>
   <input 
    type="checkbox" 
    name="subscription" 
    checked={subscription}
    onChange={this.handleCheckboxChange}
   />
   Subscription
  </label>
  </div>
 }
}

export {Form}
```

#### Radio button
```jsx
import React from 'react'

class Form extends React.Component {
 state = {
  gender: '',
 }
 
 handleChange = (event) => {
  {/* name - прилетает динамически */}
  this.setState({[event.target.name]: event.target.value})
 }
 
 render() {
  {/* Деструктуризация */}
  const {gender} = this.state;
 
  return <div>
   <input 
    type="radio" 
    name="gender"
    value="male"
    onChange={this.handleChange}
    checked={gender === "male"}
   /> Mail
  <input
   type="radio"
   name="gender"
   value="female"
   onChange={this.handleChange}
   checked={gender === "female"}
  /> Female
  </div> 
 }
}

export {Form}
```

## Создание формы подписки


```jsx
import React from 'react'

class Form extends React.Component {
 state = {
  email: '',
  subscription: false,
 }
 
 handleChange = (event) => {
  this.setState({[event.target.name]: event.target.value})
 }
 
 handleCheckbox = (event) => {
  this.setState({[event.target.name]: event.target.checked})
 }
 
 handleSubmit = () => {
   const isValidEmail = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/.test(this.state.email.toLocalLowerCase())
   
   const isValidCheckbox = this.state.subcription
   
   if(!isValidEmail) {
    alert('Your email is not valid')
    return
   }
   
   if(!isValidCheckbox) {
    alert('You should accept all terms and conditions')
    return
   }
   
   this.setState({
    email: '',
    subscription: false,
   })
   alert('Thank you for subscription!')
 }
 
 render() {
  {/* Деструктуризация */}
  const {email,subscription} = this.state;
 
  return <div>
   <input 
    type="email" 
    name="email"
    placeholder="email"
    value={email}
    onChange={this.handleChange}
    onBlur={this.validateEmail}
   />
   
   <label>
   <input 
    type="checkbox" 
    name="subscription" 
    checked={subscription}
    onChange={this.handleCheckbox}
   />
   I agree with terms and conditions
  </label>
  
  <button onClick={this.handleSubmit}>Send</button>
  </div>
 }
}

export {Form}
```

## Использование рефа управление фокусом

```jsx
import React from 'react'

class FormWithRef extends React.Component {
 constructor() {
  super();
  this.state = {
   card: '',
   email: '',
  }
  this.firstNameRef = React.createRef();
  this.emailRef = React.createRef();
 }
 
 handleChange = (event) => {
  this.setState(() => ({[event.target.name]: event.target.value}), () => {
   if(this.state.card.length === 16) {
    this.emailRef.current.focus();
   }
  })
 }
 
 componentDidMount() {
  console.log(this.firstNameRef)
  this.firstNameRef.current.focus();
 }
 
 render() {
  const {card, email} = this.state;
 
  return <div>
   <input 
    type="text" 
    name="card"
    placeholder="card"
    value={card}
    onChange={this.handleChange}
    ref={this.firstNameRef}
   />
   <input 
    type="email" 
    name="email"
    placeholder="email"
    value={email}
    onChange={this.handleChange}
    ref={this.emailRef}
   />
  </div>
 }
}

export {Form}
```

## Неуправляемые компоненты

Работая с неуправляемыми компонентами мы не должны вешать какието обработчики, они должны принудительно брать из стейта и в самом стейте мы тоже не храним значения. Как правило мы просто должны создать реф на каждое поле и с каждым полем работать и этот реф в соответствующее место повесить.

```jsx
import React from 'react'

class FormWithRef extends React.Component {
 constructor() {
  super();

  this.cardRef = React.createRef();
  this.emailRef = React.createRef();
 }
 
 handleSubmit = (event) => {
  event.preventDefault();
  if (this.cardRef.current.value.length < 16) {
   alert('invalid card number');
   return;
  }
  
  // send
  
  this.cardRef.current.value = '';
  this.emailRef.current.value = '';
 }
 
 render() {
 
  return <form onSubmit={this.handleSubmit}>
   <input 
    type="text" 
    name="card"
    placeholder="card"
    ref={this.cardRef}
   />
   <input 
    type="email" 
    name="email"
    placeholder="email"
    ref={this.emailRef}
   />
  </form>
 }
}

export {Form}
```

