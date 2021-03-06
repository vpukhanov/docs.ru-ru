---
title: Разработка для нескольких платформ с помощью .NET Framework
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: ''
ms.suite: ''
ms.technology: dotnet-standard
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b153baaa-130c-4169-860b-e580591de91e
caps.latest.revision: 13
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 9acceb04ea48ef7d9a99d8a82c63090ee344ea54
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/23/2017
---
# <a name="developing-for-multiple-platforms-with-the-net-framework"></a>Разработка для нескольких платформ с помощью .NET Framework
Вы можете разрабатывать приложения для платформ Майкрософт и других поставщиков, используя .NET Framework и Visual Studio.  
  
## <a name="options-for-cross-platform-development"></a>Варианты для межплатформенной разработки  
 Для разработки приложений для нескольких платформ можно использовать один исходный код или двоичные файлы, а также осуществлять вызовы между кодом .NET Framework и API-интерфейсами среды выполнения Windows.  
  
|Цель...|Используйте...|  
|-----------------------|------------|  
|Совместное использование кода между приложениями Windows Phone 8.1 и Windows 8.1|**Общие проекты** (шаблон универсальных приложений в Visual Studio 2013 с обновлением 2).<br /><br /> -В настоящее время Visual Basic не поддерживается.<br />— Вы можете разделять код конкретной платформы с помощью #`if` инструкции.<br /><br /> Дополнительные сведения см. в следующих ресурсах:<br /><br /> -   [Создание приложений, предназначенных для Windows и Windows Phone с помощью Visual Studio](http://msdn.microsoft.com/library/windows/apps/dn609832.aspx) (статья MSDN)<br />-   [С помощью Visual Studio для создания универсальных XAML-приложений](http://blogs.msdn.com/b/visualstudio/archive/2014/04/14/using-visual-studio-to-build-universal-xaml-apps.aspx) (запись блога)<br />-   [С помощью Visual Studio для создания Конвергированных XAML-приложений](http://channel9.msdn.com/Events/Build/2014/3-591) (видео)|  
|Совместное использование двоичных файлов приложениями для различных платформ|**Проекты переносимой библиотеки классов** для кода, не зависящего от платформы.<br /><br /> — Это подход обычно используется для кода, который реализует бизнес-логику.<br />-Используется Visual Basic или C#.<br />-Поддержка API зависит от платформы.<br />-Проекты переносимой библиотеки классов, предназначенных для Windows 8.1 и Windows Phone 8.1 поддерживают API среды выполнения Windows и XAML. Эти возможности недоступны в более старых версиях переносимой библиотеки классов.<br />— При необходимости можно абстрагировать код платформы, используя интерфейсы или абстрактные классы.<br /><br /> Дополнительные сведения см. в следующих ресурсах:<br /><br /> -   [Переносимая библиотека классов](../../../docs/standard/cross-platform/cross-platform-development-with-the-portable-class-library.md) (статья MSDN)<br />-   [Как заставить переносимой библиотеки классов работать на вас](http://blogs.msdn.com/b/dsplaisted/archive/2012/08/27/how-to-make-portable-class-libraries-work-for-you.aspx) (запись блога)<br />-   [Использование переносимой библиотеки классов с MVVM](../../../docs/standard/cross-platform/using-portable-class-library-with-model-view-view-model.md) (статья MSDN)<br />-   [Ресурсы приложений для библиотек, предназначенных для нескольких платформ](../../../docs/standard/cross-platform/app-resources-for-libraries-that-target-multiple-platforms.md) (статья MSDN)<br />-   [Анализатор переносимости .NET](http://visualstudiogallery.msdn.microsoft.com/1177943e-cfb7-4822-a8a6-e56c7905292b) (расширение Visual Studio)|  
|Совместное использование кода между приложениями для платформ, отличных от Windows Phone 8.1 и Windows 8.1|**Добавить как ссылку** компонентов.<br /><br /> -Этот подход используется для логики приложения, общие для обоих приложений, но не может быть перенесена, для какой-либо причине. Эту возможность можно использовать в коде Visual Basic или C#.<br />     Например, Windows Phone 8 и Windows 8 используют одни API среды выполнения Windows, но переносимые библиотеки классов не поддерживают среду выполнения Windows для этих платформ. Вы можете использовать `Add as link` для совместного использования кода среды выполнения Windows между приложением Windows Phone 8 и приложением Магазина Windows, предназначенного для Windows 8.<br /><br /> Дополнительные сведения см. в следующих ресурсах:<br /><br /> -   [Совместное использование кода с добавить как ссылку](http://msdn.microsoft.com/library/windowsphone/develop/jj714082\(v=vs.105\).aspx) (статья MSDN)<br />-   [Как: Добавление существующих элементов в проект](http://msdn.microsoft.com/library/vstudio/9f4t9t92\(v=vs.100\).aspx) (статья MSDN)|  
|Создание приложений Магазина Windows с использованием .NET Framework или вызов API среды выполнения Windows из кода .NET Framework|**API среды выполнения Windows** из кода .NET Framework на C# или Visual Basic и использование .NET Framework для создания приложений для магазина Windows. Следует помнить о различиях API двух платформ. Однако существуют классы, помогающие обойти эти отличия.<br /><br /> Дополнительные сведения см. в следующих ресурсах:<br /><br /> -   [.NET framework поддержка для приложений магазина Windows и среды выполнения Windows](../../../docs/standard/cross-platform/support-for-windows-store-apps-and-windows-runtime.md) (статья MSDN)<br />-   [Передача URI в среду выполнения Windows](../../../docs/standard/cross-platform/passing-a-uri-to-the-windows-runtime.md) (статья MSDN)<br />-   <!--zz <xref:System.IO.WindowsRuntimeStreamExtensions>-->`System.IO.WindowsRuntimeStreamExtensions` (Страница справочника по API на портале MSDN)<br />-   <!--zz <xref:System.WindowsRuntimeSystemExtensions>-->`System.WindowsRuntimeSystemExtensions` (Страница справочника по API на портале MSDN)|  
|Создание приложений .NET Framework для платформ других поставщиков|**Ссылочные сборки переносимой библиотеки классов** в .NET Framework и Visual Studio расширения или стороннее средство, например Xamarin.<br /><br /> Дополнительные сведения см. в следующих ресурсах:<br /><br /> -   [Переносимая библиотека классов теперь доступна на всех платформах.](http://blogs.msdn.com/b/dotnet/archive/2013/10/14/portable-class-library-pcl-now-available-on-all-platforms.aspx) (публикация блога)<br />-   [Xamarin](http://xamarin.com/visual-studio) (веб-сайт Xamarin)|  
|Использование JavaScript и HTML для межплатформенной разработки|**Шаблоны универсальных приложений** в Visual Studio 2013 обновление 2 для разработки с API среды выполнения Windows для Windows 8.1 и Windows Phone 8.1. В текущий момент нет возможности использовать JavaScript и HTML с API-интерфейсами .NET Framework для разработки межплатформенных приложений.<br /><br /> Дополнительные сведения см. в следующих ресурсах:<br /><br /> -   [Шаблоны проектов JavaScript](http://msdn.microsoft.com/library/windows/apps/hh758331.aspx)<br />-   [Перенос приложения среды выполнения Windows с использованием JavaScript для Windows Phone](http://msdn.microsoft.com/library/windows/apps/dn636144.aspx)|
