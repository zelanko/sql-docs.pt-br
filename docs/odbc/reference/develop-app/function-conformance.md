---
title: Conformidade de função | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 33cd0ad4269ed59e31c8ab343ddbb01806afce04
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305587"
---
# <a name="function-conformance"></a>Conformidade de função
A tabela a seguir indica o nível de conformidade de cada função ODBC, onde isso é bem definido.  
  
|Função|Compatibilidade com nível|  
|--------------|-----------------------|  
|**SQLAllocHandle**|Núcleo|  
|**SQLBindCol**|Núcleo|  
|**SQLBindParameter**|Núcleo[1]|  
|**SQLBrowseConnect**|Nível 1|  
|**SQLBulkOperations**|Nível 1|  
|**SQLCancel**|Núcleo[1]|  
|**SQLCloseCursor**|Núcleo|  
|**SQLColAttribute**|Núcleo[1]|  
|**SQLColumnPrivileges**|Nível 2|  
|**SQLColumns**|Núcleo|  
|**SQLConnect**|Núcleo|  
|**SQLCopyDesc**|Núcleo|  
|**SQLDataSources**|Núcleo|  
|**SQLDescribeCol**|Núcleo[1]|  
|**SQLDescribeParam**|Nível 2|  
|**Sqldisconnect**|Núcleo|  
|**SQLDriverConnect**|Núcleo|  
|**SQLDrivers**|Núcleo|  
|**SQLEndTran**|Núcleo[1]|  
|**SQLExecDirect**|Núcleo|  
|**SQLExecute**|Núcleo|  
|**SQLFetch**|Núcleo|  
|**SQLFetchScroll**|Núcleo[1]|  
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
|**SQlGetEnvAttr**|Núcleo|  
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
|**SQLSetConnectAttr**|Núcleo[2]|  
|**Sqlsetcursorname**|Núcleo|  
|**SQLSetDescField**|Núcleo[1]|  
|**SQLSetDescRec**|Núcleo|  
|**SQLSetEnvAttr**|Núcleo[2]|  
|**SQLSetPos**|Nível 1[1]|  
|**SQLSetStmtAttr**|Núcleo[2]|  
|**SQLSpecialColumns**|Núcleo[1]|  
|**SQLStatistics**|Núcleo|  
|**SQLTablePrivileges**|Nível 2|  
|**SQLTables**|Núcleo|  
  
 [1] Características significativas desta função estão disponíveis apenas em níveis mais altos de conformidade.  
  
 [2] Definir certos atributos a valores não padrão depende do nível de conformidade. Para obter mais informações, consulte a próxima seção, [Atribuição de Conformidade](../../../odbc/reference/develop-app/attribute-conformance.md).
