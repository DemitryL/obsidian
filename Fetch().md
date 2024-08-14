JavaScript может отправлять сетевые запросы на сервер и подгружать новую информацию по мере необходимости.

Например, мы можем использовать сетевой запрос, чтобы:

- Отправить заказ,
- Загрузить информацию о пользователе,
- Запросить последние обновления с сервера,
- …и т.п.

Для сетевых запросов из JavaScript есть широко известный термин «AJAX» (аббревиатура от **A**synchronous **J**avaScript **A**nd **X**ML). XML мы использовать не обязаны, просто термин старый, поэтому в нём есть это слово.

Базовый синтаксис:

```javascript
let promise = fetch(url, [options])
```

- **`url`** – URL для отправки запроса.
- **`options`** – дополнительные параметры: метод, заголовки и так далее.

Без `options` это простой GET-запрос, скачивающий содержимое по адресу `url`.

Процесс получения ответа обычно происходит в два этапа.

**Во-первых, `promise` выполняется с объектом встроенного класса Response в качестве результата, как только сервер пришлёт заголовки ответа.**

Промис завершается с ошибкой, если `fetch` не смог выполнить HTTP-запрос, например при ошибке сети или если нет такого сайта. HTTP-статусы 404 и 500 не являются ошибкой.

Мы можем увидеть HTTP-статус в свойствах ответа:

- **`status`** – код статуса HTTP-запроса, например 200.
- **`ok`** – логическое значение: будет `true`, если код HTTP-статуса в диапазоне 200-299.

Например:

```javascript
let response = await fetch(url);

if (response.ok) { // если HTTP-статус в диапазоне 200-299
  // получаем тело ответа (см. про этот метод ниже)
  let json = await response.json();
} else {
  alert("Ошибка HTTP: " + response.status);
}
```

**Во-вторых, для получения тела ответа нам нужно использовать дополнительный вызов метода.**

`Response` предоставляет несколько методов, основанных на промисах, для доступа к телу ответа в различных форматах:

- **`response.text()`** – читает ответ и возвращает как обычный текст,
- **`response.json()`** – декодирует ответ в формате JSON,
- **`response.formData()`** – возвращает ответ как объект `FormData` (разберём его в [следующей главе](https://learn.javascript.ru/formdata)),
- **`response.blob()`** – возвращает объект как [Blob](https://learn.javascript.ru/blob) (бинарные данные с типом),
- **`response.arrayBuffer()`** – возвращает ответ как [ArrayBuffer](https://learn.javascript.ru/arraybuffer-binary-arrays) (низкоуровневое представление бинарных данных),
- помимо этого, `response.body` – это объект [ReadableStream](https://streams.spec.whatwg.org/#rs-class), с помощью которого можно считывать тело запроса по частям. Мы рассмотрим и такой пример несколько позже.

Например, получим JSON-объект с последними коммитами из репозитория на GitHub:

```javascript
let url = 'https://api.github.com/repos/javascript-tutorial/en.javascript.info/commits';
let response = await fetch(url);

let commits = await response.json(); // читаем ответ в формате JSON

alert(commits[0].author.login);
```

То же самое без `await`, с использованием промисов:

```javascript
fetch('https://api.github.com/repos/javascript-tutorial/en.javascript.info/commits')
  .then(response => response.json())
  .then(commits => alert(commits[0].author.login));
```

## Итого

Типичный запрос с помощью `fetch` состоит из двух операторов `await`:

```javascript
let response = await fetch(url, options); // завершается с заголовками ответа
let result = await response.json(); // читать тело ответа в формате JSON
```

Или, без `await`:

```javascript
fetch(url, options)
  .then(response => response.json())
  .then(result => /* обрабатываем результат */)
```

Параметры ответа:

- `response.status` – HTTP-код ответа,
- `response.ok` – `true`, если статус ответа в диапазоне 200-299.
- `response.headers` – похожий на `Map` объект с HTTP-заголовками.

Методы для получения тела ответа:

- **`response.text()`** – возвращает ответ как обычный текст,
- **`response.json()`** – декодирует ответ в формате JSON,
- **`response.formData()`** – возвращает ответ как объект FormData (кодировка form/multipart, см. следующую главу),
- **`response.blob()`** – возвращает объект как [Blob](https://learn.javascript.ru/blob) (бинарные данные с типом),
- **`response.arrayBuffer()`** – возвращает ответ как [ArrayBuffer](https://learn.javascript.ru/arraybuffer-binary-arrays) (низкоуровневые бинарные данные),

Опции `fetch`, которые мы изучили на данный момент:

- `method` – HTTP-метод,
- `headers` – объект с запрашиваемыми заголовками (не все заголовки разрешены),
- `body` – данные для отправки (тело запроса) в виде текста, `FormData`, `BufferSource`, `Blob` или `UrlSearchParams`.

В следующем примере используем `.then()` — обработчик результата, полученного от асинхронной операции. Обработчик дождётся ответа от сервера, принимает ответ, и, в данном случае, неявно вернёт ответ, обработанный методом `.json()`.

```js
fetch('http://jsonplaceholder.typicode.com/posts')
  .then((response) => response.json()
  // Получим ответ в виде массива из объектов:
  // [{...}, {...}, {...}, ...]
)
```

