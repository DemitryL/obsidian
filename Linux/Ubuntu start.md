  
Все ниже перечисленные команды нужно копировать в терминал. Терминал можно вызвать комбинацией **CTRL+ALT+T**.

Обновим Ubuntu из терминала:
```bash
sudo apt-get update 
sudo apt-get upgrade
```

Решаем проблему с отображением кириллицы в текстовом редакторе Gedit
```bash
gsettings set org.gnome.gedit.preferences.encodings candidate-encodings "['UTF-8', 'WINDOWS-1251', 'KOI8-R', 'CURRENT', 'ISO-8859-15', 'UTF-16']"
```

Устанавливаем дополнительную поддержку архиваторов
```bash
sudo apt install p7zip-rar rar unrar unace arj cabextract -y
```

Устанавливаем программы для работы с пакетами:
```bash
sudo apt install synaptic gdebi  -y
```

Устанавливаем скриншотер Flameshot и инструмент для создания GIF-анимации Peek
```bash
sudo apt-get install flameshot 
sudo apt-get install peek
```

Устанавливаем инструмент GNOME Tweaks для настройки рабочего окружения
```bash
sudo apt install gnome-tweaks -y
```

**Добавляем поддержку AppImage**

Если вы столкнулись с проблемой запуска программ AppImage в Ubuntu 22.04 LTS, то выполните следующие решение:
```bash
sudo apt install libfuse2 -y
```

Проблема состоит в том, что в Ubuntu 22.04 отсутствует библиотека FUSE (Filesystem in Userspace).

#### Install nodejs and npm:
Refresh your local package index first:
```bash
sudo apt update
```

Then install Node.js:
```bash
sudo apt install -y curl
sudo snap install node --channel=20/stable --classic
```

```
sudo apt install npm
```

#### Install Git from the default Ubuntu repository by running:
```bash
sudo apt install git
```

Синтаксис для работы с утилитой:
```bash
sudo apt опции команда имя_пакета
```
- **download** ― скачать, но не устанавливать пакет;
- **update** ― обновление информации о списках пакетов в репозиториях,
- **upgrade** ― обновление системы без удаления пакетов,
- **full-upgrade** ― полное обновление системы с удалением конфликтующих зависимостей,
- **install** ― установка пакета,
- **remove** ― удаление пакета, но без удаления конфигурационных файлов,
- **purge** ― полное удаление пакета,
- **autoremove** ― автоматическое удаление ненужных пакетов,
- **search** ― поиск пакета в локальной базе данных,
- **show** ― узнать информацию о пакете.

#### Oh my zsh 
```bash 
sudo apt install curl wget git
sudo apt-get install zsh

sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
Вы можете изменить оболочку по умолчанию на Zsh в Ubuntu, выполнив команду «chsh -s $(that zsh) » и введя свой пароль при появлении запроса.


#### Install Google chrome browser
```bash
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i google-chrome-stable_current_amd64.deb

rm -rf google-chrome-stable_current_amd64.deb 
```


