---
title: Binding2
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 09511c6c-5749-4bb0-874e-0f0be36bfe04
caps.latest.revision: "8"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: f6553d1e1c030a30eed74ff81d3e07e28a9f25b7
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="binding"></a>Привязка
wmi Binding  
  
## <a name="syntax"></a>Синтаксис  
  
```  
class Binding  
{  
  BindingElement BindingElements[];  
  datetime CloseTimeout;  
  string Name;  
  string Namespace;  
  datetime OpenTimeout;  
  datetime ReceiveTimeout;  
  string Scheme;  
  datetime SendTimeout;  
};  
```  
  
## <a name="methods"></a>Методы  
 Класс Binding не определяет никаких методов.  
  
## <a name="properties"></a>Свойства  
 Класс Binding имеет следующие свойства.  
  
### <a name="bindingelements"></a>BindingElements  
 Тип данных: массив BindingElement  
  
 Тип доступа: только для чтения  
  
 Коллекция элементов привязки, реализованных привязкой.  
  
### <a name="closetimeout"></a>CloseTimeout  
 Тип данных: datetime  
  
 Тип доступа: только для чтения  
  
 Интервал времени, предусмотренный для завершения операции закрытия.  
  
### <a name="name"></a>name  
 Тип данных: string  
  
 Тип доступа: только для чтения  
  
 Имя привязки.  
  
### <a name="namespace"></a>Пространство имен  
 Тип данных: string  
  
 Тип доступа: только для чтения  
  
 Пространство имен XML привязки.  
  
### <a name="opentimeout"></a>OpenTimeout  
 Тип данных: datetime  
  
 Тип доступа: только для чтения  
  
 Интервал времени, предусмотренный для завершения операции открытия.  
  
### <a name="receivetimeout"></a>ReceiveTimeout  
 Тип данных: datetime  
  
 Тип доступа: только для чтения  
  
 Интервал времени, предусмотренный для завершения операции получения.  
  
### <a name="scheme"></a>Схема  
 Тип данных: string  
  
 Тип доступа: только для чтения  
  
 Схема транспорта универсальных кодов ресурсов (URI), которая используется производствами каналов и прослушивателей, созданными привязкой.  
  
### <a name="sendtimeout"></a>SendTimeout  
 Тип данных: datetime  
  
 Тип доступа: только для чтения  
  
 Интервал времени, предусмотренный для завершения операции отправки.  
  
## <a name="requirements"></a>Требования  
  
|MOF|Объявлено в файле Servicemodel.mof.|  
|---------|-----------------------------------|  
|Пространство имен|Определено в root\ServiceModel.|  
  
## <a name="see-also"></a>См. также  
 <xref:System.ServiceModel.Channels.Binding>
