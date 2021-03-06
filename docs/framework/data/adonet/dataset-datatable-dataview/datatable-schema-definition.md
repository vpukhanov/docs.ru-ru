---
title: "Определение схемы таблицы данных"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: efbcdda4-f5a9-421d-8be2-4c194c74552f
caps.latest.revision: "4"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: dotnet
ms.openlocfilehash: ae4d5af0238108d0f309ae311e172450bf226c23
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="datatable-schema-definition"></a>Определение схемы таблицы данных
Схема, или структура, таблицы представляется столбцами и ограничениями. Схема <xref:System.Data.DataTable> определяется с использованием объектов <xref:System.Data.DataColumn>, а также объектов <xref:System.Data.ForeignKeyConstraint> и <xref:System.Data.UniqueConstraint>. Столбцы таблицы могут сопоставляться со столбцами источника данных, содержать вычисляемые значения выражений, автоматически увеличивать значения или содержать значения первичного ключа.  
  
 В ссылках по имени на столбцы, связи и ограничения таблицы учитывается регистр. Поэтому в таблице могут существовать столбцы, связи и ограничения, имеющие одинаковое имя, но отличающиеся регистром. Например, можно иметь **Col1** и **col1**. В таком случае ссылка на один из столбцов по имени должна точно соответствовать регистру столбца; в противном случае возникает исключение. Например если таблица **myTable** содержит столбцы **Col1** и **col1**, необходимо предоставить ссылки, **Col1** по имени как  **myTable.Columns["Col1"]**, и **col1** как **myTable.Columns["col1"]**. Попытка сослаться на любую из столбцов, **myTable.Columns["COL1"]** создается исключение.  
  
 Правило учета регистра не применяется, если существует только один столбец, одна связь или ограничение с конкретным именем. Это означает, что если в таблице нет другого объекта столбца, связи или ограничения, имя которого совпадает с именем этого конкретного объекта столбца, связи или ограничения, то на объект можно ссылаться по имени, используя любой регистр, и исключение в этом случае не возникает. Например, если таблица имеет только **Col1**, можно ссылаться с использованием **my. Столбцы [«COL1»]**.  
  
> [!NOTE]
>  <xref:System.Data.DataTable.CaseSensitive%2A> Свойство **DataTable** не влияет на это поведение. **CaseSensitive** свойство применяется, данные в таблице и влияет на сортировку, поиск, фильтрацию, соблюдение ограничений и т. д., но не ссылки на столбцы, связи и ограничения.  
  
## <a name="in-this-section"></a>В этом разделе  
 [Добавление столбцов в DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/adding-columns-to-a-datatable.md)  
 Описывает, как определить столбцы таблицы с использованием **DataColumn** объектов.  
  
 [Создание столбцов выражений](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/creating-expression-columns.md)  
 Объясняет, как **выражение** свойство столбца может использоваться для расчета значений на основе значений из других столбцов в строке.  
  
 [Создание столбцов AutoIncrement](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/creating-autoincrement-columns.md)  
 Описывает, как для столбца может быть установлено автоматическое увеличение числовых значений для обеспечения уникального значения столбца в строке.  
  
 [Определение первичных ключей](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/defining-primary-keys.md)  
 Описывает, как задать первичный ключ таблицы из одного или нескольких **DataColumn** объектов.  
  
 [Ограничения DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatable-constraints.md)  
 Описывает, как определить внешний ключ и ограничения уникальности для столбцов в таблице.  
  
## <a name="see-also"></a>См. также  
 [DataTables](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatables.md)  
 [Центр разработчиков наборов данных и управляемых поставщиков ADO.NET](http://go.microsoft.com/fwlink/?LinkId=217917)
