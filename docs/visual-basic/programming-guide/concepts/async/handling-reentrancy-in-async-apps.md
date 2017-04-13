---
title: "Обработка повторного входа в асинхронных приложениях (Visual Basic) | Документы Microsoft"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: ef3dc73d-13fb-4c5f-a686-6b84148bbffe
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 64a708e3b88f48ad30d3f3ad25141a31f3d8f73d
ms.lasthandoff: 03/13/2017

---
# <a name="handling-reentrancy-in-async-apps-visual-basic"></a>Обработка повторного входа в асинхронных приложениях (Visual Basic)
При включении асинхронного кода в приложение следует учесть и по возможности избежать повторного входа, под которым подразумевается повторный ввод асинхронной операции до ее завершения. Если не определить и не обработать возможности повторного входа, это может привести к непредвиденным результатам.  
  
 **Содержание раздела**  
  
-   [Распознавание поддержки повторного входа](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645)  
  
-   [Обработка повторного входа](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645)  
  
    -   [Отключение кнопки запуска](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645)  
  
    -   [Отмена и перезапуск операции](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645)  
  
    -   [Запуск нескольких операций и выходные данные в очередь](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645)  
  
-   [Проверка и выполнение примера приложения](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645)  
  
> [!NOTE]
>  Чтобы выполнить этот пример, необходимо иметь Visual Studio 2012 или более поздней версии и платформы .NET Framework 4.5 или более новая версия вашего компьютера.  
  
##  <a name="BKMK_RecognizingReentrancy"></a>Распознавание поддержки повторного входа  
 В примере в этом разделе выбрать пользователей **запустить** для запуска асинхронного приложение, которое загружает ряд веб-сайтов и вычисляет общее число байтов, которые были загружены. Синхронная версия примера реагирует одинаково, независимо от того, сколько раз пользователь нажмет кнопку, поскольку после первого раза поток пользовательского интерфейса игнорирует эти события до завершения выполнения приложения. При этом в асинхронном приложении поток пользовательского интерфейса продолжает реагировать, и можно ввести асинхронную операцию повторно до ее завершения.  
  
 В следующем примере показано ожидаемое вывода, если пользователь выбирает **запустить** кнопку только один раз. На экран выводится список загруженных веб-сайтов, размер которых указан в байтах. Общее число байтов отображается в конце списка.  
  
```  
1. msdn.microsoft.com/library/hh191443.aspx                83732  
2. msdn.microsoft.com/library/aa578028.aspx               205273  
3. msdn.microsoft.com/library/jj155761.aspx                29019  
4. msdn.microsoft.com/library/hh290140.aspx               117152  
5. msdn.microsoft.com/library/hh524395.aspx                68959  
6. msdn.microsoft.com/library/ms404677.aspx               197325  
7. msdn.microsoft.com                                            42972  
8. msdn.microsoft.com/library/ff730837.aspx               146159  
  
TOTAL bytes returned:  890591  
```  
  
 Однако если пользователь нажимает кнопку больше одного раза, обработчик событий вызывается несколько раз и процесс загрузки будет каждый раз выполняться повторно. В результате одновременно запускается несколько асинхронных операций, получаемые выходные данные чередуются и счетчик общего числа байтов выдает неоднозначные результаты.  
  
```  
1. msdn.microsoft.com/library/hh191443.aspx                83732  
2. msdn.microsoft.com/library/aa578028.aspx               205273  
3. msdn.microsoft.com/library/jj155761.aspx                29019  
4. msdn.microsoft.com/library/hh290140.aspx               117152  
5. msdn.microsoft.com/library/hh524395.aspx                68959  
1. msdn.microsoft.com/library/hh191443.aspx                83732  
2. msdn.microsoft.com/library/aa578028.aspx               205273  
6. msdn.microsoft.com/library/ms404677.aspx               197325  
3. msdn.microsoft.com/en-us/library/jj155761.aspx                29019  
7. msdn.microsoft.com                                            42972  
4. msdn.microsoft.com/library/hh290140.aspx               117152  
8. msdn.microsoft.com/library/ff730837.aspx               146159  
  
TOTAL bytes returned:  890591  
  
5. msdn.microsoft.com/library/hh524395.aspx                68959  
1. msdn.microsoft.com/library/hh191443.aspx                83732  
2. msdn.microsoft.com/library/aa578028.aspx               205273  
6. msdn.microsoft.com/library/ms404677.aspx               197325  
3. msdn.microsoft.com/library/jj155761.aspx                29019  
4. msdn.microsoft.com/library/hh290140.aspx               117152  
7. msdn.microsoft.com                                            42972  
5. msdn.microsoft.com/library/hh524395.aspx                68959  
8. msdn.microsoft.com/library/ff730837.aspx               146159  
  
TOTAL bytes returned:  890591  
  
6. msdn.microsoft.com/library/ms404677.aspx               197325  
7. msdn.microsoft.com                                            42972  
8. msdn.microsoft.com/library/ff730837.aspx               146159  
  
TOTAL bytes returned:  890591  
```  
  
 Чтобы просмотреть код, создающий эти выходные данные, перейдите к концу раздела. Можно поэкспериментировать с кодом, загрузка решения на локальный компьютер и затем запустив WebsiteDownload проекта или с помощью кода в конце этого раздела для создания проекта Дополнительные сведения и инструкции, см. раздел [проверка и выполнение примера приложения](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645).  
  
##  <a name="BKMK_HandlingReentrancy"></a>Обработка повторного входа  
 Обрабатывать повторный вход можно разными способами в зависимости от того, что требуется от приложения. В этом разделе представлены следующие примеры.  
  
-   [Отключение кнопки запуска](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645)  
  
     Отключить **запустить** кнопку во время операции, чтобы пользователь не может прерывать его.  
  
-   [Отмена и перезапуск операции](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645)  
  
     Отмена любой операции, которое все еще выполняется, когда пользователь выбирает **запустить** еще раз, а затем продолжить позволяют наиболее недавно запрошенной операции.  
  
-   [Запуск нескольких операций и выходные данные в очередь](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645)  
  
     Разрешение всем запрошенным операциям выполняться асинхронно и настройка согласования отображения выходных данных для вывода результатов каждой операции вместе и по порядку.  
  
###  <a name="BKMK_DisableTheStartButton"></a>Отключение кнопки запуска  
 Можно заблокировать **запустить** кнопку во время операции с отключения кнопки в верхней части `StartButton_Click` обработчика событий. Затем можно повторно включить кнопку из блока `Finally` по завершении операции, чтобы пользователь мог запустить приложение повторно.  
  
 В следующем коде показаны эти изменения, которые помечены звездочками. Изменения добавляются в код в конце этого раздела, или можно загрузить из завершенного приложения [образцы Async: повторного входа в приложениях рабочего стола .NET](http://go.microsoft.com/fwlink/?LinkId=266571). Имя проекта — DisableStartButton.  
  
```vb  
  
Private Async Sub StartButton_Click(sender As Object, e As RoutedEventArgs)  
    ' This line is commented out to make the results clearer in the output.  
    'ResultsTextBox.Text = ""  
  
    ' ***Disable the Start button until the downloads are complete.   
    StartButton.IsEnabled = False  
  
    Try  
        Await AccessTheWebAsync()  
  
    Catch ex As Exception  
        ResultsTextBox.Text &= vbCrLf & "Downloads failed."  
    ' ***Enable the Start button in case you want to run the program again.   
    Finally  
        StartButton.IsEnabled = True  
  
    End Try  
End Sub  
```  
  
 В результате этих изменений кнопка не будет реагировать в течение загрузки веб-сайтов методом `AccessTheWebAsync`, поэтому повторный вход в процесс будет невозможен.  
  
###  <a name="BKMK_CancelAndRestart"></a>Отмена и перезапуск операции  
 Вместо отключения **запустить** кнопки, можно сохранять активность кнопки но, если пользователь нажимает эту кнопку еще раз, отменить операцию, которая уже выполняется и продолжения запущенная последней операции.  
  
 Дополнительные сведения об отмене см. в разделе [Fine-Tuning асинхронного приложения (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/fine-tuning-your-async-application.md).  
  
 Для настройки этого сценария, внесите следующие изменения в базовый код, который предоставляется в [проверка и выполнение примера приложения](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645). Также можно загрузить из завершенного приложения [образцы Async: повторного входа в приложениях рабочего стола .NET](http://go.microsoft.com/fwlink/?LinkId=266571). Этот проект называется CancelAndRestart.  
  
1.  Объявите <xref:System.Threading.CancellationTokenSource>переменной, `cts`, который находится в области видимости для всех методов.</xref:System.Threading.CancellationTokenSource>  
  
    ```vb  
    Class MainWindow // Or Class MainPage  
  
        ' *** Declare a System.Threading.CancellationTokenSource.  
        Dim cts As CancellationTokenSource  
  
    ```  
  
2.  В `StartButton_Click` определите, выполняется ли операция на данный момент. Если значение `cts` — `Nothing`, операция не активна. Если значение не `Nothing`, отменить операцию, которая уже выполняется.  
  
    ```vb  
    ' *** If a download process is already underway, cancel it.  
    If cts IsNot Nothing Then  
        cts.Cancel()  
    End If  
  
    ```  
  
3.  Задайте для `cts` другое значение, представляющее текущий процесс.  
  
    ```vb  
    ' *** Now set cts to cancel the current process if the button is chosen again.  
    Dim newCTS As CancellationTokenSource = New CancellationTokenSource()  
    cts = newCTS  
  
    ```  
  
4.  В конце `StartButton_Click`, текущий процесс будет завершен, поэтому значение `cts` к `Nothing`.  
  
    ```vb  
    ' *** When the process completes, signal that another process can proceed.  
    If cts Is newCTS Then  
        cts = Nothing  
    End If  
  
    ```  
  
 В следующем коде показаны все изменения в `StartButton_Click`. Добавления помечены звездочками.  
  
```vb  
Private Async Sub StartButton_Click(sender As Object, e As RoutedEventArgs)  
  
    ' This line is commented out to make the results clearer.   
    'ResultsTextBox.Text = ""  
  
    ' *** If a download process is underway, cancel it.  
    If cts IsNot Nothing Then  
        cts.Cancel()  
    End If  
  
    ' *** Now set cts to cancel the current process if the button is chosen again.  
    Dim newCTS As CancellationTokenSource = New CancellationTokenSource()  
    cts = newCTS  
  
    Try  
        ' *** Send a token to carry the message if the operation is canceled.  
        Await AccessTheWebAsync(cts.Token)  
  
    Catch ex As OperationCanceledException  
        ResultsTextBox.Text &= vbCrLf & "Download canceled." & vbCrLf  
  
    Catch ex As Exception  
        ResultsTextBox.Text &= vbCrLf & "Downloads failed."  
    End Try  
  
    ' *** When the process is complete, signal that another process can proceed.  
    If cts Is newCTS Then  
        cts = Nothing  
    End If  
End Sub  
  
```  
  
 В `AccessTheWebAsync` внесите следующие изменения.  
  
-   Добавьте параметр, чтобы принимать токен отмены из `StartButton_Click`.  
  
-   Используйте <xref:System.Net.Http.HttpClient.GetAsync%2A>метод для загрузки на веб-сайтах, поскольку `GetAsync` принимает <xref:System.Threading.CancellationToken>аргумент.</xref:System.Threading.CancellationToken> </xref:System.Net.Http.HttpClient.GetAsync%2A>  
  
-   Перед вызовом метода `DisplayResults` для отображения результатов для каждого загруженного веб-сайта проверьте `ct`, чтобы убедиться, что текущая операция не отменена.  
  
 В следующем коде показаны эти изменения, которые помечены звездочками.  
  
```vb  
' *** Provide a parameter for the CancellationToken from StartButton_Click.  
Private Async Function AccessTheWebAsync(ct As CancellationToken) As Task  
  
    ' Declare an HttpClient object.  
    Dim client = New HttpClient()  
  
    ' Make a list of web addresses.  
    Dim urlList As List(Of String) = SetUpURLList()  
  
    Dim total = 0  
    Dim position = 0  
  
    For Each url In urlList  
        ' *** Use the HttpClient.GetAsync method because it accepts a   
        ' cancellation token.  
        Dim response As HttpResponseMessage = Await client.GetAsync(url, ct)  
  
        ' *** Retrieve the website contents from the HttpResponseMessage.  
        Dim urlContents As Byte() = Await response.Content.ReadAsByteArrayAsync()  
  
        ' *** Check for cancellations before displaying information about the   
        ' latest site.   
        ct.ThrowIfCancellationRequested()  
  
        position += 1  
        DisplayResults(url, urlContents, position)  
  
        ' Update the total.  
        total += urlContents.Length  
    Next  
  
    ' Display the total count for all of the websites.  
    ResultsTextBox.Text &=  
        String.Format(vbCrLf & vbCrLf & "TOTAL bytes returned:  " & total & vbCrLf)  
End Function  
  
```  
  
 При выборе **начать** несколько раз во время этого приложения, он должен создать результаты, которые похожи на следующие выходные данные.  
  
```  
1. msdn.microsoft.com/library/hh191443.aspx                83732  
2. msdn.microsoft.com/library/aa578028.aspx               205273  
3. msdn.microsoft.com/library/jj155761.aspx                29019  
4. msdn.microsoft.com/library/hh290140.aspx               122505  
5. msdn.microsoft.com/library/hh524395.aspx                68959  
6. msdn.microsoft.com/library/ms404677.aspx               197325  
Download canceled.  
  
1. msdn.microsoft.com/library/hh191443.aspx                83732  
2. msdn.microsoft.com/library/aa578028.aspx               205273  
3. msdn.microsoft.com/library/jj155761.aspx                29019  
Download canceled.  
  
1. msdn.microsoft.com/library/hh191443.aspx                83732  
2. msdn.microsoft.com/library/aa578028.aspx               205273  
3. msdn.microsoft.com/library/jj155761.aspx                29019  
4. msdn.microsoft.com/library/hh290140.aspx               117152  
5. msdn.microsoft.com/library/hh524395.aspx                68959  
6. msdn.microsoft.com/library/ms404677.aspx               197325  
7. msdn.microsoft.com                                            42972  
8. msdn.microsoft.com/library/ff730837.aspx               146159  
  
TOTAL bytes returned:  890591  
```  
  
 Чтобы исключить частичные списки, раскомментируйте первую строку кода в `StartButton_Click`, чтобы очищать текстовое поле при каждом перезапуске операции.  
  
###  <a name="BKMK_RunMultipleOperations"></a>Запуск нескольких операций и выходные данные в очередь  
 Третий пример является и самым сложным в том, что другая асинхронная операция каждый раз, которое выбирает пользователь запускает приложение **запустить** кнопки и все операции выполняются до их завершения. Все запрошенные операции загружают веб-сайты из списка асинхронно, однако выходные данные операций представляются последовательно. То есть, чередуются Фактическое действие загрузки, как выходные данные в [распознавание повторный вход](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645) показывает, но список результатов для каждой группы предоставляется отдельно.  
  
 Операции совместно используют глобальный <xref:System.Threading.Tasks.Task>, `pendingWork`, который служит для отображения процесса привратника.</xref:System.Threading.Tasks.Task>  
  
 Этот пример можно запустить, вставив изменения в код в [построение приложения](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645), или вы можете следовать указаниям в [загрузка приложения](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645) для загрузки образца и запуска проекта QueueResults.  
  
 Следующий результат показан результат, если пользователь выбирает **запустить** кнопку только один раз. Указывает метку буквы A, что получается после первой **запустить** кнопка. Нумерация показывает порядок отображения URL-адресов в списке целевых объектов для загрузки.  
  
```  
  
#Starting group A.  
#Task assigned for group A.  
  
A-1. msdn.microsoft.com/library/hh191443.aspx                87389  
A-2. msdn.microsoft.com/library/aa578028.aspx               209858  
A-3. msdn.microsoft.com/library/jj155761.aspx                30870  
A-4. msdn.microsoft.com/library/hh290140.aspx               119027  
A-5. msdn.microsoft.com/library/hh524395.aspx                71260  
A-6. msdn.microsoft.com/library/ms404677.aspx               199186  
A-7. msdn.microsoft.com                                            53266  
A-8. msdn.microsoft.com/library/ff730837.aspx               148020  
  
TOTAL bytes returned:  918876  
  
#Group A is complete.  
```  
  
 Если пользователь **запустить** три раза, приложение выдает результат, похожий на приведенный ниже. Информационные строки, начинающиеся с символа #, отслеживают ход выполнения приложения.  
  
```  
#Starting group A.  
#Task assigned for group A.  
  
A-1. msdn.microsoft.com/library/hh191443.aspx                87389  
A-2. msdn.microsoft.com/library/aa578028.aspx               207089  
A-3. msdn.microsoft.com/library/jj155761.aspx                30870  
A-4. msdn.microsoft.com/library/hh290140.aspx               119027  
A-5. msdn.microsoft.com/library/hh524395.aspx                71259  
A-6. msdn.microsoft.com/library/ms404677.aspx               199185  
  
#Starting group B.  
#Task assigned for group B.  
  
A-7. msdn.microsoft.com                                            53266  
  
#Starting group C.  
#Task assigned for group C.  
  
A-8. msdn.microsoft.com/library/ff730837.aspx               148010  
  
TOTAL bytes returned:  916095  
  
B-1. msdn.microsoft.com/library/hh191443.aspx                87389  
B-2. msdn.microsoft.com/library/aa578028.aspx               207089  
B-3. msdn.microsoft.com/library/jj155761.aspx                30870  
B-4. msdn.microsoft.com/library/hh290140.aspx               119027  
B-5. msdn.microsoft.com/library/hh524395.aspx                71260  
B-6. msdn.microsoft.com/library/ms404677.aspx               199186  
  
#Group A is complete.  
  
B-7. msdn.microsoft.com                                            53266  
B-8. msdn.microsoft.com/library/ff730837.aspx               148010  
  
TOTAL bytes returned:  916097  
  
C-1. msdn.microsoft.com/library/hh191443.aspx                87389  
C-2. msdn.microsoft.com/library/aa578028.aspx               207089  
  
#Group B is complete.  
  
C-3. msdn.microsoft.com/library/jj155761.aspx                30870  
C-4. msdn.microsoft.com/library/hh290140.aspx               119027  
C-5. msdn.microsoft.com/library/hh524395.aspx                72765  
C-6. msdn.microsoft.com/library/ms404677.aspx               199186  
C-7. msdn.microsoft.com                                            56190  
C-8. msdn.microsoft.com/library/ff730837.aspx               148010  
  
TOTAL bytes returned:  920526  
  
#Group C is complete.  
  
```  
  
 Группы B и C запускаются до завершения группы A, однако результаты для каждой группы отображаются отдельно. Все выходные данные для группы A отображается первой, затем все выходные данные для группы B, а затем все выходные данные для группы C. Приложение всегда отображаются группы в порядке и для каждой группы, всегда отображает сведения об отдельных веб-сайтов в порядке следования URL-адреса в список URL-адресов.  
  
 Тем не менее невозможно предсказать порядок, в котором фактически происходит загрузка. После запуска нескольких групп все созданные ими задачи загрузки остаются активными. Не следует предполагать, что данные A-1 будут загружены до данных B-1, а данные A-1 будут загружены до данных A-2.  
  
#### <a name="global-definitions"></a>Глобальные определения  
 Пример кода содержит объявление двух следующих глобальных переменных, доступных для всех методов.  
  
```vb  
Class MainWindow    ' Class MainPage in Windows Store app.  
  
    ' ***Declare the following variables where all methods can access them.   
    Private pendingWork As Task = Nothing  
    Private group As Char = ChrW(AscW("A") - 1)  
```  
  
 Переменная `Task`, `pendingWork`, отслеживает процесс отображения и предотвращает прерывание операции отображения одной группы другой группой. Символьная переменная, `group`, помечает выходные данные различных групп, чтобы гарантировать отображение результатов в ожидаемом порядке.  
  
#### <a name="the-click-event-handler"></a>Обработчик событий нажатия  
 Обработчик событий `StartButton_Click`, увеличивается каждый раз при выборе группы буква **запустить** кнопки. Затем обработчик вызывает метод `AccessTheWebAsync` для запуска операции загрузки.  
  
```vb  
Private Async Sub StartButton_Click(sender As Object, e As RoutedEventArgs)  
    ' ***Verify that each group's results are displayed together, and that  
    ' the groups display in order, by marking each group with a letter.  
    group = ChrW(AscW(group) + 1)  
    ResultsTextBox.Text &= String.Format(vbCrLf & vbCrLf & "#Starting group {0}.", group)  
  
    Try  
        ' *** Pass the group value to AccessTheWebAsync.  
        Dim finishedGroup As Char = Await AccessTheWebAsync(group)  
  
        ' The following line verifies a successful return from the download and   
        ' display procedures.   
        ResultsTextBox.Text &= String.Format(vbCrLf & vbCrLf & "#Group {0} is complete." & vbCrLf, finishedGroup)  
  
    Catch ex As Exception  
        ResultsTextBox.Text &= vbCrLf & "Downloads failed."  
  
    End Try  
End Sub  
```  
  
#### <a name="the-accessthewebasync-method"></a>Метод AccessTheWebAsync  
 В этом примере метод `AccessTheWebAsync` разбит на два метода. Первый метод, `AccessTheWebAsync`, запускает все задачи загрузки для группы и передает задаче `pendingWork` управление процессом отображения. Метод использует Language Integrated Query (запрос LINQ) и <xref:System.Linq.Enumerable.ToArray%2A>для запуска задач загрузки одновременно.</xref:System.Linq.Enumerable.ToArray%2A>  
  
 Затем метод `AccessTheWebAsync` вызывает метод `FinishOneGroupAsync` для ожидания завершения каждой загрузки и отображения ее длины.  
  
 Метод `FinishOneGroupAsync` возвращает задачу, которая назначена `pendingWork`, в `AccessTheWebAsync`. Это значение предотвращает прерывание другой операцией до завершения выполнения задачи.  
  
```vb  
Private Async Function AccessTheWebAsync(grp As Char) As Task(Of Char)  
  
    Dim client = New HttpClient()  
  
    ' Make a list of the web addresses to download.  
    Dim urlList As List(Of String) = SetUpURLList()  
  
    ' ***Kick off the downloads. The application of ToArray activates all the download tasks.  
    Dim getContentTasks As Task(Of Byte())() =  
        urlList.Select(Function(addr) client.GetByteArrayAsync(addr)).ToArray()  
  
    ' ***Call the method that awaits the downloads and displays the results.  
    ' Assign the Task that FinishOneGroupAsync returns to the gatekeeper task, pendingWork.  
    pendingWork = FinishOneGroupAsync(urlList, getContentTasks, grp)  
  
    ResultsTextBox.Text &=  
        String.Format(vbCrLf & "#Task assigned for group {0}. Download tasks are active." & vbCrLf, grp)  
  
    ' ***This task is complete when a group has finished downloading and displaying.  
    Await pendingWork  
  
    ' You can do other work here or just return.  
    Return grp  
End Function  
```  
  
#### <a name="the-finishonegroupasync-method"></a>Метод FinishOneGroupAsync  
 Этот метод выполняет циклический переход по задачам загрузки в группе, ожидая каждую из них, отображая длину загруженного веб-сайта и добавляя длину в общую сумму.  
  
 Первый оператор в `FinishOneGroupAsync` использует `pendingWork` чтобы убедиться в том, что метод ввода не мешает операции уже находится в процессе отображения или который уже находится в состоянии ожидания. Если такая операция выполняется, новая операция должна дождаться своей очереди.  
  
```vb  
Private Async Function FinishOneGroupAsync(urls As List(Of String), contentTasks As Task(Of Byte())(), grp As Char) As Task  
  
    ' Wait for the previous group to finish displaying results.  
    If pendingWork IsNot Nothing Then  
        Await pendingWork  
    End If  
  
    Dim total = 0  
  
    ' contentTasks is the array of Tasks that was created in AccessTheWebAsync.  
    For i As Integer = 0 To contentTasks.Length - 1  
        ' Await the download of a particular URL, and then display the URL and  
        ' its length.  
        Dim content As Byte() = Await contentTasks(i)  
        DisplayResults(urls(i), content, i, grp)  
        total += content.Length  
    Next  
  
    ' Display the total count for all of the websites.  
    ResultsTextBox.Text &=  
        String.Format(vbCrLf & vbCrLf & "TOTAL bytes returned:  " & total & vbCrLf)  
End Function  
```  
  
 Этот пример можно запустить, вставив изменения в код в [построение приложения](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645), или вы можете следовать указаниям в [загрузка приложения](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645) для загрузки образца и запуска проекта QueueResults.  
  
#### <a name="points-of-interest"></a>Интересующие точки  
 Информационные строки, начинающиеся с символа # в выходных данных, поясняют, как работает этот пример.  
  
 Выходные данные демонстрируют следующие схемы.  
  
-   Группу можно запустить, когда предыдущая группа отображает свои выходные данные, но отображение выходных данных предыдущей группы не прерывается.  
  
    ```  
    #Starting group A.  
    #Task assigned for group A. Download tasks are active.  
  
    A-1. msdn.microsoft.com/library/hh191443.aspx                87389  
    A-2. msdn.microsoft.com/library/aa578028.aspx               207089  
    A-3. msdn.microsoft.com/library/jj155761.aspx                30870  
    A-4. msdn.microsoft.com/library/hh290140.aspx               119037  
    A-5. msdn.microsoft.com/library/hh524395.aspx                71260  
  
    #Starting group B.  
    #Task assigned for group B. Download tasks are active.  
  
    A-6. msdn.microsoft.com/library/ms404677.aspx               199186  
    A-7. msdn.microsoft.com                                            53078  
    A-8. msdn.microsoft.com/library/ff730837.aspx               148010  
  
    TOTAL bytes returned:  915919  
  
    B-1. msdn.microsoft.com/library/hh191443.aspx                87388  
    B-2. msdn.microsoft.com/library/aa578028.aspx               207089  
    B-3. msdn.microsoft.com/library/jj155761.aspx                30870  
  
    #Group A is complete.  
  
    B-4. msdn.microsoft.com/library/hh290140.aspx               119027  
    B-5. msdn.microsoft.com/library/hh524395.aspx                71260  
    B-6. msdn.microsoft.com/library/ms404677.aspx               199186  
    B-7. msdn.microsoft.com                                            53078  
    B-8. msdn.microsoft.com/library/ff730837.aspx               148010  
  
    TOTAL bytes returned:  915908  
    ```  
  
-   `pendingWork` Задачи `Nothing` в начале `FinishOneGroupAsync` только для группы A, которая запущена первой. Группа A еще не завершила выражение await, когда она достигает метода `FinishOneGroupAsync`. Таким образом, управление не возвращается `AccessTheWebAsync`, а первое присваивание задаче `pendingWork` не возникает.  
  
-   Следующие две строки всегда отображаются в выходных данных вместе. Код не прерывается нигде между запуском операции группы в обработчике `StartButton_Click` и назначением задачи для группы в `pendingWork`.  
  
    ```  
    #Starting group B.  
    #Task assigned for group B. Download tasks are active.  
    ```  
  
     После входа группы в обработчик `StartButton_Click` операция не завершает выражение await до входа операции в метод `FinishOneGroupAsync`. Таким образом, другие операции не могут получить контроль во время выполнения этого фрагмента кода.  
  
##  <a name="BKMD_SettingUpTheExample"></a>Проверка и выполнение примера приложения  
 Чтобы лучше понять пример приложения, его можно загрузить, построить самостоятельно или просмотреть код в конце этого раздела, не реализуя приложение.  
  
> [!NOTE]
>  Чтобы запустить пример как классического приложения Windows Presentation Foundation (WPF), необходимо иметь Visual Studio 2012 или более поздней версии и платформы .NET Framework 4.5 или более новая версия вашего компьютера.  
  
###  <a name="BKMK_DownloadingTheApp"></a>Загрузка приложения  
  
1.  Загрузите сжатый файл с [образцы Async: повторного входа в приложениях рабочего стола .NET](http://go.microsoft.com/fwlink/?LinkId=266571).  
  
2.  Распакуйте загруженный файл, а затем запустите Visual Studio.  
  
3.  В строке меню выберите **Файл**, **Открыть**, **Проект/Решение**.  
  
4.  Перейдите к папке, содержащей распакованный пример кода, а затем откройте файл решения (SLN-файл).  
  
5.  В **обозревателе решений**, откройте контекстное меню для проекта, который требуется запустить, а затем выберите **по StartUpProject**.  
  
6.  Нажмите сочетание клавиш CTRL+F5, чтобы выполнить сборку и запуск проекта.  
  
###  <a name="BKMK_BuildingTheApp"></a>Построение приложения  
 Ниже приводится код для построения примера в качестве приложения WPF.  
  
##### <a name="to-build-a-wpf-app"></a>Построение приложения WPF  
  
1.  Запустите Visual Studio.  
  
2.  В строке меню выберите **Файл**, **Создать**, **Проект**.  
  
     Откроется диалоговое окно **Новый проект** .  
  
3.  В **установленные шаблоны** панели разверните **Visual Basic**, а затем разверните **Windows**.  
  
4.  В списке типов проекта выберите **приложение WPF**.  
  
5.  Назовите проект `WebsiteDownloadWPF`, а затем выберите **ОК** кнопки.  
  
     Появится новый проект в **обозревателе решений**.  
  
6.  В редакторе кода Visual Studio перейдите на вкладку **MainWindow.xaml** .  
  
     Если вкладка не отображается, откройте контекстное меню для MainWindow.xaml в **обозревателе решений**, а затем выберите **Просмотр кода**.  
  
7.  В **XAML** Просмотр файла MainWindow.XAML, замените код следующим кодом.  
  
    ```vb  
    <Window x:Class="MainWindow"  
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
        xmlns:local="using:WebsiteDownloadWPF"  
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"  
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
        mc:Ignorable="d">  
  
        <Grid Width="517" Height="360">  
            <Button x:Name="StartButton" Content="Start" HorizontalAlignment="Left" Margin="-1,0,0,0" VerticalAlignment="Top" Click="StartButton_Click" Height="53" Background="#FFA89B9B" FontSize="36" Width="518"  />  
            <TextBox x:Name="ResultsTextBox" HorizontalAlignment="Left" Margin="-1,53,0,-36" TextWrapping="Wrap" VerticalAlignment="Top" Height="343" FontSize="10" ScrollViewer.VerticalScrollBarVisibility="Visible" Width="518" FontFamily="Lucida Console" />  
        </Grid>  
    </Window>  
    ```  
  
     Появится простое окно, содержащее текстовое поле и кнопку в **разработки** файла MainWindow.XAML.  
  
8.  Добавить ссылку <xref:System.Net.Http>.</xref:System.Net.Http>  
  
9. В **обозревателе решений**, откройте контекстное меню для MainWindow.xaml.vb и выберите **Просмотр кода**.  
  
10. В файл MainWindow.xaml.vb замените код следующим кодом.  
  
    ```vb  
    ' Add the following Imports statements, and add a reference for System.Net.Http.  
    Imports System.Net.Http  
    Imports System.Threading  
  
    Class MainWindow  
  
        Private Async Sub StartButton_Click(sender As Object, e As RoutedEventArgs)  
            ' This line is commented out to make the results clearer in the output.  
            'ResultsTextBox.Text = ""  
  
            Try  
                Await AccessTheWebAsync()  
  
            Catch ex As Exception  
                ResultsTextBox.Text &= vbCrLf & "Downloads failed."  
  
            End Try  
        End Sub  
  
        Private Async Function AccessTheWebAsync() As Task  
  
            ' Declare an HttpClient object.  
            Dim client = New HttpClient()  
  
            ' Make a list of web addresses.  
            Dim urlList As List(Of String) = SetUpURLList()  
  
            Dim total = 0  
            Dim position = 0  
  
            For Each url In urlList  
                ' GetByteArrayAsync returns a task. At completion, the task  
                ' produces a byte array.  
                Dim urlContents As Byte() = Await client.GetByteArrayAsync(url)  
  
                position += 1  
                DisplayResults(url, urlContents, position)  
  
                ' Update the total.  
                total += urlContents.Length  
            Next  
  
            ' Display the total count for all of the websites.  
            ResultsTextBox.Text &=  
                String.Format(vbCrLf & vbCrLf & "TOTAL bytes returned:  " & total & vbCrLf)  
        End Function  
  
        Private Function SetUpURLList() As List(Of String)  
            Dim urls = New List(Of String) From  
            {  
                "http://msdn.microsoft.com/library/hh191443.aspx",  
                "http://msdn.microsoft.com/library/aa578028.aspx",  
                "http://msdn.microsoft.com/library/jj155761.aspx",  
                "http://msdn.microsoft.com/library/hh290140.aspx",  
                "http://msdn.microsoft.com/library/hh524395.aspx",  
                "http://msdn.microsoft.com/library/ms404677.aspx",  
                "http://msdn.microsoft.com",  
                "http://msdn.microsoft.com/library/ff730837.aspx"  
            }  
            Return urls  
        End Function  
  
        Private Sub DisplayResults(url As String, content As Byte(), pos As Integer)  
            ' Display the length of each website. The string format is designed  
            ' to be used with a monospaced font, such as Lucida Console or  
            ' Global Monospace.  
  
            ' Strip off the "http:'".  
            Dim displayURL = url.Replace("http://", "")  
            ' Display position in the URL list, the URL, and the number of bytes.  
            ResultsTextBox.Text &= String.Format(vbCrLf & "{0}. {1,-58} {2,8}", pos, displayURL, content.Length)  
        End Sub  
    End Class  
    ```  
  
11. Нажмите сочетание клавиш CTRL + F5, чтобы запустить программу, а затем выберите **начать** несколько раз.  
  
12. Внесите изменения в [отключить кнопку Пуск](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645), [Отмена и перезапуск операции](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645), или [выполнения нескольких операций и очереди вывода](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645) обрабатывать повторный вход.  
  
## <a name="see-also"></a>См. также  
 [Пошаговое руководство: Доступ к Интернету с помощью модификатора Async и Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)   
 [Асинхронное программирование с использованием Async и Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/index.md)