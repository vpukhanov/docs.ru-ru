---
title: Оператор false (Справочник по C#)
ms.date: 07/20/2015
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
helpviewer_keywords:
- false operator keyword [C#]
ms.assetid: 81a888fd-011e-4589-b242-6c261fea505e
caps.latest.revision: 21
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 6f9761fb49e2c7f6e4a7615e64cec9fed88318c1
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="false-operator-c-reference"></a>Оператор false (Справочник по C#)
Возвращает [логическое](../../../csharp/language-reference/keywords/bool.md) значение `true`, чтобы указать, что операнд является `false`, и возвращает значение `false` в противном случае.  
  
 До версии C# 2.0 операторы `true` и `false` использовались для создания пользовательских типов значений, допускающих значение NULL, которые были совместимы с такими типами, как `SqlBool`. Однако теперь язык предоставляет встроенную поддержку для типов, допускающих значение NULL, и по возможности следует использовать их вместо перегрузки операторов `true` и `false`. Дополнительные сведения см. в разделе [Типы, допускающие значение NULL](../../../csharp/programming-guide/nullable-types/index.md).  
  
 С логическими значениями, допускающими значение NULL, выражение `a != b` не обязательно равно `!(a == b)`, так как одно или оба значений могут иметь значение NULL. Необходимо перегрузить оба оператора `true` и `false` отдельно, чтобы правильно обработать значения NULL в выражении. В следующем примере демонстрируется перегрузка и использование операторов `true` и `false`.  
  
 [!code-csharp[csrefKeywordsOperator#16](../../../csharp/language-reference/keywords/codesnippet/CSharp/false-operator_1.cs)]  
  
 Тип, который перегружает операторы `true` и `false`, может использоваться для выражений управления в операторах [if](../../../csharp/language-reference/keywords/if-else.md), [do](../../../csharp/language-reference/keywords/do.md), [while](../../../csharp/language-reference/keywords/while.md) и [for](../../../csharp/language-reference/keywords/for.md) и в [условных выражениях](../../../csharp/language-reference/operators/conditional-operator.md).  
  
 Если тип определяет оператор `false`, он должен также определять оператор [true](../../../csharp/language-reference/keywords/true.md).  
  
 Тип не может непосредственно перегрузить условные логические операторы [&&](../../../csharp/language-reference/operators/conditional-and-operator.md) и [||](../../../csharp/language-reference/operators/conditional-or-operator.md), однако такой же результат может быть достигнут путем перегрузки обычных логических операторов и операторов `true` и `false`.  
  
## <a name="c-language-specification"></a>Спецификация языка C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>См. также  
 [Справочник по C#](../../../csharp/language-reference/index.md)  
 [Руководство по программированию на C#](../../../csharp/programming-guide/index.md)  
 [Ключевые слова в C#](../../../csharp/language-reference/keywords/index.md)  
 [Операторы в C#](../../../csharp/language-reference/operators/index.md)  
 [true](../../../csharp/language-reference/keywords/true.md)
