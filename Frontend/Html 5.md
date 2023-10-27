- [ ] 1. Теги, сематические теги
- [ ] 2. Разница между старым и новым Html
### Tags
![[html5.png]]

##### Tag для отображения описания сайта в поисковиках
~~~
<meta name="description" content="Описание">
~~~
##### Using a favicon
~~~
<link rel="shortcut icon" href="/favicon.ico" type="image/x-icon">
<link rel="icon" href="/favicon.ico" type="image/x-icon">
~~~
[Favicon generator](https://www.favicon-generator.org/)

#### Подключение шрифтов двумя способоми
-----
##### Подключение шрифтов online

[google fonts](https://fonts.google.com/?preview.text_type=paragraph&stylecount=1)
~~~css
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300&display=swap');

font-family: 'Roboto', sans-serif;
~~~
~~~html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300&display=swap" rel="stylesheet">
~~~

-----
##### Подключение шрифтов offline
[font generator](https://www.fontsquirrel.com/tools/webfont-generator)
~~~
@font-face {
  font-family: "Roboto";
  font-style: normal;
  font-weight: 400;
  /* Браузер сначала попробует найти шрифт локально */
  src: local("Roboto"),
       /* Если не получилось, загрузит woff2 */
       url("/fonts/roboto.woff2") format("woff2"),
       /* Если браузер не поддерживает woff2, загрузит woff */
       url("/fonts/roboto.woff") format("woff");
}

/* Теперь можно использовать шрифт */
body {
  font-family: "Roboto", "Arial", sans-serif;
}
~~~

----

[[IT]]
-----