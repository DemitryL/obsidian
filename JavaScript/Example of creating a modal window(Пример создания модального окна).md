Итак, рассмотрим пример создания модельного окна.

Add html 
```html
<button id="myBtn">Open Modal</button>

<!--- The Modal --->
<div id="myModal" class="modal">
 <!--- Modal content --->
 <div class="modal-content">
  <span class="close">&times;</span>
  <p>Some text in the Modal..</p>
 </div>
</div>
```

Add `Css`
```css
.modal {
 display: none;
 position: fixed;
 z-index: 1;
 left: 0;
 top: 0;
 width: 100%;
 height: 100%;
 overflow: auto;
 background-color: rgba(0, 0, 0, .4);
}
.open {
 display: block;
}
.modal-content {
 background-color: #fefefe;
 margin: 15% auto;
 padding: 20px;
 border: 1px solid #888;
 width: 80%;
}
.close {
 color: #aaa;
 float: right;
 font-size: 28px;
 font-weight: bold;
}
.close:hover,
.close:focus {
 color: black;
 text-decoration: none;
 cursor: pointer;
}
```

Add JavaScript
```js
const btn = document.getElementById('myBtn');
const modal = document.gerElementById('myModal');

btn.addEventListener('click', openModal);

function openModal() {
 modal.classList.add('open');
 attachModalEvents();
}

function attachModalEvents() {
 modal.querySelector('.close').addEventListener('click', closeModal);
 document.addEventListener('keydown', handleEscape);
 modal.addEventListener('click', handleOutside);
}

function handleEscape(event) {
 if(event.key === 'Escape'){
  closeModal();
 }
}

function handleOutside(event) {
 const isClickOutside = !!event.target.closest('.modal-content');

 if (!isClickOutside) {
  closeModal();
 }
}

function closeModal() {
 modal.classList.remove('open');

 detachModalEvents();
}

function detachModalEvents() {
 modal.querySelector('.close').removeEventListener('click', closeModal);
 document.removeEventListener('keydown', handleEscape);
 modal.removeEventListener('click', handleOutside);
}
```

