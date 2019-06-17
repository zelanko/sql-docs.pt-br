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
manager: craigg
ms.openlocfilehash: b6cb2f56113487922866573caf3b5f8b67fff7c4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63061574"
---
# <a name="function-conformance"></a>Conformidade de função
A tabela a seguir indica o nível de conformidade de cada função ODBC, que isso é bem definido.  
  
|Função|nível de conformidade|  
|--------------|-----------------------|  
|**SQLAllocHandle**|Núcleo|  
|**SQLBindCol**|Núcleo|  
|**SQLBindParameter**|Core[1]|  
|**SQLBrowseConnect**|Nível 1|  
|**SQLBulkOperations**|Nível 1|  
|**SQLCancel**|Core[1]|  
|**SQLCloseCursor**|Núcleo|  
|**SQLColAttribute**|Core[1]|  
|**SQLColumnPrivileges**|Nível 2|  
|**SQLColumns**|Núcleo|  
|**SQLConnect**|Núcleo|  
|**SQLCopyDesc**|Núcleo|  
|**SQLDataSources**|Núcleo|  
|**SQLDescribeCol**|Core[1]|  
|**SQLDescribeParam**|Nível 2|  
|**SQLDisconnect**|Núcleo|  
|**SQLDriverConnect**|Núcleo|  
|**SQLDrivers**|Núcleo|  
|**SQLEndTran**|Core[1]|  
|**SQLExecDirect**|Núcleo|  
|**SQLExecute**|Núcleo|  
|**SQLFetch**|Núcleo|  
|**SQLFetchScroll**|Core[1]|  
|**SQLForeignKeys**|Nível 2|  
|**SQLFreeHandle**|Núcleo|  
|**SQLFreeStmt**|Núcleo|  
|**SQLGetConnectAttr**|Núcleo|  
|**SQLGetCursorName**|Núcleo|  
|**SQLGetData**|Núcleo|  
|**SQLGetDescField**|Núcleo|  
|**SQLGetDescRec**|Núcleo|  
|**SQLGetDiagField**|Núcleo|  
|**SQLGetDiagRec**|Núcleo|  
|**SQLGetEnvAttr**|Núcleo|  
|**SQLGetFunctions**|Núcleo|  
|**SQLGetInfo**|Núcleo|  
|**SQLGetStmtAttr**|Núcleo|  
|**SQLGetTypeInfo**|Núcleo|  
|**SQLMoreResults**|Nível 1|  
|**SQLNativeSql**|Núcleo|  
|**SQLNumParams**|Núcleo|  
|**SQLNumResultCols**|Núcleo|  
|**SQLParamData**|Núcleo|  
|**SQLPrepare**|Núcleo|  
|**SQLPrimaryKeys**|Nível 1|  
|**SQLProcedureColumns**|Nível 1|  
|**SQLProcedures**|Nível 1|  
|**SQLPutData**|Núcleo|  
|**SQLRowCount**|Núcleo|  
|**SQLSetConnectAttr**|Core [2]|  
|**SQLSetCursorName**|Núcleo|  
|**SQLSetDescField**|Core[1]|  
|**SQLSetDescRec**|Núcleo|  
|**SQLSetEnvAttr**|Core [2]|  
|**SQLSetPos**|Nível 1 [1]|  
|**SQLSetStmtAttr**|Core [2]|  
|**SQLSpecialColumns**|Core[1]|  
|**SQLStatistics**|Núcleo|  
|**SQLTablePrivileges**|Nível 2|  
|**SQLTables**|Núcleo|  
  
 [1] recursos significativos dessa função estão disponíveis somente em níveis mais altos de conformidade.  
  
 [2] definir certos atributos como valores não padrão depende do nível de conformidade. Para obter mais informações, consulte a próxima seção, [conformidade com o atributo](../../../odbc/reference/develop-app/attribute-conformance.md).
