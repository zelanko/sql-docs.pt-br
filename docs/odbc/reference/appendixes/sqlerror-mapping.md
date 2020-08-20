---
description: Mapeamento SQLError
title: Mapeamento de SQLError | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5d18d1b25acbbe56f29555274a7b8d995b7355d0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466018"
---
# <a name="sqlerror-mapping"></a>Mapeamento SQLError
Quando um aplicativo chama **SqlError** por meio de um driver ODBC *3. x* , a chamada para  
  
```  
SQLError(henv, hdbc, hstmt, szSqlState, pfNativeError, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)   
```  
  
 está mapeado para  
  
```  
SQLGetDiagRec(HandleType, Handle, RecNumber, szSqlstate, pfNativeErrorPtr, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)  
```  
  
 com o argumento *HandleType* definido como o valor SQL_HANDLE_ENV, SQL_HANDLE_DBC ou SQL_HANDLE_STMT, conforme apropriado, e o argumento *Handle* definido como o valor em *HENV*, *HDBC*ou *HSTMT*, conforme apropriado. O argumento *RecNumber* é determinado pelo Gerenciador de driver.
