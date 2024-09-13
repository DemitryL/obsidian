# МНОГОПОТОЧНОСТЬ(multithreading) in GO

//Немного общих слов

//Go из коробки - язык конкурентный , а не параллельный.

// 1. Что такое конкурентность?
// Конкурентность - это подвид многопоточного исоплнения программ, где различные задачи ("работники") конкурируют за ресурсы.
// Конкурентность навязывается различными факторами :
// _ приорететы исполнения
// _ простой ресурсов
// ручная передача

// 2. Пример конкурентности
// Екатерина бегает утром. Во время пробежки развязываются шнурки. Екатерина останавливается. Завязывает шнурки.
// Затем продолжает пробежку.
// Это классический пример конкурентности.

// 3. А параллелизм?
// Параллелизм - это подвид многопоточного исполнения программ, в котором множество задач ("работников") используют ресурсы ОДНОВРЕМЕННО.

// 4. Пример параллелизма
// Екатерина также бегает по утрам. Но в этот раз она еще и слушает музыку. В этот раз Екатерина ОДНОВРЕМЕННО и бегает и слушает музыку.

// 5. В чем разница и что лучше?
// Рассмотрим простой пример - браузер.
// Когжа мы заходим на какую-нибудь страницу : должно быть выполнено 2 действия
// _ загрузка html страницы (файла)
// _ отрисовка (рендеринг) в окне браузера

// Если данные задачи выполняются конкуретно, то сначала вы загрузите необходимый объем файлов , а уже затем выполните отрисовку.
// Процессор в этой ситуации будет осуществлять переключение контекста (context switch) в нужный момент (по завершении загрузки) и
// результат будет ожидаем.

// С другой стороны, если бы эти 2 задачи выполнялись параллельно, результат был бы немного шокирующим и непредсказуемым.

// 6. Как реализована конкуретность в языке?
// В Go поддержк конкуретности реализована с исползованием под-программ (со-программ) , т.н. "горутин" (или corutines/gorutines)

//7 . Горутина, это кто?
// Горутина - это фукнция или метод, которая запускает другие функции/методы или выполняет какие-то действия.
// Горутина , с технической точки зрения, может восприниматься как легковесный тред. На одном системном потоке может одновременно
// находиться огромное количество конкурирующих за ресурсы горутин.

// 8. Преимущества горутин над классическими тредами
// _ горутина легковесная (размер горутины в миллионы раз меньше, чем размер классического треда в С++/Java)
// _ исопльзование большого количество горутин занимает меньшее количество потоков ОС (в отличе от Java/C++, где отдельный тред
// требует выделения отдельного потока в ОС)
// горутины могут общатсья друг с другом используя каналы

## Пример go routine

//main.go

```go
package main

import "fmt"

//1. Данная функция будет запущена в качестве горутины.
// Важно: горутины никогда ничего не возвращают через явное использование return
func newGoRoutine() {
	fmt.Println("Hey, I'm new Gorutine!")
}

//2. функция main - на самом деле тоже горутина.
// Особенность в том - что если эта горутина завершается - все остальные
// запущенные убиваются сразу!
func main() {
	go newGoRoutine() // в этот момент происходит формирование запроса на вызов функции в отдельной горутины.
	// соответственно код основной горутины main продолжает сразу же выполняться и не ждет завершения newGoRoutine()
	fmt.Println("Main goroutine work!")
	//Запустим код и....
}
```

## Fix-сим выполнение go routine

//main.go

```go
package main

import (
	"fmt"
	"time"
)

func newGoRoutine() {
	fmt.Println("Hey, I'm new Gorutine!")
}

func main() {
	go newGoRoutine()
	time.Sleep(1 * time.Second) // немного тормозим выполнение main горутины, таким образом даем время для того,
	// чтобы newGoRoutine успела выполниться
	fmt.Println("Main goroutine work!")
}
```

## Запускаем несколько го рутин

//main.go

```go
package main

import (
	"fmt"
	"time"
)

//1. Запустим несколько горутин и посмотрим, как они бьются за ресурсы

//2. Определим первую горутину
func printEvenNumbers() {
	for i := 1000; i < 1020; i += 2 {
		time.Sleep(250 * time.Millisecond)
		fmt.Printf("%d ", i)
	}
}

//3. Определим вторую горутину
func printOddNumbers() {
	for i := 1; i < 20; i += 2 {
		time.Sleep(450 * time.Millisecond)
		fmt.Printf("%d ", i)
	}
}

// 4. Определим main горутину
func main() {
	go printEvenNumbers()               // сразу идем дальше, запуск функции будет происходит в отдельной горутине
	go printOddNumbers()                // также идем дальше, запуск функции будет происходит потом
	time.Sleep(7000 * time.Millisecond) // тормозим основную горутину, чтобы остальные успели что-то сделать
	fmt.Println("main goroutine died")
}

//5. Таким образом горутины работают следующим образом : (нарисуем прямоугольник с палочками!)
```

## Каналы

//main.go

```go
package main

import "fmt"

//1. Каналы - средство для коммуникации между горутинами.
// Каналы можно рассматривать как соединетильные трубы, через которые горутины между собой общаются (аналогично тому,
// как вода течет по трубам, данные передаются через каналы)

//2. Объявление канала.
// Каналы по умолчанию имеют zeroValue - nil. Поэтому их создают через фукнцию make.

func main() {
	var a chan int // объявляем канал, через который будут передаваться данные типа int
	if a == nil {
		fmt.Println("channel is nil, Let's define it")
		a = make(chan int)
		fmt.Printf("Type of a is %T\n", a)
	}
}
```

//main.go

```go
package main

import "fmt"

//1. Для отправки данных в канал a (chan int) используем синтаксис
//a <- dataInt

//2. Для получения данных из канала используем синактсис
// dataInt := <- a

//3. Отправка и получения данных из канала - блокирующая операция!
// Это означает, что если данные отправлены в канал, то выполнение текущей программы останавливается до тех пор, пока с другой
// стороны из этого канала кто-то не считает данные.

// Аналогично и в обратную сторону. Если кто-то читает из канала, то выполнение текущей программы (горутины) останавливается до тех пор,
// пока кто-то в этот канал не отправит данные.

//4. Пример использования каналов.
func newGoRoutine(done chan bool) {
	fmt.Println("Hey, I'm new Gorutine!")
	done <- true
}

func main() {
	done := make(chan bool)
	go newGoRoutine(done)
	<-done // в этой точке выполнение main горутины останавливается до тех пор, пока в канал кто-нибудь не запишет данные!
	fmt.Println("Main goroutine work!")
}
```

## Процесс блокирования

//main.go

```go
package main

import (
	"fmt"
	"time"
)

//1. Немного перепишем последнюю программу, чтобы лучше увидеть как устроен процесс блокирования

func newGoRoutine(done chan bool) {
	fmt.Println("Hey, I'm newGoRoutine and I'm going sleep!")
	time.Sleep(4 * time.Second)
	fmt.Println("newGoRoutine awake and going to send data to channel")
	done <- true
}

func main() {
	done := make(chan bool)
	fmt.Println("I'm main goroutine and I wanna call newGoRoutine")
	go newGoRoutine(done)
	<-done
	fmt.Println("Ok, Main goroutine recieved data and gonna die!")
}
```

## Задача

//main.go

```go
package main

import "fmt"

//1. Создадим чуть более полезную программу, которая будет делать следующие действия:
// берем число, например 456
// (4^2 + 5^2 + 6^2) + (4^3 + 5^3 + 6^3)
// Подсчитаем сумму квадартов цифр и сумму кубов, а затем сложим полученные результаты
//Делать будем следующим образом:
// * main gorutine получает число и вызывает 2 другие горутины, по итогу, получив от них результаты,
// она просто их сложит и выведет на консоль
// ** squaresGoRoutine - будет запущена main и подсчитает сумму квадратов всех цифр, результат положит в канал
// ** cubesGoRoutine - будет запущена main и подсчиатет сумму кубов всех цифр , результат полужит в канал

func squaresGoRoutine(num int, squareChan chan int) {
	sum := 0
	for num != 0 {
		digit := num % 10
		sum += digit * digit
		num /= 10
	}
	squareChan <- sum
}

func cubesGoRoutine(num int, cubeChan chan int) {
	sum := 0
	for num != 0 {
		digit := num % 10
		sum += digit * digit * digit
		num /= 10
	}
	cubeChan <- sum
}

func main() {
	number := 6735271
	squareChan := make(chan int)
	cubeChan := make(chan int)
	go squaresGoRoutine(number, squareChan)
	go cubesGoRoutine(number, cubeChan)
	squaresSum, cubesSum := <-squareChan, <-cubeChan
	fmt.Println("Total result is:", squaresSum+cubesSum)
}
```

## DEADLOCK

//main.go

```go
package main

//1. Deadlock - ситуация, когда кто-то пишет в канал НО ИЗ НЕГО НИКОГДА НИКТО НИЧЕГО НЕ ПРОЧИТАЕТ,
// или когда кто-то читает из канала
// НО В НЕГО НИКТО НИКОГДА НЕ ЗАПИШЕТ!

// По сути ситуация означает, что для отправляющей стороны отсутствует
// получатель (с другой стороны никто не ждет данных). И наоборот.

func main() {
	ch := make(chan int)
	ch <- 10
	// <-ch
}
```

## Однонаправленные каналы

//main.go

```go
package main

//1. Каналы могут иметь направление.
// То что инициализировалось до этого момента инициализировало
// ДВУНАПРАВЛЕННЫЙ КАНАЛ (в него можно и писать и из него можно читать)
// Можно создать канал только на отправку:
// sendChan := make(chan<- int)

// Можно создать канал только на чтение
// readChan := make(<-chan int)

func sender(sendChan chan<- int) {
	sendChan <- 10 // Тут все ок
}

func main() {
	sendChan := make(chan<- int)
	go sender(sendChan)
	<-sendChan // тут не ок, т.к. канал только на отправку данных, но не чтение.
}

//2. Использование однонаправленных каналов никак не сказывается на производительности,
// а служит лишь для логического разделения кода
```

## Закрытие каналов

//main.go

```go
package main

import "fmt"

//1. Закрытие каналов и итерирование
// Со стороны получателя можно использоваться синтаксис
// val, ok := <- ch
//где val - значение помещенное в канал отправителем
// ok - true/false в зависимости от того, открыт канал или уже закрыт отправителем.
// если канал закрыт то в val будет помещено zeroValue для типа канала

func generator(ch chan int) {
	for i := 0; i < 25; i++ {
		ch <- i
	}
	close(ch)
}

func main() {
	ch := make(chan int)
	go generator(ch)
	for {
		val, ok := <-ch
		if !ok {
			break
		}
		fmt.Println("Recieved from channel", val)
	}

	// Конструкцию можно упростить и использовать
	// for val := range ch {
	// 	fmt.Println("Recieved from channel:", val)
	// }
}
```

## Задача

//main.go

```go
package main

import "fmt"

//1. Попробуем решить старую задачу с подсчетом суммы квадратов и кубов полученного числа с использованием закрытия каналов

func digits(number int, dchnl chan int) {
	for number != 0 {
		digit := number % 10
		dchnl <- digit
		number /= 10
	}
	close(dchnl)
}
func calcSquares(number int, squareop chan int) {
	sum := 0
	dch := make(chan int)
	go digits(number, dch) // своя горутина для генерации цифр
	for digit := range dch {
		sum += digit * digit
	}
	squareop <- sum
	close(squareop)
}

func calcCubes(number int, cubeop chan int) {
	sum := 0
	dch := make(chan int)
	go digits(number, dch) // еще одна горутина для генерации цифр
	for digit := range dch {
		sum += digit * digit * digit
	}
	cubeop <- sum
	close(cubeop)
}

func main() {
	number := 589
	sqrch := make(chan int)
	cubech := make(chan int)
	go calcSquares(number, sqrch)
	go calcCubes(number, cubech)
	squares, cubes := <-sqrch, <-cubech
	fmt.Println("Final output", squares+cubes)
}
```

## Буферезированный канал

// main.go

```go
package main

import "fmt"

//1. Буферезированный канал - канал с буфером, в который можно напихать со стороны отправителя не 1 пак данных, а столько, сколько
// позволяет в буфер.

// ch := make(chan int, capacityIntValue)

func main() {
	ch := make(chan string, 5) // Создадим канал вместимостью 2
	ch <- "Bob"                // Не блокиуремся , т.к. можно запихнуть в буфер еще 4 элемента
	ch <- "Alex"               // Не блокируемся, т.к. можно еще запихнуть в буфер 3 элемента
	fmt.Println(<-ch)
	fmt.Println(<-ch)
}
```

## Как блокируется буферезированный канал

```go
package main

import (
	"fmt"
	"time"
)

//1. Как блокируется буферезированный канал?
func write(ch chan int) {
	for i := 0; i < 5; i++ {
		ch <- i
		fmt.Println("successfully wrote", i, "to ch")
	}
	close(ch)
}

//2. Как только буфер заполняется - канал блокируется до тех пор, пока не будет освобождено место (буфер может быть освобожден не до конца!)

func main() {
	ch := make(chan int, 2)
	go write(ch)
	time.Sleep(2 * time.Second)
	for v := range ch {
		fmt.Println("read value", v, "from ch")
		time.Sleep(2 * time.Second)

	}

}

// 3. Длина и вместимость канала.
// Длина канала len(ch) - сколько сейчас элементов в канале
// Вместимость cap(ch) - какой размер буфера у канала
```

## 2-ой способ аркестрирования го рутин

```go
package main

import (
	"fmt"
	"sync"
	"time"
)

//1. Еще один инструмент для оркестрирования горутинами - это WaitGroup
// По сути WaitGroup - это счетчик горутин.
// Когда горутина запускается делается WaitGroup++
// Когда горутина завершается делается WaitGroup--
//Таким образом когда WaitGroup == 0 делаем вывод, что все горутины отработали!

//Пример

func process(i int, wg *sync.WaitGroup) {
	fmt.Println("started Goroutine ", i)
	time.Sleep(2 * time.Second)
	fmt.Printf("Goroutine %d ended\n", i)
	wg.Done() //WaitGroup--
}

func main() {
	no := 5
	var wg sync.WaitGroup
	for i := 0; i < no; i++ {
		wg.Add(1) // WaitGroup++
		go process(i, &wg)
	}
	wg.Wait() // if WaitGroup == 0 ? До тех пор, пока это условие не выполнено - мы заблокированы в данной строке для main горутины
	fmt.Println("All go routines finished executing")
}
```

## SELECT

//main.go

```go
package main

import (
	"fmt"
	"time"
)

//1. Select - это инструмент, позволяющий выбирать из множества канальных операций (чтение/запись) для множества каналов.
// Если из 10 каналов что-то пришло в один - select выбирает его
// Если из 10 каналов что-то пришло сразу в два и более - select выбирает случайный

func server1(ch chan string) {
	time.Sleep(6 * time.Second)
	ch <- "from server1"
}
func server2(ch chan string) {
	time.Sleep(3 * time.Second)
	ch <- "from server2"

}
func main() {
	output1 := make(chan string)
	output2 := make(chan string)
	go server1(output1)
	go server2(output2)
	select {
	case s1 := <-output1:
		fmt.Println(s1)
	case s2 := <-output2: // выбирается этот кейс, т.к. в этот канал будут помещены данные быстрее
		fmt.Println(s2)
	}
}
```

## SELECT - альтернативные действия пока канал еще не готов

```go
package main

import (
	"fmt"
	"time"
)

//1. На практике select чаще всего используется для того, чтобы предпринимать какие-то действия,
// пока в каналы еще не пришли данные

//Пример
func process(ch chan string) {
	time.Sleep(10500 * time.Millisecond)
	ch <- "process successful"
}

func main() {
	ch := make(chan string)
	go process(ch)
	for {
		time.Sleep(1000 * time.Millisecond)
		select {
		case v := <-ch:
			fmt.Println("received value: ", v)
			return
		default:
			fmt.Println("no value received")
		}
	}

}
```

## Select как инструмент защиты от deadlock

```go
package main

//1. Select как инструмент защиты от deadlock
// Добавление default страхует от появление deadlock в ходе выполнения и берет работу на себя (попробуйте убрать default и все умрет)

import "fmt"

func main() {
	var ch chan string
	select {
	case v := <-ch:
		fmt.Println("received value", v)
	default:
		fmt.Println("default case executed")

	}
}
```

## SELECT - Опрос каналов.

```go
package main

//1. Опрос каналов. Как было сказано ранее - в случае если готовы более чем один канал - выбирается случайный.
import (
	"fmt"
	"time"
)

func server1(ch chan string) {
	ch <- "from server1"
}
func server2(ch chan string) {
	ch <- "from server2"

}
func main() {
	output1 := make(chan string)
	output2 := make(chan string)
	go server1(output1)
	go server2(output2)
	time.Sleep(1 * time.Second)
	select {
	case s1 := <-output1:
		fmt.Println(s1)
	case s2 := <-output2:
		fmt.Println(s2)
	}
}
```

## Мьютексы - средства защиты от "Resource Sharing"

```go
package main

//1. Мьютексы - средства защиты от "Resource Sharing"
// Что это такое?
// Во время работы конкурентных программ, главной точкой является тот факт, что множества горутин
// не должны одновременно использовать какой-то общий экземпляр (файл, переменную, бд) для одновременных модификаций.

// 2. Пример RS
// Допустим у нас код
//     x = x + 1
// Пока работает 1 горутина - проблем никаких нет и иннкремент стандартный
// Теперь представим что горутин 2
// ПОСКЛЬКУ ДЛЯ ОБЕИХ ГОРУТИН ДАННЫЙ РЕСУРС БУДЕТ ИСПОЛЬЗОВАТЬСЯ КОНКУРЕТНО, ОЖИДАТЬ ЧТО ПО ИТОГУ РАБОТУ ОБЕИХ ГОРУТИН
// (При начальном X=0) X будет равен 2 - НЕЛЬЗЯ.
//*  Первая и вторая горутина могут начать работать с парметром x =0 (вторая не дождется , пока первая увеличит X на единицу)
// * В итоге будет X = 1
//* Первая горутина начнает работать, увеличивает x на единицу , но не успевает присвоить его
//* Первая горутина начинает работать, завершается, потом стартуер вторая (этот вариант оптимистичный, но сработает с вероятность 1/3!)

// Для того, чтобы избежать этой пробелмы использую мьютексы (мьютекс блокирует ресурс до тех пор , пока его не осводит одна из горутин)
// В таком случае код с инкрементом выглядел бы как :
// mutex.Lock()
// x = x + 1
// mutex.Unlock()

import (
	"fmt"
	"sync"
)

// 2. Пример. Возникновение RS часто именую как Race Condition (состояние гонки)

var x = 0

func increment(wg *sync.WaitGroup) {
	x = x + 1
	wg.Done()
}
func main() {
	var w sync.WaitGroup
	for i := 0; i < 1000; i++ {
		w.Add(1)
		go increment(&w)
	}
	w.Wait()
	fmt.Println("final value of x", x)
}
```

## mutex - Разрешим состояние гоник при помощи введение пары мьютексов!

```go
package main

// Разрешим состояние гоник при помощи введение пары мьютексов!
import (
	"fmt"
	"sync"
)

var x = 0

func increment(wg *sync.WaitGroup, m *sync.Mutex) {
	m.Lock()
	x = x + 1
	m.Unlock()
	wg.Done()
}
func main() {
	var w sync.WaitGroup
	var m sync.Mutex
	for i := 0; i < 1000; i++ {
		w.Add(1)
		go increment(&w, &m)
	}
	w.Wait()
	fmt.Println("final value of x", x)
}
```

## Решение данной проблемы через канал

```go
package main

//Также состояние гонки может быть разрешено через использование каналов (т.к. каналы это более детальный инстурмент
// коммуницирования)
import (
	"fmt"
	"sync"
)

var x = 0

func increment(wg *sync.WaitGroup, ch chan bool) {
	ch <- true
	x = x + 1
	<-ch
	wg.Done()
}
func main() {
	var w sync.WaitGroup
	ch := make(chan bool, 1)
	for i := 0; i < 1000; i++ {
		w.Add(1)
		go increment(&w, ch)
	}
	w.Wait()
	fmt.Println("final value of x", x)
}
```
