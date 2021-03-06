---
title: Оператор Delegate
ms.date: 07/20/2015
ms.prod: .net
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Delegate
helpviewer_keywords:
- delegate keyword [Visual Basic]
- Delegate statement [Visual Basic]
ms.assetid: f799c518-0817-40cc-ad0b-4da846fdba57
caps.latest.revision: 27
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 7e79a261f74cbc7aa067af63629e31bedf65d163
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="delegate-statement"></a>Оператор Delegate
Используется для объявления делегата. Делегат — это ссылочный тип, который ссылается на `Shared` метод типа или метода экземпляра объекта. Для создания экземпляра этого класса делегата можно использовать любую процедуру с соответствующими типами параметров и возвращаемых. Процедура может затем быть вызвана через экземпляр делегата.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
[ <attrlist> ] [ accessmodifier ] _  
[ Shadows ] Delegate [ Sub | Function ] name [( Of typeparamlist )] [([ parameterlist ])] [ As type ]  
```  
  
## <a name="parts"></a>Части  
  
|Термин|Определение|  
|---|---|  
|`attrlist`|Необязательно. Список атрибутов, которые применяются для данного делегата. Несколько атрибутов разделяются запятыми. Необходимо заключить [список атрибутов](../../../visual-basic/language-reference/statements/attribute-list.md) в угловые скобки («`<`«и»`>`»).|  
|`accessmodifier`|Необязательно. Указывает, какой код может обращаться к делегату. Ниже указаны доступные значения.<br /><br /> -   [Открытые](../../../visual-basic/language-reference/modifiers/public.md). Любой код, который можно получить доступ к элементу, который объявляет делегат к нему возможен доступ.<br />-   [Защищенные](../../../visual-basic/language-reference/modifiers/protected.md). Только код в пределах класса делегата или производного класса к нему возможен доступ.<br />-   [Дружественные](../../../visual-basic/language-reference/modifiers/friend.md). Только код внутри той же сборке может получить доступ к делегата.<br />-   [Закрытый](../../../visual-basic/language-reference/modifiers/private.md). Только код внутри элемента, который объявляет делегат может обращаться к его.<br /><br /> Можно указать `Protected Friend` для обеспечения доступа из кода внутри класса делегата, производном классе или той же сборки.|  
|`Shadows`|Необязательно. Указывает, что этот делегат повторно объявляет и скрывает идентично именованный программный элемент или набор перегруженных элементов в базовом классе. Можно скрыть любой тип объявленного элемента, используя любой другой тип.<br /><br /> Скрытый элемент недоступен из производного класса, который его скрывает, за исключением тех классов, из которых недоступен скрывающий элемент. Например если `Private` элемент скрывает элемент базового класса, код, который не имеет разрешения на доступ к `Private` элемент обращается к элементу базового класса.|  
|`Sub`|Необязательно, но либо `Sub` или `Function` должны отображаться. Объявляет процедуру представителем `Sub` процедуру, которая не возвращает значение.|  
|`Function`|Необязательно, но либо `Sub` или `Function` должны отображаться. Объявляет процедуру представителем `Function` процедуры, возвращающей значение.|  
|`name`|Обязательный. Имя типа делегата; соответствует стандартным правилам именования переменных.|  
|`typeparamlist`|Необязательно. Список параметров типа для этого делегата. Несколько параметров типа разделяются запятыми. Кроме того, каждый параметр типа можно объявить как вариант с использованием `In` и `Out` универсальных модификаторов. Необходимо заключить [список типов](../../../visual-basic/language-reference/statements/type-list.md) в круглые скобки и ввести его с `Of` ключевое слово.|  
|`parameterlist`|Необязательно. Список параметров, передаваемых при вызове процедуры. Необходимо заключить [список параметров](../../../visual-basic/language-reference/statements/parameter-list.md) в круглые скобки.|  
|`type`|Требуется, если указана `Function` процедуры. Тип данных возвращаемого значения.|  
  
## <a name="remarks"></a>Примечания  
 `Delegate` Типы параметров и возвращаемых классом делегата, определяются оператором. Для создания экземпляра этого класса делегата можно использовать любую процедуру с соответствующими параметрами и возвращаемыми типами. Процедура может затем быть вызвана через экземпляр делегата путем вызова делегата `Invoke` метод.  
  
 Делегаты можно объявлять пространства имен, модуля, класса или структуры уровня, но не внутри процедуры.  
  
 Каждый класс делегата определяет конструктор, которому передается спецификация метода объекта. Аргумент конструктора делегата должен быть ссылкой на метод или лямбда-выражение.  
  
 Чтобы указать ссылку на метод, используйте следующий синтаксис:  
  
 `AddressOf` [`expression`.]`methodname`  
  
 Тип `expression` во время компиляции должен представлять собой имя класса или интерфейса, который содержит метод с указанным именем, сигнатура которого соответствует сигнатуре класса делегата. `methodname` должен быть общим методом или методом экземпляра. `methodname` всегда является обязательным, даже если делегат создается для метода по умолчанию в классе.  
  
 Чтобы указать лямбда-выражение, используйте следующий синтаксис:  
  
 `Function` ([`parm` As `type`, `parm2` As `type2`, ...]) `expression`  
  
 Сигнатура функции должна соответствовать сигнатуре типа делегата. Дополнительные сведения о лямбда-выражениях см. в разделе [Лямбда-выражения](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md).  
  
 Дополнительные сведения о делегатах см. в разделе [делегаты](../../../visual-basic/programming-guide/language-features/delegates/index.md).  
  
## <a name="example"></a>Пример  
 В следующем примере используется `Delegate` инструкцию, чтобы объявить делегат для работы с двумя числами и возвращает число. `DelegateTest` Метод принимает экземпляр делегата этого типа и использует его для работы с парой чисел.  
  
 [!code-vb[VbVbalrDelegates#14](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/delegate-statement_1.vb)]  
  
## <a name="see-also"></a>См. также  
 [Оператор AddressOf](../../../visual-basic/language-reference/operators/addressof-operator.md)  
 [Of](../../../visual-basic/language-reference/statements/of-clause.md)  
 [Делегаты](../../../visual-basic/programming-guide/language-features/delegates/index.md)  
 [Практическое руководство. Использование универсального класса](../../../visual-basic/programming-guide/language-features/data-types/how-to-use-a-generic-class.md)  
 [Универсальные типы в Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)  
 [Ковариация и контрвариантность](../../programming-guide/concepts/covariance-contravariance/index.md)  
 [In](../../../visual-basic/language-reference/modifiers/in-generic-modifier.md)  
 [Out](../../../visual-basic/language-reference/modifiers/out-generic-modifier.md)
