---
title: '#line (справочник по C#)'
ms.date: 07/20/2015
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- '#line'
helpviewer_keywords:
- '#line directive [C#]'
ms.assetid: 6439e525-5dd5-4acb-b8ea-efabb32ff95b
caps.latest.revision: 13
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 3d2f42915d214349eebff40949482d7f603c0c2c
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="line-c-reference"></a>#line (Справочник по C#)
Директива `#line` позволяет изменять номер строки компилятора и при необходимости имя файла, в который будут выводиться ошибки и предупреждения. В этом примере показано, как включить в отчет два предупреждения, связанные с номерами строк. Директива `#line 200` принудительно устанавливает номер строки 200 (по умолчанию используется номер 7). До выполнения следующей директивы #line в отчете будет указываться имя файла "Special". Директива #line по умолчанию восстанавливает нумерацию строк в исходное состояние с учетом строк, номера которых были изменены с помощью предшествующей директивы.  
  
```csharp
class MainClass  
{  
    static void Main()  
    {  
#line 200 "Special"  
        int i;    // CS0168 on line 200  
        int j;    // CS0168 on line 201  
#line default  
        char c;   // CS0168 on line 9  
        float f;  // CS0168 on line 10  
#line hidden // numbering not affected  
        string s;   
        double d; // CS0168 on line 13  
    }  
}  
```  
  
## <a name="remarks"></a>Примечания  
 Директива `#line` может использоваться на автоматизированном промежуточном этапе процесса построения. Например, если строки были удалены из первоначального файла с исходным кодом, но вам по-прежнему требуется создавать выходные файлы компилятора на основе изначальной нумерации строк в файле, можно удалить строки и затем смоделировать их первичную нумерацию с помощью директивы `#line`.  
  
 Директива `#line hidden` скрывает последующие строки для отладчика. В этом случае при пошаговой проверке кода разработчиком все строки между `#line hidden` и следующей директивой `#line` (кроме случаев, когда это также директива `#line hidden`) будут пропущены. Этот параметр также можно использовать для того, чтобы дать ASP.NET возможность различать определяемый пользователем и создаваемый компьютером код. В основном эта функция используется в ASP.NET, но также может быть полезна и в других генераторах исходного кода.  
  
 Директива `#line hidden` не влияет на имена файлов и номера строк в отчетах об ошибках. Это значит, что при обнаружении ошибки в скрытом блоке компилятор укажет в отчете текущие имя файла и номер строки, где найдена ошибка.  
  
 Директива `#line filename` задает имя файла, которое будет отображаться в выходных данных компилятора. По умолчанию используется фактическое имя файла с исходным кодом. Имя файла должно заключаться в двойные кавычки (" "). Перед ним должен указываться номер строки.  
  
 Файл с исходным кодом может содержать любое количество директив `#line`.  
  
## <a name="example-1"></a>Пример 1  
 В следующем примере демонстрируется, как отладчик игнорирует скрытые строки кода. При выполнении этого примера будут показаны три строки текста. Тем не менее, если задать точку останова, как показано в этом примере, и нажать клавишу F10 для пошаговой отладки кода, вы увидите, что отладчик игнорирует скрытую строку. Обратите внимание, что даже если точка останова установлена на скрытой строке, отладчик по-прежнему будет игнорировать ее.  
  
```csharp
// preprocessor_linehidden.cs  
using System;  
class MainClass   
{  
    static void Main()   
    {  
        Console.WriteLine("Normal line #1."); // Set break point here.  
#line hidden  
        Console.WriteLine("Hidden line.");  
#line default  
        Console.WriteLine("Normal line #2.");  
    }  
}  
```  
  
## <a name="see-also"></a>См. также  
 [Справочник по C#](../../../csharp/language-reference/index.md)  
 [Руководство по программированию на C#](../../../csharp/programming-guide/index.md)  
 [Директивы препроцессора C#](../../../csharp/language-reference/preprocessor-directives/index.md)
