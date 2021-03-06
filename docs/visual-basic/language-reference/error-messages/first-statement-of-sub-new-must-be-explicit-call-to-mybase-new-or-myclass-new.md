---
title: 'Первый оператор в это &#39; Конструктор Sub New &#39; должен быть явным вызовом &#39; MyBase.New &#39; или &#39; MyClass.New &#39; так как &#39; &lt;имя_конструктора&gt;&#39; в базовом классе &#39;&lt; имя_базового_класса&gt;&#39; &#39;&lt; имя_производного_класса&gt;&#39; помечен как устаревший: &#39;&lt; сообщение об ошибке&gt;&#39;'
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc30920
- bc30920
helpviewer_keywords:
- BC30920
ms.assetid: e47dc755-4294-4368-b813-2177b7677957
caps.latest.revision: 10
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 8882acd947251d85804fbefd54267ce078e31b95
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/18/2017
---
# <a name="first-statement-of-this-39sub-new39-must-be-an-explicit-call-to-39mybasenew39-or-39myclassnew39-because-the-39ltconstructornamegt39-in-the-base-class-39ltbaseclassnamegt39-of-39ltderivedclassnamegt39-is-marked-obsolete-39lterrormessagegt39"></a>Первый оператор в это &#39; Конструктор Sub New &#39; должен быть явным вызовом &#39; MyBase.New &#39; или &#39; MyClass.New &#39; так как &#39; &lt;имя_конструктора&gt;&#39; в базовом классе &#39;&lt; имя_базового_класса&gt;&#39; &#39;&lt; имя_производного_класса&gt;&#39; помечен как устаревший: &#39;&lt; сообщение об ошибке&gt;&#39;
Конструктор класса не вызывает явно конструктор базового класса, а вызванный неявно конструктор базового класса помечается атрибутом <xref:System.ObsoleteAttribute> , что является причиной возникновения ошибки.  
  
 Если конструктор производного класса не вызывает конструктор базового класса, [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] пытается создать неявный вызов конструктора базового класса без параметров. Если в базовом классе нет доступного конструктора, который можно вызывать без аргументов, [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] не удается создать неявный вызов. В этом случае необходимый конструктор помечается атрибутом <xref:System.ObsoleteAttribute> , и поэтому [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] не может вызвать его.  
  
 Вы можете пометить любой программный элемент как неиспользуемый, применив к нему атрибут <xref:System.ObsoleteAttribute> . Если вы это сделаете, вы можете задать для свойства <xref:System.ObsoleteAttribute.IsError%2A> атрибута значение `True` или `False`. Если задать значение `True`, компилятор будет рассматривать попытку использовать элемент как ошибку. Если задать значение `False`или оставить значение по умолчанию `False`, то при попытке использовать элемент компилятор выдаст предупреждение.  
  
 **Идентификатор ошибки:** BC30920  
  
## <a name="to-correct-this-error"></a>Исправление ошибки  
  
1.  Проверьте указанное сообщение об ошибке и выполните соответствующее действие.  
  
2.  Включите вызов `MyBase.New()` или `MyClass.New()` в качестве первого оператора `Sub New` в производном классе.  
  
## <a name="see-also"></a>См. также  
 [Обзор атрибутов](../../../visual-basic/programming-guide/concepts/attributes/index.md)
 
