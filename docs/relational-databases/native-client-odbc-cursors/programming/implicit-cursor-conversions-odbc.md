---
title: Conversões implícitas de Cursor (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-cursors
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, implicit cursor conversions
- implicit cursor conversions
- cursors [ODBC], implicit cursor conversions
ms.assetid: fe29a58d-8448-4512-9ffd-b414784ba338
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d6d03a04c6c46941dc205d791029de5b63acaff0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="implicit-cursor-conversions-odbc"></a>Conversões implícitas de cursor (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Os aplicativos podem solicitar um tipo de cursor por meio de [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) e, em seguida, executar uma instrução SQL que não é suportada por cursores de servidor do tipo solicitado. Uma chamada para **SQLExecute** ou **SQLExecDirect** retorna SQL_SUCCESS_WITH_INFO e **SQLGetDiagRec** retorna:  
  
```  
szSqlState = "01S02", *pfNativeError = 0,  
szErrorMsg="[Microsoft][SQL Server Native Client] Cursor type changed"  
```  
  
 O aplicativo pode determinar que tipo de cursor está sendo usado agora chamando **SQLGetStmtOption** definido como SQL_CURSOR_TYPE. A conversão do tipo de cursor se aplica somente a uma instrução. O próximo **SQLExecDirect** ou **SQLExecute** será feita usando as configurações originais do cursor de instrução.  
  
## <a name="see-also"></a>Consulte também  
 [Detalhes da programação de cursor &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
