[Link](https://nvchad.com/)
Настроим с нуля NvChad IDE - сборку Neovim для работы с JavaScript и TypeScript. Настроим LSP, Lint, Prettier, тесты и отладку.

Перед установкой бекапим старую конфигурацию 
```shell
mv ~/.config/nvim ~/.config/nvim-bk
```
Далее удаляем share 
```shell
rm -rf ~/.local/share/nvim
```
 Проверяем что nvim пустой
```shell
 nvim
```


Next copy command :
```shell
git clone https://github.com/NvChad/NvChad ~/.config/nvim --depth 1 && nvim

yes
```

Назначение клавиш
<leader> - пробел
<leader> + e - открывает дерево
<leader> + w - сохранение 
\\ - разделение окна
Ctrl + ] - развернуть терминал вертикально
Ctrl + \\ - развернуть терминал горизонтально

Для неотеста 
<leader> + tt - запускает неотест
<leader> + tf - запускает файл
<leader> + to - output test
<leader> + ts - summary test

Для отладки 
<leader> + du - dedug ui
<leader> + db - добавляет брекпоинт 
<leader> + ds - start 
<leader> + dn - step over

с - копирование 
p - вставка
d -delete
r - rename
y - copy

:q - exit
Ctrl + x - позволяет перемещатся между терминалами

<leader> + ff - search in file
<leader> + fv - search in direction
<leader> + fa - показывает все файлы включая скрытые

перемещение между буферами tab or shift + tab
<leader> + x - закрыть файл
<leader> + ra - переименовать символ

<leader> + fm - автомотически форматируется по приттеру
