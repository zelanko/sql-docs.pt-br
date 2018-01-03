---
title: Usando SQLGetDiagRec e SQLGetDiagField | Microsoft Docs
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
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], and SQLGetDiagRec
- SQLGetDiagRec function [ODBC], and SQLGetDiagField
- diagnostic information [ODBC], SqlGetDiagRec
- retrieving diagnostic information [ODBC]
ms.assetid: 4f486bb1-fad8-4064-ac9d-61f2de85b68b
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3be99267a7b2b5395a03c6a5a03fd9b6c33742e8
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="using-sqlgetdiagrec-and-sqlgetdiagfield"></a>Usando SQLGetDiagRec e SQLGetDiagField
Aplicativos chamam **SQLGetDiagRec** ou **SQLGetDiagField** para recuperar informações de diagnóstico. Essas funções aceitam um identificador de ambiente, conexão, instrução ou descritor e retornam o diagnóstico da função que esse identificador usado pela última vez. O diagnóstico de logon de um identificador específico será descartado quando uma nova função é chamada usando esse identificador. Se a função retornou vários registros de diagnósticos, o aplicativo chama essas funções várias vezes; o número total de registros de status é recuperado pela chamada **SQLGetDiagField** para o registro de cabeçalho (record 0) com a opção SQL_DIAG_NUMBER.  
  
 Aplicativos recuperam campos individuais de diagnósticos chamando **SQLGetDiagField** e especificando o campo a recuperar. Alguns campos de diagnósticos não tem nenhum significado para determinados tipos de identificadores. Para obter uma lista de campos de diagnóstico e seus significados, consulte o [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) descrição da função.  
  
 Aplicativos recuperam o SQLSTATE, o código de erro nativo e a mensagem de diagnóstico em uma única chamada chamando **SQLGetDiagRec**; **SQLGetDiagRec** não pode ser usado para recuperar as informações de registro de cabeçalho.  
  
 Por exemplo, o código a seguir solicita ao usuário uma instrução SQL e executa-o. Se quaisquer informações de diagnóstico foi retornadas, ele chama **SQLGetDiagField** para obter o número de registros de status e **SQLGetDiagRec** para obter o SQLSTATE, o código de erro nativo e a mensagem de diagnóstico dos registros.  
  
```  
SQLCHAR       SqlState[6], SQLStmt[100], Msg[SQL_MAX_MESSAGE_LENGTH];  
SQLINTEGER    NativeError;  
SQLSMALLINT   i, MsgLen;  
SQLRETURN     rc1, rc2;  
SQLHSTMT      hstmt;  
  
// Prompt the user for an SQL statement.  
GetSQLStmt(SQLStmt);  
  
// Execute the SQL statement and return any errors or warnings.  
rc1 = SQLExecDirect(hstmt, SQLStmt, SQL_NTS);  
if ((rc1 == SQL_SUCCESS_WITH_INFO) || (rc1 == SQL_ERROR)) {  
   // Get the status records.  
   i = 1;  
   while ((rc2 = SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, i, SqlState, &NativeError,  
            Msg, sizeof(Msg), &MsgLen)) != SQL_NO_DATA) {  
      DisplayError(SqlState,NativeError,Msg,MsgLen);  
      i++;  
   }  
}  
  
if ((rc1 == SQL_SUCCESS) || (rc1 == SQL_SUCCESS_WITH_INFO)) {  
   // Process statement results, if any.  
}  
```
