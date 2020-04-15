---
title: Escrevendo Drivers ODBC 3.x | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- upgrading drivers [ODBC]
- ODBC drivers [ODBC], upgrading
- backward compatibility [ODBC], drivers
- compatibility [ODBC], drivers
ms.assetid: 9b75f59b-623f-4711-9ca2-e751b3622e00
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 62f2a701fd5ac94c92d41494a4fd1ab023edaf25
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300356"
---
# <a name="writing-odbc-3x-drivers"></a>Gravar drivers 3.x ODBC
A tabela a seguir mostra suporte de função em um ODBC 3. *x* driver e um aplicativo ODBC, e o mapeamento realizado pelo Driver Manager quando as funções são chamadas contra um ODBC 3. *x* driver.  
  
|Função|Com suporte<br /><br /> por um<br /><br /> ODBC 3. *x*<br /><br /> Driver?|Com suporte<br /><br /> por um<br /><br /> ODBC 3. *x*<br /><br /> Aplicativo?|Mapeado/suportado<br /><br /> pelo ODBC 3. *x*<br /><br /> Driver Manager para<br /><br /> um ODBC 3. *x* driver?|  
|--------------|----------------------------------------------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------|  
|**SQLAllocConnect**|Não|Não[1]|Sim|  
|**SQLAllocEnv**|Não|Não[1]|Sim|  
|**SQLAllocHandle**|Sim|Sim|Não|  
|**SQLAllocStmt**|Não|Não[1]|Sim|  
|**SQLBindCol**|Sim|Sim|Não|  
|**SQLBindParam**|Não|Sim[2]|Sim|  
|**SQLBindParameter**|Sim|Sim|Não|  
|**SQLBrowseConnect**|Sim|Sim|Não|  
|**SQLBulkOperations**|Sim|Sim|Não|  
|**SQLCancel**|Sim|Sim|Não|  
|**SQLCloseCursor**|Sim|Sim|Não|  
|**SQLColAttribute**|Sim|Sim|Não|  
|**SQLColAttributea**|Não[3]|Não|Sim|  
|**SQLColumnPrivileges**|Sim|Sim|Não|  
|**SQLColumns**|Sim|Sim|Não|  
|**SQLConnect**|Sim|Sim|Não|  
|**SQLCopyDesc**|Sim|Sim|Sim[4]|  
|**SQLDataSources**|Não|Sim|Sim|  
|**SQLDescribeCol**|Sim|Sim|Não|  
|**SQLDescribeParam**|Sim|Sim|Não|  
|**Sqldisconnect**|Sim|Sim|Não|  
|**SQLDriverConnect**|Sim|Sim|Não|  
|**SQLDrivers**|Não|Sim|Sim|  
|**SQLEndTran**|Sim|Sim|Não|  
|**Sqlerror**|Não|Não[1]|Sim|  
|**SQLExecDirect**|Sim|Sim|Não|  
|**SQLExecute**|Sim|Sim|Não|  
|**Sqlextendedfetch**|Sim|Não|Não|  
|**SQLFetch**|Sim|Sim|Não|  
|**SQLFetchScroll**|Sim|Sim|Não|  
|**SQLForeignKeys**|Sim|Sim|Não|  
|**SQLFreeConnect**|Não|Sim[1]|Sim|  
|**SQLFreeEnv**|Não|Sim[1]|Sim|  
|**SQLFreeHandle**|Sim|Sim|Não|  
|**SQLFreeStmt**|Sim|Sim|Não|  
|**SQLGetConnectAttr**|Sim|Sim|Não|  
|**Opção SQLGetConnect**|Não[5]|Não[1]|Sim|  
|**SQLGetCursorName**|Sim|Sim|Não|  
|**SQLGetData**|Sim|Sim|Não|  
|**SQLGetDescField**|Sim|Sim|Não|  
|**SQLGetDescRec**|Sim|Sim|Não|  
|**SQLGetDiagField**|Sim|Sim|Não|  
|**SQLGetDiagRec**|Sim|Sim|Não|  
|**SQlGetEnvAttr**|Sim|Sim|Não|  
|**SQLGetFunctions**|Não[6]|Sim|Sim|  
|**SQLGetInfo**|Sim|Sim|Não|  
|**SQLGetStmtAttr**|Sim|Sim|Não|  
|**Opção SQLGetStmt**|Não[5]|Não[1]|Sim|  
|**SQLGetTypeInfo**|Sim|Sim|Não|  
|**SQLMoreResults**|Sim|Sim|Não|  
|**SQLNativeSql**|Sim|Sim|Não|  
|**SQLNumParams**|Sim|Sim|Não|  
|**SQLNumResultCols**|Sim|Sim|Não|  
|**SQLParamData**|Sim|Sim|Não|  
|**Opções de SQLParam**|Não|Não|Sim|  
|**SQLPrepare**|Sim|Sim|Não|  
|**SQLPrimaryKeys**|Sim|Sim|Não|  
|**SQLProcedureColumns**|Sim|Sim|Não|  
|**SQLProcedures**|Sim|Sim|Não|  
|**SQLPutData**|Sim|Sim|Não|  
|**SQLRowCount**|Sim|Sim|Não|  
|**SQLSetConnectAttr**|Sim|Sim|Não|  
|**Sqlsetconnectoption**|Não[5]|Não[1]|Sim|  
|**Sqlsetcursorname**|Sim|Sim|Não|  
|**SQLSetDescField**|Sim|Sim|Não|  
|**SQLSetDescRec**|Sim|Sim|Não|  
|**SQLSetEnvAttr**|Sim|Sim|Não|  
|**SQLSetPos**|Sim|Sim|Não|  
|**SQLSetParam**|Não|Não|Sim|  
|**SQLSetScrollOption**|Sim|Sim|Não|  
|**SQLSetStmtAttr**|Sim|Sim|Não|  
|**SQLSetStmtOpção**|Não[5]|Não[1]|Sim|  
|**SQLSpecialColumns**|Sim|Sim|Não|  
|**SQLStatistics**|Sim|Sim|Não|  
|**SQLTablePrivileges**|Sim|Sim|Não|  
|**SQLTables**|Sim|Sim|Não|  
|**SQLTransact**|Não|Não[1]|Sim|  
  
 [1] Esta função é preterida em ODBC 3. *x*. ODBC 3. *x* aplicativos não devem usar esta função. No entanto, um aplicativo compatível com CLI do Grupo Aberto ou ISO pode chamar essa função.  
  
 [2] ODBC 3. *os* aplicativos x devem usar **SQLBindParameter** em vez de **SQLBindParam**. No entanto, um aplicativo compatível com CLI do Grupo Aberto ou ISO pode chamar essa função.  
  
 [3] Os escritores de driver devem notar que o ODBC 2. *x* atributos de coluna SQL_COLUMN_PRECISION, SQL_COLUMN_SCALE e SQL_COLUMN_LENGTH devem ser suportados com **SQLColAttribute**.  
  
 [4] **O SQLCopyDesc** é parcialmente implementado pelo Driver Manager quando um descritor está sendo copiado entre conexões que pertencem a diferentes drivers. Os drivers são necessários para suportar **o SQLCopyDesc** em duas de suas próprias conexões. Funções como **SQLDrivers**, que são implementadas exclusivamente pelo Driver Manager, não aparecem nesta lista.  
  
 [5] Em certas circunstâncias, os motoristas podem precisar suportar essa função. Para obter mais informações, consulte a página de referência desta função.  
  
 [6] O driver pode optar por suportar **SQLGetFunctions** se o conjunto de funções que o driver suporta variar de conexão para conexão.
