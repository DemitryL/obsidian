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

lazy config [link](https://github.com/folke/lazy.nvim)  - for install plugins on nvim

astronvim config [link](https://docs.astronvim.com/)

neo-tree config [link](https://github.com/nvim-neo-tree/neo-tree.nvim)  -  filesystem as sidebar

treesitter config [link](https://github.com/nvim-treesitter/nvim-treesitter)  - lighting sintacsys 

lsp config [link]()  - configuration add on laungch server 

THEME
onedark config [link](https://github.com/joshdick/onedark.vim) - 

autocomplits config - plugins 

mason [link](https://github.com/williamboman/mason.nvim) - 

null-ls [link](https://github.com/jose-elias-alvarez/null-ls.nvim)  -  