**[RANGER](https://github.com/ranger/ranger)**

Установка ranger :
~~~bash
sudo apt install ranger
~~~

Запуск командой в терминале :
~~~bash
ranger
~~~

# Ranger. Лучший файловый менеджер для Linux.

## About Ranger

Вообще преимущества этого менеджера в том, что он очень гибкий, легко настраивается и имеет хоткеи как у Vim. Если вы работаете в Vim, то для вас это будет вообще сказка.

Например, для того чтобы перейти в начало мы можем нажать `gg`, а чтобы в конец `G`

Чтобы переименовать файл нажимаем `aa`

Для навигации можно использовать все те же привычные `H J K L`

Для того, чтобы найти файл используем `/` как в Vim

`i` откроет файл с помощью просмотрщика, `r` откроет меню “открыть с помощью”

`zh` покажет скрытые файлы

С помощью прбела можно выбрать несколько файлов и делать с ними что-нибудь.

`yy` как в Vim скопирует, `dd` вырежет `pp` вставит

## Вкладки

Есть удобная работа с вкладками

`CTRL+N` создаст новую вкладку

`CTRL+W` закроет текущую

`tab` перейдет на следующую вкладку `SHIFT+tab` предыдущую

`q` выход

## Shell

Так же можно выполнять любую команду Ranger-a шелла через `:`

И обычную команду через `!`

Отличиются режимы тем, что через `:` запускаются именно функции Ranger, например в Ranger есть своя функция chmod и если мы напишем `:chmod +x 1.sh` то нам выдаст ошибку, так как там другой синтаксис.

Но если введем `!chmod +x 1.sh` то все будет нормально, так как выполнится стандартная шеловская команда `chmod`

Мы так же можем не писать имя если выполняем команду для выделенного файла. Можем сделать просто `!chmod +x %f` или мы можем выбрать несколько файлов и сделать для них для всех `!chmod +x %s`

**chmod** – изменить права на текущий файл.

Также Ranger позволяет объединять файлы в группы для выполнения замены. Это делается при помощи заполнителей:

**%f**: заменить выделенный файл
**%d**: заменить текущий каталог
**%s**: заменить выбранные файлы
**%t** : заменить текущие отмеченные файлы.
## Themes

Ranger поставляется с 4 цветовыми темами:

_default_
_jungle_
_snow_
_solarized_
  
Чтобы изменить тему, добавьте "**set colorscheme**  `theme`" в rc.conf

## Алиасы

В `Ranger` есть очень удобные алисы, задаются они подобным образом:

```
map gd cd ~/Documents
map td tab_new ~/Documents
map md shell mv %s ~/Documents 
map Yd shell cp %s ~/Documents

map ga cd ~/Documents/Articles
map ta tab_new ~/Documents/Articles
map ma shell mv %s ~/Documents/Articles
map Ya shell cp %s ~/Documents/Articles

map gw cd ~/Documents/Work
map tw tab_new ~/Documents/Work
map mw shell mv %s ~/Documents/Work
map Yw shell cp %s ~/Documents/Work

map gb cd ~/Documents/Books
map tb tab_new ~/Documents/Books
map mb shell mv %s ~/Documents/Books
map Yb shell cp %s ~/Documents/Books

map gp cd ~/projects
```

При нажатии на `gd` я перейду в `~/Documents`

```
ga` перейду в `~/Documents/Articles
gp` перейду в `~/projects
```

То есть я всегда знаю, что кнопка `g` это вроде “go” а вторая буква это директория в которую я перейду. Это очень удобно и легко запоминается.

По такой же аналогии и с точно такими же вторыми буквами есть создание нового таба через кнопку `t`, копирование через кнопку `Y` и перемещение через кнопку `m`

На алиас я могу добавить абсолютно любую свою команду. Я вот уже показывал вам, что я могу нажать прость `x` и файлик скопируется на мой сервер и ссылка у меня окажется в буфере обмена.

Или я могу нажать на кнопку `Z` и все выделенные файлы у меня запакуются в `zip` архив. Нажать на кнопку `T` и выделенные файлы запакуются в `.tag.gz`

Можно легко работать с изображениями, например `C` поворачивает картинку на 90 градусов по часовой стрелке, а `F` зеркалит картинку по горизонтали.

## Сортировка

Сортировать файлы тоже довольно просто. os сортирует по размеру, `ob` по имени, `om` по времени создания файла, `oc` по времени изменения, `ot` по типу, `oe` по расширению.

## Конфигурирование

Настраивается Ranger в трех файлах

`rc.conf` - в котором находятся все ваши горячие клавиши и то, что загружается вместе с ranger
`scope.sh` — скрипт, чия задача определение типов файлов, работает на ranger, особого напилинга не требует

```
commands.py` - в котором будут все ваши кастомные функции запускаемые через `:
```

`rifle.conf` - в котором вы определяете какой тип файла какой программой открывать

### rifle.conf
Первый раз открыв этот файл можно взяться за голову и ощутить сильное желание его закрыть, больше никогда не видя оного. Но всё не так страшно :)

Тут прописаны файловые ассоциации к действию.
Разберём на примере для действия на «активацию» pdf файла:

ext pdf, has evince, X, flag f = evince -- "$@"

Теперь приведём это в более удачную цветовую раскраску:

ext `pdf`, has `evince`, X, flag f = `evince` -- "$@"

И осилим разобрать что к чему:
**ext** определяет действие к следующему сегменту - **pdf (тут может быть перечислено несколько типов файлов или целая группа, на пример video или audio)**, далее условия, **has evince** — если в системе есть гляделка пдф-файлов **evince, X, flag f** — условие при запуске в графической среде, и после «=» команда, что выполнит этот файл и «**$@**» - это внутренняя передача пути файла, это править не нужно. Суммируем — для создания собственных правил, вам необходимо изменить только зеленые переменные из примера.

Касательно того, что есть одно и то же правило, но на разные программы: первым выполниться то, что прошло все условия и выше по списку. Потому если вы имеете желание использовать конкретные программы в конкретных случаях — просто
закомментируйте лишнее.


-----

# Кастомизация ranger, install plugins :

### **[Image Previews](https://github.com/ranger/ranger/wiki/Image-Previews)**
##### With ueberzug
The original python version of ueberzug has been discontinued but an active fork rewrriten in c++ is available and works as a drop-in replacement.

- This will work with most terminals and even with tmux but requires X11. Doesn't work well with tabs.
    
- Install [ueberzugpp](https://github.com/jstkdng/ueberzugpp) or on Arch Linux it is also available in the [AUR](https://aur.archlinux.org/packages/ueberzugpp).

##### For **xUbuntu 22.04** run the following:

###### Keep in mind that the owner of the key may distribute updates, packages and repositories that your system will trust ([more information](https://help.ubuntu.com/community/SecureApt)).

```bash

echo 'deb http://download.opensuse.org/repositories/home:/justkidding/xUbuntu_22.04/ /' | sudo tee /etc/apt/sources.list.d/home:justkidding.list
curl -fsSL https://download.opensuse.org/repositories/home:justkidding/xUbuntu_22.04/Release.key | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/home_justkidding.gpg > /dev/null
sudo apt update
sudo apt install ueberzugpp

```


- Add the following lines to your `~/.config/ranger/rc.conf`.
    
    ```
    set preview_images true
    set preview_images_method ueberzug
    ```
    
- Restart ranger and navigate to an image file. \o/

### **[Ranger icons](https://github.com/alexanderjeurissen/ranger_devicons)**
Ranger has added support for loading directories in the plugins folder which makes it easier to install and keep plugins updated. To install, just clone the repo into the plugins folder:

~~~bash
git clone https://github.com/alexanderjeurissen/ranger_devicons ~/.config/ranger/plugins/ranger_devicons
~~~

Добавлем в конфиг  :
>  nvim rc.conf
  >>  default_linemode devicons  
  

### **[Ranger fzf](https://github.com/cjbassi/ranger-fzf/blob/master/__init__.py)**

```
commands.py` - в котором будут все ваши кастомные функции запускаемые через `:
```

~~~python

import os
import subprocess

import ranger.api.commands as ranger

class fzf(ranger.Command):
    """
    :fzf_select

    Find a file using fzf.

    With a prefix argument select only directories.
    """

    def execute(self):
        if self.quantifier:
            # match only directories
            command = "find -L . \( -path '*/\.*' -o -fstype 'dev' -o -fstype 'proc' \) -prune \
            -o -type d -print 2> /dev/null | sed 1d | cut -b3- | fzf +m"
        else:
            # match files and directories
            command = "find -L . \( -path '*/\.*' -o -fstype 'dev' -o -fstype 'proc' \) -prune \
            -o -print 2> /dev/null | sed 1d | cut -b3- | fzf +m"
        fzf = self.fm.execute_command(command, stdout=subprocess.PIPE)
        stdout, _ = fzf.communicate()
        if fzf.returncode == 0:
            fzf_file = os.path.abspath(stdout.decode('utf-8').rstrip('\n'))
            if os.path.isdir(fzf_file):
                self.fm.cd(fzf_file)
            else:
                self.fm.select_file(fzf_file)
                
~~~


### Для открытия файлов с помощью редактора nvim

Вносим код в файл 
~~~bash
~/ .bashrc
~~~

Code 
~~~bash
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion" # This loads nvm bash_completion

export VISUAL=nvim;
export EDITOR=nvim;
~~~

