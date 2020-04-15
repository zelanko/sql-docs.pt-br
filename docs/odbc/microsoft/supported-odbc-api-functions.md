---
title: Funções de API ODBC suportadas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC, API functions
- ODBC SQL grammar, API functions mapped to driver (table) [ODBC]
ms.assetid: b28a8ed6-09b1-4acf-bf3e-f90bb32422de
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ec6ceaf57d8fe3c5325f85a9644cf4c8016663e4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304097"
---
# <a name="supported-odbc-api-functions"></a>Funções de API do ODBC com suporte
O objetivo do nivelamento é informar o aplicativo quais recursos estão disponíveis para ele a partir do motorista. Os drivers de banco de dados de desktop do Microsoft ODBC suportam todas as funções Core e Level 1.  
  
 Para obter mais informações sobre os níveis de conformidade para funções e gramática, consulte [Níveis de Conformidade](../../odbc/reference/develop-app/conformance-levels.md) no *Programador oDBC*.  
  
 O suporte às funções de API oDBC pode depender do driver usado. A tabela a seguir resume o suporte às funções. A coluna mais à esquerda fornece um link para a página de referência geral para cada função. Essas páginas de referência estão listadas em ordem alfabética na seção [De referência da API ODBC,](../../odbc/reference/syntax/odbc-api-reference.md) sob [a referência do programador ODBC](../../odbc/reference/odbc-programmer-s-reference.md). As colunas à direita fornecem links para notas específicas do driver sobre cada função suportada. Esses tópicos específicos do driver estão listados na seção "Outros detalhes de programação" para cada driver. Alternativamente, se as mesmas observações sobre uma função se aplicam a todos os Drivers de banco de dados de desktop da ODBC, a coluna mais à direita fornece um link para um tópico que resume o suporte dos Drivers de banco de dados da área de trabalho para essa função. Esses tópicos são listados no final da seção atual ("Funções de API ODBC suportadas").  
  
|Função ODBC|Acesse notas específicas do driver|dBASE Notas específicas do driver|Notas específicas paradoxdas do driver|Notas específicas do driver do arquivo de texto|Notas específicas do Excel Driver|Notas relevantes para todos os drivers|  
|-------------------|-----------------------------------|----------------------------------|------------------------------------|--------------------------------------|----------------------------------|-----------------------------------|  
|[SQLBindParameter](../../odbc/reference/syntax/sqlbindparameter-function.md)|||||[Excel](../../odbc/microsoft/sqlbindparameter-excel-driver.md)||  
|[SQLColAttributea](../../odbc/reference/syntax/sqlcolattributes-function.md)|[Acesso](../../odbc/microsoft/sqlcolattributes-access-driver.md)|[Dbase](../../odbc/microsoft/sqlcolattributes-dbase-driver.md)|[Paradoxo](../../odbc/microsoft/sqlcolattributes-paradox-driver.md)|[Arquivo de texto](../../odbc/microsoft/sqlcolattributes-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlcolattributes-excel-driver.md)||  
|[SQLColumns](../../odbc/reference/syntax/sqlcolattributes-function.md)|[Acesso](../../odbc/microsoft/sqlcolattributes-access-driver.md)|[Dbase](../../odbc/microsoft/sqlcolattributes-dbase-driver.md)|[Paradoxo](../../odbc/microsoft/sqlcolattributes-paradox-driver.md)|[Arquivo de texto](../../odbc/microsoft/sqlcolattributes-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlcolattributes-excel-driver.md)||  
|[SQLConfigDataSource](../../odbc/reference/syntax/sqlconfigdatasource-function.md)|[Acesso](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)|[Dbase](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)|[Paradoxo](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)|[Arquivo de texto](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)|[Excel](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)||  
|[SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md)|[Acesso](../../odbc/microsoft/sqldriverconnect-access-driver.md)|[Dbase](../../odbc/microsoft/sqldriverconnect-dbase-driver.md)|[Paradoxo](../../odbc/microsoft/sqldriverconnect-paradox-driver.md)|[Arquivo de texto](../../odbc/microsoft/sqldriverconnect-text-file-driver.md)|[Excel](../../odbc/microsoft/sqldriverconnect-excel-driver.md)||  
|[SQLGetCursorName](../../odbc/reference/syntax/sqlgetcursorname-function.md)||||||[Todos os drivers](../../odbc/microsoft/sqlgetcursorname-desktop-database-drivers.md)|  
|[SQLGetData](../../odbc/reference/syntax/sqlgetdata-function.md)||||||[Todos os drivers](../../odbc/microsoft/sqlgetdata-desktop-database-drivers.md)|  
|[SQLGetInfo](../../odbc/reference/syntax/sqlgetinfo-function.md)|[Acesso](../../odbc/microsoft/sqlgetinfo-access-driver.md)|[Dbase](../../odbc/microsoft/sqlgetinfo-dbase-driver.md)|[Paradoxo](../../odbc/microsoft/sqlgetinfo-paradox-driver.md)|[Arquivo de texto](../../odbc/microsoft/sqlgetinfo-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlgetinfo-excel-driver.md)|
|[Opção SQLGetStmt](../../odbc/reference/syntax/sqlgetstmtoption-function.md)||||||[Todos os drivers](../../odbc/microsoft/sqlgetstmtoption-desktop-database-drivers.md)|  
|[SQLGetTypeInfo](../../odbc/reference/syntax/sqlgettypeinfo-function.md)|[Acesso](../../odbc/microsoft/sqlgettypeinfo-access-driver.md)|[Dbase](../../odbc/microsoft/sqlgettypeinfo-dbase-driver.md)|[Paradoxo](../../odbc/microsoft/sqlgettypeinfo-paradox-driver.md)|[Arquivo de texto](../../odbc/microsoft/sqlgettypeinfo-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlgettypeinfo-excel-driver.md)||  
|[SQLMoreResults](../../odbc/reference/syntax/sqlmoreresults-function.md)||||||[Todos os drivers](../../odbc/microsoft/sqlmoreresults-desktop-database-drivers.md)|  
|[SQLPrepare](../../odbc/reference/syntax/sqlprepare-function.md)||||||[Todos os drivers](../../odbc/microsoft/sqlprepare-desktop-database-drivers.md)|  
|[SQLProcedureColumns](../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|[Acesso](../../odbc/microsoft/sqlprocedurecolumns-access-driver.md)||||||  
|[SQLProcedures](../../odbc/reference/syntax/sqlprocedures-function.md)||||||[Todos os drivers](../../odbc/microsoft/sqlprocedures-desktop-database-drivers.md)|  
|[Sqlsetconnectoption](../../odbc/reference/syntax/sqlsetconnectoption-function.md)|[Acesso](../../odbc/microsoft/sqlsetconnectoption-access-driver.md)|[Dbase](../../odbc/microsoft/sqlsetconnectoption-dbase-driver.md)|[Paradoxo](../../odbc/microsoft/sqlsetconnectoption-paradox-driver.md)|[Arquivo de texto](../../odbc/microsoft/sqlsetconnectoption-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlsetconnectoption-excel-driver.md)||  
|[Sqlsetcursorname](../../odbc/reference/syntax/sqlsetcursorname-function.md)||||||[Todos os drivers](../../odbc/microsoft/sqlsetcursorname-desktop-database-drivers.md)|  
|[SQLSetPos](../../odbc/reference/syntax/sqlsetpos-function.md)||||||[Todos os drivers](../../odbc/microsoft/sqlsetpos-desktop-database-drivers.md)|  
|[Opções de SQLSetScroll](../../odbc/reference/syntax/sqlsetscrolloptions-function.md)||||||[Todos os drivers](../../odbc/microsoft/sqlsetscrolloptions-desktop-database-drivers.md)|  
|[SQLSetStmtOpção](../../odbc/reference/syntax/sqlsetstmtoption-function.md)||||||[Todos os drivers](../../odbc/microsoft/sqlsetstmtoption-desktop-database-drivers.md)|  
|[SQLSpecialColumns](../../odbc/reference/syntax/sqlspecialcolumns-function.md)||||||[Todos os drivers](../../odbc/microsoft/sqlspecialcolumns-desktop-database-drivers.md)|  
|[SQLStatistics](../../odbc/reference/syntax/sqlstatistics-function.md)|[Acesso](../../odbc/microsoft/sqlstatistics-access-driver.md)|[Dbase](../../odbc/microsoft/sqlstatistics-dbase-driver.md)|[Paradoxo](../../odbc/microsoft/sqlstatistics-paradox-driver.md)|[Arquivo de texto](../../odbc/microsoft/sqlstatistics-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlstatistics-excel-driver.md)||  
|[SQLTables](../../odbc/reference/syntax/sqltables-function.md)|[Acesso](../../odbc/microsoft/sqltables-access-driver.md)|[Dbase](../../odbc/microsoft/sqltables-dbase-driver.md)|[Paradoxo](../../odbc/microsoft/sqltables-paradox-driver.md)|[Arquivo de texto](../../odbc/microsoft/sqltables-text-file-driver.md)|[Excel](../../odbc/microsoft/sqltables-excel-driver.md)|  
|[SQLTransact](../../odbc/reference/syntax/sqltransact-function.md)|[Acesso](../../odbc/microsoft/sqltransact-access-driver.md)|[Dbase](../../odbc/microsoft/sqltransact-dbase-driver.md)|[Paradoxo](../../odbc/microsoft/sqltransact-paradox-driver.md)|[Arquivo de texto](../../odbc/microsoft/sqltransact-text-file-driver.md)|[Excel](../../odbc/microsoft/sqltransact-excel-driver.md)||  
  
 Os tópicos a seguir fornecem observações sobre as funções da ODBC. Essas observações se aplicam a todos os drivers de banco de dados de desktop da ODBC.  
  
-   [SQLGetData (Drivers de banco de dados de área de trabalho)](../../odbc/microsoft/sqlgetdata-desktop-database-drivers.md)  
  
-   [SQLGetStmtOption (Drivers de banco de dados da área de trabalho)](../../odbc/microsoft/sqlgetstmtoption-desktop-database-drivers.md)  
  
-   [SQLMoreResults (Drivers de banco de dados de área de trabalho)](../../odbc/microsoft/sqlmoreresults-desktop-database-drivers.md)  
  
-   [SQLPrepare (Drivers de banco de dados de área de trabalho)](../../odbc/microsoft/sqlprepare-desktop-database-drivers.md)  
  
-   [SQLProcedures (Drivers de banco de dados de área de trabalho)](../../odbc/microsoft/sqlprocedures-desktop-database-drivers.md)  
  
-   [SQLSetCursorName (Drivers de banco de dados de área de trabalho)](../../odbc/microsoft/sqlsetcursorname-desktop-database-drivers.md)  
  
-   [SQLSetPos (Drivers de banco de dados de área de trabalho)](../../odbc/microsoft/sqlsetpos-desktop-database-drivers.md)  
  
-   [SQLSetScrollOptions (Drivers de banco de dados de área de trabalho)](../../odbc/microsoft/sqlsetscrolloptions-desktop-database-drivers.md)  
  
-   [SQLSetStmtOption (Drivers de banco de dados de área de trabalho)](../../odbc/microsoft/sqlsetstmtoption-desktop-database-drivers.md)  
  
-   [SQLSpecialColumns (Drivers de banco de dados de área de trabalho)](../../odbc/microsoft/sqlspecialcolumns-desktop-database-drivers.md)
