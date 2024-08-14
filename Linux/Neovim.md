#### Комбинации nvim

```bash
## Перемещение по файлу
- k - up, - j - down, - h - left, - l - right;

- w - на слово вправо;
- b - на слово влево;
- W - до пробела вправо;
- B - до пробела влево;

- ^ - в начало текущей строки; 
- $ - в конец текущей строки;

- } - абзац вниз;
- { - абзац вверх;

- gg - перейти в начало файла;
- G - перейти в конец файла;

- <Ctrl-y> - на строку вниз -
- <Ctrl-e> - на строку верх - 
- без изменения положения курсора;

## Выделение
- v - выделить;
- shift + v - выделить целую строку;

## Ввод текста
- i — перейти в режим ввода с текущей позиции;
- a — перейти в режим ввода после курсора;

- I — переместиться в начало строки -
- А — переместиться в конец строки -
- и перейти в режим ввода;

## Удаление и вставка
- dd — удалить текущую строку (вырезать);
- D - удаление символов с текущего положения курсора до конца строки;
- yy (также Y) — копирование текущей строки в буфер;
- p — вставка содержимого буфера под курсором.
- P — вставка содержимого буфера перед курсором;

## Отмена изменений
- u — отмена последней команды;
- U — отмена всех последних изменений в строке, если строка не удалена;

## Поиск
/фраза - поиск фразы во всем документе.
n - следующее найденное (вниз) N - предыдущее (вверх).

## Выход
- :q! - выйти без сохранения;
- :wq - записать файл и выйти;
- ZZ - записать файл и выйти;

```

Custom keyboards
```bash
## Ввод текста
- jk — выход из режима ввода с текущей позиции;

## Search
- <leader>nh - очистить основные моменты поиска

## increment/decrement
- <leader>+ - увелечение числа
- <leader>- - уменьшение числа

## window management
## split
- | - открытие окна вертикально
- \\ - открытие окна горизонтально
- <leader>se - сделать окна одинаковыми размерами
- <leader>sx - закрыть текущее окно
- <leader>sm - увеличивает текущее окно

## new tab open/close
- <leader>to - открыть новый таб
- <leader>tx - закрыть таб
- <Tab> - перейти на следующий таб
- <s-Tab> - перейти на предыдущий таб

## explorer is folder | new-tree.lua
- <leader>ee - открыть проводник папок
- <leader>ef - открыть текущий проводник 
- <leader>ec - свернуть проводник файлов
- <leader>er - обновить проводник файлов

## telescope.lua
- <leader>ff - нечеткий поиск файлов в cmd
- <leader>fr - нечеткий поиск последних файлов
- <leader>fs - найти строку в cmd
- <leader>fc - найдите строку под курсором в cmd

## save file | auto-session.lua
- <leader>wr - восстановить сеанс для cmd
- <leader>ws - сохранить сеанс для корневой директории автосессии

## TODO comments | todo-comments.lua
--TODO
--HACK
--BUG
- ]t - search on comment Next todo comment
- [t - previous todo comment

## substitute.lua
- s - замените движением
- ss - заменяющая строка
- S - заменить на конечную строку
- x - s - заменой является визуальный режим

##

```

Install neovim: 
```bash
## Ubuntu
sudo apt install neovim

## Manjaro
sudo pacman -S neovim, ripgrep, node
```
Install font [Link](https://www.nerdfonts.com/font-downloads) JetBrainsMono

## Setup Initial File Structure
Your config will be located in ~/.config/nvim.

>lua
  >josean
	>core
	  init.lua
	  keymaps.lua
	  options.lua
	>plugins
	  >lsp
	    lspconfig.lua
	    mason.lua
	  alpha.lua
	  auto-session.lua
	  autopairs.lua
	  bufferline.lua
	  colorscheme.lua
	  comment.lua
	  dressing.lua
	  formatting.lua
	  gitsingns.lua
	  init.lua
	  lazygit.lua
	  linting.lua
	  lualine.lua
	  nvim-cmp.lua
	  nvim-tree.lua
	  substitute.lua
	  surround.lua
	  telescope.lua
	  todo-comments.lua
	  treesitter.lua
	  vim-maximizer.lua
	  which-key.lua
	lazy.lua
.stylua.toml
init.lua
lazy-lock.json


## Setup lazy.nvim
lazy.nvim is a modern plugin manager for Neovim.

- Install plenary & vim-tmux-navigator
В сочетании с набором привязок клавиш tmux плагин позволит вам плавно перемещаться между разделениями vim и tmux, используя согласованный набор горячих клавиш.

- Install & configure tokyonight colorscheme
tokyonight.nvim — это темная и светлая тема, которая поддерживает новейшие функции Neovim и улучшает цвета терминала.

- Setup nvim-tree file explorer
Nvimtree — это плагин Neovim для просмотра файловой системы и других древовидных структур в любом стиле, который вам подходит, включая боковые панели, плавающие окна, разделенный стиль, значки файлов или все сразу!

- Setup which-key
WhichKey — это Lua-плагин для Neovim, который отображает всплывающее окно с возможными сочетаниями клавиш для команды, которую вы начали вводить.

- Setup telescope fuzzy finder
Telescope.nvim — это расширяемый инструмент нечеткого поиска по спискам. Построен на новейших потрясающих функциях ядра neovim. Телескоп основан на модульности, что позволяет легко настраивать его.

- Setup a greeter
Мы собираемся настроить приветствие для стартапа Neovim с помощью Alpha-Nvim.

- Setup automated session manager auto-session.lua
Автоматическое управление сеансами отлично подходит для автоматического сохранения сеансов перед выходом из Neovim и возвращения к работе после возвращения.

- Setup bufferline for better looking tabs
Этот плагин бессовестно пытается имитировать эстетику текстовых редакторов с графическим интерфейсом/Doom Emacs.

- Setup lualine for a better statusline 
Невероятно быстрая и простая в настройке строка состояния Neovim, написанная на Lua.

- Setup dressing.nvim 
С выпуском Neovim 0.6 мы получили возможность расширить ядро ​​пользовательского интерфейса (vim.ui.select и vim.ui.input). Они существуют для того, чтобы позволить авторам плагинов переопределять их, улучшая поведение по умолчанию, и это именно то, что мы собираемся сделать.

- Setup vim-maximizer 
Разворачивает и восстанавливает текущее окно в Vim.

- Setup treesitter 
Treesitter — это потрясающая функция Neovim, которая обеспечивает улучшенную подсветку синтаксиса, отступы, автоматическую пометку, пошаговый выбор и многие другие интересные функции.

- Setup autocompletion nvim-cmp.lua
Плагин механизма завершения для neovim, написанный на Lua. Источники завершения устанавливаются из внешних репозиториев и "sourced".

- Setup auto closing pairs autopairs.lua
Этот плагин поможет нам автоматически закрывать окружающие символы, такие как круглые скобки, фигурные скобки, кавычки, одинарные кавычки и теги.

- Setup commenting plugin comment.lua
Добавляет или оборачивает выделленный блок в коментарий
'gc' ---Line-comment keymap
'gb' ---Block-comment keymap

- Setup todo comments todo-comments.lua
"]t" - "Next todo comment" 
"[t" - "Previous todo comment"

- Setup substitution plugin substitute.lua
Цель replace.nvim — предоставить новые движения оператора, чтобы упростить выполнение быстрых замен и обменов.
"ss" = "Substitute line" (Заменить строку)
"S" = "Substitute to end of line" (Заменить в конец строки)

- Setup nvim-surround surround.lua
Добавить/удалить/изменить окружающие пары
Вызовы функций и теги HTML «из коробки»

- Setup mason.nvim  mason.lua
Mason.nvim используется для установки и управления всеми языковыми серверами, которые вам нужны для языков, над которыми вы работаете.

- Setup nvim-lspconfig lspconfig.lua 
Nvim-lspconfig используется для настройки языковых серверов.

- Setup formatting formatting.lua
Мы собираемся использовать Conform.nvim для настройки форматирования в Neovim. 
"<leader>mp"

- Setup linting linting.lua 
Мы собираемся использовать nvim-lint для настройки линтинга в Neovim.
"<leader>l"

# Setup git functionality
- Setup gitsigns plugin gitsigns.lua
Gitsigns — отличный плагин для взаимодействия с git-ханками в Neovim.
']c' - gitsigns.nav_hunk('next')
'[c' - gitsigns.nav_hunk('prev')

- Setup lazygit integration lazygit.lua


