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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 514922fd085cfd2ba19eb5c07dd844db82d55202
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303338"
---
# <a name="sqlgetinfo-function"></a>Função SQLGetInfo
**Conformidade**  
 Versão introduzida: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **O SQLGetInfo** retorna informações gerais sobre o driver e a fonte de dados associadas a uma conexão.  
  
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
 *ConexãoHandle*  
 [Entrada] Identificador de conexão.  
  
 *Infotipo*  
 [Entrada] Tipo de informação.  
  
 *InfoValuePtr*  
 [Saída] Ponteiro para um buffer no qual para retornar as informações. Dependendo do *InfoType* solicitado, as informações retornadas serão uma das seguintes: uma seqüência de caracteres com término nulo, um valor SQLUSMALLINT, uma máscara de bit SQLUINTEGER, um sinalizador SQLUINTEGER, um valor binário SQLUINTEGER ou um valor SQLULEN.  
  
 Se o argumento *InfoType* for SQL_DRIVER_HDESC ou SQL_DRIVER_HSTMT, o argumento *InfoValuePtr* será de entrada e saída. (Consulte os descritores SQL_DRIVER_HDESC ou SQL_DRIVER_HSTMT posteriormente nesta descrição da função para obter mais informações.)  
  
 Se *o InfoValuePtr* for NULL, *stringLengthLengthTr* ainda retornará o número total de bytes (excluindo o caractere de rescisão nula para dados de caracteres) disponível para retornar no buffer apontado pelo *InfoValuePtr*.  
  
 *BufferLength*  
 [Entrada] Comprimento do \*buffer *InfoValuePtr.* Se o valor no * \*InfoValuePtr* não for uma seqüência de caracteres ou se *o InfoValuePtr* for um ponteiro nulo, o argumento *BufferLength* será ignorado. O driver assume que o tamanho do * \*InfoValuePtr* é SQLUSMALLINT ou SQLUINTEGER, com base no *InfoType*. Se * \*o InfoValuePtr* for uma seqüência unicode (ao chamar **SQLGetInfoW),** o argumento *BufferLength* deve ser um número uniforme; se não, SQLSTATE HY090 (comprimento inválido da seqüência ou buffer) é devolvido.  
  
 *StringLengthPtr*  
 [Saída] Ponteiro para um buffer no qual retornar o número total de bytes (excluindo o caractere de rescisão nula para dados de caracteres) disponível para retornar em **InfoValuePtr*.  
  
 Para dados de caracteres, se o número de bytes disponíveis para \*retornar for maior ou igual a *BufferLength,* as informações no *InfoValuePtr* são truncadas em *bytes BufferLength* menos o comprimento de um caractere de rescisão nula e é anulada nula pelo driver.  
  
 Para todos os outros tipos de dados, o valor do *BufferLength* é ignorado e o driver assume que o tamanho do \* *InfoValuePtr* é SQLUSMALLINT ou SQLUINTEGER, dependendo do *InfoType*.  
  
## <a name="return-value"></a>Valor retornado  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLGetInfo** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_DBC e uma *alça* de *ConnectionHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados pelo **SQLGetInfo** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cordas, truncados direito|O \*buffer *InfoValuePtr* não era grande o suficiente para retornar todas as informações solicitadas. Portanto, a informação foi truncada. O comprimento das informações solicitadas em sua forma não truncada é devolvido em **StringLengthLengthPtr*. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|08003|Conexão não aberta|(DM) O tipo de informação solicitada no *InfoType* requer uma conexão aberta. Dos tipos de informações reservados pela ODBC, apenas SQL_ODBC_VER podem ser devolvidos sem conexão aberta.|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados à qual o driver estava conectado falhou antes da função ser concluída.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar memória necessária para suportar a execução ou a conclusão da função.|  
|HY010|Erro de seqüência de função|(DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foram chamados para o *StatementHandle* e retornaram SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY024|Valor do atributo inválido|(DM) O argumento *infotype* foi SQL_DRIVER_HSTMT, e o valor apontado pelo *InfoValuePtr* não era uma alça de declaração válida.<br /><br /> (DM) O argumento *InfoType* foi SQL_DRIVER_HDESC, e o valor apontado pelo *InfoValuePtr* não era uma alça de descritor válida.|  
|HY090|Comprimento de seqüência ou buffer inválido|(DM) O valor especificado para *o argumento BufferLength* foi inferior a 0.<br /><br /> (DM) O valor especificado para *BufferLength* era um número ímpar, e * \*o InfoValuePtr* era de um tipo de dados Unicode.|  
|HY096|Tipo de informação fora do alcance|O valor especificado para o argumento *InfoType* não era válido para a versão do ODBC suportada pelo driver.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Campo opcional não implementado|O valor especificado para o argumento *InfoType* foi um valor específico do driver que não é suportado pelo driver.|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver que corresponde ao *ConnectionHandle* não suporta a função.|  
  
## <a name="comments"></a>Comentários  
 Os tipos de informações atualmente definidos são mostrados em "Tipos de informações", posteriormente nesta seção; espera-se que mais sejam definidos para aproveitar diferentes fontes de dados. Uma série de tipos de informações é reservada pela ODBC; os desenvolvedores de driver devem reservar valores para seu próprio uso específico do driver do Open Group. **O SQLGetInfo** não realiza conversão ou *thunking* unicode (consulte [Apêndice A: Códigos de erro ODBC](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md) da *referência do programador ODBC)* para *infotypes definidos*pelo driver . Para obter mais informações, consulte [tipos de dados específicos do driver, tipos de descritores, tipos de informações, tipos de diagnóstico e atributos](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md). O formato das informações \*retornadas no *InfoValuePtr* depende do *InfoType* solicitado. **O SQLGetInfo** retornará as informações em um dos cinco formatos diferentes:  
  
-   Uma seqüência de caracteres com término nulo  
  
-   Um valor SQLUSMALLINT  
  
-   Uma máscara de bit SQLUINTEGER  
  
-   Um valor SQLUINTEGER  
  
-   Um valor binário SQLUINTEGER  
  
 O formato de cada um dos seguintes tipos de informações é observado na descrição do tipo. O aplicativo deve lançar o valor devolvido em **InfoValuePtr* de acordo. Para um exemplo de como um aplicativo pode recuperar dados de uma máscara de bits SQLUINTEGER, consulte "Exemplo de código".  
  
 Um driver deve devolver um valor para cada tipo de informação definido nas tabelas a seguir. Se um tipo de informação não se aplicar ao driver ou à fonte de dados, o driver retorna um dos valores listados na tabela a seguir.  
  
 String de caractere ("Y" ou "N")  
 "N"  
  
 Cadeia de caracteres (não "Y" ou "N")  
 cadeia de caracteres vazia  
  
 SQLUSMALLINT  
 0  
  
 Máscara de bit SQLUINTEGER ou valor binário SQLUINTEGER  
 0L  
  
 Por exemplo, se uma fonte de dados não suportar procedimentos, o **SQLGetInfo** retorna os valores listados na tabela a seguir para os valores do *InfoType* relacionados aos procedimentos.  
  
 SQL_PROCEDURES  
 "N"  
  
 SQL_ACCESSIBLE_PROCEDURES  
 "N"  
  
 SQL_MAX_PROCEDURE_NAME_LEN  
 0  
  
 SQL_PROCEDURE_TERM  
 cadeia de caracteres vazia  
  
 **O SQLGetInfo** retorna o SQLSTATE HY096 (valor de argumento inválido) para valores do *InfoType* que estão na gama de tipos de informações reservados para uso pelo ODBC, mas não são definidos pela versão do ODBC suportada pelo driver. Para determinar qual versão do ODBC um driver cumpre, um aplicativo chama **SQLGetInfo** com o SQL_DRIVER_ODBC_VER tipo de informação. **O SQLGetInfo** retorna o SQLSTATE HYC00 (recurso opcional não implementado) para valores do *InfoType* que estão na gama de tipos de informações reservadas para uso específico do driver, mas não são suportados pelo driver.  
  
 Todas as chamadas para **sqlGetInfo** requerem uma conexão aberta, exceto quando o *InfoType* é SQL_ODBC_VER, o que retorna a versão do Gerenciador de driver.  
  
## <a name="information-types"></a>Tipos de informações  
 Esta seção lista os tipos de informações suportados pelo **SQLGetInfo**. Os tipos de informação são agrupados categoricamente e listados alfabeticamente. Os tipos de informações que foram adicionados ou renomeados para ODBC 3 *.x* também estão listados.  
  
## <a name="driver-information"></a>Informações do motorista  
 Os seguintes valores do *argumento InfoType* retornam informações sobre o driver ODBC, como o número de declarações ativas, o nome de origem dos dados e o nível de conformidade dos padrões de interface:  
  
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
>  Ao implementar **o SQLGetInfo,** um driver pode melhorar o desempenho minimizando o número de vezes que as informações são enviadas ou solicitadas do servidor.  
  
## <a name="dbms-product-information"></a>Informações sobre produtos DBMS  
 Os seguintes valores do *argumento InfoType* retornam informações sobre o produto DBMS, como o nome e a versão do DBMS:  
  
 SQL_DATABASE_NAMESQL_DBMS_NAMESQL_DBMS_VER  
  
## <a name="data-source-information"></a>Informações sobre a fonte de dados  
 Os seguintes valores do *argumento InfoType* retornam informações sobre a fonte de dados, como características do cursor e recursos de transação:  
  
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
  
## <a name="supported-sql"></a>SQL suportado  
 Os seguintes valores do *argumento InfoType* retornam informações sobre as instruções SQL suportadas pela fonte de dados. A sintaxe SQL de cada recurso descrito por esses tipos de informações é a sintaxe SQL-92. Esses tipos de informações não descrevem exaustivamente toda a gramática SQL-92. Em vez disso, eles descrevem as partes da gramática para as quais as fontes de dados normalmente oferecem diferentes níveis de suporte. Especificamente, a maioria das instruções DDL no SQL-92 estão cobertas.  
  
 Os aplicativos devem determinar o nível geral de gramática suportada a partir do SQL_SQL_CONFORMANCE tipo de informação e usar os outros tipos de informações para determinar variações do nível de conformidade das normas indicadas.  
  
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
  
## <a name="sql-limits"></a>Limites sql  
 Os seguintes valores do *argumento InfoType* retornam informações sobre os limites aplicados a identificadores e cláusulas em instruções SQL, como os comprimentos máximos de identificadores e o número máximo de colunas em uma lista selecionada. As limitações podem ser impostas pelo driver ou pela fonte de dados.  
  
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
  
## <a name="scalar-function-information"></a>Informações da função escalar  
 Os seguintes valores do *argumento InfoType* retornam informações sobre as funções escalares suportadas pela fonte de dados e pelo driver. Para obter mais informações sobre funções escalares, consulte [Apêndice E: Funções Escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).  
  
|||  
|-|-|  
|SQL_CONVERT_FUNCTIONS|SQL_TIMEDATE_ADD_INTERVALS|  
|SQL_NUMERIC_FUNCTIONS|SQL_TIMEDATE_DIFF_INTERVALS|  
|SQL_STRING_FUNCTIONS|SQL_TIMEDATE_FUNCTIONS|  
|SQL_SYSTEM_FUNCTIONS||  
  
## <a name="conversion-information"></a>Informações de conversão  
 Os seguintes valores do argumento *InfoType* retornam uma lista dos tipos de dados SQL para os quais a fonte de dados pode converter o tipo de dados SQL especificado com a função **ESCALAR CONVERTER:**  
  
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
  
## <a name="information-types-added-for-odbc-3x"></a>Tipos de informações adicionados para ODBC 3.x  
 Os seguintes valores do argumento *InfoType* foram adicionados para ODBC 3 *.x*:  
  
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
  
## <a name="information-types-renamed-for-odbc-3x"></a>Tipos de informações renomeados para ODBC 3.x  
 Os seguintes valores do argumento *InfoType* foram renomeados para ODBC 3 *.x*.  
  
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
  
## <a name="information-types-deprecated-in-odbc-3x"></a>Tipos de informações preteridos em ODBC 3.x  
 Os seguintes valores do argumento *InfoType* foram preteridos em ODBC 3 *.x*. Os drivers ODBC 3 *.x* devem continuar a suportar esses tipos de informações para compatibilidade retrógrada com aplicativos ODBC 2 *.x.* (Para obter mais informações sobre esses tipos, consulte [o suporte ao SQLGetInfo](../../../odbc/reference/appendixes/sqlgetinfo-support.md) no Apêndice G: Diretrizes do driver para compatibilidade retrógrada.)  
  
|||  
|-|-|  
|SQL_FETCH_DIRECTION|SQL_POS_OPERATIONS|  
|SQL_LOCK_TYPES|SQL_POSITIONED_STATEMENTS|  
|SQL_ODBC_API_CONFORMANCE|SQL_SCROLL_CONCURRENCY|  
|SQL_ODBC_SQL_CONFORMANCE|SQL_STATIC_SENSITIVITY|  
  
## <a name="information-type-descriptions"></a>Descrições do tipo de informação  
 A tabela a seguir lista alfabeticamente cada tipo de informação, a versão do ODBC em que foi introduzida e sua descrição.  
  
 SQL_ACCESSIBLE_PROCEDURES (ODBC 1.0)  
 Uma seqüência de caracteres: "Y" se o usuário puder executar todos os procedimentos retornados pelo **SQLProcedures;** "N" se houver procedimentos retornados que o usuário não pode executar.  
  
 SQL_ACCESSIBLE_TABLES (ODBC 1.0)  
 Uma seqüência de caracteres: "Y" se o usuário tiver privilégios **SELECT** garantidos para todas as tabelas retornadas por **SQLTables;** "N" se houver tabelas retornadas que o usuário não pode acessar.  
  
 SQL_ACTIVE_ENVIRONMENTS(ODBC 3.0)  
 Um valor SQLUSMALLINT que especifica o número máximo de ambientes ativos que o driver pode suportar. Se não houver um limite especificado ou o limite for desconhecido, este valor será definido como zero.  
  
 SQL_AGGREGATE_FUNCTIONS (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando o suporte para funções de agregação:  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 Um driver de conformidade de nível de entrada SQL-92 sempre retornará todas essas opções conforme suportado.  
  
 SQL_ALTER_DOMAIN (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando as cláusulas na declaração **ALTER DOMAIN,** conforme definido no SQL-92, suportado pela fonte de dados. Um driver sql-92 completo compatível com nível sempre retornará todas as máscaras de bit. Um valor de retorno de "0" significa que a declaração **ALTER DOMAIN** não é suportada.  
  
 O nível de conformidade SQL-92 ou FIPS no qual este recurso deve ser suportado é mostrado entre parênteses ao lado de cada máscara de bit.  
  
 As seguintes máscaras de bit são usadas para determinar quais cláusulas são suportadas:  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT = A adição de uma restrição de domínio é suportada (nível completo)  
  
 SQL_AD_ADD_DOMAIN_DEFAULT \<= alterar \<domínio>> de cláusula padrão de domínio definido é suportado (nível completo)  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION \<= cláusula de definição de nome de restrição> é suportado para nomear restrição de domínio (nível intermediário)  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT \<= cláusula de restrição de domínio de queda> é suportado (nível completo)  
  
 SQL_AD_DROP_DOMAIN_DEFAULT \<= alterar \<domínio> a cláusula padrão de domínio de queda> é suportado (nível completo)  
  
 Os bits a seguir \<especificam os \<atributos de restrição suportados> se adicionar> de restrição de domínio for suportado (o bit SQL_AD_ADD_DOMAIN_CONSTRAINT está definido):  
  
 SQL_AD_ADD_CONSTRAINT_DEFERRABLE (nível completo)SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE (nível completo)SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED (nível completo)SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE (Nível Completo)  
  
 SQL_ALTER_TABLE (ODBC 2.0)  
 Uma máscara de bit SQLUINTEGER enumerando as cláusulas na declaração **ALTER TABLE** suportada pela fonte de dados.  
  
 O nível de conformidade SQL-92 ou FIPS no qual este recurso deve ser suportado é mostrado entre parênteses ao lado de cada máscara de bit.  
  
 As seguintes máscaras de bit são usadas para determinar quais cláusulas são suportadas:  
  
 SQL_AT_ADD_COLUMN_COLLATION \<= adicionar coluna> cláusula é suportada, com facilidade para especificar colagem de coluna (nível completo) (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_DEFAULT \<= adicionar> a cláusula é suportada, com facilidade para especificar padrões de coluna (nível de transição FIPS) (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_SINGLE \<= adicionar> de coluna é suportado (nível de transição FIPS) (ODBC 3.0)  
  
 SQL_AT_ADD_CONSTRAINT \<= adicionar> a cláusula é suportada, com facilidade para especificar restrições de coluna (nível de transição FIPS) (ODBC 3.0)  
  
 SQL_AT_ADD_TABLE_CONSTRAINT \<= adicionar a cláusula de> de restrição de tabela (nível de transição FIPS) (ODBC 3.0)  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION \<= definição de nome de restrição> é suportado para nomear restrições de coluna e tabela (nível intermediário) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_CASCADE \<= coluna de queda> CASCADE é suportada (nível de transição FIPS) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_DEFAULT \<= alterar \<coluna> cláusula padrão da coluna de queda> é suportado (nível intermediário) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_RESTRICT \<= coluna de queda> RESTRICT é suportado (nível de transição FIPS) (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT \<= coluna de queda> RESTRICT é suportado (nível de transição FIPS) (ODBC 3.0)  
  
 SQL_AT_SET_COLUMN_DEFAULT \<= alterar \<coluna> definir cláusula padrão da coluna> é suportado (nível intermediário) (ODBC 3.0)  
  
 Os bits a \<seguir especificam os atributos de restrição de suporte> se for em vez de especificar as restrições de coluna ou tabela (o SQL_AT_ADD_CONSTRAINT bit está definido):  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED (nível completo) (ODBC 3.0)SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE (nível completo) (ODBC 3.0)SQL_AT_CONSTRAINT_DEFERRABLE (nível completo) (ODBC 3.0)SQL_AT_CONSTRAINT_NON_DEFERRABLE (nível completo) (ODBC 3.0)  
  
 SQL_ASYNC_DBC_FUNCTIONS (ODBC 3.8)  
 Um valor SQLUINTEGER que indica se o driver pode executar funções assíncronas na alça de conexão.  
  
 SQL_ASYNC_DBC_CAPABLE = O driver pode executar funções de conexão de forma assíncrona.  
  
 SQL_ASYNC_DBC_NOT_CAPABLE = O driver não pode executar funções de conexão de forma assíncrona.  
  
 SQL_ASYNC_MODE (ODBC 3.0)  
 Um valor SQLUINTEGER que indica o nível de suporte assíncrono no driver:  
  
 SQL_AM_CONNECTION = A execução assíncrona do nível de conexão é suportada. Todas as alças de declaração associadas a uma determinada alça de conexão estão no modo assíncrono ou todas estão no modo síncrono. Uma alça de declaração em uma conexão não pode estar no modo assíncrono, enquanto outra alça de declaração na mesma conexão está no modo síncrono, e vice-versa.  
  
 SQL_AM_STATEMENT = Execução assíncrona nível de declaração é suportada. Algumas alças de declaração associadas a uma alça de conexão podem estar no modo assíncrono, enquanto outras alças de declaração na mesma conexão estão no modo síncrono.  
  
 SQL_AM_NONE = O modo assíncrono não é suportado.  
  
 SQL_ASYNC_NOTIFICATION  
 Um valor SQLUINTEGER que indica se o driver suporta notificação assíncrona:  
  
-   **SQL_ASYNC_NOTIFICATION_CAPABLE SQL_ASYNC_NOTIFICATION_CAPABLE.** A notificação de execução assíncrona é suportada pelo motorista.  
  
-   **SQL_ASYNC_NOTIFICATION_NOT_CAPABLE SQL_ASYNC_NOTIFICATION_NOT_CAPABLE** A notificação de execução assíncrona não é suportada pelo motorista.  
  
 Existem duas categorias de operações assíncronas da ODBC: operações assíncronas de nível de conexão e operações assíncronas de nível de declaração.  Se um driver retornar SQL_ASYNC_NOTIFICATION_CAPABLE, ele deve suportar a notificação de todas as APIs que ele pode executar assíncronamente.  
  
 SQL_BATCH_ROW_COUNT (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER que enumera o comportamento do driver em relação à disponibilidade de contagem de linhas. As seguintes máscaras de bit são usadas juntamente com o tipo de informação:  
  
 SQL_BRC_ROLLED_UP = As contagens de linha para declarações de INSERT, DELETE ou UPDATE consecutivas são enroladas em uma. Se esta broca não estiver definida, as contagens de linha estarão disponíveis para cada declaração.  
  
 SQL_BRC_PROCEDURES = Contagem de linhas, se houver, estão disponíveis quando um lote é executado em um procedimento armazenado. Se as contagens de linha estiverem disponíveis, elas podem ser enroladas ou disponíveis individualmente, dependendo da SQL_BRC_ROLLED_UP bit.  
  
 SQL_BRC_EXPLICIT = Contagens de linha, se houver, estão disponíveis quando um lote é executado diretamente ligando para **SQLExecute** ou **SQLExecDirect**. Se as contagens de linha estiverem disponíveis, elas podem ser enroladas ou disponíveis individualmente, dependendo da SQL_BRC_ROLLED_UP bit.  
  
 SQL_BATCH_SUPPORT (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando o suporte do driver para lotes. As seguintes máscaras de bit são usadas para determinar qual nível é suportado:  
  
 SQL_BS_SELECT_EXPLICIT = O driver suporta lotes explícitos que podem ter demonstrações de geração definidas por resultados.  
  
 SQL_BS_ROW_COUNT_EXPLICIT = O driver suporta lotes explícitos que podem ter instruções geradoras de contagem de linhas.  
  
 SQL_BS_SELECT_PROC = O driver suporta procedimentos explícitos que podem ter demonstrações geradoras definidas por resultados.  
  
 SQL_BS_ROW_COUNT_PROC = O driver suporta procedimentos explícitos que podem ter declarações geradoras de contagem de linhas.  
  
 SQL_BOOKMARK_PERSISTENCE (ODBC 2.0)  
 Uma máscara de bit SQLUINTEGER enumerando as operações através das quais os marcadores persistem.  
  
 As seguintes máscaras de bit são usadas em conjunto com a bandeira para determinar por quais pontos de apostas persistem:  
  
 SQL_BP_CLOSE = Marcadores são válidos depois que um aplicativo chama **SQLFreeStmt** com a opção SQL_CLOSE ou **SQLCloseCursor** para fechar o cursor associado a uma declaração.  
  
 SQL_BP_DELETE = O marcador de uma linha é válido após a exclusão dessa linha.  
  
 SQL_BP_DROP = Marcadores são válidos depois que um aplicativo chama **SQLFreeHandle** com um *HandleType* de SQL_HANDLE_STMT para soltar uma declaração.  
  
 SQL_BP_TRANSACTION = Marcadores são válidos depois que um aplicativo comete ou reverte uma transação.  
  
 SQL_BP_UPDATE = O marcador de uma linha é válido após qualquer coluna nessa linha ter sido atualizada, incluindo as colunas-chave.  
  
 SQL_BP_OTHER_HSTMT = Um marcador associado a uma declaração pode ser usado com outra declaração. A menos que SQL_BP_CLOSE ou SQL_BP_DROP seja especificado, o cursor da primeira declaração deve estar aberto.  
  
 SQL_CATALOG_LOCATION (ODBC 2.0)  
 Um valor SQLUSMALLINT que indica a posição do catálogo em um nome de tabela qualificado:  
  
 SQL_CL_STARTSQL_CL_END  
  
 Por exemplo, um driver Xbase retorna SQL_CL_START porque o nome do diretório (catálogo) está no início do nome da tabela, como em \EMPDATA\EMP. Dbf. Um driver oracle server retorna SQL_CL_END porque o catálogo está ADMIN.EMP@EMPDATAno final do nome da tabela, como em .  
  
 Um driver sql-92 completo de conformidade de nível sempre retornará SQL_CL_START. Um valor de 0 é devolvido se os catálogos não forem suportados pela fonte de dados. Para determinar se os catálogos são suportados, um aplicativo chama **sqlGetInfo** com o SQL_CATALOG_NAME tipo de informação.  
  
 Este *InfoType* foi renomeado para ODBC 3.0 do ODBC 2.0 *InfoType* SQL_QUALIFIER_LOCATION.  
  
 SQL_CATALOG_NAME (ODBC 3.0)  
 Uma seqüência de caracteres: "Y" se o servidor suportar nomes de catálogo, ou "N" se não o fizer.  
  
 Um driver sql-92 completo de conformidade de nível sempre retornará "Y".  
  
 SQL_CATALOG_NAME_SEPARATOR(ODBC 1.0)  
 Uma seqüência de caracteres: o caractere ou caracteres que a fonte de dados define como o separador entre um nome de catálogo e o elemento de nome qualificado que o segue ou precede.  
  
 Uma seqüência de string vazia é devolvida se os catálogos não forem suportados pela fonte de dados. Para determinar se os catálogos são suportados, um aplicativo chama **sqlGetInfo** com o SQL_CATALOG_NAME tipo de informação. Um driver sql-92 completo de conformidade de nível sempre retornará ".".  
  
 Este *InfoType* foi renomeado para ODBC 3.0 do *InfoType* 2.0 da ODBC SQL_QUALIFIER_NAME_SEPARATOR.  
  
 SQL_CATALOG_TERM (ODBC 1.0)  
 Uma seqüência de caracteres com o nome do fornecedor de origem de dados para um catálogo; por exemplo, "banco de dados" ou "diretório". Esta seqüência pode estar em maiúsculas, minúsculas ou mistas.  
  
 Uma seqüência de string vazia é devolvida se os catálogos não forem suportados pela fonte de dados. Para determinar se os catálogos são suportados, um aplicativo chama **sqlGetInfo** com o SQL_CATALOG_NAME tipo de informação. Um driver sql-92 completo de conformidade de nível sempre retornará "catálogo".  
  
 Este *InfoType* foi renomeado para ODBC 3.0 do *InfoType* 2.0 da ODBC SQL_QUALIFIER_TERM.  
  
 SQL_CATALOG_USAGE (ODBC 2.0)  
 Uma máscara de bit SQLUINTEGER enumerando as instruções nas quais os catálogos podem ser usados.  
  
 As seguintes máscaras de bit são usadas para determinar onde os catálogos podem ser usados:  
  
 SQL_CU_DML_STATEMENTS = Os catálogos são suportados em todas as instruções de linguagem de manipulação de dados: **SELECT**, **INSERT**, **UPDATE**, **DELETE**, e se suportado, **SELECIONE PARA ATUALIZAR** e atualizar e excluir declarações.  
  
 SQL_CU_PROCEDURE_INVOCATION = Os catálogos são suportados na declaração de invocação do procedimento ODBC.  
  
 SQL_CU_TABLE_DEFINITION = Os catálogos são suportados em todas as instruções de definição de tabela: **CREATE TABLE**, **CREATE VIEW**, ALTER **TABLE**, **DROP TABLE**e DROP **VIEW**.  
  
 SQL_CU_INDEX_DEFINITION = Os catálogos são suportados em todas as demonstrações de definição de índice: **CREATE INDEX** e **DROP INDEX**.  
  
 SQL_CU_PRIVILEGE_DEFINITION = Os catálogos são suportados em todas as declarações de definição de privilégios: **GRANT** e **REVOKE**.  
  
 Um valor de 0 é devolvido se os catálogos não forem suportados pela fonte de dados. Para determinar se os catálogos são suportados, um aplicativo chama **sqlGetInfo** com o SQL_CATALOG_NAME tipo de informação. Um driver sql-92 completo de conformidade de nível sempre retornará uma máscara de bits com todos esses bits definidos.  
  
 Este *InfoType* foi renomeado para ODBC 3.0 do *InfoType* 2.0 da ODBC SQL_QUALIFIER_USAGE.  
  
 SQL_COLLATION_SEQ (ODBC 3.0)  
 O nome da seqüência de colagem. Esta é uma seqüência de caracteres que indica o nome da coletânea padrão para o conjunto de caracteres padrão para este servidor (por exemplo, 'ISO 8859-1' ou EBCDIC). Se isso não for desconhecido, uma corda vazia será devolvida. Um driver sql-92 completo de conformidade de nível sempre retornará uma seqüência não vazia.  
  
 SQL_COLUMN_ALIAS (ODBC 2.0)  
 Uma seqüência de caracteres: "Y" se a fonte de dados suportar alias de coluna; caso contrário, "N".  
  
 Um alias de coluna é um nome alternativo que pode ser especificado para uma coluna na lista de seleção usando uma cláusula AS. Um driver de conformidade de nível de entrada SQL-92 sempre retorna "Y".  
  
 SQL_CONCAT_NULL_BEHAVIOR (ODBC 1.0)  
 Um valor SQLUSMALLINT que indica como a fonte de dados lida com a concatenação de colunas de tipo de caracteres de valor NULA com colunas de tipo de caracteres não anuladas:  
  
 SQL_CB_NULL = Resultado é NULO valorizado.  
  
 SQL_CB_NON_NULL = Resultado é a concatenação de colunas ou colunas não-NULA.  
  
 Um driver de conformidade de nível de entrada SQL-92 sempre retornará SQL_CB_NULL.  
  
 SQL_CONVERT_BIGINTSQL_CONVERT_BINARYSQL_CONVERT_BIT SQL_CONVERT_GUIDSQL_CONVERT_DATESQL_CONVERT_DECIMALSQL_CONVERT_DOUBLESQL_CONVERT_FLOATSQL_CONVERT_INTEGERSQL_CONVERT_INTERVAL_YEAR_MONTHSQL_CONVERT_INTERVAL_DAY_TIMESQL_CONVERT_LONGVARBINARYSQL_CONVERT_LONGVARCHARSQL_CONVERT_NUMERICSQL_CONVERT_REALSQL_CONVERT_SMALLINTSQL_CONVERT_TIMESQL_CONVERT_TIMESTAMPSQL_CONVERT_TINYINTSQL_CONVERT_VARBINARYSQL_CONVERT_VARCHAR SQL_CONVERT_CHAR (ODBC 1.0)  
 Uma máscara de bit SQLUINTEGER. A máscara de bitindica as conversões suportadas pela fonte de dados com a função **ESCALAR CONVERT** para dados do tipo nomeado no *InfoType*. Se a máscara de bits for igual a zero, a fonte de dados não suportará nenhuma conversão de dados do tipo nomeado, incluindo conversão para o mesmo tipo de dados.  
  
 Por exemplo, para determinar se uma fonte de dados suporta a conversão de dados SQL_INTEGER para o SQL_BIGINT tipo de dados, um aplicativo chama **SQLGetInfo** com o *InfoType* de SQL_CONVERT_INTEGER. O aplicativo realiza uma **operação AND** com a máscara de bit retornada e SQL_CVT_BIGINT. Se o valor resultante não for zero, a conversão será suportada.  
  
 As seguintes máscaras de bit são usadas para determinar quais conversões são suportadas:  
  
 SQL_CVT_BIGINT (ODBC 1.0)SQL_CVT_BINARY (ODBC 1.0)SQL_CVT_BIT (ODBC 1.0) SQL_CVT_GUID (ODBC 3.5)SQL_CVT_CHAR (ODBC 1.0) SQL_CVT_DATE (ODBC 1.0)SQL_CVT_DECIMAL (ODBC 1.0)SQL_CVT_DOUBLE (ODBC 1). SQL_CVT_FLOAT SQL_ (ODBC 1.0)SQL_CVT_INTEGER (ODBC 1.0)SQL_CVT_INTERVAL_YEAR_MONTH (ODBC 3.0)SQL_CVT_INTERVAL_DAY_TIME (ODBC 3.0)SQL_CVT_LONGVARBINARY (ODBC 1.0)SQL_CVT_LONGVARCHAR (ODBC 1.0)SQL_CVT_NUMERIC (ODBC 1.0)SQL_ CVT_REAL ODBC 1.0)SQL_CVT_SMALLINT (ODBC 1.0)SQL_CVT_TIME (ODBC 1.0)SQL_CVT_TIMESTAMP (ODBC 1.0)SQL_CVT_TINYINT (ODBC 1.0)SQL_CVT_VARBINARY (ODBC 1.0)SQL_CVT_VARCHAR (ODBC 1.0)  
  
 SQL_CONVERT_FUNCTIONS (ODBC 1.0)  
 Uma máscara de bit SQLUINTEGER enumerando as funções de conversão escalar suportadas pelo driver e a fonte de dados associada.  
  
 A máscara de bit sadia é usada para determinar quais funções de conversão são suportadas:  
  
 SQL_FN_CVT_CASTSQL_FN_CVT_CONVERT  
  
 SQL_CORRELATION_NAME (ODBC 1.0)  
 Um valor SQLUSMALLINT que indica se os nomes de correlação de tabela são suportados:  
  
 SQL_CN_NONE = Nomes de correlação não são suportados.  
  
 SQL_CN_DIFFERENT = Nomes de correlação são suportados, mas devem diferir dos nomes das tabelas que representam.  
  
 SQL_CN_ANY = Nomes de correlação são suportados e podem ser qualquer nome definido pelo usuário válido.  
  
 Um driver de conformidade de nível de entrada SQL-92 sempre retornará SQL_CN_ANY.  
  
 SQL_CREATE_ASSERTION (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando as cláusulas na declaração **CREATE ASSERTION,** conforme definido no SQL-92, suportado pela fonte de dados.  
  
 As seguintes máscaras de bit são usadas para determinar quais cláusulas são suportadas:  
  
 SQL_CA_CREATE_ASSERTION  
  
 Os bits a seguir especificam o atributo de restrição suportado se a capacidade de especificar atributos de restrição for suportada explicitamente (consulte os SQL_ALTER_TABLE e SQL_CREATE_TABLE tipos de informações):  
  
 SQL_CA_CONSTRAINT_INITIALLY_DEFERREDSQL_CA_CONSTRAINT_INITIALLY_IMMEDIATESQL_CA_CONSTRAINT_DEFERRABLESQL_CA_CONSTRAINT_NON_DEFERRABLE  
  
 Um driver sql-92 completo de conformidade de nível sempre retornará todas essas opções conforme suportado. Um valor de retorno de "0" significa que a declaração **CREATE ASSERTION** não é suportada.  
  
 SQL_CREATE_CHARACTER_SET (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando as cláusulas na declaração **CREATE CHARACTER SET,** conforme definido no SQL-92, suportado pela fonte de dados.  
  
 As seguintes máscaras de bit são usadas para determinar quais cláusulas são suportadas:  
  
 SQL_CCS_CREATE_CHARACTER_SETSQL_CCS_COLLATE_CLAUSESQL_CCS_LIMITED_COLLATION  
  
 Um driver sql-92 completo de conformidade de nível sempre retornará todas essas opções conforme suportado. Um valor de retorno de "0" significa que a declaração **CREATE CHARACTER SET** não é suportada.  
  
 SQL_CREATE_COLLATION (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando as cláusulas na declaração **CREATE COLLATION,** conforme definido no SQL-92, suportado pela fonte de dados.  
  
 A máscara de bit sadia é usada para determinar quais cláusulas são suportadas:  
  
 SQL_CCOL_CREATE_COLLATION  
  
 Um driver sql-92 completo de conformidade de nível sempre retornará esta opção conforme suportado. Um valor de retorno de "0" significa que a declaração **CREATE COLLATION** não é suportada.  
  
 SQL_CREATE_DOMAIN (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando as cláusulas na declaração **CREATE DOMAIN,** conforme definido no SQL-92, suportado pela fonte de dados.  
  
 As seguintes máscaras de bit são usadas para determinar quais cláusulas são suportadas:  
  
 SQL_CDO_CREATE_DOMAIN = A declaração CREATE DOMAIN é suportada (nível intermediário).  
  
 SQL_CDO_CONSTRAINT_NAME_DEFINITION \<= definição de nome de restrição> é suportado para nomear restrições de domínio (nível intermediário).  
  
 Os bits a seguir especificam a capacidade de criar restrições de coluna:SQL_CDO_DEFAULT = A especificação das restrições de domínio é suportada (nível intermediário)SQL_CDO_CONSTRAINT = A especificação de padrões de domínio é suportada (nível intermediário)SQL_CDO_COLLATION = A colagem de domínio especificando é suportada (nível completo)  
  
 Os bits a seguir especificam os atributos de restrição suportados se a especificação das restrições de domínio for suportada (SQL_CDO_DEFAULT está definida):  
  
 SQL_CDO_CONSTRAINT_INITIALLY_DEFERRED (nível completo)SQL_CDO_CONSTRAINT_INITIALLY_IMMEDIATE (nível completo)SQL_CDO_CONSTRAINT_DEFERRABLE (nível completo)SQL_CDO_CONSTRAINT_NON_DEFERRABLE (nível completo)  
  
 Um valor de retorno de "0" significa que a declaração **CREATE DOMAIN** não é suportada.  
  
 SQL_CREATE_SCHEMA(ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando as cláusulas na declaração **CREATE SCHEMA,** conforme definido no SQL-92, suportado pela fonte de dados.  
  
 As seguintes máscaras de bit são usadas para determinar quais cláusulas são suportadas:  
  
 SQL_CS_CREATE_SCHEMASQL_CS_AUTHORIZATIONSQL_CS_DEFAULT_CHARACTER_SET  
  
 Um driver de conformidade de nível intermediário SQL-92 sempre devolverá as opções de SQL_CS_CREATE_SCHEMA e SQL_CS_AUTHORIZATION como suportadas. Estes também devem ser suportados no nível de entrada SQL-92, mas não necessariamente como instruções SQL. Um driver sql-92 completo de conformidade de nível sempre retornará todas essas opções conforme suportado.  
  
 SQL_CREATE_TABLE (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando as cláusulas na declaração **CREATE TABLE,** conforme definido no SQL-92, suportado pela fonte de dados.  
  
 O nível de conformidade SQL-92 ou FIPS no qual este recurso deve ser suportado é mostrado entre parênteses ao lado de cada máscara de bit.  
  
 As seguintes máscaras de bit são usadas para determinar quais cláusulas são suportadas:  
  
 SQL_CT_CREATE_TABLE = A declaração CREATE TABLE é suportada. (Nível de entrada)  
  
 SQL_CT_TABLE_CONSTRAINT = Suporte-se a restrições de tabela especificando (nível de transição FIPS)  
  
 SQL_CT_CONSTRAINT_NAME_DEFINITION = \<A cláusula de definição de nome de restrição> é suportada para nomear restrições de coluna e tabela (nível intermediário)  
  
 Os seguintes bits especificam a capacidade de criar tabelas temporárias:  
  
 SQL_CT_COMMIT_PRESERVE = As linhas excluídas são preservadas no commit. (Nível completo) SQL_CT_COMMIT_DELETE = Linhas excluídas são excluídas no commit. (Nível completo) SQL_CT_GLOBAL_TEMPORARY = Podem ser criadas tabelas temporárias globais. (Nível completo) SQL_CT_LOCAL_TEMPORARY = Podem ser criadas tabelas temporárias locais. (Nível completo)  
  
 Os seguintes bits especificam a capacidade de criar restrições de coluna:  
  
 SQL_CT_COLUMN_CONSTRAINT = A especificação das restrições da coluna é suportada (nível de transição FIPS)SQL_CT_COLUMN_DEFAULT = Especificar padrões de coluna é suportado (nível de transição FIPS)SQL_CT_COLUMN_COLLATION = Especificar a colagem de colunas é suportada (nível completo)  
  
 Os seguintes bits especificam os atributos de restrição suportados se a especificação das restrições de coluna ou tabela for suportada:  
  
 SQL_CT_CONSTRAINT_INITIALLY_DEFERRED (nível completo)SQL_CT_CONSTRAINT_INITIALLY_IMMEDIATE (nível completo)SQL_CT_CONSTRAINT_DEFERRABLE (nível completo)SQL_CT_CONSTRAINT_NON_DEFERRABLE (nível completo)  
  
 SQL_CREATE_TRANSLATION(ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando as cláusulas na declaração **CREATE TRANSLATION,** conforme definido no SQL-92, suportado pela fonte de dados.  
  
 A máscara de bit sadia é usada para determinar quais cláusulas são suportadas:  
  
 SQL_CTR_CREATE_TRANSLATION  
  
 Um driver sql-92 completo de conformidade de nível sempre retornará essas opções conforme suportado. Um valor de retorno de "0" significa que a declaração **CREATE TRANSLATION** não é suportada.  
  
 SQL_CREATE_VIEW (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando as cláusulas na declaração **CREATE VIEW,** conforme definido no SQL-92, suportado pela fonte de dados.  
  
 As seguintes máscaras de bit são usadas para determinar quais cláusulas são suportadas:  
  
 SQL_CV_CREATE_VIEWSQL_CV_CHECK_OPTIONSQL_CV_CASCADEDSQL_CV_LOCAL  
  
 Um valor de retorno de "0" significa que a declaração **CREATE VIEW** não é suportada.  
  
 Um driver de conformidade de nível de entrada SQL-92 sempre retornará as opções de SQL_CV_CREATE_VIEW e SQL_CV_CHECK_OPTION como suportado.  
  
 Um driver sql-92 completo de conformidade de nível sempre retornará todas essas opções conforme suportado.  
  
 SQL_CURSOR_COMMIT_BEHAVIOR (ODBC 1.0)  
 Um valor SQLUSMALLINT que indica como uma operação **COMMIT** afeta cursores e instruções preparadas na fonte de dados (o comportamento da fonte de dados quando você comete uma transação).  
  
 O valor deste atributo refletirá o estado atual da próxima configuração: SQL_COPT_SS_PRESERVE_CURSORS.  
  
 SQL_CB_DELETE = Feche os cursores e exclua as declarações preparadas. Para usar o cursor novamente, o aplicativo deve repreparar e reexecutar a declaração.  
  
 SQL_CB_CLOSE = Fechar cursores. Para declarações preparadas, o aplicativo pode chamar **SQLExecute** na instrução sem chamar **sqlprepare** novamente. O padrão para o driver SQL ODBC é SQL_CB_CLOSE. Isso significa que o driver SQL ODBC fechará seu cursor quando você cometer uma transação.  
  
 SQL_CB_PRESERVE = Preserve os cursores na mesma posição que antes da operação **COMMIT.** O aplicativo pode continuar a buscar dados, ou pode fechar o cursor e executar a declaração sem prepará-los.  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR (ODBC 1.0)  
 Um valor SQLUSMALLINT que indica como uma operação **ROLLBACK** afeta cursores e instruções preparadas na fonte de dados:  
  
 SQL_CB_DELETE = Feche os cursores e exclua as declarações preparadas. Para usar o cursor novamente, o aplicativo deve repreparar e reexecutar a declaração.  
  
 SQL_CB_CLOSE = Fechar cursores. Para declarações preparadas, o aplicativo pode chamar **SQLExecute** na instrução sem chamar **sqlprepare** novamente.  
  
 SQL_CB_PRESERVE = Preserve os cursores na mesma posição que antes da operação **ROLLBACK.** O aplicativo pode continuar a buscar dados, ou pode fechar o cursor e reexecutar a declaração sem reprepará-los.  
  
 SQL_CURSOR_SENSITIVITY (ODBC 3.0)  
 Um valor SQLUINTEGER que indica o suporte para sensibilidade do cursor:  
  
 SQL_INSENSITIVE = Todos os cursores da alça da declaração mostram o conjunto de resultados sem refletir quaisquer alterações que foram feitas a ele por qualquer outro cursor dentro da mesma transação.  
  
 SQL_UNSPECIFIED = Não é especificado se os cursores na alça da declaração tornam visíveis as alterações que foram feitas para um resultado definido por outro cursor dentro da mesma transação. Os cursors na alça da declaração podem tornar visíveis nenhuma, algumas ou todas essas alterações.  
  
 SQL_SENSITIVE = Os cursors são sensíveis às alterações que foram feitas por outros cursores dentro da mesma transação.  
  
 Um driver de conformidade de nível de entrada SQL-92 sempre retornará a opção SQL_UNSPECIFIED conforme suportado.  
  
 Um driver sql-92 completo de conformidade de nível sempre retornará a opção SQL_INSENSITIVE conforme suportado.  
  
 SQL_DATA_SOURCE_NAME (ODBC 1.0)  
 Uma seqüência de caracteres com o nome de origem de dados que foi usado durante a conexão. Se o aplicativo chamado **SQLConnect,** este é o valor do argumento *szDSN.* Se o aplicativo chamado **SQLDriverConnect** ou **SQLBrowseConnect,** este é o valor da palavra-chave DSN na seqüência de conexão passada para o driver. Se a seqüência de conexões não contiver a palavra-chave **DSN** (como quando contém a palavra-chave **DRIVER),** esta é uma seqüência vazia.  
  
 SQL_DATA_SOURCE_READ_ONLY(ODBC 1.0)  
 Uma cadeia de caracteres. "Y" se a fonte de dados estiver definida como SOMENTE LEITURA, "N" se for diferente.  
  
 Essa característica diz respeito apenas à própria fonte de dados; não é uma característica do driver que permite o acesso à fonte de dados. Um driver que é lido/gravar pode ser usado com uma fonte de dados que é somente leitura. Se um driver for somente leitura, todas as suas fontes de dados devem ser somente leitura e devem retornar SQL_DATA_SOURCE_READ_ONLY.  
  
 SQL_DATABASE_NAME (ODBC 1.0)  
 Uma seqüência de caracteres com o nome do banco de dados atual em uso, se a fonte de dados definir um objeto chamado "banco de dados".  
  
> [!NOTE]
>  No ODBC 3 *.x,* o valor retornado para este *InfoType* também pode ser devolvido ligando para **SQLGetConnectAttr** com um argumento *de atributo* de SQL_ATTR_CURRENT_CATALOG.  
  
 SQL_DATETIME_LITERALS (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando os literais de data-hora SQL-92 suportados pela fonte de dados. Observe que estes são os literais de data-hora listados na especificação SQL-92 e são separados das cláusulas de escape literal de data-hora definidas pela ODBC. Para obter mais informações sobre as cláusulas de fuga literal de data-hora da ODBC, consulte [Data, Hora e Carimbo de Hora Literal](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md).  
  
 Um driver de conformidade de nível FIPS Transitional sempre retornará o valor "1" na máscara de bits para os bits na lista a seguir. Um valor de "0" significa que os literais de datatime SQL-92 não são suportados.  
  
 As seguintes máscaras de bit são usadas para determinar quais literais são suportados:  
  
 SQL_DL_SQL92_DATESQL_DL_SQL92_TIMESQL_DL_SQL92_TIMESTAMPSQL_DL_SQL92_INTERVAL_YEARSQL_DL_SQL92_INTERVAL_MONTHSQL_DL_SQL92_INTERVAL_DAYSQL_DL_SQL92_INTERVAL_HOURSQL_DL_SQL92_INTERVAL_MINUTESQL_DL_SQL92_INTERVAL_SECONDSQL_DL_SQL92_INTERVAL_YEAR_TO_MONTHSQL_DL_SQL92_INTERVAL_DAY_TO_HOUR  
  
 SQL_DL_SQL92_INTERVAL_DAY_TO_MINUTESQL_DL_SQL92_INTERVAL_DAY_TO_SECONDSQL_DL_SQL92_INTERVAL_HOUR_TO_MINUTESQL_DL_SQL92_INTERVAL_HOUR_TO_SECONDSQL_DL_SQL92_INTERVAL_MINUTE_TO_SECOND  
  
 SQL_DBMS_NAME (ODBC 1.0)  
 Uma seqüência de caracteres com o nome do produto DBMS acessado pelo driver.  
  
 SQL_DBMS_VER (ODBC 1.0)  
 Uma seqüência de caracteres que indica a versão do produto DBMS acessada pelo driver. A versão é do formulário ##.############ onde os dois primeiros dígitos são a versão principal, os próximos dois dígitos são a versão menor, e os últimos quatro dígitos são a versão de lançamento. O driver deve renderizar a versão do produto DBMS neste formulário, mas também pode anexar a versão específica do produto DBMS. Por exemplo, "04.01.0000 Rdb 4.1".  
  
 SQL_DDL_INDEX (ODBC 3.0)  
 Um valor SQLUINTEGER que indica suporte à criação e queda de índices:  
  
 SQL_DI_CREATE_INDEXSQL_DI_DROP_INDEX  
  
 SQL_DEFAULT_TXN_ISOLATION (ODBC 1.0)  
 Um valor SQLUINTEGER que indica o nível de isolamento de transação padrão suportado pelo driver ou fonte de dados, ou zero se a fonte de dados não suportar transações. Os seguintes termos são usados para definir os níveis de isolamento da transação:  
  
 **Leitura Suja** A transação 1 muda de linha. A transação 2 lê a linha alterada antes que a transação 1 comprometa a alteração. Se a transação 1 reverter a alteração, a transação 2 terá lido uma linha que é considerada nunca existiu.  
  
 **Leitura não repetível** A transação 1 lê uma linha. A transação 2 atualiza ou exclui essa linha e compromete essa alteração. Se a transação 1 tentar reler a linha, ela receberá diferentes valores de linha ou descobrirá que a linha foi excluída.  
  
 **Fantasma** A transação 1 lê um conjunto de linhas que satisfazem alguns critérios de pesquisa. A transação 2 gera uma ou mais linhas (através de inserções ou atualizações) que correspondem aos critérios de pesquisa. Se a transação 1 reexecutar a declaração que lê as linhas, ela receberá um conjunto diferente de linhas.  
  
 Se a fonte de dados suportar transações, o driver retorna uma das seguintes máscaras de bits:  
  
 SQL_TXN_READ_UNCOMMITTED = Leituras sujas, leituras não repetíveis e fantasmas são possíveis.  
  
 SQL_TXN_READ_COMMITTED = Leituras sujas não são possíveis. Leituras não repetíveis e fantasmas são possíveis.  
  
 SQL_TXN_REPEATABLE_READ = Leituras sujas e leituras não repetíveis não são possíveis. Fantasmas são possíveis.  
  
 SQL_TXN_SERIALIZABLE = As transações são serializáveis. Transações serializáveis não permitem leituras sujas, leituras não repetíveis ou fantasmas.  
  
 SQL_DESCRIBE_PARAMETER (ODBC 3.0)  
 Uma seqüência de caracteres: "Y" se os parâmetros puderem ser descritos; "N", se não.  
  
 Um driver de conformidade completa do SQL-92 geralmente retornará "Y" porque suportará a declaração **DESCRIBE INPUT.** Como isso não especifica diretamente o suporte sql subjacente, no entanto, a descrição de parâmetros pode não ser suportada, mesmo em um driver sql-92 completo de conformidade de nível.  
  
 SQL_DM_VER (ODBC 3.0)  
 Uma seqüência de caracteres com a versão do Driver Manager. A versão é do formulário ##.##################################################################  
  
 O primeiro conjunto de dois dígitos é a versão principal do ODBC, dada pela constante SQL_SPEC_MAJOR.  
  
 O segundo conjunto de dois dígitos é a versão Menor ODBC, como dado pelo SQL_SPEC_MINOR constante.  
  
 O terceiro conjunto de quatro dígitos é o número de compilação principal do Driver Manager.  
  
 O último conjunto de quatro dígitos é o número de compilação menor do Driver Manager.  
  
 A versão do Windows 7 Driver Manager é 03.80. A versão do Windows 8 Driver Manager é 03.81.  
  
 SQL_DRIVER_AWARE_POOLING_SUPPORTED (ODBC 3.8)  
 Um valor SQLUINTEGER que indica se o driver suporta pooling consciente do driver. (Para obter mais informações, consulte [Pooling de conexão com reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md).  
  
 SQL_DRIVER_AWARE_POOLING_CAPABLE indica que o motorista pode suportar o mecanismo de pooling consciente do motorista.  
  
 SQL_DRIVER_AWARE_POOLING_NOT_CAPABLE indica que o motorista não pode suportar o mecanismo de pooling consciente do motorista.  
  
 Um motorista não precisa implementar SQL_DRIVER_AWARE_POOLING_SUPPORTED e o Driver Manager não honrará o valor de retorno do motorista.  
  
 SQL_DRIVER_HDBCSQL_DRIVER_HENV (ODBC 1.0)  
 Um valor SQLULEN, o cabo de ambiente do driver ou o cabo de conexão, determinado pelo *infoType*do argumento .  
  
 Esses tipos de informações são implementados apenas pelo Driver Manager.  
  
 SQL_DRIVER_HDESC (ODBC 3.0)  
 Um valor SQLULEN, a alça do descritor do driver determinada pela alça descritores do \*Driver Manager, que deve ser transmitida na entrada no *InfoValuePtr* a partir do aplicativo. Neste caso, *InfoValuePtr* é um argumento de entrada e saída. A alça do descritor \*de entrada passada no *InfoValuePtr* deve ter sido alocada explicitamente ou implicitamente no *ConnectionHandle*.  
  
 O aplicativo deve fazer uma cópia do punho do descritor do Driver Manager antes de chamar **o SQLGetInfo** com esse tipo de informação, para garantir que a alça não seja sobreescrita na saída.  
  
 Esse tipo de informação é implementado apenas pelo Driver Manager.  
  
 SQL_DRIVER_HLIB (ODBC 2.0)  
 Um valor SQLULEN, o *hinst* da biblioteca de carga retornou ao Driver Manager quando ele carregou o Driver DLL em um sistema operacional Microsoft Windows, ou seu equivalente em outro sistema operacional. A alça é válida apenas para o cabo de conexão especificado na chamada para **SQLGetInfo**.  
  
 Esse tipo de informação é implementado apenas pelo Driver Manager.  
  
 SQL_DRIVER_HSTMT (ODBC 1.0)  
 Um valor SQLULEN, a alça de demonstração do driver determinada pela alça \*de declaração do Driver Manager, que deve ser transmitida na entrada no *InfoValuePtr* a partir do aplicativo. Neste caso, *InfoValuePtr* é um argumento de entrada e saída. A alça de \*declaração de entrada passada no *InfoValuePtr* deve ter sido alocada no argumento *ConnectionHandle*.  
  
 O aplicativo deve fazer uma cópia do cabo de declaração do Driver Manager antes de chamar **o SQLGetInfo** com esse tipo de informação, para garantir que a alça não seja sobreescrita na saída.  
  
 Esse tipo de informação é implementado apenas pelo Driver Manager.  
  
 SQL_DRIVER_NAME (ODBC 1.0)  
 Uma seqüência de caracteres com o nome do arquivo do driver usado para acessar a fonte de dados.  
  
 SQL_DRIVER_ODBC_VER (ODBC 2.0)  
 Uma seqüência de caracteres com a versão de ODBC que o driver suporta. A versão é do formulário ##.##, onde os dois primeiros dígitos são a versão principal e os próximos dois dígitos são a versão menor. SQL_SPEC_MAJOR e SQL_SPEC_MINOR definem os números das versões principais e menores. Para a versão do ODBC descrita neste manual, estes são 3 e 0, e o motorista deve retornar "03.00".  
  
 O Gerenciador de Driver sdbc não modificará o valor de retorno do SQLGetInfo(SQL_DRIVER_ODBC_VER) para manter a compatibilidade retrógrada para aplicativos existentes. O driver especifica qual valor será devolvido. No entanto, um driver que suporta extensibilidade do tipo de dados C deve retornar 3.8 (ou mais) quando um aplicativo chamar **SQLSetEnvAttr** para definir SQL_ATTR_ODBC_VERSION para 3.8. Para obter mais informações, consulte [Tipos de dados C em ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 SQL_DRIVER_VER (ODBC 1.0)  
 Uma seqüência de caracteres com a versão do driver e, opcionalmente, uma descrição do motorista. No mínimo, a versão é do formulário ##.###############, onde os dois primeiros dígitos são a versão principal, os próximos dois dígitos são a versão menor, e os últimos quatro dígitos são a versão de lançamento.  
  
 SQL_DROP_ASSERTION (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando as cláusulas na declaração **DROP ASSERTION,** conforme definido no SQL-92, suportado pela fonte de dados.  
  
 A máscara de bit sadia é usada para determinar quais cláusulas são suportadas:  
  
 SQL_DA_DROP_ASSERTION  
  
 Um driver sql-92 completo de conformidade de nível sempre retornará esta opção conforme suportado.  
  
 SQL_DROP_CHARACTER_SET(ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando as cláusulas na declaração **DROP CHARACTER SET,** conforme definido no SQL-92, suportado pela fonte de dados.  
  
 A máscara de bit sadia é usada para determinar quais cláusulas são suportadas:  
  
 SQL_DCS_DROP_CHARACTER_SET  
  
 Um driver sql-92 completo de conformidade de nível sempre retornará esta opção conforme suportado.  
  
 SQL_DROP_COLLATION (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando as cláusulas na declaração **DROP COLLATION,** conforme definido no SQL-92, suportado pela fonte de dados.  
  
 A máscara de bit sadia é usada para determinar quais cláusulas são suportadas:  
  
 SQL_DC_DROP_COLLATION  
  
 Um driver sql-92 completo de conformidade de nível sempre retornará esta opção conforme suportado.  
  
 SQL_DROP_DOMAIN (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando as cláusulas na declaração **DROP DOMAIN,** conforme definido no SQL-92, suportado pela fonte de dados.  
  
 As seguintes máscaras de bit são usadas para determinar quais cláusulas são suportadas:  
  
 SQL_DD_DROP_DOMAINSQL_DD_CASCADESQL_DD_RESTRICT  
  
 Um driver de conformidade de nível intermediário SQL-92 sempre retornará todas essas opções conforme suportado.  
  
 SQL_DROP_SCHEMA (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando as cláusulas na declaração **DROP SCHEMA,** conforme definido no SQL-92, suportado pela fonte de dados.  
  
 As seguintes máscaras de bit são usadas para determinar quais cláusulas são suportadas:  
  
 SQL_DS_DROP_SCHEMASQL_DS_CASCADESQL_DS_RESTRICT  
  
 Um driver de conformidade de nível intermediário SQL-92 sempre retornará todas essas opções conforme suportado.  
  
 SQL_DROP_TABLE (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando as cláusulas na declaração **TABELA DROP,** conforme definido no SQL-92, suportado pela fonte de dados.  
  
 As seguintes máscaras de bit são usadas para determinar quais cláusulas são suportadas:  
  
 SQL_DT_DROP_TABLESQL_DT_CASCADESQL_DT_RESTRICT  
  
 Um driver de conformidade de nível FIPS Transitional sempre retornará todas essas opções conforme suportado.  
  
 SQL_DROP_TRANSLATION (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando as cláusulas na declaração **DROP TRANSLATION,** conforme definido no SQL-92, suportado pela fonte de dados.  
  
 A máscara de bit sadia é usada para determinar quais cláusulas são suportadas:  
  
 SQL_DTR_DROP_TRANSLATION  
  
 Um driver sql-92 completo de conformidade de nível sempre retornará esta opção conforme suportado.  
  
 SQL_DROP_VIEW (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando as cláusulas na declaração **DROP VIEW,** conforme definido no SQL-92, suportado pela fonte de dados.  
  
 As seguintes máscaras de bit são usadas para determinar quais cláusulas são suportadas:  
  
 SQL_DV_DROP_VIEWSQL_DV_CASCADESQL_DV_RESTRICT  
  
 Um driver de conformidade de nível FIPS Transitional sempre retornará todas essas opções conforme suportado.  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER que descreve os atributos de um cursor dinâmico que são suportados pelo driver. Esta máscara de bitcontém o primeiro subconjunto de atributos; para o segundo subconjunto, veja SQL_DYNAMIC_CURSOR_ATTRIBUTES2.  
  
 As seguintes máscaras de bit são usadas para determinar quais atributos são suportados:  
  
 SQL_CA1_NEXT = Um argumento *FetchOrientation* de SQL_FETCH_NEXT é suportado em uma chamada para **SQLFetchScroll** quando o cursor é um cursor dinâmico.  
  
 SQL_CA1_ABSOLUTE = Os argumentos *FetchOrientation* de SQL_FETCH_FIRST, SQL_FETCH_LAST e SQL_FETCH_ABSOLUTE são suportados em uma chamada para **SQLFetchScroll** quando o cursor é um cursor dinâmico. (O conjunto de linhas que será buscado é independente da posição atual do cursor.)  
  
 SQL_CA1_RELATIVE = Os argumentos *FetchOrientation* de SQL_FETCH_PRIOR e SQL_FETCH_RELATIVE são suportados em uma chamada para **SQLFetchScroll** quando o cursor é um cursor dinâmico. (O conjunto de linhas que será buscado depende da posição atual do cursor. Observe que isso é separado de SQL_FETCH_NEXT porque em um cursor somente para frente, apenas SQL_FETCH_NEXT é suportado.)  
  
 SQL_CA1_BOOKMARK = Um argumento *FetchOrientation* de SQL_FETCH_BOOKMARK é suportado em uma chamada para **SQLFetchScroll** quando o cursor é um cursor dinâmico.  
  
 SQL_CA1_LOCK_EXCLUSIVE = Um argumento *LockType* de SQL_LOCK_EXCLUSIVE é suportado em uma chamada para **SQLSetPos** quando o cursor é um cursor dinâmico.  
  
 SQL_CA1_LOCK_NO_CHANGE = Um argumento *LockType* de SQL_LOCK_NO_CHANGE é suportado em uma chamada para **SQLSetPos** quando o cursor é um cursor dinâmico.  
  
 SQL_CA1_LOCK_UNLOCK = Um argumento *LockType* de SQL_LOCK_UNLOCK é suportado em uma chamada para **SQLSetPos** quando o cursor é um cursor dinâmico.  
  
 SQL_CA1_POS_POSITION = Um argumento de *Operação* de SQL_POSITION é suportado em uma chamada para **SQLSetPos** quando o cursor é um cursor dinâmico.  
  
 SQL_CA1_POS_UPDATE = Um argumento de *Operação* de SQL_UPDATE é suportado em uma chamada para **SQLSetPos** quando o cursor é um cursor dinâmico.  
  
 SQL_CA1_POS_DELETE = Um argumento de *Operação* de SQL_DELETE é suportado em uma chamada para **SQLSetPos** quando o cursor é um cursor dinâmico.  
  
 SQL_CA1_POS_REFRESH = Um argumento de *Operação* de SQL_REFRESH é suportado em uma chamada para **SQLSetPos** quando o cursor é um cursor dinâmico.  
  
 SQL_CA1_POSITIONED_UPDATE = Uma ATUALIZAÇÃO ONDE a declaração Atual de SQL é suportada quando o cursor é um cursor dinâmico. (Um driver de conformidade de nível de entrada SQL-92 sempre retornará essa opção conforme suportado.)  
  
 SQL_CA1_POSITIONED_DELETE = Uma EXCLUSão ONDE A corrente da declaração SQL é suportada quando o cursor é um cursor dinâmico. (Um driver de conformidade de nível de entrada SQL-92 sempre retornará essa opção conforme suportado.)  
  
 SQL_CA1_SELECT_FOR_UPDATE = Uma declaração Select For UPDATE SQL é suportada quando o cursor é um cursor dinâmico. (Um driver de conformidade de nível de entrada SQL-92 sempre retornará essa opção conforme suportado.)  
  
 SQL_CA1_BULK_ADD = Um argumento de *Operação* de SQL_ADD é suportado em uma chamada para **SQLBulkOperations** quando o cursor é um cursor dinâmico.  
  
 SQL_CA1_BULK_UPDATE_BY_BOOKMARK = Um argumento de *Operação* de SQL_UPDATE_BY_BOOKMARK é suportado em uma chamada para **SQLBulkOperations** quando o cursor é um cursor dinâmico.  
  
 SQL_CA1_BULK_DELETE_BY_BOOKMARK = Um argumento de *Operação* de SQL_DELETE_BY_BOOKMARK é suportado em uma chamada para **SQLBulkOperations** quando o cursor é um cursor dinâmico.  
  
 SQL_CA1_BULK_FETCH_BY_BOOKMARK = Um argumento de *Operação* de SQL_FETCH_BY_BOOKMARK é suportado em uma chamada para **SQLBulkOperations** quando o cursor é um cursor dinâmico.  
  
 Um driver de conformidade de nível intermediário SQL-92 geralmente retornará as opções SQL_CA1_NEXT, SQL_CA1_ABSOLUTE e SQL_CA1_RELATIVE como suportadas, porque suporta cursores roláveis através da declaração SQL FETCH incorporada. Como isso não determina diretamente o suporte sql subjacente, no entanto, os cursores roláveis podem não ser suportados, mesmo para um driver de conformidade de nível intermediário SQL-92.  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES2 (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER que descreve os atributos de um cursor dinâmico que são suportados pelo driver. Esta máscara de bitcontém o segundo subconjunto de atributos; para o primeiro subconjunto, veja SQL_DYNAMIC_CURSOR_ATTRIBUTES1.  
  
 As seguintes máscaras de bit são usadas para determinar quais atributos são suportados:  
  
 SQL_CA2_READ_ONLY_CONCURRENCY = Um cursor dinâmico somente leitura, no qual não são permitidas atualizações, é suportado. (O atributo de declaração SQL_ATTR_CONCURRENCY pode ser SQL_CONCUR_READ_ONLY para um cursor dinâmico).  
  
 SQL_CA2_LOCK_CONCURRENCY = Um cursor dinâmico que usa o nível mais baixo de bloqueio suficiente para garantir que a linha possa ser atualizada seja suportada. (O atributo de declaração SQL_ATTR_CONCURRENCY pode ser SQL_CONCUR_LOCK para um cursor dinâmico.) Esses bloqueios devem ser consistentes com o nível de isolamento da transação definido pelo atributo de conexão SQL_ATTR_TXN_ISOLATION.  
  
 SQL_CA2_OPT_ROWVER_CONCURRENCY = Um cursor dinâmico que usa o controle de concorrência otimista comparando versões de linha é suportado. (O atributo de declaração SQL_ATTR_CONCURRENCY pode ser SQL_CONCUR_ROWVER para um cursor dinâmico.)  
  
 SQL_CA2_OPT_VALUES_CONCURRENCY = Um cursor dinâmico que usa o controle de concorrência otimista comparando valores é suportado. (O atributo de declaração SQL_ATTR_CONCURRENCY pode ser SQL_CONCUR_VALUES para um cursor dinâmico.)  
  
 SQL_CA2_SENSITIVITY_ADDITIONS = As linhas adicionadas são visíveis a um cursor dinâmico; o cursor pode rolar até essas linhas. (Quando essas linhas são adicionadas ao cursor é dependente do motorista.)  
  
 SQL_CA2_SENSITIVITY_DELETIONS = As linhas excluídas não estão mais disponíveis para um cursor dinâmico e não deixam um "buraco" no conjunto de resultados; depois que o cursor dinâmico rola de uma linha excluída, ele não pode retornar a essa linha.  
  
 SQL_CA2_SENSITIVITY_UPDATES = Atualizações de linhas são visíveis para um cursor dinâmico; se o cursor dinâmico rolar e retornar a uma linha atualizada, os dados retornados pelo cursor são os dados atualizados, não os dados originais.  
  
 SQL_CA2_MAX_ROWS_SELECT = O atributo de declaração SQL_ATTR_MAX_ROWS afeta as instruções **SELECT** quando o cursor é um cursor dinâmico.  
  
 SQL_CA2_MAX_ROWS_INSERT = O atributo de declaração SQL_ATTR_MAX_ROWS afeta as instruções **INSERT** quando o cursor é um cursor dinâmico.  
  
 SQL_CA2_MAX_ROWS_DELETE = O atributo de declaração SQL_ATTR_MAX_ROWS afeta as instruções **DELETE** quando o cursor é um cursor dinâmico.  
  
 SQL_CA2_MAX_ROWS_UPDATE = O atributo de declaração SQL_ATTR_MAX_ROWS afeta as instruções **UPDATE** quando o cursor é um cursor dinâmico.  
  
 SQL_CA2_MAX_ROWS_CATALOG = O atributo de declaração SQL_ATTR_MAX_ROWS afeta os conjuntos de resultados **do CATALOG** quando o cursor é um cursor dinâmico.  
  
 SQL_CA2_MAX_ROWS_AFFECTS_ALL = O atributo de declaração SQL_ATTR_MAX_ROWS afeta as instruções **SELECT,** **INSERT,** **DELETE**e **UPDATE** e OS conjuntos de resultados **do CATÁLOGO,** quando o cursor é um cursor dinâmico.  
  
 SQL_CA2_CRC_EXACT = A contagem exata de linhas está disponível no campo de diagnóstico SQL_DIAG_CURSOR_ROW_COUNT quando o cursor é um cursor dinâmico.  
  
 SQL_CA2_CRC_APPROXIMATE = Uma contagem aproximada de linhas está disponível no campo de diagnóstico SQL_DIAG_CURSOR_ROW_COUNT quando o cursor é um cursor dinâmico.  
  
 SQL_CA2_SIMULATE_NON_UNIQUE = O driver não garante que as instruções de atualização ou exclusão posicionadas simuladas afetarão apenas uma linha quando o cursor for um cursor dinâmico; é responsabilidade do aplicativo garantir isso. (Se uma declaração afetar mais de uma linha, **SQLExecute** ou **SQLExecDirect** retornarão o SQLSTATE 01001 [conflito de operação cursor].) Para definir esse comportamento, o aplicativo chama **SQLSetStmtAttr** com o atributo SQL_ATTR_SIMULATE_CURSOR definido como SQL_SC_NON_UNIQUE.  
  
 SQL_CA2_SIMULATE_TRY_UNIQUE = O driver tenta garantir que as instruções de atualização ou exclusão posicionadas simuladas afetarão apenas uma linha quando o cursor for um cursor dinâmico. O driver sempre executa tais instruções, mesmo que possam afetar mais de uma linha, como quando não há uma chave única. (Se uma declaração afetar mais de uma linha, **SQLExecute** ou **SQLExecDirect** retornarão o SQLSTATE 01001 [conflito de operação cursor].) Para definir esse comportamento, o aplicativo chama **SQLSetStmtAttr** com o atributo SQL_ATTR_SIMULATE_CURSOR definido como SQL_SC_TRY_UNIQUE.  
  
 SQL_CA2_SIMULATE_UNIQUE = O driver garante que as instruções de atualização ou exclusão posicionadas simuladas afetarão apenas uma linha quando o cursor for um cursor dinâmico. Se o driver não puder garantir isso para uma determinada declaração, **SQLExecDirect** ou **SQLPrepare** retornar SQLSTATE 01001 (conflito de operação cursor). Para definir esse comportamento, o aplicativo chama **SQLSetStmtAttr** com o atributo SQL_ATTR_SIMULATE_CURSOR definido como SQL_SC_UNIQUE.  
  
 SQL_EXPRESSIONS_IN_ORDERBY (ODBC 1.0)  
 Uma seqüência de caracteres: "Y" se a fonte de dados suportar expressões na lista **ORDER BY;** "N" se não o fizer.  
  
 SQL_FILE_USAGE (ODBC 2.0)  
 Um valor SQLUSMALLINT que indica como um driver de nível único trata diretamente os arquivos em uma fonte de dados:  
  
 SQL_FILE_NOT_SUPPORTED = O driver não é um driver de nível único. Por exemplo, um driver ORACLE é um driver de dois níveis.  
  
 SQL_FILE_TABLE = Um driver de nível único trata arquivos em uma fonte de dados como tabelas. Por exemplo, um driver Xbase trata cada arquivo Xbase como uma tabela.  
  
 SQL_FILE_CATALOG = Um driver de nível único trata arquivos em uma fonte de dados como um catálogo. Por exemplo, um driver do Microsoft Access trata cada arquivo do Microsoft Access como um banco de dados completo.  
  
 Um aplicativo pode usar isso para determinar como os usuários selecionarão dados. Por exemplo, os usuários do Xbase geralmente pensam em dados como armazenados em arquivos, enquanto os usuários do ORACLE e do Microsoft Access geralmente pensam em dados como armazenados em tabelas.  
  
 Quando um usuário seleciona uma fonte de dados Xbase, o aplicativo pode exibir a caixa de diálogo comum Windows **File Open;** quando o usuário seleciona uma fonte de dados Microsoft Access ou ORACLE, o aplicativo pode exibir uma caixa de diálogo **Tabela seleto** personalizada.  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1 (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER que descreve os atributos de um cursor somente para frente que são suportados pelo driver. Esta máscara de bitcontém o primeiro subconjunto de atributos; para o segundo subconjunto, veja SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2.  
  
 As seguintes máscaras de bit são usadas para determinar quais atributos são suportados:  
  
 SQL_CA1_NEXTSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 Para obter descrições dessas máscaras de bit, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (e substitua o "cursor somente para a frente" por "cursor dinâmico" nas descrições).  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER que descreve os atributos de um cursor somente para frente que são suportados pelo driver. Esta máscara de bitcontém o segundo subconjunto de atributos; para o primeiro subconjunto, veja SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1.  
  
 As seguintes máscaras de bit são usadas para determinar quais atributos são suportados:  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_SIMULATE_UNIQUE  
  
 Para obter descrições dessas máscaras de bit, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES2 (e substitua o "cursor somente para a frente" por "cursor dinâmico" nas descrições).  
  
 SQL_GETDATA_EXTENSIONS (ODBC 2.0)  
 Uma máscara de bit SQLUINTEGER enumerando extensões para **SQLGetData**.  
  
 As seguintes máscaras de bit são usadas em conjunto com o sinalizador para determinar quais extensões comuns o driver suporta para **SQLGetData**:  
  
 SQL_GD_ANY_COLUMN = **SQLGetData** pode ser chamado para qualquer coluna desvinculada, incluindo aquelas antes da última coluna vinculada. Observe que as colunas devem ser chamadas por ordem de número de coluna ascendente, a menos que SQL_GD_ANY_ORDER também seja devolvida.  
  
 SQL_GD_ANY_ORDER = **SQLGetData** pode ser chamado para colunas desvinculadas em qualquer ordem. Observe que **o SQLGetData** só pode ser chamado para colunas após a última coluna vinculada, a menos que SQL_GD_ANY_COLUMN também seja devolvido.  
  
 SQL_GD_BLOCK = **SQLGetData** pode ser chamada para uma coluna desvinculada em qualquer linha em um bloco (onde o tamanho do conjunto de linhas é maior que 1) de dados após o posicionamento para essa linha com **SQLSetPos**.  
  
 SQL_GD_BOUND = **SQLGetData** pode ser chamado para colunas vinculadas, além de colunas não vinculadas. Um motorista não pode devolver esse valor a menos que ele também retorne SQL_GD_ANY_COLUMN.  
  
 SQL_GD_OUTPUT_PARAMS = **SQLGetData** pode ser chamado para retornar os valores do parâmetro de saída. Para obter mais informações, consulte [Recuperando parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
 **O SQLGetData** é obrigado a retornar dados somente de colunas não vinculadas que ocorrem após a última coluna vinculada, são chamados por ordem de aumentar o número da coluna e não estão em uma linha em um bloco de linhas.  
  
 Se um driver suportar marcadores (de comprimento fixo ou de comprimento variável), ele deve suportar a chamada **SQLGetData** na coluna 0. Esse suporte é necessário independentemente do que o driver retorna para uma chamada para **SQLGetInfo** com o *infoType*SQL_GETDATA_EXTENSIONS .  
  
 SQL_GROUP_BY (ODBC 2.0)  
 Um valor SQLUSMALLINT que especifica a relação entre as colunas na cláusula **GROUP BY** e as colunas não agregadas na lista de seleção:  
  
 SQL_GB_COLLATE = Uma cláusula **COLLATE** pode ser especificada no final de cada coluna de agrupamento. (ODBC 3.0)  
  
 SQL_GB_NOT_SUPPORTED = As cláusulas **GROUP BY** não são suportadas. (ODBC 2.0)  
  
 SQL_GB_GROUP_BY_EQUALS_SELECT = A cláusula **GROUP BY** deve conter todas as colunas não agregadas na lista de seleção. Não pode conter outras colunas. Por exemplo, **SELECT DEPT, MAX(WAGE) DO GRUPO DE FUNCIONÁRIOS DO DEPARTAMENTO**. (ODBC 2.0)  
  
 SQL_GB_GROUP_BY_CONTAINS_SELECT = A cláusula **GROUP BY** deve conter todas as colunas não agregadas na lista de seleção. Ele pode conter colunas que não estão na lista de seleção. Por exemplo, **SELECT DEPT, MAX(WAGE) DO GRUPO DE EMPREGADOS POR DEPT, AGE**. (ODBC 2.0)  
  
 SQL_GB_NO_RELATION = As colunas da cláusula **GROUP BY** e da lista de seleção não estão relacionadas. O significado de colunas não agrupadas e não agregadas na lista selecionada é dependente da origem dos dados. Por exemplo, **SELECT DEPT, SALÁRIO DO GRUPO DE EMPREGADOS POR DEPT, AGE**. (ODBC 2.0)  
  
 Um driver de conformidade de nível de entrada SQL-92 sempre retornará a opção SQL_GB_GROUP_BY_EQUALS_SELECT conforme suportado. Um driver sql-92 completo de conformidade de nível sempre retornará a opção SQL_GB_COLLATE conforme suportado. Se nenhuma das opções for suportada, a cláusula **GROUP BY** não será suportada pela fonte de dados.  
  
 SQL_IDENTIFIER_CASE(ODBC 1.0)  
 Um valor SQLUSMALLINT da seguinte forma:  
  
 SQL_IC_UPPER = Os identificadores em SQL não são sensíveis a maiúsculas e são armazenados em maiúsculas no catálogo do sistema.  
  
 SQL_IC_LOWER = Os identificadores em SQL não são sensíveis a maiúsculas e minúsculas no catálogo do sistema.  
  
 SQL_IC_SENSITIVE = Identificadores em SQL são sensíveis a maiúsculas e minúsculas e são armazenadas em caso misto no catálogo do sistema.  
  
 SQL_IC_MIXED = Os identificadores em SQL não são sensíveis a maiúsculas e minúsculas e são armazenados em caso misto no catálogo do sistema.  
  
 Como os identificadores no SQL-92 nunca são sensíveis a maiúsculas e minúsculas, um driver que se adapte estritamente ao SQL-92 (qualquer nível) nunca retornará a opção SQL_IC_SENSITIVE como suportado.  
  
 SQL_IDENTIFIER_QUOTE_CHAR (ODBC 1.0)  
 A seqüência de caracteres que é usada como delimitador de partida e final de um identificador citado (delimitado) em instruções SQL. (Os identificadores passados como argumentos para as funções ODBC não devem ser citados.) Se a fonte de dados não suportar identificadores citados, um branco será devolvido.  
  
 Essa seqüência de caracteres também pode ser usada para citar argumentos de função de catálogo quando o atributo de conexão SQL_ATTR_METADATA_ID é definido como SQL_TRUE.  
  
 Como o caractere de citação do identificador no SQL-92 é a marca de cotação dupla ("), um driver que se conforma estritamente com SQL-92 sempre retornará o caractere de marcação de cotação dupla.  
  
 SQL_INDEX_KEYWORDS (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER que enumera palavras-chave na declaração CREATE INDEX que são suportadas pelo driver:  
  
 SQL_IK_NONE = Nenhuma das palavras-chave é suportada.  
  
 SQL_IK_ASC = palavra-chave ASC é suportada.  
  
 SQL_IK_DESC = palavra-chave DESC é suportada.  
  
 SQL_IK_ALL = Todas as palavras-chave são suportadas.  
  
 Para ver se a declaração CREATE INDEX é suportada, um aplicativo chama **SQLGetInfo** com o SQL_DLL_INDEX tipo de informação.  
  
 SQL_INFO_SCHEMA_VIEWS (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando as visualizações no INFORMATION_SCHEMA que são suportadas pelo driver. As visualizações e o conteúdo de INFORMATION_SCHEMA são definidos no SQL-92.  
  
 O nível de conformidade SQL-92 ou FIPS no qual este recurso deve ser suportado é mostrado entre parênteses ao lado de cada máscara de bit.  
  
 As seguintes máscaras de bit são usadas para determinar quais visualizações são suportadas:  
  
 SQL_ISV_ASSERTIONS = Identifica as afirmações do catálogo que pertencem a um determinado usuário. (Nível completo)  
  
 SQL_ISV_CHARACTER_SETS = Identifica os conjuntos de caracteres do catálogo que podem ser acessados por um determinado usuário. (Nível intermediário)  
  
 SQL_ISV_CHECK_CONSTRAINTS = Identifica as restrições check que pertencem a um determinado usuário. (Nível intermediário)  
  
 SQL_ISV_COLLATIONS = Identifica as colações de caracteres para o catálogo que podem ser acessadas por um determinado usuário. (Nível completo)  
  
 SQL_ISV_COLUMN_DOMAIN_USAGE = Identifica colunas para o catálogo que dependem de domínios definidos no catálogo e são de propriedade de um determinado usuário. (Nível intermediário)  
  
 SQL_ISV_COLUMN_PRIVILEGES = Identifica os privilégios em colunas de tabelas persistentes disponíveis ou concedidas por um determinado usuário. (Nível de transição FIPS)  
  
 SQL_ISV_COLUMNS = Identifica as colunas de tabelas persistentes que podem ser acessadas por um determinado usuário. (Nível de transição FIPS)  
  
 SQL_ISV_CONSTRAINT_COLUMN_USAGE = Semelhante à CONSTRAINT_TABLE_USAGE vista, as colunas são identificadas para as várias restrições que pertencem a um determinado usuário. (Nível intermediário)  
  
 SQL_ISV_CONSTRAINT_TABLE_USAGE = Identifica as tabelas que são usadas por restrições (referenciais, únicas e afirmações) e são de propriedade de um determinado usuário. (Nível intermediário)  
  
 SQL_ISV_DOMAIN_CONSTRAINTS = Identifica as restrições de domínio (dos domínios do catálogo) que podem ser acessadas por um determinado usuário. (Nível intermediário)  
  
 SQL_ISV_DOMAINS = Identifica os domínios definidos em um catálogo que pode ser acessado pelo usuário. (Nível intermediário)  
  
 SQL_ISV_KEY_COLUMN_USAGE = Identifica colunas definidas no catálogo que são restritas como chaves por um determinado usuário. (Nível intermediário)  
  
 SQL_ISV_REFERENTIAL_CONSTRAINTS = Identifica as restrições referenciais que pertencem a um determinado usuário. (Nível intermediário)  
  
 SQL_ISV_SCHEMATA = Identifica os esquemas que pertencem a um determinado usuário. (Nível intermediário)  
  
 SQL_ISV_SQL_LANGUAGES = Identifica os níveis de conformidade SQL, opções e dialetos suportados pela implementação do SQL. (Nível intermediário)  
  
 SQL_ISV_TABLE_CONSTRAINTS = Identifica as restrições de tabela que pertencem a um determinado usuário. (Nível intermediário)  
  
 SQL_ISV_TABLE_PRIVILEGES = Identifica os privilégios em tabelas persistentes disponíveis ou concedidas por um determinado usuário. (Nível de transição FIPS)  
  
 SQL_ISV_TABLES = Identifica as tabelas persistentes definidas em um catálogo que podem ser acessadas por um determinado usuário. (Nível de transição FIPS)  
  
 SQL_ISV_TRANSLATIONS = Identifica traduções de caracteres para o catálogo que podem ser acessadas por um determinado usuário. (Nível completo)  
  
 SQL_ISV_USAGE_PRIVILEGES = Identifica os privilégios de USO em objetos de catálogo disponíveis ou de propriedade de um determinado usuário. (Nível de transição FIPS)  
  
 SQL_ISV_VIEW_COLUMN_USAGE = Identifica as colunas nas quais as visualizações do catálogo que pertencem a um determinado usuário são dependentes. (Nível intermediário)  
  
 SQL_ISV_VIEW_TABLE_USAGE = Identifica as tabelas nas quais as visualizações do catálogo que pertencem a um determinado usuário são dependentes. (Nível intermediário)  
  
 SQL_ISV_VIEWS = Identifica as tabelas visualizadas definidas neste catálogo que podem ser acessadas por um determinado usuário. (Nível de transição FIPS)  
  
 SQL_INSERT_STATEMENT (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER que indica suporte para instruções **INSERT:**  
  
 SQL_IS_INSERT_LITERALS  
  
 SQL_IS_INSERT_SEARCHED  
  
 SQL_IS_SELECT_INTO  
  
 Um driver de conformidade de nível de entrada SQL-92 sempre retornará todas essas opções conforme suportado.  
  
 SQL_INTEGRITY (ODBC 1.0)  
 Uma seqüência de caracteres: "Y" se a fonte de dados suportar o Centro de Aprimoramento de Integridade; "N" se não o fizer.  
  
 Este *InfoType* foi renomeado para ODBC 3.0 do ODBC 2.0 *InfoType* SQL_ODBC_SQL_OPT_IEF.  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES1 (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER que descreve os atributos de um cursor de conjunto de chaves que são suportados pelo driver. Esta máscara de bitcontém o primeiro subconjunto de atributos; para o segundo subconjunto, veja SQL_KEYSET_CURSOR_ATTRIBUTES2.  
  
 As seguintes máscaras de bit são usadas para determinar quais atributos são suportados:  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 Para obter descrições dessas máscaras de bit, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (e substitua o "cursor orientado por keyset" por "cursor dinâmico" nas descrições).  
  
 Um driver de conformidade de nível intermediário SQL-92 geralmente retornará as opções de SQL_CA1_NEXT, SQL_CA1_ABSOLUTE e SQL_CA1_RELATIVE como suportadas, porque o driver suporta cursores roláveis através da declaração SQL FETCH incorporada. Como isso não determina diretamente o suporte sql subjacente, no entanto, os cursores roláveis podem não ser suportados, mesmo para um driver de conformidade de nível intermediário SQL-92.  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES2 (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER que descreve os atributos de um cursor de conjunto de chaves que são suportados pelo driver. Esta máscara de bitcontém o segundo subconjunto de atributos; para o primeiro subconjunto, veja SQL_KEYSET_CURSOR_ATTRIBUTES1.  
  
 As seguintes máscaras de bit são usadas para determinar quais atributos são suportados:  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_SIMULATE_UNIQUE  
  
 Para obter descrições dessas máscaras de bit, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (e substitua o "cursor orientado por keyset" por "cursor dinâmico" nas descrições).  
  
 SQL_KEYWORDS (ODBC 2.0)  
 Uma seqüência de caracteres que contém uma lista separada por comuma de todas as palavras-chave específicas da fonte de dados. Esta lista não contém palavras-chave específicas para ODBC ou palavras-chave usadas tanto pela fonte de dados quanto pelo ODBC. Esta lista representa todas as palavras-chave reservadas; aplicativos interoperáveis não devem usar essas palavras em nomes de objetos.  
  
 Para obter uma lista de palavras-chave ODBC, consulte [Palavras-chave reservadas](../../../odbc/reference/appendixes/reserved-keywords.md) no [apêndice C: Gramática SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md). O **valor #define** SQL_ODBC_KEYWORDS contém uma lista separada por comuma de palavras-chave ODBC.  
  
 Apêndice C: Gramática SQL  
  
 SQL_LIKE_ESCAPE_CLAUSE (ODBC 2.0)  
 Uma seqüência de caracteres: "Y" se a fonte de dados suportar um caractere de fuga para o caractere percentual (%) e ressaltar o caráter (_) em um predicado **LIKE** e o driver suporta a sintaxe ODBC para definir um caractere de fuga de predicado **LIKE;** "N" caso contrário.  
  
 SQL_MAX_ASYNC_CONCURRENT_STATEMENTS (ODBC 3.0)  
 Um valor SQLUINTEGER que especifica o número máximo de instruções simultâneas ativas no modo assíncrono que o driver pode suportar em uma determinada conexão. Se não houver um limite específico ou o limite for desconhecido, este valor é zero.  
  
 SQL_MAX_BINARY_LITERAL_LEN (ODBC 2.0)  
 Um valor SQLUINTEGER que especifica o comprimento máximo (número de caracteres hexadecimal, excluindo o prefixo literal e o sufixo retornado pelo **SQLGetTypeInfo**) de um literal binário em uma declaração SQL. Por exemplo, o binário literal 0xFFAA tem um comprimento de 4. Se não houver comprimento máximo ou o comprimento for desconhecido, este valor será definido como zero.  
  
 SQL_MAX_CATALOG_NAME_LEN (ODBC 1.0)  
 Um valor SQLUSMALLINT que especifica o comprimento máximo de um nome de catálogo na fonte de dados. Se não houver comprimento máximo ou o comprimento for desconhecido, este valor será definido como zero.  
  
 Um driver FIPS Full conformant retornapelo menos 128.  
  
 Este *InfoType* foi renomeado para ODBC 3.0 do ODBC 2.0 *InfoType* SQL_MAX_QUALIFIER_NAME_LEN.  
  
 SQL_MAX_CHAR_LITERAL_LEN (ODBC 2.0)  
 Um valor SQLUINTEGER que especifica o comprimento máximo (número de caracteres, excluindo o prefixo literal e o sufixo retornado por **SQLGetTypeInfo**) de um caractere literal em uma declaração SQL. Se não houver comprimento máximo ou o comprimento for desconhecido, este valor será definido como zero.  
  
 SQL_MAX_COLUMN_NAME_LEN (ODBC 1.0)  
 Um valor SQLUSMALLINT que especifica o comprimento máximo de um nome de coluna na fonte de dados. Se não houver comprimento máximo ou o comprimento for desconhecido, este valor será definido como zero.  
  
 Um driver fips de nível de conformidade de nível retornará pelo menos 18. Um driver de conformidade de nível FIPS Intermediate retornará pelo menos 128.  
  
 SQL_MAX_COLUMNS_IN_GROUP_BY (ODBC 2.0)  
 Um valor SQLUSMALLINT que especifica o número máximo de colunas permitidas em uma cláusula **GROUP BY.** Se não houver um limite especificado ou o limite for desconhecido, este valor será definido como zero.  
  
 Um driver fips de nível de conformidade de nível retornará pelo menos 6. Um driver de conformidade de nível FIPS Intermediário retornará pelo menos 15.  
  
 SQL_MAX_COLUMNS_IN_INDEX (ODBC 2.0)  
 Um valor SQLUSMALLINT que especifica o número máximo de colunas permitidas em um índice. Se não houver um limite especificado ou o limite for desconhecido, este valor será definido como zero.  
  
 SQL_MAX_COLUMNS_IN_ORDER_BY (ODBC 2.0)  
 Um valor SQLUSMALLINT que especifica o número máximo de colunas permitidas em uma cláusula **ORDER BY.** Se não houver um limite especificado ou o limite for desconhecido, este valor será definido como zero.  
  
 Um driver fips de nível de conformidade de nível retornará pelo menos 6. Um driver de conformidade de nível FIPS Intermediário retornará pelo menos 15.  
  
 SQL_MAX_COLUMNS_IN_SELECT (ODBC 2.0)  
 Um valor SQLUSMALLINT que especifica o número máximo de colunas permitidas em uma lista selecionada. Se não houver um limite especificado ou o limite for desconhecido, este valor será definido como zero.  
  
 Um driver fips de nível de conformidade de nível retornará pelo menos 100. Um driver de conformidade de nível FIPS Intermediário retornará pelo menos 250.  
  
 SQL_MAX_COLUMNS_IN_TABLE (ODBC 2.0)  
 Um valor SQLUSMALLINT que especifica o número máximo de colunas permitidas em uma tabela. Se não houver um limite especificado ou o limite for desconhecido, este valor será definido como zero.  
  
 Um driver fips de nível de conformidade de nível retornará pelo menos 100. Um driver de conformidade de nível FIPS Intermediário retornará pelo menos 250.  
  
 SQL_MAX_CONCURRENT_ACTIVITIES (ODBC 1.0)  
 Um valor SQLUSMALLINT que especifica o número máximo de instruções ativas que o driver pode suportar para uma conexão. Uma instrução é definida como ativa se tiver resultados pendentes, com o termo "resultados" significando linhas de uma operação **SELECT** ou linhas afetadas por uma operação **INSERT**, **UPDATE**ou **DELETE** (como uma contagem de linhas), ou se estiver em um estado NEED_DATA. Esse valor pode refletir uma limitação imposta pelo driver ou pela fonte de dados. Se não houver um limite especificado ou o limite for desconhecido, este valor será definido como zero.  
  
 Este *InfoType* foi renomeado para ODBC 3.0 do ODBC 2.0 *InfoType* SQL_ACTIVE_STATEMENTS.  
  
 SQL_MAX_CURSOR_NAME_LEN (ODBC 1.0)  
 Um valor SQLUSMALLINT que especifica o comprimento máximo de um nome de cursor na fonte de dados. Se não houver comprimento máximo ou o comprimento for desconhecido, este valor será definido como zero.  
  
 Um driver fips de nível de conformidade de nível retornará pelo menos 18. Um driver de conformidade de nível FIPS Intermediate retornará pelo menos 128.  
  
 SQL_MAX_DRIVER_CONNECTIONS (ODBC 1.0)  
 Um valor SQLUSMALLINT que especifica o número máximo de conexões ativas que o driver pode suportar para um ambiente. Esse valor pode refletir uma limitação imposta pelo driver ou pela fonte de dados. Se não houver um limite especificado ou o limite for desconhecido, este valor será definido como zero.  
  
 Este *InfoType* foi renomeado para ODBC 3.0 do ODBC 2.0 *InfoType* SQL_ACTIVE_CONNECTIONS.  
  
 SQL_MAX_IDENTIFIER_LEN (ODBC 3.0)  
 Um SQLUSMALLINT que indica o tamanho máximo em caracteres que a fonte de dados suporta para nomes definidos pelo usuário.  
  
 Um driver fips de nível de conformidade de nível retornará pelo menos 18. Um driver de conformidade de nível FIPS Intermediate retornará pelo menos 128.  
  
 SQL_MAX_INDEX_SIZE (ODBC 2.0)  
 Um valor SQLUINTEGER que especifica o número máximo de bytes permitidos nos campos combinados de um índice. Se não houver um limite especificado ou o limite for desconhecido, este valor será definido como zero.  
  
 SQL_MAX_PROCEDURE_NAME_LEN (ODBC 1.0)  
 Um valor SQLUSMALLINT que especifica o comprimento máximo de um nome de procedimento na fonte de dados. Se não houver comprimento máximo ou o comprimento for desconhecido, este valor será definido como zero.  
  
 SQL_MAX_ROW_SIZE(ODBC 2.0)  
 Um valor SQLUINTEGER que especifica o comprimento máximo de uma única linha em uma tabela. Se não houver um limite especificado ou o limite for desconhecido, este valor será definido como zero.  
  
 Um driver fips entry-conformant retornará pelo menos 2.000. Um driver de conformidade de nível FIPS Intermediate retornará pelo menos 8.000.  
  
 SQL_MAX_ROW_SIZE_INCLUDES_LONG (ODBC 3.0)  
 Uma seqüência de caracteres: "Y" se o tamanho máximo da linha retornado para o SQL_MAX_ROW_SIZE tipo de informação inclua o comprimento de todas as colunas SQL_LONGVARCHAR e SQL_LONGVARBINARY na linha; "N" caso contrário.  
  
 SQL_MAX_SCHEMA_NAME_LEN (ODBC 1.0)  
 Um valor SQLUSMALLINT que especifica o comprimento máximo de um nome de esquema na fonte de dados. Se não houver comprimento máximo ou o comprimento for desconhecido, este valor será definido como zero.  
  
 Um driver fips de nível de conformidade de nível retornará pelo menos 18. Um driver de conformidade de nível FIPS Intermediate retornará pelo menos 128.  
  
 Este *InfoType* foi renomeado para ODBC 3.0 do ODBC 2.0 *InfoType* SQL_MAX_OWNER_NAME_LEN.  
  
 SQL_MAX_STATEMENT_LEN (ODBC 2.0)  
 Um valor SQLUINTEGER que especifica o comprimento máximo (número de caracteres, incluindo espaço em branco) de uma declaração SQL. Se não houver comprimento máximo ou o comprimento for desconhecido, este valor será definido como zero.  
  
 SQL_MAX_TABLE_NAME_LEN (ODBC 1.0)  
 Um valor SQLUSMALLINT que especifica o comprimento máximo de um nome de tabela na fonte de dados. Se não houver comprimento máximo ou o comprimento for desconhecido, este valor será definido como zero.  
  
 Um driver fips de nível de conformidade de nível retornará pelo menos 18. Um driver de conformidade de nível FIPS Intermediate retornará pelo menos 128.  
  
 SQL_MAX_TABLES_IN_SELECT (ODBC 2.0)  
 Um valor SQLUSMALLINT que especifica o número máximo de tabelas permitidas na cláusula **DE** uma declaração **SELECT.** Se não houver um limite especificado ou o limite for desconhecido, este valor será definido como zero.  
  
 Um driver fips de nível de conformidade de nível retornará pelo menos 15. Um driver de conformidade de nível FIPS Intermediário retornará pelo menos 50.  
  
 SQL_MAX_USER_NAME_LEN (ODBC 2.0)  
 Um valor SQLUSMALLINT que especifica o comprimento máximo de um nome de usuário na fonte de dados. Se não houver comprimento máximo ou o comprimento for desconhecido, este valor será definido como zero.  
  
 SQL_MULT_RESULT_SETS (ODBC 1.0)  
 Uma seqüência de caracteres: "Y" se a fonte de dados suportar vários conjuntos de resultados, "N" se não o fizer.  
  
 Para obter mais informações sobre vários conjuntos de resultados, consulte [Múltiplos resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 SQL_MULTIPLE_ACTIVE_TXN (ODBC 1.0)  
 Uma seqüência de caracteres: "Y" se o driver suportar mais de uma transação ativa ao mesmo tempo, "N" se apenas uma transação puder estar ativa a qualquer momento.  
  
 As informações devolvidas para este tipo de informação não se aplicam no caso de transações distribuídas.  
  
 SQL_NEED_LONG_DATA_LEN (ODBC 2.0)  
 Uma seqüência de caracteres: "Y" se a fonte de dados precisar do comprimento de um longo valor de dados (o tipo de dados é SQL_LONGVARCHAR, SQL_LONGVARBINARY ou um tipo de dados específico da fonte de dados longo) antes que esse valor seja enviado para a fonte de dados, "N" se não o fizer. Para obter mais informações, consulte [SQLBindParameter Function](../../../odbc/reference/syntax/sqlbindparameter-function.md) e [SQLSetPos Function](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
 SQL_NON_NULLABLE_COLUMNS (ODBC 1.0)  
 Um valor SQLUSMALLINT que especifica se a fonte de dados suporta NÃO NULA em colunas:  
  
 SQL_NNC_NULL = Todas as colunas devem ser anuladas.  
  
 SQL_NNC_NON_NULL = As colunas não podem ser anuladas. (A fonte de dados suporta a restrição de coluna **NÃO NULA** nas instruções **CREATE TABLE.)**  
  
 Um driver de conformidade de nível de entrada SQL-92 retornará SQL_NNC_NON_NULL.  
  
 SQL_NULL_COLLATION (ODBC 2.0)  
 Um valor SQLUSMALLINT que especifica onde nulls são classificados em um conjunto de resultados:  
  
 SQL_NC_END = NULLs são classificados no final do conjunto de resultados, independentemente das palavras-chave ASC ou DESC.  
  
 SQL_NC_HIGH = NULLs são classificados na extremidade alta do conjunto de resultados, dependendo das palavras-chave ASC ou DESC.  
  
 SQL_NC_LOW = NULLs são classificados na extremidade baixa do conjunto de resultados, dependendo das palavras-chave ASC ou DESC.  
  
 SQL_NC_START = NULLs são classificados no início do conjunto de resultados, independentemente das palavras-chave ASC ou DESC.  
  
 SQL_NUMERIC_FUNCTIONS (ODBC 1.0)  
 Nota: O tipo de informação foi introduzido no ODBC 1.0; cada bitmask é rotulado com a versão em que foi introduzido.  
  
 Uma máscara de bit SQLUINTEGER enumerando as funções numéricas escalares suportadas pelo driver e fonte de dados associada.  
  
 As seguintes máscaras de bit são usadas para determinar quais funções numéricas são suportadas:  
  
 SQL_FN_NUM_ABS (ODBC 1.0)SQL_FN_NUM_ACOS (ODBC 1.0)SQL_FN_NUM_ASIN (ODBC 1.0)SQL_FN_NUM_ATAN (ODBC 1.0)SQL_FN_NUM_ATAN2 (ODBC 1.0)SQL_FN_NUM_CEILING (ODBC 1.0)SQL_FN_NUM_COS (ODBC 1 .0)SQL_FN_NUM_COT (ODBC 1.0)SQL_FN_NUM_DEGREES (ODBC 2.0)SQL_FN_NUM_EXP (ODBC 1.0)SQL_FN_NUM_FLOOR (ODBC 1.0)SQL_FN_NUM_LOG (ODBC 1.0)SQL_FN_NUM_LOG10 (ODBC 2.0)SQL_FN_ NUM_MOD (ODBC 1.0)SQL_FN_NUM_PI (ODBC 1.0)SQL_FN_NUM_POWER (ODBC 2.0)SQL_FN_NUM_RADIANS (ODBC 2.0)SQL_FN_NUM_RAND (ODBC 1.0)SQL_FN_NUM_ROUND (ODBC 2.0)SQL_FN_NUM_SIGN (ODBC 1.0)SQL_FN_NUM_SIN (ODBC 1.0)SQL_FN_NUM_SQRT (ODBC 1.0)SQL_FN_NUM_TAN (ODBC 1.0)SQL_FN_NUM_TRUNCATE (ODBC 2.0)SQL_FN_NUM_TRUNCATE (ODBC 2.0)SQL_FN_NUM_TRUNCATE (ODBC 2.0) SQL_FN_NUM_TRUNCATE (ODBC 2.0)SQL_FN_NUM_TRUNCATE (ODBC 2.0)SQL_FN_NUM_TRUNCATE (ODBC 2.0)SQL_FN_NUM_TRUNCATE (ODBC 2.0)SQL_FN_NUM_TRUNCATE (ODBC 2.0)SQL_FN_NUM_TRUNCATE (ODBC 2.0)SQL_FN_NUM_TRUNCATE (ODBC 2.0)SQL_FN_NUM_TRUNCATE (ODBC 2.0)SQL_FN_NUM_TRUNCATE (ODBC 2.0)SQL_FN_NUM_TRUNCATE (ODBC 2.0)SQL_FN_NUM_TRUNCATE (ODBC 2.0)SQL_FN_NUM_TRUNCATE (ODBC 2.0)SQL_FN_NUM_TRUNCATE (ODBC 2.0)SQL_FN_NUM_TRUNCATE (ODBC 2.0)SQL_FN_NUM_TRUNCATE (ODBC 2.0)SQL_FN_NUM_TRUNCATE (ODBC 2.0)SQL_FN_NUM_TRUNCATE (ODBC 2.0)SQL_FN_NUM_TRUNCATE (ODBC 2.0)SQL_FN_NUM_TRUNCATE (ODBC 2.0)SQL_FN_NUM_TRUNCATE (ODBC 2.0)SQL_FN_NUM_TRUNCATE (  
  
 SQL_ODBC_INTERFACE_CONFORMANCE(ODBC 3.0)  
 Um valor SQLUINTEGER que indica o nível da interface ODBC 3 *.x* que o driver cumpre.  
  
 SQL_OIC_CORE: O nível mínimo que todos os motoristas da ODBC devem cumprir. Esse nível inclui elementos básicos da interface, como funções de conexão, funções para preparar e executar uma declaração SQL, funções básicas de metadados do conjunto de resultados, funções básicas do catálogo e assim por diante.  
  
 SQL_OIC_LEVEL1: Um nível que inclui a funcionalidade do nível de conformidade dos padrões principais, além de cursores roláveis, marcadores, atualizações posicionadas e exclusões, e assim por diante.  
  
 SQL_OIC_LEVEL2: Um nível que inclui a funcionalidade de nível de conformidade de padrões nível 1, além de recursos avançados, como cursores sensíveis; atualizar, excluir e atualizar por marcadores; suporte ao procedimento armazenado; funções de catálogo para chaves primárias e estrangeiras; suporte a vários catálogos; e assim por diante.  
  
 Para obter mais informações, consulte [Níveis de conformidade de interface](../../../odbc/reference/develop-app/interface-conformance-levels.md).  
  
 SQL_ODBC_VER(ODBC 1.0)  
 Uma seqüência de caracteres com a versão do ODBC à qual o Driver Manager está em conformidade. A versão é do formulário ##.#..0000, onde os dois primeiros dígitos são a versão principal e os próximos dois dígitos são a versão menor. Isso é implementado apenas no Driver Manager.  
  
 SQL_OJ_CAPABILITIES (ODBC 2.01)  
 Uma máscara de bit SQLUINTEGER enumerando os tipos de junções externas suportadas pelo driver e fonte de dados. As seguintes máscaras de bit são usadas para determinar quais tipos são suportados:  
  
 SQL_OJ_LEFT = As junções externas esquerdas são apoiadas.  
  
 SQL_OJ_RIGHT = As junções externas direitas são suportadas.  
  
 SQL_OJ_FULL = As adesões externas completas são suportadas.  
  
 SQL_OJ_NESTED = As adesões externas aninhadas são suportadas.  
  
 SQL_OJ_NOT_ORDERED = Os nomes da coluna na cláusula ON da junta externa não devem estar na mesma ordem que seus respectivos nomes de tabela na cláusula **OUTER JOIN.**  
  
 SQL_OJ_INNER = A mesa interna (a mesa direita em uma junta externa esquerda ou a mesa esquerda em uma junta externa direita) também pode ser usada em uma junta interna. Isso não se aplica a adesões externas completas, que não possuem uma tabela interna.  
  
 SQL_OJ_ALL_COMPARISON_OPS = O operador de comparação na cláusula ON pode ser qualquer um dos operadores de comparação da ODBC. Se este bit não for definido, apenas o operador de comparação equal (=) pode ser usado em adesões externas.  
  
 Se nenhuma dessas opções for devolvida como suportada, nenhuma cláusula de adesão externa será suportada.  
  
 Para obter informações sobre o suporte dos operadores de adesão relacional em uma declaração SELECT, conforme definido pelo SQL-92, consulte SQL_SQL92_RELATIONAL_JOIN_OPERATORS.  
  
 SQL_ORDER_BY_COLUMNS_IN_SELECT (ODBC 2.0)  
 Uma seqüência de caracteres: "Y" se as colunas na cláusula **ORDER BY** devem estar na lista de seleção; caso contrário, "N".  
  
 SQL_PARAM_ARRAY_ROW_COUNTS (ODBC 3.0)  
 Um SQLUINTEGER enumerando as propriedades do driver em relação à disponibilidade de contagem de linhas em uma execução parametrizada. Tem os seguintes valores:  
  
 SQL_PARC_BATCH = As contagens de linhas individuais estão disponíveis para cada conjunto de parâmetros. Isso é conceitualmente equivalente ao driver gerando um lote de instruções SQL, uma para cada parâmetro definido na matriz. Informações de erro estendidas podem ser recuperadas usando o campo descritor SQL_PARAM_STATUS_PTR.  
  
 SQL_PARC_NO_BATCH = Há apenas uma contagem de linhas disponível, que é a contagem cumulativa de linha resultante da execução da declaração para toda a matriz de parâmetros. Isso é conceitualmente equivalente ao tratamento da declaração juntamente com a matriz completa de parâmetros como uma unidade atômica. Os erros são tratados da mesma forma que se uma declaração fosse executada.  
  
 SQL_PARAM_ARRAY_SELECTS (ODBC 3.0)  
 Um SQLUINTEGER enumerando as propriedades do driver em relação à disponibilidade de conjuntos de resultados em uma execução parametrizada. Tem os seguintes valores:  
  
 SQL_PAS_BATCH = Há um conjunto de resultados disponível por conjunto de parâmetros. Isso é conceitualmente equivalente ao driver gerando um lote de instruções SQL, uma para cada parâmetro definido na matriz.  
  
 SQL_PAS_NO_BATCH = Há apenas um conjunto de resultados disponível, que representa o conjunto de resultados cumulativos resultante da execução da declaração para o conjunto completo de parâmetros. Isso é conceitualmente equivalente ao tratamento da declaração juntamente com a matriz completa de parâmetros como uma unidade atômica.  
  
 SQL_PAS_NO_SELECT = Um driver não permite que uma declaração de geração definida por resultado seja executada com uma matriz de parâmetros.  
  
 SQL_PROCEDURE_TERM (ODBC 1.0)  
 Uma seqüência de caracteres com o nome do fornecedor de origem de dados para um procedimento; por exemplo, "procedimento de banco de dados", "procedimento armazenado", "procedimento", "pacote" ou "consulta armazenada".  
  
 SQL_PROCEDURES (ODBC 1.0)  
 Uma seqüência de caracteres: "Y" se a fonte de dados suportar procedimentos e o driver suportar a sintaxe de invocação do procedimento ODBC; "N" caso contrário.  
  
 SQL_POS_OPERATIONS (ODBC 2.0)  
 Uma máscara de bit SQLINTEGER enumerando as operações de suporte em **SQLSetPos**.  
  
 As máscaras de bit sadias são usadas em conjunto com a bandeira para determinar quais opções são suportadas.  
  
 SQL_POS_POSITION (ODBC 2.0) SQL_POS_REFRESH (ODBC 2.0) SQL_POS_UPDATE (ODBC 2.0) SQL_POS_DELETE (ODBC 2.0) SQL_POS_ADD (ODBC 2.0)  
  
 SQL_QUOTED_IDENTIFIER_CASE (ODBC 2.0)  
 Um valor SQLUSMALLINT da seguinte forma:  
  
 SQL_IC_UPPER = Os identificadores citados no SQL não são sensíveis a maiúsculas e são armazenados em maiúsculas no catálogo do sistema.  
  
 SQL_IC_LOWER = Os identificadores citados no SQL não são sensíveis a maiúsculas e minúsculas no catálogo do sistema.  
  
 SQL_IC_SENSITIVE = Os identificadores citados no SQL são sensíveis a maiúsculas e minúsculas e são armazenados em case misto no catálogo do sistema. (Em um banco de dados compatível com SQL-92, os identificadores citados são sempre sensíveis a maiúsculas e minúsculas.)  
  
 SQL_IC_MIXED = Os identificadores citados no SQL não são sensíveis a maiúsculas e minúsculas e são armazenados em case misto no catálogo do sistema.  
  
 Um driver de conformidade de nível de entrada SQL-92 sempre retornará SQL_IC_SENSITIVE.  
  
 SQL_ROW_UPDATES (ODBC 1.0)  
 Uma seqüência de caracteres: "Y" se um cursor orientado por keyset ou um cursor misto mantiver versões ou valores de linha para todas as linhas buscadas e, portanto, pode detectar quaisquer atualizações que foram feitas a uma linha por qualquer usuário desde que a linha foi buscada pela última vez. (Isso se aplica apenas a atualizações, não a exclusões ou inserções.) O driver pode devolver o sinalizador SQL_ROW_UPDATED para a matriz de status da linha quando **SQLFetchScroll** for chamado. Caso contrário, "N".  
  
 SQL_SCHEMA_TERM (ODBC 1.0)  
 Uma seqüência de caracteres com o nome do fornecedor de origem de dados para um esquema; por exemplo, "proprietário", "ID de autorização" ou "Esquema".  
  
 A seqüência de caracteres pode ser devolvida na parte superior, inferior ou mista.  
  
 Um driver de conformidade de nível de entrada SQL-92 sempre retornará "esquema".  
  
 Este *InfoType* foi renomeado para ODBC 3.0 do ODBC 2.0 *InfoType* SQL_OWNER_TERM.  
  
 SQL_SCHEMA_USAGE (ODBC 2.0)  
 Uma máscara de bit SQLUINTEGER enumerando as instruções nas quais os esquemas podem ser usados:  
  
 SQL_SU_DML_STATEMENTS = Os Schemas são suportados em todas as instruções de linguagem de manipulação de dados: **SELECT**, **INSERT**, **UPDATE**, **DELETE**, e se suportado, **SELECIONE PARA ATUALIZAR** e posicionar as declarações de atualização e exclusão.  
  
 SQL_SU_PROCEDURE_INVOCATION = Schemas são apoiados na declaração de invocação do procedimento ODBC.  
  
 SQL_SU_TABLE_DEFINITION = Os schemas são suportados em todas as instruções de definição de tabela: **CREATE TABLE**, **CREATE VIEW**, ALTER **TABLE**, **DROP TABLE**e DROP **VIEW**.  
  
 SQL_SU_INDEX_DEFINITION = Os schemas são suportados em todas as demonstrações de definição de índice: **CREATE INDEX** e **DROP INDEX**.  
  
 SQL_SU_PRIVILEGE_DEFINITION = Os schemas são suportados em todas as declarações de definição de privilégios: **GRANT** e **REVOKE**.  
  
 Um driver de conformidade de nível de entrada SQL-92 sempre retornará as opções de SQL_SU_DML_STATEMENTS, SQL_SU_TABLE_DEFINITION e SQL_SU_PRIVILEGE_DEFINITION, conforme suportado.  
  
 Este *InfoType* foi renomeado para ODBC 3.0 do *InfoType* 2.0 da ODBC SQL_OWNER_USAGE.  
  
 SQL_SCROLL_OPTIONS (ODBC 1.0)  
 Nota: O tipo de informação foi introduzido no ODBC 1.0; cada bitmask é rotulado com a versão em que foi introduzido.  
  
 Uma máscara de bit SQLUINTEGER enumerando as opções de rolagem suportadas para cursores roláveis.  
  
 As seguintes máscaras de bit são usadas para determinar quais opções são suportadas:  
  
 SQL_SO_FORWARD_ONLY = O cursor só rola para a frente. (ODBC 1.0)  
  
 SQL_SO_STATIC = Os dados no conjunto de resultados são estáticos. (ODBC 2.0)  
  
 SQL_SO_KEYSET_DRIVEN = O driver salva e usa as teclas para cada linha no conjunto de resultados. (ODBC 1.0)  
  
 SQL_SO_DYNAMIC = O driver mantém as teclas para cada linha no conjunto de linhas (o tamanho do conjunto de teclas é o mesmo do tamanho do conjunto de linhas). (ODBC 1.0)  
  
 SQL_SO_MIXED = O driver mantém as teclas para cada linha do conjunto de chaves, e o tamanho do conjunto de teclas é maior do que o tamanho do conjunto de linhas. O cursor é acionado por keyset dentro do conjunto de chaves e dinâmico fora do conjunto de chaves. (ODBC 1.0)  
  
 Para obter informações sobre cursores roláveis, consulte [Cursors roláveis](../../../odbc/reference/develop-app/scrollable-cursors.md).  
  
 SQL_SEARCH_PATTERN_ESCAPE (ODBC 1.0)  
 Uma seqüência de caracteres especificando o que o driver suporta como um caractere de fuga que permite o uso do padrão corresponder metacaracteres sublinhar (_) e porcentagem de sinal (%) como caracteres válidos em padrões de pesquisa. Esse caractere de fuga se aplica apenas para os argumentos de função de catálogo que suportam strings de pesquisa. Se esta seqüência estiver vazia, o driver não suportará um caractere de fuga padrão de pesquisa.  
  
 Como esse tipo de informação não indica suporte geral do caractere de fuga no predicado **LIKE,** o SQL-92 não inclui requisitos para esta seqüência de caracteres.  
  
 Este *InfoType* está limitado às funções do catálogo. Para obter uma descrição do uso do caractere de fuga nas strings de padrão de pesquisa, consulte [Argumentos de valor de padrão](../../../odbc/reference/develop-app/pattern-value-arguments.md).  
  
 SQL_SERVER_NAME (ODBC 1.0)  
 Uma seqüência de caracteres com o nome do servidor específico da fonte de dados real; útil quando um nome de origem de dados é usado durante **sqlconnect,** **SQLDriverConnect**e **SQLBrowseConnect**.  
  
 SQL_SPECIAL_CHARACTERS (ODBC 2.0)  
 Uma seqüência de caracteres que contém todos os caracteres especiais (ou seja, todos os caracteres, exceto de a a a z, de A a Z, 0 a 9, e sublinhado) que podem ser usados em um nome identificador, como um nome de tabela, nome da coluna ou nome do índice, na fonte de dados. Por exemplo, "#$^". Se um identificador contiver um ou mais desses caracteres, o identificador deve ser um identificador delimitado.  
  
 SQL_SQL_CONFORMANCE (ODBC 3.0)  
 Um valor SQLUINTEGER que indica o nível de SQL-92 suportado pelo driver:  
  
 SQL_SC_SQL92_ENTRY = Nível de entrada compatível com SQL-92.  
  
 SQL_SC_FIPS127_2_TRANSITIONAL = compatível com nível transitório FIPS 127-2.  
  
 SQL_SC_SQL92_FULL = Nível completo compatível com SQL-92.  
  
 SQL_SC_ SQL92_INTERMEDIATE = Nível intermediário Compatível com SQL-92.  
  
 SQL_SQL92_DATETIME_FUNCTIONS (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando as funções escalares de data-hora que são suportadas pelo driver e pela fonte de dados associada, conforme definido no SQL-92.  
  
 As seguintes máscaras de bit são usadas para determinar quais funções de data-hora são suportadas:  
  
 SQL_SDF_CURRENT_DATESQL_SDF_CURRENT_TIMESQL_SDF_CURRENT_TIMESTAMP  
  
 SQL_SQL92_FOREIGN_KEY_DELETE_RULE (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando as regras suportadas para uma chave estrangeira em uma declaração **DELETE,** conforme definido no SQL-92.  
  
 As seguintes máscaras de bit são usadas para determinar quais cláusulas são suportadas pela fonte de dados:  
  
 SQL_SFKD_CASCADESQL_SFKD_NO_ACTIONSQL_SFKD_SET_DEFAULTSQL_SFKD_SET_NULL  
  
 Um driver de conformidade de nível FIPS Transitional sempre retornará todas essas opções conforme suportado.  
  
 SQL_SQL92_FOREIGN_KEY_UPDATE_RULE (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando as regras suportadas para uma chave estrangeira em uma declaração **UPDATE,** conforme definido no SQL-92.  
  
 As seguintes máscaras de bit são usadas para determinar quais cláusulas são suportadas pela fonte de dados:  
  
 SQL_SFKU_CASCADESQL_SFKU_NO_ACTIONSQL_SFKU_SET_DEFAULTSQL_SFKU_SET_NULL  
  
 Um driver sql-92 completo de conformidade de nível sempre retornará todas essas opções conforme suportado.  
  
 SQL_SQL92_GRANT (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando as cláusulas suportadas na declaração **GRANT,** conforme definido no SQL-92.  
  
 O nível de conformidade SQL-92 ou FIPS no qual este recurso deve ser suportado é mostrado entre parênteses ao lado de cada máscara de bit.  
  
 As seguintes máscaras de bit são usadas para determinar quais cláusulas são suportadas pela fonte de dados:  
  
 SQL_SG_DELETE_TABLE (Nível de Entrada)SQL_SG_INSERT_COLUMN (Nível Intermediário)SQL_SG_INSERT_TABLE (Nível de Entrada) SQL_SG_REFERENCES_TABLE (Nível de Entrada)SQL_SG_REFERENCES_COLUMN (Nível de Entrada)SQL_SG_SELECT_TABLE (Nível de Entrada)SQL_SG_UPDATE_COLUMN (Nível de Entrada)SQL_SG_UPDATE_TABLE (Nível de Entrada) SQL_SG_USAGE_ON_DOMAIN (nível de transição FIPS)SQL_SG_USAGE_ON_CHARACTER_SET (nível de transição FIPS)SQL_SG_USAGE_ON_COLLATION (nível de transição FIPS)SQL_SG_USAGE_ON_TRANSLATION (FIPS Transitional nível)SQL_SG_WITH_GRANT_OPTION (nível de entrada)  
  
 SQL_SQL92_NUMERIC_VALUE_FUNCTIONS (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando as funções escalares de valor numérico que são suportadas pelo driver e pela fonte de dados associada, conforme definido no SQL-92.  
  
 As seguintes máscaras de bit são usadas para determinar quais funções numéricas são suportadas:  
  
 SQL_SNVF_BIT_LENGTHSQL_SNVF_CHAR_LENGTHSQL_SNVF_CHARACTER_LENGTHSQL_SNVF_EXTRACTSQL_SNVF_OCTET_LENGTHSQL_SNVF_POSITION  
  
 SQL_SQL92_PREDICATES (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando os predicados suportados em uma declaração **SELECT,** conforme definido no SQL-92.  
  
 O nível de conformidade SQL-92 ou FIPS no qual este recurso deve ser suportado é mostrado entre parênteses ao lado de cada máscara de bit.  
  
 As seguintes máscaras de bit são usadas para determinar quais opções são suportadas pela fonte de dados:  
  
 SQL_SP_BETWEEN (Nível de entrada)SQL_SP_COMPARISON (Nível de Entrada)SQL_SP_EXISTS (Nível de Entrada)SQL_SP_IN (Nível de Entrada)SQL_SP_ISNOTNULL (Nível de Entrada)SQL_SP_ISNULL (Nível de Entrada)SQL_SP_LIKE (Nível de Entrada)SQL_SP_MATCH_FULL (Nível Completo)SQL_SP_MATCH_PARTIAL(Nível Completo)SQL_SP_MATCH_UNIQUE_FULL (Nível Completo)SQL_SP_MATCH_UNIQUE_PARTIAL (Nível Completo)SQL_SP_OVERLAPS (Nível de Transição FIPS)SQL_SP_QUANTIFIED_COMPARISON (Nível de Entrada)SQL_SP_UNIQUE (Nível de Entrada)  
  
 SQL_SQL92_RELATIONAL_JOIN_OPERATORS (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando os operadores de juntação relacional suportados em uma declaração **SELECT,** conforme definido no SQL-92.  
  
 O nível de conformidade SQL-92 ou FIPS no qual este recurso deve ser suportado é mostrado entre parênteses ao lado de cada máscara de bit.  
  
 As seguintes máscaras de bit são usadas para determinar quais opções são suportadas pela fonte de dados:  
  
 SQL_SRJO_CORRESPONDING_CLAUSE (nível intermediário)SQL_SRJO_CROSS_JOIN (nível completo)SQL_SRJO_EXCEPT_JOIN (nível intermediário)SQL_SRJO_FULL_OUTER_JOIN (nível intermediário) SQL_SRJO_INNER_JOIN (nível de transição FIPS)SQL_SRJO_INTERSECT_JOIN (nível intermediário)SQL_SRJO_LEFT_OUTER_JOIN (nível transitório FIPS)SQL_SRJO_NATURAL_JOIN (nível transitório FIPS)SQL_SRJO_RIGHT_OUTER_JOIN (nível de transição FIPS)SQL_SRJO_UNION_JOIN (nível completo)  
  
 SQL_SRJO_INNER_JOIN indica suporte para a sintaxe **INNER JOIN,** não para a capacidade de adesão interna. O suporte para a sintaxe **INNER JOIN** é FIPS TRANSITIONAL, enquanto o suporte para a capacidade de adesão interna é **ENTRY**.  
  
 SQL_SQL92_REVOKE(ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando as cláusulas suportadas na declaração **REVOKE,** conforme definido no SQL-92, suportado pela fonte de dados.  
  
 O nível de conformidade SQL-92 ou FIPS no qual este recurso deve ser suportado é mostrado entre parênteses ao lado de cada máscara de bit.  
  
 As seguintes máscaras de bit são usadas para determinar quais cláusulas são suportadas pela fonte de dados:  
  
 SQL_SR_CASCADE (nível de transição FIPS) SQL_SR_DELETE_TABLE (Nível de Entrada)SQL_SR_GRANT_OPTION_FOR (Nível Intermediário) SQL_SR_INSERT_COLUMN (Nível Intermediário)SQL_SR_INSERT_TABLE (Nível de Entrada)SQL_SR_REFERENCES_COLUMN (Nível de Entrada)SQL_SR_REFERENCES_TABLE (Nível de Entrada)SQL_SR_RESTRICT (nível de transição FIPS)SQL_SR_SELECT_TABLE (Nível de Entrada)SQL_SR_UPDATE_COLUMN (Nível de Entrada)SQL_SR_UPDATE_TABLE (Nível de Entrada)SQL_SR_USAGE_ON_DOMAIN (nível de transição FIPS)SQL_SR_USAGE_ON_CHARACTER_ SET (nível de transição FIPS)SQL_SR_USAGE_ON_COLLATION (nível de transição FIPS)SQL_SR_USAGE_ON_TRANSLATION (nível de transição FIPS)  
  
 SQL_SQL92_ROW_VALUE_CONSTRUCTOR(ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando as expressões de construção de valor de linha suportadas em uma declaração **SELECT,** conforme definido no SQL-92. As seguintes máscaras de bit são usadas para determinar quais opções são suportadas pela fonte de dados:  
  
 SQL_SRVC_VALUE_EXPRESSION SQL_SRVC_NULL SQL_SRVC_DEFAULT SQL_SRVC_ROW_SUBQUERY  
  
 SQL_SQL92_STRING_FUNCTIONS (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando as funções escalares de seqüência de strings que são suportadas pelo driver e pela fonte de dados associada, conforme definido no SQL-92.  
  
 As seguintes máscaras de bit são usadas para determinar quais funções de string são suportadas:  
  
 SQL_SSF_CONVERTSQL_SSF_LOWERSQL_SSF_UPPERSQL_SSF_SUBSTRINGSQL_SSF_TRANSLATESQL_SSF_TRIM_BOTHSQL_SSF_TRIM_LEADINGSQL_SSF_TRIM_TRAILING  
  
 SQL_SQL92_VALUE_EXPRESSIONS (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando as expressões de valor suportadas, conforme definido no SQL-92.  
  
 O nível de conformidade SQL-92 ou FIPS no qual este recurso deve ser suportado é mostrado entre parênteses ao lado de cada máscara de bit.  
  
 As seguintes máscaras de bit são usadas para determinar quais opções são suportadas pela fonte de dados:  
  
 SQL_SVE_CASE (nível intermediário)SQL_SVE_CAST (nível FIPS Transitional)SQL_SVE_COALESCE (nível intermediário)SQL_SVE_NULLIF (nível intermediário)  
  
 SQL_STANDARD_CLI_CONFORMANCE (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando o padrão CLI ou padrões aos quais o driver está em conformidade. As seguintes máscaras de bit são usadas para determinar quais níveis o driver cumpre:  
  
 SQL_SCC_XOPEN_CLI_VERSION1: O driver está em conformidade com a versão 1 do Open Group CLI.  
  
 SQL_SCC_ISO92_CLI: O motorista está em conformidade com a ISO 92 CLI.  
  
 SQL_STATIC_CURSOR_ATTRIBUTES1 (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER que descreve os atributos de um cursor estático que são suportados pelo driver. Esta máscara de bitcontém o primeiro subconjunto de atributos; para o segundo subconjunto, veja SQL_STATIC_CURSOR_ATTRIBUTES2.  
  
 As seguintes máscaras de bit são usadas para determinar quais atributos são suportados:  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 Para obter descrições dessas máscaras de bit, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (e substitua o "cursor estático" por "cursor dinâmico" nas descrições).  
  
 Um driver de conformidade de nível intermediário SQL-92 geralmente retornará as opções de SQL_CA1_NEXT, SQL_CA1_ABSOLUTE e SQL_CA1_RELATIVE como suportadas, porque o driver suporta cursores roláveis através da declaração SQL FETCH incorporada. Como isso não determina diretamente o suporte sql subjacente, no entanto, os cursores roláveis podem não ser suportados, mesmo para um driver de conformidade de nível intermediário SQL-92.  
  
 SQL_STATIC_CURSOR_ATTRIBUTES2 (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER que descreve os atributos de um cursor estático que são suportados pelo driver. Esta máscara de bitcontém o segundo subconjunto de atributos; para o primeiro subconjunto, veja SQL_STATIC_CURSOR_ATTRIBUTES1.  
  
 As seguintes máscaras de bit são usadas para determinar quais atributos são suportados:  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_SIMULATE_UNIQUE  
  
 Para obter descrições dessas máscaras de bit, consulte SQL_DYNAMIC_CURSOR_ATTRIBUTES2 (e substitua o "cursor estático" por "cursor dinâmico" nas descrições).  
  
 SQL_STRING_FUNCTIONS (ODBC 1.0)  
 Nota: O tipo de informação foi introduzido no ODBC 1.0; cada bitmask é rotulado com a versão em que foi introduzido.  
  
 Uma máscara de bit SQLUINTEGER enumerando as funções de seqüência escalar suportadas pelo driver e a fonte de dados associada.  
  
 As seguintes máscaras de bit são usadas para determinar quais funções de string são suportadas:  
  
 SQL_FN_STR_ASCII (ODBC 1.0)SQL_FN_STR_BIT_LENGTH (ODBC 3.0)SQL_FN_STR_CHAR (ODBC 1.0)SQL_FN_STR_CHAR_LENGTH (ODBC 3.0)SQL_FN_STR_CHARACTER_LENGTH (ODBC 3.0)SQL_FN_STR_CONCAT (ODBC 1.0)SQL_FN_STR_DIFFERENCE (O DBC 2.0)SQL_FN_STR_INSERT (ODBC 1.0)SQL_FN_STR_LCASE (ODBC 1.0)SQL_FN_STR_LEFT (ODBC 1.0)SQL_FN_STR_LENGTH (ODBC 1.0)SQL_FN_STR_LOCATE (ODBC 1.0) SQL_FN_STR_LTRIM (ODBC 1.0) SQL_FN_STR_LTRIM (ODBC 1.0) SQL_FN_STR_OCTET_LENGTH (ODBC 3.0) SQL_FN_STR_POSITION (ODBC 3.0)SQL_FN_STR_REPEAT (ODBC 1.0)SQL_FN_STR_REPLACE (ODBC 1.0)SQL_FN_STR_RIGHT (ODBC 1.0)SQL_FN_STR_RTRIM (ODBC 1.0)SQL_FN_STR_SOUNDEX (ODBC 2.0)SQL_FN_STR_SPACE (ODBC 2.0)SQL_FN_STR_SUBSTRING (ODBC 1.0)SQL_FN_STR_UCASE (ODBC 1.0)SQL_FN_STR_UCASE (ODBC 1.0)SQL_FN_STR_UCASE (ODBC 1.0)  
  
 Se um aplicativo pode chamar a função **ESCALADOR LOCALIZAR** com os *argumentos string_exp1*, *string_exp2*e *iniciar,* o motorista retorna a máscara de bitSQL_FN_STR_LOCATE. Se um aplicativo pode chamar a função ESCALADOR LOCALIZAR com apenas os argumentos *string_exp1* e *string_exp2,* o motorista retorna a máscara de bitSQL_FN_STR_LOCATE_2. Os drivers que suportam totalmente a função **ESCALADOR LOCATE** retornam ambas as máscaras de bit.  
  
 (Para obter mais informações, consulte [Funções de corda](../../../odbc/reference/appendixes/string-functions.md) no apêndice E, "Funções escalares.")  
  
 SQL_SUBQUERIES (ODBC 2.0)  
 Uma máscara de bit SQLUINTEGER enumerando os predicados que suportam subquenias:  
  
 SQL_SQ_CORRELATED_SUBQUERIESSQL_SQ_COMPARISONSQL_SQ_EXISTSSQL_SQ_INSQL_SQ_QUANTIFIED  
  
 A máscara de bits SQL_SQ_CORRELATED_SUBQUERIES indica que todos os predicados que suportam subconsultas suportam subconsultas correlacionadas.  
  
 Um driver de conformidade de nível de entrada SQL-92 sempre retornará uma máscara de bits na qual todos esses bits estão definidos.  
  
 SQL_SYSTEM_FUNCTIONS (ODBC 1.0)  
 Uma máscara de bit SQLUINTEGER enumerando as funções do sistema escalar suportadas pelo driver e a fonte de dados associada.  
  
 As seguintes máscaras de bit são usadas para determinar quais funções do sistema são suportadas:  
  
 SQL_FN_SYS_DBNAMESQL_FN_SYS_IFNULLSQL_FN_SYS_USERNAME  
  
 SQL_TABLE_TERM (ODBC 1.0)  
 Uma seqüência de caracteres com o nome do fornecedor de origem de dados para uma tabela; por exemplo, "tabela" ou "arquivo".  
  
 Esta seqüência de caracteres pode estar em maiúsculas, minúsculas ou mistas.  
  
 Um driver de conformidade de nível de entrada SQL-92 sempre retorna "tabela".  
  
 SQL_TIMEDATE_ADD_INTERVALS(ODBC 2.0)  
 Uma máscara de bit SQLUINTEGER enumerando os intervalos de carimbo de tempo suportados pelo driver e a fonte de dados associada para a função escalar TIMESTAMPADD.  
  
 As seguintes máscaras de bit são usadas para determinar quais intervalos são suportados:  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 Um driver de conformidade de nível FIPS Transitional sempre retornará uma máscara de bits na qual todos esses bits estão definidos.  
  
 SQL_TIMEDATE_DIFF_INTERVALS (ODBC 2.0)  
 Uma máscara de bit SQLUINTEGER enumerando os intervalos de carimbo de tempo suportados pelo driver e a fonte de dados associada para a função escalar TIMESTAMPDIFF.  
  
 As seguintes máscaras de bit são usadas para determinar quais intervalos são suportados:  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 Um driver de conformidade de nível FIPS Transitional sempre retornará uma máscara de bits na qual todos esses bits estão definidos.  
  
 SQL_TIMEDATE_FUNCTIONS(ODBC 1.0)  
 Nota: O tipo de informação foi introduzido no ODBC 1.0; cada bitmask é rotulado com a versão em que foi introduzido.  
  
 Uma máscara de bit SQLUINTEGER enumerando as funções de data e hora escalares suportadas pelo driver e fonte de dados associada.  
  
 As seguintes máscaras de bit são usadas para determinar quais funções de data e hora são suportadas:  
  
 SQL_FN_TD_CURRENT_DATE ODBC 3.0)SQL_FN_TD_CURRENT_TIME (ODBC 3.0)SQL_FN_TD_CURRENT_TIMESTAMP (ODBC 3.0)SQL_FN_TD_CURDATE (ODBC 1.0)SQL_FN_TD_CURTIME (ODBC 1.0) SQL_FN_TD_DAYNAME (ODBC 2.0)SQL_FN_TD_DAYOFMONTH (ODBC 2.0)SQL_FN_TD_DAYOFMONTH (ODBC BC 1.0)SQL_FN_TD_DAYOFWEEK (ODBC 1.0)SQL_FN_TD_DAYOFYEAR (ODBC 1.0) SQL_FN_TD_EXTRACT (ODBC 3.0)SQL_FN_TD_HOUR (ODBC 1.0)SQL_FN_TD_MINUTE (ODBC 1.0)SQL_FN_TD_MONTH (ODBC 1.0)SQL_FN_TD_MONTHNAME (ODBC 2.0)SQL_FN_TD_NOW (ODBC 1.0)SQL_FN_TD_QUARTER (ODBC 1.0)SQL_FN_TD_SECOND (ODBC 1.0)SQL_FN_TD_TIMESTAMPADD (ODBC 2.0)SQL_FN_TD_TIMESTAMPDIFF (ODBC 2.0)SQL_FN_TD_WEEK (ODBC 1.0)SQL_FN_TD_YEAR (ODBC 1.0)  
  
 SQL_TXN_CAPABLE (ODBC 1.0)  
 Nota: O tipo de informação foi introduzido no ODBC 1.0; cada valor de retorno é rotulado com a versão em que foi introduzido.  
  
 Um valor SQLUSMALLINT descrevendo o suporte à transação no driver ou na fonte de dados:  
  
 SQL_TC_NONE = Transações não suportadas. (ODBC 1.0)  
  
 SQL_TC_DML = As transações podem conter apenas instruções de Linguagem de Manipulação de Dados (DML)**(SELECT,** **INSERT,** **UPDATE,** **DELETE).** As instruções DDL (Data Definition Language, linguagem de definição de dados) encontradas em uma transação causam um erro. (ODBC 1.0)  
  
 SQL_TC_DDL_COMMIT = As transações podem conter apenas instruções DML. As demonstrações de DDL (**CREATE TABLE**, **DROP INDEX**, e assim por diante) encontradas em uma transação fazem com que a transação seja realizada. (ODBC 2.0)  
  
 SQL_TC_DDL_IGNORE = As transações podem conter apenas instruções DML. As declarações de DDL encontradas em uma transação são ignoradas. (ODBC 2.0)  
  
 SQL_TC_ALL = As transações podem conter instruções DDL e instruções DML em qualquer ordem. (ODBC 1.0)  
  
 (Como o suporte às transações é obrigatório no SQL-92, um driver conformante SQL-92 [qualquer nível] nunca retornará SQL_TC_NONE.)  
  
 SQL_TXN_ISOLATION_OPTION(ODBC 1.0)  
 Uma máscara de bit SQLUINTEGER enumerando os níveis de isolamento da transação disponíveis no driver ou na fonte de dados.  
  
 As seguintes máscaras de bit são usadas em conjunto com o sinalizador para determinar quais opções são suportadas:  
  
 SQL_TXN_READ_UNCOMMITTEDSQL_TXN_READ_COMMITTEDSQL_TXN_REPEATABLE_READSQL_TXN_SERIALIZABLE  
  
 Para obter descrições desses níveis de isolamento, consulte a descrição de SQL_DEFAULT_TXN_ISOLATION.  
  
 Para definir o nível de isolamento da transação, um aplicativo chama **SQLSetConnectAttr** para definir o atributo SQL_ATTR_TXN_ISOLATION. Para obter mais informações, consulte [SQLSetConnectAttr Function](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 Um driver de conformidade de nível de entrada SQL-92 sempre retornará SQL_TXN_SERIALIZABLE conforme suportado. Um driver de conformidade de nível FIPS Transitional sempre retornará todas essas opções conforme suportado.  
  
 SQL_UNION (ODBC 2.0)  
 Uma máscara de bit SQLUINTEGER enumerando o suporte à cláusula **da UNIÃO:**  
  
 SQL_U_UNION = A fonte de dados suporta a cláusula **da UNIÃO.**  
  
 SQL_U_UNION_ALL = A fonte de dados apoia a palavra-chave **ALL** na cláusula **da UNIÃO.** (**SQLGetInfo** retorna tanto SQL_U_UNION quanto SQL_U_UNION_ALL neste caso.)  
  
 Um driver de conformidade de nível de entrada SQL-92 sempre retornará essas duas opções como suportadas.  
  
 SQL_USER_NAME (ODBC 1.0)  
 Uma seqüência de caracteres com o nome usado em um banco de dados específico, que pode ser diferente do nome de login.  
  
 SQL_XOPEN_CLI_YEAR (ODBC 3.0)  
 Uma seqüência de caracteres que indica o ano de publicação da especificação do Grupo Aberto com a qual a versão do Gerenciador de Driver ODBC cumpre totalmente.  
  
 SQL_ACCESSIBLE_PROCEDURES (ODBC 1.0)  
 Uma seqüência de caracteres: "Y" se o usuário puder executar todos os procedimentos retornados pelo **SQLProcedures;** "N" se houver procedimentos retornados que o usuário não pode executar.  
  
 SQL_ACCESSIBLE_TABLES (ODBC 1.0)  
 Uma seqüência de caracteres: "Y" se o usuário tiver privilégios **SELECT** garantidos para todas as tabelas retornadas por **SQLTables;** "N" se houver tabelas retornadas que o usuário não pode acessar.  
  
 SQL_ACTIVE_ENVIRONMENTS(ODBC 3.0)  
 Um valor SQLUSMALLINT que especifica o número máximo de ambientes ativos que o driver pode suportar. Se não houver um limite especificado ou o limite for desconhecido, este valor será definido como zero.  
  
 SQL_AGGREGATE_FUNCTIONS (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando o suporte para funções de agregação:  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 Um driver de conformidade de nível de entrada SQL-92 sempre retornará todas essas opções conforme suportado.  
  
 SQL_ALTER_DOMAIN (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando as cláusulas na declaração **ALTER DOMAIN,** conforme definido no SQL-92, suportado pela fonte de dados. Um driver sql-92 completo compatível com nível sempre retornará todas as máscaras de bit. Um valor de retorno de "0" significa que a declaração **ALTER DOMAIN** não é suportada.  
  
 O nível de conformidade SQL-92 ou FIPS no qual este recurso deve ser suportado é mostrado entre parênteses ao lado de cada máscara de bit.  
  
 As seguintes máscaras de bit são usadas para determinar quais cláusulas são suportadas:  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT = A adição de uma restrição de domínio é suportada (nível completo)  
  
 SQL_AD_ADD_DOMAIN_DEFAULT \<= alterar \<domínio>> de cláusula padrão de domínio definido é suportado (nível completo)  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION \<= cláusula de definição de nome de restrição> é suportado para nomear restrição de domínio (nível intermediário)  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT \<= cláusula de restrição de domínio de queda> é suportado (nível completo)  
  
 SQL_AD_DROP_DOMAIN_DEFAULT \<= alterar \<domínio> a cláusula padrão de domínio de queda> é suportado (nível completo)  
  
 Os bits a seguir \<especificam os \<atributos de restrição suportados> se adicionar> de restrição de domínio for suportado (o bit SQL_AD_ADD_DOMAIN_CONSTRAINT está definido):  
  
 SQL_AD_ADD_CONSTRAINT_DEFERRABLE (nível completo)SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE (nível completo)SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED (nível completo)SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE (Nível Completo)  
  
 SQL_ALTER_TABLE (ODBC 2.0)  
 Uma máscara de bit SQLUINTEGER enumerando as cláusulas na declaração **ALTER TABLE** suportada pela fonte de dados.  
  
 O nível de conformidade SQL-92 ou FIPS no qual este recurso deve ser suportado é mostrado entre parênteses ao lado de cada máscara de bit.  
  
 As seguintes máscaras de bit são usadas para determinar quais cláusulas são suportadas:  
  
 SQL_AT_ADD_COLUMN_COLLATION \<= adicionar coluna> cláusula é suportada, com facilidade para especificar colagem de coluna (nível completo) (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_DEFAULT \<= adicionar> a cláusula é suportada, com facilidade para especificar padrões de coluna (nível de transição FIPS) (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_SINGLE \<= adicionar> de coluna é suportado (nível de transição FIPS) (ODBC 3.0)  
  
 SQL_AT_ADD_CONSTRAINT \<= adicionar> a cláusula é suportada, com facilidade para especificar restrições de coluna (nível de transição FIPS) (ODBC 3.0)  
  
 SQL_AT_ADD_TABLE_CONSTRAINT \<= adicionar a cláusula de> de restrição de tabela (nível de transição FIPS) (ODBC 3.0)  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION \<= definição de nome de restrição> é suportado para nomear restrições de coluna e tabela (nível intermediário) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_CASCADE \<= coluna de queda> CASCADE é suportada (nível de transição FIPS) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_DEFAULT \<= alterar \<coluna> cláusula padrão da coluna de queda> é suportado (nível intermediário) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_RESTRICT \<= coluna de queda> RESTRICT é suportado (nível de transição FIPS) (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT \<= coluna de queda> RESTRICT é suportado (nível de transição FIPS) (ODBC 3.0)  
  
 SQL_AT_SET_COLUMN_DEFAULT \<= alterar \<coluna> definir cláusula padrão da coluna> é suportado (nível intermediário) (ODBC 3.0)  
  
 Os bits a \<seguir especificam os atributos de restrição de suporte> se for em vez de especificar as restrições de coluna ou tabela (o SQL_AT_ADD_CONSTRAINT bit está definido):  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED (nível completo) (ODBC 3.0)SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE (nível completo) (ODBC 3.0)SQL_AT_CONSTRAINT_DEFERRABLE (nível completo) (ODBC 3.0)SQL_AT_CONSTRAINT_NON_DEFERRABLE (nível completo) (ODBC 3.0)  
  
 SQL_ASYNC_MODE (ODBC 3.0)  
 Um valor SQLUINTEGER que indica o nível de suporte assíncrono no driver:  
  
 SQL_AM_CONNECTION = A execução assíncrona do nível de conexão é suportada. Todas as alças de declaração associadas a uma determinada alça de conexão estão no modo assíncrono ou todas estão no modo síncrono. Uma alça de declaração em uma conexão não pode estar no modo assíncrono, enquanto outra alça de declaração na mesma conexão está no modo síncrono, e vice-versa.  
  
 SQL_AM_STATEMENT = Execução assíncrona nível de declaração é suportada. Algumas alças de declaração associadas a uma alça de conexão podem estar no modo assíncrono, enquanto outras alças de declaração na mesma conexão estão no modo síncrono.  
  
 SQL_AM_NONE = O modo assíncrono não é suportado.  
  
 SQL_BATCH_ROW_COUNT (ODBC 3.0)  
 Uma máscara de bit SQLUINTEGER enumerando o comportamento do driver em relação à disponibilidade de contagem de linhas. As seguintes máscaras de bit são usadas juntamente com o tipo de informação:  
  
 SQL_BRC_ROLLED_UP = As contagens de linha para declarações de INSERT, DELETE ou UPDATE consecutivas são enroladas em uma. Se esta broca não estiver definida, as contagens de linha estarão disponíveis para cada declaração.  
  
 SQL_BRC_PROCEDURES = Contagem de linhas, se houver, estão disponíveis quando um lote é executado em um procedimento armazenado. Se as contagens de linha estiverem disponíveis, elas podem ser enroladas ou disponíveis individualmente, dependendo da SQL_BRC_ROLLED_UP bit.  
  
 SQL_BRC_EXPLICIT = Contagens de linha, se houver, estão disponíveis quando um lote é executado diretamente ligando para **SQLExecute** ou **SQLExecDirect**. Se as contagens de linha estiverem disponíveis, elas podem ser enroladas ou disponíveis individualmente, dependendo da SQL_BRC_ROLLED_UP bit.  
  
## <a name="example"></a>Exemplo  
 **SQLGetInfo** retorna listas de opções suportadas como uma máscara de bit SQLUINTEGER em **InfoValuePtr*. A máscara de bit para cada opção é usada juntamente com o sinalizador para determinar se a opção é suportada.  
  
 Por exemplo, um aplicativo pode usar o seguinte código para determinar se a função escalar SUBSTRING é suportada pelo driver associado à conexão.  
  
 Para outro exemplo de uso do **SQLGetInfo,** consulte [SQLTables Function](../../../odbc/reference/syntax/sqltables-function.md).  
  
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
  
 Determinar se um driver suporta uma função  
 [Função SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
 Retornando a configuração de um atributo de declaração  
 [Função SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)  
  
 Retornando informações sobre os tipos de dados de uma fonte de dados  
 [Função SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
