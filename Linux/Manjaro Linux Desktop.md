Установка и полная настройка 

Pacman - это пакетный менеджер, система которая позваляет устанавливать программы.
```shell
sudo pacman -S // установка программы
sudo pacman -Syu // обновление программ и всей системы.
sudo pacman -R // удаление программы
sudo pacman -Ss // поиск пакета
```

Установка пакетов
```shell
sudo pacman -S neovim 
sudo pacman -S tmux 
sudo pacman -S gcc
sudo pacman -S htop zip unzip
sudo pacman -S chromium
pamac build google-chrome
sudo pacman -S git pass
sudo pacman -S alacritty
sudo pacman -S nodejs
sudo pacman -S npm
sudo pacman -S code
```

Установка питона отдельно для работы pip
Download python3 **[Link](https://www.python.org/downloads/)**
```shell
//перенос в домашнюю дирикторию
mv Download/Python-3.12.0.tar.xz .
// распаковка
tar -xvf Python-3.12.0.tar.xz
// переходим в папку
cd Python-3.12.0

./configure --prefix=/home/sterx/.python3.12 --enable-optimizations

// j8 это по количеству ядер
make -j8

sudo make altinstall

cd 

./.python3.12/bin/python3.12

./.python3.12/bin/pip3.12

nvim ~/.zshrc

```

В файл .zshrc добавляем следующую строку:
```
export PATH=/home/sterx/.python3.12/bin:$PATH
```

Проверяем:
```
python3.12

python3.12 -m pip
```

Установка oh my zsh  [Link](https://ohmyz.sh/):
```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Обои для рабочего стола [Link](https://www.goodfon.ru/ai-art/)

