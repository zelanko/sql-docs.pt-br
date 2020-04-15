---
title: Declarações SQL inseridas pelo Usuário | Microsoft Docs
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
ms.openlocfilehash: bf2f8cf36be392cb42a970fa2fb0b19c35daeb39
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301957"
---
# <a name="sql-statements-entered-by-the-user"></a>Instruções SQL inseridas pelo usuário
Aplicativos que realizam análise ad hoc também geralmente permitem que o usuário insira declarações SQL diretamente. Por exemplo:  
  
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
  
 Essa abordagem simplifica a codificação de aplicativos; o aplicativo depende do usuário para construir a declaração SQL e na fonte de dados para verificar a validade da declaração. Como é difícil escrever uma interface gráfica de usuário que exponha adequadamente os meandros do SQL, simplesmente pedir ao usuário para inserir o texto da declaração SQL pode ser uma alternativa preferível. No entanto, isso exige que o usuário saiba não apenas do SQL, mas também do esquema da fonte de dados que está sendo consultada. Alguns aplicativos fornecem uma interface gráfica de usuário pela qual o usuário pode criar uma declaração SQL básica e também fornecer uma interface de texto com a qual o usuário pode modificá-lo.
