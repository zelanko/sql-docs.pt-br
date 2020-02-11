---
title: SQLGetInfo (driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetInfo function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: fbc39e3d-67d9-4331-bf5f-76dbd74c4c45
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 14837bc5ba3368fbb0d33680ee1c54936ab0a224
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67898844"
---
# <a name="sqlgetinfo-visual-foxpro-odbc-driver"></a>SQLGetInfo (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: completo  
  
 Conformidade da API ODBC: nível 1  
  
 Retorna informações gerais sobre o driver ODBC do Visual FoxPro e a fonte de dados associada a um identificador de conexão, *HDBC*. A lista a seguir mostra o valor retornado pelo driver ODBC do Visual FoxPro para cada argumento *fInfoType* e comentários sobre os valores retornados.  
  
 Para obter mais informações, consulte [SQLGetInfo](../../odbc/reference/syntax/sqlgetinfo-function.md) na *referência do programador de ODBC*.  
  
## <a name="a"></a>Um  
 SQL_ACCESSIBLE_PROCEDURES retorna ' n'.  
  
 SQL_ACCESSIBLE_TABLES retorna ' Y '.  
  
 SQL_ACTIVE_CONNECTIONS retorna 0.  
  
 SQL_ACTIVE_STATEMENTS retorna 0.  
  
 SQL_ALTER_TABLE retorna SQL_AT_ADD_COLUMN ou SQL_AT_DROP_COLUMN.  
  
## <a name="b"></a>B  
 SQL_BOOKMARK_PERSISTENCE retorna SQL_BP_SCROLL.  
  
## <a name="c"></a>C  
 SQL_COLUMN_ALIAS retorna ' Y '.  
  
 SQL_CONCAT_NULL_BEHAVIOR retorna SQL_CB_NULL.  
  
 SQL_CONVERT_BIGINT retorna 0. O driver ODBC do Visual FoxPro não dá suporte a *bigint*.  
  
 SQL_CONVERT_BINARY retorna 0.  
  
 SQL_CONVERT_BIT retorna 0.  
  
 SQL_CONVERT_CHAR retorna 0.  
  
 SQL_CONVERT_DATE retorna 0.  
  
 SQL_CONVERT_DECIMAL retorna 0.  
  
 SQL_CONVERT_DOUBLE retorna 0.  
  
 SQL_CONVERT_FLOAT retorna 0.  
  
 SQL_CONVERT_INTEGER retorna 0.  
  
 SQL_CONVERT_LONGVARBINARY retorna 0.  
  
 SQL_CONVERT_LONGVARCHAR retorna 0.  
  
 SQL_CONVERT_NUMERIC retorna 0.  
  
 SQL_CONVERT_REAL retorna 0.  
  
 SQL_CONVERT_SMALLINT retorna 0.  
  
 SQL_CONVERT_TIME retorna 0.  
  
 SQL_CONVERT_TIMESTAMP retorna 0.  
  
 SQL_CONVERT_TINYINT retorna 0.  
  
 SQL_CONVERT_VARBINARY retorna 0.  
  
 SQL_CONVERT_VARCHAR retorna 0.  
  
 SQL_CONVERT_FUNCTIONS retorna 0.  
  
 SQL_CORRELATION_NAME retorna SQL_CN_ANY.  
  
 SQL_CURSOR_COMMIT_BEHAVIOR retorna SQL_CB_PRESERVE.  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR retorna SQL_CB_PRESERVE.  
  
## <a name="d"></a>D  
 SQL_DATA_SOURCE_NAME retorna o valor passado como DSN para [SQLConnect](../../odbc/microsoft/sqlconnect-visual-foxpro-odbc-driver.md)ou [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md); Retorna uma cadeia de caracteres vazia se nenhum DSN for especificado.  
  
 SQL_DATA_SOURCE_READ_ONLY retorna ' n'.  
  
 SQL_DATABASE_NAME retornará um caminho UNC completo para o banco de dados atual se a fonte for um [banco](../../odbc/microsoft/visual-foxpro-terminology.md)de dado. Se a fonte de dados se conectar a um diretório de [tabelas](../../odbc/microsoft/visual-foxpro-terminology.md), a função retornará o caminho para o diretório.  
  
 SQL_DBMS_NAME retorna "Visual FoxPro".  
  
 SQL_DBMS_VER retorna "03.00.0000".  
  
 SQL_DEFAULT_TXN_ISOLATION retorna SQL_TXN_READ_COMMITTED. Leituras sujas não são possíveis, mas leituras e fantasmas não repetíveis são possíveis.  
  
 O SQL_DRIVER_HDBC é implementado pelo Gerenciador de driver.  
  
 O SQL_DRIVER_HENV é implementado pelo Gerenciador de driver.  
  
 O SQL_DRIVER_HLIB é implementado pelo Gerenciador de driver.  
  
 O SQL_DRIVER_HSTMT é implementado pelo Gerenciador de driver.  
  
 SQL_DRIVER_NAME retorna "vfpodbc. dll".  
  
 SQL_DRIVER_ODBC_VER retorna "2,50" (SQL_SPEC_MAJOR, SQL_SPEC_MINOR).  
  
 SQL_DRIVER_VER retorna "01.00.0000".  
  
## <a name="e"></a>E  
 SQL_EXPRESSIONS_IN_ORDERBY retorna ' n'.  
  
## <a name="f"></a>F  
 SQL_FETCH_DIRECTION retorna:  
  
-   SQL_FD_FETCH_NEXT  
  
-   SQL_FD_FETCH_FIRST  
  
-   SQL_FD_FETCH_LAST  
  
-   SQL_FD_FETCH_PRIOR  
  
-   SQL_FD_FETCH_ABSOLUTE  
  
-   SQL_FD_FETCH_RELATIVE  
  
-   SQL_FD_FETCH_BOOKMARK.  
  
 SQL_FILE_USAGE retorna SQL_FILE_QUALIFIER para o banco de dados (arquivo. DBC) e para as fontes de dado da tabela livre (arquivo. dbf).  
  
## <a name="g-h"></a>G-H  
 SQL_GETDATA_EXENSIONS retorna:  
  
-   SQL_GD_ANY_COLUMN  
  
-   SQL_GD_ANY_BLOCK  
  
-   SQL_GD_ANY_BOUND  
  
-   SQL_GD_ANY_ORDER  
  
 SQL_GROUP_BY retorna SQL_GB_NO_RELATION.  
  
## <a name="i-j"></a>I-J  
 SQL_IDENTIFIER_CASE retorna SQL_IC_MIXED.  
  
 SQL_IDENTIFIER_QUOTE_CHAR retorna '.  
  
## <a name="k"></a>K  
 SQL_KEYWORDS retorna "".  
  
## <a name="l"></a>L  
 SQL_LIKE_ESCAPE_CLAUSE retorna ' n'.  
  
 SQL_LOCK_TYPES retorna SQL_LCK_NO_CHANGE.  
  
## <a name="m"></a>M  
 SQL_MAX_BINARY_LITERAL_LEN retorna 0.  
  
 SQL_MAX_CHAR_LITERAL_LEN retorna 254.  
  
 SQL_MAX_COLUMN_NAME_LEN retorna 128.  
  
 SQL_MAX_COLUMNS_IN_GROUP_BY retorna 16.  
  
 SQL_MAX_COLUMNS_IN_ORDER_BY retorna 16.  
  
 SQL_MAX_COLUMNS_IN_INDEX retorna 0.  
  
 SQL_MAX_COLUMNS_IN_SELECT retorna 254.  
  
 SQL_MAX_COLUMNS_IN_TABLE retorna 254.  
  
 SQL_MAX_CURSOR_NAME_LEN retorna 254.  
  
 SQL_MAX_INDEX_SIZE retorna 0.  
  
 SQL_MAX_OWNER_NAME_LEN retorna 0.  
  
 SQL_MAX_PROCEDURE_NAME_LEN retorna 0. O driver ODBC do Visual FoxPro não permite acesso direto aos procedimentos armazenados do Visual FoxPro.  
  
 SQL_MAX_QUALIFIER_NAME_LEN retorna o comprimento máximo do caminho do sistema operacional.  
  
 SQL_MAX_ROW_SIZE retorna 254 ^ 2.  
  
 SQL_MAX_ROW_SIZE_INCLUDES_LONG retorna ' n'.  
  
 SQL_MAX_STATEMENT_LEN retorna 8192.  
  
 SQL_MAX_TABLE_NAME_LEN retorna 128.  
  
 SQL_MAX_TABLES_IN_SELECT retorna 16.  
  
 SQL_MAX_USER_NAME_LEN retorna 0.  
  
 SQL_MULT_RESULT_SETS retorna ' Y '.  
  
 SQL_MULTIPLE_ACTIVE_TXN retorna ' Y '. Várias conexões podem ter várias transações abertas ao mesmo tempo.  
  
## <a name="n"></a>N  
 SQL_NEED_LONG_DATA_LEN retorna ' n'.  
  
 SQL_NON_NULLABLE_COLUMNS retorna SQL_NNC_NON_NULL.  
  
 SQL_NULL_COLLATION retorna SQL_NC_LOW.  
  
 SQL_NUMERIC_FUNCTIONS retorna todas as funções, exceto SQL_FN_NUM_POWER, que não tem suporte pelo driver ODBC do Visual FoxPro. Há suporte para as seguintes funções:  
  
-   SQL_FN_NUM_ABS  
  
-   SQL_FN_NUM_ACOS  
  
-   SQL_FN_NUM_ASIN  
  
-   SQL_FN_NUM_ATAN  
  
-   SQL_FN_NUM_ATAN2  
  
-   SQL_FN_NUM_CELING  
  
-   SQL_FN_NUM_COS  
  
-   SQL_FN_NUM_COT  
  
-   SQL_FN_NUM_DEGREES  
  
-   SQL_FN_NUM_EXP  
  
-   SQL_FN_NUM_FLOOR  
  
-   SQL_FN_NUM_LOG  
  
-   SQL_FN_NUM_LOG10  
  
-   SQL_FN_NUM_MOD  
  
-   SQL_FN_NUM_PI  
  
-   SQL_FN_NUM_RADIANS  
  
-   SQL_FN_NUM_RAND  
  
-   SQL_FN_NUM_ROUND  
  
-   SQL_FN_NUM_SIGN  
  
-   SQL_FN_NUM_SIN  
  
-   SQL_FN_NUM_SQRT  
  
-   SQL_FN_NUM_TAN  
  
## <a name="o"></a>O  
 SQL_ODBC_API_CONFORMANCE retorna SQL_OAC_LEVEL1.  
  
 SQL_ODBC_SAG_CLI_CONFORMANCE retorna SQL_OSCC_COMPLIANT.  
  
 SQL_ODBC_SQL_CONFORMANCE retorna SQL_OSC_MINIMUM. Há suporte para a sintaxe SQL mínima.  
  
 SQL_ODBC_SQL_OPT_IEF retorna "N".  
  
 O SQL_ODBC_VER é implementado pelo Gerenciador de driver.  
  
 SQL_ORDER_BY_COLUMNS_IN_SELECT retorna "N".  
  
 SQL_OUTER_JOINS retorna "N".  
  
 SQL_OWNER_TERM retorna "". O driver ODBC do Visual FoxPro não oferece suporte a proprietários para seus objetos.  
  
 SQL_OWNER_USAGE retorna 0. O driver ODBC do Visual FoxPro não oferece suporte a proprietários para seus objetos.  
  
## <a name="p"></a>P  
 SQL_POS_OPERATIONS retorna SQL_POS_POSITION.  
  
 SQL_POSITIONED_STATEMENTS retorna 0.  
  
 SQL_PROCEDURE_TERM retorna "".  
  
 SQL_PROCEDURES retorna ' n'.  
  
## <a name="q"></a>Q  
 SQL_QUALIFIER_LOCATION retorna SQL_QL_START.  
  
 SQL_QUALIFIER_NAME_SEPARATOR retorna '! ' ou '\\'. O separador entre Database e Table é '! ' para fontes de dados conectadas aos [bancos](../../odbc/microsoft/visual-foxpro-terminology.md)de\\dados e ' ' para fontes de dado que são diretórios de [tabelas livres](../../odbc/microsoft/visual-foxpro-terminology.md).  
  
 SQL_QUALIFIER_TERM retorna "Database" ou "Directory". O qualificador é "Database" para fontes de dados conectadas a [bancos](../../odbc/microsoft/visual-foxpro-terminology.md)de dados e "Directory" para fontes de dado que são diretórios de [tabelas livres](../../odbc/microsoft/visual-foxpro-terminology.md).  
  
 SQL_QUALIFIER_USAGE não oferece suporte a SQL_QU_PRIVILEGE_DEFINITION; Ele retorna SQL_QU_DML_STATEMENT ou SQL_QU_TABLE_DEFINITION.  
  
 SQL_QUOTED_IDENTIFIER_CASE retorna SQL_IC_MIXED.  
  
## <a name="r"></a>R  
 SQL_ROW_UPDATES retorna "N". O driver ODBC do Visual FoxPro dá suporte apenas a cursores estáticos e progressivos.  
  
## <a name="s"></a>S  
 SQL_SCROLL_CONCURRENCY retorna SQL_SCCO_READ_ONLY.  
  
 SQL_SCROLL_OPTIONS retorna SQL_SO_STATIC ou SQL_SO_READONLY.  
  
 SQL_SEARCH_PATTERN_ESCAPE retorna "\\".  
  
 SQL_SERVER_NAME retorna "".  
  
 SQL_SPECIAL_CHARACTERS retorna "~ @ # $% ^".  
  
 SQL_STATIC_SENSITIVITY retorna 0. O driver ODBC do Visual FoxPro não oferece suporte a atualizações posicionais.  
  
 SQL_STRING_FUNCTIONS não oferece suporte a SQL_FN_STR_INSERT, SQL_FN_STR_LOCATE, SQL_FN_STR_LOCATE_2 ou SQL_FN_STR_SOUNDEX.  
  
 Ele retorna:  
  
-   SQL_FN_STR_ASCII  
  
-   SQL_FN_STR_CHAR  
  
-   SQL_FN_STR_CONCAT  
  
-   SQL_FN_STR_DIFFERENCE  
  
-   SQL_FN_STR_LCASE  
  
-   SQL_FN_STR_LEFT  
  
-   SQL_FN_STR_LENGTH  
  
-   SQL_FN_STR_LTRIM  
  
-   SQL_FN_STR_REPEAT  
  
-   SQL_FN_STR_REPLACE  
  
-   SQL_FN_STR_RIGHT  
  
-   SQL_FN_STR_RTRIM  
  
-   SQL_FN_STR_SUBSTRING  
  
-   SQL_FN_STR_UCASE  
  
-   SQL_FN_STR_SPACE.  
  
 SQL_SUBQUERIES retorna:  
  
-   SQL_SQ_CORRELATED_SUBQUERIES  
  
-   SQL_SQ_COMPARISON  
  
-   SQL_SQ_EXISTS  
  
-   SQL_SQ_IN  
  
-   SQL_SQ_QUANTIFIED.  
  
 SQL_SYSTEM_FUNCTIONS retorna:  
  
-   SQL_FN_SYS_DBNAME  
  
-   SQL_FN_SYS_IFNULL  
  
 Mas não:  
  
-   SQL_FN_SYS_USERNAME  
  
## <a name="t"></a>T  
 SQL_TABLE_TERM retorna "Table".  
  
 SQL_TIMEDATE_ADD_INTERVALS retorna:  
  
-   SQL_FN_TSI_ SEGUNDO  
  
-   SQL_FN_TSI_MINUTE  
  
-   SQL_FN_TSI_HOUR  
  
-   SQL_FN_TSI_DAY  
  
-   SQL_FN_TSI_MONTH  
  
-   SQL_FN_TSI_YEAR  
  
 Mas não:  
  
-   SQL_FN_TSI_FRAC_SECOND  
  
-   SQL_FN_TSI_WEEK  
  
-   SQL_FN_TSI_QUARTER  
  
 SQL_TIMEDATE_DIFF_INTERVALS retorna:  
  
-   SQL_FN_TSI_ SEGUNDO  
  
-   SQL_FN_TSI_MINUTE  
  
-   SQL_FN_TSI_HOUR  
  
-   SQL_FN_TSI_DAY  
  
-   SQL_FN_TSI_MONTH  
  
-   SQL_FN_TSI_YEAR  
  
 SQL_TIMEDATE_FUNCTIONS não oferece suporte a SQL_FN_TD_QUARTER, SQL_FN_TD_TIMESTAMPADD, SQL_FN_TD_DAYOFYEAR ou SQL_FN_TD_WEEK.  
  
 Ele retorna:  
  
-   SQL_FN_TD_CURDATE  
  
-   SQL_FN_TD_CURTIME  
  
-   SQL_FN_TD_DAYNAME  
  
-   SQL_FN_TD_DAYOFMONTH  
  
-   SQL_FN_TD_DAYOFWEEK  
  
-   SQL_FN_TD_HOUR  
  
-   SQL_FN_TD_MINUTE  
  
-   SQL_FN_TD_MONTH  
  
-   SQL_FN_TD_MONTHNAME  
  
-   SQL_FN_TD_NOW  
  
-   SQL_FN_TD_SECOND  
  
-   SQL_FN_TD_TIMESTAMPDIFF  
  
-   SQL_FN_TD_YEAR.  
  
 SQL_TXN_CAPABLE retorna SQL_TC_DML.  
  
 SQL_TXN_ISOLATION_OPTION retorna SQL_TXN_READ_COMMITTED.  
  
## <a name="u-z"></a>U-Z  
 SQL_UNION retorna SQL_U_UNION ou SQL_U_UNION_ALL.  
  
 SQL_USER_NAME retorna \<> em branco.
