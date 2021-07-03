

[TOC]



---













📽️ - посмотри воркшоу

⚗️ - проведи эксперимент

🔬 - изучи внимательно

📖 - прочитай документация

🪙 - подумай о сложности

🐞 - запомни ошибку

🔨 - запомни решение

🏔️ - обойди камень предкновенья

⏰ - сделай перерыв

🏡 - попробуй дома

💡 - обсуди светлые идеи

🙋 - задай вопрос

⚡ - запомни панику













---





















## Встроенные типы

























---



- Целочисленные

  ```go
  int  int8  int16  int32  int64
  uint uint8 uint16 uint32 uint64 uintptr
  // The int, uint, and uintptr types are usually 32 bits wide on 32-bit systems 
  // and 64 bits wide on 64-bit systems. When you need an integer value you should
  // use int unless you have a specific reason to use a sized or unsigned integer type.
  byte // alias for uint8
  
  bool
  ```

- Вещественные

  ```go
  float32 float64
  complex64 complex128
  ```

- Cтроковые

  ```go
  string
  rune // alias for int32
       // represents a Unicode code point
  ```

- Указатели

  ```go
  *int
  nil
  ```

----

### Литералы

| литерал        | тип                  |
| -------------- | -------------------- |
| `0`            | **int**              |
| `0.64`         | **float64**          |
| `0.867 + 0.5i` | **complex128**       |
| `-3`           | **int**              |
| `true`         | **bool** (**true**)  |
| `false`        | **bool** (**false**) |
| `'a'`          | **rune**             |
| `"text"`       | **string**           |
| **``**         | **string**           |
| `nil`          | **nil**              |



```go
func main() {
  fmt.Printf("%v %t\n", 4, 4)
  fmt.Printf("%v %t\n", -3, -3)
  fmt.Printf("%v %t\n", 9.5, 9.5)
  fmt.Printf("%v %t\n", 0.867 + 0.5i, 0.867 + 0.5i)
  fmt.Printf("%v %t\n", true, true)
  fmt.Printf("%v %t\n", false, false)
  fmt.Printf("%v %t\n", "", "")
  fmt.Printf("%v %t\n", 'a', 'a')
  fmt.Printf("%v %t\n", nil, nil)
}
```

---























## Переменные























---

### Объявление

- локальной переменной

```go
func main() {
  var answer int // zero-value: 0
}
```

- группы локальных переменных

```go
func main() {
	var (
    found  bool  // zero-value: false
    answer *uint // zero-value: nil
	)
}
```

- глобальные переменные

```go
package main

var found bool
```

- группы локальных переменных

```go
package main

var (
	found bool
	answer int // bad approach ? 💡
)
```



---

### Инициализация

- Объявление и инициализация

```go
func main() {
  var answer = uint(0)    // int type
}
```

- Короткая запись 

```go
func main() {
  answer := 0    // int type
}
```

- Множественное объявление с инициализацией

```go
func main () {
  var (
    found  = false   
    answer = 0
  )
}
```

- Распаковка при множественной инициализации

```go
func main() {
    var i, j int = 0, 0
}
```

```go
func main() {
  answer := nil // скомпилируется ? 🙋
}
```

---



```go
func main() {
	var found bool
 	found := true // compilation error 🐞
}

```

```go
func main() {
 	found = true // compilation error 🐞
}
```

```go
func main() {
  answer := false
  answer := 42 // compilation error 🐞
}
```

```go
func main() {
  answer := &int64(0) // compilation error 🐞
}
```

```go
func main() {
  answer := new(int64) 🔨
}
```

```go
func main() {
	a, b := 20, 30
  fmt.Printf("a=%d and b=%d", a, b)
	b, c := 40, 50
  fmt.Printf("b=%d and c=%d", a, b) // 🙋
}
```

---

### Приведениe

- Явное приведение типов

```go
func main() {
  answer := uint(42)
}
```

- Сужение типов

```go
func main() {
  answer := int8(128)  // compilation error 🐞
}
```

- Расширение типов

```go
[1] uint8 -> uint16 -> uint32 -> uint64
[2] int8 -> int16 -> int32 -> int64

[3] uint8 -> int16
[4] uint16 -> int32
[5] uint32 -> int64

[6] float32 -> float64

[7] complex64 -> complex128
```

```go
[8] int -> bool // 🙋
[9] bool -> int // 🙋
```

- [ ] Попробуй различные схемы сужения и расширения 🏡

---





















## Алгебра



























---

### Арифметические операторы





| Оператор | Наименование        | Типы                                      |
| :------- | ------------------- | ----------------------------------------- |
| `+`      | sum                 | integers, floats, complex values, strings |
| `-`      | difference          | integers, floats, complex values          |
| `*`      | product             | -//-                                      |
| `/`      | quotient            | -//-                                      |
| `%`      | remainder           | integers                                  |
| `&`      | bitwise AND         | -//-                                      |
| `|`      | bitwise OR          | -//-                                      |
| `^`      | bitwise XOR         | -//-                                      |
| `&^`     | bit clear (AND NOT) | -//-                                      |
| `<<`     | left shift          | integer << unsigned integer               |
| `>>`     | right shift         | integer >> unsigned integer               |



> Неявного преобразования типов нет, поэтому используй явное





---

### Операторы сравнения



| Оператор | Наименование     | Типы                      |
| -------- | ---------------- | ------------------------- |
| **==**   | equal            | comparable                |
| **!=**   | not equal        | -//-                      |
| **<**    | less             | integers, floats, strings |
| **<=**   | less or equal    | -//-                      |
| **>**    | greater          | -//-                      |
| **>=**   | greater or equal | -//-                      |



- Boolean, integer, floats, complex values and strings are comparable.
- Strings are ordered lexically byte-wise.
- Two pointers are equal if they point to the same variable or if both are nil.
- Two channel values are equal if they were created by the same call to make or if both are nil.
- Two interface values are equal if they have identical dynamic types and equal concrete values or if both are nil.
- A value `x` of non-interface type `X` and a value t of interface type `T` are equal if `t`’s dynamic type is identical to `X` and `t`’s concrete value is equal to `x`.
- Two struct values are equal if their corresponding non-blank fields are equal.
- Two array values are equal if their corresponding elements are equal.



---

### Логические операторы

| Оператор | Наименование    | Пример                          |
| -------- | --------------- | ------------------------------- |
| `&&`     | conditional AND | `answer ∈ (20;30)` 🏡            |
| `||`     | conditional OR  | `answer ∈ (-∞; 20) ∪ (30;+∞)` 🏡 |
| `!`      | NOT             | `not found`                     |

### Операторы при работе с указателями

| Оператор | Наименование        | Пример    |
| -------- | ------------------- | --------- |
| `&`      | address of          | `&answer` |
| `*`      | pointer indirection | `*result` |

```go
func main() {
  
  answer := 42
  fmt.Printf("address of answer: %v", &answer)
}
```

```go
func main() {
  
  answer := new(int)
  fmt.Printf("value of answer: %v", *answer)
}
```

> Тернарные операторы отсутствуют

- [ ] Посмотреть адреса для различных переменных и констант 🏡

---





















## Константы



























---

### Иницилизация

- Локальные

```go
func main() {
	const (
		helloMessage = "hello world"
		exitMessage  = "exit"
	)
}
```

- Глобальные

```go
package main

const (
	MessageOk   = "ok"
  MessageFail = "fail"
)
```

- Пример одиночного определения с ошибкой

```go
package main

import "fmt"

const Pi = 3.14

func main() {
	Pi = 7          // compilation error 🐞
	fmt.Println(Pi)
}
```

- [ ]  Указатель на константный объект и константный указатель на объект 💡

---





















## Ветвления



























---

### Условный оператор `if`

- простой пример c `if`

```go
if <condition> {
}
```

- пример c `else`

```go
if <condition> {
} else {
}
```

- пример с `elseif`

```go
if <condition> {
} else if <condition> {
} else {
}
```

```go
if answer == 0 { // answer == 0 🙋
}

if ptr == nil { // ptr == nil 🙋
}
```

```go
if <assignment-statement>; <condition> {
}
```

- [ ] Попробуй `!`, `&&`, `||`, `()` 🏡

---

### Условный опeратор `switch`

- вариант с default

```go
switch level {
  case 0:
    return "DEBUG"
	case 1:
    return "INFO"
  default:
    return "unsupported" // bad approach 🐞
}
```

- вариант со списком случаев

```go
switch httpCode {
  //...
case http.TooManyRequest,
  http.GatewayTimeout: 
  return grpc.UNAVAILABLE
default:
  return grpc.UNKNOWN
}
```

- вариант с приваиванием

```go
switch hour := time.Now().Hour(); {
case hour < 12:
    fmt.Println("Good morning!")
case hour < 17:
    fmt.Println("Good afternoon!")
default:
    fmt.Println("Good evening!")
}
```

- [ ] Попробуй ключевое слово `fallthrough` и `break` 🏡

---



















## Циклы



























---

### Опeратор `for`

- бесконечный цикл

```go
for {
  
}
```

- использование ключевого слова `break`

```go
for {
  // ...
  if condition {
    break
  }
  // ...
}
```

- цикл с предусловием

```go
for i := 0; i < 10; i++ {
  fmt.Println(i)
}
```

- цикл с условием

>Цикл с постусловием отсутствует, можно использовать с предусловием

```go
for ok := true; ok; ok = condition {
	//...
}
```

- [ ] Попробуй вложенные циклы и функциональные объекты 🏡

---



















## Функции



























---

### Аргументы

- без аргументов

```go
func main() {
  //...
}
```

- одиночноe

```go
func Round(x float64) float64
  // ... you can try it at home 🏡
}
```

- множественное

```go
func MaxOf(a uint, b uint) uint {
  //... you can try it at home 🏡
}
// vs func MaxOf(a, b uint) uint 🙋
```

- переменное

```go
func MaxOf(items ...int) int {
  //... you can try it at home 🏡
}

MaxOf(1)
MaxOf(1, 2)
```

> Часто импользуете значения по умолчанию для параметров функции ? 🙋 

---

### Возвращаемые значения

- без возвращаемого значения

```go
func init() {
  // ...
}

a := init()
```

- множественное число

```go
func MinMax(a, b uint) (uint, uint) {
  // ...
}
```

- именнованые аргументы

```go
func MinMax(a, b uint) (min uint, max uint) {
  // ...
}
```

> Максимальное количество возвращаемых значений 💡

- указатель на локальную переменную

```go
func findValue(key string) *int {
  var result int
  // ...
  return &result
}
```

> Как часто используете перегрузку функций ? 🙋

---

### Функторы

- Функторы

```go
func main () {  
	maxOf := func(one, two, three int) {
    //... you can try it at home 🏡
  }
  answer := maxOf(1, 2, 3)
  fmt.Println(answer)
}
```

- Анонимные функции

```go
func main() {
	fmt.Printf(
		"100 (°F) = %.2f (°C)\n",
		func(f float64) float64 {
			return (f - 32.0) * (5.0 / 9.0)
		}(100),
	)

```

- Алисы

```go
type HandlerFunc = func(ResponseWriter, *Request)

func Logging(fn HandlerFunc) HandlerFunc {
  return func(resp ResponseWriter, req *Request) {
    log.Debug(req)
    fn(resp, req)
    log.Debug(resp)
  }
}
```

---

























## Перечисления

























---

### Примеры

- c использованием ключевого слова `iota`

```go
const (
  DebugLevel uint8 = iota // 0
  InfoLevel               // 1
  WarnLevel               // 2
  ErrorLevel              // 3
)
```

- с алиасом

```go
type Level uint8

const (
  DebugLevel Level = 0
  InfoLevel  Level = 1
  WarnLevel  Level = 2
  ErrorLevel Level = 3
)
```

- с алиасом и `iota`

```go
type Level uint8

const (
  DebugLevel Level = iota // 0
  InfoLevel               // 1
  WarnLevel               // 2
  ErrorLevel              // 3
  // ...
)
```

- [ ]  Пример наименования для вариации замены пространства имен `LevelDebug` 💡

---



















## ⏰



























---























## Контейнеры

























---

























## Cтатический массив **Array**

























---

### Инициализация

- явное указание размера

```go
var decisions [4]uint
//fmt.Printf("len: %d\n", len(decisions)) // 4
//fmt.Printf("cap: %d\n", cap(decisions)) // 4
```

- нулевой размер

```go
var decisions [0]uint
//fmt.Printf("len: %d\n", len(decisions)) // 0
//fmt.Printf("cap: %d\n", cap(decisions)) // 0
```

- выводимое значение размера

```go
var levels = [...]string {"fatal","error","info","debug"}
```

- выход за пределы границ

```go
var decisions [4]uint     // [0][1][2][3]
fmt.Println(decisions[4]) // invalid array index 4 🐞
```

### Итерирование

```go
for index, value := range decisions {
}
```

```go
for _, value := range decisions {
}
```

- [ ] Чтение, изменение, копирование и расширение 🏡

---















## **Slice**

```sh
array := [5]rune{'a', 'b', 'c', 'd', 'e'}
array[i:j]
// 
// [ptr: 0xc00010c000, len: 5 , cap: 7]
//   ┃
//   ┗━━━━━━━━━━━━━━> ['a']['b']['c']['d']['e'][   ][   ]
//                      0    1    2    3    4    5    6
```



















---



```go
symbols := [...]rune{'a', 'b', 'c', 'd', 'e'}

half := symbols[0:len(symbols)/2] // first half
fmt.Println(half)

half = symbols[len(symbols)/2:]  // second half
fmt.Println(half)
```

### Инициализация

- пустой

```go
var sourceArray []uint // nil
fmt.Println(len(sourceArray))
fmt.Println(cap(sourceArray))
sourceArray = append(sourceArray, uint(1))
var copyArray []uint // nil
copyArray = append(copyArray, sourceArray...)
```

- из array

```go
symbols := [...]rune{'a', 'b', 'c', 'd', 'e'}

half := symbols[0:len(symbols)/2]
fmt.Println(half)
```

```go
array := []rune{'a', 'b', 'c', 'd', 'e'}
fmt.Println(len(array)) 
fmt.Println(cap(array)) 🙋
```

- с определенными размерами

```go
array := make([]int, 0, 10) // len and capacity
items := make([]int, 10)    // only len, capacity = len
```

---

### Чтение

```go
array := make([]int, 0, 10)
items := make([]int, 10)

fmt.Println(array[0]) // ⚡ index out of range [0] with length 0
fmt.Println(items[0]) 
```

### Запись

```go
items := make([]int, 10)
for i := 0; i < len(items); i++ {
  items[i] = i+1
}

items := make([]int, 0, 10)
for i := 0; i < len(items); i++ {
  items = append(items, i+1)
}
```

### Добавление

- в пустой **slice**
- одного элемента
- множества элементов

### Итерирование

```go
symbols := []rune{'a', 'b', 'c', 'd', 'e'}
for index, symbol := range symbols {
  fmt.Println(string(symbol))
}
```

> Случай с **capacity** и случай с **len**



---





















## **Map**

























---



### Инициализация

```go
var idToName map[uint]string  // nil
```

```go
fmt.Println(idToName[0]) // if missed returns zero value
```

```go
idToName[1] = "Vera" // ⚡ panic: assignment to entry in nil map
```

```go
idToName := map[uint]string{}
```

```go
idToName[1] = "Vera"
```

```go
idToName := map[uint]string {
  0: "Sveta",
  1: "Vera",
  2: "Nika",
}

idToName[3] = "Veronika"
```

```go
if _, found := idToName[0]; !found {
  // ...
}
```

> ok **vs** found 🙋

---

### Итерирование

```go
//  key value
for id, name := range idToName {
  fmt.Printf("user with id <%d> has name <%s>", id, name)
}
```

```go
//     value
for _, name := range idToName {
  fmt.Println(name)
}
```

```go
//  key
for id := range idToName {
  fmt.Println(id)
}
```


Копирование

```go
idToName := map[uint]string {
  0: "Sveta",
  1: "Vera",
  2: "Nika",
}

collection := idToName
collection[3] = "Veronika"
fmt.Println(idToName) // 🙋
```

```go
for k, v := range b {
    a[k] = v
}
```

> slices, maps, and functions; these types cannot be compared using `==`

---

























- [ ] Какие контейнеры бывают в C++ ? 🙋

























---











## **ZeroValue**







| Типы        | Значения |
| ----------- | -------- |
| `string`    | ""       |
| `map`       | nil      |
| `slice`     | nil      |
| `bool`      | false    |
| **Pointer** | nil      |
| **Numeric** | 0        |













---

## 



















## Pointer

























---

Указатели

```go
package main

import (
  "fmt"
  "unsafe"
)

func main() {
  var result *uint     // zero-value
  answer := new(int64) // new or make
  
  fmt.Printf("size: %d", unsafe.Sizeof(result))
  
  if answer != nil {
    fmt.Printf("answer: %d", *answer)
  }

  fmt.Printf("answer: %d", *result) // ⚡
  
  answer := new(int64) // new or make
  *answer = 42

  foo := 0
  result = &foo
}
```



Инициализация: **var**, **new**, **make**

Размер: 32, 64

Разыменование и получение адреса

Специальный тип: **uintptr**



---





## Container







---

### List

```go
type Element
    func (e *Element) Next() *Element
    func (e *Element) Prev() *Element

type List
    func New() *List
    func (l *List) Back() *Element
    func (l *List) Front() *Element
    func (l *List) Init() *List
    func (l *List) InsertAfter(v interface{}, mark *Element) *Element
    func (l *List) InsertBefore(v interface{}, mark *Element) *Element
    func (l *List) Len() int
    func (l *List) MoveAfter(e, mark *Element)
    func (l *List) MoveBefore(e, mark *Element)
    func (l *List) MoveToBack(e *Element)
    func (l *List) MoveToFront(e *Element)
    func (l *List) PushBack(v interface{}) *Element
    func (l *List) PushBackList(other *List)
    func (l *List) PushFront(v interface{}) *Element
    func (l *List) PushFrontList(other *List)
    func (l *List) Remove(e *Element) interface{}
```



---

### Heap

```go
func Fix(h Interface, i int)
func Init(h Interface)
func Pop(h Interface) interface{}
func Push(h Interface, x interface{})
func Remove(h Interface, i int) interface{}
type Interface
```





---

### Ring



```go
type Ring
    func New(n int) *Ring
    func (r *Ring) Do(f func(interface{}))
    func (r *Ring) Len() int
    func (r *Ring) Link(s *Ring) *Ring
    func (r *Ring) Move(n int) *Ring
    func (r *Ring) Next() *Ring
    func (r *Ring) Prev() *Ring
    func (r *Ring) Unlink(n int) *Ring
```





---

### Stack

```go











```

- Queue
- ForwardList
- Deque



[collections package](https://github.com/golang-collections/collections)

