---
title: Mapeamento de SQLError | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLError
- SQLError function [ODBC], mapping
ms.assetid: 802ac711-7e5d-4152-9698-db0cafcf6047
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0ba54875173e6836279db6c043a017af8a191dae
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlerror-mapping"></a>Mapeamento de SQLError
Quando um aplicativo chama **SQLError** por meio de um ODBC 3 *. x* driver, a chamada para  
  
```  
SQLError(henv, hdbc, hstmt, szSqlState, pfNativeError, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)   
```  
  
 é mapeado para  
  
```  
SQLGetDiagRec(HandleType, Handle, RecNumber, szSqlstate, pfNativeErrorPtr, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)  
```  
  
 com o *HandleType* argumento definido como o valor SQL_HANDLE_ENV, SQL_HANDLE_DBC ou SQL_HANDLE_STMT, conforme apropriado e o *tratar* argumento definido como o valor em *henv*, *hdbc*, ou *hstmt*, conforme apropriado. O *RecNumber* argumento é determinado pelo Gerenciador de Driver.
