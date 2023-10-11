---

---
`Kotlin tutorial for Toasty by ASCIIMoth`
# Ссылки
- [Онлайн песочница для выполнения кода в браузере](https://play.kotlinlang.org)
- [Официальный тур по языку](https://kotlinlang.org/docs/kotlin-tour-welcome.html)
- [И еще один официальный материал но уже точно для людей имеющих какой-то опыт](https://kotlinlang.org/docs/basic-syntax.html)
- [И еще один](https://play.kotlinlang.org/byExample/01_introduction/01_Hello%20world)
- [Geeks4Geeks](https://www.geeksforgeeks.org/kotlin-programming-language/)котлина
- [w3schools](https://www.w3schools.com/kotlin/index.php) (самое понятное и целостное на фоне остальных)

# Предисловие

В целом все источники объясняют все +- одинаково: базовые вещи описываются подробно, а где-то начиная с `ООП` начинаются такие объяснения, для понимания которых уже нужно знать что такое `ООП` как таковое.
По этому тут будут вперемешку ссылки на разные источники и мои пояснения, так чтобы из этого сложилась понятная картина.

И да, многие вещи упоминаются в одном месте, а объясняются сильно ниже. Без этого никак. Если ты не понял что-то но ниже про это есть глава, не надо задерживаться на вопросе сейчас.

Внизу статьи есть [[#Словарь]] в который ты можешь записывать новые для себя термины по ходу дела
## Исполнение кода
Я обычно за то чтобы для начала устанавливать базовый [[README#^1|тулчейн]] и дергать его руками без помощи `IDE` и прочих слоев абстракции и уже поняв как все устроенно внутри переходить к продвинутым средствам разработки. Но у котлина (как и многих вещей связанных с миром java) тулчейн довольно монструозный, так что до тех пор пока это не будет явно указанно в соответствующей главе, используй [браузерную песочницу](https://play.kotlinlang.org).

Содержимое этой статьи разбито на блоки. В каждом блоке есть одна или несколько ссылок на внешние источники и (опционально) мои пояснения.
Также в большинстве блоков есть строка ==Заменить своей заметкой== вместо который ты должен записать своими словами изученный материал.
К некоторым блокам приложены задания. Это предварительно написанный код, который надо дописать в соответствии с задачей так чтобы он заработал. Рядом с зданиями есть чекбокс. Отмечай его, когда решаешь задания, чтобы я знал что проверять.
И свои заметки и решения задач ты должен дописывать прямо сюда в текст статьи и коммитить на гитхаб.

# Язык
Kotlin это язык созданный в 2016 году конторой JetBrains, которая де юре иностранная, но де факто изначально Питерская. Назван в честь острова [Котлин](https://ru.wikipedia.org/wiki/%D0%9A%D0%BE%D1%82%D0%BB%D0%B8%D0%BD) там же под Питером.

Kotlin изначально работает на основе JVM(виртуальной машины java) из за чего у него с жавой очень хороший интероп. Библиотеки на java можно использовать в проектах на kotlin и наоборот. Из-за этого с момента своего появления kotlin сразу имеет обширную экосистему из java мира в котором есть библиотеки для вобще всего. Также по скольку JVM работает вобще на всем чем можно, kotlin тоже получает это свойство. В какой то момент google даже принял kotlin в качестве официального языка для разработки под андроид.
Однако к текущему моменту котлин обзавелся помимо JVM поддержкой кучи других платформ, от транспиляции в JavaScript до компиляции в нативные бинарники. Прямо сейчас прикручивают копиляцию в wasm. Ну и в принципе язык старается стать универсальным.

Также как у Dart с Flutter'ом, у котлина есть свой крупный фреймворк для интерфейсов вокруг которого много чего крутится в экосистеме - Compose.

# Синтаксис
Kotlin относится к семейству `C like` языков т.е. заимствует синтаксис у C.

Код состоит из выражений. Выражением является любая синтаксическая конструкция которая может быть выполнена:
```kotlin
// Это вражение
1 + 2
// Это тоже выражение
print("A")
// Присвоение это тоже выражение
a = 1

// Выражения могут вкладываться друг в друга
// В таком случае они будут исполняться в порядке от наиболее вложенного к наименее

// Здесь сначала выполниться 1+2 что даст 3
// а затем выполнится print(3), что напечатает "3" в консоль
print(1+2)

// Здесь сначала выполнится 2+3 что даст 5
// а затем a = 5, что присвоит переменной a знаение 5
a = 2 + 3
```
В конце выражений используется `;`, но опционально. Если на одной строчке находится только одно выражение, точка с запятой не нужна. Если же несколько выражений записаны в одну строчку, их надо разделять `;`:
```kotlin
println("A")
println("B")
```
``` kotlin
println("A"); println("B")
```
Несколько выражений выполняющихся друг за другом могут быть сгруппированы в `блок кода` с помощью фигурных скобок:
```kotlin
{
	print("A")
	print("B");print("C")
}
```
Блоки кода используются в функциях, циклах, условиях и вообще много где.
Принято внутри каждого блока кода добавлять дополнительный отступ:
```kotlin
{
	{
		{
			print("A")
		}
	}
}
```
Это делает код более читаемым, позволяя легко определять границы блоков на глаз.

Однако ничего не мешает написать весь блок в одну строчку, особенно если в нем только одно выражение
```kotlin
{print("A")}
```

# Ключевые слова
Ключевые слова, это слова которые сами по себе что-то значат в языке. Их нельзя использовать для чего либо кроме их предназначения, нельзя создавать переменные или функции с такими именами и тд. Функционал и правила применения ключевых слов это данность и они в общем то и составляют сам язык.
Список ключевых слов котлина
```kotlin
as break class continue do else false for fun if in is null object package return super this throw true try typealias typeof val var when while
```

#  Комментарии
- https://www.w3schools.com/kotlin/kotlin_comments.php
Комментарии это способ исключить часть текста из программы. Текст в комментариях игнорируется компилятором и не влияет на работу программы.
Комментарии можно (и нужно) использовать для объяснения того как работает код. Хоть сколько-то крупные объемы кода без комментариев сложно воспринимать даже написавшему их человеку через время, не говоря уже о других людях. Как известно `Код чаще читается чем пишется`, по этому писать комментарии важно всегда, даже если кажется что код очевиден.
Также комментарии можно использовать чтобы "выключить" кусок кода, оставив его при этом в файле.
Комментарий можно объявить двумя способами
С двух слешей начинается однострочный комментарий и продолжается до конца строки
```kotlin
// Это комментари
print("A") // И это тоже
```
Со слеша и астериска(звездочки `*`) и заканчивается ими же но в обратном порядке
```kotlin
/* Такой комментарий тоже может быть однострочным */
/* Или
состоять
из
какаого
угодно
колличества
строк
*/
```


# Точка входа
Точка входа (entry point) это место с которого начинается выполнение кода. В kotlin (как и во многих других языках) это функция main ( подробнее о функциях далее).
Выглядит это так
``` kotlin
fun main() {
	/* Когда программа запустится
	содержимое этого блока кода будет выполнено*/
}
```

# Печать
В kotlin есть встроенная функция `println` для печати текста в стандартный поток вывода `stdout`.
```kotlin
println("A")
println("B")
```
Она печатает текст, но ее также можно использовать для того чтобы печатать текстовое представление других типов данных, например чисел:
```kotlin
println(2+3)
```
Функция `println` автоматически переносит курсор на новую строку после каждой печати:
```kotlin
/* Будет напечатано:
A
B
C
*/
fun main() {
	println("A")
	println("B")
	println("C")
}
```
Также есть похожая функция `print` которая не переносит курсор:
```kotlin
/* Будет напечатано:
ABC
*/
fun main() {
	print("A")
	print("B")
	print("C")
}
```

- [x] Задание 1
```kotlin
fun main() {
	/* Напиши код который печатает в одну строчку: */
	// A2B
	/* При этом не используя в коде цифру 2 */
	print("A")
    print(1+1)
    print("B")
	
}
```

# Переменные
- https://www.w3schools.com/kotlin/kotlin_variables.php
- https://www.geeksforgeeks.org/kotlin-variables/
==Заменить своей заметкой==
- [x] Задание 2
Чем неизменяемые переменные отличаются от констант?
==В языке Котлин не существует констант, но всё ещё есть неизменяемые переменные обозначающиеся ключевым словом val, которым можно присвоить значение только один раз==
- [x] Задание 3
Что такое область видимости (scope)?
==Область видимости - это пространство в пределах которго существуют переменные работы с ними. Область видимости может быть вложенной в другую, в таком случае она наследует все переменные из родительской. Новый блок кода создаёт новую область видимости. Также существует глобальная область видимости, находящаяся вне блоков кода.==
- [x] Задание 4
```kotlin
fun main() {
	var x = 1
	run {
		//Исправь эту строчку так чтобы при запуске программы печаталась двойка:
		//var x = 2 
		x = 2
	}
	print(x)
}
```

# Словарь
- `Тулчейн` - дословно `tool chain` - набор, как правило связанных, инструментов для работы с чем либо. Например тулчейн языка, тулчейн для разработки под андроид итд ^1
- JVM - виртуальная машина Java 
- Интероп - 
- Транспиляция - 
