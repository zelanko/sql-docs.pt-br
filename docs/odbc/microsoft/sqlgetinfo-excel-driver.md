---
title: SQLGetInfo (Driver do Excel) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLGetInfo
- SQLGetInfo function [ODBC], Excel Driver
ms.assetid: fed4aea2-6d3d-4199-a5db-3d033eb63927
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9357c66b494b00e7533f7aab00028fe19c1975af
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetinfo-excel-driver"></a>SQLGetInfo (Driver do Excel)
> [!NOTE]  
>  Este tópico fornece informações específicas de Driver do Excel. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLGetInfo** oferece suporte ao tipo de informações SQL_FILE_USAGE. O valor retornado é um inteiro de 16 bits que indica como o driver trata diretamente os arquivos em uma fonte de dados:  
  
-   SQL_FILE_NOT_SUPPORTED — O driver não é um driver de camada única.  
  
-   SQL_FILE_TABLE — Um driver de camada única trata arquivos em uma fonte de dados como tabelas.  
  
-   SQL_FILE_QUALIFIER — Um driver de camada única trata arquivos em uma fonte de dados como um qualificador.  
  
 O driver ODBC retorna SQL_FILE_TABLE para Microsoft Exceldriver porque cada arquivo é uma tabela.  
  
## <a name="sqldbmsver"></a>SQL_DBMS_VER  
  
|ISAM|Versão|Formato de números de versão|  
|----------|-------------|-------------------------------|  
|Microsoft Excel|3.0|03.00.0000|  
||4.0|04.00.0000|  
||5.0/7.0|05.00.0000|  
||97/2000|08.00.0000|  
  
## <a name="sqlfileusage"></a>SQL_FILE_USAGE  
 SQL_FILE_TABLE (Excel 3.0/4.0)  
  
 SQL_FILE_CATALOG (Excel 5.0/7.0)  
  
## <a name="sqlmaxcharliterallen"></a>SQL_MAX_CHAR_LITERAL_LEN  
 255 (3.0/4.0/5.0/7.0 Excel)  
  
 65535 (Excel 97)  
  
## <a name="sqlmaxcolumnnamelen"></a>SQL_MAX_COLUMN_NAME_LEN  
 30 (Excel 3.0/4.0)  
  
 64 (5.0/7.0/97 Excel)  
  
## <a name="sqlmaxtablenamelen"></a>SQL_MAX_TABLE_NAME_LEN  
 12 (Excel 3.0/4.0)  
  
 31 (5.0/7.0/97 Excel)  
  
## <a name="sqlcatalognameseparator"></a>SQL_CATALOG_NAME_SEPARATOR  
 "\\" (Excel 3.0/4.0)  
  
 "." (5.0/7.0/97 do excel)  
  
## <a name="sqlcatalogterm"></a>SQL_CATALOG_TERM  
 "Directory" (Excel 3.0/4.0)  
  
 "Pasta de trabalho" (5.0/7.0/97 Excel)  
  
## <a name="sqlcatalogusage"></a>SQL_CATALOG_USAGE  
 SQL_QU_DML_STATEMENTS &AMP;#124; SQL_QU_TABLE_DEFINITION  
  
## <a name="sqltimedatefunctions"></a>SQL_TIMEDATE_FUNCTIONS  
 SQL_FN_TD_CURDATE &AMP;#124; SQL_FN_TD_CURTIME &AMP;#124; SQL_FN_TD_DAYOFMONTH &AMP;#124; SQL_FN_TD_DAYOFWEEK &AMP;#124; SQL_FN_TD_DAYOFYEAR &AMP;#124; SQL_FN_TD_HOUR &AMP;#124; SQL_FN_TD_MINUTE &AMP;#124; SQL_FN_TD_MONTH &AMP;#124; SQL_FN_TD_NOW &AMP;#124; SQL_FN_TD_SECOND &AMP;#124; SQL_FN_TD_WEEK &AMP;#124; SQL_FN_TD_YEAR
