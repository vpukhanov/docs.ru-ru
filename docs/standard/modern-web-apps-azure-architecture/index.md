---
title: Разработка современных веб-приложений с помощью ASP.NET Core и Azure
description: Разработка современных веб-приложений с помощью ASP.NET Core и Azure | Введение
author: ardalis
ms.author: wiwagn
ms.date: 10/06/2017
ms.prod: .net-core
ms.technology: dotnet-docker
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 1140a18aba685f3415d7c599d1b76648bf9924e7
ms.sourcegitcommit: c3957fdb990060559d73cca44ab3e2c7b4d049c0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/05/2018
---
# <a name="architect-modern-web-applications-with-aspnet-core-and-azure"></a>Разработка современных веб-приложений с помощью ASP.NET Core и Azure

![изображение обложки](./media/cover.jpg)


.NET Core и ASP.NET Core имеют ряд преимуществ по сравнению с традиционной разработкой .NET. Используйте .NET Core для серверных приложений, если для их успешной работы вам важны некоторые или все приведенные далее аспекты:

-   Поддержка разных платформ

-   Использование микрослужб

-   Использование контейнеров Docker

-   Требования к обеспечению высокой производительности и масштабируемости

-   Параллельное управление версиями приложения .NET на одном сервере

Эти требования поддерживаются традиционными приложениями .NET, однако оптимизированные платформы ASP.NET Core и .NET Core обеспечивают улучшенную поддержку указанных выше сценариев.

Все больше организаций предпочитают размещать свои веб-приложения в облаке с помощью таких служб, как Microsoft Azure. Рекомендуется рассмотреть возможность размещения приложения в облаке, если для приложения или организации важны следующие моменты:

-   Сокращение инвестиций в центр обработки данных (оборудование, программное обеспечение, помещения, коммунальные услуги и т. д.)

-   Гибкие цены (оплата за фактически используемые, а не простаивающие ресурсы)

-   Исключительная надежность

-   Улучшенная мобильность приложений, простота изменения места и способа их развертывания

-   Гибкая емкость, масштабирование в соответствии с фактическими потребностями

Создание веб-приложений с помощью ASP.NET Core, размещенных в Microsoft Azure, характеризуется многочисленными конкурентными преимуществами по сравнению с традиционными альтернативами. Платформа ASP.NET Core оптимизирована для современных методик разработки веб-приложений и сценариев размещения в облаке. В этом руководстве вы узнаете, как спроектировать приложения ASP.NET Core, чтобы максимально эффективно воспользоваться этими возможностями.

## <a name="purpose"></a>Цель

Этот документ является полным руководством по созданию монолитных веб-приложений с помощью ASP.NET Core и Azure.

Это руководство дополняет документ *Проектирование и разработка контейнерных приложений и приложений на основе микрослужб в .NET*, в котором более подробно рассматриваются Docker, микрослужбы и процедура развертывания контейнеров для размещения корпоративных приложений.

> ### <a name="architecting-and-developing-containerized-microservice-based-apps-in-net"></a>Проектирование и разработка контейнерных приложений и приложений на основе микрослужб в .NET
> - **электронная книга**  
> <http://aka.ms/MicroservicesEbook>
> - **Пример приложения**  
> <http://aka.ms/microservicesarchitecture>

## <a name="who-should-use-this-guide"></a>Кому необходимо это руководство

Это руководство предназначено главным образом для разработчиков, руководителей отделов разработки и архитекторов, заинтересованных в создании современных веб-приложений с помощью технологий и служб Майкрософт в облаке.

Вторичной аудиторией являются лица, ответственные за принятие технических решений, которые уже знакомы с ASP.NET и (или) Azure и которым требуются сведения о целесообразности обновления до ASP.NET Core для разработки новых и поддержки существующих проектов.

## <a name="how-you-can-use-this-guide"></a>Как использовать это руководство

Это руководство было сведено в относительно небольшой документ, в котором основное внимание уделяется созданию веб-приложений с помощью современных технологий .NET и Windows Azure. Поэтому, чтобы получить базовое представление о таких приложениях и разобраться в соответствующих технических рекомендациях, изучите документ полностью. Это руководство вместе с примером приложения может быть хорошей отправной точкой или полезным справочным документом. Используйте приведенный пример приложения в качестве шаблона для собственных приложений, или чтобы увидеть, каким образом можно организовать составные части приложения. Принимая решение о применении этих вариантов к своему приложению, вы всегда можете обратиться к описанным в руководстве принципам и направлениям архитектуры и технологическим возможностям.

При необходимости вы можете порекомендовать это руководство членам своей команды, чтобы и они были в курсе всех важных аспектов. Если все заинтересованные лица будут использовать общий набор терминологии и придерживаться основополагающих принципов, архитектурные модели и практики будут применяться более последовательно.

## <a name="references"></a>Ссылки
- **Выбор между .NET Core и .NET Framework для серверных приложений**  
<https://docs.microsoft.com/dotnet/standard/choosing-core-framework-server>

>[!div class="step-by-step"]
[Далее] (modern-web-applications-characteristics.md)
