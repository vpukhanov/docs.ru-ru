---
title: -target (Visual Basic)
ms.date: 03/13/2018
ms.prod: .net
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- target compiler options [Visual Basic]
- -target compiler options [Visual Basic]
- /target compiler options [Visual Basic]
ms.assetid: e0954147-548b-461f-9c4b-a8f88845616c
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 8596cb7d43b2c54b46dedc40488ed1b4e2c31b69
ms.sourcegitcommit: 498799639937c89de777361aab74261efe7b79ea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/22/2018
---
# <a name="-target-visual-basic"></a>-target (Visual Basic)
Задает формат выходных данных компилятора.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
-target:{exe | library | module | winexe | appcontainerexe | winmdobj}  
```  
  
## <a name="remarks"></a>Примечания  
 В следующей таблице перечислены действия `-target` параметр.  
  
|**Параметр**|**Behavior**|  
|----------------|------------------|  
|`-target:exe`|Указывает компилятору создавать исполняемое консольное приложение.<br /><br /> Это параметр по умолчанию, если аргумент `-target` параметра. Исполняемый файл создается с расширением .exe.<br /><br /> Если не указано иначе с `/out` параметр, выходной файл получает имя входного файла, содержащего `Sub Main` процедуры.<br /><br /> Только один `Sub Main` процедура является обязательной в файлах исходного кода, которые компилируются в файл .exe. Используйте `-main` параметр компилятора, чтобы указать класс, содержащий `Sub Main` процедуры.|  
|`-target:library`|Указывает компилятору создать библиотеку динамической компоновки (DLL).<br /><br /> Файл библиотеки динамической компоновки создается с расширением DLL.<br /><br /> Если не указано иначе с `-out` параметр, выходной файл получает имя первого входного файла.<br /><br /> При создании библиотеки DLL, `Sub Main` процедура не требуется.|  
|`-target:module`|Указывает компилятору создавать модуль, который может быть добавлен в сборку.<br /><br /> Выходной файл создается с расширением .netmodule.<br /><br /> Общеязыковой среде выполнения .NET не удается загрузить файл, у которого нет сборки. Тем не менее, можно включить такой файл в манифест сборки с помощью `-reference`.<br /><br /> Если код одного модуля ссылается на внутренние типы другого модуля, оба модуля должны быть включены в манифест сборки с помощью `-reference`.<br /><br /> [- Addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md) параметр импортирует метаданные из модуля.|  
|`-target:winexe`|Указывает компилятору на необходимость создания исполняемого приложения на основе Windows.<br /><br /> Исполняемый файл создается с расширением .exe. Приложение, на основе Windows — это предоставляет пользовательский интерфейс, либо из [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] библиотеки классов или с помощью API-интерфейсов Win32.<br /><br /> Если не указано иначе с `-out` параметр, выходной файл получает имя входного файла, содержащего `Sub Main` процедуры.<br /><br /> Только один `Sub Main` процедура является обязательной в файлах исходного кода, которые компилируются в файл .exe. В случаях, если код содержит более одного класса, имеющего `Sub Main` процедуре, воспользуйтесь `-main` параметр компилятора, чтобы указать класс, содержащий `Sub Main` процедуры|  
|`-target:appcontainerexe`|Указывает компилятору на необходимость создания исполняемого приложения на основе Windows, необходимо запустить в контейнере приложения. Этот параметр предназначен для использования [!INCLUDE[win8_appname_long](~/includes/win8-appname-long-md.md)] приложений.<br /><br /> **Appcontainerexe** параметр устанавливает бит в поле характеристики [переносимый исполняемый файл](http://go.microsoft.com/fwlink/p/?LinkId=236960) файла. Этот бит указывает, что приложение необходимо запустить в контейнере приложения. Если этот бит устанавливается, если возникает ошибка `CreateProcess` метод пытается запустить приложение вне контейнера приложения. Помимо этот бит параметр **-target: appcontainerexe** эквивалентно **-target: winexe**.<br /><br /> Исполняемый файл создается с расширением .exe.<br /><br /> Если не указано иное с помощью `-out` параметр, выходной файл получает имя входного файла, содержащего `Sub Main` процедуры.<br /><br /> Только один `Sub Main` процедура является обязательной в файлах исходного кода, которые компилируются в файл .exe. Если код содержит более одного класса, имеющего `Sub Main` процедуре, воспользуйтесь `-main` параметр компилятора, чтобы указать класс, содержащий `Sub Main` процедуры|  
|`-target:winmdobj`|Указывает компилятору создать промежуточный файл, который можно преобразовать в бинарный winmd-файл среды выполнения Windows. Winmd-файл может использоваться программ, помимо программы на управляемом языке JavaScript и C++.<br /><br /> Промежуточный файл создается с расширением .winmdobj.<br /><br /> Если не указано иное с помощью `-out` параметр, выходной файл получает имя первого входного файла. Объект `Sub Main` процедуры не требуется.<br /><br /> Winmdobj-файл предназначен для использования в качестве входных данных для <xref:Microsoft.Build.Tasks.WinMDExp> экспорта средство для создания файла метаданных (WinMD) Windows. WinMD-файл с расширением .winmd и содержит код из исходной библиотеки и определения WinMD, JavaScript, C++ и использование среды выполнения Windows.|  
  
 Если не указано `-target:module`, `-target` вызывает [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] манифест сборки, добавляется в выходной файл.  
  
 Создает каждый экземпляр Vbc.exe, не более одного выходного файла. При указании параметра компилятора `-out` или `-target` более одного раза, последнее из них компилятора процессы, вступили в силу. Сведения о всех файлах в компиляции добавляется в манифест. Все выходные файлы, за исключением тех, которые созданы с `-target:module` содержать метаданные сборки в манифесте. Используйте [Ildasm.exe (дизассемблер IL)](https://msdn.microsoft.com/library/f7dy01k1) для просмотра метаданных в выходной файл.  
  
 Краткой формой `-target` является `-t`.  
  
### <a name="to-set--target-in-the-visual-studio-ide"></a>Для установки - target в Интегрированной среде разработки Visual Studio  
  
1.  Выберите проект в **Обозревателе решений**. В меню **Проект** выберите пункт **Свойства**.   
  
2.  Перейдите на вкладку **Приложение** .  
  
3.  Измените значение в **тип приложения** поле.  
  
## <a name="example"></a>Пример  
 Следующий код компилирует `in.vb`, создавая `in.dll`:  
  
```console
vbc -target:library in.vb  
```  
  
## <a name="see-also"></a>См. также  
 [Компилятор Visual Basic с интерфейсом командной строки](../../../visual-basic/reference/command-line-compiler/index.md)  
 [-main](../../../visual-basic/reference/command-line-compiler/main.md)  
 [-out (Visual Basic)](../../../visual-basic/reference/command-line-compiler/out.md)  
 [-ссылке (Visual Basic)](../../../visual-basic/reference/command-line-compiler/reference.md)  
 [-addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md)  
 [-moduleassemblyname](../../../visual-basic/reference/command-line-compiler/moduleassemblyname.md)  
 [Сборки и глобальный кэш сборок](../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)  
 [Примеры командных строк компиляции](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
