---
description: Instruções SQL inseridas pelo usuário
title: Instruções SQL inseridas pelo usuário | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- user-entered SQL statements [ODBC]
- SQL statements [ODBC], constructing
- SQL statements [ODBC], entered by user
ms.assetid: 109af162-93ba-425a-8fe5-49c7dc7cc784
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6d7d7ee7ffc2a4c949173c3eee888e4c41b9e741
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424538"
---
# <a name="sql-statements-entered-by-the-user"></a>Instruções SQL inseridas pelo usuário
Os aplicativos que executam a análise ad hoc também permitem que o usuário insira instruções SQL diretamente. Por exemplo:   
  
```  
SQLCHAR *     Statement, SqlState[6], Msg[SQL_MAX_MESSAGE_LENGTH];  
SQLSMALLINT   i, MsgLen;  
SQLINTEGER    NativeError;  
SQLRETURN     rc1, rc2;  
  
// Prompt user for SQL statement.  
GetSQLStatement(Statement);  
  
// Execute the statement directly. Because it will be executed only once,  
// do not prepare it.  
rc1 = SQLExecDirect(hstmt, Statement, SQL_NTS);  
  
// Process any errors or returned information.  
if ((rc1 == SQL_ERROR) || rc1 == SQL_SUCCESS_WITH_INFO) {  
   i = 1;  
   while ((rc2 = SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, i, SqlState, &NativeError,  
         Msg, sizeof(Msg), &MsgLen)) != SQL_NO_DATA) {  
      DisplayError(SqlState, NativeError, Msg, MsgLen);  
      i++;  
   }  
}  
```  
  
 Essa abordagem simplifica a codificação de aplicativos; o aplicativo depende do usuário para criar a instrução SQL e na fonte de dados para verificar a validade da instrução. Como é difícil escrever uma interface gráfica do usuário que exponha adequadamente as complexidades do SQL, simplesmente pedir ao usuário que insira o texto da instrução SQL pode ser uma alternativa preferida. No entanto, isso exige que o usuário saiba não apenas o SQL, mas também o esquema da fonte de dados que está sendo consultada. Alguns aplicativos fornecem uma interface gráfica do usuário pela qual o usuário pode criar uma instrução SQL básica e também fornecer uma interface de texto com a qual o usuário pode modificá-la.
