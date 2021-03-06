---
title: "Практическое руководство. Преобразование строки (String) в массив символов в Visual Basic"
ms.custom: 
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- character arrays [Visual Basic], converting strings
- arrays [Visual Basic], converting strings to
- examples [Visual Basic], string conversion
- strings [Visual Basic], converting to arrays
- string conversion [Visual Basic], arrays
ms.assetid: 1b54b686-ab29-413b-adce-6bd5422376eb
caps.latest.revision: "7"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 59d0da52c8f78b93c76325e6242156c106deeaf1
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="how-to-convert-a-string-to-an-array-of-characters-in-visual-basic"></a>Практическое руководство. Преобразование строки (String) в массив символов в Visual Basic
Иногда полезно располагать сведениями о символов в строке и позициях этих символов, например при анализе строки. В этом примере показано, как получить массив символов в строку путем вызова строки <xref:System.String.ToCharArray%2A> метод.  
  
## <a name="example"></a>Пример  
 В этом примере показано, как разбить строку в `Char` массива и как разбить строку на `String` массив знаков Юникода. Причина различия — что Юникода может состоять из двух или более `Char` символов (например, суррогатная пара или несамостоятельных последовательность символов). Дополнительные сведения см. в разделе <xref:System.Globalization.TextElementEnumerator> и «Стандарте Юникод» http://www.Unicode.org.  
  
 [!code-vb[VbVbalrStrings#75](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/how-to-convert-a-string-to-an-array-of-characters_1.vb)]  
  
## <a name="example"></a>Пример  
 Это более сложным для разбиения строки на знаков Юникода, но это необходимо для получения сведений о визуальном представлении строки. В этом примере используется <xref:System.Globalization.StringInfo.SubstringByTextElements%2A> метод, чтобы получить сведения о текстовых символов Юникода, составляющих строку.  
  
 [!code-vb[VbVbalrStrings#76](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/how-to-convert-a-string-to-an-array-of-characters_2.vb)]  
  
## <a name="see-also"></a>См. также  
 <xref:System.String.Chars%2A>  
 <xref:System.Globalization.StringInfo?displayProperty=nameWithType>  
 [Практическое руководство. Доступ к символам в строках](../../../../visual-basic/programming-guide/language-features/strings/how-to-access-characters-in-strings.md)  
 [Преобразование между строками и другими типами данных в Visual Basic](../../../../visual-basic/programming-guide/language-features/strings/converting-between-strings-and-other-data-types.md)  
 [Строки](../../../../visual-basic/programming-guide/language-features/strings/index.md)
