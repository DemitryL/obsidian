##### Копирование удаленного репозитория локально
~~~
git clone <url>
~~~
### Отправка проекта на GitHub
-------
##### Создаем новый репозиторий
![[new-repo.png]]
##### Задаем имя репозиторию и выбираем публичный или приватный

![[repo.png]]

##### Проверяем что ветка названа main, если нет то вводим команду
~~~
git branch -M main
~~~
##### Подключаемся к удаленному репозиторию командой:
~~~
git remote add origin <link on repository>
~~~

##### Проверяем подлючение к репозиторию командой:
~~~
git remote -v
~~~
![[repo-add.png]]

##### Отправка локального репозитория на GitHub:
~~~
git push origin main
~~~
##### Далее вводим логин и пароль который является токином:
##### Coздаем токин, заходим в настройки(settings) далее в (Developer settings)  -> (Personal access tokens)  ->(Tokens(classic)) -> (Generate new token)

----
## Удаление репозитория на GitHub:

1. Заходим в репозиторий 
2. Settings
3. Delete this repository

#Link: [[IT]]



