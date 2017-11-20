---
title: "Função conformidade | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- conformance levels [ODBC], function
- function conformance levels [ODBC]
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: bb5d68cf-d238-481e-babc-2e9401b4700e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 48ed4bc9b52b6a905972e566870e7e2f86fc4734
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="function-conformance"></a>Conformidade de função
A tabela a seguir indica o nível de conformidade de cada função ODBC, que isso é bem definido.  
  
|Função|Nível de conformidade|  
|--------------|-----------------------|  
|**SQLAllocHandle**|Núcleo|  
|**SQLBindCol**|Núcleo|  
|**SQLBindParameter**|Núcleo [1]|  
|**SQLBrowseConnect**|Nível 1|  
|**SQLBulkOperations**|Nível 1|  
|**SQLCancel**|Núcleo [1]|  
|**SQLCloseCursor**|Núcleo|  
|**SQLColAttribute**|Núcleo [1]|  
|**SQLColumnPrivileges**|Nível 2|  
|**SQLColumns**|Núcleo|  
|**SQLConnect**|Núcleo|  
|**SQLCopyDesc**|Núcleo|  
|**SQLDataSources**|Núcleo|  
|**SQLDescribeCol**|Núcleo [1]|  
|**SQLDescribeParam**|Nível 2|  
|**SQLDisconnect**|Núcleo|  
|**SQLDriverConnect**|Núcleo|  
|**SQLDrivers**|Núcleo|  
|**SQLEndTran**|Núcleo [1]|  
|**SQLExecDirect**|Núcleo|  
|**SQLExecute**|Núcleo|  
|**SQLFetch**|Núcleo|  
|**SQLFetchScroll**|Núcleo [1]|  
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
|**SQLSetConnectAttr**|Núcleo [2]|  
|**SQLSetCursorName**|Núcleo|  
|**SQLSetDescField**|Núcleo [1]|  
|**SQLSetDescRec**|Núcleo|  
|**SQLSetEnvAttr**|Núcleo [2]|  
|**SQLSetPos**|Nível 1 [1]|  
|**SQLSetStmtAttr**|Núcleo [2]|  
|**SQLSpecialColumns**|Núcleo [1]|  
|**SQLStatistics**|Núcleo|  
|**SQLTablePrivileges**|Nível 2|  
|**SQLTables**|Núcleo|  
  
 [1] recursos significativos dessa função estão disponíveis somente em níveis mais altos de conformidade.  
  
 [2] definir determinados atributos como valores não padrão depende do nível de conformidade. Para obter mais informações, consulte a próxima seção, [conformidade atributo](../../../odbc/reference/develop-app/attribute-conformance.md).

