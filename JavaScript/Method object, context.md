```js
const developer = {
  name: 'Vasiliy',
  surname: 'Petrov',
  age: 30,
  skills: ['JavaScript', 'TypeScript', 'CSS'],
  isMaried: false,
  addAge() {
    this.age++;
  }
}
```

У нас есть очень интересная особенность,
касаемая объектов. У нас внутри объектов есть
так называемый контекст. Есть ключевое слово this.
Это this будет ссылаться на контекст того объекта, с которым мы сейчас работаем.

То есть в нашем случае этот this
равен всему этому объекту.

```js
developer.addAge(); // 31
```