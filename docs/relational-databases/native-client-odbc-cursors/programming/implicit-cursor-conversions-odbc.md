---
title: Conversões implícitas do cursor (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, implicit cursor conversions
- implicit cursor conversions
- cursors [ODBC], implicit cursor conversions
ms.assetid: fe29a58d-8448-4512-9ffd-b414784ba338
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ced726893b0f287db6b1fec7c8d16c6b844eea2b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298376"
---
# <a name="implicit-cursor-conversions-odbc"></a>Conversões implícitas de cursor (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Os aplicativos podem solicitar um tipo de cursor através [do SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) e, em seguida, executar uma declaração SQL que não é suportada por cursores de servidor do tipo solicitado. Uma chamada para **SQLExecute** ou **SQLExecDirect** retorna SQL_SUCCESS_WITH_INFO e **o SQLGetDiagRec** retorna:  
  
```  
szSqlState = "01S02", *pfNativeError = 0,  
szErrorMsg="[Microsoft][SQL Server Native Client] Cursor type changed"  
```  
  
 O aplicativo pode determinar que tipo de cursor está sendo usado agora ligando para **SQLGetStmtOption** definido como SQL_CURSOR_TYPE. A conversão do tipo de cursor se aplica somente a uma instrução. O próximo **SQLExecDirect** ou **SQLExecute** será feito usando as configurações do cursor de declaração original.  
  
## <a name="see-also"></a>Consulte Também  
 [Detalhes da programação do cursor &#40;&#41;da ODBC](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
