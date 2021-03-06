---
title: "Транспорт интеграции с MSMQ"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2bf9893a-fbd1-41fc-b6de-a41a44279936
caps.latest.revision: "5"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 18dd1262c572a7e8844d9fe2beb5de7f52c28e1e
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="msmq-integration-transport"></a>Транспорт интеграции с MSMQ
В этом разделе перечислены все исключения, вызываемые транспортом интеграции MSMQ.  
  
## <a name="exception-list"></a>Список исключений  
  
|Код ресурса|Строка ресурса|  
|-------------------|---------------------|  
|MessageSizeMustBeInIntegerRange|Эта фабрика помещает сообщения в буфер, поэтому размер сообщений должен лежать в диапазоне целого числа.|  
|MsmqByteArrayBodyExpected|Обнаружено несоответствие между указанным форматом сериализации и телом MSMQ-сообщения. Невозможно отправить или получить сообщение. Формат сериализации ByteArray требует, чтобы тело MSMQ-сообщения имело тип byte[].|  
|MsmqCannotDeserializeActiveXMessage|Произошла ошибка сериализации ActiveX. Невозможно отправить или получить сообщение. Указанный тип variant тела не соответствует фактическому телу MSMQ-сообщения.|  
|MsmqCannotUseBodyTypeWithActiveXSerialization|Обнаружено несоответствие свойств сообщения. Невозможно отправить или получить сообщение. Задать свойство сообщения BodyType невозможно, если используется формат сериализации ActiveX.|  
|MsmqInvalidServiceOperationForMsmqIntegrationBinding|Сбой при проверке MsmqIntegrationBinding. Запуск конечной точки службы невозможен. Указанная привязка не поддерживает сигнатуру метода для указанной операции службы в указанном контракте. Исправьте операцию службы, чтобы она использовала MsmqIntegrationBinding.|  
|MsmqInvalidTypeDeserialization|При сериализации ActiveX произошел сбой, так как не распознан формат сериализации. Невозможно отправить или получить сообщение.|  
|MsmqInvalidTypeSerialization|Тип variant не распознан. При сериализации ActiveX произошел сбой. Невозможно отправить или получить сообщение. Указанный тип variant не поддерживается.|  
|MsmqStreamBodyExpected|Обнаружено несоответствие между форматом сериализации и содержимым тела. Невозможно отправить или получить сообщение. В режиме сериализации потока можно отправлять или получать только тела типа stream.|
