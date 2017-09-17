---
title: Mapeamento de SQLError | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLError
- SQLError function [ODBC], mapping
ms.assetid: 802ac711-7e5d-4152-9698-db0cafcf6047
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7ebbe17713149276acbe061bfb8ba41503026306
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlerror-mapping"></a>Mapeamento de SQLError
Quando um aplicativo chama **SQLError** por meio de um ODBC 3*. x* driver, a chamada para  
  
```  
SQLError(henv, hdbc, hstmt, szSqlState, pfNativeError, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)   
```  
  
 é mapeado para  
  
```  
SQLGetDiagRec(HandleType, Handle, RecNumber, szSqlstate, pfNativeErrorPtr, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)  
```  
  
 com o *HandleType* argumento definido como o valor SQL_HANDLE_ENV, SQL_HANDLE_DBC ou SQL_HANDLE_STMT, conforme apropriado e o *tratar* argumento definido como o valor em *henv*, *hdbc*, ou *hstmt*, conforme apropriado. O *RecNumber* argumento é determinado pelo Gerenciador de Driver.
