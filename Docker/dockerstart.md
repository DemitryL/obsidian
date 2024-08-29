# Install Docker for Manjaro

```bash
sudo pacman -S docker
```

## Обзор команд

```bash
// Запуск контейнера из образа
docker run "name"

// Список запущенных контейнеров
docker ps
// Весь список контейнеров
docker ps -a

// Остановка работующего контейнера
docker stop (id || names)

// Удаление контейнера остановленного или завершенного
docker rm (id || names)

// Список образов
docker images

// Удаление образов
docker rmi "name"
// ПЕРЕД УНИЧТОЖЕНИЕМ ОБРАЗА останови и удали все связанные с ним контейнеры

// Просто скачать образ без запуска
docker pull "name"

// Увидеть содержимое файла внутри контейнера
docker exec "names" cat /etc/hosts

// Attach & detach
// Вывод работы в консоле, остановка работы ctrl + c
docker run "путь к приложению"

// Работа приложения в фоновом режиме
docker run -d "путь к приложению"

// Прикрепить работу к консоле
docker attach (id || names)

```


```bash
// Запуск контейнера с оболочкой shell
docker run -it "name" sh
/# hostname  // id container
/# cat /etc/*rel*  // Релизная информация контейнера
/# exit 

// Удаление сразу всех образов и контейнеров
docker rm $(docker ps -aq)
```
