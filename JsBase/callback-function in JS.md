## Что такое коллбэк?

**Простыми словами:** коллбэк — это функция, которая должна быть выполнена после того, как другая функция завершила выполнение (отсюда и название: callback — функция обратного вызова).

**Чуть сложнее:** В JavaScript функции — это объекты. Поэтому функции могут принимать другие функции в качестве аргументов, а также возвращать функции в качестве результата. Функции, которые это умеют, называются функциями высшего порядка. А любая функция, которая передается как аргумент, называется callback-функцией.

## Зачем нужны коллбэки?

По одной простой причине: JavaScript — это [событийно-ориентированный язык](http://ru.hexlet.io/professions/frontend?promo_name=prof-frontend&promo_position=article-body&promo_type=link). Поэтому вместо того, чтобы ждать ответа для дальнейшего выполнения программы, JavaScript продолжит выполнение, одновременно ожидая других событий. Давайте разберем простой пример:
```js
const first = () => {
  console.log(1);
};

const second = () => {
  console.log(2);
};

first();
second();
```

Как вы и ожидаете, функция `first` выполнится первой, а функция `second` уже после нее. Поэтому в консоли будет выведен следующий результат:

```
// 1
// 2
```

Пока что все понятно. Но что, если функция `first` содержит некий код, который не может выполниться немедленно? К примеру, работа с API, где мы отправляем запрос и должны ждать ответа. Чтобы смоделировать такую ситуацию, мы используем функцию `setTimeout`, которая вызывает функцию после заданного временного промежутка. Мы отсрочим выполнение функции на 500 миллисекунд, как будто бы это запрос к некому API. Теперь код будет выглядеть так:
```js
const first = () => {
  // Как будто бы запрос к API
  setTimeout(() => {
    console.log(1);
  }, 500 );
};

const second = () => {
  console.log(2);
};

first();
second();
```

Неважно, понимаете ли вы сейчас, как работает `setTimeout()`. Основная идея — теперь мы отложили исполнение команды `console.log(1)` на 500 миллисекунд. И что теперь выведет наша программа?

```
first();
second();
// 2
// 1
```

Хотя мы по-прежнему вызываем функцию `first` первой, ее вывод появился вторым, после вывода функции `second`. Но JavaScript не нарушает порядок вызова функций, он просто не дожидается ответа от функции `first`, а сразу двигается дальше — к функции `second`.

Поэтому нельзя просто вызывать функции в нужном порядке и надеяться, что они в любом случае выполнятся в том же порядке. Коллбэки же позволяют нам быть уверенными в том, что определенный код не начнет исполнение до того момента, пока другой код не завершит исполнение.

## Создаем коллбэк

Во-первых, откройте консоль разработчика в Google Chrome (Windows: Ctrl + Shift + J)(Mac: Cmd + Option + J), либо свой IDE, либо просто Repl.it, и введите в консоли следующую функцию:

```js
const doHomework = (subject) => {
  alert(`Starting my ${subject} homework.`);
};
```

Мы создали функцию `doHomework`. Наша функция принимает одну переменную — название предмета, которым мы будем заниматься. Вызовите функцию, набрав следующий текст в консоли:

```js
doHomework('math');
// Выводит алерт: Starting my math homework.
```

Теперь давайте добавим в определение функции еще один параметр, это и будет наш коллбэк. Затем вызовем ее, определив функцию-callback в качестве аргумента:
```js
const doHomework = (subject, callback) => {
  alert(`Starting my ${subject} homework.`);
  callback();
};

doHomework('math', () => {
  alert('Finished my homework');
});
```

Если вы введете этот код в консоли, вы получите два алерта один за другим, в первом будет сообщение о том, что выполнение домашнего задания началось (Starting my math homework.), а во втором — что вы закончили выполнять задание (Finished my homework).

Однако коллбэки не обязательно должны быть определены при вызове функции. Они могут быть определены и в другом месте кода, например, так:

```js
const doHomework = (subject, callback) => {
  alert(`Starting my ${subject} homework.`);
  callback();
};

const alertFinished = () => {
  alert('Finished my homework');
};

doHomework('math', alertFinished);
```

Таким образом, результат выполнения этого кода такой же, как и в предыдущем примере, однако сам код немного другой. Как вы видите, мы передали функцию `alertFinished` как аргумент в функцию `doHomework` при ее вызове.

Перепишем пример вызова функции с `setTimeout` для последовательного выполнения функций:

```js
const first = (callback) => {
  // Как будто бы запрос к API
  setTimeout(() => {
    console.log(1);
    callback();
  }, 500 );
};

const second = () => {
  console.log(2);
};

first(second);
// 1
// 2
```

## Пример из реальной жизни

На прошлой неделе я опубликовал статью «Создаем бота для Твиттера в 38 строк кода». Этот код работает благодаря API Твиттера. И когда мы делаем запрос к API, мы должны дождаться ответа до того, как начнем выполнять с этим ответом какие-то действия. Это прекрасный пример того, как в реальной жизни выглядит коллбэк. Вот как выглядит сам запрос:

```js
T.get('search/tweets', params, (err, data, response) => {
  if (!err) {
    // Происходит какая-то магия
  } else {
    console.log(err);
  }
});
```

`T.get` просто значит, что мы выполняем get запрос к API Твиттера. В запросе три параметра: `'search/tweets'` – это адрес (роут) запроса, `params` – наши параметры поиска и в конце передается анонимная функция-callback.

Коллбэк здесь нужен, потому что нам нужно дождаться ответа от сервера до того, как приступим к дальнейшему выполнению кода. Мы не знаем, успешным будет наш запрос или нет, поэтому после отправки параметров поиска на `search/tweets` через get-запрос, мы просто ждем. Как только Твиттер ответит, выполнится наша callback-функция. Твиттер отправит нам в качестве ответа или объект err (error – ошибка), или объект response. В коллбэке мы можем через if() проверить, был ли запрос успешным или нет, и затем действовать соответственно.


[[JS BASE]]
---