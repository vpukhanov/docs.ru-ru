---
title: Глобализация и локализация приложений .NET Framework
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: ''
ms.suite: ''
ms.technology: dotnet-standard
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- international applications [.NET Framework]
- globalization [.NET Framework], encoding
- global applications
- internationalization
- world-ready applications
- application development [.NET Framework], globalization
- multilingual application development
ms.assetid: 9a59696b-d89b-45bd-946d-c75da4732d02
caps.latest.revision: 42
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 63f0e001280773c55f18f0604ca93986acbb9674
ms.sourcegitcommit: 91691981897cf8451033cb01071d8f5d94017f97
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/09/2018
---
# <a name="globalizing-and-localizing-net-framework-applications"></a>Глобализация и локализация приложений .NET Framework
Разработка [международного приложения](http://msdn.microsoft.com/goglobal/bb978433.aspx), в том числе приложения, которое можно локализовать на один или несколько языков, включает следующие шаги: глобализацию, анализ локализуемости и локализацию.  
  
 [Глобализация](../../../docs/standard/globalization-localization/globalization.md)  
 Этот шаг включает проектирование и программирование приложения, не зависящего от языка и региональных параметров и поддерживающего локализованные пользовательские интерфейсы и региональные данные для всех пользователей. Это предполагает принятие проектных и программных решений, которые не основаны на предположениях в отношении определенного языка или региональных параметров. Хотя глобализованное приложение не локализовано, однако оно разработано и составлено так, чтобы впоследствии его можно было относительно легко локализовать на один или несколько языков.  
  
 [Анализ локализуемости](../../../docs/standard/globalization-localization/localizability-review.md)  
 Этот шаг позволяет проверить код и дизайн приложения, чтобы убедиться в возможности простой локализации приложения и убедиться, что исполняемый код и ресурсы приложения разделены. Если этап глобализации был эффективным, анализ локализуемости подтвердит проектные решения и решения кодирования, принятые во время глобализации. На этапе анализа локализуемости можно выявить оставшиеся проблемы, чтобы не пришлось менять исходный код приложения на этапе локализации.  
  
 [Локализация](../../../docs/standard/globalization-localization/localization.md)  
 Этот этап включает настройку приложения для конкретных языков или регионов. Если этапы глобализации и анализа локализуемости были проведены правильно, то локализация заключается главным образом в переводе пользовательского интерфейса.  
  
 Выполнение этих трех этапов обеспечивает два преимущества:  
  
-   Освобождает от необходимости модифицировать приложение, разработанное для поддержки одного языка и региона, например английского языка (США), чтобы обеспечить поддержку дополнительных языков и регионов.  
  
-   В результате создаются локализованные приложения, которые более стабильны и содержат меньше ошибок.  
  
 .NET Framework предоставляет широкие возможности для разработки международных и локализованных приложений. В частности, многие члены типов в библиотеке классов .NET Framework упрощают глобализацию, возвращая значения, отражающие соглашения либо языка и региональных параметров текущего пользователя, либо заданных языка и региональных параметров. Кроме того, платформа .NET Framework поддерживает вспомогательные сборки, которые упрощают процесс локализации приложений.  
  
 Дополнительные сведения см. в [документации по глобализации](/globalization/).  
  
## <a name="in-this-section"></a>В этом разделе  
 [Глобализация](../../../docs/standard/globalization-localization/globalization.md)  
 Описание первого этапа создания международного приложения, который предполагает проектирование и кодирование приложения, не зависящего от языка и региональных параметров.  
  
 [Анализ локализуемости](../../../docs/standard/globalization-localization/localizability-review.md)  
 Описание второго этапа создания международного приложения, который предполагает выявление потенциальных препятствий для локализации.  
  
 [Локализация](../../../docs/standard/globalization-localization/localization.md)  
 Описание заключительного этапа создания локализованного приложения, который предполагает настройку пользовательского интерфейса приложения для конкретных регионов или языков и региональных параметров.  
  
 [Операции со строками без учета языка и региональных параметров](../../../docs/standard/globalization-localization/culture-insensitive-string-operations.md)  
 Описание использования методов и классов .NET Framework, которые по умолчанию зависят от языка и региональных параметров, для обеспечения результатов, не зависящих от этих параметров.  
  
 [Рекомендации по разработке международных приложений](../../../docs/standard/globalization-localization/best-practices-for-developing-world-ready-apps.md)  
 Описание лучших методик по глобализации, локализации и разработке международных приложений ASP.NET.  
  
## <a name="reference"></a>Ссылка  
 Пространство имен <xref:System.Globalization?displayProperty=nameWithType>  
 Содержит классы, определяющие сведения, относящиеся к культуре, такие как язык, название страны, используемые календари, шаблоны форматирования дат, денежных единиц и чисел, а также порядок сортировки строк.  
  
 Пространство имен <xref:System.Resources>  
 Предоставляет классы для создания и использования ресурсов, а также управления ими.  
  
 Пространство имен <xref:System.Text>  
 Содержит классы, представляющие ASCII, ANSI, Юникод и другие форматы кодировки символов.  
  
 [Resgen.exe (генератор файлов ресурсов)](../../../docs/framework/tools/resgen-exe-resource-file-generator.md)  
 Описание использования программы Resgen.exe для преобразования файлов .txt и .resx и файлов формата XML (.resx) в двоичные файлы .resources общей среды исполнения.  
  
 [Winres.exe (редактор ресурсов Windows Forms)](../../../docs/framework/tools/winres-exe-windows-forms-resource-editor.md)  
 Описание использования Winres.exe для локализации форм Windows Forms.
