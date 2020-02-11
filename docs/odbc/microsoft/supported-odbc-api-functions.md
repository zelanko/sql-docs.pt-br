---
title: Funções de API ODBC com suporte | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9dafa6325901e289b54915bde19189b5bac69aeb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68080698"
---
# <a name="supported-odbc-api-functions"></a>Funções de API do ODBC com suporte
A finalidade do nivelamento é informar ao aplicativo quais recursos estão disponíveis para ele do driver. Os drivers de banco de dados do Microsoft ODBC Desktop dão suporte a todas as funções de núcleo e nível 1.  
  
 Para obter mais informações sobre níveis de conformidade para funções e gramática, consulte [níveis de conformidade](../../odbc/reference/develop-app/conformance-levels.md) na *referência do programador de ODBC*.  
  
 O suporte a funções da API ODBC pode ser dependente do driver usado. A tabela a seguir resume o suporte para o functions. A coluna mais à esquerda fornece um link para a página de referência geral de cada função. Essas páginas de referência são listadas em ordem alfabética na seção [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md) , sob [referência do programador de ODBC](../../odbc/reference/odbc-programmer-s-reference.md). As colunas à direita fornecem links para observações específicas do driver sobre cada função com suporte. Esses tópicos específicos de driver são listados na seção "outros detalhes de programação" para cada driver. Como alternativa, se os mesmos comentários sobre uma função se aplicarem a todos os drivers de banco de dados da área de trabalho ODBC, a coluna mais à direita fornecerá um link para um tópico que resume o suporte de drivers do banco de dados da área de trabalho para essa função. Esses tópicos são listados no final da seção atual ("funções de API ODBC com suporte").  
  
|Função ODBC|Acessar observações específicas do driver|observações específicas do driver do dBASE|Notas específicas do driver do Paradox|Observações específicas do driver de arquivo de texto|Notas específicas do driver do Excel|Observações relevantes para todos os drivers|  
|-------------------|-----------------------------------|----------------------------------|------------------------------------|--------------------------------------|----------------------------------|-----------------------------------|  
|[SQLBindParameter](../../odbc/reference/syntax/sqlbindparameter-function.md)|||||[Excel](../../odbc/microsoft/sqlbindparameter-excel-driver.md)||  
|[SQLColAttributes](../../odbc/reference/syntax/sqlcolattributes-function.md)|[Access](../../odbc/microsoft/sqlcolattributes-access-driver.md)|[dBASE](../../odbc/microsoft/sqlcolattributes-dbase-driver.md)|[Paradox](../../odbc/microsoft/sqlcolattributes-paradox-driver.md)|[Arquivo de texto](../../odbc/microsoft/sqlcolattributes-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlcolattributes-excel-driver.md)||  
|[SQLColumns](../../odbc/reference/syntax/sqlcolattributes-function.md)|[Access](../../odbc/microsoft/sqlcolattributes-access-driver.md)|[dBASE](../../odbc/microsoft/sqlcolattributes-dbase-driver.md)|[Paradox](../../odbc/microsoft/sqlcolattributes-paradox-driver.md)|[Arquivo de texto](../../odbc/microsoft/sqlcolattributes-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlcolattributes-excel-driver.md)||  
|[SQLConfigDataSource](../../odbc/reference/syntax/sqlconfigdatasource-function.md)|[Access](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)|[dBASE](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)|[Paradox](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)|[Arquivo de texto](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)|[Excel](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)||  
|[SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md)|[Access](../../odbc/microsoft/sqldriverconnect-access-driver.md)|[dBASE](../../odbc/microsoft/sqldriverconnect-dbase-driver.md)|[Paradox](../../odbc/microsoft/sqldriverconnect-paradox-driver.md)|[Arquivo de texto](../../odbc/microsoft/sqldriverconnect-text-file-driver.md)|[Excel](../../odbc/microsoft/sqldriverconnect-excel-driver.md)||  
|[SQLGetCursorName](../../odbc/reference/syntax/sqlgetcursorname-function.md)||||||[Todos os drivers](../../odbc/microsoft/sqlgetcursorname-desktop-database-drivers.md)|  
|[SQLGetData](../../odbc/reference/syntax/sqlgetdata-function.md)||||||[Todos os drivers](../../odbc/microsoft/sqlgetdata-desktop-database-drivers.md)|  
|[SQLGetInfo](../../odbc/reference/syntax/sqlgetinfo-function.md)|[Access](../../odbc/microsoft/sqlgetinfo-access-driver.md)|[dBASE](../../odbc/microsoft/sqlgetinfo-dbase-driver.md)|[Paradox](../../odbc/microsoft/sqlgetinfo-paradox-driver.md)|[Arquivo de texto](../../odbc/microsoft/sqlgetinfo-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlgetinfo-excel-driver.md)|
|[SQLGetStmtOption](../../odbc/reference/syntax/sqlgetstmtoption-function.md)||||||[Todos os drivers](../../odbc/microsoft/sqlgetstmtoption-desktop-database-drivers.md)|  
|[SQLGetTypeInfo](../../odbc/reference/syntax/sqlgettypeinfo-function.md)|[Access](../../odbc/microsoft/sqlgettypeinfo-access-driver.md)|[dBASE](../../odbc/microsoft/sqlgettypeinfo-dbase-driver.md)|[Paradox](../../odbc/microsoft/sqlgettypeinfo-paradox-driver.md)|[Arquivo de texto](../../odbc/microsoft/sqlgettypeinfo-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlgettypeinfo-excel-driver.md)||  
|[SQLMoreResults](../../odbc/reference/syntax/sqlmoreresults-function.md)||||||[Todos os drivers](../../odbc/microsoft/sqlmoreresults-desktop-database-drivers.md)|  
|[SQLPrepare](../../odbc/reference/syntax/sqlprepare-function.md)||||||[Todos os drivers](../../odbc/microsoft/sqlprepare-desktop-database-drivers.md)|  
|[SQLProcedureColumns](../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|[Access](../../odbc/microsoft/sqlprocedurecolumns-access-driver.md)||||||  
|[SQLProcedures](../../odbc/reference/syntax/sqlprocedures-function.md)||||||[Todos os drivers](../../odbc/microsoft/sqlprocedures-desktop-database-drivers.md)|  
|[SQLSetConnectOption](../../odbc/reference/syntax/sqlsetconnectoption-function.md)|[Access](../../odbc/microsoft/sqlsetconnectoption-access-driver.md)|[dBASE](../../odbc/microsoft/sqlsetconnectoption-dbase-driver.md)|[Paradox](../../odbc/microsoft/sqlsetconnectoption-paradox-driver.md)|[Arquivo de texto](../../odbc/microsoft/sqlsetconnectoption-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlsetconnectoption-excel-driver.md)||  
|[SQLSetCursorName](../../odbc/reference/syntax/sqlsetcursorname-function.md)||||||[Todos os drivers](../../odbc/microsoft/sqlsetcursorname-desktop-database-drivers.md)|  
|[SQLSetPos](../../odbc/reference/syntax/sqlsetpos-function.md)||||||[Todos os drivers](../../odbc/microsoft/sqlsetpos-desktop-database-drivers.md)|  
|[SQLSetScrollOptions](../../odbc/reference/syntax/sqlsetscrolloptions-function.md)||||||[Todos os drivers](../../odbc/microsoft/sqlsetscrolloptions-desktop-database-drivers.md)|  
|[SQLSetStmtOption](../../odbc/reference/syntax/sqlsetstmtoption-function.md)||||||[Todos os drivers](../../odbc/microsoft/sqlsetstmtoption-desktop-database-drivers.md)|  
|[SQLSpecialColumns](../../odbc/reference/syntax/sqlspecialcolumns-function.md)||||||[Todos os drivers](../../odbc/microsoft/sqlspecialcolumns-desktop-database-drivers.md)|  
|[SQLStatistics](../../odbc/reference/syntax/sqlstatistics-function.md)|[Access](../../odbc/microsoft/sqlstatistics-access-driver.md)|[dBASE](../../odbc/microsoft/sqlstatistics-dbase-driver.md)|[Paradox](../../odbc/microsoft/sqlstatistics-paradox-driver.md)|[Arquivo de texto](../../odbc/microsoft/sqlstatistics-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlstatistics-excel-driver.md)||  
|[SQLTables](../../odbc/reference/syntax/sqltables-function.md)|[Access](../../odbc/microsoft/sqltables-access-driver.md)|[dBASE](../../odbc/microsoft/sqltables-dbase-driver.md)|[Paradox](../../odbc/microsoft/sqltables-paradox-driver.md)|[Arquivo de texto](../../odbc/microsoft/sqltables-text-file-driver.md)|[Excel](../../odbc/microsoft/sqltables-excel-driver.md)|  
|[SQLTransact](../../odbc/reference/syntax/sqltransact-function.md)|[Access](../../odbc/microsoft/sqltransact-access-driver.md)|[dBASE](../../odbc/microsoft/sqltransact-dbase-driver.md)|[Paradox](../../odbc/microsoft/sqltransact-paradox-driver.md)|[Arquivo de texto](../../odbc/microsoft/sqltransact-text-file-driver.md)|[Excel](../../odbc/microsoft/sqltransact-excel-driver.md)||  
  
 Os tópicos a seguir fornecem comentários sobre as funções ODBC. Esses comentários se aplicam a todos os drivers de banco de dados de desktop ODBC.  
  
-   [SQLGetData (Drivers de banco de dados de área de trabalho)](../../odbc/microsoft/sqlgetdata-desktop-database-drivers.md)  
  
-   [SQLGetStmtOption (drivers de banco de dados de desktop)](../../odbc/microsoft/sqlgetstmtoption-desktop-database-drivers.md)  
  
-   [SQLMoreResults (Drivers de banco de dados de área de trabalho)](../../odbc/microsoft/sqlmoreresults-desktop-database-drivers.md)  
  
-   [SQLPrepare (Drivers de banco de dados de área de trabalho)](../../odbc/microsoft/sqlprepare-desktop-database-drivers.md)  
  
-   [SQLProcedures (Drivers de banco de dados de área de trabalho)](../../odbc/microsoft/sqlprocedures-desktop-database-drivers.md)  
  
-   [SQLSetCursorName (Drivers de banco de dados de área de trabalho)](../../odbc/microsoft/sqlsetcursorname-desktop-database-drivers.md)  
  
-   [SQLSetPos (Drivers de banco de dados de área de trabalho)](../../odbc/microsoft/sqlsetpos-desktop-database-drivers.md)  
  
-   [SQLSetScrollOptions (Drivers de banco de dados de área de trabalho)](../../odbc/microsoft/sqlsetscrolloptions-desktop-database-drivers.md)  
  
-   [SQLSetStmtOption (Drivers de banco de dados de área de trabalho)](../../odbc/microsoft/sqlsetstmtoption-desktop-database-drivers.md)  
  
-   [SQLSpecialColumns (Drivers de banco de dados de área de trabalho)](../../odbc/microsoft/sqlspecialcolumns-desktop-database-drivers.md)
