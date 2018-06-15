---
title: Função conformidade | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- conformance levels [ODBC], function
- function conformance levels [ODBC]
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: bb5d68cf-d238-481e-babc-2e9401b4700e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 182b53071f5d7d4c3486a84f789954e12772e0bc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32914251"
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
