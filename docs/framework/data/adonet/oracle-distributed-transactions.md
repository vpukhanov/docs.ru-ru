---
title: "Распределенные транзакции Oracle"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c340ca81-ef79-402f-b204-c5156b890fe5
caps.latest.revision: "3"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: dotnet
ms.openlocfilehash: c901ccf9132dc766d78efb24428b6469458a70fa
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="oracle-distributed-transactions"></a>Распределенные транзакции Oracle
Объект <xref:System.Data.OracleClient.OracleConnection> автоматически прикрепляется к существующей распределенной транзакции, если он определяет, что транзакция активна. Автоматическое прикрепление к транзакции происходит при открытии соединения или его получении из пула соединений. Автоматическое прикрепление к существующим транзакциям можно отменить, задав  
  
```  
Enlist=false  
```  
  
 в качестве параметра строки соединения для <xref:System.Data.OracleClient.OracleConnection>.  
  
## <a name="see-also"></a>См. также  
 [Oracle и ADO.NET](../../../../docs/framework/data/adonet/oracle-and-adonet.md)  
 [Центр разработчиков наборов данных и управляемых поставщиков ADO.NET](http://go.microsoft.com/fwlink/?LinkId=217917)
