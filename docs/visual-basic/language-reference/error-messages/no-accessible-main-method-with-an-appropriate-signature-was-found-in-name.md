---
title: "Ни один из доступных &#39; Main &#39; найден метод с соответствующей сигнатурой в &#39; &lt;имя&gt;&#39;"
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc30737
- vbc30737
helpviewer_keywords:
- BC30737
ms.assetid: 3f40bacd-3fac-4741-b204-852f693d4340
caps.latest.revision: 
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: e6a2d66c860b72bd3ef59c02f548ac563fab6b8c
ms.sourcegitcommit: 34ec7753acf76f90a0fa845235ef06663dc9e36e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/21/2017
---
# <a name="no-accessible-39main39-method-with-an-appropriate-signature-was-found-in-39ltnamegt39"></a>Ни один из доступных &#39; Main &#39; найден метод с соответствующей сигнатурой в &#39; &lt;имя&gt;&#39;
Приложения командной строки должны иметь `Sub Main` определен. `Main`должен быть объявлен как `Public Shared` , если оно определено в классе или как `Public` , если определено в модуле.  
  
 **Идентификатор ошибки:** BC30737  
  
## <a name="to-correct-this-error"></a>Исправление ошибки  
  
-   Определение `Public Sub Main` процедуры для вашего проекта. Он объявляется как `Shared` только в том случае, если она определяется внутри класса.  
  
## <a name="see-also"></a>См. также  
 [Структура программы Visual Basic](../../../visual-basic/programming-guide/program-structure/structure-of-a-visual-basic-program.md)  
 [Процедуры](../../../visual-basic/programming-guide/language-features/procedures/index.md)
