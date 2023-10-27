## Общий обзор и синтаксис

### Fetch

Функция `fetch()` является методом объекта `window` в JavaScript и составляющей [Fetch API](https://developer.mozilla.org/ru/docs/Web/API/Fetch_API/Using_Fetch). Этот метод встроен в ядро современного JS, поэтому пользователям не нужно устанавливать никакого дополнительного кода. `Fetch()` позволяет нам получать данные из API асинхронно без установки дополнительных библиотек.

~~~javascript
fetch(url)
  .then((res) => {
    // код ответа
  })
  .catch((error) => {
    // код ошибки
  });
~~~
Приведенный выше фрагмент кода представляет собой простой запрос на получение с помощью функции `fetch()`. В методе `fetch()` есть один обязательный аргумент - `url`. Параметр `url` - это адрес, с которого пользователь хотел бы получать данные. Метод `fetch()` возвращает промис (Promise, или обещание), который может разрешиться в виде объекта ответа или отклонить его с ошибкой.

~~~javascript
fetch(url, {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify(data),
})
  .then((response) => response.json())
  .catch((error) => console.log(error));
~~~
Вторые аргументы в методе `fetch()` - это параметры, и они не являются обязательными. Если пользователь не передает параметры, запрос всегда получает и загружает контент с заданного URL. Промис возвращает объект ответа, и поэтому пользователям необходимо использовать другой метод для получения тела ответа. Есть несколько различных методов, которые пользователи могут использовать в зависимости от формата тела ответа:

- `response.json()`
- `response.text()`
- `response.blob()`
- `response.formData()`
- `response.arrayBuffer()`

Самым популярным является `response.json()`.

К сожалению, встроенной функции `fetch()` нет в Node.js, но есть полифил, такой как [node-fetch](http://npmjs.com/package/node-fetch). Существует несколько [известных вариаций](https://github.com/node-fetch/node-fetch/blob/master/docs/v3-LIMITS.md) между node-fetch и `fetch()` браузера.

### Axios

**Axios** - это библиотека JavaScript для выполнения HTTP-запросов из Node.js, XMLHttpRequest или браузера. Как современная библиотека, она основана на Promise API, Axios имеет некоторые преимущества, такие как защита от атак с подделкой межсайтовых запросов (CSFR). Чтобы иметь возможность использовать [библиотеку Axios](https://axios-http.com/), пользователи должны установить ее и импортировать в ваш проект, используя CDN, npm, Yarn или Bower.

~~~javascript
axios.get(url)
  .then((response) => console.log(response))
  .catch((error) => console.log(error));
~~~

Приведенный выше фрагмент кода представляет собой использование метода `get()` для получения и обработки как ответа от сервера, так и ошибки. Когда пользователи создают объект конфигурации, они могут определять набор [свойств](https://github.com/axios/axios#request-config). Наиболее распространены такие, как `url`, `baseURL`, `params`, `auth`, `headers`, `responseType` и `data`. В качестве ответа Axios возвращает промис, который разрешится с помощью объекта ответа или объекта ошибки. В объекте ответа есть следующие значения:

- `data`: фактическое тело ответа
- `status`:  код состояния HTTP вызова, например 200 или 404
- `statusText`: статус HTTP в виде текстового сообщения
- `headers`: заголовки - то же, что и в запросе
- `config`: запрос конфигурации
- `request`: объект XMLHttpRequest (XHR)

~~~javascript
axios({
  url: "http://api.com",
  method: "POST",
  header: {
    "Content-Type": "application/json",
  },
  data: { name: "Sabesan", age: 25 },
});
~~~
В `fetch()` пользователям необходимо работать с двумя обещаниями . В Axios они могут избегать шаблонов и писать более чистый и лаконичный код. Давайте посмотрим на отличия.  
Axios использует свойство `data`  для работы с данными, а `fetch()` - свойство `body`.  
Данные в `fetch()` преобразованы в строку.  
URL-адрес в `fetch()` передается как аргумент, а в Axios URL-адрес устанавливается в объекте конфигурации.

## Использование JSON

### Fetch

После применения метода `fetch()`, пользователям необходимо использовать какой-то метод для обработки данных ответа. Кроме того, когда пользователи отправляют тело с запросом, пользователям необходимо преобразовать данные в строку.

~~~javascript
fetch('url')
  .then((response) => response.json())
  .then((data) => console.log(data))
  .catch((error) => console.log(error));
~~~
В приведенном выше фрагменте кода с ответом пользователям необходимо использовать `response.json()`, а затем  написать обработку ответа, в который поступают данные. То есть процесс всегда будет двухэтапным.

### Axios

В Axios пользователи передают данные в запросе или получают данные из ответа, причем данные **автоматически преобразовываются в строку**. Следовательно, никаких других операций не требуется.

~~~javascript
axios.get('url')
    .then((response)=>console.log(response))
    .catch((error)=>console.log(error))
~~~

В приведенном выше примере вы видите, что вам нужен всего один `then`.

Автоматическое преобразование данных - отличная функция и плюс в копилку Axios.

## Обработка ошибок (Error Handling)

### Fetch

Каждый раз, когда вы получаете ответ от метода `fetch()`, вам нужно проверять, является ли статус успешным, потому что даже если это не так, вы все равно получите ответ. В случае `fetch()` обещание не будет выполнено тогда и только тогда, когда не будет выполнен сам запрос.

~~~javascript
fetch('url')
    .then((response)=>{
        if(!response.ok){
            throw Error (response.statusText);
        }
        return response.json();
    })
    .then((data)=>console.log(data))
    .catch((error)=>console.log(error))<code class="jm kt ku kv kw b">
~~~
`Fetch()` не вызывает сетевых ошибок. Следовательно, вы всегда должны проверять свойство `response.ok` при работе с `fetch()`. Вы можете вынести проверку ошибок в функцию, чтобы сделать ее проще и удобнее для повторного использования.

~~~javascript
const checkError = response => {
    if (!response.ok) throw Error(response.statusText);
    return response.json();
  };
  
  fetch("url")
    .then(checkError)
    .then(data => console.log(data))
    .catch(error => console.log("error", error));
~~~
### Axios

В Axios обрабатывать ошибки довольно просто, потому что Axios выдает сетевые ошибки. Если будет неподходящий ответ, например с кодом 404, промис будет отклонен и вернет ошибку. Следовательно, вам нужно отловить ошибку, и вы можете проверить, что это была за ошибка.

~~~javascript
axios.get('url')
    .then((response)=> console.log(response))
    .catch((error)=>{
        if(error.response){
        // Когда код состояния ответа выходит за пределы диапазона 2xx
        console.log(error.response.data);
        console.log(error.response.status);
        console.log(error.response.headers);
        } else if (error.request){
            //Когда не был получен ответ после того, как запрос был сделан
            console.log(error.request);
        } else {
            // Ошибка
            console.log(error.message);
        }
    })
~~~
## Прогресс загрузки внешних файлов (download progress)

При загрузке больших активов индикаторы прогресса очень полезны для пользователей с низкой скоростью интернета.  Раньше для создания [индикаторов прогресса загрузки](https://html-plus.in.ua/use-progress-element-in-css-js/) разработчики использовали `XMLHttpRequest.onprogress` в качестве обработчика обратного вызова.
### Fetch

Чтобы отслеживать прогресс загрузки в `fetch()`, вы можете использовать одно из свойств `response.body`, объект [`ReadableStream`](https://learn.javascript.ru/fetch-progress). Он предоставляет фрагменты основных данных и позволяет подсчитать, сколько данных потребляется во времени.

~~~javascript
// original code: https://github.com/AnthumChris/fetch-progress-indicators
const element = document.getElementById('progress');

fetch('url')
  .then(response => {

    if (!response.ok) {
      throw Error(response.status+' '+response.statusText)
    }

    // убеждаемся, что ReadableStream поддерживается браузером
    if (!response.body) {
      throw Error('ReadableStream пока еще не поддерживается вашим браузером.')
    }

    // сохраняем размер тела объекта в байтах
    const contentLength = response.headers.get('content-length');

    // убеждаемся, что contentLength доступен
    if (!contentLength) {
      throw Error('Заголовок ответа Content-Length не доступен');
    }

    // преобразовываем целое число в число с основанием 10
    const total = parseInt(contentLength, 10);

    let loaded = 0;

    return new Response(

      // создаем и возвращаем объект ReadableStream
      new ReadableStream({
        start(controller) {
          const reader = response.body.getReader();

          read();
          function read() {
            reader.read().then(({done, value}) => {
              if (done) {
                controller.close();
                return; 
              }
              loaded += value.byteLength;
              progress({loaded, total})
              controller.enqueue(value);
              read();
            }).catch(error => {
              console.error(error);
              controller.error(error)                  
            })
          }
        }
      })
    );
  })
  .then(response => 
    // создать blob из данных  
    response.blob()
  )
  .then(data => {
    // вставляем загруженное изображение на страницу
    document.getElementById('img').src = URL.createObjectURL(data);
  })
  .catch(error => {
    console.error(error);
  })

function progress({loaded, total}) {
  element.innerHTML = Math.round(loaded/total*100)+'%';
}
~~~
В приведенном выше примере демонстрируется использование `ReadableStream` для предоставления пользователям прогресса загрузки изображений.
### Axios

В Axios также возможна реализация индикатора прогресса, и это даже проще, потому что существует готовый модуль, который можно установить и внедрить. Он называется [Axios Progress Bar.](https://github.com/rikmms/progress-bar-4-axios/)

~~~javascript
loadProgressBar();

function downloadFile(url) {
    axios.get(url, {responseType: 'blob'})
      .then(response => {
        const reader = new window.FileReader();
        reader.readAsDataURL(response.data); 
        reader.onload = () => {
          document.getElementById('img').setAttribute('src', reader.result);
        }
      })
      .catch(error => {
        console.log(error)
      });
}
~~~
## Прогресс загрузки файлов на сервер (Upload Progress)

### Fetch

Используя `fetch()`, вы не можете отслеживать процесс загрузки каких-либо файлов на сервер.

### Axios

В Axios, напротив, вы можете следить за процессом загрузки файлов, которые находятся на вашем компьютере или сервере.

~~~javascript
const config = {
    onUploadProgress: event => console.log(event.loaded)
  };

axios.put("/api", data, config);
~~~
## HTTP-перехват

Перехват может быть важен для вас, когда вам нужно проверить или изменить свой HTTP-запрос от приложения к серверу или наоборот - например, аутентификация, ведение журнала и т. д.

### Fetch

Fetch API по умолчанию не обеспечивает перехват HTTP. Существует возможность перезаписать метод `fetch()` и определить, что должно произойти во время отправки запроса, но это займет больше времени и строчек кода, да и может быть сложнее, чем использование функций Axios. Вы можете перезаписать глобальный метод `fetch()` и определить свой собственный перехватчик, как в следующем коде:

~~~javascript
fetch = (originalFetch => {
    return (...arguments) => {
      const result = originalFetch.apply(this, arguments);
        return result.then(console.log('Request was sent'));
    };
  })(fetch);
  
fetch('url')
    .then(response => response.json())
    .then(data => {
      console.log(data) 
    });
~~~
### Axios

HTTP-перехват Axios - одна из ключевых особенностей этой библиотеки, поэтому вам не нужно создавать дополнительный код для ее использования.

~~~javascript
// перехватчики запросов
axios.interceptors.request.use((config)=>{
    console.log('Запрос отправлен');
    return config;
})

// перехватчики запросов
axios.interceptors.response.use((response) => {
    // выполнить операцию в зависимости от ответа
    return response; 
})

axios.get('url')
    .then((response)=>console.log(response))
    .catch((error)=>console.log(error))
~~~
В приведенном выше коде методы `axios.interceptors.request.use()` и `axios.interceptors.response.use()` используются для определения кода, который будет запускаться перед отправкой HTTP-запроса.

## Тайм-аут ответа

### Fetch

`Fetch()` обеспечивает функцию тайм-аута ответа через интерфейс `AbortController`.

~~~javascript
const controller = new AbortController();
const signal = controller.signal;
const options = {
  method: 'POST',
  signal: signal,
  body: JSON.stringify({
    firstName: 'Sabesan',
    lastName: 'Sathananthan'
  })
};  
const promise = fetch('/login', options);
const timeoutId = setTimeout(() => controller.abort(), 5000);

promise
  .then(response => {/* handle the response */})
  .catch(error => console.error('timeout exceeded'));
~~~
В приведенном выше коде с помощью конструктора `AbortController.AbortController()` необходимо создать объект `AbortController`. Объект `AbortController` позволяет позже прервать запрос. В статье «[Глубокое понимание API Fetch JavaScript](https://medium.com/better-programming/deep-insights-into-javascripts-fetch-api-e8e8203c0965)» вы найдете информацию о том, как `signal` является свойством `AbortController`, который доступен только для чтения. `signal` предоставляет способ связаться с запросом или прервать его. Если сервер не отвечает менее чем через пять секунд, операция завершается вызовом `controller.abort()`.

### Axios

Используя необязательное свойство тайм-аута в объекте конфигурации, вы можете установить количество миллисекунд до завершения запроса.
~~~javascript
axios({
    method: 'post',
    url: '/login',
    timeout: 5000,    // 5 секунд тайм-аута
    data: {
      firstName: 'Sabesan',
      lastName: 'Sathananthan'
    }
  })
  .then(response => {/* заголовок ответа */})
  .catch(error => console.error('timeout exceeded'))
~~~
Одна из причин, по которой разработчики JavaScript выбирают Axios, а не `fetch()`, - простота установки тайм-аута.

## Параллельные запросы

### Fetch

Чтобы сделать несколько одновременных запросов, вы можете использовать встроенный метод `Promise.all()`. Просто передайте массив запросов `fetch()` в `Promise.all()`, а затем асинхронную функцию для обработки ответа.

~~~javascript
Promise.all([
  fetch('https://api.github.com/users/sabesansathananthan'),
  fetch('https://api.github.com/users/rcvaram')
])
.then(async([res1, res2]) => {
  const a = await res1.json();
  const b = await res2.json();
  console.log(a.login + ' has ' + a.public_repos + ' public repos on GitHub');
  console.log(b.login + ' has ' + b.public_repos + ' public repos on GitHub');
})
.catch(error => {
  console.log(error);
});
~~~
### Axios

Вы можете добиться указанного выше результата, используя метод `axios.all()`. Передайте все запросы на выборку в виде массива методу `axios.all()`. Назначьте свойства массива ответов отдельным переменным с помощью функции `axios.spread()`, например:

~~~javascript
axios.all([
  axios.get('https://api.github.com/users/sabesansathananthan'), 
  axios.get('https://api.github.com/users/rcvaram')
])
.then(axios.spread((obj1, obj2) => {
  // Оба запросв теперь завершены
  console.log(obj1.data.login + ' has ' + obj1.data.public_repos + ' public repos on GitHub');
  console.log(obj2.data.login + ' has ' + obj2.data.public_repos + ' public repos on GitHub');
}));
~~~
## Обратная совместимость

Обратная совместимость, или поддержка браузерами, может быть важна, если вы пишите код, который должен хорошо работать не только в современных браузерах, но и в устаревших или малопопулярных тоже.
## Fetch

Fetch API поддерживают браузеры Chrome 42+, Safari 10.1+, Firefox 39+ и Edge 14+. Полная совместимая таблица доступна на сайте [caniuse.com](https://caniuse.com/?search=Fetch). Чтобы реализовать функции, аналогичные `fetch()` в браузерах, которые не поддерживают этот метод, вы можете использовать `fetch()` с полифиллом, таким как [`windows.fetch()`](https://github.com/github/fetch).

Чтобы использовать **полифилл fetch**, установите его с помощью этой команды npm:
~~~javascript
import {fetch as fetchPolyfill} from 'whatwg-fetch'

window.fetch(...)   // use native browser version
fetchPolyfill(...)  // use polyfill implementation
~~~
Имейте в виду, что в некоторых старых браузерах вам может также понадобиться полифилл для промисов.
## Axios

Axios не похож на `fetch()`. Axios обеспечивает широкую поддержку браузеров. Даже старые браузеры, такие как IE11, могут без проблем запускать Axios. Полная таблица совместимости доступна в [документации Axios](https://github.com/axios/axios#browser-support).
## Заключение

Для большинства ваших нужд в HTTP-соединениях Axios предоставляет простой в использовании API в компактном виде. Есть несколько альтернативных библиотек для связи по протоколу HTTP, например [ky](https://github.com/sindresorhus/ky), крошечный и элегантный HTTP-клиент, основанный на `window.fetch`, или [superagent](https://www.npmjs.com/package/superagent) - небольшая прогрессивная клиентская библиотека HTTP-запросов, основанная на XMLHttpRequest.

Однако, Axios - это лучшее решение для приложений с большим количеством HTTP-запросов и для тех разработчиков, которым нужна хорошая обработка ошибок или перехват HTTP-запросов. В случае же небольших проектов с несколькими простыми вызовами Fetch API может быть лучшим выбором.


[[JAVASCRIPT]]
-----














