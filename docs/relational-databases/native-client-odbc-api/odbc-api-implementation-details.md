---
title: Detalhes da implementação da API da ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, functions
- SQL Server Native Client ODBC driver, SQL Server-specific behaviors
- ODBC, SQL Server-specific behaviors
- functions [ODBC]
ms.assetid: dca92489-f179-4b1f-997c-adcc46aa17a3
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 880c38483b3896f95ccfde4f8237d6d0acbf8e3c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302687"
---
# <a name="odbc-api-implementation-details"></a>ODBC API Implementation Details
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC (Open Database Connectivity) é uma interface de programação de aplicativo do Microsoft Win32 usada pelos aplicativos para acessar dados em fontes de dados ODBC.  
  
 A referência do driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client não documenta todas as chamadas de função do ODBC. Só essas funções com parâmetros ou comportamentos específicos de driver quando usados com o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client são abordados.  
  
 O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client está em conformidade com a especificação do ODBC 3.51. Para obter uma referência abrangente do ODBC 3.51, baixe o SDK dos componentes de acesso a dados da Microsoft no [Data Access and Storage Developer Center](https://go.microsoft.com/fwlink?linkid=4173)ou visualize a referência do [Programador ODBC](https://go.microsoft.com/fwlink/?LinkId=45250) on-line.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md)  
  
-   [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md)  
  
-   [SQLBrowseConnect](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)  
  
-   [SQLCancel](../../relational-databases/native-client-odbc-api/sqlcancel.md)  
  
-   [SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md)  
  
-   [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)  
  
-   [SQLColumnPrivileges](../../relational-databases/native-client-odbc-api/sqlcolumnprivileges.md)  
  
-   [SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md)  
  
-   [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)  
  
-   [SQLConnect](../../relational-databases/native-client-odbc-api/sqlconnect.md)  
  
-   [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md)  
  
-   [SQLDescribeParam](../../relational-databases/native-client-odbc-api/sqldescribeparam.md)  
  
-   [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md)  
  
-   [SQLDrivers](../../relational-databases/native-client-odbc-api/sqldrivers.md)  
  
-   [SQLEndTran](../../relational-databases/native-client-odbc-api/sqlendtran.md)  
  
-   [SQLExecDirect](../../relational-databases/native-client-odbc-api/sqlexecdirect.md)  
  
-   [SQLExecute](../../relational-databases/native-client-odbc-api/sqlexecute.md)  
  
-   [SQLFetch](../../relational-databases/native-client-odbc-api/sqlfetch.md)  
  
-   [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)  
  
-   [SQLForeignKeys](../../relational-databases/native-client-odbc-api/sqlforeignkeys.md)  
  
-   [SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md)  
  
-   [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md)  
  
-   [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md)  
  
-   [SQLGetCursorName](../../relational-databases/native-client-odbc-api/sqlgetcursorname.md)  
  
-   [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)  
  
-   [SQLGetDescField](../../relational-databases/native-client-odbc-api/sqlgetdescfield.md)  
  
-   [SQLGetDiagField](../../relational-databases/native-client-odbc-api/sqlgetdiagfield.md)  
  
-   [SQLGetFunctions](../../relational-databases/native-client-odbc-api/sqlgetfunctions.md)  
  
-   [SQLGetInfo](../../relational-databases/native-client-odbc-api/sqlgetinfo.md)  
  
-   [SQLGetStmtAttr](../../relational-databases/native-client-odbc-api/sqlgetstmtattr.md)  
  
-   [SQLGetTypeInfo](../../relational-databases/native-client-odbc-api/sqlgettypeinfo.md)  
  
-   [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)  
  
-   [SQLNativeSql](../../relational-databases/native-client-odbc-api/sqlnativesql.md)  
  
-   [SQLNumParams](../../relational-databases/native-client-odbc-api/sqlnumparams.md)  
  
-   [SQLNumResultCols](../../relational-databases/native-client-odbc-api/sqlnumresultcols.md)  
  
-   [SQLParamData](../../relational-databases/native-client-odbc-api/sqlparamdata.md)  
  
-   [SQLPrimaryKeys](../../relational-databases/native-client-odbc-api/sqlprimarykeys.md)  
  
-   [SQLProcedureColumns](../../relational-databases/native-client-odbc-api/sqlprocedurecolumns.md)  
  
-   [SQLProcedures](../../relational-databases/native-client-odbc-api/sqlprocedures.md)  
  
-   [SQLPutData](../../relational-databases/native-client-odbc-api/sqlputdata.md)  
  
-   [SQLRowCount](../../relational-databases/native-client-odbc-api/sqlrowcount.md)  
  
-   [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)  
  
-   [SQLSetDescField](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md)  
  
-   [SQLSetDescRec](../../relational-databases/native-client-odbc-api/sqlsetdescrec.md)  
  
-   [SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md)  
  
-   [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)  
  
-   [SQLSpecialColumns](../../relational-databases/native-client-odbc-api/sqlspecialcolumns.md)  
  
-   [SQLStatistics](../../relational-databases/native-client-odbc-api/sqlstatistics.md)  
  
-   [SQLTablePrivileges](../../relational-databases/native-client-odbc-api/sqltableprivileges.md)  
  
-   [SQLTables](../../relational-databases/native-client-odbc-api/sqltables.md)  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Native Client &#40;ODBC&#41; Reference](https://msdn.microsoft.com/library/06b7edee-8636-49d9-9b5c-2c710bf4fa2d)   
 [Criando aplicativos com o SQL Server Native Client](../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
