# PostgreSQL install and working on Ubuntu 

Обновим Ubuntu из терминала:
```bash
sudo apt-get update 
sudo apt-get upgrade
```
Установка postgresql в ubuntu происходит при помощи команды:

```bash
sudo apt install postgresql postgresql-contrib -y
```
После завершения установки PostgreSQL запустится автоматически. Однако вы можете сами проверить статус службы:

```bash
sudo systemctl status postgresql.service
```
OR
```bash
sudo service postgresql status
```

Для добавления в автозагрузку необходимо ввести команду:
```bash
sudo systemctl enable postgresql.service
```
Если по каким-либо причинам сервис не запустился автоматически, можно сделать это вручную:

```bash
sudo systemctl start postgresql.service
```
***Установка PostgreSQL успешно завершена, и программа готова к дальнейшей настройке.***

## Как настроить PostgreSQL и начать работать с СУБД

Прежде чем приступать к настройке инструмента, требуется проверить возможность подключения к нему. Во время установки PostgreSQL автоматически создает аккаунт с именем postgres. Авторизуемся при помощи него и войдем в аккаунт:

```bash
sudo -i -u postgres
```
Открываем консоль PostgreSQL:
```bash
psql
```
Обратите внимание, что данная команда выполняется без аргумента sudo. При успешной авторизации отобразится консоль.

Здесь же можно узнать статус подключения. Для этого воспользуемся командой:
```bash
\conninfo
```
В ответ отобразится вся информация о текущем подключении.

По умолчанию для пользователя postgres не назначен пароль, но мы рекомендуем его установить на данном этапе. Для этого требуется ввести команду:

```bash
\password
```
OR
```bash
\password postgres
```

Для выхода из консоли введите:
```bash
\q
```

Затем чтобы вернутся к нормальному режиму введите команду:
```bash
exit
```

## Create new user

```bash
sudo -i -u postgres
```

```bash
createuser --interactive
```

Enter name of role to add:
```bash
name_user // имя пользователя
```
Next create database:
```bash
createdb database_name
```

## Create new user Linux

```bash
sudo adduser name_user
```
Создаем пароль для входа под этого пользователя:

```bash
New password:
Retype new password:
  Full Name []: name_user
    Enter 
    Enter
    Enter
    Enter
    y
```

Переключится на созданного пользователя:
```bash
su name_user
```

Открытие psql и переход на базу данных:
```bash
psql -d database_name
```

```bash
\conninfo
```
