---
title: SQLGetInfo (visual FoxPro ODBC Driver) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2d4b976083b46bf632c4890c7fce3b0f13a9a761
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295186"
---
# <a name="sqlgetinfo-visual-foxpro-odbc-driver"></a>SQLGetInfo (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver Visual FoxPro ODBC. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: Completo  
  
 Conformidade da API ODBC: Nível 1  
  
 Retorna informações gerais sobre o Driver Visual FoxPro ODBC e fonte de dados associada a uma alça de conexão, *hdbc*. A lista a seguir mostra o valor devolvido pelo Driver Visual FoxPro ODBC para cada argumento *fInfoType* e comentários sobre os valores retornados.  
  
 Para obter mais informações, consulte [SQLGetInfo](../../odbc/reference/syntax/sqlgetinfo-function.md) no *Programador ODBC .*  
  
## <a name="a"></a>Um  
 SQL_ACCESSIBLE_PROCEDURES retorna 'N'.  
  
 SQL_ACCESSIBLE_TABLES devolve 'Y'.  
  
 SQL_ACTIVE_CONNECTIONS retorna 0.  
  
 SQL_ACTIVE_STATEMENTS retorna 0.  
  
 SQL_ALTER_TABLE retorna SQL_AT_ADD_COLUMN ou SQL_AT_DROP_COLUMN.  
  
## <a name="b"></a>B  
 SQL_BOOKMARK_PERSISTENCE volta SQL_BP_SCROLL.  
  
## <a name="c"></a>C  
 SQL_COLUMN_ALIAS devolve 'Y'.  
  
 SQL_CONCAT_NULL_BEHAVIOR returns SQL_CB_NULL.  
  
 SQL_CONVERT_BIGINT retorna 0. O driver Visual FoxPro ODBC não suporta *BigInt*.  
  
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
  
 SQL_CORRELATION_NAME volta SQL_CN_ANY.  
  
 SQL_CURSOR_COMMIT_BEHAVIOR volta SQL_CB_PRESERVE.  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR volta SQL_CB_PRESERVE.  
  
## <a name="d"></a>D  
 SQL_DATA_SOURCE_NAME retorna o valor passado como DSN para [SQLConnect](../../odbc/microsoft/sqlconnect-visual-foxpro-odbc-driver.md)ou [SQLDriverConnect;](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md) retorna uma seqüência de string vazia se nenhum DSN for especificado.  
  
 SQL_DATA_SOURCE_READ_ONLY retorna 'N'.  
  
 SQL_DATABASE_NAME retorna um caminho UNC completo para o banco de dados atual se a fonte de dados for um [banco de dados](../../odbc/microsoft/visual-foxpro-terminology.md). Se a fonte de dados se conectar a um diretório de [tabelas,](../../odbc/microsoft/visual-foxpro-terminology.md)a função retorna o caminho para o diretório.  
  
 SQL_DBMS_NAME retorna "Visual FoxPro".  
  
 SQL_DBMS_VER retorna "03.00.0000".  
  
 SQL_DEFAULT_TXN_ISOLATION volta SQL_TXN_READ_COMMITTED. Leituras sujas não são possíveis, mas leituras não repetíveis e fantasmas são possíveis.  
  
 SQL_DRIVER_HDBC é implementado pelo Driver Manager.  
  
 SQL_DRIVER_HENV é implementado pelo Driver Manager.  
  
 SQL_DRIVER_HLIB é implementado pelo Driver Manager.  
  
 SQL_DRIVER_HSTMT é implementado pelo Driver Manager.  
  
 SQL_DRIVER_NAME retorna "vfpodbc.dll".  
  
 SQL_DRIVER_ODBC_VER retorna "02,50" (SQL_SPEC_MAJOR, SQL_SPEC_MINOR).  
  
 SQL_DRIVER_VER retorna "01.00.0000".  
  
## <a name="e"></a>E  
 SQL_EXPRESSIONS_IN_ORDERBY retorna 'N'.  
  
## <a name="f"></a>F  
 SQL_FETCH_DIRECTION retorna:  
  
-   SQL_FD_FETCH_NEXT  
  
-   SQL_FD_FETCH_FIRST  
  
-   SQL_FD_FETCH_LAST  
  
-   SQL_FD_FETCH_PRIOR  
  
-   SQL_FD_FETCH_ABSOLUTE  
  
-   SQL_FD_FETCH_RELATIVE  
  
-   SQL_FD_FETCH_BOOKMARK.  
  
 SQL_FILE_USAGE retorna SQL_FILE_QUALIFIER tanto para fontes de dados de banco de dados (arquivo.dbc) quanto para fontes de dados de tabela gratuita (arquivo.dbf).  
  
## <a name="g-h"></a>G-H  
 SQL_GETDATA_EXENSIONS retorna:  
  
-   SQL_GD_ANY_COLUMN  
  
-   SQL_GD_ANY_BLOCK  
  
-   SQL_GD_ANY_BOUND  
  
-   SQL_GD_ANY_ORDER  
  
 SQL_GROUP_BY volta SQL_GB_NO_RELATION.  
  
## <a name="i-j"></a>I-J.  
 SQL_IDENTIFIER_CASE volta SQL_IC_MIXED.  
  
 SQL_IDENTIFIER_QUOTE_CHAR retorna..  
  
## <a name="k"></a>K  
 SQL_KEYWORDS retorna "".  
  
## <a name="l"></a>L  
 SQL_LIKE_ESCAPE_CLAUSE retorna 'N'.  
  
 SQL_LOCK_TYPES volta SQL_LCK_NO_CHANGE.  
  
## <a name="m"></a>M  
 SQL_MAX_BINARY_LITERAL_LEN retorna 0.  
  
 SQL_MAX_CHAR_LITERAL_LEN retorna 254.  
  
 SQL_MAX_COLUMN_NAME_LEN retorna 128.  
  
 SQL_MAX_COLUMNS_IN_GROUP_BY retorna 16.  
  
 SQL_MAX_COLUMNS_IN_ORDER_BY retorna em 16.  
  
 SQL_MAX_COLUMNS_IN_INDEX retorna 0.  
  
 SQL_MAX_COLUMNS_IN_SELECT retorna 254.  
  
 SQL_MAX_COLUMNS_IN_TABLE retorna 254.  
  
 SQL_MAX_CURSOR_NAME_LEN retorna 254.  
  
 SQL_MAX_INDEX_SIZE retorna 0.  
  
 SQL_MAX_OWNER_NAME_LEN retorna 0.  
  
 SQL_MAX_PROCEDURE_NAME_LEN retorna 0. O visual FoxPro ODBC Driver não permite acesso direto aos procedimentos armazenados pelo Visual FoxPro.  
  
 SQL_MAX_QUALIFIER_NAME_LEN retorna o comprimento máximo do caminho do sistema operacional.  
  
 SQL_MAX_ROW_SIZE retorna 254^2.  
  
 SQL_MAX_ROW_SIZE_INCLUDES_LONG retorna 'N'.  
  
 SQL_MAX_STATEMENT_LEN retorna 8192.  
  
 SQL_MAX_TABLE_NAME_LEN retorna 128.  
  
 SQL_MAX_TABLES_IN_SELECT retorna em 16.  
  
 SQL_MAX_USER_NAME_LEN retorna 0.  
  
 SQL_MULT_RESULT_SETS retorna 'Y'.  
  
 SQL_MULTIPLE_ACTIVE_TXN retorna 'Y'. Várias conexões podem ter várias transações abertas ao mesmo tempo.  
  
## <a name="n"></a>N  
 SQL_NEED_LONG_DATA_LEN retorna 'N'.  
  
 SQL_NON_NULLABLE_COLUMNS volta SQL_NNC_NON_NULL.  
  
 SQL_NULL_COLLATION volta SQL_NC_LOW.  
  
 SQL_NUMERIC_FUNCTIONS retorna todas as funções, exceto SQL_FN_NUM_POWER, que não é suportado pelo Visual FoxPro ODBC Driver. As seguintes funções são suportadas:  
  
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
 SQL_ODBC_API_CONFORMANCE volta SQL_OAC_LEVEL1.  
  
 SQL_ODBC_SAG_CLI_CONFORMANCE volta SQL_OSCC_COMPLIANT.  
  
 SQL_ODBC_SQL_CONFORMANCE volta SQL_OSC_MINIMUM. A sintaxe SQL mínima é suportada.  
  
 SQL_ODBC_SQL_OPT_IEF retorna "N".  
  
 SQL_ODBC_VER é implementado pelo Driver Manager.  
  
 SQL_ORDER_BY_COLUMNS_IN_SELECT retorna "N".  
  
 SQL_OUTER_JOINS retorna "N".  
  
 SQL_OWNER_TERM retorna "". O Visual FoxPro ODBC Driver não suporta proprietários de seus objetos.  
  
 SQL_OWNER_USAGE retorna 0. O Visual FoxPro ODBC Driver não suporta proprietários de seus objetos.  
  
## <a name="p"></a>P  
 SQL_POS_OPERATIONS returns SQL_POS_POSITION.  
  
 SQL_POSITIONED_STATEMENTS retorna 0.  
  
 SQL_PROCEDURE_TERM retorna "".  
  
 SQL_PROCEDURES retorna 'N'.  
  
## <a name="q"></a>Q  
 SQL_QUALIFIER_LOCATION volta SQL_QL_START.  
  
 SQL_QUALIFIER_NAME_SEPARATOR retorna '!'\\ou ''. O separador entre banco de dados e tabela é '!' para fontes de dados conectadas a [bancos de dados](../../odbc/microsoft/visual-foxpro-terminology.md)e '\\' para fontes de dados que são diretórios de [tabelas gratuitas](../../odbc/microsoft/visual-foxpro-terminology.md).  
  
 SQL_QUALIFIER_TERM retorna "banco de dados" ou "diretório". O qualificador é "banco de dados" para fontes de dados conectadas a [bancos de dados](../../odbc/microsoft/visual-foxpro-terminology.md)e "diretório" para fontes de dados que são diretórios de [tabelas gratuitas.](../../odbc/microsoft/visual-foxpro-terminology.md)  
  
 SQL_QUALIFIER_USAGE não suporta SQL_QU_PRIVILEGE_DEFINITION; ele retorna SQL_QU_DML_STATEMENT ou SQL_QU_TABLE_DEFINITION.  
  
 SQL_QUOTED_IDENTIFIER_CASE volta SQL_IC_MIXED.  
  
## <a name="r"></a>R  
 SQL_ROW_UPDATES retorna "N". O Visual FoxPro ODBC Driver suporta apenas cursores estáticos e avançados.  
  
## <a name="s"></a>S  
 SQL_SCROLL_CONCURRENCY volta SQL_SCCO_READ_ONLY.  
  
 SQL_SCROLL_OPTIONS retorna SQL_SO_STATIC ou SQL_SO_READONLY.  
  
 SQL_SEARCH_PATTERN_ESCAPE retorna".\\  
  
 SQL_SERVER_NAME retorna "".  
  
 SQL_SPECIAL_CHARACTERS retorna "~@#$%^".  
  
 SQL_STATIC_SENSITIVITY retorna 0. O Visual FoxPro ODBC Driver não suporta atualizações posicionais.  
  
 SQL_STRING_FUNCTIONS não suporta SQL_FN_STR_INSERT, SQL_FN_STR_LOCATE, SQL_FN_STR_LOCATE_2 ou SQL_FN_STR_SOUNDEX.  
  
 Isso retorna:  
  
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
  
 mas não:  
  
-   SQL_FN_SYS_USERNAME  
  
## <a name="t"></a>T  
 SQL_TABLE_TERM retorna "mesa".  
  
 SQL_TIMEDATE_ADD_INTERVALS retorna:  
  
-   segundo SQL_FN_TSI_  
  
-   SQL_FN_TSI_MINUTE  
  
-   SQL_FN_TSI_HOUR  
  
-   SQL_FN_TSI_DAY  
  
-   SQL_FN_TSI_MONTH  
  
-   SQL_FN_TSI_YEAR  
  
 mas não:  
  
-   SQL_FN_TSI_FRAC_SECOND  
  
-   SQL_FN_TSI_WEEK  
  
-   SQL_FN_TSI_QUARTER  
  
 SQL_TIMEDATE_DIFF_INTERVALS retorna:  
  
-   segundo SQL_FN_TSI_  
  
-   SQL_FN_TSI_MINUTE  
  
-   SQL_FN_TSI_HOUR  
  
-   SQL_FN_TSI_DAY  
  
-   SQL_FN_TSI_MONTH  
  
-   SQL_FN_TSI_YEAR  
  
 SQL_TIMEDATE_FUNCTIONS não suporta SQL_FN_TD_QUARTER, SQL_FN_TD_TIMESTAMPADD, SQL_FN_TD_DAYOFYEAR ou SQL_FN_TD_WEEK.  
  
 Isso retorna:  
  
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
  
 SQL_TXN_CAPABLE volta SQL_TC_DML.  
  
 SQL_TXN_ISOLATION_OPTION volta SQL_TXN_READ_COMMITTED.  
  
## <a name="u-z"></a>U-Z  
 SQL_UNION retorna SQL_U_UNION ou SQL_U_UNION_ALL.  
  
 SQL_USER_NAME \<retorna em branco>.
