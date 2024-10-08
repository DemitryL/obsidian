## Yarn / Yarn2

How to upgrade yarn version using terminal:

latest version: 
```bash
yarn set version stable
```

## Как начать работу?

### Установка
Yarn придерживается стратегии глобальной установки первой версии, а уже затем переключения на вторую для конкретного проекта.

Сначала установим глобальный Yarn, который мы будем использовать для создания локальных экземпляров:
```shell
❯ npm install -g yarn
```

Выполнив данную инструкцию (запуск `yarn --version` должен вывести что-то вроде `1.22.x`), перейдём к созданию каталога для запуска нового проекта:

```bash
❯ mkdir my-app
❯ cd my-app
```

“Berry” — кодовое имя релизной ветки Yarn 2.  
Изменим версию Yarn конкретно для каталога `my-app`:

```bash
❯ yarn set version berry
```

После выполнения данной команды установка будет завершена, и можно переходить к установке зависимостей!

### Добавление зависимостей

Общие команды управления остались теми же, что и в предыдущих версиях:

- `yarn init`  —  инициализация проекта
- `yarn add <package> [--dev]`  —  добавление пакета
- `yarn remove <package>`  —  удаление пакета
- `yarn up <package>`  —  обновление пакета

Также, вы можете увидеть некоторые изменения консольного интерфейса в новой версии Yarn:

- каждый набор связанных задач, выполняемых в процессе установки, сгруппирован;
- почти все сообщения имеют собственные коды ошибок, которые можно найти в [документации](https://yarnpkg.com/advanced/error-codes);
- цвета теперь используются только для обозначения важных частей каждого сообщения.

## Что в итоге

Ветка Yarn 1.x (Classic) уже официально перешла в статус поддержки, предполагающей только исправление уязвимостей.

Все новые функции будут разрабатываться исключительно для Yarn 2, версия которого будет распространяться через `yarn set version`.

Для React Native всё таки придётся подключать node modules.


### Yarn Gulp 

## 🛠️ Установка

- установите [NodeJS](https://nodejs.org/en/)
- установите глобально:
    - [Yarn](https://yarnpkg.com/getting-started): `npm i -g yarn`
    - [Gulp](https://gulpjs.com/): `npm i -g gulp`
    - [Bem Tools](https://www.npmjs.com/package/bem-tools-core): `npm i -g bem-tools-core`
- скачайте сборку с помощью [Git](https://git-scm.com/downloads): `git clone https://github.com/andreyalexeich/gulp-scss-starter.git`
- перейдите в скачанную папку со сборкой: `cd gulp-scss-starter`
- введите `yarn set version berry`
- скачайте необходимые зависимости: `yarn`
- чтобы начать работу, введите команду: `yarn run dev` (режим разработки)
- чтобы собрать проект, введите команду `yarn run build` (режим сборки)

Если вы всё сделали правильно, у вас должен открыться браузер с локальным сервером. Режим сборки предполагает оптимизацию проекта: сжатие изображений, минифицирование CSS и JS-файлов для загрузки на сервер.