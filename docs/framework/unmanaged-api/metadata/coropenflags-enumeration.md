---
title: "Перечисление CorOpenFlags"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name:
- CorOpenFlags
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorOpenFlags
helpviewer_keywords:
- CorOpenFlags enumeration [.NET Framework metadata]
ms.assetid: e27a83b5-2698-4996-9032-1e0fed8b91ca
topic_type:
- apiref
caps.latest.revision: 
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 4447f648277576169c9004d1880283728639c8f3
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/19/2018
---
# <a name="coropenflags-enumeration"></a>Перечисление CorOpenFlags
Содержит значения флага, которые управляют поведением метаданных при открытии файлов манифеста.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
typedef enum CorOpenFlags  
{  
    ofRead              =   0x00000000,  
    ofWrite             =   0x00000001,  
    ofReadWriteMask     =   0x00000001,  
    ofCopyMemory        =   0x00000002,  
    ofCacheImage        =   0x00000004,  
    ofManifestMetadata  =   0x00000008,  
    ofReadOnly          =   0x00000010,  
    ofTakeOwnership     =   0x00000020,  
    ofCacheImage        =   0x00000004,  
    ofNoTypeLib         =   0x00000080,  
    ofNoTransform       =   0x00001000,  
    ofReserved1         =   0x00000100,  
    ofReserved2         =   0x00000200,  
    ofReserved          =   0xffffff40  
} CorOpenFlags;  
```  
  
## <a name="members"></a>Участники  
  
|Член|Описание|  
|------------|-----------------|  
|`ofRead`|Указывает, что файл следует открывать только для чтения.|  
|`ofWrite`|Указывает, что файл следует открывать для записи.<br /><br /> При использовании флага `ofWrite` во время открытия файла .WINMD также следует передавать флаг `ofNoTransform`.|  
|`ofReadWriteMask`|Маска для чтения и записи.|  
|`ofCopyMemory`|Указывает, что файл следует считывать в память. Метаданным следует создавать свою собственную копию.|  
|`ofCacheImage`|Является устаревшей. Этот флаг отклонен.|  
|`ofManifestMetadata`|Является устаревшей. Этот флаг отклонен.|  
|`ofReadOnly`|Указывает, что файл должен быть открыт для чтения, а вызов `QueryInterface` для [IMetaDataEmit](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md) нельзя сделать.|  
|`ofTakeOwnership`|Указывает, что память была выделена с помощью вызова [CoTaskMemAlloc](http://msdn.microsoft.com/library/c4cb588d-9482-4f90-a92e-75b604540d5c) и будет освобождена метаданными.|  
|`ofNoTypeLib`|Является устаревшей. Этот флаг отклонен.|  
|`ofNoTransform`|Указывает, что автоматические преобразования из файла .WINMD следует отключить. Другими словами, проекцию типа среды выполнения Windows на тип платформы .NET Framework следует отключить. Дополнительные сведения см. в разделе [под изнутри .NET и среды выполнения Windows](http://msdn.microsoft.com/magazine/jj651569.aspx).|  
|`ofReserved1`|Зарезервировано для внутреннего использования.|  
|`ofReserved2`|Зарезервировано для внутреннего использования.|  
|`ofReserved`|Зарезервировано для внутреннего использования.|  
  
## <a name="requirements"></a>Требования  
 **Платформы:** разделе [требования к системе для](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок:** CorHdr.h  
  
 **Версии платформы .NET framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>См. также  
 [Перечисления метаданных](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
