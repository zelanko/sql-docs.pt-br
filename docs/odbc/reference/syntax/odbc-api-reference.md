---
title: Referência da API ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apitype: dllExport
ms.assetid: b7a49774-f458-44ce-9a04-a0457501405b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d56d6068b842256bd450844c7b163727e5d35f3d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62653393"
---
# <a name="odbc-api-reference"></a>Referência de API do ODBC
Os tópicos nesta seção descrevem cada função ODBC em ordem alfabética. Cada função é definida como uma função de linguagem de programação de C. Descrições incluem o seguinte:  
  
-   Finalidade  
  
-   Versão do ODBC  
  
-   Nível de conformidade padrão da CLI  
  
-   Sintaxe  
  
-   Argumentos  
  
-   Valores retornados  
  
-   Diagnóstico  
  
-   Comentários sobre a implementação e uso  
  
-   Exemplo de código  
  
-   Referências a funções relacionadas  
  
 O nível de conformidade padrão da CLI pode ser uma das seguintes opções: ISO-92, abra o grupo, ODBC, ou preterido. Uma função marcada como em conformidade com ISO 92 também aparece no Open Group versão 1, como Open Group é um superconjunto puro de 92 ISO. Uma função marcada como compatível com o Open grupo também aparece no ODBC 3. *x*, pois o ODBC 3. *x* é um superconjunto puro do Open Group versão 1. Uma função marcada como compatível com ODBC aparece em nenhum padrão. Uma função marcada como preterida foi preterida no ODBC 3. *x*.  
  
 Manipulação de informações de diagnóstico é descrita na [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) descrição da função. O texto associado a valores SQLSTATE está incluído para fornecer uma descrição da condição, mas não se destina para prescrever um texto específico.  
  
> [!NOTE]  
>  Para obter informações sobre as funções ODBC específicos do driver, consulte a seção do driver.  
  
 Esta seção contém tópicos para as seguintes funções:  
  
-   [Função SQLAllocConnect](../../../odbc/reference/syntax/sqlallocconnect-function.md)  
  
-   [Função SQLAllocEnv](../../../odbc/reference/syntax/sqlallocenv-function.md)  
  
-   [Função SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
-   [Função SQLAllocStmt](../../../odbc/reference/syntax/sqlallocstmt-function.md)  
  
-   [Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)  
  
-   [Função SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)  
  
-   [Função SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)  
  
-   [Função SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)  
  
-   [Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)  
  
-   [Função SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md)  
  
-   [Função SQLCloseCursor](../../../odbc/reference/syntax/sqlclosecursor-function.md)  
  
-   [Função SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)  
  
-   [Função SQLColAttributes](../../../odbc/reference/syntax/sqlcolattributes-function.md)  
  
-   [Função SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)  
  
-   [Função SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)  
  
-   [Função SQLCompleteAsync](../../../odbc/reference/syntax/sqlcompleteasync-function.md)  
  
-   [Função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)  
  
-   [Função SQLCopyDesc](../../../odbc/reference/syntax/sqlcopydesc-function.md)  
  
-   [Função SQLDataSources](../../../odbc/reference/syntax/sqldatasources-function.md)  
  
-   [Função SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)  
  
-   [Função SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)  
  
-   [Função SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)  
  
-   [Função SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)  
  
-   [Função SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)  
  
-   [Função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)  
  
-   [Função SQLError](../../../odbc/reference/syntax/sqlerror-function.md)  
  
-   [Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)  
  
-   [Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)  
  
-   [Função SQLExtendedFetch](../../../odbc/reference/syntax/sqlextendedfetch-function.md)  
  
-   [Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)  
  
-   [Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)  
  
-   [Função SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)  
  
-   [Função SQLFreeConnect](../../../odbc/reference/syntax/sqlfreeconnect-function.md)  
  
-   [Função SQLFreeEnv](../../../odbc/reference/syntax/sqlfreeenv-function.md)  
  
-   [Função SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)  
  
-   [Função SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)  
  
-   [Função SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
-   [Função SQLGetConnectOption](../../../odbc/reference/syntax/sqlgetconnectoption-function.md)  
  
-   [Função SQLGetCursorName](../../../odbc/reference/syntax/sqlgetcursorname-function.md)  
  
-   [Função SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)  
  
-   [Função SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)  
  
-   [Função SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)  
  
-   [Função SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
-   [Função SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
-   [Função SQLGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)  
  
-   [Função SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
-   [Função SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)  
  
-   [Função SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)  
  
-   [Função SQLGetStmtOption](../../../odbc/reference/syntax/sqlgetstmtoption-function.md)  
  
-   [Função SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)  
  
-   [Função SQLMoreResults](../../../odbc/reference/syntax/sqlmoreresults-function.md)  
  
-   [Função SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md)  
  
-   [Função SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)  
  
-   [Função SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)  
  
-   [Função SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)  
  
-   [Função SQLParamOptions](../../../odbc/reference/syntax/sqlparamoptions-function.md)  
  
-   [Função SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)  
  
-   [Função SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)  
  
-   [Função SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)  
  
-   [Função SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)  
  
-   [Função SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)  
  
-   [Função SQLRowCount](../../../odbc/reference/syntax/sqlrowcount-function.md)  
  
-   [Função SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)  
  
-   [Função SQLSetConnectOption](../../../odbc/reference/syntax/sqlsetconnectoption-function.md)  
  
-   [Função SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)  
  
-   [Função SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)  
  
-   [Função SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)  
  
-   [Função SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)  
  
-   [Função SQLSetParam](../../../odbc/reference/syntax/sqlsetparam-function.md)  
  
-   [Função SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)  
  
-   [Função SQLSetScrollOptions](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)  
  
-   [Função SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)  
  
-   [Função SQLSetStmtOption](../../../odbc/reference/syntax/sqlsetstmtoption-function.md)  
  
-   [Função SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)  
  
-   [Função SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)  
  
-   [Função SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)  
  
-   [Função SQLTables](../../../odbc/reference/syntax/sqltables-function.md)  
  
-   [Função SQLTransact](../../../odbc/reference/syntax/sqltransact-function.md)
