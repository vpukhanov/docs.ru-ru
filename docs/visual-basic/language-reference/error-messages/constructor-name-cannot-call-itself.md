---
title: Конструктор &#39; &lt;имя&gt;&#39; может вызывать сам себя
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc30298
- vbc30298
helpviewer_keywords:
- BC30298
ms.assetid: 2d77b7f4-0640-4f89-9c65-f101fd2847c0
caps.latest.revision: 8
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 2361d6f4d710e17a4f4e29ac03bfde523191fa83
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/18/2017
---
# <a name="constructor-39ltnamegt39-cannot-call-itself"></a>Конструктор &#39; &lt;имя&gt;&#39; может вызывать сам себя
Объект `Sub New` процедура в классе или структуре вызывает саму себя.  
  
 Конструктор предназначен для инициализации нового экземпляра класса или структуры сразу после создания. Класс или структура может иметь несколько конструкторов, если все они имеют разные списки параметров. Конструктор может вызвать другой конструктор для использования его функциональных возможностей в дополнение к своему собственному. Но не имеет смысла для конструктора вызывать самого себя, а на самом деле это приведет к бесконечной рекурсии Если это разрешено.  
  
 **Идентификатор ошибки:** BC30298  
  
## <a name="to-correct-this-error"></a>Исправление ошибки  
  
1.  Проверьте список параметров вызываемого конструктора. Она должна отличаться от вызова конструктора.  
  
2.  Если не требуется вызывать другой конструктор, удалите `Sub New` вызова полностью.  
  
## <a name="see-also"></a>См. также  
 [Время существования. Создание и уничтожение объектов](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md)
