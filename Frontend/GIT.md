- [ ] 1. Необходимость гита
- [ ] 2. Настройка аккаунта гитхаб или гитлаб
- [ ] 3. Команды гита
- [ ] 4. Софт для управления гитом (gitkraken)

[[Git local]]
-----
[[Git server]]
-----

## Ubuntu: как обновить git до последней версии

Для того, чтобы получить последнюю версию git, необходимо добавить PPA (Personal Package Archive) из команды разработчиков Git Ubuntu в список источников программного обеспечения:

```git
$ sudo add-apt-repository ppa:git-core/ppa
```

Если получили ошибку:

```git
$ sudo: add-apt-repository: command not found
```

выполните следующее:

```git
$ sudo apt-get install software-properties-common
```

...и повторите ввод первой команды. Затем обновите список источников и обновите git:

```git
$ sudo apt-get update
...
$ sudo apt-get install git
```

Проверить версию гита после обновления:

```git
$ git --version
```

На этом всё. Успехов!
