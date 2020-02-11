---
title: Função SQLGetInfo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetInfo
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetInfo
helpviewer_keywords:
- SQLGetInfo function [ODBC]
ms.assetid: 49dceccc-d816-4ada-808c-4c6138dccb64
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b0e62e7aaba276643a2874a22e74a08214cfe51e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68030664"
---
# <a name="sqlgetinfo-function"></a>Função SQLGetInfo
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: ISO 92  
  
 **Resumo**  
 **SQLGetInfo** retorna informações gerais sobre o driver e a fonte de dados associada a uma conexão.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLGetInfo(  
     SQLHDBC         ConnectionHandle,  
     SQLUSMALLINT    InfoType,  
     SQLPOINTER      InfoValuePtr,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *ConnectionHandle*  
 [Entrada] Identificador de conexão.  
  
 *InfoType*  
 Entrada Tipo de informação.  
  
 *InfoValuePtr*  
 Der Ponteiro para um buffer no qual as informações são retornadas. Dependendo do *InfoType* solicitado, as informações retornadas serão uma das seguintes: uma cadeia de caracteres terminada em nulo, um valor SQLUSMALLINT, um BITMASK SQLUINTEGER, um sinalizador SQLUINTEGER, um valor binário SQLUINTEGER ou um valor SQLULEN.  
  
 Se o argumento *InfoType* for SQL_DRIVER_HDESC ou SQL_DRIVER_HSTMT, o argumento *InfoValuePtr* será de entrada e saída. (Consulte os descritores de SQL_DRIVER_HDESC ou SQL_DRIVER_HSTMT mais tarde nesta descrição da função para obter mais informações.)  
  
 Se *InfoValuePtr* for NULL, *StringLengthPtr* ainda retornará o número total de bytes (excluindo o caractere de terminação nula para dados de caracteres) disponíveis para retornar no buffer apontado por *InfoValuePtr*.  
  
 *BufferLength*  
 Entrada Comprimento do \*buffer *InfoValuePtr* . Se o valor em * \*InfoValuePtr* não for uma cadeia de caracteres ou se *InfoValuePtr* for um ponteiro nulo, o argumento *BufferLength* será ignorado. O driver pressupõe que o tamanho de * \*InfoValuePtr* seja SQLUSMALLINT ou SQLUINTEGER, com base no *InfoType*. Se * \*InfoValuePtr* for uma cadeia de caracteres Unicode (ao chamar **SQLGetInfoW**), o argumento *BufferLength* deverá ser um número par; caso contrário, SQLSTATE HY090 (cadeia de caracteres ou comprimento de buffer inválido) será retornado.  
  
 *StringLengthPtr*  
 Der Ponteiro para um buffer no qual retornar o número total de bytes (excluindo o caractere de terminação nula para dados de caractere) disponível para retornar em **InfoValuePtr*.  
  
 Para dados de caractere, se o número de bytes disponíveis para retornar for maior ou igual a *BufferLength*, as informações em \* *InfoValuePtr* serão truncadas para *BufferLength* bytes menos o comprimento de um caractere de terminação nula e serão terminadas em nulo pelo driver.  
  
 Para todos os outros tipos de dados, o valor de *BufferLength* é ignorado e o driver assume que o \*tamanho de *InfoValuePtr* é SQLUSMALLINT ou SQLUINTEGER, dependendo do *InfoType*.  
  
## <a name="return-value"></a>Valor retornado  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLGetInfo** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_DBC e um *identificador* de *ConnectionHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLGetInfo** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|DESCRIÇÃO|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres, truncados à direita|O buffer \* *InfoValuePtr* não era grande o suficiente para retornar todas as informações solicitadas. Portanto, as informações foram truncadas. O comprimento das informações solicitadas em seu formulário não truncado é retornado em **StringLengthPtr*. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|08003|Conexão não aberta|(DM) o tipo de informações solicitadas no *InfoType* requer uma conexão aberta. Dos tipos de informações reservados pelo ODBC, somente SQL_ODBC_VER podem ser retornados sem uma conexão aberta.|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado falhou antes da função concluir o processamento.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \*MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY010|Erro de sequência de função|(DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para *StatementHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY024|Valor de atributo inválido|(DM) o argumento *InfoType* foi SQL_DRIVER_HSTMT e o valor apontado por *InfoValuePtr* não era um identificador de instrução válido.<br /><br /> (DM) o argumento *InfoType* foi SQL_DRIVER_HDESC e o valor apontado por *InfoValuePtr* não era um identificador de descritor válido.|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|(DM) o valor especificado para o argumento *BufferLength* era menor que 0.<br /><br /> (DM) o valor especificado para *BufferLength* era um número ímpar e * \*InfoValuePtr* era de um tipo de dados Unicode.|  
|HY096|Tipo de informação fora do intervalo|O valor especificado para o argumento *InfoType* não era válido para a versão do ODBC com suporte do driver.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Campo opcional não implementado|O valor especificado para o argumento *InfoType* era um valor específico de driver que não é suportado pelo driver.|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver que corresponde ao *ConnectionHandle* não oferece suporte à função.|  
  
## <a name="comments"></a>Comentários  
 Os tipos de informações atualmente definidos são mostrados em "tipos de informações", mais adiante nesta seção; Espera-se que mais seja definido para tirar proveito de diferentes fontes de dados. Um intervalo de tipos de informações é reservado pelo ODBC; os desenvolvedores de driver devem reservar valores para seu próprio uso específico de driver de um grupo aberto. O **SQLGetInfo** não *executa conversão Unicode nem* conversões (consulte [o apêndice A: códigos de erro ODBC](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md) da *referência do programador de ODBC*) para *InfoTypes*definidas por driver. Para obter mais informações, consulte [tipos de dados específicos do driver, tipos de descritores, tipos de informações, tipos de diagnóstico e atributos](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md). O formato das informações retornadas em \* *InfoValuePtr* depende do *InfoType* solicitado. **SQLGetInfo** retornará informações em um dos cinco formatos diferentes:  
  
-   Uma cadeia de caracteres terminada em nulo  
  
-   Um valor de SQLUSMALLINT  
  
-   Um bitmask SQLUINTEGER  
  
-   Um valor SQLUINTEGER  
  
-   Um valor binário SQLUINTEGER  
  
 O formato de cada um dos tipos de informações a seguir é observado na descrição do tipo. O aplicativo deve converter o valor retornado em **InfoValuePtr* de acordo. Para obter um exemplo de como um aplicativo pode recuperar dados de um bitmask SQLUINTEGER, consulte o "exemplo de código".  
  
 Um driver deve retornar um valor para cada tipo de informação definido nas tabelas a seguir. Se um tipo de informação não se aplicar ao driver ou à fonte de dados, o driver retornará um dos valores listados na tabela a seguir.  
  
 Cadeia de caracteres ("Y" ou "N")  
 "N"  
  
 Cadeia de caracteres (não "Y" ou "N")  
 Cadeia de caracteres vazia  
  
 SQLUSMALLINT  
 0  
  
 Valor binário de bitmask SQLUINTEGER ou SQLUINTEGER  
 0L  
  
 Por exemplo, se uma fonte de dados não oferecer suporte a procedimentos, **SQLGetInfo** retornará os valores listados na tabela a seguir para os valores de *InfoType* relacionados aos procedimentos.  
  
 SQL_PROCEDURES  
 "N"  
  
 SQL_ACCESSIBLE_PROCEDURES  
 "N"  
  
 SQL_MAX_PROCEDURE_NAME_LEN  
 0  
  
 SQL_PROCEDURE_TERM  
 Cadeia de caracteres vazia  
  
 **SQLGetInfo** retorna SQLSTATE HY096 (valor de argumento inválido) para os valores de *InfoType* que estão no intervalo de tipos de informações reservado para uso pelo ODBC, mas não são definidos pela versão do ODBC com suporte do driver. Para determinar a qual versão do ODBC um driver está em conformidade, um aplicativo chama **SQLGetInfo** com o tipo de informação SQL_DRIVER_ODBC_VER. **SQLGetInfo** retorna SQLSTATE HYC00 (recurso opcional não implementado) para valores de *InfoType* que estão no intervalo de tipos de informações reservados para uso específico de driver, mas que não são suportados pelo driver.  
  
 Todas as chamadas para **SQLGetInfo** exigem uma conexão aberta, exceto quando o *infotype* é SQL_ODBC_VER, que retorna a versão do Gerenciador de driver.  
  
## <a name="information-types"></a>Tipos de informações  
 Esta seção lista os tipos de informações com suporte do **SQLGetInfo**. Os tipos de informações são agrupados de forma categórica e listados em ordem alfabética. Os tipos de informações que foram adicionados ou renomeados para ODBC 3 *. x* também são listados.  
  
## <a name="driver-information"></a>Informações do driver  
 Os valores a seguir do argumento *InfoType* retornam informações sobre o driver ODBC, como o número de instruções ativas, o nome da fonte de dados e o nível de conformidade dos padrões de interface:  
  
|||  
|-|-|  
|SQL_ACTIVE_ENVIRONMENTS|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
|SQL_ASYNC_DBC_FUNCTIONS|SQL_FILE_USAGE|  
|SQL_ASYNC_MODE|SQL_GETDATA_EXTENSIONS|  
|SQL_ASYNC_NOTIFICATION|SQL_INFO_SCHEMA_VIEWS|  
|SQL_BATCH_ROW_COUNT|SQL_KEYSET_CURSOR_ATTRIBUTES1|  
|SQL_BATCH_SUPPORT|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
|SQL_DATA_SOURCE_NAME|SQL_MAX_ASYNC_CONCURRENT_STATEMENTS|  
|SQL_DRIVER_AWARE_POOLING_SUPPORTED|SQL_MAX_CONCURRENT_ACTIVITIES|  
|SQL_DRIVER_HDBC|SQL_MAX_DRIVER_CONNECTIONS|  
|SQL_DRIVER_HDESC|SQL_ODBC_INTERFACE_CONFORMANCE|  
|SQL_DRIVER_HENV|SQL_ODBC_STANDARD_CLI_CONFORMANCE|  
|SQL_DRIVER_HLIB|SQL_ODBC_VER|  
|SQL_DRIVER_HSTMT|SQL_PARAM_ARRAY_ROW_COUNTS|  
|SQL_DRIVER_NAME|SQL_PARAM_ARRAY_SELECTS|  
|SQL_DRIVER_ODBC_VER|SQL_ROW_UPDATES|  
|SQL_DRIVER_VER|SQL_SEARCH_PATTERN_ESCAPE|  
|SQL_DYNAMIC_CURSOR_ATTRIBUTES1|SQL_SERVER_NAME|  
|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|SQL_STATIC_CURSOR_ATTRIBUTES1|  
|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1|SQL_STATIC_CURSOR_ATTRIBUTES2|  
  
> [!NOTE]  
>  Ao implementar o **SQLGetInfo**, um driver pode melhorar o desempenho, minimizando o número de vezes que as informações são enviadas ou solicitadas do servidor.  
  
## <a name="dbms-product-information"></a>Informações do produto DBMS  
 Os valores a seguir do argumento *InfoType* retornam informações sobre o produto DBMS, como o nome do DBMS e a versão:  
  
 SQL_DATABASE_NAMESQL_DBMS_NAMESQL_DBMS_VER  
  
## <a name="data-source-information"></a>Informações da fonte de dados  
 Os valores a seguir do argumento *InfoType* retornam informações sobre a fonte de dados, como características do cursor e recursos de transação:  
  
|||  
|-|-|  
|SQL_ACCESSIBLE_PROCEDURES|SQL_MULT_RESULT_SETS|  
|SQL_ACCESSIBLE_TABLES|SQL_MULTIPLE_ACTIVE_TXN|  
|SQL_BOOKMARK_PERSISTENCE|SQL_NEED_LONG_DATA_LEN|  
|SQL_CATALOG_TERM|SQL_NULL_COLLATION|  
|SQL_COLLATION_SEQ|SQL_PROCEDURE_TERM|  
|SQL_CONCAT_NULL_BEHAVIOR|SQL_SCHEMA_TERM|  
|SQL_CURSOR_COMMIT_BEHAVIOR|SQL_SCROLL_OPTIONS|  
|SQL_CURSOR_ROLLBACK_BEHAVIOR|SQL_TABLE_TERM|  
|SQL_CURSOR_SENSITIVITY|SQL_TXN_CAPABLE|  
|SQL_DATA_SOURCE_READ_ONLY|SQL_TXN_ISOLATION_OPTION|  
|SQL_DEFAULT_TXN_ISOLATION|SQL_USER_NAME|  
|SQL_DESCRIBE_PARAMETER||  
  
## <a name="supported-sql"></a>SQL com suporte  
 Os valores a seguir do argumento *InfoType* retornam informações sobre as instruções SQL com suporte na fonte de dados. A sintaxe SQL de cada recurso descrito por esses tipos de informações é a sintaxe SQL-92. Esses tipos de informações não descrevem exaustivamente toda a gramática do SQL-92. Em vez disso, eles descrevem essas partes da gramática para as quais as fontes de dados normalmente oferecem níveis diferentes de suporte. Especificamente, a maioria das instruções DDL no SQL-92 são cobertas.  
  
 Os aplicativos devem determinar o nível geral de gramática com suporte do tipo de informações SQL_SQL_CONFORMANCE e usar os outros tipos de informações para determinar variações do nível de conformidade de padrões declarados.  
  
|||  
|-|-|  
|SQL_AGGREGATE_FUNCTIONS|SQL_DROP_TABLE|  
|SQL_ALTER_DOMAIN|SQL_DROP_TRANSLATION|  
|SQL_ALTER_SCHEMA|SQL_DROP_VIEW|  
|SQL_ALTER_TABLE|SQL_EXPRESSIONS_IN_ORDERBY|  
|SQL_ANSI_SQL_DATETIME_LITERALS|SQL_GROUP_BY|  
|SQL_CATALOG_LOCATION|SQL_IDENTIFIER_CASE|  
|SQL_CATALOG_NAME|SQL_IDENTIFIER_QUOTE_CHAR|  
|SQL_CATALOG_NAME_SEPARATOR|SQL_INDEX_KEYWORDS|  
|SQL_CATALOG_USAGE|SQL_INSERT_STATEMENT|  
|SQL_COLUMN_ALIAS|SQL_INTEGRITY|  
|SQL_CORRELATION_NAME|SQL_KEYWORDS|  
|SQL_CREATE_ASSERTION|SQL_LIKE_ESCAPE_CLAUSE|  
|SQL_CREATE_CHARACTER_SET|SQL_NON_NULLABLE_COLUMNS|  
|SQL_CREATE_COLLATION|SQL_SQL_CONFORMANCE|  
|SQL_CREATE_DOMAIN|SQL_OJ_CAPABILITIES|  
|SQL_CREATE_SCHEMA|SQL_ORDER_BY_COLUMNS_IN_SELECT|  
|SQL_CREATE_TABLE|SQL_OUTER_JOINS|  
|SQL_CREATE_TRANSLATION|SQL_PROCEDURES|  
|SQL_DDL_INDEX|SQL_QUOTED_IDENTIFIER_CASE|  
|SQL_DROP_ASSERTION|SQL_SCHEMA_USAGE|  
|SQL_DROP_CHARACTER_SET|SQL_SPECIAL_CHARACTERS|  
|SQL_DROP_COLLATION|SQL_SUBQUERIES|  
|SQL_DROP_DOMAIN|SQL_UNION|  
|SQL_DROP_SCHEMA||  
  
## <a name="sql-limits"></a>Limites do SQL  
 Os valores a seguir do argumento *InfoType* retornam informações sobre os limites aplicados a identificadores e cláusulas em instruções SQL, como o comprimento máximo de identificadores e o número máximo de colunas em uma lista de seleção. As limitações podem ser impostas pelo driver ou pela fonte de dados.  
  
|||  
|-|-|  
|SQL_MAX_BINARY_LITERAL_LEN|SQL_MAX_IDENTIFIER_LEN|  
|SQL_MAX_CATALOG_NAME_LEN|SQL_MAX_INDEX_SIZE|  
|SQL_MAX_CHAR_LITERAL_LEN|SQL_MAX_PROCEDURE_NAME_LEN|  
|SQL_MAX_COLUMN_NAME_LEN|SQL_MAX_ROW_SIZE|  
|SQL_MAX_COLUMNS_IN_GROUP_BY|SQL_MAX_ROW_SIZE_INCLUDES_LONG|  
|SQL_MAX_COLUMNS_IN_INDEX|SQL_MAX_SCHEMA_NAME_LEN|  
|SQL_MAX_COLUMNS_IN_ORDER_BY|SQL_MAX_STATEMENT_LEN|  
|SQL_MAX_COLUMNS_IN_SELECT|SQL_MAX_TABLE_NAME_LEN|  
|SQL_MAX_COLUMNS_IN_TABLE|SQL_MAX_TABLES_IN_SELECT|  
|SQL_MAX_CURSOR_NAME_LEN|SQL_MAX_USER_NAME_LEN|  
  
## <a name="scalar-function-information"></a>Informações de função escalar  
 Os valores a seguir do argumento *InfoType* retornam informações sobre as funções escalares com suporte da fonte de dados e do driver. Para obter mais informações sobre funções escalares, consulte o [Apêndice E: funções escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).  
  
|||  
|-|-|  
|SQL_CONVERT_FUNCTIONS|SQL_TIMEDATE_ADD_INTERVALS|  
|SQL_NUMERIC_FUNCTIONS|SQL_TIMEDATE_DIFF_INTERVALS|  
|SQL_STRING_FUNCTIONS|SQL_TIMEDATE_FUNCTIONS|  
|SQL_SYSTEM_FUNCTIONS||  
  
## <a name="conversion-information"></a>Informações de conversão  
 Os valores a seguir do argumento *InfoType* retornam uma lista dos tipos de dados SQL para os quais a fonte de dados pode converter o tipo de dados SQL especificado com a função **Convert** escalar:  
  
|||  
|-|-|  
|SQL_CONVERT_BIGINT|SQL_CONVERT_LONGVARBINARY|  
|SQL_CONVERT_BINARY|SQL_CONVERT_LONGVARCHAR|  
|SQL_CONVERT_BIT|SQL_CONVERT_NUMERIC|  
|SQL_CONVERT_CHAR|SQL_CONVERT_REAL|  
|SQL_CONVERT_DATE|SQL_CONVERT_SMALLINT|  
|SQL_CONVERT_DECIMAL|SQL_CONVERT_TIME|  
|SQL_CONVERT_DOUBLE|SQL_CONVERT_TIMESTAMP|  
|SQL_CONVERT_FLOAT|SQL_CONVERT_TINYINT|  
|SQL_CONVERT_INTEGER|SQL_CONVERT_VARBINARY|  
|SQL_CONVERT_INTERVAL_YEAR_MONTH|SQL_CONVERT_VARCHAR|  
|SQL_CONVERT_INTERVAL_DAY_TIME||  
  
## <a name="information-types-added-for-odbc-3x"></a>Tipos de informações adicionados para ODBC 3. x  
 Os seguintes valores do argumento *InfoType* foram adicionados para ODBC 3 *. x*:  
  
|||  
|-|-|  
|SQL_ACTIVE_ENVIRONMENTS|SQL_DRIVER_AWARE_POOLING_SUPPORTED|  
|SQL_AGGREGATE_FUNCTIONS|SQL_DRIVER_HDESC|  
|SQL_ALTER_DOMAIN|SQL_DROP_ASSERTION|  
|SQL_ALTER_SCHEMA|SQL_DROP_CHARACTER_SET|  
|SQL_ANSI_SQL_DATETIME_LITERALS|SQL_DROP_COLLATION|  
|SQL_ASYNC_DBC_FUNCTIONS|SQL_DROP_DOMAIN|  
|SQL_ASYNC_MODE|SQL_DROP_SCHEMA|  
|SQL_ASYNC_NOTIFICATION|SQL_DROP_TABLE|  
|SQL_BATCH_ROW_COUNT|SQL_DROP_TRANSLATION|  
|SQL_BATCH_SUPPORT|SQL_DROP_VIEW|  
|SQL_CATALOG_NAME|SQL_DYNAMIC_CURSOR_ATTRIBUTES1|  
|SQL_COLLATION_SEQ|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|  
|SQL_CONVERT_INTERVAL_YEAR_MONTH|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1|  
|SQL_CONVERT_INTERVAL_DAY_TIME|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
|SQL_CREATE_ASSERTION|SQL_INFO_SCHEMA_VIEWS|  
|SQL_CREATE_CHARACTER_SET|SQL_INSERT_STATEMENT|  
|SQL_CREATE_COLLATION|SQL_KEYSET_CURSOR_ATTRIBUTES1|  
|SQL_CREATE_DOMAIN|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
|SQL_CREATE_SCHEMA|SQL_MAX_ASYNC_CONCURRENT_STATEMENTS|  
|SQL_CREATE_TABLE|SQL_MAX_IDENTIFIER_LEN|  
|SQL_CREATE_TRANSLATION|SQL_PARAM_ARRAY_ROW_COUNTS|  
|SQL_CURSOR_SENSITIVITY|SQL_PARAM_ARRAY_SELECTS|  
|SQL_DDL_INDEX|SQL_STATIC_CURSOR_ATTRIBUTES1|  
|SQL_DESCRIBE_PARAMETER|SQL_STATIC_CURSOR_ATTRIBUTES2|  
|SQL_DM_VER|SQL_XOPEN_CLI_YEAR|  
  
## <a name="information-types-renamed-for-odbc-3x"></a>Tipos de informações renomeados para ODBC 3. x  
 Os valores a seguir do argumento *InfoType* foram renomeados para ODBC 3 *. x*.  
  
 SQL_ACTIVE_CONNECTIONS  
 SQL_MAX_DRIVER_CONNECTIONS  
  
 SQL_ACTIVE_STATEMENTS  
 SQL_MAX_CONCURRENT_ACTIVITIES  
  
 SQL_MAX_OWNER_NAME_LEN  
 SQL_MAX_SCHEMA_NAME_LEN  
  
 SQL_MAX_QUALIFIER_NAME_LEN  
 SQL_MAX_CATALOG_NAME_LEN  
  
 SQL_ODBC_SQL_OPT_IEF  
 SQL_INTEGRITY  
  
 SQL_OWNER_TERM  
 SQL_SCHEMA_TERM  
  
 SQL_OWNER_USAGE  
 SQL_SCHEMA_USAGE  
  
 SQL_QUALIFIER_LOCATION  
 SQL_CATALOG_LOCATION  
  
 SQL_QUALIFIER_NAME_SEPARATOR  
 SQL_CATALOG_NAME_SEPARATOR  
  
 SQL_QUALIFIER_TERM  
 SQL_CATALOG_TERM  
  
 SQL_QUALIFIER_USAGE  
 SQL_CATALOG_USAGE  
  
## <a name="information-types-deprecated-in-odbc-3x"></a>Tipos de informações preteridos no ODBC 3. x  
 Os valores a seguir do argumento *InfoType* foram preteridos no ODBC 3 *. x*. Os drivers ODBC 3 *. x* devem continuar a dar suporte a esses tipos de informações para compatibilidade com versões anteriores com aplicativos ODBC 2 *. x* . (Para obter mais informações sobre esses tipos, consulte [suporte SQLGetInfo](../../../odbc/reference/appendixes/sqlgetinfo-support.md) no apêndice G: diretrizes de driver para compatibilidade com versões anteriores.)  
  
|||  
|-|-|  
|SQL_FETCH_DIRECTION|SQL_POS_OPERATIONS|  
|SQL_LOCK_TYPES|SQL_POSITIONED_STATEMENTS|  
|SQL_ODBC_API_CONFORMANCE|SQL_SCROLL_CONCURRENCY|  
|SQL_ODBC_SQL_CONFORMANCE|SQL_STATIC_SENSITIVITY|  
  
## <a name="information-type-descriptions"></a>Descrições de tipos de informações  
 A tabela a seguir lista alfabeticamente cada tipo de informação, a versão do ODBC na qual ele foi introduzido e sua descrição.  
  
 SQL_ACCESSIBLE_PROCEDURES (ODBC 1,0)  
 Uma cadeia de caracteres: "Y" se o usuário puder executar todos os procedimentos retornados por **SQLProcedures**; "N" se pode haver procedimentos retornados que o usuário não pode executar.  
  
 SQL_ACCESSIBLE_TABLES (ODBC 1,0)  
 Uma cadeia de caracteres: "Y" se o usuário for garantido, **selecione** privilégios para todas as tabelas retornadas por **SQLTables**; "N" se pode haver tabelas retornadas que o usuário não pode acessar.  
  
 SQL_ACTIVE_ENVIRONMENTS (ODBC 3,0)  
 Um valor de SQLUSMALLINT que especifica o número máximo de ambientes ativos aos quais o driver pode dar suporte. Se não houver um limite especificado ou o limite for desconhecido, esse valor será definido como zero.  
  
 SQL_AGGREGATE_FUNCTIONS (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera o suporte para funções de agregação:  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 Um driver de nível de entrada do SQL-92 sempre retornará todas essas opções como com suporte.  
  
 SQL_ALTER_DOMAIN (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera as cláusulas na instrução **ALTER Domain** , conforme definido em SQL-92, com suporte da fonte de dados. Um driver em conformidade com nível completo do SQL-92 sempre retornará todas as bitmasks. Um valor de retorno de "0" significa que não há suporte para a instrução **ALTER Domain** .  
  
 O nível de conformidade do SQL-92 ou FIPS no qual esse recurso deve ser suportado é mostrado entre parênteses ao lado de cada bitmask.  
  
 As seguintes bitmasks são usadas para determinar quais cláusulas têm suporte:  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT = há suporte para a adição de uma restrição de domínio (nível completo)  
  
 SQL_AD_ADD_DOMAIN_DEFAULT = \<alter Domain> \<definir a cláusula default do domínio> tem suporte (nível completo)  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION = \<cláusula de definição de nome de restrição> tem suporte para a restrição de domínio de nomenclatura (nível intermediário)  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT = \<há suporte para a cláusula DROP DOMAIN Constraint> (nível completo)  
  
 SQL_AD_DROP_DOMAIN_DEFAULT = \<alter Domain> \<a cláusula default do domínio de remoção> tem suporte (nível completo)  
  
 Os bits a seguir especificam \<os atributos de restrição \<com suporte> se adicionar restrição de domínio> tiver suporte (o bit de SQL_AD_ADD_DOMAIN_CONSTRAINT estiver definido):  
  
 SQL_AD_ADD_CONSTRAINT_DEFERRABLE (nível completo) SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE (nível completo) SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE (nível completo)  
  
 SQL_ALTER_TABLE (ODBC 2,0)  
 Um bitmask SQLUINTEGER que enumera as cláusulas na instrução **ALTER TABLE** com suporte da fonte de dados.  
  
 O nível de conformidade do SQL-92 ou FIPS no qual esse recurso deve ser suportado é mostrado entre parênteses ao lado de cada bitmask.  
  
 As seguintes bitmasks são usadas para determinar quais cláusulas têm suporte:  
  
 SQL_AT_ADD_COLUMN_COLLATION = \<há suporte para a cláusula ADD Column>, com instalações para especificar o agrupamento de colunas (nível completo) (ODBC 3,0)  
  
 SQL_AT_ADD_COLUMN_DEFAULT = \<há suporte para a cláusula adicionar coluna>, com instalações para especificar padrões de coluna (nível de transição FIPS) (ODBC 3,0)  
  
 SQL_AT_ADD_COLUMN_SINGLE = \<há suporte para a adição de coluna> (nível de transição FIPS) (ODBC 3,0)  
  
 SQL_AT_ADD_CONSTRAINT = \<há suporte para a cláusula ADD Column>, com instalações para especificar restrições de coluna (nível de transição FIPS) (ODBC 3,0)  
  
 SQL_AT_ADD_TABLE_CONSTRAINT = \<há suporte para a cláusula adicionar restrição de tabela> (nível de transição FIPS) (ODBC 3,0)  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION = \<definição de nome de restrição> tem suporte para a nomenclatura de restrições de coluna e tabela (nível intermediário) (ODBC 3,0)  
  
 SQL_AT_DROP_COLUMN_CASCADE = \<DROP COLUMN> Cascade tem suporte (nível de transição FIPS) (ODBC 3,0)  
  
 SQL_AT_DROP_COLUMN_DEFAULT = \<alter Column> \<cláusula de descartar coluna padrão> tem suporte (nível intermediário) (ODBC 3,0)  
  
 SQL_AT_DROP_COLUMN_RESTRICT = \<a coluna drop> restrict é suportada (nível de transição FIPS) (ODBC 3,0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3,0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT = \<a coluna drop> restrict é suportada (nível de transição FIPS) (ODBC 3,0)  
  
 SQL_AT_SET_COLUMN_DEFAULT = \<alter Column> \<definir a cláusula default da coluna> tem suporte (nível intermediário) (ODBC 3,0)  
  
 Os bits a seguir especificam \<os atributos de restrição de suporte> se a especificação de restrições de coluna ou tabela for suportada (o bit de SQL_AT_ADD_CONSTRAINT está definido):  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED (nível completo) (ODBC 3.0) SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE (nível completo) (ODBC 3.0) SQL_AT_CONSTRAINT_DEFERRABLE (nível completo) (ODBC 3.0) SQL_AT_CONSTRAINT_NON_DEFERRABLE (nível completo) (ODBC 3,0)  
  
 SQL_ASYNC_DBC_FUNCTIONS (ODBC 3,8)  
 Um valor SQLUINTEGER que indica se o driver pode executar funções de forma assíncrona no identificador de conexão.  
  
 SQL_ASYNC_DBC_CAPABLE = o driver pode executar funções de conexão de forma assíncrona.  
  
 SQL_ASYNC_DBC_NOT_CAPABLE = o driver não pode executar funções de conexão de forma assíncrona.  
  
 SQL_ASYNC_MODE (ODBC 3,0)  
 Um valor SQLUINTEGER que indica o nível de suporte assíncrono no driver:  
  
 SQL_AM_CONNECTION = há suporte para a execução assíncrona no nível de conexão. Qualquer um dos identificadores de instrução associados a um determinado identificador de conexão está no modo assíncrono ou todos estão no modo síncrono. Um identificador de instrução em uma conexão não pode estar no modo assíncrono, enquanto outro identificador de instrução na mesma conexão está no modo síncrono e vice-versa.  
  
 SQL_AM_STATEMENT = há suporte para a execução assíncrona em nível de instrução. Alguns identificadores de instrução associados a um identificador de conexão podem estar no modo assíncrono, enquanto outros identificadores de instrução na mesma conexão estão no modo síncrono.  
  
 Não há suporte para SQL_AM_NONE = modo assíncrono.  
  
 SQL_ASYNC_NOTIFICATION  
 Um valor SQLUINTEGER que indica se o driver dá suporte à notificação assíncrona:  
  
-   **SQL_ASYNC_NOTIFICATION_CAPABLE** O driver dá suporte à notificação de execução assíncrona.  
  
-   **SQL_ASYNC_NOTIFICATION_NOT_CAPABLE** O driver não dá suporte à notificação de execução assíncrona.  
  
 Há duas categorias de operações assíncronas ODBC: operações assíncronas de nível de conexão e operações assíncronas em nível de instrução.  Se um driver retornar SQL_ASYNC_NOTIFICATION_CAPABLE, ele deverá dar suporte à notificação para todas as APIs que ele possa executar de forma assíncrona.  
  
 SQL_BATCH_ROW_COUNT (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera o comportamento do driver em relação à disponibilidade de contagens de linhas. As seguintes bitmasks são usadas junto com o tipo de informação:  
  
 SQL_BRC_ROLLED_UP = contagens de linha para instruções de inserção, exclusão ou atualização consecutivas são acumuladas em uma. Se esse bit não estiver definido, as contagens de linhas estarão disponíveis para cada instrução.  
  
 SQL_BRC_PROCEDURES = contagens de linhas, se houver, estarão disponíveis quando um lote for executado em um procedimento armazenado. Se as contagens de linhas estiverem disponíveis, elas poderão ser acumuladas ou individualmente disponíveis, dependendo do SQL_BRC_ROLLED_UP bit.  
  
 SQL_BRC_EXPLICIT = contagens de linhas, se houver, estarão disponíveis quando um lote for executado diretamente chamando **SQLExecute** ou **SQLExecDirect**. Se as contagens de linhas estiverem disponíveis, elas poderão ser acumuladas ou individualmente disponíveis, dependendo do SQL_BRC_ROLLED_UP bit.  
  
 SQL_BATCH_SUPPORT (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera o suporte do driver para lotes. As seguintes bitmasks são usadas para determinar qual nível tem suporte:  
  
 SQL_BS_SELECT_EXPLICIT = o driver dá suporte a lotes explícitos que podem ter instruções de geração de conjunto de resultados.  
  
 SQL_BS_ROW_COUNT_EXPLICIT = o driver dá suporte a lotes explícitos que podem ter instruções de geração de contagem de linhas.  
  
 SQL_BS_SELECT_PROC = o driver dá suporte a procedimentos explícitos que podem ter instruções de geração de conjunto de resultados.  
  
 SQL_BS_ROW_COUNT_PROC = o driver dá suporte a procedimentos explícitos que podem ter instruções de geração de contagem de linhas.  
  
 SQL_BOOKMARK_PERSISTENCE (ODBC 2,0)  
 Um bitmask SQLUINTEGER que enumera as operações por meio das quais os indicadores persistem.  
  
 As seguintes bitmasks são usadas junto com o sinalizador para determinar por quais indicadores de opções persistem:  
  
 SQL_BP_CLOSE = os indicadores são válidos depois que um aplicativo chama **SQLFreeStmt** com a opção SQL_CLOSE ou **SQLCloseCursor** para fechar o cursor associado a uma instrução.  
  
 SQL_BP_DELETE = o indicador de uma linha é válido depois que essa linha foi excluída.  
  
 SQL_BP_DROP = os indicadores são válidos depois que um aplicativo chama **SQLFreeHandle** com um *identificadortype* de SQL_HANDLE_STMT para descartar uma instrução.  
  
 SQL_BP_TRANSACTION = os indicadores são válidos após um aplicativo confirmar ou reverter uma transação.  
  
 SQL_BP_UPDATE = o indicador de uma linha é válido depois que qualquer coluna nessa linha tiver sido atualizada, incluindo as colunas de chave.  
  
 SQL_BP_OTHER_HSTMT = um indicador associado a uma instrução pode ser usado com outra instrução. A menos que SQL_BP_CLOSE ou SQL_BP_DROP seja especificado, o cursor na primeira instrução deve ser aberto.  
  
 SQL_CATALOG_LOCATION (ODBC 2,0)  
 Um valor de SQLUSMALLINT que indica a posição do catálogo em um nome de tabela qualificado:  
  
 SQL_CL_STARTSQL_CL_END  
  
 Por exemplo, um driver Xbase retorna SQL_CL_START porque o nome do diretório (catálogo) está no início do nome da tabela, como em \EMPDATA\EMP. DBF. Um driver de servidor ORACLE retorna SQL_CL_END porque o catálogo está no final do nome da tabela, como em ADMIN.EMP@EMPDATA.  
  
 Um driver compatível com nível completo do SQL-92 sempre retornará SQL_CL_START. Um valor de 0 será retornado se os catálogos não forem suportados pela fonte de dados. Para determinar se há suporte para os catálogos, um aplicativo chama **SQLGetInfo** com o tipo de informação SQL_CATALOG_NAME.  
  
 Este *InfoType* foi renomeado para ODBC 3,0 do ODBC 2,0 *InfoType* SQL_QUALIFIER_LOCATION.  
  
 SQL_CATALOG_NAME (ODBC 3,0)  
 Uma cadeia de caracteres: "Y" se o servidor der suporte a nomes de catálogo ou "N" se não tiver.  
  
 Um driver compatível com nível completo do SQL-92 sempre retornará "Y".  
  
 SQL_CATALOG_NAME_SEPARATOR (ODBC 1,0)  
 Uma cadeia de caracteres: o caractere ou os caracteres que a fonte de dados define como o separador entre um nome de catálogo e o elemento de nome qualificado que segue ou precede.  
  
 Uma cadeia de caracteres vazia será retornada se os catálogos não forem suportados pela fonte de dados. Para determinar se há suporte para os catálogos, um aplicativo chama **SQLGetInfo** com o tipo de informação SQL_CATALOG_NAME. Um driver compatível com nível completo do SQL-92 sempre retornará ".".  
  
 Este *InfoType* foi renomeado para ODBC 3,0 do ODBC 2,0 *InfoType* SQL_QUALIFIER_NAME_SEPARATOR.  
  
 SQL_CATALOG_TERM (ODBC 1,0)  
 Uma cadeia de caracteres com o nome do fornecedor de fonte de dados para um catálogo; por exemplo, "banco de dados" ou "diretório". Essa cadeia de caracteres pode estar no caso superior, inferior ou misto.  
  
 Uma cadeia de caracteres vazia será retornada se os catálogos não forem suportados pela fonte de dados. Para determinar se há suporte para os catálogos, um aplicativo chama **SQLGetInfo** com o tipo de informação SQL_CATALOG_NAME. Um driver compatível com nível completo do SQL-92 sempre retornará "catálogo".  
  
 Este *InfoType* foi renomeado para ODBC 3,0 do ODBC 2,0 *InfoType* SQL_QUALIFIER_TERM.  
  
 SQL_CATALOG_USAGE (ODBC 2,0)  
 Um bitmask SQLUINTEGER que enumera as instruções em que os catálogos podem ser usados.  
  
 As seguintes bitmasks são usadas para determinar onde os catálogos podem ser usados:  
  
 SQL_CU_DML_STATEMENTS = os catálogos têm suporte em todas as instruções de linguagem de manipulação de dados: **selecionar**, **Inserir**, **Atualizar**, **excluir**e, se houver suporte, **Selecione para atualizar** e posicionar as instruções UPDATE e Delete.  
  
 SQL_CU_PROCEDURE_INVOCATION = os catálogos têm suporte na instrução de invocação de procedimento ODBC.  
  
 SQL_CU_TABLE_DEFINITION = os catálogos têm suporte em todas as instruções de definição de tabela: **CREATE TABLE**, **criar exibição**, **alterar tabela**, **remover tabela**e **descartar exibição**.  
  
 SQL_CU_INDEX_DEFINITION = há suporte para catálogos em todas as instruções de definição de índice: **CREATE INDEX** e **drop index**.  
  
 SQL_CU_PRIVILEGE_DEFINITION = os catálogos têm suporte em todas as instruções de definição de privilégio: **Grant** e **REVOKE**.  
  
 Um valor de 0 será retornado se os catálogos não forem suportados pela fonte de dados. Para determinar se há suporte para os catálogos, um aplicativo chama **SQLGetInfo** com o tipo de informação SQL_CATALOG_NAME. Um driver compatível com nível completo do SQL-92 sempre retornará um bitmask com todos esses bits definidos.  
  
 Este *InfoType* foi renomeado para ODBC 3,0 do ODBC 2,0 *InfoType* SQL_QUALIFIER_USAGE.  
  
 SQL_COLLATION_SEQ (ODBC 3,0)  
 O nome da sequência de agrupamento. Essa é uma cadeia de caracteres que indica o nome do agrupamento padrão para o conjunto de caracteres padrão para esse servidor (por exemplo, ' ISO 8859-1 ' ou EBCDIC). Se isso for desconhecido, uma cadeia de caracteres vazia será retornada. Um driver compatível com nível completo do SQL-92 sempre retornará uma cadeia de caracteres não vazia.  
  
 SQL_COLUMN_ALIAS (ODBC 2,0)  
 Uma cadeia de caracteres: "Y" se a fonte de dados oferecer suporte a aliases de coluna; caso contrário, "N".  
  
 Um alias de coluna é um nome alternativo que pode ser especificado para uma coluna na lista de seleção usando uma cláusula AS. Um driver compatível com nível de entrada do SQL-92 sempre retornará "Y".  
  
 SQL_CONCAT_NULL_BEHAVIOR (ODBC 1,0)  
 Um valor SQLUSMALLINT que indica como a fonte de dados lida com a concatenação de colunas de tipo de dados de caractere com valor nulo com colunas de tipo de dados de caractere com valor não nulo:  
  
 SQL_CB_NULL = o resultado é um valor nulo.  
  
 SQL_CB_NON_NULL = Result é concatenação de coluna ou colunas com valor não nulo.  
  
 Um driver de nível de entrada do SQL-92 sempre retornará SQL_CB_NULL.  
  
 SQL_CONVERT_BIGINTSQL_CONVERT_BINARYSQL_CONVERT_BIT SQL_CONVERT_CHAR SQL_CONVERT_GUIDSQL_CONVERT_DATESQL_CONVERT_DECIMALSQL_CONVERT_DOUBLESQL_CONVERT_FLOATSQL_CONVERT_INTEGERSQL_CONVERT_INTERVAL_YEAR_MONTHSQL_CONVERT_INTERVAL_ DAY_TIMESQL_CONVERT_LONGVARBINARYSQL_CONVERT_LONGVARCHARSQL_CONVERT_NUMERICSQL_CONVERT_REALSQL_CONVERT_SMALLINTSQL_CONVERT_TIMESQL_CONVERT_TIMESTAMPSQL_CONVERT_TINYINTSQL_CONVERT_VARBINARYSQL_CONVERT_VARCHAR (ODBC 1,0)  
 Um bitmask SQLUINTEGER. A bitmask indica as conversões com suporte da fonte de dados com a função **Convert** escalar para os dados do tipo nomeado no *InfoType*. Se o bitmask for igual a zero, a fonte de dados não oferecerá suporte a quaisquer conversões de dados do tipo nomeado, incluindo a conversão para o mesmo tipo de dados.  
  
 Por exemplo, para determinar se uma fonte de dados dá suporte à conversão de dados de SQL_INTEGER no tipo de dados SQL_BIGINT, um aplicativo chama **SQLGetInfo** com o *infotype* de SQL_CONVERT_INTEGER. O aplicativo executa uma operação **and** com o bitmask retornado e SQL_CVT_BIGINT. Se o valor resultante for diferente de zero, haverá suporte para a conversão.  
  
 As seguintes bitmasks são usadas para determinar quais conversões têm suporte:  
  
 SQL_CVT_BIGINT (ODBC 1.0) SQL_CVT_BINARY (ODBC 1.0) SQL_CVT_BIT (ODBC 1,0) SQL_CVT_GUID (ODBC 3.5) SQL_CVT_CHAR (ODBC 1,0) SQL_CVT_DATE (ODBC 1.0) SQL_CVT_DECIMAL (ODBC 1.0) SQL_CVT_DOUBLE (ODBC 1.0) SQL_CVT_FLOAT (ODBC 1.0) SQL_CVT_INTEGER (ODBC 1.0) SQL _CVT_INTERVAL_YEAR_MONTH (ODBC 3.0) SQL_CVT_INTERVAL_DAY_TIME (ODBC 3.0) SQL_CVT_LONGVARBINARY (ODBC 1.0) SQL_CVT_LONGVARCHAR (ODBC 1.0) SQL_CVT_NUMERIC (ODBC 1.0) SQL_CVT_REAL ODBC 1.0) SQL_CVT_SMALLINT (ODBC 1.0) SQL_CVT_TIME (ODBC 1.0) SQL_CVT_ TIMESTAMP (ODBC 1.0) SQL_CVT_TINYINT (ODBC 1.0) SQL_CVT_VARBINARY (ODBC 1.0) SQL_CVT_VARCHAR (ODBC 1,0)  
  
 SQL_CONVERT_FUNCTIONS (ODBC 1,0)  
 Um bitmask SQLUINTEGER que enumera as funções de conversão escalar com suporte do driver e a fonte de dados associada.  
  
 O seguinte bitmask é usado para determinar quais funções de conversão têm suporte:  
  
 SQL_FN_CVT_CASTSQL_FN_CVT_CONVERT  
  
 SQL_CORRELATION_NAME (ODBC 1,0)  
 Um valor de SQLUSMALLINT que indica se os nomes de correlação de tabela têm suporte:  
  
 SQL_CN_NONE = não há suporte para nomes de correlação.  
  
 SQL_CN_DIFFERENT = os nomes de correlação têm suporte, mas devem ser diferentes dos nomes das tabelas que representam.  
  
 SQL_CN_ANY = há suporte para nomes de correlação e pode ser qualquer nome definido pelo usuário válido.  
  
 Um driver de nível de entrada do SQL-92 sempre retornará SQL_CN_ANY.  
  
 SQL_CREATE_ASSERTION (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera as cláusulas na instrução **Create ASSERTION** , conforme definido em SQL-92, com suporte da fonte de dados.  
  
 As seguintes bitmasks são usadas para determinar quais cláusulas têm suporte:  
  
 SQL_CA_CREATE_ASSERTION  
  
 Os bits a seguir especificarão o atributo de restrição com suporte se a capacidade de especificar explicitamente os atributos de restrição for suportada (consulte os tipos de informações SQL_ALTER_TABLE e SQL_CREATE_TABLE):  
  
 SQL_CA_CONSTRAINT_INITIALLY_DEFERREDSQL_CA_CONSTRAINT_INITIALLY_IMMEDIATESQL_CA_CONSTRAINT_DEFERRABLESQL_CA_CONSTRAINT_NON_DEFERRABLE  
  
 Um driver compatível com nível completo do SQL-92 sempre retornará todas essas opções como com suporte. Um valor de retorno de "0" significa que não há suporte para a instrução **Create ASSERTION** .  
  
 SQL_CREATE_CHARACTER_SET (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera as cláusulas na instrução **Create character set** , conforme definido em SQL-92, com suporte da fonte de dados.  
  
 As seguintes bitmasks são usadas para determinar quais cláusulas têm suporte:  
  
 SQL_CCS_CREATE_CHARACTER_SETSQL_CCS_COLLATE_CLAUSESQL_CCS_LIMITED_COLLATION  
  
 Um driver compatível com nível completo do SQL-92 sempre retornará todas essas opções como com suporte. Um valor de retorno de "0" significa que a instrução **Create character set** não tem suporte.  
  
 SQL_CREATE_COLLATION (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera as cláusulas na instrução **Create Collation** , conforme definido em SQL-92, com suporte da fonte de dados.  
  
 O seguinte bitmask é usado para determinar quais cláusulas têm suporte:  
  
 SQL_CCOL_CREATE_COLLATION  
  
 Um driver compatível com nível completo do SQL-92 sempre retornará essa opção como com suporte. Um valor de retorno de "0" significa que não há suporte para a instrução **Create Collation** .  
  
 SQL_CREATE_DOMAIN (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera as cláusulas na instrução **Create Domain** , conforme definido em SQL-92, com suporte da fonte de dados.  
  
 As seguintes bitmasks são usadas para determinar quais cláusulas têm suporte:  
  
 SQL_CDO_CREATE_DOMAIN = há suporte para a instrução CREATE DOMAIN (nível intermediário).  
  
 SQL_CDO_CONSTRAINT_NAME_DEFINITION = \<definição de nome de restrição> tem suporte para nomear restrições de domínio (nível intermediário).  
  
 Os bits a seguir especificam a capacidade de criar restrições de coluna: SQL_CDO_DEFAULT = a especificação de restrições de domínio tem suporte (nível intermediário) SQL_CDO_CONSTRAINT = a especificação de padrões de domínio é suportada (nível intermediário) SQL_CDO_COLLATION = Há suporte para a especificação de agrupamento de domínios (nível completo)  
  
 Os seguintes bits especificarão os atributos de restrição com suporte se a especificação de restrições de domínio tiver suporte (SQL_CDO_DEFAULT estiver definido):  
  
 SQL_CDO_CONSTRAINT_INITIALLY_DEFERRED (nível completo) SQL_CDO_CONSTRAINT_INITIALLY_IMMEDIATE (nível completo) SQL_CDO_CONSTRAINT_DEFERRABLE SQL_CDO_CONSTRAINT_NON_DEFERRABLE (nível completo)  
  
 Um valor de retorno de "0" significa que não há suporte para a instrução **Create Domain** .  
  
 SQL_CREATE_SCHEMA (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera as cláusulas na instrução **Create Schema** , conforme definido em SQL-92, com suporte da fonte de dados.  
  
 As seguintes bitmasks são usadas para determinar quais cláusulas têm suporte:  
  
 SQL_CS_CREATE_SCHEMASQL_CS_AUTHORIZATIONSQL_CS_DEFAULT_CHARACTER_SET  
  
 Um driver compatível com nível intermediário SQL-92 sempre retornará as opções SQL_CS_CREATE_SCHEMA e SQL_CS_AUTHORIZATION como com suporte. Eles também devem ter suporte no nível de entrada SQL-92, mas não necessariamente como instruções SQL. Um driver compatível com nível completo do SQL-92 sempre retornará todas essas opções como com suporte.  
  
 SQL_CREATE_TABLE (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera as cláusulas na instrução **CREATE TABLE** , conforme definido em SQL-92, com suporte da fonte de dados.  
  
 O nível de conformidade do SQL-92 ou FIPS no qual esse recurso deve ser suportado é mostrado entre parênteses ao lado de cada bitmask.  
  
 As seguintes bitmasks são usadas para determinar quais cláusulas têm suporte:  
  
 SQL_CT_CREATE_TABLE = há suporte para a instrução CREATE TABLE. (Nível de entrada)  
  
 SQL_CT_TABLE_CONSTRAINT = há suporte para a especificação de restrições de tabela (nível de transição FIPS)  
  
 SQL_CT_CONSTRAINT_NAME_DEFINITION = a \<cláusula de definição de nome de restrição> tem suporte para a nomenclatura de restrições de coluna e tabela (nível intermediário)  
  
 Os bits a seguir especificam a capacidade de criar tabelas temporárias:  
  
 SQL_CT_COMMIT_PRESERVE = as linhas excluídas são preservadas na confirmação. (Nível completo) SQL_CT_COMMIT_DELETE = as linhas excluídas são excluídas na confirmação. (Nível completo) SQL_CT_GLOBAL_TEMPORARY = tabelas temporárias globais podem ser criadas. (Nível completo) SQL_CT_LOCAL_TEMPORARY = tabelas temporárias locais podem ser criadas. (Nível completo)  
  
 Os bits a seguir especificam a capacidade de criar restrições de coluna:  
  
 SQL_CT_COLUMN_CONSTRAINT = há suporte para a especificação de restrições de coluna (nível de transição FIPS) SQL_CT_COLUMN_DEFAULT = a especificação de padrões de coluna é suportada (nível de transição FIPS) SQL_CT_COLUMN_COLLATION = a especificação de agrupamento de colunas é com suporte (nível completo)  
  
 Os seguintes bits especificarão os atributos de restrição com suporte se a especificação de restrições de coluna ou tabela for suportada:  
  
 SQL_CT_CONSTRAINT_INITIALLY_DEFERRED (nível completo) SQL_CT_CONSTRAINT_INITIALLY_IMMEDIATE (nível completo) SQL_CT_CONSTRAINT_DEFERRABLE SQL_CT_CONSTRAINT_NON_DEFERRABLE (nível completo)  
  
 SQL_CREATE_TRANSLATION (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera as cláusulas na instrução **Create translation** , conforme definido em SQL-92, com suporte da fonte de dados.  
  
 O seguinte bitmask é usado para determinar quais cláusulas têm suporte:  
  
 SQL_CTR_CREATE_TRANSLATION  
  
 Um driver compatível com nível completo do SQL-92 sempre retornará essas opções como com suporte. Um valor de retorno de "0" significa que não há suporte para a instrução **Create translation** .  
  
 SQL_CREATE_VIEW (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera as cláusulas na instrução **Create View** , conforme definido em SQL-92, com suporte da fonte de dados.  
  
 As seguintes bitmasks são usadas para determinar quais cláusulas têm suporte:  
  
 SQL_CV_CREATE_VIEWSQL_CV_CHECK_OPTIONSQL_CV_CASCADEDSQL_CV_LOCAL  
  
 Um valor de retorno de "0" significa que não há suporte para a instrução **Create View** .  
  
 Um driver de nível de entrada do SQL-92 sempre retornará as opções SQL_CV_CREATE_VIEW e SQL_CV_CHECK_OPTION como com suporte.  
  
 Um driver compatível com nível completo do SQL-92 sempre retornará todas essas opções como com suporte.  
  
 SQL_CURSOR_COMMIT_BEHAVIOR (ODBC 1,0)  
 Um valor SQLUSMALLINT que indica como uma operação de **confirmação** afeta os cursores e as instruções preparadas na fonte de dados (o comportamento da fonte de dados quando você confirma uma transação).  
  
 O valor desse atributo refletirá o estado atual da próxima configuração: SQL_COPT_SS_PRESERVE_CURSORS.  
  
 SQL_CB_DELETE = fechar cursores e excluir instruções preparadas. Para usar o cursor novamente, o aplicativo deve repreparar e executar novamente a instrução.  
  
 SQL_CB_CLOSE = fechar cursores. Para instruções preparadas, o aplicativo pode chamar **SQLExecute** na instrução sem chamar **SQLPrepare** novamente. O padrão para o driver ODBC do SQL é SQL_CB_CLOSE. Isso significa que o driver ODBC do SQL fechará seus Cursors quando você confirmar uma transação.  
  
 SQL_CB_PRESERVE = preservar cursores na mesma posição que antes da operação de **confirmação** . O aplicativo pode continuar a buscar dados ou pode fechar o cursor e executar novamente a instrução sem repará-la.  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR (ODBC 1,0)  
 Um valor SQLUSMALLINT que indica como uma operação de **reversão** afeta os cursores e as instruções preparadas na fonte de dados:  
  
 SQL_CB_DELETE = fechar cursores e excluir instruções preparadas. Para usar o cursor novamente, o aplicativo deve repreparar e executar novamente a instrução.  
  
 SQL_CB_CLOSE = fechar cursores. Para instruções preparadas, o aplicativo pode chamar **SQLExecute** na instrução sem chamar **SQLPrepare** novamente.  
  
 SQL_CB_PRESERVE = preservar cursores na mesma posição que antes da operação de **reversão** . O aplicativo pode continuar a buscar dados ou pode fechar o cursor e executar novamente a instrução sem repará-la.  
  
 SQL_CURSOR_SENSITIVITY (ODBC 3,0)  
 Um valor SQLUINTEGER que indica o suporte para sensibilidade do cursor:  
  
 SQL_INSENSITIVE = todos os cursores no identificador de instrução mostram o conjunto de resultados sem refletir as alterações feitas a ele por qualquer outro cursor dentro da mesma transação.  
  
 SQL_UNSPECIFIED = não é especificado se os cursores no identificador de instrução tornam visíveis as alterações feitas em um conjunto de resultados por outro cursor dentro da mesma transação. Os cursores no identificador de instrução podem tornar visíveis nenhuma, algumas ou todas essas alterações.  
  
 SQL_SENSITIVE = cursores são sensíveis a alterações feitas por outros cursores dentro da mesma transação.  
  
 Um driver de nível de entrada do SQL-92 sempre retornará a opção SQL_UNSPECIFIED como com suporte.  
  
 Um driver compatível com nível completo do SQL-92 sempre retornará a opção SQL_INSENSITIVE como com suporte.  
  
 SQL_DATA_SOURCE_NAME (ODBC 1,0)  
 Uma cadeia de caracteres com o nome da fonte de dados que foi usado durante a conexão. Se o aplicativo chamado **SQLConnect**, esse é o valor do argumento *szDSN* . Se o aplicativo chamado **SQLDriverConnect** ou **SQLBrowseConnect**, esse é o valor da palavra-chave DSN na cadeia de conexão passada para o driver. Se a cadeia de conexão não contiver a palavra-chave **DSN** (por exemplo, quando ela contiver a palavra-chave **Driver** ), essa será uma cadeia de caracteres vazia.  
  
 SQL_DATA_SOURCE_READ_ONLY (ODBC 1,0)  
 Uma cadeia de caracteres. "Y" se a fonte de dados estiver definida como modo somente leitura, "N" se for diferente.  
  
 Essa característica pertence apenas à própria fonte de dados; Não é uma característica do driver que permite o acesso à fonte de dados. Um driver que é de leitura/gravação pode ser usado com uma fonte de dados que é somente leitura. Se um driver for somente leitura, todas as suas fontes de dados deverão ser somente leitura e deverão retornar SQL_DATA_SOURCE_READ_ONLY.  
  
 SQL_DATABASE_NAME (ODBC 1,0)  
 Uma cadeia de caracteres com o nome do banco de dados atual em uso, se a fonte de dado definir um objeto nomeado chamado "Database".  
  
> [!NOTE]
>  No ODBC 3 *. x*, o valor retornado para esse *InfoType* também pode ser retornado chamando **SQLGetConnectAttr** com um argumento de *atributo* de SQL_ATTR_CURRENT_CATALOG.  
  
 SQL_DATETIME_LITERALS (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera os literais SQL-92 DateTime suportados pela fonte de dados. Observe que esses são literais DateTime listados na especificação SQL-92 e são separados das cláusulas de escape literal DateTime definidas pelo ODBC. Para obter mais informações sobre as cláusulas de escape ODBC DateTime literal, consulte [data, hora e literais de carimbo](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)de hora.  
  
 Um driver compatível com nível de transição FIPS sempre retornará o valor "1" no bitmask para os bits na lista a seguir. Um valor de "0" significa que não há suporte para literais de DateTime do SQL-92.  
  
 As seguintes bitmasks são usadas para determinar quais literais têm suporte:  
  
 SQL_DL_SQL92_DATESQL_DL_SQL92_TIMESQL_DL_SQL92_TIMESTAMPSQL_DL_SQL92_INTERVAL_YEARSQL_DL_SQL92_INTERVAL_MONTHSQL_DL_SQL92_INTERVAL_DAYSQL_DL_SQL92_INTERVAL_HOURSQL_DL_SQL92_INTERVAL_MINUTESQL_DL_SQL92_INTERVAL_SECONDSQL_DL_ SQL92_INTERVAL_YEAR_TO_MONTHSQL_DL_SQL92_INTERVAL_DAY_TO_HOUR  
  
 SQL_DL_SQL92_INTERVAL_DAY_TO_MINUTESQL_DL_SQL92_INTERVAL_DAY_TO_SECONDSQL_DL_SQL92_INTERVAL_HOUR_TO_MINUTESQL_DL_SQL92_INTERVAL_HOUR_TO_SECONDSQL_DL_SQL92_INTERVAL_MINUTE_TO_SECOND  
  
 SQL_DBMS_NAME (ODBC 1,0)  
 Uma cadeia de caracteres com o nome do produto DBMS acessado pelo driver.  
  
 SQL_DBMS_VER (ODBC 1,0)  
 Uma cadeia de caracteres que indica a versão do produto DBMS acessado pelo driver. A versão está no formato # #. # #. # # # #, em que os dois primeiros dígitos são a versão principal, os dois próximos dígitos são a versão secundária e os últimos quatro dígitos são a versão de lançamento. O driver deve renderizar a versão do produto DBMS neste formulário, mas também pode acrescentar a versão específica do produto DBMS. Por exemplo, "04.01.0000 RDB 4,1".  
  
 SQL_DDL_INDEX (ODBC 3,0)  
 Um valor SQLUINTEGER que indica suporte para criação e remoção de índices:  
  
 SQL_DI_CREATE_INDEXSQL_DI_DROP_INDEX  
  
 SQL_DEFAULT_TXN_ISOLATION (ODBC 1,0)  
 Um valor SQLUINTEGER que indica o nível de isolamento da transação padrão com suporte pelo driver ou fonte de dados, ou zero se a fonte de dados não oferecer suporte a transações. Os seguintes termos são usados para definir os níveis de isolamento da transação:  
  
 **Leitura suja** A transação 1 altera uma linha. A transação 2 lê a linha alterada antes que a transação 1 confirme a alteração. Se a transação 1 reverter a alteração, a transação 2 terá lido uma linha que é considerada como nunca existia.  
  
 **Leitura não reproduzível** A transação 1 lê uma linha. A transação 2 atualiza ou exclui essa linha e confirma essa alteração. Se a transação 1 tentar ler novamente a linha, ela receberá valores de linha diferentes ou descobrirá que a linha foi excluída.  
  
 **Fantasma** A transação 1 lê um conjunto de linhas que atendem a alguns critérios de pesquisa. A transação 2 gera uma ou mais linhas (por meio de inserções ou atualizações) que correspondem aos critérios de pesquisa. Se a transação 1 executar novamente a instrução que lê as linhas, ela receberá um conjunto diferente de linhas.  
  
 Se a fonte de dados der suporte a transações, o driver retornará uma das seguintes bitmasks:  
  
 SQL_TXN_READ_UNCOMMITTED = leituras sujas, leituras não repetíveis e fantasmas são possíveis.  
  
 SQL_TXN_READ_COMMITTED = leituras sujas não são possíveis. Leituras e fantasmas não repetíveis são possíveis.  
  
 SQL_TXN_REPEATABLE_READ = leituras sujas e leituras não repetíveis não são possíveis. Fantasmas são possíveis.  
  
 SQL_TXN_SERIALIZABLE = as transações são serializáveis. As transações serializáveis não permitem leituras sujas, leituras não repetíveis ou fantasmas.  
  
 SQL_DESCRIBE_PARAMETER (ODBC 3,0)  
 Uma cadeia de caracteres: "Y" se os parâmetros podem ser descritos; "N", se não.  
  
 Um driver compatível com nível completo do SQL-92 normalmente retornará "Y" porque ele dará suporte à instrução de **Descrição de entrada** . Como isso não especifica diretamente o suporte do SQL subjacente, no entanto, a descrição dos parâmetros pode não ser suportada, mesmo em um driver compatível com nível completo do SQL-92.  
  
 SQL_DM_VER (ODBC 3,0)  
 Uma cadeia de caracteres com a versão do Gerenciador de driver. A versão está no formato # #. # #. # # # #. # # # #, em que:  
  
 O primeiro conjunto de dois dígitos é a principal versão do ODBC, conforme fornecido pela constante SQL_SPEC_MAJOR.  
  
 O segundo conjunto de dois dígitos é a versão secundária do ODBC, conforme fornecido pela constante SQL_SPEC_MINOR.  
  
 O terceiro conjunto de quatro dígitos é o número de Build principal do Gerenciador de driver.  
  
 O último conjunto de quatro dígitos é o número de Build secundário do Gerenciador de driver.  
  
 A versão do Gerenciador de driver do Windows 7 é 3,80. A versão do Gerenciador de driver do Windows 8 é 3,81.  
  
 SQL_DRIVER_AWARE_POOLING_SUPPORTED (ODBC 3,8)  
 Um valor SQLUINTEGER que indica se o driver dá suporte ao pool com reconhecimento de driver. (Para obter mais informações, consulte [pooling de conexão com suporte a driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md).  
  
 SQL_DRIVER_AWARE_POOLING_CAPABLE indica que o driver pode dar suporte ao mecanismo de Pooling com reconhecimento de driver.  
  
 SQL_DRIVER_AWARE_POOLING_NOT_CAPABLE indica que o driver não pode dar suporte ao mecanismo de Pooling com reconhecimento de driver.  
  
 Um driver não precisa implementar SQL_DRIVER_AWARE_POOLING_SUPPORTED e o Gerenciador de driver não vai respeitar o valor de retorno do driver.  
  
 SQL_DRIVER_HDBCSQL_DRIVER_HENV (ODBC 1,0)  
 Um valor SQLULEN, o identificador de ambiente do driver ou o identificador de conexão, determinado pelo argumento *InfoType*.  
  
 Esses tipos de informações são implementados apenas pelo Gerenciador de driver.  
  
 SQL_DRIVER_HDESC (ODBC 3,0)  
 Um valor SQLULEN, o identificador do descritor do driver determinado pelo identificador do descritor do Gerenciador de driver, que deve ser \*passado na entrada em *InfoValuePtr* do aplicativo. Nesse caso, *InfoValuePtr* é um argumento de entrada e de saída. O identificador do descritor de \*entrada passado em *InfoValuePtr* deve ter sido explicitamente ou implicitamente alocado no *ConnectionHandle*.  
  
 O aplicativo deve fazer uma cópia do identificador do descritor do Gerenciador de driver antes de chamar **SQLGetInfo** com esse tipo de informação, para garantir que o identificador não seja substituído na saída.  
  
 Esse tipo de informação é implementado apenas pelo Gerenciador de driver.  
  
 SQL_DRIVER_HLIB (ODBC 2,0)  
 Um valor SQLULEN, o *hinst* da biblioteca de carregamento retornado ao Gerenciador de driver quando ele carregou a DLL do driver em um sistema operacional Microsoft Windows ou seu equivalente em outro sistema operacional. O identificador é válido somente para o identificador de conexão especificado na chamada para **SQLGetInfo**.  
  
 Esse tipo de informação é implementado apenas pelo Gerenciador de driver.  
  
 SQL_DRIVER_HSTMT (ODBC 1,0)  
 Um valor SQLULEN, o identificador de instrução do driver determinado pelo identificador de instrução do Gerenciador de driver, que deve ser passado \*na entrada em *InfoValuePtr* do aplicativo. Nesse caso, *InfoValuePtr* é um argumento de entrada e de saída. O identificador de instrução de entrada \*passado em *InfoValuePtr* deve ter sido alocado no argumento *ConnectionHandle*.  
  
 O aplicativo deve fazer uma cópia do identificador de instrução do Gerenciador de driver antes de chamar **SQLGetInfo** com esse tipo de informação, para garantir que o identificador não seja substituído na saída.  
  
 Esse tipo de informação é implementado apenas pelo Gerenciador de driver.  
  
 SQL_DRIVER_NAME (ODBC 1,0)  
 Uma cadeia de caracteres com o nome do arquivo do driver usado para acessar a fonte de dados.  
  
 SQL_DRIVER_ODBC_VER (ODBC 2,0)  
 Uma cadeia de caracteres com a versão do ODBC à qual o driver dá suporte. A versão está no formato # #. # #, em que os dois primeiros dígitos são a versão principal e os próximos dois dígitos são a versão secundária. SQL_SPEC_MAJOR e SQL_SPEC_MINOR definem os números de versão principal e secundária. Para a versão do ODBC descrita neste manual, eles são 3 e 0, e o driver deve retornar "3, 0".  
  
 O Gerenciador de driver ODBC não modificará o valor de retorno de SQLGetInfo (SQL_DRIVER_ODBC_VER) para manter a compatibilidade com versões anteriores para aplicativos existentes. O driver especifica qual valor será retornado. No entanto, um driver que dá suporte à extensibilidade de tipo de dados C deve retornar 3,8 (ou superior) quando um aplicativo chama **SQLSetEnvAttr** para definir SQL_ATTR_ODBC_VERSION como 3,8. Para obter mais informações, consulte [Tipos de dados C em ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 SQL_DRIVER_VER (ODBC 1,0)  
 Uma cadeia de caracteres com a versão do driver e, opcionalmente, uma descrição do driver. No mínimo, a versão está no formato # #. # #. # # # #, em que os dois primeiros dígitos são a versão principal, os dois próximos dígitos são a versão secundária e os últimos quatro dígitos são a versão de lançamento.  
  
 SQL_DROP_ASSERTION (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera as cláusulas na instrução **drop ASSERTION** , conforme definido em SQL-92, com suporte da fonte de dados.  
  
 O seguinte bitmask é usado para determinar quais cláusulas têm suporte:  
  
 SQL_DA_DROP_ASSERTION  
  
 Um driver compatível com nível completo do SQL-92 sempre retornará essa opção como com suporte.  
  
 SQL_DROP_CHARACTER_SET (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera as cláusulas na instrução **drop character set** , conforme definido em SQL-92, com suporte da fonte de dados.  
  
 O seguinte bitmask é usado para determinar quais cláusulas têm suporte:  
  
 SQL_DCS_DROP_CHARACTER_SET  
  
 Um driver compatível com nível completo do SQL-92 sempre retornará essa opção como com suporte.  
  
 SQL_DROP_COLLATION (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera as cláusulas na instrução **drop Collation** , conforme definido em SQL-92, com suporte da fonte de dados.  
  
 O seguinte bitmask é usado para determinar quais cláusulas têm suporte:  
  
 SQL_DC_DROP_COLLATION  
  
 Um driver compatível com nível completo do SQL-92 sempre retornará essa opção como com suporte.  
  
 SQL_DROP_DOMAIN (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera as cláusulas na instrução **drop Domain** , conforme definido em SQL-92, com suporte da fonte de dados.  
  
 As seguintes bitmasks são usadas para determinar quais cláusulas têm suporte:  
  
 SQL_DD_DROP_DOMAINSQL_DD_CASCADESQL_DD_RESTRICT  
  
 Um driver compatível com nível intermediário do SQL-92 sempre retornará todas essas opções como com suporte.  
  
 SQL_DROP_SCHEMA (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera as cláusulas na instrução **drop Schema** , conforme definido em SQL-92, com suporte da fonte de dados.  
  
 As seguintes bitmasks são usadas para determinar quais cláusulas têm suporte:  
  
 SQL_DS_DROP_SCHEMASQL_DS_CASCADESQL_DS_RESTRICT  
  
 Um driver compatível com nível intermediário do SQL-92 sempre retornará todas essas opções como com suporte.  
  
 SQL_DROP_TABLE (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera as cláusulas na instrução **DROP TABLE** , conforme definido em SQL-92, com suporte da fonte de dados.  
  
 As seguintes bitmasks são usadas para determinar quais cláusulas têm suporte:  
  
 SQL_DT_DROP_TABLESQL_DT_CASCADESQL_DT_RESTRICT  
  
 Um driver compatível com nível de transição FIPS sempre retornará todas essas opções como com suporte.  
  
 SQL_DROP_TRANSLATION (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera as cláusulas na instrução **drop translation** , conforme definido em SQL-92, com suporte da fonte de dados.  
  
 O seguinte bitmask é usado para determinar quais cláusulas têm suporte:  
  
 SQL_DTR_DROP_TRANSLATION  
  
 Um driver compatível com nível completo do SQL-92 sempre retornará essa opção como com suporte.  
  
 SQL_DROP_VIEW (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera as cláusulas na instrução **drop View** , conforme definido em SQL-92, com suporte da fonte de dados.  
  
 As seguintes bitmasks são usadas para determinar quais cláusulas têm suporte:  
  
 SQL_DV_DROP_VIEWSQL_DV_CASCADESQL_DV_RESTRICT  
  
 Um driver compatível com nível de transição FIPS sempre retornará todas essas opções como com suporte.  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (ODBC 3,0)  
 Um bitmask SQLUINTEGER que descreve os atributos de um cursor dinâmico que são suportados pelo driver. Essa bitmask contém o primeiro subconjunto de atributos; para o segundo subconjunto, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES2.  
  
 As seguintes bitmasks são usadas para determinar quais atributos têm suporte:  
  
 SQL_CA1_NEXT = um argumento *FetchOrientation* de SQL_FETCH_NEXT tem suporte em uma chamada para **SQLFetchScroll** quando o cursor é um cursor dinâmico.  
  
 SQL_CA1_ABSOLUTE = os argumentos *FetchOrientation* de SQL_FETCH_FIRST, SQL_FETCH_LAST e SQL_FETCH_ABSOLUTE têm suporte em uma chamada para **SQLFetchScroll** quando o cursor é um cursor dinâmico. (O conjunto de linhas que será buscado é independente da posição atual do cursor.)  
  
 SQL_CA1_RELATIVE = os argumentos *FetchOrientation* de SQL_FETCH_PRIOR e SQL_FETCH_RELATIVE têm suporte em uma chamada para **SQLFetchScroll** quando o cursor é um cursor dinâmico. (O conjunto de linhas que será buscado depende da posição atual do cursor. Observe que isso é separado do SQL_FETCH_NEXT porque, em um cursor somente de avanço, há suporte apenas para SQL_FETCH_NEXT.)  
  
 SQL_CA1_BOOKMARK = um argumento *FetchOrientation* de SQL_FETCH_BOOKMARK tem suporte em uma chamada para **SQLFetchScroll** quando o cursor é um cursor dinâmico.  
  
 SQL_CA1_LOCK_EXCLUSIVE = um argumento *LockType* de SQL_LOCK_EXCLUSIVE tem suporte em uma chamada para **SQLSetPos** quando o cursor é um cursor dinâmico.  
  
 SQL_CA1_LOCK_NO_CHANGE = um argumento *LockType* de SQL_LOCK_NO_CHANGE tem suporte em uma chamada para **SQLSetPos** quando o cursor é um cursor dinâmico.  
  
 SQL_CA1_LOCK_UNLOCK = um argumento *LockType* de SQL_LOCK_UNLOCK tem suporte em uma chamada para **SQLSetPos** quando o cursor é um cursor dinâmico.  
  
 SQL_CA1_POS_POSITION = um argumento de *operação* de SQL_POSITION tem suporte em uma chamada para **SQLSetPos** quando o cursor é um cursor dinâmico.  
  
 SQL_CA1_POS_UPDATE = um argumento de *operação* de SQL_UPDATE tem suporte em uma chamada para **SQLSetPos** quando o cursor é um cursor dinâmico.  
  
 SQL_CA1_POS_DELETE = um argumento de *operação* de SQL_DELETE tem suporte em uma chamada para **SQLSetPos** quando o cursor é um cursor dinâmico.  
  
 SQL_CA1_POS_REFRESH = um argumento de *operação* de SQL_REFRESH tem suporte em uma chamada para **SQLSetPos** quando o cursor é um cursor dinâmico.  
  
 SQL_CA1_POSITIONED_UPDATE = uma atualização na qual o atual da instrução SQL tem suporte quando o cursor é um cursor dinâmico. (Um driver compatível com nível de entrada do SQL-92 sempre retornará essa opção como com suporte.)  
  
 SQL_CA1_POSITIONED_DELETE = uma exclusão na qual o atual da instrução SQL tem suporte quando o cursor é um cursor dinâmico. (Um driver compatível com nível de entrada do SQL-92 sempre retornará essa opção como com suporte.)  
  
 SQL_CA1_SELECT_FOR_UPDATE = uma instrução SELECT FOR UPDATE SQL tem suporte quando o cursor é um cursor dinâmico. (Um driver compatível com nível de entrada do SQL-92 sempre retornará essa opção como com suporte.)  
  
 SQL_CA1_BULK_ADD = um argumento de *operação* de SQL_ADD tem suporte em uma chamada para **SQLBulkOperations** quando o cursor é um cursor dinâmico.  
  
 SQL_CA1_BULK_UPDATE_BY_BOOKMARK = um argumento de *operação* de SQL_UPDATE_BY_BOOKMARK tem suporte em uma chamada para **SQLBulkOperations** quando o cursor é um cursor dinâmico.  
  
 SQL_CA1_BULK_DELETE_BY_BOOKMARK = um argumento de *operação* de SQL_DELETE_BY_BOOKMARK tem suporte em uma chamada para **SQLBulkOperations** quando o cursor é um cursor dinâmico.  
  
 SQL_CA1_BULK_FETCH_BY_BOOKMARK = um argumento de *operação* de SQL_FETCH_BY_BOOKMARK tem suporte em uma chamada para **SQLBulkOperations** quando o cursor é um cursor dinâmico.  
  
 Um driver compatível com nível intermediário do SQL-92 geralmente retornará as opções SQL_CA1_NEXT, SQL_CA1_ABSOLUTE e SQL_CA1_RELATIVE como com suporte, pois ele dá suporte a cursores roláveis por meio da instrução SQL FETCH inserida. Como isso não determina diretamente o suporte do SQL subjacente, no entanto, os cursores roláveis podem não ter suporte, mesmo para um driver compatível com nível intermediário do SQL-92.  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES2 (ODBC 3,0)  
 Um bitmask SQLUINTEGER que descreve os atributos de um cursor dinâmico que são suportados pelo driver. Essa bitmask contém o segundo subconjunto de atributos; para o primeiro subconjunto, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES1.  
  
 As seguintes bitmasks são usadas para determinar quais atributos têm suporte:  
  
 SQL_CA2_READ_ONLY_CONCURRENCY = um cursor dinâmico somente leitura, no qual não há atualizações permitidas, tem suporte. (O atributo de instrução SQL_ATTR_CONCURRENCY pode ser SQL_CONCUR_READ_ONLY para um cursor dinâmico).  
  
 SQL_CA2_LOCK_CONCURRENCY = um cursor dinâmico que usa o nível mais baixo de bloqueio suficiente para certificar-se de que a linha pode ser atualizada tem suporte. (O atributo de instrução SQL_ATTR_CONCURRENCY pode ser SQL_CONCUR_LOCK para um cursor dinâmico.) Esses bloqueios devem ser consistentes com o nível de isolamento da transação definido pelo atributo de conexão SQL_ATTR_TXN_ISOLATION.  
  
 SQL_CA2_OPT_ROWVER_CONCURRENCY = um cursor dinâmico que usa o controle de simultaneidade otimista comparando versões de linha tem suporte. (O atributo de instrução SQL_ATTR_CONCURRENCY pode ser SQL_CONCUR_ROWVER para um cursor dinâmico.)  
  
 SQL_CA2_OPT_VALUES_CONCURRENCY = um cursor dinâmico que usa o controle de simultaneidade otimista comparando valores é suportado. (O atributo de instrução SQL_ATTR_CONCURRENCY pode ser SQL_CONCUR_VALUES para um cursor dinâmico.)  
  
 SQL_CA2_SENSITIVITY_ADDITIONS = as linhas adicionadas são visíveis para um cursor dinâmico; o cursor pode rolar para essas linhas. (Onde essas linhas são adicionadas ao cursor depende do driver.)  
  
 SQL_CA2_SENSITIVITY_DELETIONS = as linhas excluídas não estão mais disponíveis para um cursor dinâmico e não deixam um "buraco" no conjunto de resultados; Depois que o cursor dinâmico rola de uma linha excluída, ele não pode retornar a essa linha.  
  
 SQL_CA2_SENSITIVITY_UPDATES = atualizações para linhas são visíveis para um cursor dinâmico; Se o cursor dinâmico rolar de e retornar para uma linha atualizada, os dados retornados pelo cursor serão os dados atualizados, não os dados originais.  
  
 SQL_CA2_MAX_ROWS_SELECT = o atributo de instrução SQL_ATTR_MAX_ROWS afeta as instruções **Select** quando o cursor é um cursor dinâmico.  
  
 SQL_CA2_MAX_ROWS_INSERT = o atributo de instrução SQL_ATTR_MAX_ROWS afeta as instruções **Insert** quando o cursor é um cursor dinâmico.  
  
 SQL_CA2_MAX_ROWS_DELETE = o atributo de instrução SQL_ATTR_MAX_ROWS afeta as instruções **delete** quando o cursor é um cursor dinâmico.  
  
 SQL_CA2_MAX_ROWS_UPDATE = o atributo de instrução SQL_ATTR_MAX_ROWS afeta as instruções **Update** quando o cursor é um cursor dinâmico.  
  
 SQL_CA2_MAX_ROWS_CATALOG = o atributo de instrução SQL_ATTR_MAX_ROWS afeta os conjuntos de resultados do **Catálogo** quando o cursor é um cursor dinâmico.  
  
 SQL_CA2_MAX_ROWS_AFFECTS_ALL = o atributo de instrução SQL_ATTR_MAX_ROWS afeta as instruções **Select**, **Insert**, **delete**e **Update** e os conjuntos de resultados do **Catálogo** , quando o cursor é um cursor dinâmico.  
  
 SQL_CA2_CRC_EXACT = a contagem de linhas exata está disponível no campo diagnóstico SQL_DIAG_CURSOR_ROW_COUNT quando o cursor é um cursor dinâmico.  
  
 SQL_CA2_CRC_APPROXIMATE = uma contagem aproximada de linhas está disponível no campo diagnóstico SQL_DIAG_CURSOR_ROW_COUNT quando o cursor é um cursor dinâmico.  
  
 SQL_CA2_SIMULATE_NON_UNIQUE = o driver não garante que as instruções de atualização ou exclusão posicionadas, afetarão apenas uma linha quando o cursor for um cursor dinâmico; é responsabilidade do aplicativo garantir isso. (Se uma instrução afetar mais de uma linha, **SQLExecute** ou **SQLExecDirect** retornará SQLSTATE 01001 [conflito de operação do cursor].) Para definir esse comportamento, o aplicativo chama **SQLSetStmtAttr** com o atributo SQL_ATTR_SIMULATE_CURSOR definido como SQL_SC_NON_UNIQUE.  
  
 SQL_CA2_SIMULATE_TRY_UNIQUE = o driver tenta garantir que as instruções de atualização ou exclusão posicionadas, afetarão apenas uma linha quando o cursor for um cursor dinâmico. O driver sempre executa essas instruções, mesmo que elas possam afetar mais de uma linha, como quando não há nenhuma chave exclusiva. (Se uma instrução afetar mais de uma linha, **SQLExecute** ou **SQLExecDirect** retornará SQLSTATE 01001 [conflito de operação do cursor].) Para definir esse comportamento, o aplicativo chama **SQLSetStmtAttr** com o atributo SQL_ATTR_SIMULATE_CURSOR definido como SQL_SC_TRY_UNIQUE.  
  
 SQL_CA2_SIMULATE_UNIQUE = o driver garante que as instruções de atualização ou exclusão posicionadas, afetarão apenas uma linha quando o cursor for um cursor dinâmico. Se o driver não puder garantir isso para uma determinada instrução, **SQLExecDirect** ou **SQLPrepare** retornará SQLSTATE 01001 (conflito de operação do cursor). Para definir esse comportamento, o aplicativo chama **SQLSetStmtAttr** com o atributo SQL_ATTR_SIMULATE_CURSOR definido como SQL_SC_UNIQUE.  
  
 SQL_EXPRESSIONS_IN_ORDERBY (ODBC 1,0)  
 Uma cadeia de caracteres: "Y" se a fonte de dados der suporte a expressões na lista **ordenar por** ; "N" se não tiver.  
  
 SQL_FILE_USAGE (ODBC 2,0)  
 Um valor SQLUSMALLINT que indica como um driver de camada única trata diretamente os arquivos em uma fonte de dados:  
  
 SQL_FILE_NOT_SUPPORTED = o driver não é um driver de camada única. Por exemplo, um driver ORACLE é um driver de duas camadas.  
  
 SQL_FILE_TABLE = um driver de camada única trata os arquivos em uma fonte de dados como tabelas. Por exemplo, um driver Xbase trata cada arquivo Xbase como uma tabela.  
  
 SQL_FILE_CATALOG = um driver de camada única trata os arquivos em uma fonte de dados como um catálogo. Por exemplo, um driver do Microsoft Access trata cada arquivo do Microsoft Access como um banco de dados completo.  
  
 Um aplicativo pode usar isso para determinar como os usuários selecionarão os dados. Por exemplo, os usuários Xbase costumam considerar os dados armazenados em arquivos, enquanto os usuários do ORACLE e do Microsoft Access geralmente consideram os dados armazenados em tabelas.  
  
 Quando um usuário seleciona uma fonte de dados Xbase, o aplicativo pode exibir a caixa de diálogo comum **Abrir arquivo** do Windows; Quando o usuário seleciona uma fonte de dados do Microsoft Access ou ORACLE, o aplicativo pode exibir uma caixa de diálogo de **seleção de tabela** personalizada.  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1 (ODBC 3,0)  
 Um bitmask SQLUINTEGER que descreve os atributos de um cursor de somente avanço que são suportados pelo driver. Essa bitmask contém o primeiro subconjunto de atributos; para o segundo subconjunto, consulte SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2.  
  
 As seguintes bitmasks são usadas para determinar quais atributos têm suporte:  
  
 SQL_CA1_NEXTSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_ UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 Para obter descrições desses bitmasks, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (e substitua "cursor de somente encaminhamento" para "cursor dinâmico" nas descrições).  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2 (ODBC 3,0)  
 Um bitmask SQLUINTEGER que descreve os atributos de um cursor de somente avanço que são suportados pelo driver. Essa bitmask contém o segundo subconjunto de atributos; para o primeiro subconjunto, consulte SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1.  
  
 As seguintes bitmasks são usadas para determinar quais atributos têm suporte:  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_ CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_ SIMULATE_UNIQUE  
  
 Para obter descrições desses bitmasks, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES2 (e substitua "cursor de somente encaminhamento" para "cursor dinâmico" nas descrições).  
  
 SQL_GETDATA_EXTENSIONS (ODBC 2,0)  
 Um bitmask SQLUINTEGER enumerando extensões para **SQLGetData**.  
  
 As seguintes bitmasks são usadas junto com o sinalizador para determinar as extensões comuns às quais o driver dá suporte para **SQLGetData**:  
  
 SQL_GD_ANY_COLUMN = **SQLGetData** pode ser chamado para qualquer coluna desassociada, incluindo aqueles antes da última coluna associada. Observe que as colunas devem ser chamadas em ordem crescente de número de coluna, a menos que SQL_GD_ANY_ORDER também seja retornado.  
  
 SQL_GD_ANY_ORDER = **SQLGetData** pode ser chamado para colunas desassociadas em qualquer ordem. Observe que **SQLGetData** pode ser chamado somente para colunas após a última coluna associada, a menos que SQL_GD_ANY_COLUMN também seja retornado.  
  
 SQL_GD_BLOCK = **SQLGetData** pode ser chamado para uma coluna não associada em qualquer linha em um bloco (onde o tamanho do conjunto de linhas é maior que 1) de dados após o posicionamento para essa linha com **SQLSetPos**.  
  
 SQL_GD_BOUND = **SQLGetData** pode ser chamado para colunas associadas além de colunas desassociadas. Um driver não pode retornar esse valor, a menos que ele também retorne SQL_GD_ANY_COLUMN.  
  
 SQL_GD_OUTPUT_PARAMS = **SQLGetData** pode ser chamado para retornar valores de parâmetro de saída. Para obter mais informações, consulte [Recuperando parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
 **SQLGetData** é necessário para retornar dados somente de colunas não associadas que ocorrem após a última coluna associada, são chamados na ordem de aumento do número da coluna e não estão em uma linha em um bloco de linhas.  
  
 Se um driver oferecer suporte a indicadores (comprimento fixo ou comprimento variável), ele deverá dar suporte à chamada de **SQLGetData** na coluna 0. Esse suporte é necessário, independentemente do que o driver retorna para uma chamada para **SQLGetInfo** com o SQL_GETDATA_EXTENSIONS *InfoType*.  
  
 SQL_GROUP_BY (ODBC 2,0)  
 Um valor SQLUSMALLINT que especifica a relação entre as colunas na cláusula **Group by** e as colunas não agregadas na lista de seleção:  
  
 SQL_GB_COLLATE = uma cláusula **COLLATE** pode ser especificada no final de cada coluna de agrupamento. (ODBC 3,0)  
  
 Não há suporte para SQL_GB_NOT_SUPPORTED = cláusulas **Group by** . (ODBC 2,0)  
  
 SQL_GB_GROUP_BY_EQUALS_SELECT = a cláusula **Group by** deve conter todas as colunas não agregadas na lista de seleção. Ele não pode conter nenhuma outra coluna. Por exemplo, **selecione Depto, Max (salário) do grupo de funcionários por departamento**. (ODBC 2,0)  
  
 SQL_GB_GROUP_BY_CONTAINS_SELECT = a cláusula **Group by** deve conter todas as colunas não agregadas na lista de seleção. Ele pode conter colunas que não estão na lista de seleção. Por exemplo, **selecione Depto, Max (salário) do grupo de funcionários por departamento, idade**. (ODBC 2,0)  
  
 SQL_GB_NO_RELATION = as colunas na cláusula **Group by** e a lista SELECT não estão relacionadas. O significado das colunas não agrupadas e não agregadas na lista de seleção é dependente da fonte de dados. Por exemplo, **selecione Depto, salário do grupo de funcionários por departamento, idade**. (ODBC 2,0)  
  
 Um driver de nível de entrada do SQL-92 sempre retornará a opção SQL_GB_GROUP_BY_EQUALS_SELECT como com suporte. Um driver compatível com nível completo do SQL-92 sempre retornará a opção SQL_GB_COLLATE como com suporte. Se nenhuma das opções tiver suporte, a cláusula **Group by** não terá suporte da fonte de dados.  
  
 SQL_IDENTIFIER_CASE (ODBC 1,0)  
 Um valor de SQLUSMALLINT da seguinte maneira:  
  
 SQL_IC_UPPER = identificadores no SQL não diferenciam maiúsculas de minúsculas e são armazenados em letras maiúsculas no catálogo do sistema.  
  
 Os identificadores SQL_IC_LOWER = no SQL não diferenciam maiúsculas de minúsculas e são armazenados em letras minúsculas no catálogo do sistema.  
  
 SQL_IC_SENSITIVE = identificadores no SQL diferenciam maiúsculas de minúsculas e são armazenados em caso misto no catálogo do sistema.  
  
 SQL_IC_MIXED = identificadores no SQL não diferenciam maiúsculas de minúsculas e são armazenados em maiúsculas e minúsculas no catálogo do sistema.  
  
 Como os identificadores em SQL-92 nunca diferenciam maiúsculas de minúsculas, um driver que está de acordo com o SQL-92 (qualquer nível) nunca retornará a opção SQL_IC_SENSITIVE como com suporte.  
  
 SQL_IDENTIFIER_QUOTE_CHAR (ODBC 1,0)  
 A cadeia de caracteres que é usada como o delimitador inicial e final de um identificador entre aspas (delimitados) nas instruções SQL. (Os identificadores passados como argumentos para funções ODBC não precisam ser colocados entre aspas.) Se a fonte de dados não oferecer suporte a identificadores entre aspas, um espaço em branco será retornado.  
  
 Essa cadeia de caracteres também pode ser usada para a cotação de argumentos de função de catálogo quando o atributo de conexão SQL_ATTR_METADATA_ID é definido como SQL_TRUE.  
  
 Como o caractere de aspas de identificador em SQL-92 é a aspa dupla ("), um driver que está de acordo com o SQL-92 sempre retornará o caractere de aspas duplas.  
  
 SQL_INDEX_KEYWORDS (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera palavras-chave na instrução CREATE INDEX que são suportadas pelo driver:  
  
 SQL_IK_NONE = não há suporte para nenhuma das palavras-chave.  
  
 SQL_IK_ASC = há suporte para a palavra-chave ASC.  
  
 SQL_IK_DESC = há suporte para a palavra-chave DESC.  
  
 SQL_IK_ALL = há suporte para todas as palavras-chave.  
  
 Para ver se a instrução CREATE INDEX tem suporte, um aplicativo chama **SQLGetInfo** com o tipo de informação SQL_DLL_INDEX.  
  
 SQL_INFO_SCHEMA_VIEWS (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera as exibições no INFORMATION_SCHEMA que são compatíveis com o driver. As exibições no, e o conteúdo de, INFORMATION_SCHEMA são conforme definido em SQL-92.  
  
 O nível de conformidade do SQL-92 ou FIPS no qual esse recurso deve ser suportado é mostrado entre parênteses ao lado de cada bitmask.  
  
 As seguintes bitmasks são usadas para determinar quais modos de exibição têm suporte:  
  
 SQL_ISV_ASSERTIONS = identifica as asserções do catálogo que pertencem a um determinado usuário. (Nível completo)  
  
 SQL_ISV_CHARACTER_SETS = identifica os conjuntos de caracteres do catálogo que podem ser acessados por um determinado usuário. (Nível intermediário)  
  
 SQL_ISV_CHECK_CONSTRAINTS = identifica as restrições de verificação que pertencem a um determinado usuário. (Nível intermediário)  
  
 SQL_ISV_COLLATIONS = identifica os agrupamentos de caracteres para o catálogo que podem ser acessados por um determinado usuário. (Nível completo)  
  
 SQL_ISV_COLUMN_DOMAIN_USAGE = identifica colunas para o catálogo que dependem de domínios definidos no catálogo e que pertencem a um determinado usuário. (Nível intermediário)  
  
 SQL_ISV_COLUMN_PRIVILEGES = identifica os privilégios em colunas de tabelas persistentes que estão disponíveis ou concedidas por um determinado usuário. (Nível de transição FIPS)  
  
 SQL_ISV_COLUMNS = identifica as colunas de tabelas persistentes que podem ser acessadas por um determinado usuário. (Nível de transição FIPS)  
  
 SQL_ISV_CONSTRAINT_COLUMN_USAGE = semelhante a CONSTRAINT_TABLE_USAGE exibição, as colunas são identificadas para as várias restrições que pertencem a um determinado usuário. (Nível intermediário)  
  
 SQL_ISV_CONSTRAINT_TABLE_USAGE = identifica as tabelas que são usadas por restrições (referenciais, exclusivas e asserções) e são de propriedade de um determinado usuário. (Nível intermediário)  
  
 SQL_ISV_DOMAIN_CONSTRAINTS = identifica as restrições de domínio (dos domínios no catálogo) que podem ser acessadas por um determinado usuário. (Nível intermediário)  
  
 SQL_ISV_DOMAINS = identifica os domínios definidos em um catálogo que podem ser acessados pelo usuário. (Nível intermediário)  
  
 SQL_ISV_KEY_COLUMN_USAGE = identifica colunas definidas no catálogo que são restritas como chaves por um determinado usuário. (Nível intermediário)  
  
 SQL_ISV_REFERENTIAL_CONSTRAINTS = identifica as restrições referenciais que pertencem a um determinado usuário. (Nível intermediário)  
  
 SQL_ISV_SCHEMATA = identifica os esquemas que pertencem a um determinado usuário. (Nível intermediário)  
  
 SQL_ISV_SQL_LANGUAGES = identifica os níveis de conformidade do SQL, as opções e os dialetos suportados pela implementação do SQL. (Nível intermediário)  
  
 SQL_ISV_TABLE_CONSTRAINTS = identifica as restrições de tabela que pertencem a um determinado usuário. (Nível intermediário)  
  
 SQL_ISV_TABLE_PRIVILEGES = identifica os privilégios em tabelas persistentes que estão disponíveis ou concedidas por um determinado usuário. (Nível de transição FIPS)  
  
 SQL_ISV_TABLES = identifica as tabelas persistentes definidas em um catálogo que podem ser acessadas por um determinado usuário. (Nível de transição FIPS)  
  
 SQL_ISV_TRANSLATIONS = identifica as conversões de caracteres para o catálogo que podem ser acessadas por um determinado usuário. (Nível completo)  
  
 SQL_ISV_USAGE_PRIVILEGES = identifica os privilégios de uso em objetos de catálogo que estão disponíveis para ou pertencentes a um determinado usuário. (Nível de transição FIPS)  
  
 SQL_ISV_VIEW_COLUMN_USAGE = identifica as colunas nas quais as exibições do catálogo que pertencem a um determinado usuário são dependentes. (Nível intermediário)  
  
 SQL_ISV_VIEW_TABLE_USAGE = identifica as tabelas nas quais as exibições do catálogo que pertencem a um determinado usuário são dependentes. (Nível intermediário)  
  
 SQL_ISV_VIEWS = identifica as tabelas exibidas definidas neste catálogo que podem ser acessadas por um determinado usuário. (Nível de transição FIPS)  
  
 SQL_INSERT_STATEMENT (ODBC 3,0)  
 Um bitmask SQLUINTEGER que indica suporte para instruções **Insert** :  
  
 SQL_IS_INSERT_LITERALS  
  
 SQL_IS_INSERT_SEARCHED  
  
 SQL_IS_SELECT_INTO  
  
 Um driver de nível de entrada do SQL-92 sempre retornará todas essas opções como com suporte.  
  
 SQL_INTEGRITY (ODBC 1,0)  
 Uma cadeia de caracteres: "Y" se a fonte de dados der suporte à instalação de aperfeiçoamento de integridade; "N" se não tiver.  
  
 Este *InfoType* foi renomeado para ODBC 3,0 do ODBC 2,0 *InfoType* SQL_ODBC_SQL_OPT_IEF.  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES1 (ODBC 3,0)  
 Um bitmask SQLUINTEGER que descreve os atributos de um cursor do conjunto de chaves que são suportados pelo driver. Essa bitmask contém o primeiro subconjunto de atributos; para o segundo subconjunto, consulte SQL_KEYSET_CURSOR_ATTRIBUTES2.  
  
 As seguintes bitmasks são usadas para determinar quais atributos têm suporte:  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_ UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 Para obter descrições desses bitmasks, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (e substitua "cursor controlado por conjunto de chaves" para "cursor dinâmico" nas descrições).  
  
 Um driver compatível com nível intermediário do SQL-92 geralmente retorna as opções SQL_CA1_NEXT, SQL_CA1_ABSOLUTE e SQL_CA1_RELATIVE, como com suporte, porque o driver dá suporte a cursores roláveis por meio da instrução SQL FETCH inserida. Como isso não determina diretamente o suporte do SQL subjacente, no entanto, os cursores roláveis podem não ter suporte, mesmo para um driver compatível com nível intermediário do SQL-92.  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES2 (ODBC 3,0)  
 Um bitmask SQLUINTEGER que descreve os atributos de um cursor do conjunto de chaves que são suportados pelo driver. Essa bitmask contém o segundo subconjunto de atributos; para o primeiro subconjunto, consulte SQL_KEYSET_CURSOR_ATTRIBUTES1.  
  
 As seguintes bitmasks são usadas para determinar quais atributos têm suporte:  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_ CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_ SIMULATE_UNIQUE  
  
 Para obter descrições desses bitmasks, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (e substitua "cursor controlado por conjunto de chaves" para "cursor dinâmico" nas descrições).  
  
 SQL_KEYWORDS (ODBC 2,0)  
 Uma cadeia de caracteres que contém uma lista separada por vírgulas de todas as palavras-chave específicas da fonte de dados. Esta lista não contém palavras-chave específicas para ODBC ou palavras-chave usadas pela fonte de dados e pelo ODBC. Esta lista representa todas as palavras-chave reservadas; aplicativos interoperáveis não devem usar essas palavras em nomes de objetos.  
  
 Para obter uma lista de palavras-chave ODBC, consulte [palavras-chave reservadas](../../../odbc/reference/appendixes/reserved-keywords.md) no [Apêndice C: gramática SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md). O valor **#define** SQL_ODBC_KEYWORDS contém uma lista separada por vírgulas de palavras-chave ODBC.  
  
 Apêndice C: Gramática SQL  
  
 SQL_LIKE_ESCAPE_CLAUSE (ODBC 2,0)  
 Uma cadeia de caracteres: "Y" se a fonte de dados der suporte a um caractere de escape para o caractere de porcentagem (%) e o caractere de sublinhado (_) em um predicado **like** e o driver dá suporte à sintaxe ODBC para definir um caractere de escape de predicado **like** ; "N" caso contrário.  
  
 SQL_MAX_ASYNC_CONCURRENT_STATEMENTS (ODBC 3,0)  
 Um valor SQLUINTEGER que especifica o número máximo de instruções simultâneas ativas no modo assíncrono para o qual o driver pode dar suporte em uma determinada conexão. Se não houver um limite específico ou se o limite for desconhecido, esse valor será zero.  
  
 SQL_MAX_BINARY_LITERAL_LEN (ODBC 2,0)  
 Um valor SQLUINTEGER que especifica o comprimento máximo (número de caracteres hexadecimais, excluindo o prefixo literal e o sufixo retornado por **SQLGetTypeInfo**) de um literal binário em uma instrução SQL. Por exemplo, o literal binário 0xFFAA tem um comprimento de 4. Se não houver nenhum comprimento máximo ou o comprimento for desconhecido, esse valor será definido como zero.  
  
 SQL_MAX_CATALOG_NAME_LEN (ODBC 1,0)  
 Um valor de SQLUSMALLINT que especifica o comprimento máximo de um nome de catálogo na fonte de dados. Se não houver nenhum comprimento máximo ou o comprimento for desconhecido, esse valor será definido como zero.  
  
 Um driver compatível com nível completo FIPS retornará pelo menos 128.  
  
 Este *InfoType* foi renomeado para ODBC 3,0 do ODBC 2,0 *InfoType* SQL_MAX_QUALIFIER_NAME_LEN.  
  
 SQL_MAX_CHAR_LITERAL_LEN (ODBC 2,0)  
 Um valor SQLUINTEGER que especifica o comprimento máximo (número de caracteres, excluindo o prefixo literal e o sufixo retornado por **SQLGetTypeInfo**) de um literal de caractere em uma instrução SQL. Se não houver nenhum comprimento máximo ou o comprimento for desconhecido, esse valor será definido como zero.  
  
 SQL_MAX_COLUMN_NAME_LEN (ODBC 1,0)  
 Um valor de SQLUSMALLINT que especifica o comprimento máximo de um nome de coluna na fonte de dados. Se não houver nenhum comprimento máximo ou o comprimento for desconhecido, esse valor será definido como zero.  
  
 Um driver compatível com nível de entrada FIPS retornará pelo menos 18. Um driver compatível com nível intermediário FIPS retornará pelo menos 128.  
  
 SQL_MAX_COLUMNS_IN_GROUP_BY (ODBC 2,0)  
 Um valor de SQLUSMALLINT que especifica o número máximo de colunas permitido em uma cláusula **Group by** . Se não houver um limite especificado ou o limite for desconhecido, esse valor será definido como zero.  
  
 Um driver compatível com nível de entrada FIPS retornará pelo menos 6. Um driver compatível com nível intermediário FIPS retornará pelo menos 15.  
  
 SQL_MAX_COLUMNS_IN_INDEX (ODBC 2,0)  
 Um valor de SQLUSMALLINT que especifica o número máximo de colunas permitido em um índice. Se não houver um limite especificado ou o limite for desconhecido, esse valor será definido como zero.  
  
 SQL_MAX_COLUMNS_IN_ORDER_BY (ODBC 2,0)  
 Um valor SQLUSMALLINT que especifica o número máximo de colunas permitido em uma cláusula **order by** . Se não houver um limite especificado ou o limite for desconhecido, esse valor será definido como zero.  
  
 Um driver compatível com nível de entrada FIPS retornará pelo menos 6. Um driver compatível com nível intermediário FIPS retornará pelo menos 15.  
  
 SQL_MAX_COLUMNS_IN_SELECT (ODBC 2,0)  
 Um valor de SQLUSMALLINT que especifica o número máximo de colunas permitido em uma lista de seleção. Se não houver um limite especificado ou o limite for desconhecido, esse valor será definido como zero.  
  
 Um driver compatível com nível de entrada FIPS retornará pelo menos 100. Um driver compatível com nível intermediário FIPS retornará pelo menos 250.  
  
 SQL_MAX_COLUMNS_IN_TABLE (ODBC 2,0)  
 Um valor de SQLUSMALLINT que especifica o número máximo de colunas permitido em uma tabela. Se não houver um limite especificado ou o limite for desconhecido, esse valor será definido como zero.  
  
 Um driver compatível com nível de entrada FIPS retornará pelo menos 100. Um driver compatível com nível intermediário FIPS retornará pelo menos 250.  
  
 SQL_MAX_CONCURRENT_ACTIVITIES (ODBC 1,0)  
 Um valor SQLUSMALLINT que especifica o número máximo de instruções ativas às quais o driver pode dar suporte para uma conexão. Uma instrução é definida como ativa se tiver resultados pendentes, com o termo "resultados", que significa linhas de uma operação **Select** ou linhas afetadas por uma operação de **inserção**, **atualização**ou **exclusão** (como uma contagem de linhas) ou se estiver em um estado NEED_DATA. Esse valor pode refletir uma limitação imposta pelo driver ou pela fonte de dados. Se não houver um limite especificado ou o limite for desconhecido, esse valor será definido como zero.  
  
 Este *InfoType* foi renomeado para ODBC 3,0 do ODBC 2,0 *InfoType* SQL_ACTIVE_STATEMENTS.  
  
 SQL_MAX_CURSOR_NAME_LEN (ODBC 1,0)  
 Um valor de SQLUSMALLINT que especifica o comprimento máximo de um nome de cursor na fonte de dados. Se não houver nenhum comprimento máximo ou o comprimento for desconhecido, esse valor será definido como zero.  
  
 Um driver compatível com nível de entrada FIPS retornará pelo menos 18. Um driver compatível com nível intermediário FIPS retornará pelo menos 128.  
  
 SQL_MAX_DRIVER_CONNECTIONS (ODBC 1,0)  
 Um valor de SQLUSMALLINT que especifica o número máximo de conexões ativas às quais o driver pode dar suporte para um ambiente. Esse valor pode refletir uma limitação imposta pelo driver ou pela fonte de dados. Se não houver um limite especificado ou o limite for desconhecido, esse valor será definido como zero.  
  
 Este *InfoType* foi renomeado para ODBC 3,0 do ODBC 2,0 *InfoType* SQL_ACTIVE_CONNECTIONS.  
  
 SQL_MAX_IDENTIFIER_LEN (ODBC 3,0)  
 Um SQLUSMALLINT que indica o tamanho máximo em caracteres que a fonte de dados dá suporte para nomes definidos pelo usuário.  
  
 Um driver compatível com nível de entrada FIPS retornará pelo menos 18. Um driver compatível com nível intermediário FIPS retornará pelo menos 128.  
  
 SQL_MAX_INDEX_SIZE (ODBC 2,0)  
 Um valor SQLUINTEGER que especifica o número máximo de bytes permitidos nos campos combinados de um índice. Se não houver um limite especificado ou o limite for desconhecido, esse valor será definido como zero.  
  
 SQL_MAX_PROCEDURE_NAME_LEN (ODBC 1,0)  
 Um valor de SQLUSMALLINT que especifica o comprimento máximo de um nome de procedimento na fonte de dados. Se não houver nenhum comprimento máximo ou o comprimento for desconhecido, esse valor será definido como zero.  
  
 SQL_MAX_ROW_SIZE (ODBC 2,0)  
 Um valor SQLUINTEGER que especifica o comprimento máximo de uma única linha em uma tabela. Se não houver um limite especificado ou o limite for desconhecido, esse valor será definido como zero.  
  
 Um driver compatível com nível de entrada FIPS retornará pelo menos 2.000. Um driver compatível com nível intermediário FIPS retornará pelo menos 8.000.  
  
 SQL_MAX_ROW_SIZE_INCLUDES_LONG (ODBC 3,0)  
 Uma cadeia de caracteres: "Y" se o tamanho máximo de linha retornado para o SQL_MAX_ROW_SIZE tipo de informação incluir o comprimento de todas as colunas de SQL_LONGVARCHAR e SQL_LONGVARBINARY na linha; "N" caso contrário.  
  
 SQL_MAX_SCHEMA_NAME_LEN (ODBC 1,0)  
 Um valor de SQLUSMALLINT que especifica o comprimento máximo de um nome de esquema na fonte de dados. Se não houver nenhum comprimento máximo ou o comprimento for desconhecido, esse valor será definido como zero.  
  
 Um driver compatível com nível de entrada FIPS retornará pelo menos 18. Um driver compatível com nível intermediário FIPS retornará pelo menos 128.  
  
 Este *InfoType* foi renomeado para ODBC 3,0 do ODBC 2,0 *InfoType* SQL_MAX_OWNER_NAME_LEN.  
  
 SQL_MAX_STATEMENT_LEN (ODBC 2,0)  
 Um valor SQLUINTEGER que especifica o comprimento máximo (número de caracteres, incluindo o espaço em branco) de uma instrução SQL. Se não houver nenhum comprimento máximo ou o comprimento for desconhecido, esse valor será definido como zero.  
  
 SQL_MAX_TABLE_NAME_LEN (ODBC 1,0)  
 Um valor de SQLUSMALLINT que especifica o comprimento máximo de um nome de tabela na fonte de dados. Se não houver nenhum comprimento máximo ou o comprimento for desconhecido, esse valor será definido como zero.  
  
 Um driver compatível com nível de entrada FIPS retornará pelo menos 18. Um driver compatível com nível intermediário FIPS retornará pelo menos 128.  
  
 SQL_MAX_TABLES_IN_SELECT (ODBC 2,0)  
 Um valor SQLUSMALLINT que especifica o número máximo de tabelas permitidas na cláusula **from** de uma instrução **Select** . Se não houver um limite especificado ou o limite for desconhecido, esse valor será definido como zero.  
  
 Um driver compatível com nível de entrada FIPS retornará pelo menos 15. Um driver compatível com nível intermediário FIPS retornará pelo menos 50.  
  
 SQL_MAX_USER_NAME_LEN (ODBC 2,0)  
 Um valor de SQLUSMALLINT que especifica o comprimento máximo de um nome de usuário na fonte de dados. Se não houver nenhum comprimento máximo ou o comprimento for desconhecido, esse valor será definido como zero.  
  
 SQL_MULT_RESULT_SETS (ODBC 1,0)  
 Uma cadeia de caracteres: "Y" se a fonte de dados der suporte a vários conjuntos de resultados, "N" se não tiver.  
  
 Para obter mais informações sobre vários conjuntos de resultados, consulte [vários resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 SQL_MULTIPLE_ACTIVE_TXN (ODBC 1,0)  
 Uma cadeia de caracteres: "Y" se o driver oferecer suporte a mais de uma transação ativa ao mesmo tempo, "N" se apenas uma transação puder estar ativa a qualquer momento.  
  
 As informações retornadas para esse tipo de informação não se aplicam no caso de transações distribuídas.  
  
 SQL_NEED_LONG_DATA_LEN (ODBC 2,0)  
 Uma cadeia de caracteres: "Y" se a fonte de dados precisar do comprimento de um valor de dados longo (o tipo de dados for SQL_LONGVARCHAR, SQL_LONGVARBINARY ou um tipo de dados específico da fonte de dados) antes desse valor ser enviado para a fonte de dados, "N" se não tiver. Para obter mais informações, consulte [função SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) e [função SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
 SQL_NON_NULLABLE_COLUMNS (ODBC 1,0)  
 Um valor SQLUSMALLINT que especifica se a fonte de dados dá suporte a NOT NULL em colunas:  
  
 SQL_NNC_NULL = todas as colunas devem ser anuláveis.  
  
 SQL_NNC_NON_NULL = colunas não podem ser anuláveis. (A fonte de dados dá suporte à restrição de coluna **NOT NULL** em instruções **CREATE TABLE** .)  
  
 Um driver compatível com nível de entrada do SQL-92 retornará SQL_NNC_NON_NULL.  
  
 SQL_NULL_COLLATION (ODBC 2,0)  
 Um valor de SQLUSMALLINT que especifica onde os nulos são classificados em um conjunto de resultados:  
  
 SQL_NC_END = NULLs são classificados no final do conjunto de resultados, independentemente das palavras-chave ASC ou DESC.  
  
 SQL_NC_HIGH = NULLs são classificados na extremidade superior do conjunto de resultados, dependendo das palavras-chave ASC ou DESC.  
  
 SQL_NC_LOW = NULLs são classificados na extremidade inferior do conjunto de resultados, dependendo das palavras-chave ASC ou DESC.  
  
 SQL_NC_START = NULLs são classificados no início do conjunto de resultados, independentemente das palavras-chave ASC ou DESC.  
  
 SQL_NUMERIC_FUNCTIONS (ODBC 1,0)  
 Observação: o tipo de informação foi introduzido no ODBC 1,0; cada bitmask é rotulado com a versão na qual foi introduzido.  
  
 Um bitmask SQLUINTEGER que enumera as funções numéricas escalares com suporte do driver e a fonte de dados associada.  
  
 As seguintes bitmasks são usadas para determinar quais funções numéricas têm suporte:  
  
 SQL_FN_NUM_ABS (ODBC 1.0) SQL_FN_NUM_ACOS (ODBC 1.0) SQL_FN_NUM_ASIN (ODBC 1.0) SQL_FN_NUM_ATAN (ODBC 1.0) SQL_FN_NUM_ATAN2 (ODBC 1.0) SQL_FN_NUM_CEILING (ODBC 1.0) SQL_FN_NUM_COS (ODBC 1.0) SQL_FN_NUM_COT (ODBC 1.0) SQL_FN_NUM_DEGREES (ODBC 2.0) SQL_ FN_NUM_EXP (ODBC 1.0) SQL_FN_NUM_FLOOR (ODBC 1.0) SQL_FN_NUM_LOG (ODBC 1.0) SQL_FN_NUM_LOG10 (ODBC 2.0) SQL_FN_NUM_MOD (ODBC 1.0) SQL_FN_NUM_PI (ODBC 1.0) SQL_FN_NUM_POWER (ODBC 2.0) SQL_FN_NUM_RADIANS (ODBC 2.0) SQL_FN_NUM_RAND (ODBC 1.0) SQL_FN_ NUM_ROUND (ODBC 2.0) SQL_FN_NUM_SIGN (ODBC 1.0) SQL_FN_NUM_SIN (ODBC 1.0) SQL_FN_NUM_SQRT (ODBC 1.0) SQL_FN_NUM_TAN (ODBC 1.0) SQL_FN_NUM_TRUNCATE (ODBC 2,0)  
  
 SQL_ODBC_INTERFACE_CONFORMANCE (ODBC 3,0)  
 Um valor SQLUINTEGER que indica o nível da interface ODBC 3 *. x* com a qual o driver está em conformidade.  
  
 SQL_OIC_CORE: o nível mínimo ao qual todos os drivers ODBC devem estar em conformidade. Esse nível inclui elementos básicos de interface, como funções de conexão, funções para preparar e executar uma instrução SQL, funções de metadados de conjunto de resultados básicas, funções de catálogo básico e assim por diante.  
  
 SQL_OIC_LEVEL1: um nível que inclui a funcionalidade do nível de conformidade dos padrões principais, além de cursores roláveis, indicadores, atualizações e exclusões posicionadas e assim por diante.  
  
 SQL_OIC_LEVEL2: um nível que inclui A funcionalidade de nível de conformidade de padrões de nível 1, além de recursos avançados, como cursores confidenciais; atualizar, excluir e atualizar por indicadores; suporte a procedimentos armazenados; funções de catálogo para chaves primárias e estrangeiras; suporte a vários catálogos; e assim por diante.  
  
 Para obter mais informações, consulte [níveis de conformidade da interface](../../../odbc/reference/develop-app/interface-conformance-levels.md).  
  
 SQL_ODBC_VER (ODBC 1,0)  
 Uma cadeia de caracteres com a versão do ODBC para a qual o Gerenciador de driver está em conformidade. A versão está no formato # #. # #. 0000, em que os dois primeiros dígitos são a versão principal e os próximos dois dígitos são a versão secundária. Isso é implementado somente no Gerenciador de driver.  
  
 SQL_OJ_CAPABILITIES (ODBC 2, 1)  
 Um bitmask SQLUINTEGER que enumera os tipos de junções externas com suporte no driver e na fonte de dados. As seguintes bitmasks são usadas para determinar quais tipos têm suporte:  
  
 SQL_OJ_LEFT = há suporte para junções externas à esquerda.  
  
 SQL_OJ_RIGHT = há suporte para junções externas à direita.  
  
 SQL_OJ_FULL = há suporte para junções externas completas.  
  
 SQL_OJ_NESTED = há suporte para junções externas aninhadas.  
  
 SQL_OJ_NOT_ORDERED = os nomes de coluna na cláusula ON da junção externa não precisam estar na mesma ordem que os respectivos nomes de tabela na cláusula de **junção externa** .  
  
 SQL_OJ_INNER = a tabela interna (a tabela direita em uma junção externa esquerda ou a tabela esquerda em uma junção externa direita) também pode ser usada em uma junção interna. Isso não se aplica a junções externas completas, que não têm uma tabela interna.  
  
 SQL_OJ_ALL_COMPARISON_OPS = o operador de comparação na cláusula ON pode ser qualquer um dos operadores de comparação ODBC. Se esse bit não estiver definido, somente o operador de comparação Equals (=) poderá ser usado em junções externas.  
  
 Se nenhuma dessas opções for retornada como com suporte, não haverá suporte para nenhuma cláusula de junção externa.  
  
 Para obter informações sobre o suporte de operadores de junção relacionais em uma instrução SELECT, conforme definido pelo SQL-92, consulte SQL_SQL92_RELATIONAL_JOIN_OPERATORS.  
  
 SQL_ORDER_BY_COLUMNS_IN_SELECT (ODBC 2,0)  
 Uma cadeia de caracteres: "Y" se as colunas na cláusula **order by** devem estar na lista de seleção; caso contrário, "N".  
  
 SQL_PARAM_ARRAY_ROW_COUNTS (ODBC 3,0)  
 Um SQLUINTEGER enumerando as propriedades do driver em relação à disponibilidade de contagens de linhas em uma execução parametrizada. Tem os seguintes valores:  
  
 SQL_PARC_BATCH = contagens de linhas individuais estão disponíveis para cada conjunto de parâmetros. Isso é conceitualmente equivalente ao driver que gera um lote de instruções SQL, um para cada parâmetro definido na matriz. As informações de erro estendidas podem ser recuperadas usando o campo descritor de SQL_PARAM_STATUS_PTR.  
  
 SQL_PARC_NO_BATCH = há apenas uma contagem de linhas disponível, que é a contagem de linhas cumulativa resultante da execução da instrução para toda a matriz de parâmetros. Isso é conceitualmente equivalente a tratar a instrução junto com a matriz de parâmetros completa como uma unidade atômica. Os erros são tratados da mesma forma como se uma instrução fosse executada.  
  
 SQL_PARAM_ARRAY_SELECTS (ODBC 3,0)  
 Um SQLUINTEGER enumerando as propriedades do driver em relação à disponibilidade dos conjuntos de resultados em uma execução parametrizada. Tem os seguintes valores:  
  
 SQL_PAS_BATCH = há um conjunto de resultados disponível por conjunto de parâmetros. Isso é conceitualmente equivalente ao driver que gera um lote de instruções SQL, um para cada parâmetro definido na matriz.  
  
 SQL_PAS_NO_BATCH = há apenas um conjunto de resultados disponível, que representa o conjunto de resultados cumulativos resultante da execução da instrução para a matriz completa de parâmetros. Isso é conceitualmente equivalente a tratar a instrução junto com a matriz de parâmetros completa como uma unidade atômica.  
  
 SQL_PAS_NO_SELECT = um driver não permite que uma instrução de geração de conjunto de resultados seja executada com uma matriz de parâmetros.  
  
 SQL_PROCEDURE_TERM (ODBC 1,0)  
 Uma cadeia de caracteres com o nome do fornecedor da fonte de dados para um procedimento; por exemplo, "procedimento de banco de dados", "procedimento armazenado", "procedimento", "pacote" ou "consulta armazenada".  
  
 SQL_PROCEDURES (ODBC 1,0)  
 Uma cadeia de caracteres: "Y" se a fonte de dados der suporte a procedimentos e o driver der suporte à sintaxe de invocação de procedimento ODBC; "N" caso contrário.  
  
 SQL_POS_OPERATIONS (ODBC 2,0)  
 Um bitmask SQLINTEGER que enumera as operações de suporte no **SQLSetPos**.  
  
 As seguintes bitmasks são usadas junto com o sinalizador para determinar quais opções têm suporte.  
  
 SQL_POS_POSITION (ODBC 2,0) SQL_POS_REFRESH (ODBC 2,0) SQL_POS_UPDATE (ODBC 2,0) SQL_POS_DELETE (ODBC 2,0) SQL_POS_ADD (ODBC 2,0)  
  
 SQL_QUOTED_IDENTIFIER_CASE (ODBC 2,0)  
 Um valor de SQLUSMALLINT da seguinte maneira:  
  
 SQL_IC_UPPER = identificadores entre aspas no SQL não diferenciam maiúsculas de minúsculas e são armazenados em letras maiúsculas no catálogo do sistema.  
  
 SQL_IC_LOWER = identificadores entre aspas no SQL não diferenciam maiúsculas de minúsculas e são armazenados em letras minúsculas no catálogo do sistema.  
  
 SQL_IC_SENSITIVE = identificadores entre aspas no SQL diferenciam maiúsculas de minúsculas e são armazenados em maiúsculas e minúsculas no catálogo do sistema. (Em um banco de dados compatível com SQL-92, os identificadores entre aspas sempre diferenciam maiúsculas de minúsculas.)  
  
 SQL_IC_MIXED = identificadores entre aspas no SQL não diferenciam maiúsculas de minúsculas e são armazenados em maiúsculas e minúsculas no catálogo do sistema.  
  
 Um driver de nível de entrada do SQL-92 sempre retornará SQL_IC_SENSITIVE.  
  
 SQL_ROW_UPDATES (ODBC 1,0)  
 Uma cadeia de caracteres: "Y" se um cursor misto ou controlado por conjunto de chaves mantém versões de linha ou valores para todas as linhas buscadas e, portanto, pode detectar todas as atualizações que foram feitas em uma linha por qualquer usuário desde que a linha foi buscada pela última vez. (Isso se aplica somente a atualizações, não a exclusões ou inserções.) O driver pode retornar o sinalizador SQL_ROW_UPDATED para a matriz de status de linha quando **SQLFetchScroll** é chamado. Caso contrário, "N".  
  
 SQL_SCHEMA_TERM (ODBC 1,0)  
 Uma cadeia de caracteres com o nome do fornecedor de fonte de dados para um esquema; por exemplo, "proprietário", "ID de autorização" ou "esquema".  
  
 A cadeia de caracteres pode ser retornada no caso superior, inferior ou misto.  
  
 Um driver compatível com nível de entrada do SQL-92 sempre retornará "Schema".  
  
 Este *InfoType* foi renomeado para ODBC 3,0 do ODBC 2,0 *InfoType* SQL_OWNER_TERM.  
  
 SQL_SCHEMA_USAGE (ODBC 2,0)  
 Um bitmask SQLUINTEGER que enumera as instruções nas quais os esquemas podem ser usados:  
  
 SQL_SU_DML_STATEMENTS = há suporte para esquemas em todas as instruções de linguagem de manipulação de dados: **selecionar**, **Inserir**, **Atualizar**, **excluir**e, se houver suporte, **Selecione para atualizar** e posicionar as instruções UPDATE e Delete.  
  
 SQL_SU_PROCEDURE_INVOCATION = há suporte para esquemas na instrução de invocação de procedimento ODBC.  
  
 SQL_SU_TABLE_DEFINITION = há suporte para esquemas em todas as instruções de definição de tabela: **CREATE TABLE**, **criar exibição**, **alterar tabela**, **remover tabela**e **descartar exibição**.  
  
 SQL_SU_INDEX_DEFINITION = há suporte para esquemas em todas as instruções de definição de índice: **CREATE INDEX** e **drop index**.  
  
 SQL_SU_PRIVILEGE_DEFINITION = há suporte para esquemas em todas as instruções de definição de privilégio: **Grant** e **REVOKE**.  
  
 Um driver compatível com nível de entrada do SQL-92 sempre retornará as opções SQL_SU_DML_STATEMENTS, SQL_SU_TABLE_DEFINITION e SQL_SU_PRIVILEGE_DEFINITION, como com suporte.  
  
 Este *InfoType* foi renomeado para ODBC 3,0 do ODBC 2,0 *InfoType* SQL_OWNER_USAGE.  
  
 SQL_SCROLL_OPTIONS (ODBC 1,0)  
 Observação: o tipo de informação foi introduzido no ODBC 1,0; cada bitmask é rotulado com a versão na qual foi introduzido.  
  
 Um bitmask SQLUINTEGER que enumera as opções de rolagem com suporte para cursores roláveis.  
  
 As seguintes bitmasks são usadas para determinar quais opções têm suporte:  
  
 SQL_SO_FORWARD_ONLY = o cursor só rola para frente. (ODBC 1,0)  
  
 SQL_SO_STATIC = os dados no conjunto de resultados são estáticos. (ODBC 2,0)  
  
 SQL_SO_KEYSET_DRIVEN = o driver salva e usa as chaves para cada linha no conjunto de resultados. (ODBC 1,0)  
  
 SQL_SO_DYNAMIC = o driver mantém as chaves para cada linha no conjunto de linhas (o tamanho do conjunto de chaves é o mesmo que o tamanho do Rowset). (ODBC 1,0)  
  
 SQL_SO_MIXED = o driver mantém as chaves para cada linha no conjunto de chaves, e o tamanho do conjuntos de chaves é maior do que o tamanho do Rowset. O cursor é orientado por conjunto de chaves dentro do conjunto de chaves e dinâmico fora do conjunto de chaves. (ODBC 1,0)  
  
 Para obter informações sobre cursores roláveis, consulte [cursores roláveis](../../../odbc/reference/develop-app/scrollable-cursors.md).  
  
 SQL_SEARCH_PATTERN_ESCAPE (ODBC 1,0)  
 Uma cadeia de caracteres que especifica o que o driver dá suporte como um caractere de escape que permite o uso dos metacaracteres de correspondência de padrões de sublinhado (_) e sinal de porcentagem (%) como caracteres válidos em padrões de pesquisa. Esse caractere de escape se aplica somente aos argumentos da função de catálogo que dão suporte a cadeias de caracteres de pesquisa. Se essa cadeia de caracteres estiver vazia, o driver não oferecerá suporte a um caractere de escape de padrão de pesquisa.  
  
 Como esse tipo de informação não indica o suporte geral do caractere de escape no predicado **like** , o SQL-92 não inclui os requisitos para essa cadeia de caracteres.  
  
 Este *InfoType* é limitado a funções de catálogo. Para obter uma descrição do uso do caractere de escape em cadeias de caracteres de padrão de pesquisa, consulte [argumentos de valor de padrão](../../../odbc/reference/develop-app/pattern-value-arguments.md).  
  
 SQL_SERVER_NAME (ODBC 1,0)  
 Uma cadeia de caracteres com o nome do servidor específico da fonte de dados; útil quando um nome de fonte de dados é usado durante **SQLConnect**, **SQLDriverConnect**e **SQLBrowseConnect**.  
  
 SQL_SPECIAL_CHARACTERS (ODBC 2,0)  
 Uma cadeia de caracteres que contém todos os caracteres especiais (ou seja, todos os caracteres, exceto a até z, A a Z, 0 a 9 e sublinhado) que podem ser usados em um nome de identificador, como um nome de tabela, nome de coluna ou nome de índice, na fonte de dados. Por exemplo, "# $ ^". Se um identificador contiver um ou mais desses caracteres, o identificador deverá ser um identificador delimitado.  
  
 SQL_SQL_CONFORMANCE (ODBC 3,0)  
 Um valor SQLUINTEGER que indica o nível de SQL-92 ao qual o driver dá suporte:  
  
 SQL_SC_SQL92_ENTRY = em conformidade com SQL-92 de nível de entrada.  
  
 SQL_SC_FIPS127_2_TRANSITIONAL = compatível com nível de transição FIPS 127-2.  
  
 SQL_SC_SQL92_FULL = em conformidade com SQL-92 de nível completo.  
  
 SQL_SC_ SQL92_INTERMEDIATE = em conformidade com SQL-92 de nível intermediário.  
  
 SQL_SQL92_DATETIME_FUNCTIONS (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera as funções escalares DateTime com suporte pelo driver e a fonte de dados associada, conforme definido em SQL-92.  
  
 As seguintes bitmasks são usadas para determinar quais funções DateTime têm suporte:  
  
 SQL_SDF_CURRENT_DATESQL_SDF_CURRENT_TIMESQL_SDF_CURRENT_TIMESTAMP  
  
 SQL_SQL92_FOREIGN_KEY_DELETE_RULE (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera as regras com suporte para uma chave estrangeira em uma instrução **delete** , conforme definido em SQL-92.  
  
 As seguintes bitmasks são usadas para determinar quais cláusulas são compatíveis com a fonte de dados:  
  
 SQL_SFKD_CASCADESQL_SFKD_NO_ACTIONSQL_SFKD_SET_DEFAULTSQL_SFKD_SET_NULL  
  
 Um driver compatível com nível de transição FIPS sempre retornará todas essas opções como com suporte.  
  
 SQL_SQL92_FOREIGN_KEY_UPDATE_RULE (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera as regras com suporte para uma chave estrangeira em uma instrução **Update** , conforme definido em SQL-92.  
  
 As seguintes bitmasks são usadas para determinar quais cláusulas são compatíveis com a fonte de dados:  
  
 SQL_SFKU_CASCADESQL_SFKU_NO_ACTIONSQL_SFKU_SET_DEFAULTSQL_SFKU_SET_NULL  
  
 Um driver compatível com nível completo do SQL-92 sempre retornará todas essas opções como com suporte.  
  
 SQL_SQL92_GRANT (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera as cláusulas com suporte na instrução **Grant** , conforme definido em SQL-92.  
  
 O nível de conformidade do SQL-92 ou FIPS no qual esse recurso deve ser suportado é mostrado entre parênteses ao lado de cada bitmask.  
  
 As seguintes bitmasks são usadas para determinar quais cláusulas são compatíveis com a fonte de dados:  
  
 SQL_SG_DELETE_TABLE (nível de entrada) SQL_SG_INSERT_COLUMN (nível intermediário) SQL_SG_INSERT_TABLE (nível de entrada) SQL_SG_REFERENCES_TABLE (nível de entrada) SQL_SG_REFERENCES_COLUMN (nível de entrada) SQL_SG_SELECT_TABLE (nível de entrada) SQL_SG_UPDATE_COLUMN ( Nível de entrada) SQL_SG_UPDATE_TABLE (nível de entrada) SQL_SG_USAGE_ON_DOMAIN (nível de transição FIPS) SQL_SG_USAGE_ON_CHARACTER_SET (nível de transição FIPS) SQL_SG_USAGE_ON_COLLATION (nível de transição FIPS) SQL_SG_USAGE_ON_TRANSLATION (FIPS Nível de transição) SQL_SG_WITH_GRANT_OPTION (nível de entrada)  
  
 SQL_SQL92_NUMERIC_VALUE_FUNCTIONS (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera as funções escalares de valor numérico que são compatíveis com o driver e a fonte de dados associada, conforme definido em SQL-92.  
  
 As seguintes bitmasks são usadas para determinar quais funções numéricas têm suporte:  
  
 SQL_SNVF_BIT_LENGTHSQL_SNVF_CHAR_LENGTHSQL_SNVF_CHARACTER_LENGTHSQL_SNVF_EXTRACTSQL_SNVF_OCTET_LENGTHSQL_SNVF_POSITION  
  
 SQL_SQL92_PREDICATES (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera os predicados com suporte em uma instrução **Select** , conforme definido em SQL-92.  
  
 O nível de conformidade do SQL-92 ou FIPS no qual esse recurso deve ser suportado é mostrado entre parênteses ao lado de cada bitmask.  
  
 As seguintes bitmasks são usadas para determinar quais opções são suportadas pela fonte de dados:  
  
 SQL_SP_BETWEEN (nível de entrada) SQL_SP_COMPARISON (nível de entrada) SQL_SP_EXISTS (nível de entrada) SQL_SP_IN (nível de entrada) SQL_SP_ISNOTNULL (nível de entrada) SQL_SP_ISNULL (nível de entrada) SQL_SP_LIKE (nível de entrada) SQL_SP_MATCH_FULL (nível completo) SQL_SP_MATCH_PARTIAL (Nível completo) SQL_SP_MATCH_UNIQUE_FULL (nível completo) SQL_SP_MATCH_UNIQUE_PARTIAL (nível completo) SQL_SP_OVERLAPS (nível de transição FIPS) SQL_SP_QUANTIFIED_COMPARISON (nível de entrada) SQL_SP_UNIQUE (nível de entrada)  
  
 SQL_SQL92_RELATIONAL_JOIN_OPERATORS (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera os operadores de junção relacionais com suporte em uma instrução **Select** , conforme definido em SQL-92.  
  
 O nível de conformidade do SQL-92 ou FIPS no qual esse recurso deve ser suportado é mostrado entre parênteses ao lado de cada bitmask.  
  
 As seguintes bitmasks são usadas para determinar quais opções são suportadas pela fonte de dados:  
  
 SQL_SRJO_CORRESPONDING_CLAUSE (nível intermediário) SQL_SRJO_CROSS_JOIN (nível completo) SQL_SRJO_EXCEPT_JOIN (nível intermediário) SQL_SRJO_FULL_OUTER_JOIN (nível intermediário) SQL_SRJO_INNER_JOIN (nível de transição FIPS) SQL_SRJO_INTERSECT_JOIN (Nível intermediário) SQL_SRJO_LEFT_OUTER_JOIN (nível de transição FIPS) SQL_SRJO_NATURAL_JOIN (nível de transição FIPS) SQL_SRJO_RIGHT_OUTER_JOIN (nível de transição FIPS) SQL_SRJO_UNION_JOIN (nível completo)  
  
 SQL_SRJO_INNER_JOIN indica suporte para a sintaxe de **junção interna** , não para a funcionalidade de junção interna. O suporte para a sintaxe de **junção interna** é a transição FIPS, enquanto o suporte para a funcionalidade de junção interna é a **entrada**.  
  
 SQL_SQL92_REVOKE (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera as cláusulas com suporte na instrução **REVOKE** , conforme definido em SQL-92, com suporte da fonte de dados.  
  
 O nível de conformidade do SQL-92 ou FIPS no qual esse recurso deve ser suportado é mostrado entre parênteses ao lado de cada bitmask.  
  
 As seguintes bitmasks são usadas para determinar quais cláusulas são compatíveis com a fonte de dados:  
  
 SQL_SR_CASCADE (nível de transição FIPS) SQL_SR_DELETE_TABLE (nível de entrada) SQL_SR_GRANT_OPTION_FOR (nível intermediário) SQL_SR_INSERT_COLUMN (nível intermediário) SQL_SR_INSERT_TABLE (nível de entrada) SQL_SR_REFERENCES_COLUMN (nível de entrada) SQL_SR_ REFERENCES_TABLE (nível de entrada) SQL_SR_RESTRICT (nível de transição FIPS) SQL_SR_SELECT_TABLE (nível de entrada) SQL_SR_UPDATE_COLUMN (nível de entrada) SQL_SR_UPDATE_TABLE (nível de entrada) SQL_SR_USAGE_ON_DOMAIN (nível de transição FIPS) SQL_SR_USAGE_ON_ CHARACTER_SET (nível de transição FIPS) SQL_SR_USAGE_ON_COLLATION (nível de transição FIPS) SQL_SR_USAGE_ON_TRANSLATION (nível de transição FIPS)  
  
 SQL_SQL92_ROW_VALUE_CONSTRUCTOR (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera as expressões de construtor de valor de linha com suporte em uma instrução **Select** , conforme definido em SQL-92. As seguintes bitmasks são usadas para determinar quais opções são suportadas pela fonte de dados:  
  
 SQL_SRVC_VALUE_EXPRESSION SQL_SRVC_NULL SQL_SRVC_DEFAULT SQL_SRVC_ROW_SUBQUERY  
  
 SQL_SQL92_STRING_FUNCTIONS (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera as funções escalares de cadeia de caracteres com suporte pelo driver e a fonte de dados associada, conforme definido em SQL-92.  
  
 As seguintes bitmasks são usadas para determinar quais funções de cadeia de caracteres têm suporte:  
  
 SQL_SSF_CONVERTSQL_SSF_LOWERSQL_SSF_UPPERSQL_SSF_SUBSTRINGSQL_SSF_TRANSLATESQL_SSF_TRIM_BOTHSQL_SSF_TRIM_LEADINGSQL_SSF_TRIM_TRAILING  
  
 SQL_SQL92_VALUE_EXPRESSIONS (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera as expressões de valor com suporte, conforme definido em SQL-92.  
  
 O nível de conformidade do SQL-92 ou FIPS no qual esse recurso deve ser suportado é mostrado entre parênteses ao lado de cada bitmask.  
  
 As seguintes bitmasks são usadas para determinar quais opções são suportadas pela fonte de dados:  
  
 SQL_SVE_CASE (nível intermediário) SQL_SVE_CAST (nível de transição FIPS) SQL_SVE_COALESCE (nível intermediário) SQL_SVE_NULLIF (nível intermediário)  
  
 SQL_STANDARD_CLI_CONFORMANCE (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera o padrão da CLI ou padrões para os quais o driver está em conformidade. As seguintes bitmasks são usadas para determinar a quais níveis o driver está em conformidade:  
  
 SQL_SCC_XOPEN_CLI_VERSION1: o driver está em conformidade com a CLI do grupo aberto versão 1.  
  
 SQL_SCC_ISO92_CLI: o driver está em conformidade com a CLI ISO 92.  
  
 SQL_STATIC_CURSOR_ATTRIBUTES1 (ODBC 3,0)  
 Um bitmask SQLUINTEGER que descreve os atributos de um cursor estático que são suportados pelo driver. Essa bitmask contém o primeiro subconjunto de atributos; para o segundo subconjunto, consulte SQL_STATIC_CURSOR_ATTRIBUTES2.  
  
 As seguintes bitmasks são usadas para determinar quais atributos têm suporte:  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_ UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 Para obter descrições desses bitmasks, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (e substitua "cursor estático" por "cursor dinâmico" nas descrições).  
  
 Um driver compatível com nível intermediário do SQL-92 geralmente retorna as opções SQL_CA1_NEXT, SQL_CA1_ABSOLUTE e SQL_CA1_RELATIVE, como com suporte, porque o driver dá suporte a cursores roláveis por meio da instrução SQL FETCH inserida. Como isso não determina diretamente o suporte do SQL subjacente, no entanto, os cursores roláveis podem não ter suporte, mesmo para um driver compatível com nível intermediário do SQL-92.  
  
 SQL_STATIC_CURSOR_ATTRIBUTES2 (ODBC 3,0)  
 Um bitmask SQLUINTEGER que descreve os atributos de um cursor estático que são suportados pelo driver. Essa bitmask contém o segundo subconjunto de atributos; para o primeiro subconjunto, consulte SQL_STATIC_CURSOR_ATTRIBUTES1.  
  
 As seguintes bitmasks são usadas para determinar quais atributos têm suporte:  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_ CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_ SIMULATE_UNIQUE  
  
 Para obter descrições desses bitmasks, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES2 (e substitua "cursor estático" por "cursor dinâmico" nas descrições).  
  
 SQL_STRING_FUNCTIONS (ODBC 1,0)  
 Observação: o tipo de informação foi introduzido no ODBC 1,0; cada bitmask é rotulado com a versão na qual foi introduzido.  
  
 Um bitmask SQLUINTEGER que enumera as funções de cadeia de caracteres escalares com suporte do driver e a fonte de dados associada.  
  
 As seguintes bitmasks são usadas para determinar quais funções de cadeia de caracteres têm suporte:  
  
 SQL_FN_STR_ASCII (ODBC 1.0) SQL_FN_STR_BIT_LENGTH (ODBC 3.0) SQL_FN_STR_CHAR (ODBC 1.0) SQL_FN_STR_CHAR_LENGTH (ODBC 3.0) SQL_FN_STR_CHARACTER_LENGTH (ODBC 3.0) SQL_FN_STR_CONCAT (ODBC 1.0) SQL_FN_STR_DIFFERENCE (ODBC 2.0) SQL_FN_STR_INSERT (ODBC 1.0) SQL_FN_STR_LCASE (ODBC 1.0) SQL_FN_STR_LEFT (ODBC 1.0) SQL_FN_STR_LENGTH (ODBC 1.0) SQL_FN_STR_LOCATE (ODBC 1,0) SQL_FN_STR_LTRIM (ODBC 1,0) SQL_FN_STR_OCTET_LENGTH (ODBC 3,0) SQL_FN_STR_POSITION (ODBC 3.0) SQL_FN_STR_REPEAT (ODBC 1.0) SQL_FN_ STR_REPLACE (ODBC 1.0) SQL_FN_STR_RIGHT (ODBC 1.0) SQL_FN_STR_RTRIM (ODBC 1.0) SQL_FN_STR_SOUNDEX (ODBC 2.0) SQL_FN_STR_SPACE (ODBC 2.0) SQL_FN_STR_SUBSTRING (ODBC 1.0) SQL_FN_STR_UCASE (ODBC 1,0)  
  
 Se um aplicativo puder chamar a função **Localizar** escalar com os argumentos *string_exp1*, *string_exp2*e *Iniciar* , o driver retornará o SQL_FN_STR_LOCATE bitmask. Se um aplicativo puder chamar a função localizar escalar apenas com os argumentos *string_exp1* e *string_exp2* , o driver retornará o SQL_FN_STR_LOCATE_2 bitmask. Os drivers que dão suporte total à função **Localizar** escalar retornam ambos os bitmasks.  
  
 (Para obter mais informações, consulte [funções de cadeia de caracteres](../../../odbc/reference/appendixes/string-functions.md) no apêndice e, "funções escalares".)  
  
 SQL_SUBQUERIES (ODBC 2,0)  
 Um bitmask SQLUINTEGER que enumera os predicados que dão suporte a subconsultas:  
  
 SQL_SQ_CORRELATED_SUBQUERIESSQL_SQ_COMPARISONSQL_SQ_EXISTSSQL_SQ_INSQL_SQ_QUANTIFIED  
  
 O bitmask SQL_SQ_CORRELATED_SUBQUERIES indica que todos os predicados que dão suporte a subconsultas dão suporte a Subconsultas correlacionadas.  
  
 Um driver compatível com nível de entrada do SQL-92 sempre retornará um bitmask no qual todos esses bits estão definidos.  
  
 SQL_SYSTEM_FUNCTIONS (ODBC 1,0)  
 Um bitmask SQLUINTEGER que enumera as funções do sistema escalar com suporte do driver e a fonte de dados associada.  
  
 As seguintes bitmasks são usadas para determinar quais funções do sistema têm suporte:  
  
 SQL_FN_SYS_DBNAMESQL_FN_SYS_IFNULLSQL_FN_SYS_USERNAME  
  
 SQL_TABLE_TERM (ODBC 1,0)  
 Uma cadeia de caracteres com o nome do fornecedor da fonte de dados para uma tabela; por exemplo, "tabela" ou "arquivo".  
  
 Essa cadeia de caracteres pode estar no caso superior, inferior ou misto.  
  
 Um driver compatível com nível de entrada do SQL-92 sempre retornará "tabela".  
  
 SQL_TIMEDATE_ADD_INTERVALS (ODBC 2,0)  
 Um bitmask SQLUINTEGER que enumera os intervalos de carimbo de data/hora com suporte do driver e a fonte de dados associada para a função escalar TIMESTAMPADD.  
  
 As seguintes bitmasks são usadas para determinar quais intervalos têm suporte:  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 Um driver compatível com nível de transição FIPS sempre retornará um bitmask no qual todos esses bits estão definidos.  
  
 SQL_TIMEDATE_DIFF_INTERVALS (ODBC 2,0)  
 Um bitmask SQLUINTEGER que enumera os intervalos de carimbo de data/hora com suporte do driver e a fonte de dados associada para a função escalar TIMESTAMPDIFF.  
  
 As seguintes bitmasks são usadas para determinar quais intervalos têm suporte:  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 Um driver compatível com nível de transição FIPS sempre retornará um bitmask no qual todos esses bits estão definidos.  
  
 SQL_TIMEDATE_FUNCTIONS (ODBC 1,0)  
 Observação: o tipo de informação foi introduzido no ODBC 1,0; cada bitmask é rotulado com a versão na qual foi introduzido.  
  
 Um bitmask SQLUINTEGER que enumera as funções de data e hora escalares com suporte no driver e na fonte de dados associada.  
  
 As seguintes bitmasks são usadas para determinar quais funções de data e hora têm suporte:  
  
 SQL_FN_TD_CURRENT_DATE ODBC 3.0) SQL_FN_TD_CURRENT_TIME (ODBC 3.0) SQL_FN_TD_CURRENT_TIMESTAMP (ODBC 3.0) SQL_FN_TD_CURDATE (ODBC 1.0) SQL_FN_TD_CURTIME (ODBC 1,0) SQL_FN_TD_DAYNAME (ODBC 2.0) SQL_FN_TD_DAYOFMONTH (ODBC 1.0) SQL_FN_TD_DAYOFWEEK ( ODBC 1.0) SQL_FN_TD_DAYOFYEAR (ODBC 1,0) SQL_FN_TD_EXTRACT (ODBC 3.0) SQL_FN_TD_HOUR (ODBC 1.0) SQL_FN_TD_MINUTE (ODBC 1.0) SQL_FN_TD_MONTH (ODBC 1.0) SQL_FN_TD_MONTHNAME (ODBC 2.0) SQL_FN_TD_NOW (ODBC 1.0) SQL_FN_TD_QUARTER (ODBC 1.0) SQL_FN_TD_ SEGUNDO (ODBC 1.0) SQL_FN_TD_TIMESTAMPADD (ODBC 2.0) SQL_FN_TD_TIMESTAMPDIFF (ODBC 2.0) SQL_FN_TD_WEEK (ODBC 1.0) SQL_FN_TD_YEAR (ODBC 1,0)  
  
 SQL_TXN_CAPABLE (ODBC 1,0)  
 Observação: o tipo de informação foi introduzido no ODBC 1,0; cada valor de retorno é rotulado com a versão na qual ele foi introduzido.  
  
 Um valor de SQLUSMALLINT que descreve o suporte de transação no driver ou na fonte de dados:  
  
 SQL_TC_NONE = transações sem suporte. (ODBC 1,0)  
  
 SQL_TC_DML = as transações podem conter apenas instruções DML (linguagem de manipulação de dados) (**Select**, **Insert**, **Update**e **delete**). As instruções DDL (linguagem de definição de dados) encontradas em uma transação causam um erro. (ODBC 1,0)  
  
 SQL_TC_DDL_COMMIT = as transações podem conter apenas instruções DML. As instruções DDL (**CREATE TABLE**, **drop index**e assim por diante) encontradas em uma transação fazem com que a transação seja confirmada. (ODBC 2,0)  
  
 SQL_TC_DDL_IGNORE = as transações podem conter apenas instruções DML. As instruções DDL encontradas em uma transação são ignoradas. (ODBC 2,0)  
  
 SQL_TC_ALL = as transações podem conter instruções DDL e instruções DML em qualquer ordem. (ODBC 1,0)  
  
 (Como o suporte a transações é obrigatório no SQL-92, um driver compatível com SQL-92 [qualquer nível] nunca retornará SQL_TC_NONE.)  
  
 SQL_TXN_ISOLATION_OPTION (ODBC 1,0)  
 Um bitmask SQLUINTEGER que enumera os níveis de isolamento da transação disponíveis do driver ou da fonte de dados.  
  
 As seguintes bitmasks são usadas junto com o sinalizador para determinar quais opções têm suporte:  
  
 SQL_TXN_READ_UNCOMMITTEDSQL_TXN_READ_COMMITTEDSQL_TXN_REPEATABLE_READSQL_TXN_SERIALIZABLE  
  
 Para obter descrições desses níveis de isolamento, consulte a descrição de SQL_DEFAULT_TXN_ISOLATION.  
  
 Para definir o nível de isolamento da transação, um aplicativo chama **SQLSetConnectAttr** para definir o atributo SQL_ATTR_TXN_ISOLATION. Para obter mais informações, consulte [função SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 Um driver de nível de entrada do SQL-92 sempre retornará SQL_TXN_SERIALIZABLE como com suporte. Um driver compatível com nível de transição FIPS sempre retornará todas essas opções como com suporte.  
  
 SQL_UNION (ODBC 2,0)  
 Um bitmask SQLUINTEGER que enumera o suporte para a cláusula **Union** :  
  
 SQL_U_UNION = a fonte de dados dá suporte à cláusula **Union** .  
  
 SQL_U_UNION_ALL = a fonte de dados dá suporte à palavra-chave **All** na cláusula **Union** . (**SQLGetInfo** retorna SQL_U_UNION e SQL_U_UNION_ALL nesse caso.)  
  
 Um driver de nível de entrada do SQL-92 sempre retornará essas duas opções como com suporte.  
  
 SQL_USER_NAME (ODBC 1,0)  
 Uma cadeia de caracteres com o nome usado em um determinado banco de dados, que pode ser diferente do nome de logon.  
  
 SQL_XOPEN_CLI_YEAR (ODBC 3,0)  
 Uma cadeia de caracteres que indica o ano de publicação da especificação de grupo aberto com a qual a versão do Gerenciador de driver ODBC está totalmente em conformidade.  
  
 SQL_ACCESSIBLE_PROCEDURES (ODBC 1,0)  
 Uma cadeia de caracteres: "Y" se o usuário puder executar todos os procedimentos retornados por **SQLProcedures**; "N" se pode haver procedimentos retornados que o usuário não pode executar.  
  
 SQL_ACCESSIBLE_TABLES (ODBC 1,0)  
 Uma cadeia de caracteres: "Y" se o usuário for garantido, **selecione** privilégios para todas as tabelas retornadas por **SQLTables**; "N" se pode haver tabelas retornadas que o usuário não pode acessar.  
  
 SQL_ACTIVE_ENVIRONMENTS (ODBC 3,0)  
 Um valor de SQLUSMALLINT que especifica o número máximo de ambientes ativos aos quais o driver pode dar suporte. Se não houver um limite especificado ou o limite for desconhecido, esse valor será definido como zero.  
  
 SQL_AGGREGATE_FUNCTIONS (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera o suporte para funções de agregação:  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 Um driver de nível de entrada do SQL-92 sempre retornará todas essas opções como com suporte.  
  
 SQL_ALTER_DOMAIN (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera as cláusulas na instrução **ALTER Domain** , conforme definido em SQL-92, com suporte da fonte de dados. Um driver em conformidade com nível completo do SQL-92 sempre retornará todas as bitmasks. Um valor de retorno de "0" significa que não há suporte para a instrução **ALTER Domain** .  
  
 O nível de conformidade do SQL-92 ou FIPS no qual esse recurso deve ser suportado é mostrado entre parênteses ao lado de cada bitmask.  
  
 As seguintes bitmasks são usadas para determinar quais cláusulas têm suporte:  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT = há suporte para a adição de uma restrição de domínio (nível completo)  
  
 SQL_AD_ADD_DOMAIN_DEFAULT = \<alter Domain> \<definir a cláusula default do domínio> tem suporte (nível completo)  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION = \<cláusula de definição de nome de restrição> tem suporte para a restrição de domínio de nomenclatura (nível intermediário)  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT = \<há suporte para a cláusula DROP DOMAIN Constraint> (nível completo)  
  
 SQL_AD_DROP_DOMAIN_DEFAULT = \<alter Domain> \<a cláusula default do domínio de remoção> tem suporte (nível completo)  
  
 Os bits a seguir especificam \<os atributos de restrição \<com suporte> se adicionar restrição de domínio> tiver suporte (o bit de SQL_AD_ADD_DOMAIN_CONSTRAINT estiver definido):  
  
 SQL_AD_ADD_CONSTRAINT_DEFERRABLE (nível completo) SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE (nível completo) SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE (nível completo)  
  
 SQL_ALTER_TABLE (ODBC 2,0)  
 Um bitmask SQLUINTEGER que enumera as cláusulas na instrução **ALTER TABLE** com suporte da fonte de dados.  
  
 O nível de conformidade do SQL-92 ou FIPS no qual esse recurso deve ser suportado é mostrado entre parênteses ao lado de cada bitmask.  
  
 As seguintes bitmasks são usadas para determinar quais cláusulas têm suporte:  
  
 SQL_AT_ADD_COLUMN_COLLATION = \<há suporte para a cláusula ADD Column>, com instalações para especificar o agrupamento de colunas (nível completo) (ODBC 3,0)  
  
 SQL_AT_ADD_COLUMN_DEFAULT = \<há suporte para a cláusula adicionar coluna>, com instalações para especificar padrões de coluna (nível de transição FIPS) (ODBC 3,0)  
  
 SQL_AT_ADD_COLUMN_SINGLE = \<há suporte para a adição de coluna> (nível de transição FIPS) (ODBC 3,0)  
  
 SQL_AT_ADD_CONSTRAINT = \<há suporte para a cláusula ADD Column>, com instalações para especificar restrições de coluna (nível de transição FIPS) (ODBC 3,0)  
  
 SQL_AT_ADD_TABLE_CONSTRAINT = \<há suporte para a cláusula adicionar restrição de tabela> (nível de transição FIPS) (ODBC 3,0)  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION = \<definição de nome de restrição> tem suporte para a nomenclatura de restrições de coluna e tabela (nível intermediário) (ODBC 3,0)  
  
 SQL_AT_DROP_COLUMN_CASCADE = \<DROP COLUMN> Cascade tem suporte (nível de transição FIPS) (ODBC 3,0)  
  
 SQL_AT_DROP_COLUMN_DEFAULT = \<alter Column> \<cláusula de descartar coluna padrão> tem suporte (nível intermediário) (ODBC 3,0)  
  
 SQL_AT_DROP_COLUMN_RESTRICT = \<a coluna drop> restrict é suportada (nível de transição FIPS) (ODBC 3,0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3,0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT = \<a coluna drop> restrict é suportada (nível de transição FIPS) (ODBC 3,0)  
  
 SQL_AT_SET_COLUMN_DEFAULT = \<alter Column> \<definir a cláusula default da coluna> tem suporte (nível intermediário) (ODBC 3,0)  
  
 Os bits a seguir especificam \<os atributos de restrição de suporte> se a especificação de restrições de coluna ou tabela for suportada (o bit de SQL_AT_ADD_CONSTRAINT está definido):  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED (nível completo) (ODBC 3.0) SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE (nível completo) (ODBC 3.0) SQL_AT_CONSTRAINT_DEFERRABLE (nível completo) (ODBC 3.0) SQL_AT_CONSTRAINT_NON_DEFERRABLE (nível completo) (ODBC 3,0)  
  
 SQL_ASYNC_MODE (ODBC 3,0)  
 Um valor SQLUINTEGER que indica o nível de suporte assíncrono no driver:  
  
 SQL_AM_CONNECTION = há suporte para a execução assíncrona no nível de conexão. Qualquer um dos identificadores de instrução associados a um determinado identificador de conexão está no modo assíncrono ou todos estão no modo síncrono. Um identificador de instrução em uma conexão não pode estar no modo assíncrono, enquanto outro identificador de instrução na mesma conexão está no modo síncrono e vice-versa.  
  
 SQL_AM_STATEMENT = há suporte para a execução assíncrona em nível de instrução. Alguns identificadores de instrução associados a um identificador de conexão podem estar no modo assíncrono, enquanto outros identificadores de instrução na mesma conexão estão no modo síncrono.  
  
 Não há suporte para SQL_AM_NONE = modo assíncrono.  
  
 SQL_BATCH_ROW_COUNT (ODBC 3,0)  
 Um bitmask SQLUINTEGER que enumera o comportamento do driver em relação à disponibilidade de contagens de linhas. As seguintes bitmasks são usadas junto com o tipo de informação:  
  
 SQL_BRC_ROLLED_UP = contagens de linha para instruções de inserção, exclusão ou atualização consecutivas são acumuladas em uma. Se esse bit não estiver definido, as contagens de linhas estarão disponíveis para cada instrução.  
  
 SQL_BRC_PROCEDURES = contagens de linhas, se houver, estarão disponíveis quando um lote for executado em um procedimento armazenado. Se as contagens de linhas estiverem disponíveis, elas poderão ser acumuladas ou individualmente disponíveis, dependendo do SQL_BRC_ROLLED_UP bit.  
  
 SQL_BRC_EXPLICIT = contagens de linhas, se houver, estarão disponíveis quando um lote for executado diretamente chamando **SQLExecute** ou **SQLExecDirect**. Se as contagens de linhas estiverem disponíveis, elas poderão ser acumuladas ou individualmente disponíveis, dependendo do SQL_BRC_ROLLED_UP bit.  
  
## <a name="example"></a>Exemplo  
 **SQLGetInfo** retorna listas de opções com suporte como um BITMASK SQLUINTEGER em **InfoValuePtr*. O bitmask para cada opção é usado junto com o sinalizador para determinar se há suporte para a opção.  
  
 Por exemplo, um aplicativo pode usar o código a seguir para determinar se a função escalar de subcadeia de caracteres é suportada pelo driver associado à conexão.  
  
 Para obter outro exemplo de como usar **SQLGetInfo**, consulte [função SQLTables](../../../odbc/reference/syntax/sqltables-function.md).  
  
```cpp  
SQLUINTEGER fFuncs;  
  
SQLGetInfo(hdbc,   
           SQL_STRING_FUNCTIONS,  
           (SQLPOINTER)&fFuncs,  
           sizeof(fFuncs),  
           NULL);  
  
// SUBSTRING supported  
if (fFuncs & SQL_FN_STR_SUBSTRING)   
   ;   // do something  
  
// SUBSTRING not supported  
else  
   ;   // do something else  
```  
  
## <a name="related-functions"></a>Funções relacionadas  
 Retornando a configuração de um atributo de conexão  
 [Função SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
 Determinando se um driver dá suporte a uma função  
 [Função SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
 Retornando a configuração de um atributo de instrução  
 [Função SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)  
  
 Retornando informações sobre os tipos de dados de uma fonte de dados  
 [Função SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
