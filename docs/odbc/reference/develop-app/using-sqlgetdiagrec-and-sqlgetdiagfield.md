---
title: Usando SQLGetDiagRec e SQLGetDiagField | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], and SQLGetDiagRec
- SQLGetDiagRec function [ODBC], and SQLGetDiagField
- diagnostic information [ODBC], SqlGetDiagRec
- retrieving diagnostic information [ODBC]
ms.assetid: 4f486bb1-fad8-4064-ac9d-61f2de85b68b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1db402e7c015ef50ce47b5137e670d9f1836a326
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63208423"
---
# <a name="using-sqlgetdiagrec-and-sqlgetdiagfield"></a>Usar SQLGetDiagRec e SQLGetDiagField
Aplicativos chamam **SQLGetDiagRec** ou **SQLGetDiagField** para recuperar informações de diagnóstico. Essas funções aceitam um identificador de ambiente, conexão, instrução ou descritor e retornam o diagnóstico da função que é usado pela última vez esse identificador. O diagnóstico registrado em um identificador específico é descartado quando uma nova função é chamada usando esse identificador. Se a função retornou vários registros de diagnóstico, o aplicativo chama essas funções várias vezes; o número total de registros de status é recuperado chamando **SQLGetDiagField** para o registro de cabeçalho (record 0) com a opção SQL_DIAG_NUMBER.  
  
 Aplicativos de recuperam campos individuais de diagnóstico, chamando **SQLGetDiagField** e especificando o campo a recuperar. Determinados campos de diagnóstico não tem nenhum significado para determinados tipos de identificadores. Para obter uma lista de campos de diagnóstico e seus significados, consulte o [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) descrição da função.  
  
 Aplicativos recuperam o SQLSTATE, o código de erro nativo e a mensagem de diagnóstico em uma única chamada chamando **SQLGetDiagRec**; **SQLGetDiagRec** não pode ser usado para recuperar informações de registro de cabeçalho.  
  
 Por exemplo, o código a seguir solicita ao usuário uma instrução SQL e o executa. Se as informações de diagnóstico foi retornadas, ele chama **SQLGetDiagField** para obter o número de registros de status e **SQLGetDiagRec** para obter o SQLSTATE, o código de erro nativo e a mensagem de diagnóstico dos registros.  
  
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
   SQLLEN numRecs = 0;
   SQLGetDiagField(SQL_HANDLE_STMT, hstmt, 0, SQL_DIAG_NUMBER, &numRecs, 0, 0);
   // Get the status records.
   i = 1;  
   while (i <= numRecs && (rc2 = SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, i, SqlState, &NativeError,  
            Msg, sizeof(Msg), &MsgLen)) != SQL_NO_DATA) {  
      DisplayError(SqlState,NativeError,Msg,MsgLen);  
      i++;  
   }  
}  
  
if ((rc1 == SQL_SUCCESS) || (rc1 == SQL_SUCCESS_WITH_INFO)) {  
   // Process statement results, if any.  
}  
```
