---
title: SQLGetInfo (Driver Paradoxo) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Paradox driver [ODBC], SQLGetInfo
- SQLGetInfo function [ODBC], Paradox Driver
ms.assetid: 43aab762-68f4-4128-b8f5-8878ea5f1258
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 354fa7f08797ee1fbfb057bfc2f2c192a8c5eddc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298566"
---
# <a name="sqlgetinfo-paradox-driver"></a>SQLGetInfo (Driver do Paradox)
> [!NOTE]  
>  Este tópico fornece informações específicas do Paradox Driver. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **O SQLGetInfo** suporta o SQL_FILE_USAGE tipo de informação. O valor retornado é um inteiro de 16 bits que indica como o driver trata diretamente os arquivos em uma fonte de dados:  
  
-   SQL_FILE_NOT_SUPPORTED - O motorista não é um motorista de nível único.  
  
-   SQL_FILE_TABLE - Um driver de nível único trata arquivos em uma fonte de dados como tabelas.  
  
-   SQL_FILE_QUALIFIER - Um driver de nível único trata arquivos em uma fonte de dados como um qualificador.  
  
 O driver ODBC retorna SQL_FILE_TABLE porque cada arquivo é uma tabela.  
  
## <a name="sql_alter_table"></a>SQL_ALTER_TABLE  
 SQL_AT_ADD_COLUMN &#124; SQL_AT_DROP_COLUMN  
  
## <a name="sql_ddl_index"></a>SQL_DDL_INDEX  
 SQL_DL_CREATE_INDEX  
  
 SQL_DL_DROP_INDEX  
  
## <a name="sql_dbms_ver"></a>SQL_DBMS_VER  
  
|Isam|Versão|Formato dos números de versão|  
|----------|-------------|-------------------------------|  
|Paradoxo|3.x|03.00.0000|  
||4.x|04.00.0000|  
||5.x|05.00.0000|  
  
## <a name="sql_catalog_usage"></a>SQL_CATALOG_USAGE  
 SQL_QU_DML_STATEMENTS &#124; SQL_QU_TABLE_DEFINITION &#124; SQL_QU_INDEX_DEFINITION  
  
## <a name="sql_timedate_functions"></a>SQL_TIMEDATE_FUNCTIONS  
 SQL_FN_TD_DAYOFMONTH &#124; SQL_FN_TD_DAYOFWEEK &#124; SQL_FN_TD_DAYOFYEAR &#124; SQL_FN_TD_HOUR &#124; SQL_FN_TD_MINUTE &#124; SQL_FN_TD_MONTH &#124; SQL_FN_TD_SECOND &#124; SQL_FN_TD_WEEK &#124; SQL_FN_TD_YEAR
