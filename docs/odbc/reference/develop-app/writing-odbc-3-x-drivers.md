---
title: Gravando drivers ODBC 3. x | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300356"
---
# <a name="writing-odbc-3x-drivers"></a>Gravar drivers 3.x ODBC
A tabela a seguir mostra o suporte de função em um ODBC 3. Driver *x* e um aplicativo ODBC e o mapeamento executado pelo Gerenciador de driver quando as funções são chamadas em relação a um ODBC 3. Driver *x* .  
  
|Função|Com suporte<br /><br /> por um<br /><br /> ODBC 3. *x*<br /><br /> Driver?|Com suporte<br /><br /> por um<br /><br /> ODBC 3. *x*<br /><br /> aplicativo?|Mapeado/com suporte<br /><br /> pelo ODBC 3. *x*<br /><br /> Gerenciador de driver para<br /><br /> um ODBC 3. Driver *x* ?|  
|--------------|----------------------------------------------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------|  
|**SQLAllocConnect**|Não|Não [1]|Sim|  
|**SQLAllocEnv**|Não|Não [1]|Sim|  
|**SQLAllocHandle**|Sim|Sim|Não|  
|**SQLAllocStmt**|Não|Não [1]|Sim|  
|**SQLBindCol**|Sim|Sim|Não|  
|**SQLBindParam**|Não|Sim [2]|Sim|  
|**SQLBindParameter**|Sim|Sim|Não|  
|**SQLBrowseConnect**|Sim|Sim|Não|  
|**SQLBulkOperations**|Sim|Sim|Não|  
|**SQLCancel**|Sim|Sim|Não|  
|**SQLCloseCursor**|Sim|Sim|Não|  
|**SQLColAttribute**|Sim|Sim|Não|  
|**SQLColAttributes**|Não [3]|Não|Sim|  
|**SQLColumnPrivileges**|Sim|Sim|Não|  
|**SQLColumns**|Sim|Sim|Não|  
|**SQLConnect**|Sim|Sim|Não|  
|**SQLCopyDesc**|Sim|Sim|Sim [4]|  
|**SQLDataSources**|Não|Sim|Sim|  
|**SQLDescribeCol**|Sim|Sim|Não|  
|**SQLDescribeParam**|Sim|Sim|Não|  
|**SQLDisconnect**|Sim|Sim|Não|  
|**SQLDriverConnect**|Sim|Sim|Não|  
|**SQLDrivers**|Não|Sim|Sim|  
|**SQLEndTran**|Sim|Sim|Não|  
|**SQLError**|Não|Não [1]|Sim|  
|**SQLExecDirect**|Sim|Sim|Não|  
|**SQLExecute**|Sim|Sim|Não|  
|**SQLExtendedFetch**|Sim|Não|Não|  
|**SQLFetch**|Sim|Sim|Não|  
|**SQLFetchScroll**|Sim|Sim|Não|  
|**SQLForeignKeys**|Sim|Sim|Não|  
|**SQLFreeConnect**|Não|Sim [1]|Sim|  
|**SQLFreeEnv**|Não|Sim [1]|Sim|  
|**SQLFreeHandle**|Sim|Sim|Não|  
|**SQLFreeStmt**|Sim|Sim|Não|  
|**SQLGetConnectAttr**|Sim|Sim|Não|  
|**SQLGetConnectOption**|Não [5]|Não [1]|Sim|  
|**SQLGetCursorName**|Sim|Sim|Não|  
|**SQLGetData**|Sim|Sim|Não|  
|**SQLGetDescField**|Sim|Sim|Não|  
|**SQLGetDescRec**|Sim|Sim|Não|  
|**SQLGetDiagField**|Sim|Sim|Não|  
|**SQLGetDiagRec**|Sim|Sim|Não|  
|**SQLGetEnvAttr**|Sim|Sim|Não|  
|**SQLGetFunctions**|Não [6]|Sim|Sim|  
|**SQLGetInfo**|Sim|Sim|Não|  
|**SQLGetStmtAttr**|Sim|Sim|Não|  
|**SQLGetStmtOption**|Não [5]|Não [1]|Sim|  
|**SQLGetTypeInfo**|Sim|Sim|Não|  
|**SQLMoreResults**|Sim|Sim|Não|  
|**SQLNativeSql**|Sim|Sim|Não|  
|**SQLNumParams**|Sim|Sim|Não|  
|**SQLNumResultCols**|Sim|Sim|Não|  
|**SQLParamData**|Sim|Sim|Não|  
|**SQLParamOptions**|Não|Não|Sim|  
|**SQLPrepare**|Sim|Sim|Não|  
|**SQLPrimaryKeys**|Sim|Sim|Não|  
|**SQLProcedureColumns**|Sim|Sim|Não|  
|**SQLProcedures**|Sim|Sim|Não|  
|**SQLPutData**|Sim|Sim|Não|  
|**SQLRowCount**|Sim|Sim|Não|  
|**SQLSetConnectAttr**|Sim|Sim|Não|  
|**SQLSetConnectOption**|Não [5]|Não [1]|Sim|  
|**SQLSetCursorName**|Sim|Sim|Não|  
|**SQLSetDescField**|Sim|Sim|Não|  
|**SQLSetDescRec**|Sim|Sim|Não|  
|**SQLSetEnvAttr**|Sim|Sim|Não|  
|**SQLSetPos**|Sim|Sim|Não|  
|**SQLSetParam**|Não|Não|Sim|  
|**SQLSetScrollOption**|Sim|Sim|Não|  
|**SQLSetStmtAttr**|Sim|Sim|Não|  
|**SQLSetStmtOption**|Não [5]|Não [1]|Sim|  
|**SQLSpecialColumns**|Sim|Sim|Não|  
|**SQLStatistics**|Sim|Sim|Não|  
|**SQLTablePrivileges**|Sim|Sim|Não|  
|**SQLTables**|Sim|Sim|Não|  
|**SQLTransact**|Não|Não [1]|Sim|  
  
 [1] Esta função foi preterida no ODBC 3. *x*. ODBC 3. os aplicativos *x* não devem usar essa função. No entanto, um grupo aberto ou um aplicativo compatível com CLI ISO pode chamar essa função.  
  
 [2] ODBC 3. os aplicativos *x* devem usar **SQLBindParameter** em vez de **SQLBindParam**. No entanto, um grupo aberto ou um aplicativo compatível com CLI ISO pode chamar essa função.  
  
 [3] os gravadores de driver devem observar que o ODBC 2. os atributos de coluna *x* SQL_COLUMN_PRECISION, SQL_COLUMN_SCALE e SQL_COLUMN_LENGTH devem ter suporte com **SQLColAttribute**.  
  
 [4] **SQLCopyDesc** é parcialmente implementado pelo Gerenciador de driver quando um descritor está sendo copiado entre conexões que pertencem a drivers diferentes. Os drivers são necessários para dar suporte a **SQLCopyDesc** em duas de suas próprias conexões. Funções como **SQLDrivers**, que são implementadas exclusivamente pelo Gerenciador de driver, não aparecem nessa lista.  
  
 [5] em determinadas circunstâncias, os drivers podem precisar dar suporte a essa função. Para obter mais informações, consulte a página de referência da função.  
  
 [6] o driver pode optar por dar suporte a **SQLGetFunctions** se o conjunto de funções que o driver dá suporte varia da conexão com a conexão.
