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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b2082a97b24284afcc879048bb08e86a7b2bb3ba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070107"
---
# <a name="sqltransact-mapping"></a>Mapeamento SQLTransact
**SQLTransact** agora é substituído por **SQLEndTran**. A principal diferença entre as duas funções é que **SQLEndTran** contém um argumento *HandleType*, que especifica o escopo do trabalho a ser feito. O *HandleType* argumento pode especificar o ambiente ou o identificador de conexão. A seguinte chamada para **SQLTransact**:  
  
```  
SQLTransact(henv, hdbc, fType)  
```  
  
 é mapeado para  
  
```  
SQLEndTran(SQL_HANDLE_DBC, ConnectionHandle, CompletionType);  
```  
  
 Se *ConnectionHandle* não é igual a SQL_NULL_HDBC. O *ConnectionHandle* argumento é definido como o valor de *hdbc*.  
  
 **SQL_Transact** é mapeado para  
  
```  
SQLEndTran (SQL_HANDLE_ENV, EnvironmentHandle, CompletionType);  
```  
  
 Se *ConnectionHandle* é igual a SQL_NULL_HDBC. O *EnvironmentHandle* argumento é definido como o valor de *henv*.  
  
 Em ambos os casos anteriores, o *CompletionType* argumento é definido como o mesmo valor de *fType*.
