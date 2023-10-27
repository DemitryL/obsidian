# Манипуляции с DOM на чистом JavaScript

Данная статья проведёт краткий экскурс в JavaScript DOM. Вы научитесь работе с ним, узнаете его преимущества и недостатки. Напишите свою библиотеку.

![Обложка поста dom-javascript](https://media.tproger.ru/uploads/2019/02/1490727404VanillaJS_DOM_manipulationA-01.png)

Как правило, когда нужно выполнить какие-либо действия с DOM, разработчики используют jQuery. Однако практически любую манипуляцию с DOM можно сделать и на чистом JavaScript с помощью его DOM API.

Рассмотрим этот API более подробно:

- DOM-запросыКак работать со списками?Добавление классов и атрибутовДобавление CSS-стилейИзменение DOMМетоды для элементовОбработчики событийПредотвращение действий по умолчаниюНаследованиеАнимацияПишем свою библиотекуПример использованияЗаключение

В конце вы напишете свою простенькую DOM-библиотеку, которую можно будет использовать в любом проекте.
### DOM-запросы

В материале представлены основы JavaScript DOM API. Все подробности и детали доступны на [Mozilla Developer Network](https://developer.mozilla.org/en-US/).

DOM-запросы осуществляются с помощью метода `.querySelector()`, который в качестве аргумента принимает произвольный СSS-селектор.
~~~javascript
const myElement = document.querySelector('#foo > div.bar')
~~~
Он вернёт первый подходящий элемент. Можно и наоборот — проверить, соответствует ли элемент селектору:
~~~javascript
myElement.matches('div.bar') === true
~~~
Если нужно получить все элементы, соответствующие селектору, используйте следующую конструкцию:
~~~javascript
const myElements = document.querySelectorAll('.bar')
~~~
Если же вы знаете, на какой родительский элемент нужно сослаться, можете просто проводить поиск среди его дочерних элементов, вместо того чтобы искать по всему коду:
~~~javascript
const myChildElemet = myElement.querySelector('input[type="submit"]') 
// Вместо: 
// document.querySelector('#foo > div.bar input[type="submit"]')
~~~
Возникает вопрос: зачем тогда использовать другие, менее удобные методы вроде `.getElementsByTagName()`? Есть маленькая проблема — результат вывода `.querySelector()` не обновляется, и когда мы добавим новый элемент (смотрите [раздел 5](https://tproger.ru/translations/dom-javascript#changeDOM)), он не изменится.
~~~javascript
const elements1 = document.querySelectorAll('div') 
const elements2 = document.getElementsByTagName('div') 
const newElement = document.createElement('div')  

document.body.appendChild(newElement) 
elements1.length === elements2.length // false
~~~

Также `querySelectorAll()` собирает всё в один список, что делает его не очень эффективным.

### Как работать со списками?

Вдобавок ко всему у `.querySelectorAll()` есть два маленьких нюанса. Вы не можете просто вызывать методы на результаты и ожидать, что они применятся к каждому из них (как вы могли привыкнуть делать это с jQuery). В любом случае нужно будет перебирать все элементы в цикле. Второе — возвращаемый объект является списком элементов, а не массивом. Следовательно, методы массивов не сработают. Конечно, есть методы и для списков, что-то вроде `.forEach()`, но, увы, они подходят не для всех случаев. Так что лучше преобразовать список в массив:
~~~javascript
// Использование Array.from()  
Array.from(myElements).forEach(doSomethingWithEachElement) 
// Или прототип массива (до ES6) 
Array.prototype.forEach.call(myElements, doSomethingWithEachElement) 
// Проще: 
[].forEach.call(myElements, doSomethingWithEachElement)
~~~

У каждого элемента есть некоторые свойства, ссылающиеся на «семью».
~~~javascript
myElement.children 
myElement.firstElementChild 
myElement.lastElementChild 
myElement.previousElementSibling 
myElement.nextElementSibling
~~~
Поскольку интерфейс элемента (`Element`) унаследован от интерфейса узла (`Node`), следующие свойства тоже присутствуют:
~~~javascript
myElement.childNodes 
myElement.firstChild 
myElement.lastChild 
myElement.previousSibling 
myElement.nextSibling 
myElement.parentNode 
myElement.parentElement
~~~
Первые свойства ссылаются на элемент, а последние (за исключением `.parentElement`) могут быть списками элементов любого типа. Соответственно, можно проверить и тип элемента:
~~~javascript
myElement.firstChild.nodeType === 3 // этот элемент будет текстовым узлом
~~~
### Добавление классов и атрибутов

Добавить новый класс очень просто:
~~~javascript
myElement.classList.add('foo') 
myElement.classList.remove('bar') myElement.classList.toggle('baz')
~~~
Добавление свойства для элемента происходит точно так же, как и для любого объекта:
~~~javascript
// Получение значения атрибута const value = myElement.value  

// Установка атрибута в качестве свойства элемента myElement.value = 'foo'  

// Для установки нескольких свойств используйте .Object.assign() 
Object.assign(myElement, {  
  value: 'foo',  
  id: 'bar' 
})  

// Удаление атрибута myElement.value = null
~~~
Можно использовать методы `.getAttibute()`, `.setAttribute()` и `.removeAttribute()`. Они сразу же поменяют HTML-атрибуты элемента (в отличие от DOM-свойств), что вызовет браузерную перерисовку (вы сможете увидеть все изменения, изучив элемент с помощью инструментов разработчика в браузере). Такие перерисовки не только требуют больше ресурсов, чем установка DOM-свойств, но и могут привести к непредвиденным ошибкам.

Как правило, их используют для элементов, у которых нет соответствующих DOM-свойств, например `colspan`. Или же если их использование действительно необходимо, например для HTML-свойств при наследовании (смотрите [раздел 9](https://tproger.ru/translations/dom-javascript#inheritance)).

### Добавление CSS-стилей

Добавляют их точно так же, как и другие свойства:
~~~javascript
myElement.style.marginLeft = '2em'
~~~
Какие-то определённые свойства можно задавать используя `.style`, но если вы хотите получить значения после некоторых вычислений, то лучше использовать `window.getComputedStyle()`. Этот метод получает элемент и возвращает [CSSStyleDeclaration](https://developer.mozilla.org/en-US/docs/Web/API/CSSStyleDeclaration), содержащий стили как самого элемента, так и его родителя:
~~~javascript
window.getComputedStyle(myElement).getPropertyValue('margin-left')
~~~
### Изменение DOM

Можно перемещать элементы:
~~~javascript
// Добавление element1 как последнего дочернего элемента 
element2 element1.appendChild(element2) 
// Вставка element2 как дочернего элемента element1 перед 
element3 element1.insertBefore(element2, element3)
~~~
Если не хочется перемещать, но нужно вставить копию, используем:
~~~javascript
// Создание клона 
const myElementClone = myElement.cloneNode() myParentElement.appendChild(myElementClone)
~~~
Метод `.cloneNode()`  принимает булевое значение в качестве аргумента, при `true` также клонируются и дочерние элементы.

Конечно, вы можете создавать новые элементы:
~~~javascript
const myNewElement = document.createElement('div') 
const myNewTextNode = document.createTextNode('some text')
~~~
А затем вставлять их как было показано выше. Удалить элемент напрямую не получится, но можно сделать это через родительский элемент:
~~~javascript
myParentElement.removeChild(myElement)
~~~
Можно обратиться и косвенно:
~~~javascript
myElement.parentNode.removeChild(myElement)
~~~
### Методы для элементов

У каждого элемента присутствуют такие свойства, как `.innerHTML` и `.textContent`, они содержат HTML-код и, соответственно, сам текст. В следующем примере изменяется содержимое элемента:
~~~javascript
// Изменяем HTML 
myElement.innerHTML = `   
 <div>     
   <h2>New content</h2     
   <p>beep boop beep boop</p>   
 </div> 
 `
   
 // Таким образом содержимое удаляется  myElement.innerHTML = null
   
 // Добавляем к HTML myElement.innerHTML += `   
 <a href="foo.html">continue reading...</a>   
 <hr/>
~~~
На самом деле изменение HTML — плохая идея, т. к. теряются все изменения, которые были сделаны ранее, а также перегружаются обработчики событий. Лучше использовать такой способ только полностью отбросив весь HTML и заменив его копией с сервера. Вот так:
~~~javascript
const link = document.createElement('a') 
const text = document.createTextNode('continue reading...') const hr = document.createElement('hr')  

link.href = 'foo.html' 
link.appendChild(text) 
myElement.appendChild(link) 
myElement.appendChild(hr)
~~~
Однако это повлечёт за собой две перерисовки в браузере, в то время как `.innerHTML` приведёт только к одной. Обойти это можно, если сначала добавить всё в [DocumentFragment](https://developer.mozilla.org/en-US/docs/Web/API/DocumentFragment), а затем добавить нужный вам фрагмент:
~~~
const fragment = document.createDocumentFragment()

fragment.appendChild(text) 
fragment.appendChild(hr) 
myElement.appendChild(fragment)
~~~
### Обработчики событий

Один из самых простых обработчиков:
~~~javascript
myElement.onclick = function onclick (event) {  console.log(event.type + ' got fired') 
}
~~~

Но, как правило, его следует избегать. Здесь `.onclick` — свойство элемента, и по идее вы можете его изменить, но вы не сможете добавлять другие обработчики используя ещё одну функцию, ссылающуюся на старую.

Для добавления обработчиков лучше использовать `.addEventListener()`. Он принимает три аргумента: тип события, функцию, которая будет вызываться всякий раз при срабатывании, и объект конфигурации (к нему мы вернёмся позже).
~~~javascript
myElement.addEventListener('click', function (event) {  console.log(event.type + ' got fired') 
})  

myElement.addEventListener('click', function (event) {  console.log(event.type + ' got fired again') 
})
~~~

Свойство `event.target` обращается к элементу, за которым закреплено событие.

А так вы сможете получить доступ ко всем свойствам:
~~~javascript
// Свойство `forms` — массив, содержащий ссылки на все формы 
const myForm = document.forms[0] 
const myInputElements = myForm.querySelectorAll('input') Array.from(myInputElements).forEach(el => {  el.addEventListener('change', function (event) {    console.log(event.target.value)  
 }) 
})
~~~
### Предотвращение действий по умолчанию

Для этого используется метод `.preventDefault()`, который блокирует стандартные действия. Например, он заблокирует отправку формы, если авторизация на клиентской стороне не была успешной:
~~~javascript
myForm.addEventListener('submit', function (event) {  
const name = this.querySelector('#name')   

if (name.value === 'Donald Duck') {    
  alert('You gotta be kidding!')    
  event.preventDefault()  
 }
})
~~~
Метод `.stopPropagation()` поможет, если у вас есть определённый обработчик события, закреплённый за дочерним элементом, и второй обработчик того же события, закреплённый за родителем.

Как говорилось ранее, метод `.addEventListener()` принимает третий необязательный аргумент в виде объекта с конфигурацией. Этот объект должен содержать любые из следующих булевых свойств (по умолчанию все в значении `false`):

- capture: событие будет прикреплено к этому элементу перед любым другим элементом ниже в DOM;
- once: событие может быть закреплено лишь единожды;
- passive: `event.preventDefault()` будет игнорироваться (исключение во время ошибки).

Наиболее распространённым свойством является `.capture`, и оно настолько распространено, что для этого существует краткий способ записи: вместо того чтобы передавать его в объекте конфигурации, просто укажите его значение здесь:
~~~javascript
myElement.addEventListener(type, listener, true)
~~~
Обработчики удаляются с помощью метода `.removeEventListener()`, принимающего два аргумента: тип события и ссылку на обработчик для удаления. Например свойство `once` можно реализовать так:
~~~javascript
myElement.addEventListener('change', function listener (event) {  console.log(event.type + ' got triggered on ' + this)  this.removeEventListener('change', listener) 
})
~~~

### Наследование

Допустим, у вас есть элемент и вы хотите добавить обработчик событий для всех его дочерних элементов. Тогда бы вам пришлось прогнать их в цикле, используя метод `myForm.querySelectorAll('input')`, как было показано выше. Однако вы можете просто добавить элементы в форму и проверить их содержимое с помощью `event.target`.
~~~javascript
myForm.addEventListener('change', function (event) {  
const target = event.target  
 if (target.matches('input')) {    
  console.log(target.value)  
 } 
})
~~~
И ещё один плюс данного метода заключается в том, что к новым дочерним элементам обработчик будет привязываться автоматически.

### Анимация

Проще всего добавить анимацию используя CSS со свойством `transition`. Но для большей гибкости (например для игры) лучше подходит JavaScript.

Вызывать метод `window.setTimeout()`, пока анимация не закончится, — не лучшая идея, так как ваше приложение может зависнуть, особенно на мобильных устройствах. Лучше использовать `window.requestAnimationFrame()` для сохранения всех изменений до следующей перерисовки. Он принимает функцию в качестве аргумента, которая в свою очередь получает метку времени:
~~~javascript
const start = window.performance.now() 
const duration = 2000  

window.requestAnimationFrame(function fadeIn (now)) {  
 const progress = now - start  
 myElement.style.opacity = progress / duration
    
 if (progress < duration) {    window.requestAnimationFrame(fadeIn)  
 } 
}
~~~

Таким способом достигается очень плавная анимация. В своей [статье](https://www.sitepoint.com/quick-tip-game-loop-in-javascript/) Марк Браун рассуждает на данную тему.

### Пишем свою библиотеку

Тот факт, что в DOM для выполнения каких-либо операций с элементами всё время приходится перебирать их, может показаться весьма утомительным по сравнению с синтаксисом jQuery `$('.foo').css({color: 'red'})`. Но почему бы не написать несколько своих методов, облегчающую данную задачу?
~~~javascript
const $ = function $ (selector, context = document) { 
const elements = Array.from(context.querySelectorAll(selector)) 

return {    
 elements,     
 html (newHtml) {      
  this.elements.forEach(element => {        
   element.innerHTML = newHtml      
  })       
  
  return this    
 },     
 
 css (newCss) {      
   this.elements.forEach(element => {        Object.assign(element.style, newCss)      
   })        
   
   return this    
   },     
   
   on (event, handler, options) {      this.elements.forEach(element => {        element.addEventListener(event, handler, options)     
   })       
   return this    
  }     

 } 
}
~~~
Теперь у вас есть своя маленькая библиотека, в которой находится всё, что вам нужно.

[Здесь](https://gist.github.com/SitePointEditors/4f6643d62a87aece860b0784 c6eeffd2) находится ещё много таких помощников.

На данный момент этот блок не поддерживается, но мы не забыли о нём!Наша команда уже занята его разработкой, он будет доступен в ближайшее время.

### Заключение

Теперь вы знаете, что для реализации простого модального окна или навигационного меню не обязательно прибегать к помощи сторонних фреймворков. Ведь в DOM API это уже всё есть, но, конечно, у данной технологии есть и свои минусы. Например всегда приходится вручную обрабатывать списки элементов, в то время как в jQuery это происходит по щелчку пальцев.


