```
package main

import (
    "fmt"
    "log"
    "net/http"
)

//w - ResponseWrite (куда писать ответ)
//r - Request (откуда брать запрос)
// Обработчик
func GetGreet(w http.ResponseWrite, r *http.Request) {
    fmt.Fprintf(w, "<h1>Hi! I'm new web-server!</h1>")
}

// Товарищ, который выбирает нужный обработчик в зависимости от адреса, по которому пришел запрос
func RequestHandler() {
    http.HandleFunc("/", GetGreet) //Если придет запрос по адресу "/" то вызывай GetGreet
    log.Fatal(http.ListenAndServe(":8080", nil)) // Запускаем вебсервер в режиме "слушанья"
}

func main() {
    RequestHandler()
}
```
