---
title: "Практическое руководство. Проверка внешних файлов сопоставления и DBML-файлов"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d9ea37f5-0a9e-4401-8fc3-1e6fd44c49f9
caps.latest.revision: "2"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: dotnet
ms.openlocfilehash: 7724586c33c19654c3657a5a4604a3c74f2c8756
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="how-to-validate-dbml-and-external-mapping-files"></a>Практическое руководство. Проверка внешних файлов сопоставления и DBML-файлов
После внесения изменений во внешние файлы сопоставлений и DBML-файлы их необходимо проверить на соответствие определениям схемы. Этот раздел предоставляет пользователям [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] шаги по реализации процесса проверки.  
  
 [!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]  
  
### <a name="to-validate-a-dbml-or-xml-file"></a>Проверка DBML-файла или XML-файла  
  
1.  В Visual Studio **файл** последовательно выберите пункты **откройте**, а затем нажмите кнопку **файл**.  
  
2.  В **открыть файл** диалогового окна выберите DBML-файл или XML-файл сопоставления, который нужно проверить.  
  
     Файл откроется в **редактора XML**.  
  
3.  Щелкните правой кнопкой мыши окно и нажмите кнопку **свойства**.  
  
4.  В **свойства** окно, нажмите кнопку с многоточием для **схемы** свойство.  
  
     **XML-схем** откроется диалоговое окно.  
  
5.  Отметьте определение схемы, соответствующее выполняемой задаче.  
  
    -   Для проверки DBML-файла используется определение схемы DbmlSchema.xsd. Дополнительные сведения см. в разделе [создание кода в LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/code-generation-in-linq-to-sql.md).  
  
    -   Для проверки внешнего XML-файла сопоставлений используется определение схемы LinqToSqlMapping.xsd. Дополнительные сведения см. в разделе [внешнего сопоставления](../../../../../../docs/framework/data/adonet/sql/linq/external-mapping.md).  
  
6.  В **используйте** столбец нужной строки определения схемы, щелкните, чтобы открыть поле раскрывающегося списка и нажмите кнопку **использовать эту схему**.  
  
     Устанавливается связь между файлом определения схемы и файлом DBML или XML.  
  
     Убедитесь, что не выбраны никакие другие определения схемы.  
  
7.  На **представление** меню, нажмите кнопку **список ошибок**.  
  
     Проверьте, не было ли создано ошибок, предупреждений или сообщений. Если ошибки, предупреждения или сообщения отсутствуют, XML-файл соответствует определению схемы.  
  
## <a name="alternate-method-for-supplying-schema-definition"></a>Альтернативный метод получения определения схемы  
 Если по некоторым причинам соответствующий XSD-файл не отображается в **XML-схем** диалоговое окно, можно загрузить XSD-файл из раздела справки. С помощью описанных ниже действий можно сохранить загруженный файл в формате Юникод, который требуется для редактора XML среды [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)].  
  
#### <a name="to-copy-a-schema-definition-file-from-a-help-topic"></a>Копирование файла определения схемы из раздела справки  
  
1.  Найдите раздел справки, который содержит определение схемы. Инструкции по выбору определения схемы см. ранее в этом разделе.  
  
    -   DBML-файлы в разделе [создание кода в LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/code-generation-in-linq-to-sql.md).  
  
    -   Внешние файлы сопоставлений, в разделе [внешнего сопоставления](../../../../../../docs/framework/data/adonet/sql/linq/external-mapping.md).  
  
2.  Нажмите кнопку **Копировать код** для копирования в файл кода в буфер обмена.  
  
3.  Откройте текстовый редактор Блокнот и создайте новый файл.  
  
4.  Вставьте код из буфера обмена в файл Блокнота.  
  
5.  Блокнота **файл** меню, нажмите кнопку **Сохранить как**.  
  
6.  В **кодировка** выберите **Юникода**.  
  
    > [!IMPORTANT]
    >  Это действие гарантирует, что в начало текстового файла будет добавлена отметка порядка байтов Юникод-16 (`FFFE`).  
  
7.  В **имя файла** Создайте имя файла с расширением XSD.  
  
## <a name="see-also"></a>См. также  
 [Ссылки](../../../../../../docs/framework/data/adonet/sql/linq/reference.md)
