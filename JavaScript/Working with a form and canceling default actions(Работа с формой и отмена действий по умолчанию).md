Вернемся к нашей форме. Мы закончили на том, что событие Enter у нас переключало focus, на потом мы обернули наши элементы, поля для ввода, обернули в форму, и Enter приводит
к перезагрузке страницы.

Это действие браузера по умолчанию. Мы можем с ним работать. Каждый раз, когда мы работаем с event, мы можем отменять некое действие
браузера по умолчанию.
```js
event.preventDefault();
```
В любом случае event содержит некий
метод, который называется prevent, то бишь предотврати дефолт (Default). То есть предотвратить действие браузера по умолчанию.

Теперь, если я буду нажимать на Enter, у меня благополучно фокус будет переключаться так, как я этого хотел, несмотря на то, что сами inputs всё еще лежат внутри формы, форма не отправляется.

Я могу сначала проверить, что я нажал на клавишу Enter, а потом отменять действия по умолчанию. Oтменять действия по умолчанию нужно вполне в конкретных случаях.
```js
function handleEvent(event) {
 console.log(event);
 console.log(event.target);

 if(event.key === 'Enter') {
  event.preventDefault();
  event.target.nextElementSibling.focus();
 }
}
```

Как только я нажму на Enter на любой кнопке внутри формы, форма у меня отправится. 

Я могу захотеть сделать предварительную валидацию. Я хочу захотеть после этой валидации
отправить данные по средствам JavaScript, а не по средствам перезагрузки браузера.
```js
const form = document.querySelector('form');

form.addEventListener('submit', handleSubmit);

function handleSubmit(event) {
 event.preventDefault();
 validate();
}

function validate() {
 inputs.forEach(input => {
  if(!input.value.trim()) {
   input.style.borderColor = 'red'
  } else {
   input.style.borderColor = 'black'
  }
 })
}
```
Мы отменим отправку формы, вызовем нашу функцию с валидацией, и если что-то идет не так,
мы подкрасим все наши элементы. 

Поэтому я могу здесь завести переменную, которая у меня будет называться `isValid`,
валидная форма и сказать ей изначально,
что она у меня валидна. 

Внутри моего цикла, если хоть одна история у меня неправильная, я не только помечу ее красным, я моей переменной с валидностью скажу, что она больше у меня не валидна, и моя функция будет возвращать это значение через return.
```js
function handleSubmit(event) {
 event.preventDefault();
 console.log('submit');

 if (validate()){
  // submit AJAX
  form.reset();
 } else {
  alert('FIX empty fields');
 }
}

function validate() {
 let isValid = true;

 inputs.forEach(input => {
  if(!input.value.trim()) {
   input.style.borderColor = 'red';
   isValid = false;
  } else {
   input.style.borderColor = 'currentColor';
  }
 });

 return isValid;
}
```

Работая с формой, у нас есть возможность сбрасывать содержимое формы. В данном случае обращаюсь к моей форме, я могу вызвать у нее
встроенный метод reset, и она просто очистит содержимое.

