---
title: Интерфейсы (Руководство по программированию в C#)
ms.date: 07/20/2015
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
helpviewer_keywords:
- interfaces [C#]
- C# language, interfaces
ms.assetid: 2feda177-ce11-432d-81b4-d50f5f35fd37
caps.latest.revision: 45
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: f14d4bf48d117558a4019a8f016e194af27a9ebf
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="interfaces-c-programming-guide"></a>Интерфейсы (Руководство по программированию в C#)
Интерфейс содержит определения для группы связанных функциональных возможностей, которые может реализовать [класс](../../../csharp/language-reference/keywords/class.md) или [структура](../../../csharp/language-reference/keywords/struct.md).  
  
 С помощью интерфейсов можно, например, включить в класс поведение из нескольких источников. Эта возможность очень важна в C#, поскольку этот язык не поддерживает множественное наследование классов. Кроме того, необходимо использовать интерфейс, если требуется имитировать наследование для структур, поскольку они не могут фактически наследовать от другой структуры или класса.  
  
 Интерфейс определяется с помощью ключевого слова [interface](../../../csharp/language-reference/keywords/interface.md), как показано в следующем примере.  
  
 [!code-csharp[csProgGuideInheritance#47](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/interfaces_1.cs)]  
  
 Любой объект (класс или структура), реализующий интерфейс <xref:System.IEquatable%601>, должен содержать определение для метода <xref:System.IEquatable%601.Equals%2A>, соответствующее сигнатуре, которую задает интерфейс. В результате вы можете быть уверены, что класс, реализующий `IEquatable<T>`, содержит метод `Equals`, с помощью которого экземпляр этого класса может определить, равен ли он другому экземпляру того же класса.  
  
 Определение `IEquatable<T>` не предоставляет реализацию для метода `Equals`. Интерфейс определяет только сигнатуру. Таким образом, интерфейс в C# аналогичен абстрактному классу, в котором все методы являются абстрактными. Класс или структура может реализовывать несколько интерфейсов, но класс может наследовать только одному классу, абстрактному или нет. Таким образом, с помощью интерфейсов можно включить в класс поведение из нескольких источников.  
  
 Дополнительные сведения об абстрактных классах см. в статье [Abstract and Sealed Classes and Class Members](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md) (Абстрактные и запечатанные классы и члены классов).  
  
 Интерфейсы могут содержать методы, свойства, события, индексаторы, а также любое сочетание этих четырех типов членов. Ссылки на примеры см. в разделе [Связанные разделы](../../../csharp/programming-guide/interfaces/index.md#BKMK_RelatedSections). Интерфейс не может содержать константы, поля, операторы, конструкторы экземпляров, методы завершения или типы. Члены интерфейса автоматически являются открытыми, и они не могут включать модификаторы доступа. Члены также не могут быть [статическими](../../../csharp/language-reference/keywords/static.md).  
  
 Для реализации члена интерфейса соответствующий член реализующего класса должен быть открытым и не статическим, а также иметь такое же имя и сигнатуру, что и член интерфейса.  
  
 Если класс (или структура) реализует интерфейс, этот класс (или структура) должен предоставлять реализацию для всех членов, которые определяет этот интерфейс. Сам интерфейс не предоставляет функциональность, которую класс или структура может наследовать таким же образом, как можно наследовать функциональность базового класса. Однако если базовый класс реализует интерфейс, то любой класс, производный от базового класса, наследует эту реализацию.  
  
 В следующем примере показана реализация интерфейса IEquatable<T\>. Реализующий класс `Car` должен предоставлять реализацию метода <xref:System.IEquatable%601.Equals%2A>.  
  
 [!code-csharp[csProgGuideInheritance#48](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/interfaces_2.cs)]  
  
 Свойства и индексаторы класса могут определять дополнительные методы доступа для свойства или индексатора, определенного в интерфейсе. Например, интерфейс может объявлять свойство, имеющее акцессор [get](../../../csharp/language-reference/keywords/get.md). Класс, реализующий этот интерфейс, может объявлять это же свойство с обоими акцессорами (`get` и [set](../../../csharp/language-reference/keywords/set.md)). Однако если свойство или индексатор использует явную реализацию, методы доступа должны совпадать. Дополнительные сведения о явной реализации см. в статьях [Явная реализация интерфейса](../../../csharp/programming-guide/interfaces/explicit-interface-implementation.md) и [Свойства интерфейса](../../../csharp/programming-guide/classes-and-structs/interface-properties.md).  
  
 Интерфейсы могут реализовывать другие интерфейсы. Класс может включать интерфейс несколько раз через базовые классы, которым он наследует, или через интерфейсы, которые реализуют другие интерфейсы. Однако класс может предоставить реализацию интерфейса только однократно и только если класс объявляет интерфейс как часть определения класса (`class ClassName : InterfaceName`). Если интерфейс наследуется, поскольку наследуется базовый класс, реализующий этот интерфейс, то базовый класс предоставляет реализацию членов этого интерфейса. Однако производный класс может повторно реализовать члены интерфейса вместо использования унаследованной реализации.  
  
 Базовый класс также может реализовывать члены интерфейса с помощью виртуальных членов. В таком случае производный класс может изменять поведение интерфейса путем переопределения виртуальных членов. Дополнительные сведения о виртуальных членах см. в статье [Полиморфизм](../../../csharp/programming-guide/classes-and-structs/polymorphism.md).  
  
## <a name="interfaces-summary"></a>Сводные сведения по интерфейсам  
 Интерфейс имеет следующие свойства.  
  
-   Интерфейс подобен абстрактному базовому классу. Любой класс (или структура), реализующий интерфейс, должен реализовывать все его члены.  
  
-   Невозможно создать экземпляр интерфейса напрямую. Его члены реализуются любым классом (или структурой), реализующим интерфейс.  
  
-   Интерфейсы могут содержать события, индексаторы, методы и свойства.  
  
-   Интерфейсы не содержат реализацию методов.  
  
-   Класс или структура может реализовывать несколько интерфейсов. Класс может наследовать базовому классу и также реализовывать один или несколько интерфейсов.  
  
## <a name="in-this-section"></a>Содержание  
 [Явная реализация интерфейса](../../../csharp/programming-guide/interfaces/explicit-interface-implementation.md)  
 В этом разделе объясняется, как создать член класса, который относится к интерфейсу.  
  
 [Практическое руководство. Явная реализация членов интерфейса](../../../csharp/programming-guide/interfaces/how-to-explicitly-implement-interface-members.md)  
 В этом разделе содержится пример явной реализации членов интерфейсов.  
  
 [Практическое руководство. Явная реализация членов двух интерфейсов](../../../csharp/programming-guide/interfaces/how-to-explicitly-implement-members-of-two-interfaces.md)  
 В этом разделе содержится пример явной реализации членов интерфейсов с помощью наследования.  
  
##  <a name="BKMK_RelatedSections"></a> Связанные разделы  
  
-   [Свойства интерфейса](../../../csharp/programming-guide/classes-and-structs/interface-properties.md)  
  
-   [Индексаторы в интерфейсах](../../../csharp/programming-guide/indexers/indexers-in-interfaces.md)  
  
-   [Практическое руководство. Реализация событий интерфейса](../../../csharp/programming-guide/events/how-to-implement-interface-events.md)  
  
-   [Классы и структуры](../../../csharp/programming-guide/classes-and-structs/index.md)  
  
-   [Наследование](../../../csharp/programming-guide/classes-and-structs/inheritance.md)  
  
-   [Методы](../../../csharp/programming-guide/classes-and-structs/methods.md)  
  
-   [Полиморфизм](../../../csharp/programming-guide/classes-and-structs/polymorphism.md)  
  
-   [Абстрактные и запечатанные классы и члены классов](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md)  
  
-   [Свойства](../../../csharp/programming-guide/classes-and-structs/properties.md)  
  
-   [События](../../../csharp/programming-guide/events/index.md)  
  
-   [Индексаторы](../../../csharp/programming-guide/indexers/index.md)  
  
## <a name="featured-book-chapter"></a>Важная глава книги  
 Глава [Интерфейсы](http://msdn.microsoft.com/library/orm-9780596521066-01-13.aspx) в документе [Изучение C# 3.0: овладение основными понятиями C# 3.0](http://msdn.microsoft.com/library/orm-9780596521066-01.aspx)  
  
## <a name="see-also"></a>См. также  
 [Руководство по программированию на C#](../../../csharp/programming-guide/index.md)  
 [Наследование](../../../csharp/programming-guide/classes-and-structs/inheritance.md)
