---
title: "Função SQLGetInfo | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 48
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 57ba22ee8645f1d3548be91adc9aafb4fc016c79
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetinfo-function"></a>Função SQLGetInfo
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 1.0 ODBC: 92 ISO  
  
 **Resumo**  
 **SQLGetInfo** retorna informações gerais sobre a fonte de dados e o driver associada a uma conexão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLGetInfo(  
     SQLHDBC         ConnectionHandle,  
     SQLUSMALLINT    InfoType,  
     SQLPOINTER      InfoValuePtr,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *Identificador da conexão*  
 [Entrada] Identificador de Conexão.  
  
 *Tipo de informação*  
 [Entrada] Tipo de informações.  
  
 *InfoValuePtr*  
 [Saída] Ponteiro para um buffer no qual retornar as informações. Dependendo do *informação* solicitada, as informações retornadas será um dos seguintes: uma cadeia de caracteres terminada em nulo, um valor SQLUSMALLINT, uma máscara de bits SQLUINTEGER, um sinalizador SQLUINTEGER, um valor binário SQLUINTEGER, ou um Valor SQLULEN.  
  
 Se o *informação* argumento é SQL_DRIVER_HDESC ou SQL_DRIVER_HSTMT, o *InfoValuePtr* argumento é de entrada e saído. (Consulte os descritores de SQL_DRIVER_HDESC ou SQL_DRIVER_HSTMT posteriormente nessa descrição de função para obter mais informações.)  
  
 Se *InfoValuePtr* for NULL, *StringLengthPtr* ainda retornará o número total de bytes (excluindo o caractere null de terminação para dados de caractere) disponíveis para retornar o buffer apontado pelo *InfoValuePtr*.  
  
 *BufferLength*  
 [Entrada] Comprimento do \* *InfoValuePtr* buffer. Se o valor em  *\*InfoValuePtr* não é uma cadeia de caracteres ou se *InfoValuePtr* é um ponteiro nulo, o *BufferLength* argumento será ignorado. O driver pressupõe que o tamanho de  *\*InfoValuePtr* é SQLUSMALLINT ou SQLUINTEGER, com base no *informação*. Se  *\*InfoValuePtr* é uma cadeia de caracteres Unicode (ao chamar **SQLGetInfoW**), o *BufferLength* argumento deve ser um número par; se não, o SQLSTATE HY090 ( Comprimento de buffer ou cadeia de caracteres inválido) será retornado.  
  
 *StringLengthPtr*  
 [Saída] Ponteiro para um buffer no qual retornar o número total de bytes (excluindo o caractere null de terminação para dados de caractere) disponíveis para retornar em **InfoValuePtr*.  
  
 Para dados de caracteres, se o número de bytes disponíveis para retornar é maior que ou igual a *BufferLength*, as informações em \* *InfoValuePtr* será truncado para  *BufferLength* bytes menos o comprimento de um encerramento nulo de caracteres e é terminada em nulo pelo driver.  
  
 Todos os outros tipos de dados, o valor de *BufferLength* é ignorada e o driver pressupõe que o tamanho do \* *InfoValuePtr* é SQLUSMALLINT ou SQLUINTEGER, dependendo do  *Tipo de informação*.  
  
## <a name="return-value"></a>Valor de retorno  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLGetInfo** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_DBC e um *tratar* de *identificador da conexão*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLGetInfo** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres truncados à direita|O buffer \* *InfoValuePtr* não era grande o suficiente para retornar todas as informações solicitadas. Portanto, as informações foi truncadas. O comprimento das informações solicitadas em sua forma completo é retornado em **StringLengthPtr*. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08003|Conexão não aberta|(DM) o tipo de informação solicitada na *informação* requer uma conexão aberta. Os tipos de informações reservados pelo ODBC, SQL_ODBC_VER só podem ser retornados sem uma conexão aberta.|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo **SQLGetDiagRec** no  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY010|Erro de sequência de função|(DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *StatementHandle* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada antes de recuperação para todos os parâmetros de fluxo de dados.|  
|HY013|Erro de gerenciamento de memória|Não foi possível processar a chamada de função porque os objetos de memória subjacente não podem ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY024|Valor de atributo inválido|(DM) a *informação* argumento era SQL_DRIVER_HSTMT, e o valor apontado por *InfoValuePtr* não era um identificador de instrução válido.<br /><br /> (DM) a *informação* argumento era SQL_DRIVER_HDESC, e o valor apontado por *InfoValuePtr* não era um identificador válido do descritor.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM) o valor especificado para o argumento *BufferLength* era menor do que 0.<br /><br /> (DM) o valor especificado para *BufferLength* foi um número ímpar, e  *\*InfoValuePtr* era de um tipo de dados Unicode.|  
|HY096|Tipo de informação fora do intervalo|O valor especificado para o argumento *informação* não era válido para a versão do ODBC com suporte pelo driver.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecido. Somente Desconecte e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Campo opcional não implementado|O valor especificado para o argumento *informação* era um valor específico do driver que não é suportado pelo driver.|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|(DM) o driver que corresponde do *identificador da conexão* não oferece suporte para a função.|  
  
## <a name="comments"></a>Comentários  
 Os tipos de informações definidos atualmente são mostrados em "Tipos de informações", posteriormente nesta seção; espera-se que mais serão definido para tirar proveito de diferentes fontes de dados. Uma variedade de tipos de informações está reservada pelo ODBC; os desenvolvedores de driver devem reservar valores para seu próprio uso específico do driver do Open Group. **SQLGetInfo** não realiza nenhuma conversão de Unicode ou *conversão* (consulte [códigos de erro de ODBC do apêndice a:](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md) do *referência do programador de ODBC*) para definido pelo driver *infotipos*. Para obter mais informações, consulte [tipos de dados específicos do Driver, tipos de descritor, tipos de informações, tipos de diagnóstico e atributos](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md). O formato das informações retornadas em \* *InfoValuePtr* depende de *informação* solicitado. **SQLGetInfo** retornará informações em um dos cinco formatos diferentes:  
  
-   Uma cadeia de caracteres terminada em nulo  
  
-   Um valor SQLUSMALLINT  
  
-   Um bitmask SQLUINTEGER  
  
-   Um valor SQLUINTEGER  
  
-   Um valor binário SQLUINTEGER  
  
 O formato de cada um dos seguintes tipos de informações é indicado na descrição do tipo. O aplicativo deve converter o valor retornado em **InfoValuePtr* adequadamente. Para obter um exemplo de como um aplicativo pode recuperar dados de uma máscara de bits SQLUINTEGER, consulte "Exemplo de código".  
  
 Um driver deve retornar um valor para cada tipo de informação que é definido nas tabelas a seguir. Se não se aplicam a um tipo de informação para o driver ou fonte de dados, o driver retorna um dos valores listados na tabela a seguir.  
  
 Cadeia de caracteres ("Y" ou "N")  
 "N"  
  
 Cadeia de caracteres (não "Y" ou "N")  
 Cadeia de caracteres vazia  
  
 SQLUSMALLINT  
 0  
  
 Máscara de bits SQLUINTEGER ou valor binário SQLUINTEGER  
 0L  
  
 Por exemplo, se uma fonte de dados não oferece suporte a procedimentos, **SQLGetInfo** retorna os valores listados na tabela a seguir para obter os valores de *informação* que estão relacionados aos procedimentos.  
  
 SQL_PROCEDURES  
 "N"  
  
 SQL_ACCESSIBLE_PROCEDURES  
 "N"  
  
 SQL_MAX_PROCEDURE_NAME_LEN  
 0  
  
 SQL_PROCEDURE_TERM  
 Cadeia de caracteres vazia  
  
 **SQLGetInfo** retorna SQLSTATE HY096 (valor de argumento inválido) para valores de *informação* que estão no intervalo de tipos de informações reservados para uso por ODBC, mas não são definidos pela versão do ODBC com suporte pelo driver. Para determinar qual versão do ODBC é um driver compatível com, um aplicativo chama **SQLGetInfo** com o tipo de informação SQL_DRIVER_ODBC_VER. **SQLGetInfo** retorna SQLSTATE HYC00 (recurso opcional não implementado) para valores de *informação* que estão no intervalo reservado para uso específico do driver de tipos de informação, mas não são suportadas pelo driver.  
  
 Todas as chamadas para **SQLGetInfo** exigem uma conexão aberta, exceto quando o *informação* é SQL_ODBC_VER, que retorna a versão do Gerenciador de Driver.  
  
## <a name="information-types"></a>Tipos de informações  
 Esta seção lista os tipos de informações com suporte pelo **SQLGetInfo**. Tipos de informações são agrupados categoricamente e listados em ordem alfabética. Tipos de informações que foram adicionados ou renomeados para ODBC 3*. x* também são listados.  
  
## <a name="driver-information"></a>Informações sobre o driver  
 Os seguintes valores da *informação* argumento retornar informações sobre o driver ODBC, como o número de instruções ativas, o nome da fonte de dados e o nível de conformidade de padrões de interface:  
  
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
>  Ao implementar **SQLGetInfo**, um driver pode melhorar o desempenho, reduzindo o número de vezes que informações são enviadas ou solicitadas do servidor.  
  
## <a name="dbms-product-information"></a>Informações de produto do DBMS  
 Os seguintes valores da *informação* argumento retornar informações sobre o produto do DBMS, como o nome do DBMS e versão:  
  
 SQL_DATABASE_NAMESQL_DBMS_NAMESQL_DBMS_VER  
  
## <a name="data-source-information"></a>Informações de fonte de dados  
 Os seguintes valores da *informação* argumento retornar informações sobre a fonte de dados, como recursos de transação e características de cursor:  
  
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
 Os seguintes valores da *informação* argumento retornar informações sobre as instruções SQL com suporte pela fonte de dados. A sintaxe SQL de cada recurso descrito por esses tipos de informações é a sintaxe SQL-92. Esses tipos de informações não exaustivamente descrevem a gramática de SQL-92 inteira. Em vez disso, eles descrevem as partes da gramática de quais dados fontes geralmente oferecem diferentes níveis de suporte. Especificamente, a maioria das instruções DDL de SQL-92 é abordada.  
  
 Aplicativos devem determinar o nível geral de gramática com suporte do tipo de informações de SQL_SQL_CONFORMANCE e use os outros tipos de informações para determinar variações do nível de conformidade de padrões definidos.  
  
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
  
## <a name="sql-limits"></a>Limites SQL  
 Os seguintes valores da *informação* argumento retornar informações sobre os limites aplicado para identificadores e cláusulas em instruções SQL, como os comprimentos máximos de identificadores e o número máximo de colunas em uma lista de seleção. Limitações podem ser impostas pelo driver ou fonte de dados.  
  
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
 Os seguintes valores da *informação* argumento retornar informações sobre as funções escalares suportado pela fonte de dados e o driver. Para obter mais informações sobre as funções escalares, consulte [funções escalares do apêndice e:](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).  
  
|||  
|-|-|  
|SQL_CONVERT_FUNCTIONS|SQL_TIMEDATE_ADD_INTERVALS|  
|SQL_NUMERIC_FUNCTIONS|SQL_TIMEDATE_DIFF_INTERVALS|  
|SQL_STRING_FUNCTIONS|SQL_TIMEDATE_FUNCTIONS|  
|SQL_SYSTEM_FUNCTIONS||  
  
## <a name="conversion-information"></a>Informações de conversão  
 Os seguintes valores da *informação* argumento retornar uma lista dos tipos de dados SQL para o qual a fonte de dados pode converter o tipo de dados SQL especificado com o **converter** função escalar:  
  
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
  
## <a name="information-types-added-for-odbc-3x"></a>Tipos de informações adicionadas para ODBC 3. x  
 Os seguintes valores da *informação* argumento foram adicionadas para ODBC 3*. x*:  
  
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
 Os seguintes valores da *informação* argumento foram renomeados para ODBC 3*. x*.  
  
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
  
## <a name="information-types-deprecated-in-odbc-3x"></a>Tipos de informações obsoletas no ODBC 3. x  
 Os seguintes valores da *informação* argumento foram substituídos no ODBC 3*. x*. ODBC 3*. x* drivers devem continuar a oferecer suporte a esses tipos de informações para fins de compatibilidade com o ODBC 2*. x* aplicativos. (Para obter mais informações sobre esses tipos, consulte [suporte SQLGetInfo](../../../odbc/reference/appendixes/sqlgetinfo-support.md) no Apêndice g: Driver diretrizes para compatibilidade com versões anteriores.)  
  
|||  
|-|-|  
|SQL_FETCH_DIRECTION|SQL_POS_OPERATIONS|  
|SQL_LOCK_TYPES|SQL_POSITIONED_STATEMENTS|  
|SQL_ODBC_API_CONFORMANCE|SQL_SCROLL_CONCURRENCY|  
|SQL_ODBC_SQL_CONFORMANCE|SQL_STATIC_SENSITIVITY|  
  
## <a name="information-type-descriptions"></a>Descrições de tipos de informações  
 A tabela a seguir lista em ordem alfabética cada tipo de informação, a versão do ODBC no qual ele foi introduzido e sua descrição.  
  
 SQL_ACCESSIBLE_PROCEDURES ODBC (1.0)  
 Uma cadeia de caracteres: "Y" se o usuário pode executar todos os procedimentos retornados pelo **SQLProcedures**; "N" caso haja procedimentos retornado se o usuário não pode executar.  
  
 SQL_ACCESSIBLE_TABLES ODBC (1.0)  
 Uma cadeia de caracteres: "Y" se o usuário tem a garantia **selecione** privilégios para todas as tabelas retornadas por **SQLTables**; "N" caso haja tabelas retornadas que o usuário não pode acessar.  
  
 SQL_ACTIVE_ENVIRONMENTS (ODBC 3.0)  
 Um valor SQLUSMALLINT que especifica o número máximo de ambientes ativos que o driver pode suportar. Se não há nenhum limite especificado ou o limite é desconhecido, esse valor é definido como zero.  
  
 SQL_AGGREGATE_FUNCTIONS (ODBC 3.0)  
 Um bitmask SQLUINTEGER enumerando suporte para funções de agregação:  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 Um driver em conformidade com o nível de entrada do SQL-92 sempre retornará todas essas opções com suporte.  
  
 SQL_ALTER_DOMAIN (ODBC 3.0)  
 Um bitmask SQLUINTEGER enumerando as cláusulas no **alterar domínio** instrução, conforme definido em SQL-92, suportado pela fonte de dados. Um driver compatível com nível completo do SQL-92 sempre retornará todas as máscaras de bits. Um valor de retorno "0" significa que o **alterar domínio** instrução não é suportada.  
  
 O nível de conformidade FIPS ou de SQL-92 em que esse recurso deve ser suportado é mostrado entre parênteses ao lado de cada máscara de bits.  
  
 Bitmasks a seguir são usados para determinar quais cláusulas são suportadas:  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT = adicionando uma restrição de domínio tem suporte (nível total)  
  
 SQL_AD_ADD_DOMAIN_DEFAULT = \<alterar domínio > \<cláusula de padrão do conjunto de domínio > é suportado (nível total)  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION = \<cláusula de definição de nome de restrição > há suporte para nomes de restrição de domínio (nível intermediário)  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT = \<cláusula de restrição drop domínio > é suportado (nível total)  
  
 SQL_AD_DROP_DOMAIN_DEFAULT = \<alterar domínio > \<cláusula de padrão de domínio drop > há suporte para (nível total)  
  
 Os bits a seguir especificam com suporte \<atributos de restrição > Se \<adicionar restrição de domínio > é suportado (o bit SQL_AD_ADD_DOMAIN_CONSTRAINT é definido):  
  
 SQL_AD_ADD_CONSTRAINT_DEFERRABLE (nível completo) SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE (nível completo) SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED (nível completo) SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE (nível completo)  
  
 SQL_ALTER_TABLE (ODBC 2.0)  
 Um bitmask SQLUINTEGER enumerando as cláusulas no **ALTER TABLE** suporte pela fonte de dados.  
  
 O nível de conformidade FIPS ou de SQL-92 em que esse recurso deve ser suportado é mostrado entre parênteses ao lado de cada máscara de bits.  
  
 Bitmasks a seguir são usados para determinar quais cláusulas são suportadas:  
  
 SQL_AT_ADD_COLUMN_COLLATION = \<adicionar coluna > cláusula é suportada com o recurso para especificar o agrupamento de coluna (nível completo) (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_DEFAULT = \<adicionar coluna > cláusula é suportada com o recurso para especificar os padrões de coluna (nível FIPS transição) (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_SINGLE = \<adicionar coluna > é (nível de FIPS transição) com suporte (ODBC 3.0)  
  
 SQL_AT_ADD_CONSTRAINT = \<adicionar coluna > cláusula é suportada com o recurso para especificar restrições de coluna (nível FIPS transição) (ODBC 3.0)  
  
 SQL_AT_ADD_TABLE_CONSTRAINT = \<adicionar restrição de tabela > há suporte para a cláusula (nível FIPS transição) (ODBC 3.0)  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION = \<definição de nome de restrição > há suporte para restrições de tabela e coluna (nível intermediário) de nomenclatura (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_CASCADE = \<descartar a coluna > é suportada em cascata (nível FIPS transição) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_DEFAULT = \<alterar a coluna > \<cláusula de padrão de coluna drop > é (nível intermediário) com suporte (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_RESTRICT = \<descartar a coluna > RESTRINGIR tem suporte (nível FIPS transição) (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT = \<descartar a coluna > RESTRINGIR tem suporte (nível FIPS transição) (ODBC 3.0)  
  
 SQL_AT_SET_COLUMN_DEFAULT = \<alterar a coluna > \<cláusula de padrão de coluna do conjunto > é (nível intermediário) com suporte (ODBC 3.0)  
  
 Os bits seguir especificam o suporte \<atributos de restrição > se há suporte para especificar restrições de coluna ou tabela (o bit SQL_AT_ADD_CONSTRAINT é definido):  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED (nível completo) (ODBC 3.0) SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE (nível completo) (ODBC 3.0) SQL_AT_CONSTRAINT_DEFERRABLE (nível completo) (ODBC 3.0) SQL_AT_CONSTRAINT_NON_DEFERRABLE (nível completo) (ODBC 3.0)  
  
 SQL_ASYNC_DBC_FUNCTIONS (ODBC 3.8)  
 Um valor SQLUINTEGER que indica se o driver pode executar funções de forma assíncrona o identificador de conexão.  
  
 SQL_ASYNC_DBC_CAPABLE = o driver pode executar funções de conexão de forma assíncrona.  
  
 SQL_ASYNC_DBC_NOT_CAPABLE = o driver não pode executar funções de conexão de forma assíncrona.  
  
 SQL_ASYNC_MODE (ODBC 3.0)  
 Um valor SQLUINTEGER que indica o nível de suporte assíncrono no driver:  
  
 SQL_AM_CONNECTION = há suporte para execução assíncrona de nível de Conexão. Todos os identificadores de instrução associados com um identificador de conexão fornecido estão no modo assíncrono ou todos estão no modo síncrono. Um identificador de instrução em uma conexão não pode estar em modo assíncrono, enquanto outro identificador de instrução sobre a mesma conexão estiver no modo síncrono e vice-versa.  
  
 SQL_AM_STATEMENT = há suporte para execução assíncrona de nível de instrução. Alguns identificadores de instrução associados com um identificador de conexão podem estar em modo assíncrono, enquanto outros identificadores de instrução sobre a mesma conexão estiver no modo síncrono.  
  
 SQL_AM_NONE = assíncrona modo não é suportado.  
  
 SQL_ASYNC_NOTIFICATION  
 Um valor SQLUINTEGER que indica se o driver dá suporte à notificação assíncrona:  
  
-   **SQL_ASYNC_NOTIFICATION_CAPABLE** notificação de execução assíncrona é suportada pelo driver.  
  
-   **SQL_ASYNC_NOTIFICATION_NOT_CAPABLE** não há suporte para notificação de execução assíncrona pelo driver.  
  
 Há duas categorias de operações assíncronas de ODBC: operações assíncronas nível de conexão e instrução de nível de operações assíncronas.  Se um driver retorna SQL_ASYNC_NOTIFICATION_CAPABLE, ele deve dar suporte à notificação para todas as APIs que ele pode executar de forma assíncrona.  
  
 SQL_BATCH_ROW_COUNT (ODBC 3.0)  
 Um bitmask SQLUINTEGER que enumera o comportamento do driver em relação à disponibilidade de linha de conta. As seguir bitmasks são usados junto com o tipo de informações:  
  
 SQL_BRC_ROLLED_UP = contagens de linhas para instruções INSERT, DELETE ou UPDATE consecutivas são acumuladas em uma. Se este bit não for definido, as contagens de linha estão disponíveis para cada instrução.  
  
 SQL_BRC_PROCEDURES = contagens de linhas, se houver, estão disponíveis quando um lote é executado em um procedimento armazenado. Se houver contagens de linhas, eles podem ser rolados para cima ou individualmente disponíveis, dependendo do bit SQL_BRC_ROLLED_UP.  
  
 SQL_BRC_EXPLICIT = contagens de linhas, se houver, estão disponíveis quando um lote é executado diretamente chamando **SQLExecute** ou **SQLExecDirect**. Se houver contagens de linhas, eles podem ser rolados para cima ou individualmente disponíveis, dependendo do bit SQL_BRC_ROLLED_UP.  
  
 SQL_BATCH_SUPPORT (ODBC 3.0)  
 Um bitmask SQLUINTEGER ao enumerar o suporte do driver de lotes. Bitmasks a seguir são usados para determinar qual nível tem suporte:  
  
 SQL_BS_SELECT_EXPLICIT = os lotes de explícita dá suporte ao driver que podem ter conjunto de resultados gerar instruções.  
  
 SQL_BS_ROW_COUNT_EXPLICIT = os lotes de explícita dá suporte ao driver que podem ter declarações de geração de contagem de linhas.  
  
 SQL_BS_SELECT_PROC = os procedimentos de explícita dá suporte ao driver que podem ter conjunto de resultados gerar instruções.  
  
 SQL_BS_ROW_COUNT_PROC = os procedimentos de explícita dá suporte ao driver que podem ter declarações de geração de contagem de linhas.  
  
 SQL_BOOKMARK_PERSISTENCE (ODBC 2.0)  
 Um bitmask SQLUINTEGER ao enumerar as operações por meio do qual indicadores persistirem.  
  
 Bitmasks a seguir são usadas junto com o sinalizador para determinar por meio do qual manter indicadores de opções:  
  
 SQL_BP_CLOSE = indicadores serão válidos depois que um aplicativo chama **SQLFreeStmt** com a opção SQL_CLOSE, ou **SQLCloseCursor** para fechar o cursor associado a uma instrução.  
  
 SQL_BP_DELETE = o indicador para uma linha é válida depois que a linha foi excluída.  
  
 SQL_BP_DROP = indicadores serão válidos depois que um aplicativo chama **SQLFreeHandle** com um *HandleType* sql_handle_stmt para uma instrução drop.  
  
 SQL_BP_TRANSACTION = indicadores serão válidos depois que um aplicativo confirma ou reverte uma transação.  
  
 SQL_BP_UPDATE = o indicador para uma linha é válida após qualquer coluna em que a linha tiver sido atualizada, incluindo colunas de chave.  
  
 SQL_BP_OTHER_HSTMT = um indicador associado a uma instrução pode ser usada com outra instrução. A menos que SQL_BP_CLOSE ou SQL_BP_DROP for especificado, o cursor na primeira instrução deve ser aberto.  
  
 SQL_CATALOG_LOCATION (ODBC 2.0)  
 Um valor SQLUSMALLINT que indica a posição do catálogo em um nome de tabela qualificado:  
  
 SQL_CL_STARTSQL_CL_END  
  
 Por exemplo, um driver Xbase retorna SQL_CL_START porque é o nome do diretório (catálogo) no início do nome da tabela, como \EMPDATA\EMP. DBF. Um driver do servidor ORACLE retorna SQL_CL_END porque o catálogo está no final do nome da tabela, como em ADMIN.EMP@EMPDATA.  
  
 Um driver em conformidade com o nível completo do SQL-92 sempre retornará SQL_CL_START. Um valor de 0 será retornado se a fonte de dados não têm suporte a catálogos. Para determinar se há suporte para o catálogo, um aplicativo chama **SQLGetInfo** com o tipo de informação SQL_CATALOG_NAME.  
  
 Isso *informação* foi renomeado para ODBC 3.0 do ODBC 2.0 *informação* SQL_QUALIFIER_LOCATION.  
  
 SQL_CATALOG_NAME (ODBC 3.0)  
 Uma cadeia de caracteres: "Y" se o servidor oferece suporte a nomes de catálogo ou "N" se não existir.  
  
 Um driver em conformidade com o nível completo do SQL-92 sempre retornará "Y".  
  
 SQL_CATALOG_NAME_SEPARATOR ODBC (1.0)  
 Uma cadeia de caracteres: um ou mais caracteres que define a fonte de dados como o separador entre um nome de catálogo e o elemento de nome qualificado que segue ou anterior.  
  
 Uma cadeia de caracteres vazia será retornada se a fonte de dados não têm suporte a catálogos. Para determinar se há suporte para o catálogo, um aplicativo chama **SQLGetInfo** com o tipo de informação SQL_CATALOG_NAME. Um driver em conformidade com o nível completo do SQL-92 sempre retornará ".".  
  
 Isso *informação* foi renomeado para ODBC 3.0 do ODBC 2.0 *informação* SQL_QUALIFIER_NAME_SEPARATOR.  
  
 SQL_CATALOG_TERM ODBC (1.0)  
 Uma cadeia de caracteres com o nome do fornecedor de fonte de dados para um catálogo. Por exemplo, "banco de dados" ou "directory". Essa cadeia de caracteres pode ser em superior, inferior ou maiusculas e minúsculas.  
  
 Uma cadeia de caracteres vazia será retornada se a fonte de dados não têm suporte a catálogos. Para determinar se há suporte para o catálogo, um aplicativo chama **SQLGetInfo** com o tipo de informação SQL_CATALOG_NAME. Um driver em conformidade com o nível completo do SQL-92 sempre retornará "catalog".  
  
 Isso *informação* foi renomeado para ODBC 3.0 do ODBC 2.0 *informação* SQL_QUALIFIER_TERM.  
  
 SQL_CATALOG_USAGE (ODBC 2.0)  
 Um bitmask SQLUINTEGER enumerando as instruções catálogos podem ser usados.  
  
 Bitmasks a seguir são usados para determinar onde o catálogo pode ser usado:  
  
 SQL_CU_DML_STATEMENTS = catálogos têm suporte em todas as instruções de linguagem de manipulação de dados: **selecione**, **inserir**, **atualização**, **excluir**e se suportado, **Selecione para atualizar** posicionado atualização e instruções delete.  
  
 SQL_CU_PROCEDURE_INVOCATION = catálogos têm suporte na instrução de chamada de procedimento ODBC.  
  
 SQL_CU_TABLE_DEFINITION = catálogos têm suporte em todas as instruções de definição de tabela: **CREATE TABLE**, **CREATE VIEW**, **ALTER TABLE**, **DROP TABLE** , e **DROP VIEW**.  
  
 SQL_CU_INDEX_DEFINITION = catálogos têm suporte em todas as instruções de definição de índice: **CREATE INDEX** e **DROP INDEX**.  
  
 SQL_CU_PRIVILEGE_DEFINITION = catálogos têm suporte em todas as instruções de definição de privilégio: **GRANT** e **REVOGAR**.  
  
 Um valor de 0 será retornado se a fonte de dados não têm suporte a catálogos. Para determinar se há suporte para o catálogo, um aplicativo chama **SQLGetInfo** com o tipo de informação SQL_CATALOG_NAME. Um driver em conformidade com o nível completo do SQL-92 sempre retornará uma máscara de bits com todos esses bits.  
  
 Isso *informação* foi renomeado para ODBC 3.0 do ODBC 2.0 *informação* SQL_QUALIFIER_USAGE.  
  
 SQL_COLLATION_SEQ (ODBC 3.0)  
 O nome da sequência de agrupamento. Isso é uma cadeia de caracteres que indica o nome do agrupamento padrão para o caractere padrão definido para este servidor (por exemplo, ' ISO 8859-1' ou EBCDIC). Se isso for desconhecido, uma cadeia de caracteres vazia será retornada. Um driver em conformidade com o nível completo do SQL-92 sempre retornará uma cadeia de caracteres não vazia.  
  
 SQL_COLUMN_ALIAS (ODBC 2.0)  
 Uma cadeia de caracteres: "Y" se a fonte de dados oferece suporte a aliases de coluna; Caso contrário, "N".  
  
 Um alias de coluna é um nome alternativo que pode ser especificado para uma coluna na lista de seleção usando uma cláusula. Um driver em conformidade com o nível de entrada do SQL-92 sempre retornará "Y".  
  
 SQL_CONCAT_NULL_BEHAVIOR ODBC (1.0)  
 Um valor SQLUSMALLINT que indica como a fonte de dados trata a concatenação NULL com valor de colunas do tipo de dados de caractere com colunas do tipo de dados de caractere com valores nulos:  
  
 SQL_CB_NULL = resultado será com valor de NULL.  
  
 SQL_CB_NON_NULL = resultado é a concatenação das colunas com valores nulos.  
  
 Um driver em conformidade com o nível de entrada do SQL-92 sempre retornará SQL_CB_NULL.  
  
 SQL_CONVERT_BIGINTSQL_CONVERT_BINARYSQL_CONVERT_BIT SQL_CONVERT_CHAR SQL_CONVERT_GUIDSQL_CONVERT_DATESQL_CONVERT_DECIMALSQL_CONVERT_DOUBLESQL_CONVERT_FLOATSQL_CONVERT_INTEGERSQL_CONVERT_INTERVAL_YEAR_MONTHSQL_CONVERT_INTERVAL_ DAY_TIMESQL_CONVERT_LONGVARBINARYSQL_CONVERT_LONGVARCHARSQL_CONVERT_NUMERICSQL_CONVERT_REALSQL_CONVERT_SMALLINTSQL_CONVERT_TIMESQL_CONVERT_TIMESTAMPSQL_CONVERT_TINYINTSQL_CONVERT_VARBINARYSQL_CONVERT_VARCHAR (ODBC 1.0)  
 Um bitmask SQLUINTEGER. A máscara de bits indica as conversões com suporte pela fonte de dados com o **converter** função escalar de dados do tipo nomeado no *informação*. Se a máscara de bits for igual a zero, a fonte de dados não oferece suporte a qualquer conversões de dados do tipo nomeado, inclusive a conversão para o mesmo tipo de dados.  
  
 Por exemplo, para determinar se uma fonte de dados suporta a conversão de dados SQL_INTEGER para o tipo de dados SQL_BIGINT, um aplicativo chama **SQLGetInfo** com o *informação* de SQL_CONVERT_INTEGER. O aplicativo executa um **AND** operação com a máscara de bits retornada e SQL_CVT_BIGINT. Se o valor resultante é diferente de zero, há suporte para a conversão.  
  
 Bitmasks a seguir são usados para determinar quais conversões têm suporte:  
  
 SQL_CVT_BIGINT (ODBC 1.0) SQL_CVT_BINARY (ODBC 1.0) SQL_CVT_BIT (ODBC 1.0) SQL_CVT_GUID (ODBC 3.5) SQL_CVT_CHAR (ODBC 1.0) SQL_CVT_DATE (ODBC 1.0) SQL_CVT_DECIMAL (ODBC 1.0) SQL_CVT_DOUBLE (ODBC 1.0) SQL_CVT_FLOAT (ODBC 1.0) SQL_CVT_INTEGER (ODBC 1.0) SQL _CVT_INTERVAL_YEAR_MONTH (ODBC 3.0) SQL_CVT_INTERVAL_DAY_TIME (ODBC 3.0) SQL_CVT_LONGVARBINARY (ODBC 1.0) SQL_CVT_LONGVARCHAR (ODBC 1.0) SQL_CVT_NUMERIC (ODBC 1.0) SQL_CVT_REAL ODBC 1.0) SQL_CVT_SMALLINT (ODBC 1.0) SQL_CVT_TIME (ODBC 1.0) SQL_CVT_ CARIMBO DE HORA (ODBC 1.0) SQL_CVT_TINYINT (ODBC 1.0) SQL_CVT_VARBINARY (ODBC 1.0) SQL_CVT_VARCHAR (ODBC 1.0)  
  
 SQL_CONVERT_FUNCTIONS ODBC (1.0)  
 Um bitmask SQLUINTEGER enumerando as funções de conversão de escalar com suporte de driver e a fonte de dados associada.  
  
 A máscara de bits a seguir é usada para determinar quais funções de conversão têm suporte:  
  
 SQL_FN_CVT_CASTSQL_FN_CVT_CONVERT  
  
 SQL_CORRELATION_NAME ODBC (1.0)  
 Um valor SQLUSMALLINT que indica se há suporte para nomes de correlação de tabela:  
  
 SQL_CN_NONE = não há suporte para nomes de correlação.  
  
 SQL_CN_DIFFERENT = correlação nomes têm suporte, mas devem ser diferente dos nomes das tabelas que eles representam.  
  
 SQL_CN_ANY = correlação nomes têm suporte e podem ser qualquer nome válido definido pelo usuário.  
  
 Um driver em conformidade com o nível de entrada do SQL-92 sempre retornará SQL_CN_ANY.  
  
 SQL_CREATE_ASSERTION (ODBC 3.0)  
 Um bitmask SQLUINTEGER enumerando as cláusulas no **criar ASSERÇÃO** instrução, conforme definido em SQL-92, suportado pela fonte de dados.  
  
 Bitmasks a seguir são usados para determinar quais cláusulas são suportadas:  
  
 SQL_CA_CREATE_ASSERTION  
  
 Os bits a seguir para especificar o atributo de restrição com suporte se houver suporte para a capacidade de especificar atributos de restrição explicitamente (consulte os tipos de informações SQL_ALTER_TABLE e SQL_CREATE_TABLE):  
  
 SQL_CA_CONSTRAINT_INITIALLY_DEFERREDSQL_CA_CONSTRAINT_INITIALLY_IMMEDIATESQL_CA_CONSTRAINT_DEFERRABLESQL_CA_CONSTRAINT_NON_DEFERRABLE  
  
 Um driver em conformidade com o nível completo do SQL-92 sempre retornará todas essas opções com suporte. Um valor de retorno "0" significa que o **criar ASSERÇÃO** instrução não é suportada.  
  
 SQL_CREATE_CHARACTER_SET (ODBC 3.0)  
 Um bitmask SQLUINTEGER enumerando as cláusulas no **criar conjunto de caracteres** instrução, conforme definido em SQL-92, suportado pela fonte de dados.  
  
 Bitmasks a seguir são usados para determinar quais cláusulas são suportadas:  
  
 SQL_CCS_CREATE_CHARACTER_SETSQL_CCS_COLLATE_CLAUSESQL_CCS_LIMITED_COLLATION  
  
 Um driver em conformidade com o nível completo do SQL-92 sempre retornará todas essas opções com suporte. Um valor de retorno "0" significa que o **criar conjunto de caracteres** instrução não é suportada.  
  
 SQL_CREATE_COLLATION (ODBC 3.0)  
 Um bitmask SQLUINTEGER enumerando as cláusulas no **criar AGRUPAMENTO** instrução, conforme definido em SQL-92, suportado pela fonte de dados.  
  
 A máscara de bits a seguir é usada para determinar quais cláusulas são suportadas:  
  
 SQL_CCOL_CREATE_COLLATION  
  
 Um driver em conformidade com o nível completo do SQL-92 sempre retornará essa opção com suporte. Um valor de retorno "0" significa que o **criar AGRUPAMENTO** instrução não é suportada.  
  
 SQL_CREATE_DOMAIN (ODBC 3.0)  
 Um bitmask SQLUINTEGER enumerando as cláusulas no **criar domínio** instrução, conforme definido em SQL-92, suportado pela fonte de dados.  
  
 Bitmasks a seguir são usados para determinar quais cláusulas são suportadas:  
  
 SQL_CDO_CREATE_DOMAIN = a criar domínio suporte para a instrução (intermediário nível).  
  
 SQL_CDO_CONSTRAINT_NAME_DEFINITION = \<definição de nome de restrição > há suporte para restrições de domínio (nível intermediário) de nomenclatura.  
  
 Os bits seguintes especificam a capacidade de criar restrições de coluna: SQL_CDO_DEFAULT = há suporte para especificar restrições de domínio (nível de intermediário) SQL_CDO_CONSTRAINT = há suporte para especificar o domínio padrão (intermediário nível) SQL_CDO_COLLATION = Há suporte para especificar o agrupamento de domínio (nível total)  
  
 Os bits a seguir para especificar os atributos de restrição com suporte se há suporte para especificar restrições de domínio (SQL_CDO_DEFAULT é definido):  
  
 SQL_CDO_CONSTRAINT_INITIALLY_DEFERRED (nível completo) SQL_CDO_CONSTRAINT_INITIALLY_IMMEDIATE (nível completo) SQL_CDO_CONSTRAINT_DEFERRABLE (nível completo) SQL_CDO_CONSTRAINT_NON_DEFERRABLE (nível completo)  
  
 Um valor de retorno "0" significa que o **criar domínio** instrução não é suportada.  
  
 SQL_CREATE_SCHEMA (ODBC 3.0)  
 Um bitmask SQLUINTEGER enumerando as cláusulas no **CREATE SCHEMA** instrução, conforme definido em SQL-92, suportado pela fonte de dados.  
  
 Bitmasks a seguir são usados para determinar quais cláusulas são suportadas:  
  
 SQL_CS_CREATE_SCHEMASQL_CS_AUTHORIZATIONSQL_CS_DEFAULT_CHARACTER_SET  
  
 Um driver em conformidade com o nível intermediário do SQL-92 sempre retornará o SQL_CS_CREATE_SCHEMA e SQL_CS_AUTHORIZATION as opções com suporte. Eles também devem ter suporte no nível de entrada do SQL-92, mas não necessariamente instruções SQL. Um driver em conformidade com o nível completo do SQL-92 sempre retornará todas essas opções com suporte.  
  
 SQL_CREATE_TABLE (ODBC 3.0)  
 Um bitmask SQLUINTEGER enumerando as cláusulas no **CREATE TABLE** instrução, conforme definido em SQL-92, suportado pela fonte de dados.  
  
 O nível de conformidade FIPS ou de SQL-92 em que esse recurso deve ser suportado é mostrado entre parênteses ao lado de cada máscara de bits.  
  
 Bitmasks a seguir são usados para determinar quais cláusulas são suportadas:  
  
 SQL_CT_CREATE_TABLE = o CREATE TABLE instrução tem suporte. (Nível de entrada)  
  
 SQL_CT_TABLE_CONSTRAINT = há suporte para especificar restrições de tabela (nível FIPS transição)  
  
 SQL_CT_CONSTRAINT_NAME_DEFINITION = o \<definição de nome de restrição > cláusula tem suporte para a nomeação de restrições de tabela e coluna (nível intermediário)  
  
 Os bits seguintes especificam a capacidade de criar tabelas temporárias:  
  
 SQL_CT_COMMIT_PRESERVE = excluídas linhas são preservadas na confirmação. (Nível completo) SQL_CT_COMMIT_DELETE = excluídas linhas são excluídas na confirmação. (Nível completo) SQL_CT_GLOBAL_TEMPORARY = Global tabelas temporárias podem ser criadas. (Nível completo) SQL_CT_LOCAL_TEMPORARY = Local tabelas temporárias podem ser criadas. (Nível completo)  
  
 Os bits seguintes especificam a capacidade de criar restrições de coluna:  
  
 SQL_CT_COLUMN_CONSTRAINT = há suporte para especificar restrições de coluna (nível FIPS transição) SQL_CT_COLUMN_DEFAULT = há suporte para especificar padrões de coluna (nível FIPS transição) SQL_CT_COLUMN_COLLATION = especificando o agrupamento da coluna é com suporte (nível completo)  
  
 Os seguintes bits especificam os atributos de restrição com suporte se há suporte para especificar restrições de coluna ou tabela:  
  
 SQL_CT_CONSTRAINT_INITIALLY_DEFERRED (nível completo) SQL_CT_CONSTRAINT_INITIALLY_IMMEDIATE (nível completo) SQL_CT_CONSTRAINT_DEFERRABLE (nível completo) SQL_CT_CONSTRAINT_NON_DEFERRABLE (nível completo)  
  
 SQL_CREATE_TRANSLATION (ODBC 3.0)  
 Um bitmask SQLUINTEGER enumerando as cláusulas no **criar tradução** instrução, conforme definido em SQL-92, suportado pela fonte de dados.  
  
 A máscara de bits a seguir é usada para determinar quais cláusulas são suportadas:  
  
 SQL_CTR_CREATE_TRANSLATION  
  
 Um driver em conformidade com o nível completo do SQL-92 sempre retornará essas opções com suporte. Um valor de retorno "0" significa que o **criar tradução** instrução não é suportada.  
  
 SQL_CREATE_VIEW (ODBC 3.0)  
 Um bitmask SQLUINTEGER enumerando as cláusulas no **CREATE VIEW** instrução, conforme definido em SQL-92, suportado pela fonte de dados.  
  
 Bitmasks a seguir são usados para determinar quais cláusulas são suportadas:  
  
 SQL_CV_CREATE_VIEWSQL_CV_CHECK_OPTIONSQL_CV_CASCADEDSQL_CV_LOCAL  
  
 Um valor de retorno "0" significa que o **CREATE VIEW** instrução não é suportada.  
  
 Um driver em conformidade com o nível de entrada do SQL-92 sempre retornará o SQL_CV_CREATE_VIEW e SQL_CV_CHECK_OPTION as opções com suporte.  
  
 Um driver em conformidade com o nível completo do SQL-92 sempre retornará todas essas opções com suporte.  
  
 SQL_CURSOR_COMMIT_BEHAVIOR ODBC (1.0)  
 Um valor SQLUSMALLINT que indica como um **confirmação** operação afeta cursores e instruções preparadas na fonte de dados (o comportamento da fonte de dados quando você confirma uma transação).  
  
 O valor deste atributo refletirá o estado atual da próxima configuração: SQL_COPT_SS_PRESERVE_CURSORS.  
  
 SQL_CB_DELETE = fechar cursores e excluir instruções preparadas. Para usar o cursor novamente, o aplicativo deve reprepare e execute novamente a instrução.  
  
 SQL_CB_CLOSE = fechar cursores. Para instruções preparadas, o aplicativo pode chamar **SQLExecute** na instrução sem chamar **SQLPrepare** novamente. O padrão para o driver ODBC do SQL é SQL_CB_CLOSE. Isso significa que o driver ODBC do SQL fechará o cursor(s) quando você confirma uma transação.  
  
 SQL_CB_PRESERVE = Preserve cursores na mesma posição como antes de **confirmar** operação. O aplicativo pode continuar buscar dados, ou pode fechar o cursor e execute novamente a instrução sem prepará-lo novamente.  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR ODBC (1.0)  
 Um valor SQLUSMALLINT que indica como um **REVERSÃO** operação afeta cursores e instruções preparadas na fonte de dados:  
  
 SQL_CB_DELETE = fechar cursores e excluir instruções preparadas. Para usar o cursor novamente, o aplicativo deve reprepare e execute novamente a instrução.  
  
 SQL_CB_CLOSE = fechar cursores. Para instruções preparadas, o aplicativo pode chamar **SQLExecute** na instrução sem chamar **SQLPrepare** novamente.  
  
 SQL_CB_PRESERVE = Preserve cursores na mesma posição como antes de **REVERSÃO** operação. O aplicativo pode continuar buscar dados, ou pode fechar o cursor e executar novamente a instrução sem repreparing-lo.  
  
 SQL_CURSOR_SENSITIVITY (ODBC 3.0)  
 Um valor SQLUINTEGER que indica o suporte a sensibilidade do cursor:  
  
 SQL_INSENSITIVE = todos os cursores ao programa de identificador de instrução que o conjunto de resultados sem refletir as alterações que foram feitas por qualquer outro cursor dentro da mesma transação.  
  
 SQL_UNSPECIFIED = é não especificado se cursores no identificador da instrução tornar visíveis as alterações feitas em um conjunto de resultados por outro cursor dentro da mesma transação. Cursores no identificador da instrução podem tornar visível none, algumas ou todas essas alterações.  
  
 SQL_SENSITIVE = cursores são sensíveis às alterações feitas por outros cursores dentro da mesma transação.  
  
 Um driver em conformidade com o nível de entrada do SQL-92 sempre retornará a opção SQL_UNSPECIFIED com suporte.  
  
 Um driver em conformidade com o nível completo do SQL-92 sempre retornará a opção SQL_INSENSITIVE com suporte.  
  
 SQL_DATA_SOURCE_NAME ODBC (1.0)  
 Uma cadeia de caracteres com o nome da fonte de dados que foi usado durante a conexão. Se o aplicativo chamado **SQLConnect**, esse é o valor da *szDSN* argumento. Se o aplicativo chamado **SQLDriverConnect** ou **SQLBrowseConnect**, esse é o valor da palavra-chave DSN na cadeia de conexão passada para o driver. Se a cadeia de caracteres de conexão não continha o **DSN** palavra-chave (como quando ele contém o **DRIVER** palavra-chave), isso é uma cadeia de caracteres vazia.  
  
 SQL_DATA_SOURCE_READ_ONLY ODBC (1.0)  
 Uma cadeia de caracteres. "Y" se a fonte de dados é definida para o modo somente leitura, "N" Se você tiver outra forma.  
  
 Essa característica diz respeito apenas a fonte de dados em si; não é uma característica do driver que permite o acesso à fonte de dados. Um driver de leitura/gravação pode ser usado com uma fonte de dados é somente leitura. Se um driver for somente leitura, todas as suas fontes de dados devem ser somente leitura e devem retornar SQL_DATA_SOURCE_READ_ONLY.  
  
 SQL_DATABASE_NAME ODBC (1.0)  
 Uma cadeia de caracteres com o nome do banco de dados atual em uso, se a fonte de dados define um objeto nomeado chamado "database".  
  
> [!NOTE]  
>  Em ODBC 3*. x*, o valor retornado para este *informação* também pode ser retornado ao chamar **SQLGetConnectAttr** com um *atributo* argumento de SQL_ATTR_CURRENT_CATALOG.  
  
 SQL_DATETIME_LITERALS (ODBC 3.0)  
 Um bitmask SQLUINTEGER ao enumerar os literais de data/hora do SQL-92 suportados pela fonte de dados. Observe que esses são os literais de data e hora listados na especificação SQL-92 e são separadas de cláusulas de fuga literal de data e hora definidas pelo ODBC. Para obter mais informações sobre as cláusulas de fuga ODBC datetime literal, consulte [data, hora e literais de carimbo de hora](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md).  
  
 Um driver de nível em conformidade com FIPS transição sempre retornará o valor "1" na máscara de bits para os bits na lista a seguir. Um valor de "0" significa que não há suporte para literais de data/hora do SQL-92.  
  
 Bitmasks a seguir são usados para determinar quais literais têm suporte:  
  
 SQL_DL_SQL92_DATESQL_DL_SQL92_TIMESQL_DL_SQL92_TIMESTAMPSQL_DL_SQL92_INTERVAL_YEARSQL_DL_SQL92_INTERVAL_MONTHSQL_DL_SQL92_INTERVAL_DAYSQL_DL_SQL92_INTERVAL_HOURSQL_DL_SQL92_INTERVAL_MINUTESQL_DL_SQL92_INTERVAL_SECONDSQL_DL_ SQL92_INTERVAL_YEAR_TO_MONTHSQL_DL_SQL92_INTERVAL_DAY_TO_HOUR  
  
 SQL_DL_SQL92_INTERVAL_DAY_TO_MINUTESQL_DL_SQL92_INTERVAL_DAY_TO_SECONDSQL_DL_SQL92_INTERVAL_HOUR_TO_MINUTESQL_DL_SQL92_INTERVAL_HOUR_TO_SECONDSQL_DL_SQL92_INTERVAL_MINUTE_TO_SECOND  
  
 SQL_DBMS_NAME ODBC (1.0)  
 Uma cadeia de caracteres com o nome do produto do DBMS acessado pelo driver.  
  
 SQL_DBMS_VER ODBC (1.0)  
 Uma cadeia de caracteres que indica a versão do produto DBMS acessado pelo driver. É a versão do formulário # #. # #. # # #, onde os dois primeiros dígitos são a versão principal, os dois dígitos são a versão secundária, e os quatro últimos dígitos são a versão de lançamento. O driver deve processar a versão de produto do DBMS neste formulário, mas também pode acrescentar a versão de produto específica do DBMS. Por exemplo, "04.01.0000 Rdb 4.1".  
  
 SQL_DDL_INDEX (ODBC 3.0)  
 Um valor SQLUINTEGER que indica o suporte para a criação e o descarte de índices:  
  
 SQL_DI_CREATE_INDEXSQL_DI_DROP_INDEX  
  
 SQL_DEFAULT_TXN_ISOLATION ODBC (1.0)  
 Um valor SQLUINTEGER que indica que o nível de isolamento de transação padrão com suporte da driver ou fonte de dados, ou zero se a fonte de dados não oferece suporte a transações. Os seguintes termos são usados para definir níveis de isolamento da transação:  
  
 **Leitura suja** 1 transação altera uma linha. Transação 2 lê a linha alterada antes que a transação 1 confirma a alteração. Se a transação 1 reverte a alteração, transação 2 têm lerá uma linha que é considerada inexistentes.  
  
 **Leitura não repetível** 1 transação lê uma linha. Transação 2 atualiza ou exclui essa linha e essa alteração é confirmada. Se a transação 1 tenta ler novamente a linha, ele irá receber valores de linha diferente ou descobrir que a linha foi excluída.  
  
 **Fantasma** 1 transação lê um conjunto de linhas que atenderem a alguns critérios de pesquisa. Transação 2 gera uma ou mais linhas (por meio de inserções ou atualizações) que correspondem aos critérios de pesquisa. Se a transação 1 reexecutes a instrução que lê as linhas, ele recebe um conjunto diferente de linhas.  
  
 Se a fonte de dados oferece suporte a transações, o driver retorna um bitmasks a seguir:  
  
 SQL_TXN_READ_UNCOMMITTED = Dirty fantasmas, leituras não repetíveis e leituras são possíveis.  
  
 SQL_TXN_READ_COMMITTED = Dirty leituras não são possíveis. Fantasmas e leituras não repetíveis são possíveis.  
  
 SQL_TXN_REPEATABLE_READ = Dirty leituras não repetíveis e leituras não são possíveis. Fantasmas são possíveis.  
  
 SQL_TXN_SERIALIZABLE = transações são serializáveis. Transações serializáveis não permitem leituras sujas, leituras não repetíveis ou fantasmas.  
  
 SQL_DESCRIBE_PARAMETER (ODBC 3.0)  
 Uma cadeia de caracteres: "Y", se os parâmetros podem ser descritos; "N", se não for.  
  
 Um driver em conformidade com o nível completo do SQL-92 geralmente retornará "Y" porque ele suportará o **entrada DESCREVEM** instrução. Porque isso não especifica diretamente o suporte a SQL subjacente, no entanto, que descreve os parâmetros talvez não tenha suporte, mesmo em um driver em conformidade com o nível completo do SQL-92.  
  
 SQL_DM_VER (ODBC 3.0)  
 Uma cadeia de caracteres com a versão do Gerenciador de Driver. É a versão do formulário # #. # #. # # #. # # #, onde:  
  
 O primeiro conjunto de dois dígitos é a versão principal do ODBC, conforme fornecido por SQL_SPEC_MAJOR a constante.  
  
 O segundo conjunto de dois dígitos é a versão secundária do ODBC, conforme fornecido por SQL_SPEC_MINOR a constante.  
  
 O terceiro conjunto de quatro dígitos é o número da compilação principal do Gerenciador de Driver.  
  
 O último conjunto de quatro dígitos é o número de compilação secundária do Gerenciador de Driver.  
  
 A versão do Gerenciador de Driver do Windows 7 é 03.80. A versão do Gerenciador de Driver do Windows 8 é 03.81.  
  
 SQL_DRIVER_AWARE_POOLING_SUPPORTED (ODBC 3.8)  
 Um valor SQLUINTEGER que indica se o driver suporta pooling com reconhecimento de driver. (Para obter mais informações, consulte [Pooling de Conexão com reconhecimento de Driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md).  
  
 SQL_DRIVER_AWARE_POOLING_CAPABLE indica que o driver pode suportar mecanismo pooling com reconhecimento de driver.  
  
 SQL_DRIVER_AWARE_POOLING_NOT_CAPABLE indica que o driver não oferece suporte a reconhecimento de driver de mecanismo de pool.  
  
 Um driver não precisa implementar SQL_DRIVER_AWARE_POOLING_SUPPORTED e o Gerenciador de Driver não poderão usar para o valor de retorno do driver.  
  
 SQL_DRIVER_HDBCSQL_DRIVER_HENV ODBC (1.0)  
 Um valor SQLULEN, identificador de ambiente ou identificador de conexão, determinada pelo argumento do driver *informação*.  
  
 Esses tipos de informações são implementados pelo Gerenciador de Driver sozinho.  
  
 SQL_DRIVER_HDESC (ODBC 3.0)  
 Valor de um SQLULEN, identificador do descritor do driver determinado pelo identificador do descritor do Gerenciador de Driver, que deve ser passado na entrada em \* *InfoValuePtr* do aplicativo. Nesse caso, *InfoValuePtr* é um argumento de entrada e saído. O identificador do descritor de entrada passado em \* *InfoValuePtr* deve ter sido explicitamente ou implicitamente alocado no *identificador da conexão*.  
  
 O aplicativo deve fazer uma cópia do descritor do Gerenciador de Driver de manipular antes de chamar **SQLGetInfo** com este tipo de informação, para certificar-se de que o identificador não é substituído na saída.  
  
 Este tipo de informação é implementado pelo Gerenciador de Driver sozinho.  
  
 SQL_DRIVER_HLIB (ODBC 2.0)  
 Um valor SQLULEN, o *hinst* da biblioteca de carga retornado para o Gerenciador de Driver quando ele carregar a DLL do driver em um sistema operacional Microsoft Windows, ou seu equivalente em outro sistema operacional. O identificador é válido somente para o identificador de conexão especificado na chamada para **SQLGetInfo**.  
  
 Este tipo de informação é implementado pelo Gerenciador de Driver sozinho.  
  
 SQL_DRIVER_HSTMT ODBC (1.0)  
 Valor de um SQLULEN, identificador de instrução do driver determinado pelo identificador de instrução do Gerenciador de Driver, que deve ser passado na entrada no \* *InfoValuePtr* do aplicativo. Nesse caso, *InfoValuePtr* é uma entrada e um argumento de saída. O identificador de instrução de entrada passado em \* *InfoValuePtr* deve ter sido alocado no argumento *identificador da conexão*.  
  
 O aplicativo deve fazer uma cópia da instrução do Gerenciador de Driver manipular antes de chamar **SQLGetInfo** com este tipo de informação, para garantir que o identificador não é substituído na saída.  
  
 Este tipo de informação é implementado pelo Gerenciador de Driver sozinho.  
  
 SQL_DRIVER_NAME ODBC (1.0)  
 Uma cadeia de caracteres com o nome do arquivo do driver usado para acessar a fonte de dados.  
  
 SQL_DRIVER_ODBC_VER (ODBC 2.0)  
 Uma cadeia de caracteres com a versão do ODBC que o driver dá suporte. É a versão do formulário # #. # #, onde os dois primeiros dígitos são a versão principal, e os dois dígitos são a versão secundária. SQL_SPEC_MAJOR e SQL_SPEC_MINOR definem os números de versão primária e secundária. Para obter a versão do ODBC descrito neste manual, os 3 e 0, e o driver deve retornar "03.00".  
  
 O Gerenciador de Driver ODBC não modificará o valor de retorno de SQLGetInfo(SQL_DRIVER_ODBC_VER) para manter a compatibilidade com versões anteriores para os aplicativos existentes. O driver Especifica qual valor será retornado. No entanto, um driver que dá suporte à extensibilidade do tipo de dados C deve retornar 3.8 (ou superior) quando um aplicativo chama **SQLSetEnvAttr** para definir SQL_ATTR_ODBC_VERSION como 3.8. Para obter mais informações, consulte [tipos de dados C em ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 SQL_DRIVER_VER ODBC (1.0)  
 Uma cadeia de caracteres com a versão do driver e, opcionalmente, uma descrição do driver. No mínimo, a versão está no formato # #. # #. # # #, onde os dois primeiros dígitos são a versão principal, os dois dígitos são a versão secundária, e os quatro últimos dígitos são a versão de lançamento.  
  
 SQL_DROP_ASSERTION (ODBC 3.0)  
 Um bitmask SQLUINTEGER enumerando as cláusulas no **DROP ASSERÇÃO** instrução, conforme definido em SQL-92, suportado pela fonte de dados.  
  
 A máscara de bits a seguir é usada para determinar quais cláusulas são suportadas:  
  
 SQL_DA_DROP_ASSERTION  
  
 Um driver em conformidade com o nível completo do SQL-92 sempre retornará essa opção com suporte.  
  
 SQL_DROP_CHARACTER_SET (ODBC 3.0)  
 Um bitmask SQLUINTEGER enumerando as cláusulas no **descartar o conjunto de caracteres** instrução, conforme definido em SQL-92, suportado pela fonte de dados.  
  
 A máscara de bits a seguir é usada para determinar quais cláusulas são suportadas:  
  
 SQL_DCS_DROP_CHARACTER_SET  
  
 Um driver em conformidade com o nível completo do SQL-92 sempre retornará essa opção com suporte.  
  
 SQL_DROP_COLLATION (ODBC 3.0)  
 Um bitmask SQLUINTEGER enumerando as cláusulas no **remover AGRUPAMENTO** instrução, conforme definido em SQL-92, suportado pela fonte de dados.  
  
 A máscara de bits a seguir é usada para determinar quais cláusulas são suportadas:  
  
 SQL_DC_DROP_COLLATION  
  
 Um driver em conformidade com o nível completo do SQL-92 sempre retornará essa opção com suporte.  
  
 SQL_DROP_DOMAIN (ODBC 3.0)  
 Um bitmask SQLUINTEGER enumerando as cláusulas no **remover domínio** instrução, conforme definido em SQL-92, suportado pela fonte de dados.  
  
 Bitmasks a seguir são usados para determinar quais cláusulas são suportadas:  
  
 SQL_DD_DROP_DOMAINSQL_DD_CASCADESQL_DD_RESTRICT  
  
 Um driver em conformidade com o nível intermediário do SQL-92 sempre retornará todas essas opções com suporte.  
  
 SQL_DROP_SCHEMA (ODBC 3.0)  
 Um bitmask SQLUINTEGER enumerando as cláusulas no **DROP SCHEMA** instrução, conforme definido em SQL-92, suportado pela fonte de dados.  
  
 Bitmasks a seguir são usados para determinar quais cláusulas são suportadas:  
  
 SQL_DS_DROP_SCHEMASQL_DS_CASCADESQL_DS_RESTRICT  
  
 Um driver em conformidade com o nível intermediário do SQL-92 sempre retornará todas essas opções com suporte.  
  
 SQL_DROP_TABLE (ODBC 3.0)  
 Um bitmask SQLUINTEGER enumerando as cláusulas no **DROP TABLE** instrução, conforme definido em SQL-92, suportado pela fonte de dados.  
  
 Bitmasks a seguir são usados para determinar quais cláusulas são suportadas:  
  
 SQL_DT_DROP_TABLESQL_DT_CASCADESQL_DT_RESTRICT  
  
 Um driver de nível em conformidade com FIPS transição sempre retornará todas essas opções com suporte.  
  
 SQL_DROP_TRANSLATION (ODBC 3.0)  
 Um bitmask SQLUINTEGER enumerando as cláusulas no **DROP tradução** instrução, conforme definido em SQL-92, suportado pela fonte de dados.  
  
 A máscara de bits a seguir é usada para determinar quais cláusulas são suportadas:  
  
 SQL_DTR_DROP_TRANSLATION  
  
 Um driver em conformidade com o nível completo do SQL-92 sempre retornará essa opção com suporte.  
  
 SQL_DROP_VIEW (ODBC 3.0)  
 Um bitmask SQLUINTEGER enumerando as cláusulas no **DROP VIEW** instrução, conforme definido em SQL-92, suportado pela fonte de dados.  
  
 Bitmasks a seguir são usados para determinar quais cláusulas são suportadas:  
  
 SQL_DV_DROP_VIEWSQL_DV_CASCADESQL_DV_RESTRICT  
  
 Um driver de nível em conformidade com FIPS transição sempre retornará todas essas opções com suporte.  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 Um bitmask SQLUINTEGER que descreve os atributos de um cursor dinâmico que são suportados pelo driver. Esse bitmask contém o primeiro subconjunto de atributos; para o subconjunto de segundo, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES2.  
  
 Bitmasks a seguir são usados para determinar quais atributos têm suporte:  
  
 SQL_CA1_NEXT = A *FetchOrientation* argumento de SQL_FETCH_NEXT é suportado em uma chamada para **SQLFetchScroll** quando o cursor é dinâmico.  
  
 SQL_CA1_ABSOLUTE = *FetchOrientation* argumentos de SQL_FETCH_FIRST, SQL_FETCH_LAST e SQL_FETCH_ABSOLUTE são suportados em uma chamada para **SQLFetchScroll** quando o cursor é dinâmico. (O conjunto de linhas que será buscado é independente da posição do cursor atual.)  
  
 SQL_CA1_RELATIVE = *FetchOrientation* argumentos de SQL_FETCH_PRIOR e SQL_FETCH_RELATIVE têm suporte em uma chamada para **SQLFetchScroll** quando o cursor é dinâmico. (O conjunto de linhas que será buscado depende da posição atual do cursor. Observe que isso é separado do SQL_FETCH_NEXT porque em um cursor somente encaminhamento, SQL_FETCH_NEXT só é suportada.)  
  
 SQL_CA1_BOOKMARK = A *FetchOrientation* argumento de SQL_FETCH_BOOKMARK é suportado em uma chamada para **SQLFetchScroll** quando o cursor é dinâmico.  
  
 SQL_CA1_LOCK_EXCLUSIVE = A *LockType* argumento de SQL_LOCK_EXCLUSIVE é suportado em uma chamada para **SQLSetPos** quando o cursor é dinâmico.  
  
 SQL_CA1_LOCK_NO_CHANGE = A *LockType* argumento de SQL_LOCK_NO_CHANGE é suportado em uma chamada para **SQLSetPos** quando o cursor é dinâmico.  
  
 SQL_CA1_LOCK_UNLOCK = A *LockType* argumento de SQL_LOCK_UNLOCK é suportado em uma chamada para **SQLSetPos** quando o cursor é dinâmico.  
  
 SQL_CA1_POS_POSITION = um *operação* argumento de SQL_POSITION é suportado em uma chamada para **SQLSetPos** quando o cursor é dinâmico.  
  
 SQL_CA1_POS_UPDATE = um *operação* argumento de SQL_UPDATE é suportado em uma chamada para **SQLSetPos** quando o cursor é dinâmico.  
  
 SQL_CA1_POS_DELETE = um *operação* argumento de SQL_DELETE é suportado em uma chamada para **SQLSetPos** quando o cursor é dinâmico.  
  
 SQL_CA1_POS_REFRESH = um *operação* argumento de SQL_REFRESH é suportado em uma chamada para **SQLSetPos** quando o cursor é dinâmico.  
  
 SQL_CA1_POSITIONED_UPDATE = uma atualização onde atual do SQL instrução é suportada quando o cursor é dinâmico. (Um driver em conformidade com o nível de entrada do SQL-92 sempre retornará essa opção com suporte.)  
  
 SQL_CA1_POSITIONED_DELETE = A excluir onde atual do SQL instrução é suportada quando o cursor é dinâmico. (Um driver em conformidade com o nível de entrada do SQL-92 sempre retornará essa opção com suporte.)  
  
 SQL_CA1_SELECT_FOR_UPDATE = SELECT para instrução UPDATE SQL tem suporte quando o cursor é dinâmico. (Um driver em conformidade com o nível de entrada do SQL-92 sempre retornará essa opção com suporte.)  
  
 SQL_CA1_BULK_ADD = um *operação* argumento de SQL_ADD é suportado em uma chamada para **SQLBulkOperations** quando o cursor é dinâmico.  
  
 SQL_CA1_BULK_UPDATE_BY_BOOKMARK = um *operação* argumento de SQL_UPDATE_BY_BOOKMARK é suportado em uma chamada para **SQLBulkOperations** quando o cursor é dinâmico.  
  
 SQL_CA1_BULK_DELETE_BY_BOOKMARK = um *operação* argumento de SQL_DELETE_BY_BOOKMARK é suportado em uma chamada para **SQLBulkOperations** quando o cursor é dinâmico.  
  
 SQL_CA1_BULK_FETCH_BY_BOOKMARK = um *operação* argumento de SQL_FETCH_BY_BOOKMARK é suportado em uma chamada para **SQLBulkOperations** quando o cursor é dinâmico.  
  
 Um driver em conformidade com o nível intermediário do SQL-92 geralmente retornará as opções SQL_CA1_NEXT, SQL_CA1_ABSOLUTE e SQL_CA1_RELATIVE com suporte, porque ele dá suporte a cursores roláveis por meio da instrução de SQL BUSCAR incorporada. Porque isso não determinam diretamente o suporte a SQL subjacente, no entanto, cursores roláveis podem não ter suporte, mesmo para um driver em conformidade com o nível intermediário do SQL-92.  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 Um bitmask SQLUINTEGER que descreve os atributos de um cursor dinâmico que são suportados pelo driver. Esse bitmask contém o subconjunto de segundo de atributos; para o subconjunto primeiro, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES1.  
  
 Bitmasks a seguir são usados para determinar quais atributos têm suporte:  
  
 SQL_CA2_READ_ONLY_CONCURRENCY = somente leitura cursor dinâmico, em que não são permitidas atualizações, há suporte. (O atributo de instrução SQL_ATTR_CONCURRENCY pode ser SQL_CONCUR_READ_ONLY para um cursor dinâmico).  
  
 SQL_CA2_LOCK_CONCURRENCY = um cursor dinâmico que usa o nível mais baixo de bloqueio suficientes para certificar-se de que a linha pode ser atualizada é suportada. (O atributo de instrução SQL_ATTR_CONCURRENCY pode ser SQL_CONCUR_LOCK para um cursor dinâmico). Esses bloqueios devem ser consistentes com o nível de isolamento de transação definido pelo atributo SQL_ATTR_TXN_ISOLATION conexão.  
  
 SQL_CA2_OPT_ROWVER_CONCURRENCY = um cursor dinâmico que usa as versões de linha de comparação do controle de simultaneidade otimista é suportado. (O atributo de instrução SQL_ATTR_CONCURRENCY pode ser SQL_CONCUR_ROWVER para um cursor dinâmico).  
  
 SQL_CA2_OPT_VALUES_CONCURRENCY = um cursor dinâmico que usa os valores de comparação de controle de simultaneidade otimista é suportado. (O atributo de instrução SQL_ATTR_CONCURRENCY pode ser SQL_CONCUR_VALUES para um cursor dinâmico).  
  
 SQL_CA2_SENSITIVITY_ADDITIONS = adicionado linhas são visíveis para um cursor dinâmico; o cursor pode rolar a essas linhas. (Onde essas linhas são adicionadas ao cursor depende do driver.)  
  
 SQL_CA2_SENSITIVITY_DELETIONS = excluídas linhas não estão mais disponíveis para um cursor dinâmico e não deixe um "buraco" no conjunto de resultados; Após rola o cursor dinâmico de uma linha excluída, ela não pode retornar a essa linha.  
  
 SQL_CA2_SENSITIVITY_UPDATES = atualizações para linhas são visíveis para um cursor dinâmico; Se o cursor dinâmico rola do e retorna para uma linha atualizada, os dados retornados pelo cursor são os dados atualizados, não os dados originais.  
  
 SQL_CA2_MAX_ROWS_SELECT = SQL_ATTR_MAX_ROWS a instrução atributo afeta **selecione** instruções quando o cursor é dinâmico.  
  
 SQL_CA2_MAX_ROWS_INSERT = SQL_ATTR_MAX_ROWS a instrução atributo afeta **inserir** instruções quando o cursor é dinâmico.  
  
 SQL_CA2_MAX_ROWS_DELETE = SQL_ATTR_MAX_ROWS a instrução atributo afeta **excluir** instruções quando o cursor é dinâmico.  
  
 SQL_CA2_MAX_ROWS_UPDATE = SQL_ATTR_MAX_ROWS a instrução atributo afeta **atualização** instruções quando o cursor é dinâmico.  
  
 SQL_CA2_MAX_ROWS_CATALOG = SQL_ATTR_MAX_ROWS a instrução atributo afeta **catálogo** conjuntos de resultados quando o cursor é dinâmico.  
  
 SQL_CA2_MAX_ROWS_AFFECTS_ALL = SQL_ATTR_MAX_ROWS a instrução atributo afeta **selecione**, **inserir**, **excluir**, e **atualização** instruções e **catálogo** os conjuntos de resultados, quando o cursor é dinâmico.  
  
 SQL_CA2_CRC_EXACT = exato contagem de linhas está disponível no campo de diagnóstico SQL_DIAG_CURSOR_ROW_COUNT quando o cursor é dinâmico.  
  
 SQL_CA2_CRC_APPROXIMATE = um aproximado contagem de linhas está disponível no campo de diagnóstico SQL_DIAG_CURSOR_ROW_COUNT quando o cursor é dinâmico.  
  
 SQL_CA2_SIMULATE_NON_UNIQUE = o driver garante que simulados posicionado atualização ou instruções delete afeta somente uma linha quando o cursor é um cursor dinâmico; é responsabilidade do aplicativo para garantir isso. (Se uma instrução afeta mais de uma linha, **SQLExecute** ou **SQLExecDirect** retornará SQLSTATE 01001 [conflito de operação de Cursor].) Para definir esse comportamento, o aplicativo chama **SQLSetStmtAttr** com o SQL_ATTR_SIMULATE_CURSOR atributo definido como SQL_SC_NON_UNIQUE.  
  
 SQL_CA2_SIMULATE_TRY_UNIQUE = o driver tentará garante que atualização posicionada simulada ou instruções delete afetará apenas uma linha quando o cursor é dinâmico. O driver sempre executa essas instruções, mesmo se eles podem afetar a mais de uma linha, como quando não há nenhuma chave exclusiva. (Se uma instrução afeta mais de uma linha, **SQLExecute** ou **SQLExecDirect** retornará SQLSTATE 01001 [conflito de operação de Cursor].) Para definir esse comportamento, o aplicativo chama **SQLSetStmtAttr** com o SQL_ATTR_SIMULATE_CURSOR atributo definido como SQL_SC_TRY_UNIQUE.  
  
 SQL_CA2_SIMULATE_UNIQUE = o driver garante que simulados posicionado atualização ou instruções delete afeta somente uma linha quando o cursor é dinâmico. Se o driver não pode garantir isso para uma determinada instrução, **SQLExecDirect** ou **SQLPrepare** retornar SQLSTATE 01001 (conflito de operação de Cursor). Para definir esse comportamento, o aplicativo chama **SQLSetStmtAttr** com o SQL_ATTR_SIMULATE_CURSOR atributo definido como SQL_SC_UNIQUE.  
  
 SQL_EXPRESSIONS_IN_ORDERBY ODBC (1.0)  
 Uma cadeia de caracteres: "Y" se a fonte de dados oferece suporte a expressões de **ORDER BY** lista; "N" se não existir.  
  
 SQL_FILE_USAGE (ODBC 2.0)  
 Um valor SQLUSMALLINT que indica como um driver de camada única trata diretamente os arquivos em uma fonte de dados:  
  
 SQL_FILE_NOT_SUPPORTED = o driver não é um driver de camada única. Por exemplo, um driver ORACLE é um driver de duas camadas.  
  
 SQL_FILE_TABLE = arquivos de trata um driver de camada única em uma fonte de dados como tabelas. Por exemplo, um driver Xbase trata cada arquivo Xbase como uma tabela.  
  
 SQL_FILE_CATALOG = arquivos de trata um driver de camada única em uma fonte de dados como um catálogo. Por exemplo, um driver do Microsoft Access trata cada arquivo do Microsoft Access como um banco de dados completo.  
  
 Um aplicativo pode usar isso para determinar como os usuários irão selecionar dados. Por exemplo, usuários Xbase geralmente pensar de dados armazenados em arquivos, enquanto os usuários do ORACLE e o Microsoft Access geralmente pensar dados conforme armazenados nas tabelas.  
  
 Quando um usuário seleciona uma fonte de dados Xbase, o aplicativo pode exibir as janelas **abrir arquivo** caixa de diálogo comum; quando o usuário seleciona uma fonte de dados do Microsoft Access ou ORACLE, o aplicativo pode exibir um personalizado  **Selecione a tabela** caixa de diálogo.  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 Um bitmask SQLUINTEGER que descreve os atributos de um cursor somente de encaminhamento com suporte pelo driver. Esse bitmask contém o primeiro subconjunto de atributos; para o subconjunto de segundo, consulte SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2.  
  
 Bitmasks a seguir são usados para determinar quais atributos têm suporte:  
  
 SQL_CA1_NEXTSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_ UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 Para obter descrições desses bitmasks, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (e substitua "cursor somente de avanço" para "cursor dinâmico" nas descrições de).  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 Um bitmask SQLUINTEGER que descreve os atributos de um cursor somente de encaminhamento com suporte pelo driver. Esse bitmask contém o subconjunto de segundo de atributos; para o subconjunto primeiro, consulte SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1.  
  
 Bitmasks a seguir são usados para determinar quais atributos têm suporte:  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_ CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_ SIMULATE_UNIQUE  
  
 Para obter descrições desses bitmasks, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES2 (e substitua "cursor somente de avanço" para "cursor dinâmico" nas descrições de).  
  
 SQL_GETDATA_EXTENSIONS (ODBC 2.0)  
 Um bitmask SQLUINTEGER enumerando extensões **SQLGetData**.  
  
 Bitmasks a seguir são usadas junto com o sinalizador para determinar quais extensões comuns que o driver dá suporte para **SQLGetData**:  
  
 SQL_GD_ANY_COLUMN = **SQLGetData** pode ser chamado para qualquer coluna desvinculada, incluindo aqueles antes da última coluna associada. Observe que as colunas devem ser chamadas em ordem crescente número de coluna, a menos que SQL_GD_ANY_ORDER também é retornado.  
  
 SQL_GD_ANY_ORDER = **SQLGetData** pode ser chamado para colunas desassociadas em qualquer ordem. Observe que **SQLGetData** pode ser chamado somente para colunas depois da última coluna associada, a menos que SQL_GD_ANY_COLUMN também é retornado.  
  
 SQL_GD_BLOCK = **SQLGetData** pode ser chamado para uma coluna não associada em qualquer linha em um bloco (onde o tamanho do conjunto de linhas é maior que 1) de dados após o posicionamento em linha com **SQLSetPos**.  
  
 SQL_GD_BOUND = **SQLGetData** pode ser chamado para colunas associadas, além de colunas não associadas. Um driver não pode retornar esse valor, a menos que ele também retorna SQL_GD_ANY_COLUMN.  
  
 SQL_GD_OUTPUT_PARAMS = **SQLGetData** pode ser chamado para retornar valores de parâmetro de saída. Para obter mais informações, consulte [recuperar parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
 **SQLGetData** é necessário para retornar dados somente de colunas desassociadas que ocorrem após a última coluna, associada são chamados em ordem crescente número de coluna e não estão em uma linha em um bloco de linhas.  
  
 Se um driver dá suporte a indicadores (comprimento fixo ou comprimento variável), deverá dar suporte a chamada **SQLGetData** na coluna 0. Esse suporte é necessária, independentemente do que o driver retorna para uma chamada para **SQLGetInfo** com o SQL_GETDATA_EXTENSIONS *informação*.  
  
 SQL_GROUP_BY (ODBC 2.0)  
 Um valor SQLUSMALLINT que especifica a relação entre as colunas a **GROUP BY** cláusula e as colunas agregadas na lista de seleção:  
  
 SQL_GB_COLLATE = A **COLLATE** cláusula pode ser especificada no final de cada coluna de agrupamento. (ODBC 3.0)  
  
 SQL_GB_NOT_SUPPORTED = **GROUP BY** cláusulas não são suportadas. (ODBC 2.0)  
  
 SQL_GB_GROUP_BY_EQUALS_SELECT = o **GROUP BY** cláusula deve conter todas as colunas agregadas na lista de seleção. Ele não pode conter todas as outras colunas. Por exemplo, **selecione departamento, MAX(SALARY) do funcionário GROUP BY departamento**. (ODBC 2.0)  
  
 SQL_GB_GROUP_BY_CONTAINS_SELECT = o **GROUP BY** cláusula deve conter todas as colunas agregadas na lista de seleção. Ele pode conter colunas que não estão na lista de seleção. Por exemplo, **selecione departamento, MAX(SALARY) do funcionário GROUP BY departamento, IDADE**. (ODBC 2.0)  
  
 SQL_GB_NO_RELATION = as colunas a **GROUP BY** cláusula e lista de seleção não estão relacionadas. O significado de colunas nongrouped, agregados na lista de seleção é – dependente da fonte de dados. Por exemplo, **selecione departamento, SALÁRIO do funcionário GROUP BY departamento, IDADE**. (ODBC 2.0)  
  
 Um driver em conformidade com o nível de entrada do SQL-92 sempre retornará a opção SQL_GB_GROUP_BY_EQUALS_SELECT com suporte. Um driver em conformidade com o nível completo do SQL-92 sempre retornará a opção SQL_GB_COLLATE com suporte. Se nenhuma das opções for compatível, o **GROUP BY** cláusula não é suportada pela fonte de dados.  
  
 SQL_IDENTIFIER_CASE ODBC (1.0)  
 Um SQLUSMALLINT valor da seguinte maneira:  
  
 SQL_IC_UPPER = identificadores em SQL não diferenciam maiusculas de minúsculas e são armazenados em letras maiusculas no catálogo do sistema.  
  
 SQL_IC_LOWER = identificadores em SQL não diferenciam maiusculas de minúsculas e são armazenados em minúsculas no catálogo do sistema.  
  
 SQL_IC_SENSITIVE = identificadores SQL diferenciam maiusculas de minúsculas e são armazenados em maiusculas e minúsculas no catálogo do sistema.  
  
 SQL_IC_MIXED = identificadores em SQL não diferenciam maiusculas de minúsculas e são armazenados em maiusculas e minúsculas no catálogo do sistema.  
  
 Como os identificadores SQL-92 nunca diferenciam maiusculas de minúsculas, um driver estritamente compatível com SQL-92 (qualquer nível) nunca retornarão a opção SQL_IC_SENSITIVE com suporte.  
  
 SQL_IDENTIFIER_QUOTE_CHAR ODBC (1.0)  
 A cadeia de caracteres que é usada como o delimitador inicial e final de um entre aspas () identificador delimitado em instruções SQL. (Identificadores transmitidos como argumentos para funções de ODBC não precisa ser colocado entre aspas.) Se a fonte de dados não dá suporte a identificadores entre aspas, um espaço em branco será retornado.  
  
 Essa cadeia de caracteres também pode ser usada para delimitar os argumentos da função de catálogo quando o atributo de conexão SQL_ATTR_METADATA_ID é definido como SQL_TRUE.  
  
 Como o caractere de aspas de identificador em SQL-92 aspas duplas ("), um driver compatível estritamente ao SQL-92 sempre retornará o caractere de aspas duplas.  
  
 SQL_INDEX_KEYWORDS (ODBC 3.0)  
 Um bitmask SQLUINTEGER que enumera as palavras-chave na instrução CREATE INDEX com suporte pelo driver:  
  
 SQL_IK_NONE = nenhum as palavras-chave tem suporte.  
  
 SQL_IK_ASC = ASC há suporte para a palavra-chave.  
  
 SQL_IK_DESC = DESC há suporte para a palavra-chave.  
  
 SQL_IK_ALL = todas as palavras-chave têm suporte.  
  
 Para ver se a instrução CREATE INDEX tem suporte, um aplicativo chama **SQLGetInfo** com o tipo de informação SQL_DLL_INDEX.  
  
 SQL_INFO_SCHEMA_VIEWS (ODBC 3.0)  
 Um bitmask SQLUINTEGER enumerando as exibições no INFORMATION_SCHEMA que são suportadas pelo driver. As exibições no e o conteúdo de INFORMATION_SCHEMA são definidos em SQL-92.  
  
 O nível de conformidade FIPS ou de SQL-92 em que esse recurso deve ser suportado é mostrado entre parênteses ao lado de cada máscara de bits.  
  
 Bitmasks a seguir são usados para determinar quais modos de exibição têm suporte:  
  
 SQL_ISV_ASSERTIONS = identifica as asserções do catálogo que são de propriedade de um determinado usuário. (Nível completo)  
  
 SQL_ISV_CHARACTER_SETS = identifica conjuntos de caracteres do catálogo que pode ser acessada por um determinado usuário. (Nível intermediário)  
  
 SQL_ISV_CHECK_CONSTRAINTS = identifica a verificação de restrições que são propriedade de um determinado usuário. (Nível intermediário)  
  
 SQL_ISV_COLLATIONS = identifica os agrupamentos de caracteres para o catálogo que podem ser acessados por um determinado usuário. (Nível completo)  
  
 SQL_ISV_COLUMN_DOMAIN_USAGE = identifica colunas para o catálogo dependem domínios definidos no catálogo e pertencem a um determinado usuário. (Nível intermediário)  
  
 SQL_ISV_COLUMN_PRIVILEGES = identifica os privilégios em colunas de tabelas persistentes que estão disponíveis para ou concedido por um determinado usuário. (FIPS transição nível)  
  
 SQL_ISV_COLUMNS = identifica as colunas de tabelas persistentes que podem ser acessadas por um determinado usuário. (FIPS transição nível)  
  
 SQL_ISV_CONSTRAINT_COLUMN_USAGE = semelhante ao modo de exibição CONSTRAINT_TABLE_USAGE, colunas são identificadas para várias restrições que são de propriedade de um determinado usuário. (Nível intermediário)  
  
 SQL_ISV_CONSTRAINT_TABLE_USAGE = identifica as tabelas que são usadas por restrições (referencial, exclusivo e declarações) e são de propriedade de um determinado usuário. (Nível intermediário)  
  
 SQL_ISV_DOMAIN_CONSTRAINTS = identifica as restrições de domínio (dos domínios no catálogo) que podem ser acessadas por um determinado usuário. (Nível intermediário)  
  
 SQL_ISV_DOMAINS = identifica os domínios definidos em um catálogo que pode ser acessado pelo usuário. (Nível intermediário)  
  
 SQL_ISV_KEY_COLUMN_USAGE = colunas identifica definidas no catálogo que são restringidas como chaves de um determinado usuário. (Nível intermediário)  
  
 SQL_ISV_REFERENTIAL_CONSTRAINTS = identifica as restrições referenciais pertencentes a um determinado usuário. (Nível intermediário)  
  
 SQL_ISV_SCHEMATA = identifica os esquemas que pertencem a um determinado usuário. (Nível intermediário)  
  
 SQL_ISV_SQL_LANGUAGES = identifica os níveis de conformidade de SQL e opções de dialetos suportados pela implementação de SQL. (Nível intermediário)  
  
 SQL_ISV_TABLE_CONSTRAINTS = identifica as restrições de tabela que são de propriedade de um determinado usuário. (Nível intermediário)  
  
 SQL_ISV_TABLE_PRIVILEGES = identifica os privilégios em tabelas persistentes que estão disponíveis para ou concedido por um determinado usuário. (FIPS transição nível)  
  
 SQL_ISV_TABLES = identifica as tabelas persistentes definidas em um catálogo que pode ser acessado por um determinado usuário. (FIPS transição nível)  
  
 SQL_ISV_TRANSLATIONS = identifica conversões de caracteres para o catálogo que podem ser acessados por um determinado usuário. (Nível completo)  
  
 SQL_ISV_USAGE_PRIVILEGES = identifica o uso de privilégios em objetos de catálogo que estão disponíveis para ou de propriedade de um determinado usuário. (FIPS transição nível)  
  
 SQL_ISV_VIEW_COLUMN_USAGE = identifica as colunas no qual o catálogo exibições que pertencem a um determinado usuário são dependentes. (Nível intermediário)  
  
 SQL_ISV_VIEW_TABLE_USAGE = identifica as tabelas em que o catálogo exibições que pertencem a um determinado usuário são dependentes. (Nível intermediário)  
  
 SQL_ISV_VIEWS = identifica as tabelas exibidas definidas neste catálogo que podem ser acessados por um determinado usuário. (FIPS transição nível)  
  
 SQL_INSERT_STATEMENT (ODBC 3.0)  
 Um bitmask SQLUINTEGER que indica o suporte para **inserir** instruções:  
  
 SQL_IS_INSERT_LITERALS  
  
 SQL_IS_INSERT_SEARCHED  
  
 SQL_IS_SELECT_INTO  
  
 Um driver em conformidade com o nível de entrada do SQL-92 sempre retornará todas essas opções com suporte.  
  
 SQL_INTEGRITY ODBC (1.0)  
 Uma cadeia de caracteres: "Y" se a fonte de dados oferece suporte a Integrity Enhancement Facility; "N" se não existir.  
  
 Isso *informação* foi renomeado para ODBC 3.0 do ODBC 2.0 *informação* SQL_ODBC_SQL_OPT_IEF.  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 Um bitmask SQLUINTEGER que descreve os atributos de um cursor de conjunto de chaves que são suportados pelo driver. Esse bitmask contém o primeiro subconjunto de atributos; para o subconjunto de segundo, consulte SQL_KEYSET_CURSOR_ATTRIBUTES2.  
  
 Bitmasks a seguir são usados para determinar quais atributos têm suporte:  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_ UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 Para obter descrições desses bitmasks, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (e substitua "cursor controlado por" para "cursor dinâmico" nas descrições de).  
  
 Um driver em conformidade com o nível intermediário do SQL-92 geralmente retornará as opções SQL_CA1_NEXT, SQL_CA1_ABSOLUTE e SQL_CA1_RELATIVE com suporte, porque o driver dá suporte a cursores roláveis por meio da instrução de SQL BUSCAR incorporada. Porque isso não determinam diretamente o suporte a SQL subjacente, no entanto, cursores roláveis podem não ter suporte, mesmo para um driver em conformidade com o nível intermediário do SQL-92.  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 Um bitmask SQLUINTEGER que descreve os atributos de um cursor de conjunto de chaves que são suportados pelo driver. Esse bitmask contém o subconjunto de segundo de atributos; para o subconjunto primeiro, consulte SQL_KEYSET_CURSOR_ATTRIBUTES1.  
  
 Bitmasks a seguir são usados para determinar quais atributos têm suporte:  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_ CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_ SIMULATE_UNIQUE  
  
 Para obter descrições desses bitmasks, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (e substitua "cursor controlado por" para "cursor dinâmico" nas descrições de).  
  
 SQL_KEYWORDS (ODBC 2.0)  
 Uma cadeia de caracteres que contém uma lista separada por vírgulas de todas as palavras-chave de específico de fonte de dados. Essa lista não contém palavras-chave específicas para ODBC ou palavras-chave usadas pela fonte de dados e ODBC. Esta lista representa todas as palavras-chave reservadas; aplicativos interoperáveis não devem usar essas palavras em nomes de objetos.  
  
 Para obter uma lista de palavras-chave ODBC, consulte [palavras-chave reservadas](../../../odbc/reference/appendixes/reserved-keywords.md) na [gramática de SQL do apêndice c:](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md). O **#define** valor SQL_ODBC_KEYWORDS contém uma lista separada por vírgulas das palavras-chave do ODBC.  
  
 Apêndice c: gramática SQL  
  
 SQL_LIKE_ESCAPE_CLAUSE (ODBC 2.0)  
 Uma cadeia de caracteres: "Y" se a fonte de dados oferece suporte a um caractere de escape de caractere de porcentagem (%) e sublinhado (_) de caractere em uma **como** predicado e o driver oferece suporte à sintaxe ODBC para definir um **como** predicado caractere de escape; "N" caso contrário.  
  
 SQL_MAX_ASYNC_CONCURRENT_STATEMENTS (ODBC 3.0)  
 Um valor SQLUINTEGER que especifica o número máximo de instruções simultâneas ativas no modo assíncrono e o driver pode dar suporte a uma determinada conexão. Se não há nenhum limite específico ou o limite é desconhecido, esse valor é zero.  
  
 SQL_MAX_BINARY_LITERAL_LEN (ODBC 2.0)  
 Um valor SQLUINTEGER que especifica o comprimento máximo (número de caracteres hexadecimais, excluindo o literal prefixo e sufixo retornado por **SQLGetTypeInfo**) de um binário literal em uma instrução SQL. Por exemplo, o binário 0xFFAA literal tem um comprimento de 4. Se não há nenhum tamanho máximo ou o comprimento é desconhecido, esse valor é definido como zero.  
  
 SQL_MAX_CATALOG_NAME_LEN ODBC (1.0)  
 Um valor SQLUSMALLINT que especifica o comprimento máximo de um nome de catálogo da fonte de dados. Se não há nenhum tamanho máximo ou o comprimento é desconhecido, esse valor é definido como zero.  
  
 Um driver de nível em conformidade com FIPS completo irá retornar pelo menos de 128.  
  
 Isso *informação* foi renomeado para ODBC 3.0 do ODBC 2.0 *informação* SQL_MAX_QUALIFIER_NAME_LEN.  
  
 SQL_MAX_CHAR_LITERAL_LEN (ODBC 2.0)  
 Um valor SQLUINTEGER que especifica o comprimento máximo (número de caracteres, excluindo o literal prefixo e sufixo retornado pela **SQLGetTypeInfo**) de um caractere literal em uma instrução SQL. Se não há nenhum tamanho máximo ou o comprimento é desconhecido, esse valor é definido como zero.  
  
 SQL_MAX_COLUMN_NAME_LEN ODBC (1.0)  
 Um valor SQLUSMALLINT que especifica o comprimento máximo de um nome de coluna na fonte de dados. Se não há nenhum tamanho máximo ou o comprimento é desconhecido, esse valor é definido como zero.  
  
 Um driver de nível em conformidade com FIPS entrada irá retornar pelo menos 18. Um driver de nível em conformidade com FIPS intermediário retornará, pelo menos, 128.  
  
 SQL_MAX_COLUMNS_IN_GROUP_BY (ODBC 2.0)  
 Um valor SQLUSMALLINT que especifica o número máximo de colunas permitido em uma **GROUP BY** cláusula. Se não há nenhum limite especificado ou o limite é desconhecido, esse valor é definido como zero.  
  
 Um driver de nível em conformidade com FIPS entrada irá retornar pelo menos 6. Um driver de nível em conformidade com FIPS intermediário irá retornar pelo menos 15.  
  
 SQL_MAX_COLUMNS_IN_INDEX (ODBC 2.0)  
 Um valor SQLUSMALLINT que especifica o número máximo de colunas permitido em um índice. Se não há nenhum limite especificado ou o limite é desconhecido, esse valor é definido como zero.  
  
 SQL_MAX_COLUMNS_IN_ORDER_BY (ODBC 2.0)  
 Um valor SQLUSMALLINT que especifica o número máximo de colunas permitido em uma **ORDER BY** cláusula. Se não há nenhum limite especificado ou o limite é desconhecido, esse valor é definido como zero.  
  
 Um driver de nível em conformidade com FIPS entrada irá retornar pelo menos 6. Um driver de nível em conformidade com FIPS intermediário irá retornar pelo menos 15.  
  
 SQL_MAX_COLUMNS_IN_SELECT (ODBC 2.0)  
 Um valor SQLUSMALLINT que especifica o número máximo de colunas permitido em uma lista de seleção. Se não há nenhum limite especificado ou o limite é desconhecido, esse valor é definido como zero.  
  
 Um driver de nível em conformidade com FIPS entrada retornará pelo menos 100. Um driver de nível em conformidade com FIPS intermediário irá retornar pelo menos 250.  
  
 SQL_MAX_COLUMNS_IN_TABLE (ODBC 2.0)  
 Um valor SQLUSMALLINT que especifica o número máximo de colunas permitido em uma tabela. Se não há nenhum limite especificado ou o limite é desconhecido, esse valor é definido como zero.  
  
 Um driver de nível em conformidade com FIPS entrada retornará pelo menos 100. Um driver de nível em conformidade com FIPS intermediário irá retornar pelo menos 250.  
  
 SQL_MAX_CONCURRENT_ACTIVITIES ODBC (1.0)  
 Um valor SQLUSMALLINT que especifica o número máximo de instruções ativas que o driver pode dar suporte para uma conexão. Uma instrução é definida como ativo se ele tiver resultados pendentes, com as linhas de significado do termo "resultados" de um **selecione** operação ou linhas afetadas por uma **inserir**, **atualização**, ou **Excluir** operação (por exemplo, uma contagem de linhas), ou se ele está em um estado NEED_DATA. Esse valor pode refletir um limite imposto pelo driver ou fonte de dados. Se não há nenhum limite especificado ou o limite é desconhecido, esse valor é definido como zero.  
  
 Isso *informação* foi renomeado para ODBC 3.0 do ODBC 2.0 *informação* SQL_ACTIVE_STATEMENTS.  
  
 SQL_MAX_CURSOR_NAME_LEN ODBC (1.0)  
 Um valor SQLUSMALLINT que especifica o comprimento máximo de um nome de cursor na fonte de dados. Se não há nenhum tamanho máximo ou o comprimento é desconhecido, esse valor é definido como zero.  
  
 Um driver de nível em conformidade com FIPS entrada irá retornar pelo menos 18. Um driver de nível em conformidade com FIPS intermediário retornará, pelo menos, 128.  
  
 SQL_MAX_DRIVER_CONNECTIONS ODBC (1.0)  
 Um valor SQLUSMALLINT que especifica o número máximo de conexões ativas que o driver pode dar suporte para um ambiente. Esse valor pode refletir um limite imposto pelo driver ou fonte de dados. Se não há nenhum limite especificado ou o limite é desconhecido, esse valor é definido como zero.  
  
 Isso *informação* foi renomeado para ODBC 3.0 do ODBC 2.0 *informação* SQL_ACTIVE_CONNECTIONS.  
  
 SQL_MAX_IDENTIFIER_LEN (ODBC 3.0)  
 Um SQLUSMALLINT que indica o tamanho máximo em caracteres que a fonte de dados oferece suporte para nomes definidos pelo usuário.  
  
 Um driver de nível em conformidade com FIPS entrada irá retornar pelo menos 18. Um driver de nível em conformidade com FIPS intermediário retornará, pelo menos, 128.  
  
 SQL_MAX_INDEX_SIZE (ODBC 2.0)  
 Um valor SQLUINTEGER que especifica o número máximo de bytes permitidos nos campos combinados de um índice. Se não há nenhum limite especificado ou o limite é desconhecido, esse valor é definido como zero.  
  
 SQL_MAX_PROCEDURE_NAME_LEN ODBC (1.0)  
 Um valor SQLUSMALLINT que especifica o comprimento máximo de um nome de procedimento na fonte de dados. Se não há nenhum tamanho máximo ou o comprimento é desconhecido, esse valor é definido como zero.  
  
 SQL_MAX_ROW_SIZE (ODBC 2.0)  
 Um valor SQLUINTEGER que especifica o comprimento máximo de uma única linha em uma tabela. Se não há nenhum limite especificado ou o limite é desconhecido, esse valor é definido como zero.  
  
 Um driver de nível em conformidade com FIPS entrada irá retornar pelo menos 2.000. Um driver de nível em conformidade com FIPS intermediário irá retornar pelo menos 8.000.  
  
 SQL_MAX_ROW_SIZE_INCLUDES_LONG (ODBC 3.0)  
 Uma cadeia de caracteres: "Y" se o tamanho máximo de linhas retornado para o tipo de informação SQL_MAX_ROW_SIZE inclui o tamanho de todas as colunas SQL_LONGVARCHAR e SQL_LONGVARBINARY na linha; "N" caso contrário.  
  
 SQL_MAX_SCHEMA_NAME_LEN ODBC (1.0)  
 Um valor SQLUSMALLINT que especifica o comprimento máximo de um nome de esquema na fonte de dados. Se não há nenhum tamanho máximo ou o comprimento é desconhecido, esse valor é definido como zero.  
  
 Um driver de nível em conformidade com FIPS entrada irá retornar pelo menos 18. Um driver de nível em conformidade com FIPS intermediário retornará, pelo menos, 128.  
  
 Isso *informação* foi renomeado para ODBC 3.0 do ODBC 2.0 *informação* SQL_MAX_OWNER_NAME_LEN.  
  
 SQL_MAX_STATEMENT_LEN (ODBC 2.0)  
 Um valor SQLUINTEGER que especifica o tamanho máximo (número de caracteres, incluindo espaços em branco) de uma instrução SQL. Se não há nenhum tamanho máximo ou o comprimento é desconhecido, esse valor é definido como zero.  
  
 SQL_MAX_TABLE_NAME_LEN ODBC (1.0)  
 Um valor SQLUSMALLINT que especifica o comprimento máximo de um nome de tabela na fonte de dados. Se não há nenhum tamanho máximo ou o comprimento é desconhecido, esse valor é definido como zero.  
  
 Um driver de nível em conformidade com FIPS entrada irá retornar pelo menos 18. Um driver de nível em conformidade com FIPS intermediário retornará, pelo menos, 128.  
  
 SQL_MAX_TABLES_IN_SELECT (ODBC 2.0)  
 Um valor SQLUSMALLINT que especifica o número máximo de tabelas permitido no **FROM** cláusula de um **selecione** instrução. Se não há nenhum limite especificado ou o limite é desconhecido, esse valor é definido como zero.  
  
 Um driver de nível em conformidade com FIPS entrada irá retornar pelo menos 15. Um driver de nível em conformidade com FIPS intermediário irá retornar pelo menos 50.  
  
 SQL_MAX_USER_NAME_LEN (ODBC 2.0)  
 Um valor SQLUSMALLINT que especifica o comprimento máximo de um nome de usuário na fonte de dados. Se não há nenhum tamanho máximo ou o comprimento é desconhecido, esse valor é definido como zero.  
  
 SQL_MULT_RESULT_SETS ODBC (1.0)  
 Uma cadeia de caracteres: "Y" se a fonte de dados oferece suporte a vários conjuntos de resultados, "N" se não existir.  
  
 Para obter mais informações sobre vários conjuntos de resultados, consulte [vários resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 SQL_MULTIPLE_ACTIVE_TXN ODBC (1.0)  
 Uma cadeia de caracteres: "Y" se o driver dá suporte a mais de uma transação ativa ao mesmo tempo, "N" se apenas uma transação pode estar ativa a qualquer momento.  
  
 As informações retornadas para este tipo de informação não é aplicável no caso de transações distribuídas.  
  
 SQL_NEED_LONG_DATA_LEN (ODBC 2.0)  
 Uma cadeia de caracteres: "Y" se a fonte de dados precisa do tamanho de um valor de dados long (o tipo de dados é um tipo de dados de específico de fonte de dados longos, SQL_LONGVARBINARY ou SQL_LONGVARCHAR) antes desse valor é enviado para a fonte de dados, "N" se não existir. Para obter mais informações, consulte [função SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) e [função SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
 SQL_NON_NULLABLE_COLUMNS ODBC (1.0)  
 Um valor SQLUSMALLINT que especifica se a fonte de dados oferece suporte a NOT NULL nas colunas:  
  
 SQL_NNC_NULL = todas as colunas devem ser anuláveis.  
  
 SQL_NNC_NON_NULL = colunas não podem ser anuláveis. (A fonte de dados oferece suporte a **não NULL** restrição de coluna no **CREATE TABLE** instruções.)  
  
 Um driver em conformidade com o nível de entrada do SQL-92 retornará SQL_NNC_NON_NULL.  
  
 SQL_NULL_COLLATION (ODBC 2.0)  
 Um valor SQLUSMALLINT que especifica onde os valores nulos são classificados em um conjunto de resultados:  
  
 SQL_NC_END = nulos são classificados no final do conjunto de resultados, independentemente das palavras-chave ASC ou DESC.  
  
 SQL_NC_HIGH = nulos são classificados na extremidade superior do conjunto de resultados, dependendo das palavras-chave ASC ou DESC.  
  
 SQL_NC_LOW = nulos são classificados na extremidade inferior do conjunto de resultados, dependendo das palavras-chave ASC ou DESC.  
  
 SQL_NC_START = nulos são classificados no início do conjunto de resultados, independentemente das palavras-chave ASC ou DESC.  
  
 SQL_NUMERIC_FUNCTIONS ODBC (1.0)  
 Observação: O tipo de informações foi introduzido no ODBC 1.0; cada máscara de bits é rotulada com a versão na qual ele foi introduzido.  
  
 Um bitmask SQLUINTEGER enumerando as funções numéricas escalares com suporte de driver e a fonte de dados associada.  
  
 Bitmasks a seguir são usados para determinar quais funções numéricas têm suporte:  
  
 SQL_FN_NUM_ABS (ODBC 1.0) SQL_FN_NUM_ACOS (ODBC 1.0) SQL_FN_NUM_ASIN (ODBC 1.0) SQL_FN_NUM_ATAN (ODBC 1.0) SQL_FN_NUM_ATAN2 SQL _ DO (ODBC 1.0) SQL_FN_NUM_CEILING (ODBC 1.0) SQL_FN_NUM_COS (ODBC 1.0) SQL_FN_NUM_COT (ODBC 1.0) SQL_FN_NUM_DEGREES (ODBC 2.0) FN_NUM_EXP (ODBC 1.0) SQL_FN_NUM_FLOOR (ODBC 1.0) SQL_FN_NUM_LOG (ODBC 1.0) SQL_FN_NUM_LOG10 SQL_FN_ DE SQL_FN_NUM_RAND (ODBC 1.0) (ODBC 2.0) SQL_FN_NUM_MOD (ODBC 1.0) SQL_FN_NUM_PI (ODBC 1.0) SQL_FN_NUM_POWER (ODBC 2.0) SQL_FN_NUM_RADIANS (ODBC 2.0) NUM_ROUND (ODBC 2.0) SQL_FN_NUM_SIGN (ODBC 1.0) SQL_FN_NUM_SIN (ODBC 1.0) SQL_FN_NUM_SQRT (ODBC 1.0) SQL_FN_NUM_TAN (ODBC 1.0) SQL_FN_NUM_TRUNCATE (ODBC 2.0)  
  
 SQL_ODBC_INTERFACE_CONFORMANCE (ODBC 3.0)  
 Um valor SQLUINTEGER que indica o nível de ODBC 3*. x* interface que é compatível com o driver.  
  
 SQL_OIC_CORE: O nível mínimo que todos os drivers ODBC são deve cumprir. Esse nível inclui elementos de interface básica, como funções de conexão, funções para preparar e executar uma instrução SQL, funções de metadados do conjunto de resultados básica, funções básicas de catálogo e assim por diante.  
  
 SQL_OIC_LEVEL1: Um nível, incluindo as principal funcionalidade de nível de conformidade de padrões, além de cursores roláveis, indicadores, posicionados atualiza e exclui e assim por diante.  
  
 SQL_OIC_LEVEL2: Um nível incluindo a funcionalidade do nível de conformidade de padrões do nível 1, mais recursos avançados, como cursores confidenciais; atualizar, excluir e atualizar indicadores; suporte de procedimento armazenado; funções de catálogo para chaves primárias e estrangeiras; suporte a vários catálogo; e assim por diante.  
  
 Para obter mais informações, consulte [níveis de conformidade de Interface](../../../odbc/reference/develop-app/interface-conformance-levels.md).  
  
 SQL_ODBC_VER ODBC (1.0)  
 Uma cadeia de caracteres com a versão do ODBC para o qual o Gerenciador de Driver está em conformidade. É a versão do formulário # #. # #. 0000, em que os dois primeiros dígitos são a versão principal e os dois dígitos são a versão secundária. Isso é implementado somente no Gerenciador de Driver.  
  
 SQL_OJ_CAPABILITIES (ODBC 2.01)  
 Um bitmask SQLUINTEGER ao enumerar os tipos de junções externas suportados pela fonte de dados e do driver. Bitmasks a seguir são usados para determinar quais tipos têm suporte:  
  
 SQL_OJ_LEFT = esquerda junções externas têm suporte.  
  
 SQL_OJ_RIGHT = direita junções externas têm suporte.  
  
 SQL_OJ_FULL = completo junções externas têm suporte.  
  
 SQL_OJ_NESTED = aninhadas junções externas têm suporte.  
  
 SQL_OJ_NOT_ORDERED = a coluna de nomes na cláusula ON da junção externa não precisam estar na mesma ordem que seus nomes de tabela do respectivos no **junção externa** cláusula.  
  
 SQL_OJ_INNER = interna tabela (a tabela à direita em uma junção externa esquerda) ou a tabela esquerda em uma junção externa direita também pode ser usada em uma inner join. Isso não se aplica a junções externas completas, que não têm uma tabela interna.  
  
 SQL_OJ_ALL_COMPARISON_OPS = a comparação operador na cláusula ON pode ser qualquer um dos operadores de comparação ODBC. Se este bit não for definido, o operador de comparação igual (=) pode ser usado em junções externas.  
  
 Se nenhuma dessas opções for retornada com suporte, não há suporte para nenhuma cláusula de junção externa.  
  
 Para obter informações sobre o suporte de operadores de junção relacional em uma instrução SELECT, conforme definido pelo SQL-92, consulte SQL_SQL92_RELATIONAL_JOIN_OPERATORS.  
  
 SQL_ORDER_BY_COLUMNS_IN_SELECT (ODBC 2.0)  
 Uma cadeia de caracteres: "Y" se as colunas de **ORDER BY** cláusula deve estar na lista de seleção; caso contrário, "N".  
  
 SQL_PARAM_ARRAY_ROW_COUNTS (ODBC 3.0)  
 Contagens de um SQLUINTEGER ao enumerar as propriedades do driver em relação à disponibilidade de linha em uma execução com parâmetros. Tem os seguintes valores:  
  
 SQL_PARC_BATCH = Individual contagens de linha estão disponíveis para cada conjunto de parâmetros. Isso é conceitualmente equivalente para o driver de geração de um lote de instruções SQL, uma para cada parâmetro definido na matriz. Informações de erro estendidas podem ser recuperadas por meio do campo de descritor SQL_PARAM_STATUS_PTR.  
  
 SQL_PARC_NO_BATCH = há contagem de apenas uma linha disponível, que é a contagem cumulativa de linhas resultante da execução da instrução para toda a matriz de parâmetros. Isso é conceitualmente equivalente para tratar a instrução junto com a matriz de parâmetro completa como uma unidade atômica. Erros são tratados da mesma, como se uma instrução foi executada.  
  
 SQL_PARAM_ARRAY_SELECTS (ODBC 3.0)  
 Define um SQLUINTEGER ao enumerar as propriedades do driver em relação à disponibilidade de resultado em uma execução com parâmetros. Tem os seguintes valores:  
  
 SQL_PAS_BATCH = há um resultado definido disponível por conjunto de parâmetros. Isso é conceitualmente equivalente para o driver de geração de um lote de instruções SQL, uma para cada parâmetro definido na matriz.  
  
 SQL_PAS_NO_BATCH = há apenas um conjunto de resultados, que representa o resultado cumulativo conjunto resultante da execução da instrução para a matriz completa de parâmetros. Isso é conceitualmente equivalente para tratar a instrução junto com a matriz de parâmetro completa como uma unidade atômica.  
  
 SQL_PAS_NO_SELECT = um driver não permite que uma instrução de geração de conjunto de resultados a ser executado com uma matriz de parâmetros.  
  
 SQL_PROCEDURE_TERM ODBC (1.0)  
 Uma cadeia de caracteres com o nome do fornecedor de fonte de dados para um procedimento. Por exemplo, "procedimento de banco de dados", "procedimento armazenado", "procedimento", "pacote" ou "consulta armazenada".  
  
 SQL_PROCEDURES ODBC (1.0)  
 Uma cadeia de caracteres: "Y" se a fonte de dados oferece suporte a procedimentos e o driver oferece suporte à sintaxe de invocação de procedimento ODBC; "N" caso contrário.  
  
 SQL_POS_OPERATIONS (ODBC 2.0)  
 Um bitmask sqlinteger que contém enumerando as operações de suporte em **SQLSetPos**.  
  
 As seguir bitmasks são usados junto com o sinalizador para determinar quais opções são suportadas.  
  
 SQL_POS_POSITION (ODBC 2.0) SQL_POS_REFRESH (ODBC 2.0) SQL_POS_UPDATE (ODBC 2.0) SQL_POS_DELETE (ODBC 2.0) SQL_POS_ADD (ODBC 2.0)  
  
 SQL_QUOTED_IDENTIFIER_CASE (ODBC 2.0)  
 Um SQLUSMALLINT valor da seguinte maneira:  
  
 SQL_IC_UPPER = Quoted identificadores em SQL não diferenciam maiusculas de minúsculas e são armazenados em letras maiusculas no catálogo do sistema.  
  
 SQL_IC_LOWER = Quoted identificadores em SQL não diferenciam maiusculas de minúsculas e são armazenados em minúsculas no catálogo do sistema.  
  
 SQL_IC_SENSITIVE = Quoted identificadores SQL diferenciam maiusculas de minúsculas e são armazenados em maiusculas e minúsculas no catálogo do sistema. (Em um banco de dados compatível com SQL-92, os identificadores entre aspas são sempre diferenciam maiusculas de minúsculas).  
  
 SQL_IC_MIXED = Quoted identificadores em SQL não diferenciam maiusculas de minúsculas e são armazenados em maiusculas e minúsculas no catálogo do sistema.  
  
 Um driver em conformidade com o nível de entrada do SQL-92 sempre retornará SQL_IC_SENSITIVE.  
  
 SQL_ROW_UPDATES ODBC (1.0)  
 Uma cadeia de caracteres: "Y" se um cursor controlado por ou misto mantém versões de linha ou para todos os valores buscados linhas e, portanto, podem detectar todas as atualizações que foram feitas em uma linha por qualquer usuário desde que a linha foi buscada pela última. (Isso se aplica apenas a atualizações, não para exclusões ou inserções.) O driver pode retornar o sinalizador SQL_ROW_UPDATED para o status de linha array quando **SQLFetchScroll** é chamado. Caso contrário, "N".  
  
 SQL_SCHEMA_TERM ODBC (1.0)  
 Uma cadeia de caracteres com o nome do fornecedor de fonte de dados para um esquema; Por exemplo, "proprietário", "ID de autorização" ou "Esquema".  
  
 A cadeia de caracteres pode ser retornada em superior, inferior ou maiusculas e minúsculas.  
  
 Um driver em conformidade com o nível de entrada do SQL-92 sempre retornará "esquema".  
  
 Isso *informação* foi renomeado para ODBC 3.0 do ODBC 2.0 *informação* SQL_OWNER_TERM.  
  
 SQL_SCHEMA_USAGE (ODBC 2.0)  
 Um bitmask SQLUINTEGER enumerando as instruções no qual os esquemas podem ser usados:  
  
 SQL_SU_DML_STATEMENTS = esquemas têm suporte em todas as instruções de linguagem de manipulação de dados: **selecione**, **inserir**, **atualização**, **excluir**e se suportado, **Selecione para atualizar** posicionado atualização e instruções delete.  
  
 SQL_SU_PROCEDURE_INVOCATION = esquemas têm suporte na instrução de chamada de procedimento ODBC.  
  
 SQL_SU_TABLE_DEFINITION = esquemas têm suporte em todas as instruções de definição de tabela: **CREATE TABLE**, **CREATE VIEW**, **ALTER TABLE**, **DROP TABLE** , e **DROP VIEW**.  
  
 SQL_SU_INDEX_DEFINITION = esquemas têm suporte em todas as instruções de definição de índice: **CREATE INDEX** e **DROP INDEX**.  
  
 SQL_SU_PRIVILEGE_DEFINITION = esquemas têm suporte em todas as instruções de definição de privilégio: **GRANT** e **REVOGAR**.  
  
 Um driver em conformidade com o nível de entrada do SQL-92 sempre retornará as opções SQL_SU_DML_STATEMENTS, SQL_SU_TABLE_DEFINITION e SQL_SU_PRIVILEGE_DEFINITION, pois tem suporte.  
  
 Isso *informação* foi renomeado para ODBC 3.0 do ODBC 2.0 *informação* SQL_OWNER_USAGE.  
  
 SQL_SCROLL_OPTIONS ODBC (1.0)  
 Observação: O tipo de informações foi introduzido no ODBC 1.0; cada máscara de bits é rotulada com a versão na qual ele foi introduzido.  
  
 Um bitmask SQLUINTEGER enumerando as opções de rolagem com suporte para cursores roláveis.  
  
 Bitmasks a seguir são usados para determinar quais opções são suportadas:  
  
 SQL_SO_FORWARD_ONLY = a cursor somente rola para frente. ODBC (1.0)  
  
 SQL_SO_STATIC = os dados no resultado do conjunto é estático. (ODBC 2.0)  
  
 SQL_SO_KEYSET_DRIVEN = a salva de driver e usa as chaves para cada linha no conjunto de resultados. ODBC (1.0)  
  
 SQL_SO_DYNAMIC = o driver mantém as chaves para cada linha no conjunto de linhas (o tamanho do conjunto de chaves é o mesmo que o tamanho do conjunto de linhas). ODBC (1.0)  
  
 SQL_SO_MIXED = o mantém as chaves do driver para cada linha no conjunto de chaves e o tamanho do conjunto de chaves é maior que o tamanho do conjunto de linhas. O cursor é controlado por dentro do conjunto de chaves e dinâmicos fora do conjunto de chaves. ODBC (1.0)  
  
 Para obter informações sobre cursores roláveis, consulte [cursores roláveis](../../../odbc/reference/develop-app/scrollable-cursors.md).  
  
 SQL_SEARCH_PATTERN_ESCAPE ODBC (1.0)  
 Uma cadeia de caracteres especificando que o driver dá suporte como um caractere de escape que permite o uso do sinal de porcentagem (%) e sublinhado metacaracteres de correspondência padrão (_) como caracteres válidos em padrões de pesquisa. Esse caractere de escape aplica-se somente para os argumentos da função de catálogo que dão suporte a cadeias de caracteres de pesquisa. Se essa cadeia de caracteres estiver vazia, o driver não oferece suporte a um caractere de escape padrão de pesquisa.  
  
 Como este tipo de informação não indica suporte geral do caractere de escape de **como** predicado, SQL-92 não inclui requisitos para essa cadeia de caracteres.  
  
 Isso *informação* é limitada às funções de catálogo. Para obter uma descrição do uso o caractere de escape em cadeias de caracteres de padrão de pesquisa, consulte [argumentos de valor padrão](../../../odbc/reference/develop-app/pattern-value-arguments.md).  
  
 SQL_SERVER_NAME ODBC (1.0)  
 Uma cadeia de caracteres com o nome de servidor específico de fonte de dados reais; útil quando um nome de fonte de dados é usado durante a **SQLConnect**, **SQLDriverConnect**, e **SQLBrowseConnect**.  
  
 SQL_SPECIAL_CHARACTERS (ODBC 2.0)  
 Uma cadeia de caracteres que contém todos os caracteres especiais (isto é, todos os caracteres, exceto à z, de À Z, 0 a 9 e sublinhado) que podem ser usados em um nome de identificador, como um nome de tabela, o nome da coluna ou o nome do índice, na fonte de dados. Por exemplo, "#$^". Se um identificador contém um ou mais desses caracteres, o identificador deve ser um identificador delimitado.  
  
 SQL_SQL_CONFORMANCE (ODBC 3.0)  
 Um valor SQLUINTEGER que indica o nível de suporte do driver do SQL-92:  
  
 SQL_SC_SQL92_ENTRY = entrada nível SQL-92 compatíveis.  
  
 SQL_SC_FIPS127_2_TRANSITIONAL = FIPS 127-2 a transição nível compatível.  
  
 SQL_SC_SQL92_FULL = nível completo compatível com o SQL-92.  
  
 SQL_SC_ SQL92_INTERMEDIATE = intermediário nível SQL-92 compatíveis.  
  
 SQL_SQL92_DATETIME_FUNCTIONS(ODBC 3.0)  
 Um bitmask SQLUINTEGER enumerando as funções escalares a data e hora que são suportadas pelo driver e a fonte de dados associados, conforme definido em SQL-92.  
  
 Bitmasks a seguir são usados para determinar quais funções de data e hora são suportadas:  
  
 SQL_SDF_CURRENT_DATESQL_SDF_CURRENT_TIMESQL_SDF_CURRENT_TIMESTAMP  
  
 SQL_SQL92_FOREIGN_KEY_DELETE_RULE(ODBC 3.0)  
 Um bitmask SQLUINTEGER ao enumerar as regras de suporte para uma chave estrangeira em uma **excluir** instrução, conforme definido em SQL-92.  
  
 Bitmasks a seguir são usados para determinar quais cláusulas são suportadas pela fonte de dados:  
  
 SQL_SFKD_CASCADESQL_SFKD_NO_ACTIONSQL_SFKD_SET_DEFAULTSQL_SFKD_SET_NULL  
  
 Um driver de nível em conformidade com FIPS transição sempre retornará todas essas opções com suporte.  
  
 SQL_SQL92_FOREIGN_KEY_UPDATE_RULE(ODBC 3.0)  
 Um bitmask SQLUINTEGER ao enumerar as regras de suporte para uma chave estrangeira em uma **atualização** instrução, conforme definido em SQL-92.  
  
 Bitmasks a seguir são usados para determinar quais cláusulas são suportadas pela fonte de dados:  
  
 SQL_SFKU_CASCADESQL_SFKU_NO_ACTIONSQL_SFKU_SET_DEFAULTSQL_SFKU_SET_NULL  
  
 Um driver em conformidade com o nível completo do SQL-92 sempre retornará todas essas opções com suporte.  
  
 SQL_SQL92_GRANT(ODBC 3.0)  
 Um bitmask SQLUINTEGER enumerando as cláusulas tem suportadas no **GRANT** instrução, conforme definido em SQL-92.  
  
 O nível de conformidade FIPS ou de SQL-92 em que esse recurso deve ser suportado é mostrado entre parênteses ao lado de cada máscara de bits.  
  
 Bitmasks a seguir são usados para determinar quais cláusulas são suportadas pela fonte de dados:  
  
 (SQL_SG_INSERT_COLUMN (nível intermediário) SQL_SG_INSERT_TABLE (nível de entrada) SQL_SG_REFERENCES_TABLE (nível de entrada) SQL_SG_REFERENCES_COLUMN (nível de entrada) SQL_SG_SELECT_TABLE (nível de entrada) SQL_SG_UPDATE_COLUMN SQL_SG_DELETE_TABLE (nível de entrada) Nível de entrada) SQL_SG_UPDATE_TABLE (nível de entrada) SQL_SG_USAGE_ON_DOMAIN (nível FIPS transição) SQL_SG_USAGE_ON_CHARACTER_SET (nível FIPS transição) SQL_SG_USAGE_ON_COLLATION (nível FIPS transição) SQL_SG_USAGE_ON_TRANSLATION (FIPS Nível de transição) SQL_SG_WITH_GRANT_OPTION (nível de entrada)  
  
 SQL_SQL92_NUMERIC_VALUE_FUNCTIONS(ODBC 3.0)  
 Um bitmask SQLUINTEGER enumerando as funções escalares do valor numérico que são suportadas pelo driver e a fonte de dados associados, conforme definido em SQL-92.  
  
 Bitmasks a seguir são usados para determinar quais funções numéricas têm suporte:  
  
 SQL_SNVF_BIT_LENGTHSQL_SNVF_CHAR_LENGTHSQL_SNVF_CHARACTER_LENGTHSQL_SNVF_EXTRACTSQL_SNVF_OCTET_LENGTHSQL_SNVF_POSITION  
  
 SQL_SQL92_PREDICATES(ODBC 3.0)  
 Um bitmask SQLUINTEGER ao enumerar os predicados com suporte em um **selecione** instrução, conforme definido em SQL-92.  
  
 O nível de conformidade FIPS ou de SQL-92 em que esse recurso deve ser suportado é mostrado entre parênteses ao lado de cada máscara de bits.  
  
 Bitmasks a seguir são usados para determinar quais opções são suportadas pela fonte de dados:  
  
 SQL_SP_BETWEEN (nível de entrada) SQL_SP_COMPARISON (nível de entrada) SQL_SP_EXISTS (nível de entrada) SQL_SP_IN (nível de entrada) SQL_SP_ISNOTNULL (nível de entrada) SQL_SP_ISNULL (nível de entrada) SQL_SP_LIKE (nível de entrada) SQL_SP_MATCH_FULL (nível completo) SQL_SP_MATCH_PARTIAL (Nível completo) SQL_SP_MATCH_UNIQUE_FULL (nível completo) SQL_SP_MATCH_UNIQUE_PARTIAL (nível completo) SQL_SP_OVERLAPS (nível FIPS transição) SQL_SP_QUANTIFIED_COMPARISON (nível de entrada) SQL_SP_UNIQUE (nível de entrada)  
  
 SQL_SQL92_RELATIONAL_JOIN_OPERATORS(ODBC 3.0)  
 Um bitmask SQLUINTEGER ao enumerar os operadores de junção relacional com suporte em um **selecione** instrução, conforme definido em SQL-92.  
  
 O nível de conformidade FIPS ou de SQL-92 em que esse recurso deve ser suportado é mostrado entre parênteses ao lado de cada máscara de bits.  
  
 Bitmasks a seguir são usados para determinar quais opções são suportadas pela fonte de dados:  
  
 SQL_SRJO_INTERSECT_JOIN SQL_SRJO_INNER_JOIN (nível FIPS transição) do SQL_SRJO_CORRESPONDING_CLAUSE (nível intermediário) SQL_SRJO_CROSS_JOIN (nível completo) SQL_SRJO_EXCEPT_JOIN (nível intermediário) SQL_SRJO_FULL_OUTER_JOIN (nível intermediário) (Nível intermediário) SQL_SRJO_LEFT_OUTER_JOIN (nível FIPS transição) SQL_SRJO_NATURAL_JOIN (nível FIPS transição) SQL_SRJO_RIGHT_OUTER_JOIN (nível FIPS transição) SQL_SRJO_UNION_JOIN (nível completo)  
  
 SQL_SRJO_INNER_JOIN indica suporte para o **INNER JOIN** sintaxe, não para o recurso de junção interna. Suporte para o **INNER JOIN** sintaxe é transição de FIPS, enquanto há suporte para o recurso de junção interna **entrada**.  
  
 SQL_SQL92_REVOKE(ODBC 3.0)  
 Um bitmask SQLUINTEGER enumerando as cláusulas tem suportadas no **REVOGAR** instrução, conforme definido em SQL-92, suportado pela fonte de dados.  
  
 O nível de conformidade FIPS ou de SQL-92 em que esse recurso deve ser suportado é mostrado entre parênteses ao lado de cada máscara de bits.  
  
 Bitmasks a seguir são usados para determinar quais cláusulas são suportadas pela fonte de dados:  
  
 SQL_SR_CASCADE (nível FIPS transição) SQL_SR_DELETE_TABLE (nível de entrada) SQL_SR_GRANT_OPTION_FOR (nível intermediário) SQL_SR_INSERT_COLUMN (nível intermediário) SQL_SR_INSERT_TABLE (nível de entrada) SQL_SR_REFERENCES_COLUMN (nível de entrada) SQL_SR_ REFERENCES_TABLE (nível de entrada) SQL_SR_RESTRICT (nível FIPS transição) SQL_SR_SELECT_TABLE (nível de entrada) SQL_SR_UPDATE_COLUMN (nível de entrada) SQL_SR_UPDATE_TABLE (nível de entrada) SQL_SR_USAGE_ON_DOMAIN (nível FIPS transição) SQL_SR_USAGE_ON_ CHARACTER_SET (nível FIPS transição) SQL_SR_USAGE_ON_COLLATION (nível FIPS transição) SQL_SR_USAGE_ON_TRANSLATION (FIPS transição nível)  
  
 SQL_SQL92_ROW_VALUE_CONSTRUCTOR(ODBC 3.0)  
 Um bitmask SQLUINTEGER enumerando as expressões de construtor de valor de linha com suporte em um **selecione** instrução, conforme definido em SQL-92. Bitmasks a seguir são usados para determinar quais opções são suportadas pela fonte de dados:  
  
 SQL_SRVC_VALUE_EXPRESSION SQL_SRVC_NULL SQL_SRVC_DEFAULT SQL_SRVC_ROW_SUBQUERY  
  
 SQL_SQL92_STRING_FUNCTIONS(ODBC 3.0)  
 Um bitmask SQLUINTEGER enumerando as funções escalares a cadeia de caracteres que são suportadas pelo driver e a fonte de dados associados, conforme definido em SQL-92.  
  
 Bitmasks a seguir são usados para determinar quais funções de cadeia de caracteres têm suporte:  
  
 SQL_SSF_CONVERTSQL_SSF_LOWERSQL_SSF_UPPERSQL_SSF_SUBSTRINGSQL_SSF_TRANSLATESQL_SSF_TRIM_BOTHSQL_SSF_TRIM_LEADINGSQL_SSF_TRIM_TRAILING  
  
 SQL_SQL92_VALUE_EXPRESSIONS(ODBC 3.0)  
 Um bitmask SQLUINTEGER enumerando as expressões de valor com suporte, conforme definido em SQL-92.  
  
 O nível de conformidade FIPS ou de SQL-92 em que esse recurso deve ser suportado é mostrado entre parênteses ao lado de cada máscara de bits.  
  
 Bitmasks a seguir são usados para determinar quais opções são suportadas pela fonte de dados:  
  
 SQL_SVE_CASE (nível intermediário) SQL_SVE_CAST (nível FIPS transição) SQL_SVE_COALESCE (nível intermediário) SQL_SVE_NULLIF (nível intermediário)  
  
 SQL_STANDARD_CLI_CONFORMANCE (ODBC 3.0)  
 Um bitmask SQLUINTEGER ao enumerar o padrão CLI ou padrões para o qual o driver está em conformidade. Bitmasks a seguir são usados para determinar qual o driver está em conformidade com os níveis:  
  
 SQL_SCC_XOPEN_CLI_VERSION1: O driver está em conformidade com a CLI do grupo aberto versão 1.  
  
 SQL_SCC_ISO92_CLI: O driver está em conformidade com ISO 92 CLI.  
  
 SQL_STATIC_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 Um bitmask SQLUINTEGER que descreve os atributos de um cursor estático que são suportados pelo driver. Esse bitmask contém o primeiro subconjunto de atributos; para o subconjunto de segundo, consulte SQL_STATIC_CURSOR_ATTRIBUTES2.  
  
 Bitmasks a seguir são usados para determinar quais atributos têm suporte:  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_ UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 Para obter descrições desses bitmasks, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (e substitua "cursor estático" para "cursor dinâmico" nas descrições de).  
  
 Um driver em conformidade com o nível intermediário do SQL-92 geralmente retornará as opções SQL_CA1_NEXT, SQL_CA1_ABSOLUTE e SQL_CA1_RELATIVE com suporte, porque o driver dá suporte a cursores roláveis por meio da instrução de SQL BUSCAR incorporada. Porque isso não determinam diretamente o suporte a SQL subjacente, no entanto, cursores roláveis podem não ter suporte, mesmo para um driver em conformidade com o nível intermediário do SQL-92.  
  
 SQL_STATIC_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 Um bitmask SQLUINTEGER que descreve os atributos de um cursor estático que são suportados pelo driver. Esse bitmask contém o subconjunto de segundo de atributos; para o subconjunto primeiro, consulte SQL_STATIC_CURSOR_ATTRIBUTES1.  
  
 Bitmasks a seguir são usados para determinar quais atributos têm suporte:  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_ CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_ SIMULATE_UNIQUE  
  
 Para obter descrições desses bitmasks, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES2 (e substitua "cursor estático" para "cursor dinâmico" nas descrições de).  
  
 SQL_STRING_FUNCTIONS ODBC (1.0)  
 Observação: O tipo de informações foi introduzido no ODBC 1.0; cada máscara de bits é rotulada com a versão na qual ele foi introduzido.  
  
 Um bitmask SQLUINTEGER enumerando as funções escalares de cadeia de caracteres com suporte de driver e a fonte de dados associada.  
  
 Bitmasks a seguir são usados para determinar quais funções de cadeia de caracteres têm suporte:  
  
 SQL_FN_STR_ASCII (ODBC 1.0) SQL_FN_STR_BIT_LENGTH (ODBC 3.0) SQL_FN_STR_CHAR (ODBC 1.0) SQL_FN_STR_CHAR_LENGTH (ODBC 3.0) SQL_FN_STR_CHARACTER_LENGTH (ODBC 3.0) SQL_FN_STR_CONCAT (ODBC 1.0) SQL_FN_STR_DIFFERENCE (ODBC 2.0) SQL_FN_STR_INSERT (ODBC 1.0) SQL_FN_STR_LCASE (ODBC 1.0) SQL_FN_STR_LEFT (ODBC 1.0) SQL_FN_STR_LENGTH (ODBC 1.0) SQL_FN_STR_LOCATE (ODBC 1.0) SQL_FN_STR_LTRIM (ODBC 1.0) SQL_FN_STR_OCTET_LENGTH (ODBC 3.0) SQL_FN_STR_POSITION (ODBC 3.0) SQL_FN_ SQL_FN_STR_REPEAT (ODBC 1.0) STR_REPLACE (ODBC 1.0) SQL_FN_STR_RIGHT (ODBC 1.0) SQL_FN_STR_RTRIM (ODBC 1.0) SQL_FN_STR_SOUNDEX (ODBC 2.0) SQL_FN_STR_SPACE (ODBC 2.0) SQL_FN_STR_SUBSTRING (ODBC 1.0) SQL_FN_STR_UCASE (ODBC 1.0)  
  
 Se um aplicativo pode chamar o **localizar** função escalar com o *string_exp1*, *string_exp2*, e *iniciar* argumentos, o driver Retorna a máscara de bits SQL_FN_STR_LOCATE. Se um aplicativo pode chamar a função escalar localizar somente com o *string_exp1* e *string_exp2* argumentos, o driver retorna a máscara de bits de SQL_FN_STR_LOCATE_2. Drivers que dão suporte total a **localizar** ambos bitmasks de retorno da função escalar.  
  
 (Para obter mais informações, consulte [funções de cadeia de caracteres](../../../odbc/reference/appendixes/string-functions.md) no Apêndice E, "funções escalares.")  
  
 SQL_SUBQUERIES (ODBC 2.0)  
 Um bitmask SQLUINTEGER ao enumerar os predicados que dão suporte a subconsultas:  
  
 SQL_SQ_CORRELATED_SUBQUERIESSQL_SQ_COMPARISONSQL_SQ_EXISTSSQL_SQ_INSQL_SQ_QUANTIFIED  
  
 A máscara de bits SQL_SQ_CORRELATED_SUBQUERIES indica que todos os predicados que dão suporte a subconsultas dá suporte a subconsultas correlacionadas.  
  
 Um driver em conformidade com o nível de entrada do SQL-92 sempre retornará uma máscara de bits em que todos esses bits são definidos.  
  
 SQL_SYSTEM_FUNCTIONS ODBC (1.0)  
 Um bitmask SQLUINTEGER enumerando as funções de sistema escalar com suporte de driver e a fonte de dados associada.  
  
 Bitmasks a seguir são usados para determinar quais funções do sistema têm suporte:  
  
 SQL_FN_SYS_DBNAMESQL_FN_SYS_IFNULLSQL_FN_SYS_USERNAME  
  
 SQL_TABLE_TERM ODBC (1.0)  
 Uma cadeia de caracteres com o nome do fornecedor de fonte de dados de uma tabela. Por exemplo, "table" ou "file".  
  
 Essa cadeia de caracteres pode ser em superior, inferior ou maiusculas e minúsculas.  
  
 Um driver em conformidade com o nível de entrada do SQL-92 sempre retorna "table".  
  
 SQL_TIMEDATE_ADD_INTERVALS (ODBC 2.0)  
 Um bitmask SQLUINTEGER ao enumerar os intervalos de carimbo de hora com suporte de driver e a fonte de dados associada para a função escalar TIMESTAMPADD.  
  
 Bitmasks a seguir são usados para determinar quais intervalos têm suporte:  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 Um driver de nível em conformidade com FIPS transição sempre retornará uma máscara de bits em que todos esses bits são definidos.  
  
 SQL_TIMEDATE_DIFF_INTERVALS (ODBC 2.0)  
 Um bitmask SQLUINTEGER ao enumerar os intervalos de carimbo de hora com suporte de driver e a fonte de dados associada para a função escalar TIMESTAMPDIFF.  
  
 Bitmasks a seguir são usados para determinar quais intervalos têm suporte:  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 Um driver de nível em conformidade com FIPS transição sempre retornará uma máscara de bits em que todos esses bits são definidos.  
  
 SQL_TIMEDATE_FUNCTIONS ODBC (1.0)  
 Observação: O tipo de informações foi introduzido no ODBC 1.0; cada máscara de bits é rotulada com a versão na qual ele foi introduzido.  
  
 Um bitmask SQLUINTEGER ao enumerar o escalar funções de data e hora com suporte de driver e a fonte de dados associada.  
  
 Bitmasks a seguir são usados para determinar quais funções de data e hora são suportadas:  
  
 SQL_FN_TD_CURRENT_DATE ODBC 3.0) SQL_FN_TD_CURRENT_TIME (ODBC 3.0) SQL_FN_TD_CURRENT_TIMESTAMP (ODBC 3.0) SQL_FN_TD_CURDATE (ODBC 1.0) SQL_FN_TD_CURTIME (ODBC 1.0) SQL_FN_TD_DAYNAME (ODBC 2.0) SQL_FN_TD_DAYOFMONTH (ODBC 1.0) (SQL_FN_TD_DAYOFWEEK ODBC 1.0) SQL_FN_TD_DAYOFYEAR (ODBC 1.0) SQL_FN_TD_EXTRACT (ODBC 3.0) SQL_FN_TD_HOUR (ODBC 1.0) SQL_FN_TD_MINUTE (ODBC 1.0) SQL_FN_TD_MONTH (ODBC 1.0) SQL_FN_TD_MONTHNAME (ODBC 2.0) SQL_FN_TD_NOW (ODBC 1.0) SQL_FN_TD_QUARTER (ODBC 1.0) SQL_FN_TD_ SEGUNDO (ODBC 1.0) SQL_FN_TD_TIMESTAMPADD (ODBC 2.0) SQL_FN_TD_TIMESTAMPDIFF (ODBC 2.0) SQL_FN_TD_WEEK (ODBC 1.0) SQL_FN_TD_YEAR (ODBC 1.0)  
  
 SQL_TXN_CAPABLE ODBC (1.0)  
 Observação: O tipo de informações foi introduzido no ODBC 1.0; cada valor de retorno é rotulado com a versão na qual ele foi introduzido.  
  
 Um valor SQLUSMALLINT que descreve o suporte a transações na fonte de dados ou driver:  
  
 SQL_TC_NONE = transações não tem suportadas. ODBC (1.0)  
  
 SQL_TC_DML = transações podem conter apenas as instruções de linguagem de manipulação de dados (DML) (**selecione**, **inserir**, **atualização**, **excluir** ). Instruções de Definition Language (DDL) de dados em uma causa de transação um erro. ODBC (1.0)  
  
 SQL_TC_DDL_COMMIT = transações podem conter apenas as instruções DML. Instruções DDL (**CREATE TABLE**, **DROP INDEX**, e assim por diante) encontrado em uma causa de transação da transação a ser confirmado. (ODBC 2.0)  
  
 SQL_TC_DDL_IGNORE = transações podem conter apenas as instruções DML. Instruções de DDL encontradas em uma transação são ignoradas. (ODBC 2.0)  
  
 SQL_TC_ALL = transações podem conter instruções DDL e as instruções DML em qualquer ordem. ODBC (1.0)  
  
 (Como suporte de transações é obrigatório em SQL-92, um driver compatível do SQL-92 [qualquer nível] nunca retornará SQL_TC_NONE.)  
  
 SQL_TXN_ISOLATION_OPTION ODBC (1.0)  
 Um bitmask SQLUINTEGER ao enumerar os níveis de isolamento de transação disponíveis da fonte de dados ou driver.  
  
 Bitmasks a seguir são usados junto com o sinalizador para determinar quais opções são suportadas:  
  
 SQL_TXN_READ_UNCOMMITTEDSQL_TXN_READ_COMMITTEDSQL_TXN_REPEATABLE_READSQL_TXN_SERIALIZABLE  
  
 Para obter descrições desses níveis de isolamento, consulte a descrição do SQL_DEFAULT_TXN_ISOLATION.  
  
 Para definir o nível de isolamento da transação, um aplicativo chama **SQLSetConnectAttr** para definir o atributo SQL_ATTR_TXN_ISOLATION. Para obter mais informações, consulte [função SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 Um driver em conformidade com o nível de entrada do SQL-92 sempre retornará SQL_TXN_SERIALIZABLE com suporte. Um driver de nível em conformidade com FIPS transição sempre retornará todas essas opções com suporte.  
  
 SQL_UNION (ODBC 2.0)  
 Um bitmask SQLUINTEGER ao enumerar o suporte para o **união** cláusula:  
  
 SQL_U_UNION = o fonte de dados oferece suporte a **união** cláusula.  
  
 SQL_U_UNION_ALL = o fonte de dados oferece suporte a **todos os** palavra-chave no **união** cláusula. (**SQLGetInfo** retorna SQL_U_UNION e SQL_U_UNION_ALL nesse caso.)  
  
 Um driver em conformidade com o nível de entrada do SQL-92 sempre retornará essas duas opções com suporte.  
  
 SQL_USER_NAME ODBC (1.0)  
 Uma cadeia de caracteres com o nome usado em um determinado banco de dados, que pode ser diferente do nome de logon.  
  
 SQL_XOPEN_CLI_YEAR (ODBC 3.0)  
 Uma cadeia de caracteres que indica o ano de publicação da especificação Open Group com a qual a versão do Gerenciador de Driver ODBC é totalmente compatível.  
  
 SQL_ACCESSIBLE_PROCEDURES ODBC (1.0)  
 Uma cadeia de caracteres: "Y" se o usuário pode executar todos os procedimentos retornados pelo **SQLProcedures**; "N" caso haja procedimentos retornado se o usuário não pode executar.  
  
 SQL_ACCESSIBLE_TABLES ODBC (1.0)  
 Uma cadeia de caracteres: "Y" se o usuário tem a garantia **selecione** privilégios para todas as tabelas retornadas por **SQLTables**; "N" caso haja tabelas retornadas que o usuário não pode acessar.  
  
 SQL_ACTIVE_ENVIRONMENTS (ODBC 3.0)  
 Um valor SQLUSMALLINT que especifica o número máximo de ambientes ativos que o driver pode suportar. Se não há nenhum limite especificado ou o limite é desconhecido, esse valor é definido como zero.  
  
 SQL_AGGREGATE_FUNCTIONS (ODBC 3.0)  
 Um bitmask SQLUINTEGER enumerando suporte para funções de agregação:  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 Um driver em conformidade com o nível de entrada do SQL-92 sempre retornará todas essas opções com suporte.  
  
 SQL_ALTER_DOMAIN (ODBC 3.0)  
 Um bitmask SQLUINTEGER enumerando as cláusulas no **alterar domínio** instrução, conforme definido em SQL-92, suportado pela fonte de dados. Um driver compatível com nível completo do SQL-92 sempre retornará todas as máscaras de bits. Um valor de retorno "0" significa que o **alterar domínio** instrução não é suportada.  
  
 O nível de conformidade FIPS ou de SQL-92 em que esse recurso deve ser suportado é mostrado entre parênteses ao lado de cada máscara de bits.  
  
 Bitmasks a seguir são usados para determinar quais cláusulas são suportadas:  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT = adicionando uma restrição de domínio tem suporte (nível total)  
  
 SQL_AD_ADD_DOMAIN_DEFAULT = \<alterar domínio > \<cláusula de padrão do conjunto de domínio > é suportado (nível total)  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION = \<cláusula de definição de nome de restrição > há suporte para nomes de restrição de domínio (nível intermediário)  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT = \<cláusula de restrição drop domínio > é suportado (nível total)  
  
 SQL_AD_DROP_DOMAIN_DEFAULT = \<alterar domínio > \<cláusula de padrão de domínio drop > há suporte para (nível total)  
  
 Os bits a seguir especificam com suporte \<atributos de restrição > Se \<adicionar restrição de domínio > é suportado (o bit SQL_AD_ADD_DOMAIN_CONSTRAINT é definido):  
  
 SQL_AD_ADD_CONSTRAINT_DEFERRABLE (nível completo) SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE (nível completo) SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED (nível completo) SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE (nível completo)  
  
 SQL_ALTER_TABLE (ODBC 2.0)  
 Um bitmask SQLUINTEGER enumerando as cláusulas no **ALTER TABLE** suporte pela fonte de dados.  
  
 O nível de conformidade FIPS ou de SQL-92 em que esse recurso deve ser suportado é mostrado entre parênteses ao lado de cada máscara de bits.  
  
 Bitmasks a seguir são usados para determinar quais cláusulas são suportadas:  
  
 SQL_AT_ADD_COLUMN_COLLATION = \<adicionar coluna > cláusula é suportada com o recurso para especificar o agrupamento de coluna (nível completo) (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_DEFAULT = \<adicionar coluna > cláusula é suportada com o recurso para especificar os padrões de coluna (nível FIPS transição) (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_SINGLE = \<adicionar coluna > é (nível de FIPS transição) com suporte (ODBC 3.0)  
  
 SQL_AT_ADD_CONSTRAINT = \<adicionar coluna > cláusula é suportada com o recurso para especificar restrições de coluna (nível FIPS transição) (ODBC 3.0)  
  
 SQL_AT_ADD_TABLE_CONSTRAINT = \<adicionar restrição de tabela > há suporte para a cláusula (nível FIPS transição) (ODBC 3.0)  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION = \<definição de nome de restrição > há suporte para restrições de tabela e coluna (nível intermediário) de nomenclatura (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_CASCADE = \<descartar a coluna > é suportada em cascata (nível FIPS transição) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_DEFAULT = \<alterar a coluna > \<cláusula de padrão de coluna drop > é (nível intermediário) com suporte (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_RESTRICT = \<descartar a coluna > RESTRINGIR tem suporte (nível FIPS transição) (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT = \<descartar a coluna > RESTRINGIR tem suporte (nível FIPS transição) (ODBC 3.0)  
  
 SQL_AT_SET_COLUMN_DEFAULT = \<alterar a coluna > \<cláusula de padrão de coluna do conjunto > é (nível intermediário) com suporte (ODBC 3.0)  
  
 Os bits seguir especificam o suporte \<atributos de restrição > se há suporte para especificar restrições de coluna ou tabela (o bit SQL_AT_ADD_CONSTRAINT é definido):  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED (nível completo) (ODBC 3.0) SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE (nível completo) (ODBC 3.0) SQL_AT_CONSTRAINT_DEFERRABLE (nível completo) (ODBC 3.0) SQL_AT_CONSTRAINT_NON_DEFERRABLE (nível completo) (ODBC 3.0)  
  
 SQL_ASYNC_MODE (ODBC 3.0)  
 Um valor SQLUINTEGER que indica o nível de suporte assíncrono no driver:  
  
 SQL_AM_CONNECTION = há suporte para execução assíncrona de nível de Conexão. Todos os identificadores de instrução associados com um identificador de conexão fornecido estão no modo assíncrono ou todos estão no modo síncrono. Um identificador de instrução em uma conexão não pode estar em modo assíncrono, enquanto outro identificador de instrução sobre a mesma conexão estiver no modo síncrono e vice-versa.  
  
 SQL_AM_STATEMENT = há suporte para execução assíncrona de nível de instrução. Alguns identificadores de instrução associados com um identificador de conexão podem estar em modo assíncrono, enquanto outros identificadores de instrução sobre a mesma conexão estiver no modo síncrono.  
  
 SQL_AM_NONE = assíncrona modo não é suportado.  
  
 SQL_BATCH_ROW_COUNT (ODBC 3.0)  
 Um bitmask SQLUINTEGER ao enumerar o comportamento do driver em relação à disponibilidade de linha de conta. As seguir bitmasks são usados junto com o tipo de informações:  
  
 SQL_BRC_ROLLED_UP = contagens de linhas para instruções INSERT, DELETE ou UPDATE consecutivas são acumuladas em uma. Se este bit não for definido, as contagens de linha estão disponíveis para cada instrução.  
  
 SQL_BRC_PROCEDURES = contagens de linhas, se houver, estão disponíveis quando um lote é executado em um procedimento armazenado. Se houver contagens de linhas, eles podem ser rolados para cima ou individualmente disponíveis, dependendo do bit SQL_BRC_ROLLED_UP.  
  
 SQL_BRC_EXPLICIT = contagens de linhas, se houver, estão disponíveis quando um lote é executado diretamente chamando **SQLExecute** ou **SQLExecDirect**. Se houver contagens de linhas, eles podem ser rolados para cima ou individualmente disponíveis, dependendo do bit SQL_BRC_ROLLED_UP.  
  
## <a name="example"></a>Exemplo  
 **SQLGetInfo** retorna a lista de opções com suporte como um bitmask SQLUINTEGER em **InfoValuePtr*. A máscara de bits para cada opção é usada junto com o sinalizador para determinar se a opção tem suporte.  
  
 Por exemplo, um aplicativo pode usar o código a seguir para determinar se a função escalar de subcadeia de caracteres é suportada pelo driver associado com a conexão.  
  
 Outro exemplo de uso **SQLGetInfo**, consulte [função SQLTables](../../../odbc/reference/syntax/sqltables-function.md).  
  
```  
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
  
 Determinando se um driver oferece suporte a uma função  
 [Função SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
 Retornando a configuração de um atributo de instrução  
 [Função SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)  
  
 Retornando informações sobre tipos de dados de uma fonte de dados  
 [Função SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)

