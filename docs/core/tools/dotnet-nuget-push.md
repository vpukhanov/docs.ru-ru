---
title: "Команда dotnet nuget push — CLI .NET Core"
description: "Команда dotnet nuget push отправляет пакет на сервер и публикует его."
author: karann-msft
ms.author: mairaw
ms.date: 08/14/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.workload:
- dotnetcore
ms.openlocfilehash: a0f872ae930d17638e018cdd204cc08a773a3df5
ms.sourcegitcommit: d95a91d685565f4d95c8773b558752864a6a3d7e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/12/2018
---
# <a name="dotnet-nuget-push"></a>dotnet nuget push

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>name

`dotnet nuget push` — отправляет пакет на сервер и публикует его.

## <a name="synopsis"></a>Краткий обзор

`dotnet nuget push [<ROOT>] [-s|--source] [-ss|--symbol-source] [-t|--timeout] [-k|--api-key] [-sk|--symbol-api-key] [-d|--disable-buffering] [-n|--no-symbols] [--force-english-output] [-h|--help]`

## <a name="description"></a>Описание:

Команда `dotnet nuget push` отправляет пакет на сервер и публикует его. Команда push использует сервер и учетные данные, указанные в системном файле конфигурации NuGet или цепочке файлов конфигурации. См. дополнительные сведения о файлах конфигурации в статье о [настройке поведения NuGet](/nuget/consume-packages/configuring-nuget-behavior). Конфигурацию NuGet по умолчанию можно получить, загрузив файл *%AppData%\NuGet\NuGet.config* (Windows) или *$HOME/.local/share* (Linux и macOS). Затем нужно загрузить все файлы *nuget.config* или *.nuget\nuget.config*, начиная с корневого каталога диска и заканчивая текущим каталогом.

## <a name="arguments"></a>Аргументы

`ROOT`

Указывает путь к файлу пакета для отправки.

## <a name="options"></a>Параметры

`-h|--help`

Выводит краткую справку по команде.

`-s|--source <SOURCE>`

Определяет URL-адрес сервера. Этот параметр является обязательным, если значение параметра конфигурации `DefaultPushSource` задано в файле конфигурации NuGet.

`--symbol-source <SOURCE>`

Указывает URL-адрес сервера символов.

`-t|--timeout <TIMEOUT>`

Указывает время ожидания для передачи на сервер в секундах. Значение по умолчанию — 300 секунд (5 минут). При указании 0 (ноль секунд) применяется значение по умолчанию.

`-k|--api-key <API_KEY>`

Ключ API для сервера.

`--symbol-api-key <API_KEY>`

Ключ API для сервера символов.

`-d|--disable-buffering`

Отключает буферизацию при передаче данных на сервер HTTP(S), чтобы снизить использование памяти.

`-n|--no-symbols`

Не передает символы (даже если они присутствуют).

`--force-english-output`

Принудительно отображает все зарегистрированные выходные данные на английском языке.

## <a name="examples"></a>Примеры

Отправляет *foo.nupkg* в источник push-уведомлений по умолчанию, предоставляя ключ API.

`dotnet nuget push foo.nupkg -k 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a`

Отправляет *foo.nupkg* в пользовательский источник push-уведомлений `http://customsource`, предоставляя ключ API.

`dotnet nuget push foo.nupkg -k 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s http://customsource/`

Отправляет *foo.nupkg* в источник push-уведомлений по умолчанию.

`dotnet nuget push foo.nupkg`

Отправляет *foo.symbols.nupkg* в источник символов по умолчанию.

`dotnet nuget push foo.symbols.nupkg`

Отправляет *foo.nupkg* в источник push-уведомлений по умолчанию, указав время ожидания 360 секунд.

`dotnet nuget push foo.nupkg --timeout 360`

Отправляет все файлы *NUPKG* из текущего каталога в источник push-уведомлений по умолчанию.

`dotnet nuget push *.nupkg`

Отправляет все файлы *NUPKG* из текущего каталога в источник push-уведомлений по умолчанию, указав собственный файл конфигурации *./config/My.Config*.

`dotnet nuget push *.nupkg --config-file ./config/My.Config`
