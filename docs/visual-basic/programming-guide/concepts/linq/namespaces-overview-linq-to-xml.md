---
title: "Обзор пространств имен (LINQ to XML)"
ms.custom: 
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b8eb31fa-4b26-4acf-8050-6e705687f458
caps.latest.revision: "3"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 082172720abd39634f7183367d4d7b8d53d2bb7e
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/18/2017
---
# <a name="namespaces-overview-linq-to-xml"></a>Обзор пространств имен (LINQ to XML)
Этот раздел знакомит с пространствами имен, классом <xref:System.Xml.Linq.XName> и классом <xref:System.Xml.Linq.XNamespace>.  
  
## <a name="xml-names"></a>Имена XML  
 Имена XML часто становятся источником сложности при программировании на XML. Имя XML состоит из пространства имен XML (которое также называется URI-кодом пространства имен XML) и локального имени. Пространство имен XML аналогично пространству имен в программах на основе [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)]. Позволяет уникально квалифицировать имена элементов и атрибутов. Это помогает избежать конфликтов имен в разных частях XML-документа. При задании пространства имен XML можно выбрать локальное имя, которое должно быть уникальным только по значению пространства имен.  
  
 Другим аспектом имен XML являются *префиксы пространств имен* XML. Именно префиксы создают основную сложность в работе с именами XML. Эти префиксы позволяют создавать ярлык пространства имен XML, что делает XML-документ более организованным и понятным. Однако, чтобы префиксы XML несли значение, необходимо, чтобы они были соотнесены с определенным контекстом, а это вносит дополнительную сложность. Например, префикс XML `aw` можно ассоциировать с одним пространством имен XML в одной части XML-дерева и с другим пространством имен XML в другой его части.  
  
 При использовании [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] с Visual Basic и XML-литералы, необходимо использовать префиксы пространства имен при работе с документами в пространствах имен.  
  
 В [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] следующий класс представляет имена XML: <xref:System.Xml.Linq.XName>. Имена XML часто появляются в API [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)], и, когда требуется использовать имя XML, обнаруживается параметр <xref:System.Xml.Linq.XName>. Однако напрямую работать с <xref:System.Xml.Linq.XName> приходится редко. <xref:System.Xml.Linq.XName> содержит неявное преобразование строки.  
  
 Дополнительные сведения см. в разделах <xref:System.Xml.Linq.XNamespace> и <xref:System.Xml.Linq.XName>.  
  
## <a name="see-also"></a>См. также  
 [Работа с пространствами имен XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/working-with-xml-namespaces.md)
