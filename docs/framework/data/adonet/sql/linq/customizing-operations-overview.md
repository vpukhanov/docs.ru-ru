---
title: "Настройка операций. Общие сведения"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a3546296-1443-4b88-aa6e-d41011041ba7
caps.latest.revision: "2"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: dotnet
ms.openlocfilehash: 6d3491ccd183224063c435f6b377f60b175d5383
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="customizing-operations-overview"></a>Настройка операций. Общие сведения
По умолчанию [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] создает динамический код SQL для операций вставки, обновления и удаления на основе сопоставления. Однако на практике часто приходится добавлять собственную бизнес-логику для обеспечения безопасности, выполнения проверок и т. д.  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]Ниже перечислены методы для настройки этих операций.  
  
## <a name="loading-options"></a>Возможности загрузки  
 В запросах можно определять, какой объем данных, связанных с основными целевыми объектами, должен извлекаться при подключении к базе данных. Эта функциональная возможность реализуется, в первую очередь, посредством использования параметров <xref:System.Data.Linq.DataLoadOptions>. Дополнительные сведения см. в разделе [отложенное или немедленное загрузки](../../../../../../docs/framework/data/adonet/sql/linq/deferred-versus-immediate-loading.md).  
  
## <a name="partial-methods"></a>Разделяемые методы  
 При использовании сопоставления по умолчанию технология [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] предоставляет разделяемые методы, которые можно использовать для реализации пользовательской бизнес-логики. Дополнительные сведения см. в разделе [Добавление бизнес логики, с помощью разделяемых методов](../../../../../../docs/framework/data/adonet/sql/linq/adding-business-logic-by-using-partial-methods.md).  
  
## <a name="stored-procedures-and-user-defined-functions"></a>Хранимые процедуры и пользовательские функции  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]поддерживает использование хранимых процедур и определяемых пользователем функций. Хранимые процедуры часто используются для настройки операций. Дополнительные сведения см. в разделе [Хранимые процедуры](../../../../../../docs/framework/data/adonet/sql/linq/stored-procedures.md).  
  
## <a name="see-also"></a>См. также  
 [Настройка операций вставки, обновления и удаления](../../../../../../docs/framework/data/adonet/sql/linq/customizing-insert-update-and-delete-operations.md)
