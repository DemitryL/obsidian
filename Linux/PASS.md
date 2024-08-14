[Link](https://www.passwordstore.org/) 

Устанавливаем пакет gpg в терминале вводим :
```shell
// Ubuntu 
sudo apt-get update
sudo apt-get -y install gpg

// Next
gpg --full-gen-key // generait key
(1) RSA and RSA (default) // type key
4096 // max length key

// time live key
0 // not expire
Yes

real name:
real email:
comment: My Keys!

(O)kay

Passphrase:******  // password securite
Duble passphrase:******
```

#### Итак, что же означают все эти странные последние строки:

**rsa** — Алгоритм шифрования RSA.  
**4096** — Длина ключа.  
**1970-01-01** — Дата создания ключа.  
**2BB680...E426AC** — Отпечаток ключа. Его следует сверять при импортировании чужого публичного ключа — у обоих сторон он должен быть одинаков.  
**uid** — Идентификатор (User-ID).  
**pub** и **sub** — Типы ключа:

**pub** — Публичный ключ.  
**sub** — Публичный подключ.  
**sec** — Секретный ключ.  
**ssb** — Секретный подключ.

### Конфигурация

Далее заходим в директорию .gnupg смотрим есть ли файл gpg.conf если нет то создаем, записываем в него данные:
```conf
echo "keyid-format 0xlong
> throw-keyids
> no-emit-version
> no-comments" > ~/.gnupg/gpg.conf
```

Файл конфигурации хранится в файле `~/.gnupg/gpg.conf`  
Вот, например, пример моего файла конфигурации, который я рекомендую себе поставить:

```
keyid-format 0xlong
throw-keyids
no-emit-version
no-comments
```

`keyid-format 0xlong` — формат вывода идентификатора ключа. У каждого ключа и подключа есть свой идентификатор. По умолчанию он не выводится, раньше выводилась его короткая версия.  
Доступные форматы:  
`none` — Не выводить (По умолчанию).  
`short` — Короткая запись.  
`0xshort` — Короткая запись с префиксом "0x".  
`long` — Длинная запись.  
`0xlong` — длинная запись с префиксом "0x".

`throw-keyids` — Не включать информацию о ключе в зашифрованное сообщение. Эта опция может быть полезна для анонимизации получателя сообщения.

`no-emit-version` — Не вставлять версию GPG в зашифрованное сообщение.

`no-comments` — Убирает все комментарии из зашифрованного сообщения.

Показать  ключи :
```shell
gpg -k  // публичные ключи
gpg -K  // приватные ключи
```

Ширфрование файла:
```shell
gpg -e -a -r "email или id key(/0x0A9C26BF7FCAC71F)" file.txt 
// -e(`--encrypt`/зашифровать) -a(`--armor` в ASCII (символьный) формате сохранить) -r(`--recipient` указание ключа которым шифруем), емейл или айди ключа и файл который шифруем
```

Далее удаляем оригинал файла и остается только зашифрованная версия:
```shell
rm file.txt // delet orig file
```

Расшифровываем файл:
```shell
gpg -d -o file.txt file.txt.asc
// -d(`--decrypt`/расшифровать) -o(выходной файл) имя файла, файл который хотим расшифровать
```

#### **Примеры**
`gpg -a -r 0x12345678 -e decrypted.txt > encrypted.gpg`  
Зашифровать файл `decrypted.txt` в файл `encrypted.gpg` ключом `0x12345678`. При этом готовый файл будет текстовым, а не бинарным.

`gpg -r 0x12345678 -d encrypted.gpg > decrypted.txt`  
Расшифровать файл `encrypted.gpg` ключом `0x12345678` и сохранить его в файл `decrypted.txt`.

Экспорт ключей:
```shell
cd /tmp
gpg --export -a "email" > public.gpg // публичный ключ
gpg --export-secret-key -a "email" > secret.gpg
```

Удаление ключей с системы:
```shell
gpg --delete-secret-keys "email"
gpg --delete-keys "email"  // публичный ключ
```

Импорт ключей: 
```shell
gpg --import public.gpg // public key
gpg --import secret.gpg 
```

### Команды и опции
Я опишу только самое основное.

`--armor`  
`-a` — Создаёт ASCII (символьный) вывод.

`--encrypt`  
`-e` — Зашифровать сообщение.

`--recipient`  
`-r` — Указать ключ, который будет использоваться для _шифрования_

`--decrypt`  
`-d` — Расшифровать сообщение.

`--export` — экспортировать
`--import` — импортировать

### Работа с паролями 
Утилита pass работает на основе gpg позволяя шифровать данные.  __pass__ -  это менеджер паролей который для шифрования данных использует gpg

Установка pass:
```shell
// Manjaro 
sudo pacman -S pass

// Ubuntu
sudo apt-get update
sudo apt-get -y install pass
```

Иницилизируем хранилище pass куда будем ширровать пароли:
```shell
pass init "email" // email(указывает всю связку ключей)
```

Сохранение пароля для gmail:
```shell
pass insert Email/gmail.com
Enter password... : ****
Retype password... : ****
```

Pass -работает таким образом что каждый пароль хранится в отдельном файле

История паролей/ Password Store:
```shell
pass
```

Посмотреть сохраненный пароль :
```shell
pass Email/gmail.com
```

Info pass document:
```shell
pass --help | less
```

Сохранение несколько строк в файле при помощи флага -m :
```shell
pass insert Social/vk -m
Yes
login: login user
password: 23423223
description: lorem ipsum

Ctrl + d
```

Генирация паролей при помощи pass:
```shell
pass generate Email/mail.ru 15   // 15(длина пароля)
```

Удаление паролей при помощи pass:
```shell
pass rm Email/mail.ru
```

Все пароли хранятся в директориии `~/.password-store`
