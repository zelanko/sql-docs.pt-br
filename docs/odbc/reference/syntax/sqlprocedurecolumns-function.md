---
title: Função SQLProcedureColumns | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLProcedureColumns
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLProcedureColumns
helpviewer_keywords:
- SQLProcedureColumns function [ODBC]
ms.assetid: 4ca37b28-a6df-465b-8988-d422d37fc025
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3d81e44b116ed6f26319d31430999a61a8a17f21
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306847"
---
# <a name="sqlprocedurecolumns-function"></a>Função SQLProcedureColumns
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: ODBC  
  
 **Resumo**  
 **SQLProcedureColumns** retorna a lista de parâmetros de entrada e saída, bem como as colunas que compõem o conjunto de resultados para os procedimentos especificados. O driver retorna as informações como um conjunto de resultados na instrução especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLProcedureColumns(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     ProcName,  
     SQLSMALLINT   NameLength3,  
     SQLCHAR *     ColumnName,  
     SQLSMALLINT   NameLength4);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 Entrada Identificador de instrução.  
  
 *CatalogName*  
 Entrada Nome do catálogo de procedimentos. Se um driver oferecer suporte a catálogos para alguns procedimentos, mas não para outros, como quando o driver recupera dados de DBMSs diferentes, uma cadeia de caracteres vazia ("") denota os procedimentos que não têm catálogos. *CatalogName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *CatalogName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *CatalogName* será um argumento comum; Ele é tratado literalmente e seu caso é significativo. Para obter mais informações, consulte [argumentos em funções de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 Entrada Comprimento em caracteres de **nome_do_catálogo*.  
  
 *SchemaName*  
 Entrada Padrão de pesquisa de cadeia de caracteres para nomes de esquema de procedimento. Se um driver oferecer suporte a esquemas para alguns procedimentos, mas não para outros, como quando o driver recupera dados de DBMSs diferentes, uma cadeia de caracteres vazia ("") denota os procedimentos que não têm esquemas.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *SchemaName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *SchemaName* é um argumento de valor de padrão; Ele é tratado literalmente e seu caso é significativo.  
  
 *NameLength2*  
 Entrada Comprimento em caracteres de **SchemaName*.  
  
 *Procname só*  
 Entrada Padrão de pesquisa de cadeia de caracteres para nomes de procedimento.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *ProcName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *ProcName* será um argumento de valor de padrão; Ele é tratado literalmente e seu caso é significativo.  
  
 *NameLength3*  
 Entrada Comprimento em caracteres de **ProcName*.  
  
 *ColumnName*  
 Entrada Padrão de pesquisa de cadeia de caracteres para nomes de coluna.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *ColumnName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *ColumnName* será um argumento de valor de padrão; Ele é tratado literalmente e seu caso é significativo.  
  
 *NameLength4*  
 Entrada Comprimento em caracteres de **ColumnName*.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLProcedureColumns** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *identificador* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLProcedureColumns** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado falhou antes da função concluir o processamento.|  
|24.000|Estado de cursor inválido|Um cursor estava aberto no *StatementHandle*e **SQLFetch** ou **SQLFetchScroll** foi chamado. Esse erro será retornado pelo Gerenciador de driver se **SQLFetch** ou **SQLFetchScroll** não tiver retornado SQL_NO_DATA e será retornado pelo driver se **SQLFetch** ou **SQLFetchScroll** tiver retornado SQL_NO_DATA.<br /><br /> Um cursor estava aberto no *StatementHandle*, mas **SQLFetch** ou **SQLFetchScroll** não tinha sido chamado.|  
|40001|Falha de serialização|A transação foi revertida devido a um deadlock de recurso com outra transação.|  
|40003|Conclusão de instrução desconhecida|A conexão associada falhou durante a execução dessa função, e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SqlError** no buffer * \*MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativo multithread.|  
|HY009|Uso inválido de ponteiro nulo|O atributo da instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, o argumento *CatalogName* era um ponteiro nulo e o SQL_CATALOG_NAME *InfoType* retorna que os nomes de catálogo têm suporte.<br /><br /> (DM) o atributo de instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, e o argumento *SchemaName*, *ProcName*ou *ColumnName* era um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *StatementHandle*. Esta função aynschronous ainda estava em execução quando a função SQLProcedureColumns foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para *StatementHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado para o *StatementHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|(DM) o valor de um dos argumentos de comprimento do nome era menor que 0, mas não é igual a SQL_NTS.<br /><br /> O valor de um dos argumentos de comprimento do nome excedeu o valor de comprimento máximo para o catálogo, o esquema, o procedimento ou o nome da coluna correspondente.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|Um catálogo de procedimentos foi especificado e o driver ou a fonte de dados não oferece suporte a catálogos.<br /><br /> Um esquema de procedimento foi especificado e o driver ou a fonte de dados não oferece suporte a esquemas.<br /><br /> Um padrão de pesquisa de cadeia de caracteres foi especificado para o esquema de procedimento, o nome do procedimento ou o nome da coluna, e a fonte de dados não oferece suporte a padrões de pesquisa para um ou mais desses argumentos.<br /><br /> A combinação das configurações atuais dos atributos de instrução SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE não era suportada pelo driver ou pela fonte de dados.<br /><br /> O atributo de instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE e o atributo de instrução SQL_ATTR_CURSOR_TYPE foi definido como um tipo de cursor para o qual o driver não dá suporte a indicadores.|  
|HYT00|Tempo limite esgotado|O período de tempo limite expirou antes que a fonte de dados retornasse o conjunto de resultados. O período de tempo limite é definido por meio de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *StatementHandle* não oferece suporte à função.|  
|IM017|A sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação for usado, a sondagem será desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesse identificador.|Se a chamada de função anterior no identificador retornar SQL_STILL_EXECUTING e se o modo de notificação estiver habilitado, **SQLCompleteAsync** deverá ser chamado na alça para executar o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 Essa função é normalmente usada antes da execução da instrução para recuperar informações sobre parâmetros de procedimento e as colunas que compõem o conjunto de resultados ou conjuntos retornados pelo procedimento, se houver. Para obter mais informações, consulte [Procedimentos](../../../odbc/reference/develop-app/procedures-odbc.md).  
  
> [!NOTE]  
>  **SQLProcedureColumns** pode não retornar todas as colunas usadas por um procedimento. Por exemplo, um driver pode retornar apenas informações sobre os parâmetros usados por um procedimento e não as colunas em um conjunto de resultados gerado por ele.  
  
 Os argumentos *schemas*, *ProcName*e *ColumnName* aceitam padrões de pesquisa. Para obter mais informações sobre padrões de pesquisa válidos, consulte [argumentos de valor de padrão](../../../odbc/reference/develop-app/pattern-value-arguments.md).  
  
> [!NOTE]  
>  Para obter mais informações sobre o uso geral, argumentos e dados retornados de funções de catálogo ODBC, consulte [Catalog Functions](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 **SQLProcedureColumns** retorna os resultados como um conjunto de resultados padrão, ordenados por PROCEDURE_CAT, PROCEDURE_SCHEM, PROCEDURE_NAME e COLUMN_TYPE. Os nomes de coluna são retornados para cada procedimento na seguinte ordem: o nome do valor de retorno, os nomes de cada parâmetro na invocação de procedimento (em ordem de chamada) e os nomes de cada coluna no conjunto de resultados retornados pelo procedimento (na ordem da coluna).  
  
 Os aplicativos devem associar colunas específicas do driver em relação ao final do conjunto de resultados. Para obter mais informações, consulte [dados retornados por funções de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
 Para determinar os comprimentos reais das colunas PROCEDURE_CAT, PROCEDURE_SCHEM, PROCEDURE_NAME e COLUMN_NAME, um aplicativo pode chamar **SQLGetInfo** com as opções SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_PROCEDURE_NAME_LEN e SQL_MAX_COLUMN_NAME_LEN.  
  
 As colunas a seguir foram renomeadas para ODBC 3. *x*. As alterações de nome de coluna não afetam a compatibilidade com versões anteriores porque os aplicativos são associados por número de coluna.  
  
|Coluna ODBC 2,0|ODBC 3. coluna *x*|  
|---------------------|-----------------------|  
|PROCEDURE_QUALIFIER|PROCEDURE_CAT|  
|PROCEDIMENTO _OWNER|PROCEDURE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 As colunas a seguir foram adicionadas ao conjunto de resultados retornado por **SQLProcedureColumns** para ODBC 3. *x*:  
  
-   COLUMN_DEF  
  
-   DATETIME_CODE  
  
-   CHAR_OCTET_LENGTH  
  
-   ORDINAL_POSITION  
  
-   IS_NULLABLE  
  
 A tabela a seguir lista as colunas no conjunto de resultados. Colunas adicionais além da coluna 19 (IS_NULLABLE) podem ser definidas pelo driver. Um aplicativo deve obter acesso a colunas específicas do driver, contando a partir do final do conjunto de resultados em vez de especificar uma posição ordinal explícita. Para obter mais informações, consulte [dados retornados por funções de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome da coluna|Número da coluna|Tipo de dados|Comentários|  
|-----------------|-------------------|---------------|--------------|  
|PROCEDURE_CAT (ODBC 2,0)|1|Varchar|Nome do catálogo de procedimentos; NULL se não for aplicável à fonte de dados. Se um driver oferecer suporte a catálogos para alguns procedimentos, mas não para outros, como quando o driver recupera dados de DBMSs diferentes, ele retorna uma cadeia de caracteres vazia ("") para os procedimentos que não têm catálogos.|  
|PROCEDURE_SCHEM (ODBC 2,0)|2|Varchar|Nome do esquema do procedimento; NULL se não for aplicável à fonte de dados. Se um driver oferecer suporte a esquemas para alguns procedimentos, mas não para outros, como quando o driver recupera dados de DBMSs diferentes, ele retorna uma cadeia de caracteres vazia ("") para os procedimentos que não têm esquemas.|  
|PROCEDURE_NAME (ODBC 2,0)|3|Varchar não nulo|Nome do procedimento. Uma cadeia de caracteres vazia é retornada para um procedimento que não tem um nome.|  
|COLUMN_NAME (ODBC 2,0)|4|Varchar não nulo|Nome da coluna de procedimento. O driver retorna uma cadeia de caracteres vazia para uma coluna de procedimento que não tem um nome.|  
|COLUMN_TYPE (ODBC 2,0)|5|Smallint não NULL|Define a coluna de procedimento como um parâmetro ou uma coluna de conjunto de resultados:<br /><br /> SQL_PARAM_TYPE_UNKNOWN: a coluna de procedimento é um parâmetro cujo tipo é desconhecido. (ODBC 1,0)<br /><br /> SQL_PARAM_INPUT: a coluna de procedimento é um parâmetro de entrada. (ODBC 1,0)<br /><br /> SQL_PARAM_INPUT_OUTPUT: a coluna de procedimento é um parâmetro de entrada/saída. (ODBC 1,0)<br /><br /> SQL_PARAM_OUTPUT: a coluna de procedimento é um parâmetro de saída. (ODBC 2,0)<br /><br /> SQL_RETURN_VALUE: a coluna de procedimento é o valor de retorno do procedimento. (ODBC 2,0)<br /><br /> SQL_RESULT_COL: a coluna de procedimento é uma coluna de conjunto de resultados. (ODBC 1,0)|  
|DATA_TYPE (ODBC 2,0)|6|Smallint não NULL|Tipo de dados SQL. Pode ser um tipo de dados ODBC do SQL ou um tipo de dados SQL específico do driver. Para os tipos de dados DateTime e Interval, essa coluna retorna os tipos de dados conciso (por exemplo, SQL_TYPE_TIME ou SQL_INTERVAL_YEAR_TO_MONTH). Para obter uma lista de tipos de dados SQL ODBC válidos, consulte [tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md) no Apêndice D: tipos de dados. Para obter informações sobre tipos de dados do SQL específicos do driver, consulte a documentação do driver.|  
|TYPE_NAME (ODBC 2,0)|7|Varchar não nulo|Nome do tipo de dados dependente de fonte de dados; por exemplo, "CHAR", "VARCHAR", "MONEY", "LONG VARBINARY" ou "CHAR () para dados de BIT".|  
|COLUMN_SIZE (ODBC 2,0)|8|Integer|O tamanho da coluna da coluna procedimento na fonte de dados. NULL é retornado para os tipos de dados em que o tamanho da coluna não é aplicável. Para obter mais informações sobre precisão, consulte [tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice D: tipos de dados.|  
|BUFFER_LENGTH (ODBC 2,0)|9|Integer|O comprimento em bytes de dados transferidos em uma operação **SQLGetData** ou **sqlfetch** se SQL_C_DEFAULT for especificado. Para dados numéricos, esse tamanho pode ser diferente do tamanho dos dados armazenados na fonte de dados. Para obter mais informações, consulte [tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md), no Apêndice D: tipos de dados.|  
|DECIMAL_DIGITS (ODBC 2,0)|10|Smallint|Os dígitos decimais da coluna procedimento na fonte de dados. NULL é retornado para os tipos de dados em que os dígitos decimais não são aplicáveis. Para obter mais informações sobre dígitos decimais, consulte [tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md), no Apêndice D: tipos de dados.|  
|NUM_PREC_RADIX (ODBC 2,0)|11|Smallint|Para tipos de dados numéricos, 10 ou 2.<br /><br /> Se for 10, os valores em COLUMN_SIZE e DECIMAL_DIGITS fornecerão o número de dígitos decimais permitidos para a coluna. Por exemplo, uma coluna DECIMAL (12, 5) retornaria um NUM_PREC_RADIX de 10, um COLUMN_SIZE de 12 e uma DECIMAL_DIGITS de 5; uma coluna FLOAT pode retornar um NUM_PREC_RADIX de 10, um COLUMN_SIZE de 15 e uma DECIMAL_DIGITS de NULL.<br /><br /> Se 2, os valores em COLUMN_SIZE e DECIMAL_DIGITS fornecem o número de bits permitidos na coluna. Por exemplo, uma coluna FLOAT poderia retornar uma NUM_PREC_RADIX de 2, uma COLUMN_SIZE de 53 e uma DECIMAL_DIGITS de NULL.<br /><br /> NULL é retornado para os tipos de dados em que NUM_PREC_RADIX não é aplicável.|  
|NULLABLE (ODBC 2,0)|12|Smallint não NULL|Se a coluna de procedimento aceita um valor nulo:<br /><br /> SQL_NO_NULLS: a coluna de procedimento não aceita valores nulos.<br /><br /> SQL_NULLABLE: a coluna Procedure aceita valores nulos.<br /><br /> SQL_NULLABLE_UNKNOWN: não é conhecido se a coluna de procedimento aceita valores nulos.|  
|COMENTÁRIOS (ODBC 2,0)|13|Varchar|Uma descrição da coluna de procedimento.|  
|COLUMN_DEF (ODBC 3,0)|14|Varchar|O valor padrão da coluna.<br /><br /> Se NULL tiver sido especificado como o valor padrão, essa coluna será a palavra NULL, não colocada entre aspas. Se o valor padrão não puder ser representado sem truncamento, essa coluna conterá TRUNCAdo, sem aspas simples delimitados. Se nenhum valor padrão tiver sido especificado, essa coluna será nula.<br /><br /> O valor de COLUMN_DEF pode ser usado na geração de uma nova definição de coluna, exceto quando ele contém o valor TRUNCAdo.|  
|SQL_DATA_TYPE (ODBC 3,0)|15|Smallint não NULL|O valor do tipo de dados SQL como ele aparece no campo SQL_DESC_TYPE do descritor. Essa coluna é igual à DATA_TYPE coluna, exceto para os tipos de dados DateTime e Interval.<br /><br /> Para os tipos de dados DateTime e Interval, o campo SQL_DATA_TYPE no conjunto de resultados retornará SQL_INTERVAL ou SQL_DATETIME, e o campo SQL_DATETIME_SUB retornará o subcódigo para o tipo de dados Interval ou DateTime específico. (Consulte o [Apêndice D: tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).)|  
|SQL_DATETIME_SUB (ODBC 3,0)|16|Smallint|O código de subtipo para tipos de dados DateTime e Interval. Para outros tipos de dados, essa coluna retorna um valor nulo.|  
|CHAR_OCTET_LENGTH (ODBC 3,0)|17|Integer|O comprimento máximo em bytes de uma coluna de tipo de dados binary ou de caractere. Para todos os outros tipos de dados, essa coluna retorna um valor nulo.|  
|ORDINAL_POSITION (ODBC 3,0)|18|Integer não NULL|Para parâmetros de entrada e saída, a posição ordinal do parâmetro na definição do procedimento (em ordem crescente de parâmetros, começando em 1). Para um valor de retorno (se houver), 0 é retornado. Para colunas de conjunto de resultados, a posição ordinal da coluna no conjunto de resultados, com a primeira coluna no conjunto de resultados sendo o número 1. Se houver vários conjuntos de resultados, as posições ordinais da coluna serão retornadas de maneira específica do driver.|  
|IS_NULLABLE (ODBC 3,0)|19|Varchar|"Não" se a coluna não incluir valores nulos.<br /><br /> "Sim" se a coluna puder incluir nulos.<br /><br /> Esta coluna retorna uma cadeia de caracteres de comprimento zero se a possibilidade de nulidade for desconhecida.<br /><br /> As regras ISO são seguidas para determinar a possibilidade de nulidade. Um DBMS em conformidade com ISO SQL não pode retornar uma cadeia de caracteres vazia.<br /><br /> O valor retornado para esta coluna é diferente do valor retornado para a coluna NULLABLE. (Consulte a descrição da coluna ANULÁVEL.)|  
  
## <a name="code-example"></a>Exemplo de código  
 Consulte [chamadas de procedimento](../../../odbc/reference/develop-app/procedure-calls.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Associando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Buscando uma única linha ou um bloco de dados em uma direção somente de avanço|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Buscando um bloco de dados ou rolando por meio de um conjunto de resultados|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Retornando uma lista de procedimentos em uma fonte de dados|[Função SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
