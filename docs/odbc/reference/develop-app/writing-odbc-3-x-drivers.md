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
manager: craigg
ms.openlocfilehash: 77a94c7505b5ab221fee4896e91f9b26850669df
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47795645"
---
# <a name="writing-odbc-3x-drivers"></a>Gravar drivers 3.x ODBC
A tabela a seguir mostra o suporte de função em um ODBC 3. *x* driver e um aplicativo ODBC e o mapeamento realizada pelo Gerenciador de Driver quando as funções são chamadas em relação a um ODBC 3. *x* driver.  
  
|Função|Tem suporte<br /><br /> por um<br /><br /> ODBC 3. *x*<br /><br /> driver?|Tem suporte<br /><br /> por um<br /><br /> ODBC 3. *x*<br /><br /> aplicativo?|Mapeado/com suporte<br /><br /> Por que o ODBC 3. *x*<br /><br /> Gerenciador de driver para<br /><br /> um ODBC 3. *x* driver?|  
|--------------|----------------------------------------------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------|  
|**SQLAllocConnect**|não|Nenhum [1]|Sim|  
|**SQLAllocEnv**|não|Nenhum [1]|Sim|  
|**Falha de SQLAllocHandle**|Sim|Sim|não|  
|**SQLAllocStmt**|não|Nenhum [1]|Sim|  
|**SQLBindCol**|Sim|Sim|não|  
|**SQLBindParam**|não|Sim [2]|Sim|  
|**SQLBindParameter**|Sim|Sim|não|  
|**SQLBrowseConnect**|Sim|Sim|não|  
|**SQLBulkOperations**|Sim|Sim|não|  
|**SQLCancel**|Sim|Sim|não|  
|**SQLCloseCursor**|Sim|Sim|não|  
|**SQLColAttribute**|Sim|Sim|não|  
|**SQLColAttributes**|Nenhum [3]|não|Sim|  
|**SQLColumnPrivileges**|Sim|Sim|não|  
|**SQLColumns**|Sim|Sim|não|  
|**SQLConnect**|Sim|Sim|não|  
|**SQLCopyDesc**|Sim|Sim|Sim [4]|  
|**SQLDataSources**|não|Sim|Sim|  
|**SQLDescribeCol**|Sim|Sim|não|  
|**SQLDescribeParam**|Sim|Sim|não|  
|**SQLDisconnect**|Sim|Sim|não|  
|**SQLDriverConnect**|Sim|Sim|não|  
|**SQLDrivers**|não|Sim|Sim|  
|**SQLEndTran**|Sim|Sim|não|  
|**SQLError**|não|Nenhum [1]|Sim|  
|**SQLExecDirect**|Sim|Sim|não|  
|**SQLExecute**|Sim|Sim|não|  
|**SQLExtendedFetch**|Sim|não|não|  
|**SQLFetch**|Sim|Sim|não|  
|**SQLFetchScroll**|Sim|Sim|não|  
|**SQLForeignKeys**|Sim|Sim|não|  
|**SQLFreeConnect**|não|Sim [1]|Sim|  
|**SQLFreeEnv**|não|Sim [1]|Sim|  
|**SQLFreeHandle**|Sim|Sim|não|  
|**SQLFreeStmt**|Sim|Sim|não|  
|**SQLGetConnectAttr**|Sim|Sim|não|  
|**SQLGetConnectOption**|Nenhum [5]|Nenhum [1]|Sim|  
|**SQLGetCursorName**|Sim|Sim|não|  
|**SQLGetData**|Sim|Sim|não|  
|**SQLGetDescField**|Sim|Sim|não|  
|**SQLGetDescRec**|Sim|Sim|não|  
|**SQLGetDiagField**|Sim|Sim|não|  
|**SQLGetDiagRec**|Sim|Sim|não|  
|**SQLGetEnvAttr**|Sim|Sim|não|  
|**SQLGetFunctions**|Nenhum [6]|Sim|Sim|  
|**SQLGetInfo**|Sim|Sim|não|  
|**SQLGetStmtAttr**|Sim|Sim|não|  
|**SQLGetStmtOption**|Nenhum [5]|Nenhum [1]|Sim|  
|**SQLGetTypeInfo**|Sim|Sim|não|  
|**SQLMoreResults**|Sim|Sim|não|  
|**SQLNativeSql**|Sim|Sim|não|  
|**SQLNumParams**|Sim|Sim|não|  
|**SQLNumResultCols**|Sim|Sim|não|  
|**SQLParamData**|Sim|Sim|não|  
|**SQLParamOptions**|não|não|Sim|  
|**SQLPrepare**|Sim|Sim|não|  
|**SQLPrimaryKeys**|Sim|Sim|não|  
|**SQLProcedureColumns**|Sim|Sim|não|  
|**SQLProcedures**|Sim|Sim|não|  
|**SQLPutData**|Sim|Sim|não|  
|**SQLRowCount**|Sim|Sim|não|  
|**SQLSetConnectAttr**|Sim|Sim|não|  
|**SQLSetConnectOption**|Nenhum [5]|Nenhum [1]|Sim|  
|**SQLSetCursorName**|Sim|Sim|não|  
|**SQLSetDescField**|Sim|Sim|não|  
|**SQLSetDescRec**|Sim|Sim|não|  
|**SQLSetEnvAttr**|Sim|Sim|não|  
|**SQLSetPos**|Sim|Sim|não|  
|**SQLSetParam**|não|não|Sim|  
|**SQLSetScrollOption**|Sim|Sim|não|  
|**SQLSetStmtAttr**|Sim|Sim|não|  
|**SQLSetStmtOption**|Nenhum [5]|Nenhum [1]|Sim|  
|**SQLSpecialColumns**|Sim|Sim|não|  
|**SQLStatistics**|Sim|Sim|não|  
|**SQLTablePrivileges**|Sim|Sim|não|  
|**SQLTables**|Sim|Sim|não|  
|**SQLTransact**|não|Nenhum [1]|Sim|  
  
 [1] essa função foi preterida em ODBC 3. *x*. ODBC 3. *x* aplicativos não devem usar essa função. No entanto, um aplicativo compatível com ISO CLI ou o Open Group pode chamar essa função.  
  
 [2] ODBC 3. *x* os aplicativos devem usar **SQLBindParameter** em vez de **SQLBindParam**. No entanto, um aplicativo compatível com ISO CLI ou o Open Group pode chamar essa função.  
  
 [3] gravadores de driver devem observar que o ODBC 2. *x* SQL_COLUMN_PRECISION, SQL_COLUMN_SCALE e SQL_COLUMN_LENGTH devem ter suporte com atributos de coluna **SQLColAttribute**.  
  
 [4] **SQLCopyDesc** parcialmente é implementada pelo Gerenciador de Driver quando um descritor está sendo copiado em conexões que pertencem a diferentes drivers. Drivers são necessários para dar suporte à **SQLCopyDesc** em duas de suas próprias conexões. As funções, como **SQLDrivers**, que são implementadas exclusivamente pelo Gerenciador de Driver, não aparecem nessa lista.  
  
 [5] em determinadas circunstâncias, os drivers talvez seja necessário dar suporte a essa função. Para obter mais informações, consulte a página de referência dessa função.  
  
 [6], o driver pode escolher dar suporte à **SQLGetFunctions** se o conjunto de funções que o driver dá suporte a varia de uma conexão para a conexão.
