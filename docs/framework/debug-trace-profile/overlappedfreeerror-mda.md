---
title: "Помощник по отладке управляемого кода overlappedFreeError"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OverlappedFreeError MDA
- overlapped free method call error
- managed debugging assistants (MDAs), overlapped structures
- overlapped structures
- MDAs (managed debugging assistants), overlapped structures
- freeing overlapped structures
ms.assetid: b6ab2d48-6eee-4bab-97a3-046b3b0a5470
caps.latest.revision: "8"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 4e17e9d6a93b69d358e89109cf965b7b9856c325
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="overlappedfreeerror-mda"></a>Помощник по отладке управляемого кода overlappedFreeError
Помощник по отладке управляемого кода `overlappedFreeError` (MDA) активируется, если метод <xref:System.Threading.Overlapped.Free%28System.Threading.NativeOverlapped%2A%29?displayProperty=nameWithType> вызывается до завершения перекрывающейся операции.  
  
## <a name="symptoms"></a>Признаки  
 Нарушение прав доступа или повреждение кучи сбора мусора.  
  
## <a name="cause"></a>Причина  
 Перекрывающаяся структура была освобождена до завершения операции. Функция, использующая перекрывающийся указатель, может выполнять запись в структуру позднее, после ее освобождения. Это может привести к повреждению кучи, поскольку требуемая область может быть занята другим объектом.  
  
 Этот помощник по отладке управляемого кода может не возвращать ошибку, если перекрывающаяся операция не была успешно запущена.  
  
## <a name="resolution"></a>Решение  
 Прежде чем вызывать метод <xref:System.Threading.Overlapped.Free%28System.Threading.NativeOverlapped%2A%29>, убедитесь, что операция ввода-вывода, использующая перекрывающуюся структуру, была завершена.  
  
## <a name="effect-on-the-runtime"></a>Влияние на среду выполнения  
 Этот помощник отладки управляемого кода не оказывает никакого влияния на среду CLR.  
  
## <a name="output"></a>Вывод  
 Ниже приведен пример выходных данных для этого помощника по отладке управляемого кода.  
  
 `An overlapped pointer (0x00ea3430) that was not allocated on the GC heap was passed via Pinvoke to the win32 function 'WriteFile' in module 'KERNEL32.DLL'. If the AppDomain is shut down, this can cause heap corruption when the async I/O completes. The best solution is to pass a NativeOverlappedStructure retrieved from a call to System.Threading.Overlapped.Pack(). If the AppDomain exits, the CLR will keep this structure alive and pinned until the I/O completes.`  
  
## <a name="configuration"></a>Конфигурация  
  
```xml  
<mdaConfig>  
  <assistants>  
    <overlappedFreeError/>  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>См. также  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>  
 [Диагностика ошибок посредством помощников по отладке управляемого кода](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)  
 [Маршалинг взаимодействия](../../../docs/framework/interop/interop-marshaling.md)
