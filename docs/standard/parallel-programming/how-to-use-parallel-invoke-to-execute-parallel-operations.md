---
title: "Практическое руководство. Использование метода Parallel.Invoke для выполнения параллельных операций"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- task parallelism in .NET
- parallel programming, task parallelism
ms.assetid: 6b3ecd79-dec9-4ce1-abf4-62e5392a59c6
caps.latest.revision: 
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 942ba120fa5273f84ac3d0a51e276223de5f5484
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/23/2017
---
# <a name="how-to-use-parallelinvoke-to-execute-parallel-operations"></a>Практическое руководство. Использование метода Parallel.Invoke для выполнения параллельных операций
В этом примере показывается, как параллелизовать операции с помощью метода <xref:System.Threading.Tasks.Parallel.Invoke%2A> в библиотеке параллельных задач. В общем источнике данных выполняются три операции. Поскольку ни одна из этих операций не изменяет источник, они могут выполняться параллельно простым способом.  
  
> [!NOTE]
>  В этой документации для определения делегатов в библиотеке параллельных задач используются лямбда-выражения. Если вы не знакомы с лямбда-выражениями в C# или Visual Basic, см. раздел [Лямбда-выражения в PLINQ и TPL](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md).  
  
## <a name="example"></a>Пример  
 [!code-csharp[TPL_Parallel#06](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/parallelinvoke.cs#06)]
 [!code-vb[TPL_Parallel#06](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/parallelinvoke.vb#06)]  
  
 Обратите внимание, что с помощью метода <xref:System.Threading.Tasks.Parallel.Invoke%2A> можно просто указать, какие действия должны выполняться параллельно, и среда выполнения обработает все сведения по планированию потока, включая автоматическое масштабирование на число ядер в главном компьютере.  
  
 В этом примере параллелизуются операции, но не данные. Как вариант можно параллелизовать запросы LINQ с помощью PLINQ и выполнять эти запросы последовательно. Кроме того, можно параллелизовать данные с помощью PLINQ. Другим вариантом является параллелизация запросов и задач. Хотя итоговая нагрузка может снизить производительность главных компьютеров с относительно небольшим числом процессоров, масштабирование будет выполняться гораздо лучше на компьютерах с большим числом процессоров.  
  
## <a name="compiling-the-code"></a>Компиляция кода  
  
-   Скопируйте и вставьте весь пример в проект Microsoft Visual Studio 2010 и нажмите клавишу F5.  
  
## <a name="see-also"></a>См. также  
 [Параллельное программирование](../../../docs/standard/parallel-programming/index.md)  
 [Практическое руководство. Отмена задачи и ее дочерних элементов](../../../docs/standard/parallel-programming/how-to-cancel-a-task-and-its-children.md)  
 [Parallel LINQ (PLINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)
