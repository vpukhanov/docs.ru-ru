---
title: Создание клиента WCF из метаданных службы
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 27f8f545-cc44-412a-b104-617e0781b803
caps.latest.revision: ''
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 9eedf84d1dccb8bc2540aca7e6bd338b4e58326d
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/26/2018
---
# <a name="generating-a-wcf-client-from-service-metadata"></a>Создание клиента WCF из метаданных службы
В этом разделе рассматривается использование различных ключей в Svcutil.exe для формирования клиентов из документов метаданных.  
  
 Документы метаданных могут находиться в устойчивом хранилище или извлекаться в оперативном режиме. Извлечение в оперативном режиме происходит либо по протоколу WS-MetadataExchange, либо по протоколу Microsoft Discovery (DISCO). Svcutil.exe одновременно отправляет следующие запросы метаданных для извлечения метаданных:  
  
-   запрос WS-MetadataExchange (MEX) по указанному адресу;  
  
-   запрос MEX с присоединенным ключом `/mex` по указанному адресу;  
  
-   Запрос DISCO (с помощью [DiscoveryClientProtocol](http://go.microsoft.com/fwlink/?LinkId=94777) из веб-службы ASP.NET) по указанному адресу.  
  
 Программа Svcutil.exe формирует клиент на основании файла WSDL или файла политики, полученного от службы. Имя участника-пользователя формируется путем добавления к имени пользователя символа "\@" и полного доменного имени. Однако для пользователей, зарегистрированных в Active Directory, этот формат не является допустимым, и имя участника-пользователя, создаваемый программой вызывает сбой проверки подлинности Kerberos со следующим сообщением: **Неудачная попытка входа.** Чтобы устранить эту проблему, необходимо вручную откорректировать файл клиента, сформированный Svcutil.exe.  
  
```  
svcutil.exe [/t:code]  <metadataDocumentPath>* | <url>* | <epr>  
```  
  
## <a name="referencing-and-sharing-types"></a>Ссылки на типы и совместное использование типов  
  
|Параметр|Описание|  
|------------|-----------------|  
|**/ reference:\<путь к файлу >**|Ссылается на типы в заданной сборке. При создании клиентов необходимо использовать этот параметр для задания сборок, которые могут содержать типы, представляющие импортируемые метаданные.<br /><br /> Краткая форма: `/r`|  
|**/excludeType:\<тип >**|Задает полное имя типа или имя типа с указанием на сборку, который необходимо исключить из ссылочных типов контракта.<br /><br /> Краткая форма: `/et`|  
  
## <a name="choosing-a-serializer"></a>Выбор сериализатора  
  
|Параметр|Описание|  
|------------|-----------------|  
|**/serializer:Auto**|Автоматически выбирает сериализатор. Выбираемый сериализатор - `DataContract`. Если использовать этот сериализатор не удается, используется сериализатор `XmlSerializer`.<br /><br /> Сокращенная форма: `/ser:Auto`|  
|**/serializer:DataContractSerializer**|Формирует типы данных, использующих для сериализации и десериализации сериализатор `DataContract`.<br /><br /> Краткая форма: `/ser:DataContractSerializer`|  
|**/serializer:XmlSerializer**|Формирует типы данных, использующих для сериализации и десериализации сериализатор `XmlSerializer`.<br /><br /> Краткая форма: `/ser:XmlSerializer`|  
|**/importXmlTypes**|Настраивает сериализатор `DataContract` на импорт типов, отличных от `DataContract`, в виде типов `IXmlSerializable`.<br /><br /> Краткая форма: `/ixt`|  
|**/dataContractOnly**|Формирует код только для типов `DataContract`. Формируются типы `ServiceContract`.<br /><br /> Для этого параметра следует задавать только локальные файлы метаданных.<br /><br /> Краткая форма: `/dconly`|  
  
## <a name="choosing-a-language-for-the-client"></a>Выбор языка для клиента  
  
|Параметр|Описание|  
|------------|-----------------|  
|**/language:\<language>**|Задает язык программирования, используемый для создания кода. Необходимо задать либо имя языка, зарегистрированное в файле Machine.config, либо полное имя класса, наследуемого от <xref:System.CodeDom.Compiler.CodeDomProvider>.<br /><br /> Значения: c#, cs, csharp, vb, vbs, visualbasic, vbscript, javascript, c++, mc, cpp<br /><br /> По умолчанию: csharp<br /><br /> Краткая форма: `/l`<br /><br /> [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Класс CodeDomProvider](http://go.microsoft.com/fwlink/?LinkId=94778).|  
  
## <a name="choosing-a-namespace-for-the-client"></a>Выбор пространства имен для клиента  
  
|Параметр|Описание|  
|------------|-----------------|  
|**/namespace:\<string,string>**|Задает сопоставление между элементом `targetNamespace` WSDL или схемы XML и пространством имен среды CLR. При использовании в качестве значения элемента `targetNamespace` подстановочного знака (*) все элементы `targetNamespaces` сопоставляются без явного сопоставления данному пространству имен среды CLR.<br /><br /> Чтобы гарантировать, что имя контракта сообщения не конфликтует с именем операции, либо дополните ссылку на тип двойными двоеточиями (`::`), либо убедитесь, что имена уникальны.<br /><br /> По умолчанию: для типов `DataContracts` выводится из целевого пространства имен документа схемы. Для всех остальных создаваемых типов используется пространство имен по умолчанию.<br /><br /> Краткая форма: `/n`|  
  
## <a name="choosing-a-data-binding"></a>Выбор привязки данных  
  
|Параметр|Описание|  
|------------|-----------------|  
|**/enableDataBinding**|Реализует интерфейс <xref:System.ComponentModel.INotifyPropertyChanged> во всех типах `DataContract` для включения привязки данных.<br /><br /> Краткая форма: `/edb`|  
  
## <a name="generating-configuration"></a>Формирование конфигурации  
  
|Параметр|Описание|  
|------------|-----------------|  
|**/config:\<configFile>**|Задает имя файла для формируемого файла конфигурации.<br /><br /> По умолчанию: output.config|  
|**/mergeConfig**|Объединяет созданную конфигурацию с существующим файлом (вместо его перезаписи).|  
|**/noConfig**|Запрещает создавать файлы конфигурации.|  
  
## <a name="see-also"></a>См. также  
 [Использование метаданных](../../../../docs/framework/wcf/feature-details/using-metadata.md)  
 [Общие сведения об архитектуре метаданных](../../../../docs/framework/wcf/feature-details/metadata-architecture-overview.md)
