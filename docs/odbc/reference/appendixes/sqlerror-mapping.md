---
title: Mapeamento SQLError | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLError
- SQLError function [ODBC], mapping
ms.assetid: 802ac711-7e5d-4152-9698-db0cafcf6047
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4a278609ee53fe7898d32c1986da2650202b8a98
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199471"
---
# <a name="sqlerror-mapping"></a>Mapeamento SQLError
Quando um aplicativo chama **SQLError** por meio de um ODBC 3 *. x* driver, a chamada para  
  
```  
SQLError(henv, hdbc, hstmt, szSqlState, pfNativeError, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)   
```  
  
 é mapeado para  
  
```  
SQLGetDiagRec(HandleType, Handle, RecNumber, szSqlstate, pfNativeErrorPtr, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)  
```  
  
 com o *HandleType* argumento definido como SQL_HANDLE_ENV, SQL_HANDLE_DBC ou SQL_HANDLE_STMT, o valor conforme apropriado e o *manipular* argumento definido como o valor em *henv*, *hdbc*, ou *hstmt*, conforme apropriado. O *RecNumber* argumento é determinado pelo Gerenciador de Driver.
