---
title: "Удаление содержимого узла в DOM"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 615d81a7-f44f-416c-a9ab-bfe03f85e6e4
caps.latest.revision: 
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 45a8d5006599b23165a174770f4d72974ea0e5ec
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/23/2017
---
# <a name="removing-node-content-in-the-dom"></a>Удаление содержимого узла в DOM
Для типов узлов, наследующих от <xref:System.Xml.XmlCharacterData>, являющихся типами узлов <xref:System.Xml.XmlComment>,<xref:System.Xml.XmlText>,<xref:System.Xml.XmlCDataSection>,<xref:System.Xml.XmlWhitespace> и <xref:System.Xml.XmlSignificantWhitespace>, можно удалить символы с помощью метода <xref:System.Xml.XmlCharacterData.DeleteData%2A>, который удаляет диапазон символов из узла. Если требуется полностью удалить содержимое, нужно удалить узел, содержащий содержимое. Если требуется сохранить узел, содержимое которого неверно, нужно изменить содержимое. См. дополнительные сведения об [изменении узлов, содержимого и значений в документе XML](../../../../docs/standard/data/xml/modifying-nodes-content-and-values-in-an-xml-document.md).  
  
## <a name="see-also"></a>См. также  
 [Модель объектов документов XML (DOM)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)
