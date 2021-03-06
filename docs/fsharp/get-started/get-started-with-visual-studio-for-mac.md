---
title: 'Начало работы с F # в Visual Studio для Mac'
description: 'Сведения об использовании языка F # в Visual Studio для Mac.'
author: cartermp
ms.author: phcart
ms.date: 02/13/2017
ms.topic: article
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.openlocfilehash: f56d67a7ecb9c68703638cbe05d8531891c132cd
ms.sourcegitcommit: b750a8e3979749b214e7e10c82efb0a0524dfcb1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="get-started-with-f-in-visual-studio-for-mac"></a>Начало работы с F # в Visual Studio для Mac

F # и инструменты Visual F # поддерживаются в Visual Studio для Mac интегрированной среды разработки.  Для начала следует [скачать Visual Studio для Mac](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs), если это еще не сделано.  В этой статье используется сообщества Visual Studio 2017 г. для Mac, но можно использовать F # с версией по своему усмотрению.

## <a name="installing-f"></a>Установка F # #

После загрузки Visual Studio для Mac, он предложит выбрать, следует установить.  Для целей данной статьи мы оставите значения по умолчанию.  В отличие от Visual Studio для Windows необходимо специально установить поддержку языка F #.  Нажмите кнопку «Установить» для продолжения.

После завершения установки, нажмите кнопку «Запустить Visual Studio».  Его можно также запустить через Finder на macOS.

## <a name="creating-a-console-application"></a>Создание консольного приложения

Одним из основных проектов в Visual Studio для Mac является консольное приложение.  Вот как это делается.  После открытия Visual Studio для Mac:

1. На **файл** последовательно выберите пункты **новое решение**.

2.  В диалоговом окне нового проекта существует 2 различных шаблонов для консольного приложения.  Имеется один под другими -> .NET, который нацелен на .NET Framework.  Второй шаблон находится в .NET Core -> приложения, который нацелен на .NET Core.  Либо шаблон должен работать в данной статье.

3. В разделе консольное приложение C# в F # при необходимости измените.  Выберите **Далее** кнопку, чтобы переместить вперед!  

4. Присвойте проекту имя и выберите нужный вариант для приложения.  Обратите внимание на панели предварительного просмотра, чтобы части экрана, отображающий структуру каталогов, которая будет создана на основании выбранных параметров.  

5. Нажмите кнопку **Создать**.  Теперь вы увидите проекта F # в обозревателе решений.

## <a name="writing-your-code"></a>Создание кода

Давайте начнем путем написания кода сначала.  Убедитесь, что `Program.fs` файл открыт, а затем замените его содержимое следующим:

[!code-fsharp[HelloSquare](../../../samples/snippets/fsharp/getting-started/hello-square.fs)]

В приведенном выше примере, функция `square` был определен принимающий входных данных с именем `x` и умножает его самостоятельно.  Поскольку в языке F # используется [вывод типа](../language-reference/type-inference.md), тип `x` указывать не требуется.  Компилятор F # понимает типы, где умножение является допустимым и будет назначать тип для `x` зависимости от способа `square` вызывается.  Если навести на `square`, вы увидите следующее:

```
val square: x:int -> int
```

Это значение, называемое сигнатура типа функции.  Оно может быть прочитано следующим образом: «квадратная является функция, которая принимает целое число с именем x и создает целое число».  Обратите внимание, что компилятор присваивает `square` `int` тип сейчас - это, поскольку умножения, не является универсальным через *все* типов, а вместо этого универсального между закрытый набор типов.  Компилятор F # выбрать `int` это точка, но он позволяет корректировать сигнатура типа при вызове метода `square` в другой тип входных данных, таких как `float`.

Другой функции `main`, определения, отмеченный `EntryPoint` атрибут, чтобы информировать компилятор F #, выполнение программы должны начать прямо отсюда.  Следует, то же соглашение, что и другие [языки программирования C-стиле](https://en.wikipedia.org/wiki/Entry_point#C_and_C.2B.2B), где аргументы командной строки могут быть переданы в эту функцию и возвращают целочисленный код (обычно `0`).

В этой функции, которая вызывается метод `square` функцию с аргументом `12`.  Компилятор F #, затем назначает тип `square` быть `int -> int` (то есть функция, которая принимает `int` и создает `int`).  Вызов `printfn` является форматированный функцию печати, в которой используется строка формата, похожи на языки программирования C-стиле, параметры, которые соответствуют алгоритмам, заданным в строке формата, а затем выводит результат и новую строку.

## <a name="running-your-code"></a>Выполнение кода

Можно запустить код и просмотреть результаты, щелкнув **запуска** меню верхнего уровня и затем **Запуск без отладки**.  Это будет выполняться программа без отладки и позволяет вам быстро просматривать результаты.

Теперь вы увидите следующее напечатаны в окне консоли, всплывает Visual Studio для Mac:

```
12 squared is 144!
```

Поздравляем!  Создания первого проекта F # в Visual Studio для Mac, написаны функции F # распечатать результаты вызова этой функции и запустите проект и результатов.

## <a name="using-f-interactive"></a>С помощью F # Interactive

Одна из наиболее функций Visual F # для работы с проектами в Visual Studio для Mac — интерактивное окно F #.  Он позволяет отправить код по процессу, в которой можно вызвать этот код и просмотреть результат в интерактивном режиме.

Чтобы начать использовать его, выделите `square` функции, определенной в коде.  Нажмите кнопку **изменить** меню верхнего уровня.  Затем выберите **отправить выделение в F # Interactive**.  Это выполняет код в интерактивное окно F #.  Или щелкните выделение правой кнопкой мыши и выберите **отправить выделение в F # Interactive**.  Появится окно F # Interactive отображаются со следующими в ней:

```
>

val square : x:int -> int

>
```

В следующем примере показано сигнатуру функции для `square` функции, которую вы уже видели раньше при прохождении курсора над функции.  Поскольку `square` — теперь определен в F # Interactive процесса, его можно вызвать с разными значениями:

```
> square 12;;
val it : int = 144
>square 13;;
val it : int = 169
```

Это действие выполняет функцию, привязывающий результат к имени нового `it`и выводит тип и значение `it`.  Обратите внимание, вы должны завершить работу с каждой строки `;;`.  Это как F # Interactive знает после завершения вызова функции.  Можно также определять новые функции в F # Interactive:

```
> let isOdd x = x % 2 <> 0;;

val isOdd : x:int -> bool

> isOdd 12;;
val it : bool = false
```

Выше определения новую функцию `isOdd`, который принимает `int` и проверяет, является ли нечетное!  Эта функция для просмотра возвращается с разными вводными данными.  Можно вызывать функции в вызовах функций:

```
> isOdd (square 15);;
val it : bool = true
```

Можно также использовать [оператор прямого канала](../language-reference/symbol-and-operator-reference/index.md) конвейерная передача значения в двух функций:

```
> 15 |> square |> isOdd;;
val it : bool = true
```

Оператор прямого канала и многое другое, рассматриваются в следующих занятиях рассматривается.

Это представление только в том, что можно сделать с F # Interactive.  Для получения дополнительных сведений ознакомьтесь [интерактивного программирование на F #](../tutorials/fsharp-interactive/index.md).

## <a name="next-steps"></a>Следующие шаги

Если это еще не сделано, извлечь [обзор языка F #](../tour.md), который рассматриваются некоторые основные возможности языка F #.  Он приведен обзор некоторых возможностей F # и предоставить достаточно примеры кода можно скопировать в Visual Studio для Mac и запустить.  Существуют также некоторые полезные внешние ресурсы, которые можно использовать в демонстрации [руководство по F #](../index.md).

## <a name="see-also"></a>См. также
 [Visual F#](../index.md)  
 [Обзор языка F#](../tour.md)  
 [Справочник по языку F #](../language-reference/index.md)  
 [Вывод типа](../language-reference/type-inference.md)  
 [Справочник символов и операторов](../language-reference/symbol-and-operator-reference/index.md)  
