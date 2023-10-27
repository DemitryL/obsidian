##### Настройка имени для git локально
~~~
git config --global user.name "<name>"
~~~
##### Настройка email для git локально
~~~
git config --global user.email "<email>""
~~~
##### Проверка настройки git
~~~
git config --list
~~~
### Создание нового репозитороя вводить в папке проекта
~~~
git init
~~~
После инициализации создается скрытая папка  **.git**
### : Основные команды Git
##### Текущее состояние репозитория 
~~~
git status
~~~
##### Подготовка файлов перед коммитом
~~~
git add <files> or git add .
~~~
##### Создание коммита с записью изменений в репозиторий
~~~
git commit -m "<message>"
~~~
##### Посмотреть истории изменений (коммитов)
~~~
git log
~~~
##### Переход в определенную версию проекта по SHA1 хешу коммита
~~~
git checkout <commit hash>
~~~
##### Переход в определенную версию проекта по названию ветки
~~~
git checkout <branch name>
~~~
##### Тип файла (хеша)
~~~
git cat-file -t <hash>
~~~
##### Содержимое хеша
~~~
git cat-file -p <hash>
~~~
##### Создание новой ветки
~~~
git branch <branch name>
~~~
##### Переход в новую ветку перемещая HEAD
~~~
git checkout <branch name>
~~~
##### Создание новой ветки и переход в нее
~~~
git checkout -b <branch name>
~~~
##### Отображает список всех веток
~~~
git branch
~~~
##### Переименование текущей ветки
~~~
git branch -m <new branch name>
~~~
##### Удаление ветки (текущую ветку удалять нельзя)
~~~
git branch -d <branch name>
~~~
##### Слияние другой ветки (feature branch) в текущую ветку (receiving branch)
~~~
git merge <feature branch name>
~~~

## Links:
[[IT]]	