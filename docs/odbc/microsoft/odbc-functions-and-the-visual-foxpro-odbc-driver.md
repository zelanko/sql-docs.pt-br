---
title: Funções ODBC e o Driver ODBC do Visual FoxPro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC level 2 API functions [ODBC]
- ODBC level 1 API functions [ODBC]
- functions [ODBC], API
- ODBC API functions [ODBC]
- level 1 API functions [ODBC]
- API functions [ODBC]
- core level API functions [ODBC]
- level 2 API functions [ODBC]
- ODBC core level API functions [ODBC]
ms.assetid: 512f9cee-ffad-439b-b612-b49c34c32658
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2610383df0f3dde453fe3ba40b10dea85582b9c7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915760"
---
# <a name="odbc-functions-and-the-visual-foxpro-odbc-driver"></a>Funções ODBC e o Driver ODBC do Visual FoxPro
Os tópicos nesta seção fornecem um breve resumo de funções API ODBC e quaisquer detalhes do Visual FoxPro específicos.  
  
> [!NOTE]  
>  Para obter informações gerais sobre as funções ODBC, consulte [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md) no "Guia do programador de ODBC".  
  
 As funções da API de ODBC foram divididas em três categorias principais: Principais funções da API de nível, funções de API do nível 1 e funções de API do nível 2.  
  
> [!NOTE]  
>  Várias das funções se comportam de forma diferente dependendo se a fonte de dados é definida como uma conexão em um diretório de [tabelas livres](../../odbc/microsoft/visual-foxpro-terminology.md) (arquivos. dbf) ou para um Visual FoxPro [banco de dados](../../odbc/microsoft/visual-foxpro-terminology.md) (arquivo. dbc). Determinadas operações têm suporte somente para conexões de banco de dados.  
  
## <a name="core-level-api-support"></a>Suporte de API de nível de núcleo  
 As funções de API de nível de núcleo de ODBC são listadas na tabela a seguir. Todas essas funções têm suporte para o Driver de ODBC do Visual FoxPro.  
  
|||  
|-|-|  
|[SQLAllocConnect](../../odbc/microsoft/sqlallocconnect-visual-foxpro-odbc-driver.md)|[SQLExecute](../../odbc/microsoft/sqlexecute-visual-foxpro-odbc-driver.md)|  
|[SQLAllocEnv](../../odbc/microsoft/sqlallocenv-visual-foxpro-odbc-driver.md)|[SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md)|  
|[SQLAllocStmt](../../odbc/microsoft/sqlallocstmt-visual-foxpro-odbc-driver.md)|[SQLFreeConnect](../../odbc/microsoft/sqlfreeconnect-visual-foxpro-odbc-driver.md)|  
|[SQLBindCol](../../odbc/microsoft/sqlbindcol-visual-foxpro-odbc-driver.md)|[SQLFreeEnv](../../odbc/microsoft/sqlfreeenv-visual-foxpro-odbc-driver.md)|  
|[SQLCancel](../../odbc/microsoft/sqlcancel-visual-foxpro-odbc-driver.md)|[SQLFreeStmt](../../odbc/microsoft/sqlfreestmt-visual-foxpro-odbc-driver.md)|  
|[SQLColAttributes](../../odbc/microsoft/sqlcolattributes-visual-foxpro-odbc-driver.md)|[SQLGetCursorName](../../odbc/microsoft/sqlgetcursorname-visual-foxpro-odbc-driver.md)|  
|[SQLConnect](../../odbc/microsoft/sqlconnect-visual-foxpro-odbc-driver.md)|[SQLNumResultCols](../../odbc/microsoft/sqlnumresultcols-visual-foxpro-odbc-driver.md)|  
|[SQLDescribeCol](../../odbc/microsoft/sqldescribecol-visual-foxpro-odbc-driver.md)|[SQLPrepare](../../odbc/microsoft/sqlprepare-visual-foxpro-odbc-driver.md)|  
|[SQLDisconnect](../../odbc/microsoft/sqldisconnect-visual-foxpro-odbc-driver.md)|[SQLRowCount](../../odbc/microsoft/sql-row-count-visual-foxpro-odbc-driver.md)|  
|[SQLError](../../odbc/microsoft/sqlerror-visual-foxpro-odbc-driver.md)|[SQLSetCursorName](../../odbc/microsoft/sqlsetcursorname-visual-foxpro-odbc-driver.md)|  
|[SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)|[SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md)|  
  
## <a name="level-1-api-support"></a>Suporte de API de nível 1  
 As funções de API do ODBC nível 1 são listadas na tabela a seguir. Todas essas funções são totalmente ou parcialmente suportadas pelo Driver de ODBC do Visual FoxPro.  
  
|||  
|-|-|  
|[SQLBindParameter](../../odbc/microsoft/sqlbindparameter-visual-foxpro-odbc-driver.md)|[SQLGetTypeInfo](../../odbc/microsoft/sqlgettypeinfo-visual-foxpro-odbc-driver.md)|  
|[SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)|[SQLParamData](../../odbc/microsoft/sqlparamdata-visual-foxpro-odbc-driver.md)|  
|[SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)|[SQLPutData](../../odbc/microsoft/sqlputdata-visual-foxpro-odbc-driver.md)|  
|[SQLGetConnectOption](../../odbc/microsoft/sqlgetconnectoption-visual-foxpro-odbc-driver.md)|[SQLSetConnectOption](../../odbc/microsoft/sqlsetconnectoption-visual-foxpro-odbc-driver.md)|  
|[SQLGetData](../../odbc/microsoft/sqlgetdata-visual-foxpro-odbc-driver.md)|[SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md)|  
|[SQLGetFunctions](../../odbc/microsoft/sqlgetfunctions-visual-foxpro-odbc-driver.md)|[SQLSpecialColumns](../../odbc/microsoft/sqlspecialcolumns-visual-foxpro-odbc-driver.md)|  
|[SQLGetInfo](../../odbc/microsoft/sqlgetinfo-visual-foxpro-odbc-driver.md)|[SQLStatistics](../../odbc/microsoft/sqlstatistics-visual-foxpro-odbc-driver.md)|  
|[SQLGetStmtOption](../../odbc/microsoft/sqlgetstmtoption-visual-foxpro-odbc-driver.md)|[SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)|  
  
## <a name="level-2-api-support"></a>Suporte à API de nível 2  
 As seguintes funções de API do ODBC nível 2 têm suporte total ou parcialmente:  
  
-   [SQLDataSources](../../odbc/microsoft/sqldatasources-visual-foxpro-odbc-driver.md)  
  
-   [SQLDrivers](../../odbc/microsoft/sqldrivers-visual-foxpro-odbc-driver.md)  
  
-   [SQLExtendedFetch](../../odbc/microsoft/sqlextendedfetch-visual-foxpro-odbc-driver.md)  
  
-   [SQLMoreResults](../../odbc/microsoft/sqlmoreresults-visual-foxpro-odbc-driver.md)  
  
-   [SQLNumParams](../../odbc/microsoft/sqlnumparams-visual-foxpro-odbc-driver.md)  
  
-   [SQLParamOptions](../../odbc/microsoft/sqlparamoptions-visual-foxpro-odbc-driver.md)  
  
-   [SQLPrimaryKeys](../../odbc/microsoft/sqlprimarykeys-visual-foxpro-odbc-driver.md)  
  
-   [SQLSetPos](../../odbc/microsoft/sqlsetpos-visual-foxpro-odbc-driver.md)  
  
-   [SQLSetScrollOptions](../../odbc/microsoft/sqlsetscrolloptions-visual-foxpro-odbc-driver.md) (suporte parcial)  
  
 Não há suporte para as seguintes funções de API do nível 2:  
  
-   SQLBrowseConnect  
  
-   SQLColumnPrivileges  
  
-   SQLDescribeParam  
  
-   SQLForeignKeys  
  
-   SQLNativeSql  
  
-   SQLProcedureColumns  
  
-   SQLProcedures  
  
-   SQLTablePrivileges
