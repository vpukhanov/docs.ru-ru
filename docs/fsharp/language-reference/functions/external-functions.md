---
title: "Внешние функции (F#)"
description: "Дополнительные сведения о поддержке языка F # для вызова функции в машинный код."
keywords: "visual f#, f#, функциональное программирование"
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: c26b6124-ceaa-471c-9dc9-861b4dfa332a
ms.openlocfilehash: 69b73983a91bc6c7cc38fa34484a3c89fc01858f
ms.sourcegitcommit: 685143b62385500f59bc36274b8adb191f573a16
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/09/2017
---
# <a name="external-functions"></a>Внешние функции

В этом разделе описывается поддержка языка F # для вызова функции в машинный код.

## <a name="syntax"></a>Синтаксис

```fsharp
[<DllImport( arguments )>]
extern declaration
```

## <a name="remarks"></a>Примечания

В предыдущем синтаксисе *аргументы* представляет аргументы, передаваемые `System.Runtime.InteropServices.DllImportAttribute` атрибута. Первым аргументом является строка, представляющая имя библиотеки DLL, содержащей эту функцию без расширения DLL. Дополнительные аргументы, которые можно указать для любого из открытых свойств объекта `System.Runtime.InteropServices.DllImportAttribute` класса, например, соглашение о вызовах.

Предположим, что у вас есть собственный библиотеки DLL C++, содержащий следующую экспортированную функцию.

```cpp
#include <stdio.h>
extern "C" void __declspec(dllexport) HelloWorld()
{
    printf("Hello world, invoked by F#!\n");
}
```

Эту функцию можно вызвать из F #, используя следующий код.

```fsharp
open System.Runtime.InteropServices

module InteropWithNative =
    [<DllImport(@"C:\bin\nativedll", CallingConvention = CallingConvention.Cdecl)>]
    extern void HelloWorld()

InteropWithNative.HelloWorld()
```

Взаимодействие с машинным кодом называется *неуправляемого* и является компонентом среды CLR. Дополнительные сведения см. в разделе [Взаимодействие с неуправляемым кодом](../../../../docs/framework/interop/index.md). Сведения в этом разделе применима в F #.


## <a name="see-also"></a>См. также

[Функции](index.md)
