
Переменная – это «именованное хранилище» для данных. Мы можем использовать переменные для хранения товаров, посетителей и других данных.

* Мы также можем объявить несколько переменных в одной строке:
~~~javascript
let user = 'John', age = 25, message = 'Hello';
~~~

* Такой способ может показаться короче, но мы не рекомендуем его. Для лучшей читаемости объявляйте каждую переменную на новой строке.
* Многострочный вариант немного длиннее, но легче для чтения:
~~~javascript
let user = 'John';
let age = 25;
let message = 'Hello';
~~~

* Например, переменную `message` можно представить как коробку с названием `"message"` и значением `"Hello!"` внутри:
![[Screenshot from 2023-09-01 20-13-39.png]]

Мы можем положить любое значение в коробку.
Мы также можем изменить его столько раз, сколько захотим:
~~~javascript
let message;
message = 'Hello!';
message = 'World!'; // значение изменено
alert(message);
~~~
При изменении значения старые данные удаляются из переменной:
![[Screenshot from 2023-09-01 20-14-07.png]]


## Константы
	: Чтобы объявить константную, то есть, неизменяемую переменную, используйте `const` вместо `let`:

1. Имя переменной должно содержать только буквы, цифры или символы `$` и `_`.
2. Первый символ не должен быть цифрой.

Примеры неправильных имён переменных:
~~~javascript
let 1a; // не может начинаться с цифры
let my-name; // дефис '-' не разрешён в имени
~~~
Переменные, объявленные с помощью `const`, называются «константами». Их нельзя изменить. Попытка сделать это приведёт к ошибке:
### Константы в верхнем регистре

* Широко распространена практика использования констант в качестве псевдонимов для трудно запоминаемых значений, которые известны до начала исполнения скрипта. Названия таких констант пишутся с использованием заглавных букв и подчёркивания.

Например, сделаем константы для различных цветов в «шестнадцатеричном формате»:
~~~javascript
const COLOR_RED = "#F00";
const COLOR_GREEN = "#0F0";
const COLOR_BLUE = "#00F";
const COLOR_ORANGE = "#FF7F00";
// ...когда нам нужно выбрать цвет
let color = COLOR_ORANGE;
alert(color); // #FF7F00
~~~
Другими словами, константы с именами, записанными заглавными буквами, используются только как псевдонимы для «жёстко закодированных» значений.

Несколько хороших правил:

- Используйте легко читаемые имена, такие как `userName` или `shoppingCart`.
- Избегайте использования аббревиатур или коротких имён, таких как `a`, `b`, `c`, за исключением тех случаев, когда вы точно знаете, что так нужно.
- Делайте имена максимально описательными и лаконичными. Примеры плохих имён: `data` и `value`. Такие имена ничего не говорят. Их можно использовать только в том случае, если из контекста кода очевидно, какие данные хранит переменная.
- Договоритесь с вашей командой об используемых терминах. Если посетитель сайта называется «user», тогда мы должны называть связанные с ним переменные `currentUser` или `newUser`, а не, к примеру, `currentVisitor` или `newManInTown`.

## Итого:
	: Мы можем объявить переменные для хранения данных с помощью ключевых слов `var`, `let` или `const`.

- `let` – это современный способ объявления.
- `var` – это устаревший способ объявления. Обычно мы вообще не используем его, но мы рассмотрим тонкие отличия от `let` в главе Устаревшее ключевое слово "var" на случай, если это всё-таки вам понадобится.
- `const` – похоже на `let`, но значение переменной не может изменяться.




