---
title: Модульное тестирование в .NET Core
description: Выполнять модульное тестирование стало как никогда просто. Узнайте, как использовать модульное тестирование в проектах .NET Core и .NET Standard.
keywords: .NET, .NET Core, .NET Standard, unit testing
author: ardalis
ms.author: wiwagn
ms.date: 08/30/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: 815ac74c-4bd9-4a94-a87c-78288b27c0e2
ms.workload:
- dotnetcore
ms.openlocfilehash: cb78a66a3a6a7158a86a76d62e5230c75b51a416
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/23/2017
---
# <a name="unit-testing-in-net-core-and-net-standard"></a>Модульное тестирование в .NET Core и .NET Standard

При разработке платформы .NET Core учитывались возможности тестирования, поэтому создавать модульные тесты для приложений стало еще проще. В этой статье вкратце рассматриваются модульные тесты (и то, чем они отличаются от других типов тестов). В связанных ресурсах демонстрируется, как добавить тестовый проект в решение и как затем выполнять модульные тесты с помощью командной строки или Visual Studio.

.NET Core 2.0 поддерживает [.NET Standard 2.0](../../standard/net-standard.md). Библиотеки, используемые для демонстрации модульного тестирования в этом разделе, зависят от .NET Standard и будут работать с другими типами проектов.

Начиная с .NET Core 2.0 доступны шаблоны проекта модульных тестов не только для C#, но и для Visual Basic и F #.

## <a name="getting-started-with-testing"></a>Приступая к тестированию

Наличие набора автоматических тестов — один из лучших способов обеспечить работу приложения именно так, как она задумывалась разработчиками. Доступны разные типы тестов для приложений, включая тесты интеграции, веб-тесты, нагрузочные тесты и т. д. На самом низком уровне применяются модульные тесты, которые проверяют отдельные компоненты или методы программного обеспечения. Модульные тесты должны применяться только к коду, находящемуся под контролем разработчика, но не к компонентам инфраструктуры, таким как базы данных, файловые системы или сетевые ресурсы. Модульные тесты можно создавать в рамках [разработки на основе тестирования (TDD)](http://deviq.com/test-driven-development/) или добавлять в существующий код для проверки его правильности. В любом случае они должны быть небольшими, иметь понятные имена и выполняться быстро, так как в идеале у вас должна быть возможность выполнить сотни таких тестов перед публикацией изменений в репозитории общего кода проекта.

> [!NOTE]
> У разработчиков часто возникают проблемы с тем, чтобы придумать подходящие имена для тестовых классов и методов. В качестве отправной точки команда разработчиков ASP.NET следует [этим соглашениям](https://github.com/aspnet/Home/wiki/Engineering-guidelines#unit-tests-and-functional-tests).

При создании модульных тестов будьте внимательны, чтобы случайно не добавить зависимости от инфраструктуры. Из-за них тесты, как правило, выполняются медленнее и менее стабильно и их следует зарезервировать для тестов интеграции. Чтобы избежать скрытых зависимостей в коде приложения, следуйте [принципу явных зависимостей](http://deviq.com/explicit-dependencies-principle/) и используйте [внедрение зависимостей](/aspnet/core/fundamentals/dependency-injection) для запроса зависимостей из платформы. Кроме того, можно выделить модульные тесты в отдельный проект, изолировав их от тестов интеграции, чтобы гарантировать отсутствие в этом проекте ссылок на пакеты инфраструктуры или зависимостей от них.

Дополнительные сведения о модульном тестировании в проектах .NET Core:

Поддержка проектов модульных тестов для .NET Core: [C#](../../csharp/index.md), [F #](../../fsharp/index.md) и [Visual Basic](../../visual-basic/index.md). Вы можете также выбрать [xUnit](http://xunit.github.io), [NUnit](http://nunit.org) или [MSTest](https://github.com/Microsoft/vstest-docs).

Дополнительные сведения об этих комбинациях см. в этих пошаговых руководствах:

* Создание модульных тестов с помощью [*XUnit*, *C#* и .NET Core CLI](unit-testing-with-dotnet-test.md).
* Создание модульных тестов с помощью [*NUnit*, *C#* и интерфейса командной строки .NET Core](unit-testing-with-nunit.md).
* Создание модульных тестов с помощью [*MSTest*, *C#* и .NET Core CLI](unit-testing-with-mstest.md).
* Создание модульных тестов с помощью [*XUnit*, *F#* и .NET Core CLI](unit-testing-fsharp-with-dotnet-test.md).
* Создание модульных тестов с помощью [*NUnit*, *F#* и интерфейса командной строки .NET Core](unit-testing-fsharp-with-nunit.md).
* Создание модульных тестов с помощью [*MSTest*, *F#* и .NET Core CLI](unit-testing-fsharp-with-mstest.md).
* Создание модульных тестов с помощью [*XUnit*, *Visual Basic* и .NET Core CLI](unit-testing-visual-basic-with-dotnet-test.md).
* Создание модульных тестов с помощью [*NUnit*, *Visual Basic* и интерфейса командной строки .NET Core](unit-testing-visual-basic-with-nunit.md).
* Создание модульных тестов с помощью [*MSTest*, *Visual Basic* и .NET Core CLI](unit-testing-visual-basic-with-mstest.md).

Вы можете выбрать разные языки для библиотек классов и модульных тестов. Дополнительные сведения см. в пошаговых руководствах выше (вы можете комбинировать их).

* Visual Studio Enterprise предлагает отличные средства тестирования для .NET Core. Дополнительные сведения: [Live Unit Testing](/visualstudio/test/live-unit-testing) и [Code Coverage](https://github.com/Microsoft/vstest-docs/blob/master/docs/analyze.md#working-with-code-coverage).
* Дополнительные сведения и примеры использования фильтрации при выборочном модульном тестировании см. в руководстве по [выполнению выборочных модульных тестов](selective-unit-tests.md) и [включению и исключению тестов с помощью Visual Studio](/visualstudio/test/live-unit-testing#including-and-excluding-test-projects-and-test-methods).
* Команда разработчиков XUnit разработала учебник, в котором показано, как [использовать xUnit с .NET Core и Visual Studio](http://xunit.github.io/docs/getting-started-dotnet-core.html).
