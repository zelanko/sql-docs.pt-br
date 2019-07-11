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
ms.openlocfilehash: 452ee7b5e2c9e38aaf0fb81969228f5c5e7b5559
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793068"
---
# <a name="sqlerror-mapping"></a>Mapeamento SQLError
Quando um aplicativo chama **SQLError** por meio de ODBC *3.x* driver, a chamada para  
  
```  
SQLError(henv, hdbc, hstmt, szSqlState, pfNativeError, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)   
```  
  
 é mapeado para  
  
```  
SQLGetDiagRec(HandleType, Handle, RecNumber, szSqlstate, pfNativeErrorPtr, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)  
```  
  
 com o *HandleType* argumento definido como SQL_HANDLE_ENV, SQL_HANDLE_DBC ou SQL_HANDLE_STMT, o valor conforme apropriado e o *manipular* argumento definido como o valor em *henv*, *hdbc*, ou *hstmt*, conforme apropriado. O *RecNumber* argumento é determinado pelo Gerenciador de Driver.
