---
title: "Сопоставления типов данных ODBC"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 43c35d32-831d-480f-a150-78f7e869d17f
caps.latest.revision: "3"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: dotnet
ms.openlocfilehash: 6c383207c8290932c407af8c317775b5943b5450
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="odbc-data-type-mappings"></a>Сопоставления типов данных ODBC
В приведенной ниже таблице показаны выводимые типы [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] для типов данных поставщика данных .NET Framework для ODBC (<xref:System.Data.Odbc>). Приведены также типизированные методы доступа для <xref:System.Data.Odbc.OdbcDataReader>.  
  
|Тип ODBC|Тип [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]|Типизированный метод доступа [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]|  
|---------------|----------------------------------------------------------------------|--------------------------------------------------------------------------------|  
|SQL_BIGINT|Int64|GetInt64()|  
|SQL_BINARY|Byte[]|GetBytes()|  
|SQL_BIT|Boolean|GetBoolean()|  
|SQL_CHAR|Строковое<br /><br /> Char[]|GetString()<br /><br /> GetChars()|  
|SQL_DECIMAL|Десятичное число|GetDecimal()|  
|SQL_DOUBLE|Double|GetDouble()|  
|SQL_GUID|Guid|GetGuid()|  
|SQL_INTEGER|Int32|GetInt32()|  
|SQL_LONG_VARCHAR|Строковое<br /><br /> Char[]|GetString()<br /><br /> GetChars()|  
|SQL_LONGVARBINARY|Byte[]|GetBytes()|  
|SQL_NUMERIC|Десятичное число|GetDecimal()|  
|SQL_REAL|Single|GetFloat()|  
|SQL_SMALLINT|Int16|GetInt16()|  
|SQL_TINYINT|Byte|GetByte()|  
|SQL_TYPE_TIMES|DateTime|GetDateTime()|  
|SQL_TYPE_TIMESTAMP|DateTime|GetDateTime()|  
|SQL_VARBINARY|Byte[]|GetBytes()|  
|SQL_WCHAR|Строковое<br /><br /> Char[]|GetString()<br /><br /> GetChars()|  
|SQL_WLONGVARCHAR|Строковое<br /><br /> Char[]|GetString()<br /><br /> GetChars()|  
|SQL_WVARCHAR|Строковое<br /><br /> Char[]|GetString()<br /><br /> GetChars()|  
  
## <a name="see-also"></a>См. также  
 [Извлечение и изменение данных в ADO.NET](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)  
 [Центр разработчиков наборов данных и управляемых поставщиков ADO.NET](http://go.microsoft.com/fwlink/?LinkId=217917)
