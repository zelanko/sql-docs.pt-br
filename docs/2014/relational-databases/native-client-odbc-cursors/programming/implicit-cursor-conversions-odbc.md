---
title: Conversões implícitas de cursor (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, implicit cursor conversions
- implicit cursor conversions
- cursors [ODBC], implicit cursor conversions
ms.assetid: fe29a58d-8448-4512-9ffd-b414784ba338
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 300ce02538a59ef043424d866ad4ce49267fcfa4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62711564"
---
# <a name="implicit-cursor-conversions-odbc"></a>Conversões implícitas de cursor (ODBC)
  Os aplicativos podem solicitar um tipo de cursor por meio de [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) e, em seguida, executar uma instrução SQL que não tenha suporte de cursores de servidor do tipo solicitado. Uma chamada para **SQLExecute** ou **SQLExecDirect** retorna SQL_SUCCESS_WITH_INFO e **SQLGetDiagRec** retorna:  
  
```  
szSqlState = "01S02", *pfNativeError = 0,  
szErrorMsg="[Microsoft][SQL Server Native Client] Cursor type changed"  
```  
  
 O aplicativo pode determinar que tipo de cursor está sendo usado agora chamando **SQLGetStmtOption** definido como SQL_CURSOR_TYPE. A conversão do tipo de cursor se aplica somente a uma instrução. O próximo **SQLExecDirect** ou **SQLExecute** será feito usando as configurações de cursor da instrução original.  
  
## <a name="see-also"></a>Consulte Também  
 [Detalhes de programação do cursor &#40;&#41;ODBC](cursor-programming-details-odbc.md)  
  
  
