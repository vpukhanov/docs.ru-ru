---
title: "Функция BlessIWbemServices (Справочник по неуправляемым API)"
description: "Функция BlessIWbemServices указывает ли учетные данные разрешают доступ к классу IWbemServices."
ms.date: 11/06/2017
ms.prod: .net-framework
ms.technology:
- dotnet-clr
ms.topic: reference
api_name:
- BlessIWbemServices
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- BlessIWbemServices
helpviewer_keywords:
- BlessIWbemServices function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: f384e8d045dd7a6f2f864f0991f8caf4a674408b
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="blessiwbemservices-function"></a>Функция BlessIWbemServices
Указывает, разрешить ли учетные данные пользователя доступ к указанным [IWbemServices](https://msdn.microsoft.com/library/aa392093(v=vs.85).aspx) класса.   
  
[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>Синтаксис  
  
```  
HRESULT BlessIWbemServices (
   [in] IWbemServices* pIWbemServices,
   [in] BSTR strUser, 
   [in] BSTR strPassword, 
   [in] BSTR strAuthority, 
   [in] DWORD impLevel, 
   [in] DWORD authnLevel
);
```  

## <a name="parameters"></a>Параметры

`pIWbemServices`  
[in] Указатель на [IWbemServices](https://msdn.microsoft.com/library/aa392093(v=vs.85).aspx) объекта, для которого требуются разрешения.

`strUser`  
[in] Имя пользователя.

`strPassword`  
[in] Пароль, связанный с `strUser`.

`strAuthority`[in] Имя домена пользователя. В разделе [ConnectServerWmi](connectserverwmi.md) функции для получения дополнительной информации.

`impLevel`[in] Уровень олицетворения.

`authnLevel`[in] Уровень авторизации.

## <a name="return-value"></a>Возвращаемое значение

Следующие значения, возвращаемые этой функцией, определяются в *WinError.h* заголовочный файл, или их можно определить как константы в коде:

|Константа  |Значение  |Описание:  |
|---------|---------|---------|
| `E_INVALIDARG` | 0x80070057 | Один или несколько аргументов являются недопустимыми. |
| `E_POINTER` | отметкой 0x80004003 | Свойство `pIWbemServices` имеет значение `null`. | 
| `E_FAIL` | 0x80000008 | Произошла неизвестная ошибка. |
| `E_OUTOFMEMORY` | 0x80000002 | Недостаточно памяти для выполнения операции. | 
| `S_OK` | 0 | Успешный вызов функции. | 

## <a name="requirements"></a>Требования  
 **Платформы:** разделе [требования к системе для](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок:** WMINet_Utils.idl  
  
 **Версии платформы .NET framework:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>См. также  
[WMI и счетчиков производительности (Справочник по неуправляемым API)](index.md)
