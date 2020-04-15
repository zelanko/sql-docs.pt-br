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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 69a17086253b40469b0ed98cb6f870f319f03f52
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306747"
---
# <a name="using-sqlgetdiagrec-and-sqlgetdiagfield"></a>Usar SQLGetDiagRec e SQLGetDiagField
Os aplicativos chamam **SQLGetDiagRec** ou **SQLGetDiagField** para recuperar informações de diagnóstico. Essas funções aceitam um ambiente, conexão, declaração ou manuseio e retornam diagnósticos da função que usou essa alça pela última vez. Os diagnósticos registrados em uma alça específica são descartados quando uma nova função é chamada usando essa alça. Se a função retornou vários registros de diagnóstico, o aplicativo chamará essas funções várias vezes; o número total de registros de status é recuperado ligando para **SQLGetDiagField** para o registro de cabeçalho (registro 0) com a opção SQL_DIAG_NUMBER.  
  
 Os aplicativos recuperam campos de diagnóstico individuais ligando para **SQLGetDiagField** e especificando o campo a ser recuperado. Certos campos de diagnóstico não têm qualquer significado para certos tipos de alças. Para obter uma lista de campos de diagnóstico e seus significados, consulte a descrição da função [SQLGetDiagField.](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
 Os aplicativos recuperam o SQLSTATE, o código de erro nativo e a mensagem de diagnóstico em uma única chamada, ligando para **sqlGetDiagRec**; **O SQLGetDiagRec** não pode ser usado para recuperar informações do registro de cabeçalho.  
  
 Por exemplo, o código a seguir solicita ao usuário uma instrução SQL e executa-a. Se alguma informação de diagnóstico for devolvida, ela liga para **o SQLGetDiagField** para obter o número de registros de status e **o SQLGetDiagRec** para obter o SQLSTATE, código de erro nativo e mensagem de diagnóstico desses registros.  
  
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
