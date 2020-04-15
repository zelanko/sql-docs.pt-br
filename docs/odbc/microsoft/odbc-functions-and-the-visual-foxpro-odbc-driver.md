---
title: Funções ODBC e o driver Visual FoxPro ODBC | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 26bb1f24a7dbb307d3048b8ec2a8ae293ddbe7ff
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298096"
---
# <a name="odbc-functions-and-the-visual-foxpro-odbc-driver"></a>Funções ODBC e o Driver ODBC do Visual FoxPro
Os tópicos desta seção fornecem um breve resumo das funções da API do ODBC e quaisquer detalhes específicos do Visual FoxPro.  
  
> [!NOTE]  
>  Para obter informações gerais sobre as funções da ODBC, consulte [a referência da API da ODBC](../../odbc/reference/syntax/odbc-api-reference.md) no "Guia do Programador ODBC".  
  
 As funções da API ODBC foram divididas em três categorias principais aqui: funções de API de nível de núcleo, funções de API nível 1 e funções de API nível 2.  
  
> [!NOTE]  
>  Várias das funções se comportam de forma diferente, dependendo se a fonte de dados é definida como uma conexão com um diretório de [tabelas livres](../../odbc/microsoft/visual-foxpro-terminology.md) (arquivos.dbf) ou a um banco de [dados](../../odbc/microsoft/visual-foxpro-terminology.md) Visual FoxPro (arquivo.dbc). Certas operações são suportadas apenas para conexões de banco de dados.  
  
## <a name="core-level-api-support"></a>Suporte à API de nível central  
 As funções de API de nível de núcleo do ODBC estão listadas na tabela a seguir. Todas essas funções são suportadas pelo Visual FoxPro ODBC Driver.  
  
|||  
|-|-|  
|[SQLAllocConnect](../../odbc/microsoft/sqlallocconnect-visual-foxpro-odbc-driver.md)|[SQLExecute](../../odbc/microsoft/sqlexecute-visual-foxpro-odbc-driver.md)|  
|[SQLAllocEnv](../../odbc/microsoft/sqlallocenv-visual-foxpro-odbc-driver.md)|[SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md)|  
|[SQLAllocStmt](../../odbc/microsoft/sqlallocstmt-visual-foxpro-odbc-driver.md)|[SQLFreeConnect](../../odbc/microsoft/sqlfreeconnect-visual-foxpro-odbc-driver.md)|  
|[SQLBindCol](../../odbc/microsoft/sqlbindcol-visual-foxpro-odbc-driver.md)|[SQLFreeEnv](../../odbc/microsoft/sqlfreeenv-visual-foxpro-odbc-driver.md)|  
|[SQLCancel](../../odbc/microsoft/sqlcancel-visual-foxpro-odbc-driver.md)|[SQLFreeStmt](../../odbc/microsoft/sqlfreestmt-visual-foxpro-odbc-driver.md)|  
|[SQLColAttributea](../../odbc/microsoft/sqlcolattributes-visual-foxpro-odbc-driver.md)|[SQLGetCursorName](../../odbc/microsoft/sqlgetcursorname-visual-foxpro-odbc-driver.md)|  
|[SQLConnect](../../odbc/microsoft/sqlconnect-visual-foxpro-odbc-driver.md)|[SQLNumResultCols](../../odbc/microsoft/sqlnumresultcols-visual-foxpro-odbc-driver.md)|  
|[SQLDescribeCol](../../odbc/microsoft/sqldescribecol-visual-foxpro-odbc-driver.md)|[SQLPrepare](../../odbc/microsoft/sqlprepare-visual-foxpro-odbc-driver.md)|  
|[Sqldisconnect](../../odbc/microsoft/sqldisconnect-visual-foxpro-odbc-driver.md)|[SQLRowCount](../../odbc/microsoft/sql-row-count-visual-foxpro-odbc-driver.md)|  
|[Sqlerror](../../odbc/microsoft/sqlerror-visual-foxpro-odbc-driver.md)|[Sqlsetcursorname](../../odbc/microsoft/sqlsetcursorname-visual-foxpro-odbc-driver.md)|  
|[SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)|[SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md)|  
  
## <a name="level-1-api-support"></a>Suporte à API nível 1  
 As funções de API nível 1 do ODBC estão listadas na tabela a seguir. Todas essas funções são totalmente ou parcialmente suportadas pelo Visual FoxPro ODBC Driver.  
  
|||  
|-|-|  
|[SQLBindParameter](../../odbc/microsoft/sqlbindparameter-visual-foxpro-odbc-driver.md)|[SQLGetTypeInfo](../../odbc/microsoft/sqlgettypeinfo-visual-foxpro-odbc-driver.md)|  
|[SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)|[SQLParamData](../../odbc/microsoft/sqlparamdata-visual-foxpro-odbc-driver.md)|  
|[SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)|[SQLPutData](../../odbc/microsoft/sqlputdata-visual-foxpro-odbc-driver.md)|  
|[Opção SQLGetConnect](../../odbc/microsoft/sqlgetconnectoption-visual-foxpro-odbc-driver.md)|[Sqlsetconnectoption](../../odbc/microsoft/sqlsetconnectoption-visual-foxpro-odbc-driver.md)|  
|[SQLGetData](../../odbc/microsoft/sqlgetdata-visual-foxpro-odbc-driver.md)|[SQLSetStmtOpção](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md)|  
|[SQLGetFunctions](../../odbc/microsoft/sqlgetfunctions-visual-foxpro-odbc-driver.md)|[SQLSpecialColumns](../../odbc/microsoft/sqlspecialcolumns-visual-foxpro-odbc-driver.md)|  
|[SQLGetInfo](../../odbc/microsoft/sqlgetinfo-visual-foxpro-odbc-driver.md)|[SQLStatistics](../../odbc/microsoft/sqlstatistics-visual-foxpro-odbc-driver.md)|  
|[Opção SQLGetStmt](../../odbc/microsoft/sqlgetstmtoption-visual-foxpro-odbc-driver.md)|[SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)|  
  
## <a name="level-2-api-support"></a>Suporte à API nível 2  
 As seguintes funções de API nível 2 da ODBC são totalmente ou parcialmente suportadas:  
  
-   [SQLDataSources](../../odbc/microsoft/sqldatasources-visual-foxpro-odbc-driver.md)  
  
-   [SQLDrivers](../../odbc/microsoft/sqldrivers-visual-foxpro-odbc-driver.md)  
  
-   [Sqlextendedfetch](../../odbc/microsoft/sqlextendedfetch-visual-foxpro-odbc-driver.md)  
  
-   [SQLMoreResults](../../odbc/microsoft/sqlmoreresults-visual-foxpro-odbc-driver.md)  
  
-   [SQLNumParams](../../odbc/microsoft/sqlnumparams-visual-foxpro-odbc-driver.md)  
  
-   [Opções de SQLParam](../../odbc/microsoft/sqlparamoptions-visual-foxpro-odbc-driver.md)  
  
-   [SQLPrimaryKeys](../../odbc/microsoft/sqlprimarykeys-visual-foxpro-odbc-driver.md)  
  
-   [SQLSetPos](../../odbc/microsoft/sqlsetpos-visual-foxpro-odbc-driver.md)  
  
-   [SQLSetScrollOptions](../../odbc/microsoft/sqlsetscrolloptions-visual-foxpro-odbc-driver.md) (suporte parcial)  
  
 As seguintes funções de API nível 2 não são suportadas:  
  
-   SQLBrowseConnect  
  
-   SQLColumnPrivileges  
  
-   SQLDescribeParam  
  
-   SQLForeignKeys  
  
-   SQLNativeSql  
  
-   SQLProcedureColumns  
  
-   SQLProcedures  
  
-   SQLTablePrivileges
