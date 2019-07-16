---
title: Função conformidade | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- conformance levels [ODBC], function
- function conformance levels [ODBC]
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: bb5d68cf-d238-481e-babc-2e9401b4700e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 45eb427b660496430334633b5d43ee8989211c0f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069749"
---
# <a name="function-conformance"></a>Conformidade de função
A tabela a seguir indica o nível de conformidade de cada função ODBC, que isso é bem definido.  
  
|Função|nível de conformidade|  
|--------------|-----------------------|  
|**SQLAllocHandle**|Core|  
|**SQLBindCol**|Core|  
|**SQLBindParameter**|Core [1]|  
|**SQLBrowseConnect**|Nível 1|  
|**SQLBulkOperations**|Nível 1|  
|**SQLCancel**|Core [1]|  
|**SQLCloseCursor**|Core|  
|**SQLColAttribute**|Core [1]|  
|**SQLColumnPrivileges**|Nível 2|  
|**SQLColumns**|Core|  
|**SQLConnect**|Core|  
|**SQLCopyDesc**|Core|  
|**SQLDataSources**|Core|  
|**SQLDescribeCol**|Core [1]|  
|**SQLDescribeParam**|Nível 2|  
|**SQLDisconnect**|Core|  
|**SQLDriverConnect**|Core|  
|**SQLDrivers**|Core|  
|**SQLEndTran**|Core [1]|  
|**SQLExecDirect**|Core|  
|**SQLExecute**|Core|  
|**SQLFetch**|Core|  
|**SQLFetchScroll**|Core [1]|  
|**SQLForeignKeys**|Nível 2|  
|**SQLFreeHandle**|Core|  
|**SQLFreeStmt**|Core|  
|**SQLGetConnectAttr**|Core|  
|**SQLGetCursorName**|Core|  
|**SQLGetData**|Core|  
|**SQLGetDescField**|Core|  
|**SQLGetDescRec**|Core|  
|**SQLGetDiagField**|Core|  
|**SQLGetDiagRec**|Core|  
|**SQLGetEnvAttr**|Core|  
|**SQLGetFunctions**|Core|  
|**SQLGetInfo**|Core|  
|**SQLGetStmtAttr**|Core|  
|**SQLGetTypeInfo**|Core|  
|**SQLMoreResults**|Nível 1|  
|**SQLNativeSql**|Core|  
|**SQLNumParams**|Core|  
|**SQLNumResultCols**|Core|  
|**SQLParamData**|Core|  
|**SQLPrepare**|Core|  
|**SQLPrimaryKeys**|Nível 1|  
|**SQLProcedureColumns**|Nível 1|  
|**SQLProcedures**|Nível 1|  
|**SQLPutData**|Core|  
|**SQLRowCount**|Core|  
|**SQLSetConnectAttr**|Core [2]|  
|**SQLSetCursorName**|Core|  
|**SQLSetDescField**|Core [1]|  
|**SQLSetDescRec**|Core|  
|**SQLSetEnvAttr**|Core [2]|  
|**SQLSetPos**|Nível 1 [1]|  
|**SQLSetStmtAttr**|Core [2]|  
|**SQLSpecialColumns**|Core [1]|  
|**SQLStatistics**|Core|  
|**SQLTablePrivileges**|Nível 2|  
|**SQLTables**|Core|  
  
 [1] recursos significativos dessa função estão disponíveis somente em níveis mais altos de conformidade.  
  
 [2] definir certos atributos como valores não padrão depende do nível de conformidade. Para obter mais informações, consulte a próxima seção, [conformidade com o atributo](../../../odbc/reference/develop-app/attribute-conformance.md).
