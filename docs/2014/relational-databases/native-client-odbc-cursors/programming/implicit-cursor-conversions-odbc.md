---
title: Conversões implícitas de Cursor (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, implicit cursor conversions
- implicit cursor conversions
- cursors [ODBC], implicit cursor conversions
ms.assetid: fe29a58d-8448-4512-9ffd-b414784ba338
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 60fabee858409f65a73bb03749a64b532e79d66b
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37422325"
---
# <a name="implicit-cursor-conversions-odbc"></a>Conversões implícitas de cursor (ODBC)
  Os aplicativos podem solicitar um tipo de cursor por meio [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) e, em seguida, executar uma instrução SQL que não é suportada por cursores de servidor do tipo solicitado. Uma chamada para **SQLExecute** ou **SQLExecDirect** retorna SQL_SUCCESS_WITH_INFO e **SQLGetDiagRec** retorna:  
  
```  
szSqlState = "01S02", *pfNativeError = 0,  
szErrorMsg="[Microsoft][SQL Server Native Client] Cursor type changed"  
```  
  
 O aplicativo pode determinar que tipo de cursor está sendo usado agora chamando **SQLGetStmtOption** definido como SQL_CURSOR_TYPE. A conversão do tipo de cursor se aplica somente a uma instrução. A próxima **SQLExecDirect** ou **SQLExecute** será feita usando as configurações de cursor de instrução original.  
  
## <a name="see-also"></a>Consulte também  
 [Detalhes de programação de cursor &#40;ODBC&#41;](cursor-programming-details-odbc.md)  
  
  
