---
title: Mapeamento de SQLTransact | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLTransact
- SQLTransact function [ODBC], mapping
ms.assetid: 8a01041f-3572-46f9-8213-b817f3cf929c
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4e1e9d43a6e968d20042eff30552223c87813a86
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="sqltransact-mapping"></a>Mapeamento de SQLTransact
**SQLTransact** é agora substituído pelo **SQLEndTran**. A principal diferença entre as duas funções é que **SQLEndTran** contém um argumento *HandleType*, que especifica o escopo do trabalho a ser feito. O *HandleType* argumento pode especificar o ambiente ou o identificador de conexão. A seguinte chamada para **SQLTransact**:  
  
```  
SQLTransact(henv, hdbc, fType)  
```  
  
 é mapeado para  
  
```  
SQLEndTran(SQL_HANDLE_DBC, ConnectionHandle, CompletionType);  
```  
  
 Se *identificador da conexão* não é igual a SQL_NULL_HDBC. O *identificador da conexão* argumento é definido como o valor de *hdbc*.  
  
 **SQL_Transact** é mapeado para  
  
```  
SQLEndTran (SQL_HANDLE_ENV, EnvironmentHandle, CompletionType);  
```  
  
 Se *identificador da conexão* é igual a SQL_NULL_HDBC. O *EnvironmentHandle* argumento é definido como o valor de *henv*.  
  
 Em ambos os casos anteriores, o *CompletionType* argumento é definido como o mesmo valor como *fType*.
