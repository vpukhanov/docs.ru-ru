---
title: Пространства имен в Visual Basic
ms.custom: ''
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.global
helpviewer_keywords:
- assemblies [Visual Basic], namespaces
- name collisions
- Global keyword [Visual Basic]
- namespace pollution
- names [Visual Basic], avoiding conflicts
- naming conflicts [Visual Basic], namespaces
- namespaces [Visual Basic], assemblies
- Visual Basic code, namespaces
- fully qualified names [Visual Basic]
- naming conventions [Visual Basic], naming conflicts
- namespaces
ms.assetid: cffac744-ab8c-4f1f-ba50-732c22ab4b88
caps.latest.revision: 27
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: c18d0a9abb1d8b9e3e22f3b81bf605fb8ed75cfa
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="namespaces-in-visual-basic"></a>Пространства имен в Visual Basic
Пространства имен упорядочивают объекты, определенные в сборке. Сборки могут содержать несколько пространств имен, которые, в свою очередь, могут содержать другие пространства имен. Пространства имен предотвращают неоднозначность и упрощают ссылки при использовании больших групп объектов, таких как библиотеки классов.  
  
 Например, [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] определяет класс <xref:System.Windows.Forms.ListBox> в пространстве имен <xref:System.Windows.Forms?displayProperty=nameWithType>. В следующем фрагменте кода показано, как объявить переменную, используя полное имя для этого класса:  
  
 [!code-vb[VbVbalrApplication#6](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/namespaces_1.vb)]  
  
## <a name="avoiding-name-collisions"></a>Предотвращение конфликтов имен  
 Пространства имен[!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] помогают решить проблему, которую иногда называют *загрязнением пространства имен*, при которой у разработчика библиотеки классов возникают трудности, связанные с использованием аналогичных имен в другой библиотеке. Такие конфликты с существующими компонентами иногда называют *конфликтами имен*.  
  
 Например, если вы создаете новый класс `ListBox`, то можете использовать его внутри проекта без уточнения. Однако если вы захотите использовать в том же проекте класс [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] <xref:System.Windows.Forms.ListBox> , потребуется использовать полную ссылку, чтобы сделать ссылку уникальной. Если эта ссылка не является уникальной, [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] выдает сообщение об ошибке, уведомляющее о неоднозначности имени. В примере кода ниже показано, как объявить эти объекты:  
  
 [!code-vb[VbVbalrApplication#7](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/namespaces_2.vb)]  
  
 На следующем рисунке показаны две иерархии пространств имен, в каждой из которых присутствует объект `ListBox`.  
  
 ![Иерархия пространства имен](../../../visual-basic/programming-guide/program-structure/media/vanamespacehierarchy.gif "vaNamespaceHierarchy")  
  
 По умолчанию каждый исполняемый файл, созданный с помощью [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] , содержит пространство имен с таким же именем, как и у проекта. Например, если вы определяете объект в проекте `ListBoxProject`, то исполняемый файл ListBoxProject.exe содержит пространство имен `ListBoxProject`.  
  
 Несколько сборок могут использовать одно и то же пространство имен. [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] обрабатывает их как единый набор имен. Например, можно определить классы для пространства имен `SomeNameSpace` в сборке `Assemb1`, а также определить дополнительные классы для того же пространства имен из сборки `Assemb2`.  
  
## <a name="fully-qualified-names"></a>полные имена  
 Полные имена — это ссылки на объекты, имеющие префикс в виде имени пространства имен, в котором определен объект. Вы можете использовать объекты, определенные в других проектах, если создадите ссылку на класс (выбрав **Добавить ссылку** в меню **Проект** ) и затем используете полное имя объекта в коде. В следующем фрагменте кода показано, как использовать полное имя объекта из пространства имен другого проекта:  
  
 [!code-vb[VbVbalrApplication#8](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/namespaces_3.vb)]  
  
 Полные имена предотвращают возникновение конфликтов имен, так как позволяют компилятору определить, какой именно объект используется. Однако сами эти имена могут получиться длинными и громоздкими. Чтобы обойти эту проблему, можно использовать оператор `Imports` для определения *псевдонима*— сокращенного имени, которое можно применить вместо полного имени. Например, в следующем примере кода создаются псевдонимы для двух полных имен, которые затем используются для определения двух объектов.  
  
 [!code-vb[VbVbalrApplication#9](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/namespaces_4.vb)]  
  
 [!code-vb[VbVbalrApplication#10](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/namespaces_5.vb)]  
  
 Если вы применяете оператор `Imports` без псевдонима, можно использовать все имена в данном пространстве имен без уточнения при условии, что они являются уникальными в данном проекте. Если проект содержит операторы `Imports` для пространств имен, где есть элементы с одинаковым именем, необходимо полностью уточнять это имя. Предположим, что проект содержал два следующих оператора `Imports` :  
  
 [!code-vb[VbVbalrApplication#11](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/namespaces_6.vb)]  
  
 При попытке использовать `Class1` без полного уточнения [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] выдает сообщение об ошибке, указывающее, что имя `Class1` является неоднозначным.  
  
## <a name="namespace-level-statements"></a>Операторы уровня пространства имен  
 В пространстве имен можно определить такие элементы, как модули, интерфейсы, классы, делегаты, перечисления, структуры и другие пространства имен. Вы не можете определить такие элементы, как свойства, процедуры, переменные и события, на уровне пространства имен. Их следует объявить внутри контейнеров, таких как модули, структуры или классы.  
  
## <a name="global-keyword-in-fully-qualified-names"></a>Ключевое слово Global в полных именах  
 Если вы определили вложенную иерархию пространств имен, доступ кода внутри этой иерархии к пространству имен <xref:System?displayProperty=nameWithType> платформы .NET Framework может быть заблокирован. В следующем примере показана иерархия, где пространство имен `SpecialSpace.System` блокирует доступ к <xref:System?displayProperty=nameWithType>.  
  
```vb  
Namespace SpecialSpace  
    Namespace System  
        Class abc  
            Function getValue() As System.Int32  
                Dim n As System.Int32  
                Return n  
            End Function  
        End Class  
    End Namespace  
End Namespace  
```  
  
 В результате компилятору Visual Basic не удается разрешить успешно ссылку в <xref:System.Int32?displayProperty=nameWithType>, так как `SpecialSpace.System` не определяет `Int32`. Можно использовать ключевое слово `Global` для запуска цепочки квалификации на самом внешнем уровне библиотеки классов .NET Framework. Это позволяет указать пространство имен <xref:System?displayProperty=nameWithType> или любое другое пространство имен в библиотеке классов. Это показано в следующем примере.  
  
```vb  
Namespace SpecialSpace  
    Namespace System  
        Class abc  
            Function getValue() As Global.System.Int32  
                Dim n As Global.System.Int32  
                Return n  
            End Function  
        End Class  
    End Namespace  
End Namespace  
```  
  
 Можно использовать `Global` для доступа к другим пространствам имен корневого уровня, таким как <xref:Microsoft.VisualBasic?displayProperty=nameWithType>, и любому пространству имен, сопоставленному с проектом.  
  
## <a name="global-keyword-in-namespace-statements"></a>Ключевое слово Global в операторах пространства имен  
 Можно также использовать ключевое слово `Global` в [Namespace Statement](../../../visual-basic/language-reference/statements/namespace-statement.md). Это позволяет определить пространство имен из корневых пространств имен проекта.  
  
 Все пространства имен в проекте основаны на его корневом пространстве имен.  Visual Studio назначает имя проекта в качестве корневого пространства имен по умолчанию для всего кода в проекте. Например, если проект называется `ConsoleApplication1`, его программные элементы относятся к пространству имен `ConsoleApplication1`. При объявлении `Namespace Magnetosphere`ссылки на `Magnetosphere` в проекте будут обращаться к `ConsoleApplication1.Magnetosphere`.  
  
 В следующих примерах используется ключевое слово `Global` для объявления пространства имен из корневого пространства имен для проекта.  
  
 [!code-vb[VbVbalrApplication#22](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/namespaces_7.vb)]  
  
 В объявлении пространства имен `Global` не может быть вложенным в другое пространство имен.  
  
 Можно использовать [страница "приложение" в конструкторе проектов (Visual Basic)](/visualstudio/ide/reference/application-page-project-designer-visual-basic) для просмотра и изменения **корневое пространство имен** проекта.  Для новых проектов параметру **Корневое пространство имен** по умолчанию присваивается имя проекта. Чтобы сделать `Global` пространством имен верхнего уровня, можно очистить запись **Корневое пространство имен** , оставив поле пустым. Очистка значения **Корневое пространство имен** избавляет от необходимости использовать ключевое слово `Global` в объявлениях пространств имен.  
  
 Когда оператор `Namespace` объявляет имя, которое также является пространством имен в платформе .NET Framework, пространство имен .NET Framework станет недоступным, если в полном имени не используется ключевое слово `Global` . Для обеспечения доступа к пространству имен .NET Framework без использования ключевого слова `Global` можно включить ключевое слово `Global` в оператор `Namespace` .  
  
 В следующем примере ключевое слово `Global` присутствует в объявлении пространства имен `System.Text` .  
  
 Если ключевое слово `Global` отсутствует в объявлении пространства имен, к <xref:System.Text.StringBuilder> нельзя обратиться без указания `Global.System.Text.StringBuilder`. Если ключевое слово `ConsoleApplication1`не использовалось, для проекта с именем `System.Text` ссылки на `ConsoleApplication1.System.Text` обращаются к `Global` .  
  
 [!code-vb[VbVbalrApplication#21](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/namespaces_8.vb)]  
  
## <a name="see-also"></a>См. также  
 <xref:System.Windows.Forms.ListBox>  
 <xref:System.Windows.Forms?displayProperty=nameWithType>  
 [Сборки и глобальный кэш сборок](../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)  
 [Практическое руководство. Создание и использование сборок с помощью командной строки](http://msdn.microsoft.com/library/70f65026-3687-4e9c-ab79-c18b97dd8be4)  
 [Ссылки и оператор Imports](../../../visual-basic/programming-guide/program-structure/references-and-the-imports-statement.md)  
 [Оператор Imports (пространство имен и тип .NET)](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)  
 [Написание кода в решениях Office](https://msdn.microsoft.com/library/bb608596)
