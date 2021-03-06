---
title: 'Асинхронное программирование на F #'
description: 'Узнайте, как асинхронное программирование на F # выполняется через модель уровня языка программирования, просты в использовании и естественный язык.'
keywords: .NET, .NET Core
author: cartermp
ms.author: phcart
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: f9196bfc-b8a8-4d33-8b53-0dcbd58a69d8
ms.openlocfilehash: c3fde46e804b7acac78d3ce5454a3c6f806e24e7
ms.sourcegitcommit: 655fd4f78741967f80c409cef98347fdcf77857d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/28/2018
---
# <a name="async-programming-in-f"></a>Асинхронное программирование на F # #

> [!NOTE]
> В этой статье были обнаружены некоторые неточности.  Он перезаписывается.  В разделе [проблема #666](https://github.com/dotnet/docs/issues/666) Дополнительные сведения об изменениях.

Асинхронное программирование на F # можно сделать с помощью модели программирования уровня языка в использовании и естественный язык.

Асинхронное программирование на F # лежит `Async<'T>`, представление работы, которая запускается в фоновом режиме, где `'T` — либо тип, возвращаемый через специальные `return` ключевое слово или `unit` если асинхронный рабочий процесс не имеет результат, возвращаемый.

Ключевым принципом, чтобы понять, является тип выражение async `Async<'T>`, который является просто _спецификации_ выполняться в контексте асинхронной работы. Не выполняется, пока не запустить ее явно с помощью одного из начала функции (такие как `Async.RunSynchronously`). Несмотря на то, что это другим способом обдумывания выполняет работу, он получилась довольно просто на практике.

Например предположим, что требуется загрузить dotnetfoundation.org HTML-код, не блокируя основной поток. Вы можете добиться следующим образом.

```fsharp
open System
open System.Net

let fetchHtmlAsync url = 
    async {
        let uri = Uri(url)
        use webClient = new WebClient()

        // Execution of fetchHtmlAsync won't continue until the result
        // of AsyncDownloadString is bound.
        let! html = webClient.AsyncDownloadString(uri)
        return html
    }

let html = "https://dotnetfoundation.org" |> fetchHtmlAsync |> Async.RunSynchronously
printfn "%s" html
```

Вот и все! Помимо использования `async`, `let!`, и `return`, это просто обычный код F #.

Существует несколько синтаксических конструкций, которые стоит обратить внимание:

*   `let!` Привязывает результат выражения async (выполняемый для другого контекста).
*   `use!` работает аналогично `let!`, но удаляет его связанных ресурсов, когда он покидает область действия.
*   `do!` будет ожидать асинхронный рабочий процесс, который не возвращает ничего.
*   `return` просто возвращает результат вычисления выражения async.
*   `return!` выполняет другой асинхронный рабочий процесс и возвращает его возвращаемое значение в результате.

Кроме того обычные `let`, `use`, и `do` ключевые слова могут использоваться вместе с асинхронные версии так же, как в обычной функции.

## <a name="how-to-start-async-code-in-f"></a>Запуск асинхронного кода в F # #

Как упоминалось ранее, асинхронного кода представляет собой спецификацию для работы в другом контексте, который должен быть явным образом запущено. Ниже приведены два основных способа для решения этой задачи:

1.  `Async.RunSynchronously` запускается это асинхронный рабочий процесс в другом потоке и ожидает его результат.

```fsharp
open System
open System.Net

let fetchHtmlAsync url = 
    async {
        let uri = Uri(url)
        use webClient = new WebClient()
        let! html = webClient.AsyncDownloadString(uri)
        return html
    }

 // Execution will pause until fetchHtmlAsync finishes
 let html = "https://dotnetfoundation.org" |> fetchHtmlAsync |> Async.RunSynchronously

 // you actually have the result from fetchHtmlAsync now!
 printfn "%s" html
 ```

2.  `Async.Start` запустить рабочий процесс async в другом потоке и будет **не** ожидает его результат.

```fsharp
open System
open System.Net
  
let uploadDataAsync url data = 
    async {
        let uri = Uri(url)
        use webClient = new WebClient()
        webClient.UploadStringAsync(uri, data)
    }

let workflow = uploadDataAsync "https://url-to-upload-to.com" "hello, world!"

// Execution will continue after calling this!
Async.Start(workflow)

printfn "%s" "uploadDataAsync is running in the background..."
 ```

Существуют другие способы запуска асинхронного рабочего процесса, доступного для более конкретных сценариев. Дополнительные сведения [в справочнике по Async](https://msdn.microsoft.com/library/ee370232.aspx).

### <a name="a-note-on-threads"></a>Примечание в потоках

Выше фразу «в другом потоке», но важно знать, что **это не означает, что асинхронные рабочие процессы являются оболочкой для многопоточности**. Рабочий процесс фактически» происходит переключение» между потоками, займов их для небольшой объем времени для выполнения требуемых задач. Когда это асинхронный рабочий процесс фактически «ожидание» (например, для сетевой вызов, чтобы он возвращал нечто ожидания), любой поток, который он займов во время освобождается до нормальной работе перейдите на что-нибудь другое. Это позволяет асинхронные рабочие процессы для использования системы, они так же эффективно, как можно запускать и делает их особенно строгую для сценариев большого объема операций ввода-вывода.

## <a name="how-to-add-parallelism-to-async-code"></a>Добавление параллелизма асинхронного кода

Иногда можно требуется для выполнения нескольких асинхронных заданий в параллельном режиме, собирать их результаты и интерпретировать их иным образом. `Async.Parallel` позволяет сделать это без необходимости использования библиотеки параллельных задач, которой будет применяться для присвоения `Task<'T>` и `Async<'T>` типов.

Следующий пример будет использовать `Async.Parallel` для загрузки HTML из четырех популярных сайтов в параллельном режиме, дождитесь завершения выполнения этих задач, а затем напечатать HTML, который был загружен.

```fsharp
open System
open System.Net

let urlList = 
    [ "https://www.microsoft.com"
      "https://www.google.com"
      "https://www.amazon.com"
      "https://www.facebook.com" ]

let fetchHtmlAsync url = 
    async {
        let uri = Uri(url)
        use webClient = new WebClient()
        let! html = webClient.AsyncDownloadString(uri)
        return html
    }

let getHtmlList urls =
    urls
    |> Seq.map fetchHtmlAsync   // Build an Async<'T> for each site
    |> Async.Parallel           // Returns an Async<'T []>
    |> Async.RunSynchronously   // Wait for the result of the parallel work

let htmlList = getHtmlList urlList

// We now have the downloaded HTML for each site!
for html in htmlList do
    printfn "%s" html
```

## <a name="important-info-and-advice"></a>Важные сведения и советы

*   Добавьте «Async» в конец любой функции, которые вы будете использовать

 Несмотря на то, что это просто соглашение об именовании, он облегчить как возможность обнаружения API. Особенно в том случае, если существует синхронные и асинхронные версии ту же подпрограмму, рекомендуется явно указать, который является асинхронным, через имя.

*   Прослушивание компилятор!

 Очень строгие компилятор F #, сделав его практически невозможно сделать что-нибудь troubling как код «async» синхронное выполнение. Если попадаться предупреждение, это знак, что код не будет выполняться, как вы считаете, что будет происходить. Если компилятор может сделать довольными, код будет выполнен скорее должным образом.

## <a name="for-the-cvb-programmer-looking-into-f"></a>Для программистов C# и Visual Basic, разобраться в F # #

В этом разделе предполагается, вы уже знакомы с моделью асинхронного в C# или Visual Basic. Если вы не, [асинхронного программирования в C#](../../../csharp/async.md) является отправной точкой.

Нет принципиальное отличие модель языка C# и Visual Basic async модели асинхронного F #.

При вызове функции, которая возвращает `Task` или `Task<'T>`, уже началось выполнение этого задания. Дескриптор, возвращенный представляет асинхронную задание уже выполняется. Напротив, при вызове функцию с модификатором async в языке F # `Async<'a>` возвращается представляет задание, которое будет иметь **создан** в определенный момент. Основные сведения об этой модели обладает широкими возможностями, так как она допускает асинхронных заданий в языке F # для связывать друг с другом, выполнять условно и работы с большей степенью гранулярности элемента управления.

Существует несколько других сходства и различия отметить.

### <a name="similarities"></a>Сходства

*   `let!`, `use!`, и `do!` аналогичны `await` при вызове асинхронного задания изнутри `async{ }` блока.

 Три ключевых слова можно использовать только в пределах `async { }` блока, подобно тому, как `await` может быть вызван только внутри `async` метод. Иными словами `let!` Если необходимо для сбора и использования результата, то для `use!` является прежним, но для других операций, ресурсы которого следует получить удаляются после его использования, и `do!` удобно для, если нужно подождать, пока это асинхронный рабочий процесс без возвращаемого значения для завершения Прежде чем продолжить.

*   F # поддерживает параллелизм данных аналогичным образом.

 Несмотря на то, что он работает очень по-разному, `Async.Parallel` соответствует `Task.WhenAll` сценарий Желательное результатов набора асинхронных заданий, если все они завершаются.

### <a name="differences"></a>Различия

*   Вложенные `let!` не разрешено, в отличие от вложенных `await`

 В отличие от `await`, которой могут быть вложенными неопределенно долгое время, `let!` невозможно, необходимо его результат привязаны перед его использованием внутри другой `let!`, `do!`, или `use!`.

*   Поддержка отмены проще в языке F # чем в C# или Visual Basic.

 Поддержка отмены середине выполнения задачи в C# и Visual Basic требуется выполнить проверку `IsCancellationRequested` свойства или метода `ThrowIfCancellationRequested()` на `CancellationToken` объект, который передается в асинхронный метод.

Напротив F # асинхронные рабочие процессы — это более естественным образом поддерживать отмену. Отмена выполняется простой трехшаговый процесс.

1.  Создайте объект `CancellationTokenSource`.
2.  Передайте его в начала функции.
3.  Вызов `Cancel` на маркер.

Пример

```fsharp
open System
open System.Net

let uploadDataAsync url data = 
    async {
        let uri = Uri(url)
        use webClient = new WebClient()
        webClient.UploadStringAsync(uri, data)
    }

let workflow = uploadDataAsync "https://url-to-upload-to.com" "hello, world!"

let token = new CancellationTokenSource()
Async.Start (workflow, token)

// Immediately cancel uploadDataAsync after it's been started.
token.Cancel()
```

Вот и все!

## <a name="further-resources"></a>Дополнительные ресурсы:

*   [Асинхронные рабочие процессы в MSDN](https://msdn.microsoft.com/library/dd233250.aspx)
*   [Асинхронные последовательностей для F #](https://fsprojects.github.io/FSharp.Control.AsyncSeq/library/AsyncSeq.html)
*   [Служебные программы F # данных HTTP](https://fsharp.github.io/FSharp.Data/library/Http.html)
