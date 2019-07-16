---
title: Gravando Drivers 3.x ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fb403cef47f901cdb43bbb32c669ba68aa34913d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078901"
---
# <a name="writing-odbc-3x-drivers"></a>Gravar drivers 3.x ODBC
A tabela a seguir mostra o suporte de função em um ODBC 3. *x* driver e um aplicativo ODBC e o mapeamento realizada pelo Gerenciador de Driver quando as funções são chamadas em relação a um ODBC 3. *x* driver.  
  
|Função|Tem suporte<br /><br /> por um<br /><br /> ODBC 3. *x*<br /><br /> driver?|Tem suporte<br /><br /> por um<br /><br /> ODBC 3. *x*<br /><br /> aplicativo?|Mapeado/com suporte<br /><br /> Por que o ODBC 3. *x*<br /><br /> Gerenciador de driver para<br /><br /> um ODBC 3. *x* driver?|  
|--------------|----------------------------------------------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------|  
|**SQLAllocConnect**|Não|Nenhum [1]|Sim|  
|**SQLAllocEnv**|Não|Nenhum [1]|Sim|  
|**SQLAllocHandle**|Sim|Sim|Não|  
|**SQLAllocStmt**|Não|Nenhum [1]|Sim|  
|**SQLBindCol**|Sim|Sim|Não|  
|**SQLBindParam**|Não|Sim [2]|Sim|  
|**SQLBindParameter**|Sim|Sim|Não|  
|**SQLBrowseConnect**|Sim|Sim|Não|  
|**SQLBulkOperations**|Sim|Sim|Não|  
|**SQLCancel**|Sim|Sim|Não|  
|**SQLCloseCursor**|Sim|Sim|Não|  
|**SQLColAttribute**|Sim|Sim|Não|  
|**SQLColAttributes**|Nenhum [3]|Não|Sim|  
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
|**SQLError**|Não|Nenhum [1]|Sim|  
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
|**SQLGetConnectOption**|Nenhum [5]|Nenhum [1]|Sim|  
|**SQLGetCursorName**|Sim|Sim|Não|  
|**SQLGetData**|Sim|Sim|Não|  
|**SQLGetDescField**|Sim|Sim|Não|  
|**SQLGetDescRec**|Sim|Sim|Não|  
|**SQLGetDiagField**|Sim|Sim|Não|  
|**SQLGetDiagRec**|Sim|Sim|Não|  
|**SQLGetEnvAttr**|Sim|Sim|Não|  
|**SQLGetFunctions**|Nenhum [6]|Sim|Sim|  
|**SQLGetInfo**|Sim|Sim|Não|  
|**SQLGetStmtAttr**|Sim|Sim|Não|  
|**SQLGetStmtOption**|Nenhum [5]|Nenhum [1]|Sim|  
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
|**SQLSetConnectOption**|Nenhum [5]|Nenhum [1]|Sim|  
|**SQLSetCursorName**|Sim|Sim|Não|  
|**SQLSetDescField**|Sim|Sim|Não|  
|**SQLSetDescRec**|Sim|Sim|Não|  
|**SQLSetEnvAttr**|Sim|Sim|Não|  
|**SQLSetPos**|Sim|Sim|Não|  
|**SQLSetParam**|Não|Não|Sim|  
|**SQLSetScrollOption**|Sim|Sim|Não|  
|**SQLSetStmtAttr**|Sim|Sim|Não|  
|**SQLSetStmtOption**|Nenhum [5]|Nenhum [1]|Sim|  
|**SQLSpecialColumns**|Sim|Sim|Não|  
|**SQLStatistics**|Sim|Sim|Não|  
|**SQLTablePrivileges**|Sim|Sim|Não|  
|**SQLTables**|Sim|Sim|Não|  
|**SQLTransact**|Não|Nenhum [1]|Sim|  
  
 [1] essa função foi preterida em ODBC 3. *x*. ODBC 3. *x* aplicativos não devem usar essa função. No entanto, um aplicativo compatível com ISO CLI ou o Open Group pode chamar essa função.  
  
 [2] ODBC 3. *x* os aplicativos devem usar **SQLBindParameter** em vez de **SQLBindParam**. No entanto, um aplicativo compatível com ISO CLI ou o Open Group pode chamar essa função.  
  
 [3] gravadores de driver devem observar que o ODBC 2. *x* SQL_COLUMN_PRECISION, SQL_COLUMN_SCALE e SQL_COLUMN_LENGTH devem ter suporte com atributos de coluna **SQLColAttribute**.  
  
 [4] **SQLCopyDesc** parcialmente é implementada pelo Gerenciador de Driver quando um descritor está sendo copiado em conexões que pertencem a diferentes drivers. Drivers são necessários para dar suporte à **SQLCopyDesc** em duas de suas próprias conexões. As funções, como **SQLDrivers**, que são implementadas exclusivamente pelo Gerenciador de Driver, não aparecem nessa lista.  
  
 [5] em determinadas circunstâncias, os drivers talvez seja necessário dar suporte a essa função. Para obter mais informações, consulte a página de referência dessa função.  
  
 [6], o driver pode escolher dar suporte à **SQLGetFunctions** se o conjunto de funções que o driver dá suporte a varia de uma conexão para a conexão.
