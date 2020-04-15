---
title: Mapeamento SQLTransact | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLTransact
- SQLTransact function [ODBC], mapping
ms.assetid: 8a01041f-3572-46f9-8213-b817f3cf929c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6aaa056fca860a70f81ad7c3a4cd8539512bc25d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304877"
---
# <a name="sqltransact-mapping"></a>Mapeamento SQLTransact
**SQLTransact** agora é substituído por **SQLEndTran**. A maior diferença entre as duas funções é que **o SQLEndTran** contém um argumento *HandleType*, que especifica o escopo do trabalho a ser feito. O argumento *HandleType* pode especificar o ambiente ou o cabo de conexão. A seguinte chamada para **SQLTransact**:  
  
```  
SQLTransact(henv, hdbc, fType)  
```  
  
 é mapeado para  
  
```  
SQLEndTran(SQL_HANDLE_DBC, ConnectionHandle, CompletionType);  
```  
  
 se *ConnectionHandle* não for igual a SQL_NULL_HDBC. O argumento *ConnectionHandle* é definido como o valor do *hdbc*.  
  
 **SQL_Transact** é mapeado para  
  
```  
SQLEndTran (SQL_HANDLE_ENV, EnvironmentHandle, CompletionType);  
```  
  
 se *ConnectionHandle* for igual a SQL_NULL_HDBC. O argumento *EnvironmentHandle* é definido para o valor de *henv*.  
  
 Em ambos os casos anteriores, o argumento *CompletType* é definido para o mesmo valor que *fType*.
