---
title: "Função SQLProcedureColumns | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLProcedureColumns
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLProcedureColumns
helpviewer_keywords: SQLProcedureColumns function [ODBC]
ms.assetid: 4ca37b28-a6df-465b-8988-d422d37fc025
caps.latest.revision: "22"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 03b9d05021f44df544715823fb984d72d87bdce7
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="sqlprocedurecolumns-function"></a>Função SQLProcedureColumns
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 1.0 ODBC: ODBC  
  
 **Resumo**  
 **SQLProcedureColumns** retorna a lista de parâmetros de entrada e saída, bem como as colunas que compõem o conjunto de resultados para os procedimentos especificados. O driver retorna as informações como um conjunto de resultados na instrução especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
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
 [Entrada] Identificador de instrução.  
  
 *CatalogName*  
 [Entrada] Nome do catálogo de procedimento. Se um driver dá suporte a catálogos para alguns procedimentos, mas não para outras pessoas, como quando o driver recupera os dados de diferentes DBMSs, uma cadeia de caracteres vazia ("") denota esses procedimentos que não têm catálogos. *CatalogName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *CatalogName* é tratado como um identificador e o seu caso não é significativo. Se for SQL_FALSE, *CatalogName* é um argumento comum; ela será tratada literalmente e seu caso é significativo. Para obter mais informações, consulte [argumentos em funções de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Entrada] Comprimento em caracteres de **CatalogName*.  
  
 *SchemaName*  
 [Entrada] Padrão de pesquisa de cadeia de caracteres para nomes de esquema de procedimento. Se um driver dá suporte a esquemas para alguns procedimentos, mas não para outras pessoas, como quando o driver recupera os dados de diferentes DBMSs, uma cadeia de caracteres vazia ("") indica que esses procedimentos que não têm esquemas.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *SchemaName* é tratado como um identificador e o seu caso não é significativo. Se for SQL_FALSE, *SchemaName* é um argumento de valor padrão; ela será tratada literalmente e seu caso é significativo.  
  
 *NameLength2*  
 [Entrada] Comprimento em caracteres de **SchemaName*.  
  
 *ProcName*  
 [Entrada] Padrão de pesquisa de cadeia de caracteres para nomes de procedimento.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *ProcName* é tratado como um identificador e o seu caso não é significativo. Se for SQL_FALSE, *ProcName* é um argumento de valor padrão; ela será tratada literalmente e seu caso é significativo.  
  
 *NameLength3*  
 [Entrada] Comprimento em caracteres de **ProcName*.  
  
 *ColumnName*  
 [Entrada] Padrão de pesquisa de cadeia de caracteres para nomes de coluna.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *ColumnName* é tratado como um identificador e o seu caso não é significativo. Se for SQL_FALSE, *ColumnName* é um argumento de valor padrão; ela será tratada literalmente e seu caso é significativo.  
  
 *NameLength4*  
 [Entrada] Comprimento em caracteres de **ColumnName*.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLProcedureColumns** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* sql_handle_stmt e um *tratar* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLProcedureColumns** e explica cada uma no contexto dessa função; as descrições de SQLSTATEs retornadas pelo Driver é anterior a notação "(DM)" Manager. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|24000|Estado de cursor inválido|Um cursor foi aberto o *StatementHandle*, e **SQLFetch** ou **SQLFetchScroll** tivesse sido chamada. Esse erro é retornado pelo Gerenciador de Driver se **SQLFetch** ou **SQLFetchScroll** não retornou SQL_NO_DATA e é retornada pelo driver se **SQLFetch** ou **SQLFetchScroll** retornou SQL_NO_DATA.<br /><br /> Um cursor foi aberto o *StatementHandle*, mas **SQLFetch** ou **SQLFetchScroll** não tivesse sido chamada.|  
|40001|Falha na serialização|A transação foi revertida devido a um deadlock de recursos com outra transação.|  
|40003|Conclusão de instrução desconhecido|A conexão associada falhou durante a execução dessa função e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo **SQLError** no  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em uma aplicativos multithread.|  
|HY009|Uso inválido de ponteiro nulo|O atributo de instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, o *CatalogName* argumento era um ponteiro nulo e o SQL_CATALOG_NAME *informação* retorna nomes de catálogo é suportadas.<br /><br /> (DM), o atributo da instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE e o *SchemaName*, *ProcName*, ou *ColumnName* argumento era um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função aynschronous ainda estava em execução quando a função SQLProcedureColumns foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *StatementHandle* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada antes de recuperação para todos os parâmetros de fluxo de dados.<br /><br /> (DM) uma função de execução assíncrona (não la) foi chamada para o *StatementHandle* e ainda estava em execução quando esta função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retorna SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todas as colunas ou parâmetros de dados em execução.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM) o valor de um dos argumentos de comprimento de nome era menor do que 0 mas não igual a SQL_NTS.<br /><br /> O valor de um dos argumentos de comprimento de nome excedeu o valor de comprimento máximo para o catálogo correspondente, o esquema, o procedimento ou o nome da coluna.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecido. Somente Desconecte e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|Um catálogo de procedimento foi especificado e o driver ou fonte de dados não dá suporte a catálogos.<br /><br /> Foi especificado um esquema de procedimento e o driver ou fonte de dados não dá suporte a esquemas.<br /><br /> Um padrão de cadeia de caracteres de pesquisa foi especificado para o esquema de procedimento, o nome do procedimento ou o nome da coluna e a fonte de dados não dá suporte a padrões de pesquisa para um ou mais desses argumentos.<br /><br /> A combinação das configurações atuais dos atributos de instrução SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE não era compatível com a driver ou fonte de dados.<br /><br /> O atributo da instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE, e o atributo de instrução SQL_ATTR_CURSOR_TYPE foi definido como um tipo de cursor para o qual o driver não oferecer suporte a indicadores.|  
|HYT00|Tempo limite esgotado|O período de tempo limite expirou antes da fonte de dados retornou o conjunto de resultados. O período de tempo limite é definido por meio de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|O driver em (DM) associado a *StatementHandle* não oferece suporte para a função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem está desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior na alça retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 Esta função geralmente é usada antes da execução da instrução para recuperar informações sobre parâmetros de procedimento e as colunas que compõem o conjunto de resultados ou conjuntos retornados pelo procedimento, se houver. Para obter mais informações, consulte [procedimentos](../../../odbc/reference/develop-app/procedures-odbc.md).  
  
> [!NOTE]  
>  **SQLProcedureColumns** não pode retornar todas as colunas usadas por um procedimento. Por exemplo, um driver pode retornar apenas informações sobre os parâmetros usados por um procedimento e não as colunas em um conjunto de resultados gerado.  
  
 O *SchemaName*, *ProcName*, e *ColumnName* argumentos aceitam padrões de pesquisa. Para obter mais informações sobre os padrões de pesquisa válidos, consulte [argumentos de valor padrão](../../../odbc/reference/develop-app/pattern-value-arguments.md).  
  
> [!NOTE]  
>  Para obter mais informações sobre o uso geral, os argumentos e os dados retornados de funções de catálogo ODBC, consulte [funções de catálogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 **SQLProcedureColumns** retorna os resultados como um conjunto de resultados padrão, ordenado por PROCEDURE_CAT, PROCEDURE_SCHEM, PROCEDURE_NAME e COLUMN_TYPE. Nomes de coluna são retornados para cada procedimento na seguinte ordem: o nome do valor de retorno, os nomes de cada parâmetro na invocação de procedimento (em ordem de chamada) e, em seguida, os nomes de cada coluna no conjunto de resultados retornado pelo procedimento (em ordem de coluna).  
  
 Os aplicativos devem associar colunas específicas do driver em relação ao final do conjunto de resultados. Para obter mais informações, consulte [dados retornados pelas funções de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
 Para determinar os comprimentos reais das colunas PROCEDURE_CAT, PROCEDURE_SCHEM, PROCEDURE_NAME e nome da coluna, um aplicativo pode chamar **SQLGetInfo** com o SQL_MAX_ SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, PROCEDURE_NAME_LEN e SQL_MAX_COLUMN_NAME_LEN opções.  
  
 As seguintes colunas foram renomeadas para ODBC 3. *x*. As alterações de nome de coluna não afetam a compatibilidade com versões anteriores, porque aplicativos associar pelo número de coluna.  
  
|Coluna de ODBC 2.0|ODBC 3. *x* coluna|  
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
  
 A tabela a seguir lista as colunas no conjunto de resultados. Colunas adicionais além da coluna 19 (IS_NULLABLE) podem ser definidas pelo driver. Um aplicativo deve acessar colunas específicas do driver por contagem regressiva do final do conjunto de resultados em vez de especificar uma posição ordinal explícita. Para obter mais informações, consulte [dados retornados pelas funções de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome da coluna|Número da coluna|Tipo de dados|Comentários|  
|-----------------|-------------------|---------------|--------------|  
|PROCEDURE_CAT (ODBC 2.0)|1|Varchar|Nome do catálogo de procedimento; NULL se não for aplicável à fonte de dados. Se um driver dá suporte a catálogos para alguns procedimentos, mas não para outras pessoas, como quando o driver recupera os dados de diferentes DBMSs, ele retorna uma cadeia de caracteres vazia ("") para esses procedimentos que não têm catálogos.|  
|PROCEDURE_SCHEM (ODBC 2.0)|2|Varchar|Nome do esquema de procedimento; NULL se não for aplicável à fonte de dados. Se um driver dá suporte a esquemas para alguns procedimentos, mas não para outras pessoas, como quando o driver recupera os dados de diferentes DBMSs, ele retorna uma cadeia de caracteres vazia ("") para esses procedimentos que não têm esquemas.|  
|PROCEDURE_NAME (ODBC 2.0)|3|Varchar não nulo|Nome do procedimento. Uma cadeia de caracteres vazia é retornada para um procedimento que não tem um nome.|  
|NOME DA COLUNA (ODBC 2.0)|4|Varchar não nulo|Nome da coluna de procedimento. O driver retorna uma cadeia de caracteres vazia para uma coluna de procedimento que não tem um nome.|  
|COLUMN_TYPE (ODBC 2.0)|5|Smallint não NULL|Define a coluna de procedimento como um parâmetro ou uma coluna do conjunto de resultados:<br /><br /> SQL_PARAM_TYPE_UNKNOWN: A coluna de procedimento é um parâmetro cujo tipo é desconhecido. ODBC (1.0)<br /><br /> SQL_PARAM_INPUT: A coluna de procedimento é um parâmetro de entrada. ODBC (1.0)<br /><br /> SQL_PARAM_INPUT_OUTPUT: A coluna de procedimento é um parâmetro de entrada/saída. ODBC (1.0)<br /><br /> SQL_PARAM_OUTPUT: A coluna de procedimento é um parâmetro de saída. (ODBC 2.0)<br /><br /> SQL_RETURN_VALUE: A coluna de procedimento é o valor de retorno do procedimento. (ODBC 2.0)<br /><br /> SQL_RESULT_COL: A coluna de procedimento é uma coluna do conjunto de resultados. ODBC (1.0)|  
|DATA_TYPE (ODBC 2.0)|6|Smallint não NULL|Tipo de dados SQL. Isso pode ser um tipo de dados SQL ODBC ou um tipo de dados SQL específico do driver. Para tipos de dados de data e hora e intervalo, esta coluna retorna os tipos de dados conciso (por exemplo, SQL_TYPE_TIME ou SQL_INTERVAL_YEAR_TO_MONTH). Para obter uma lista de tipos de dados ODBC SQL válidos, consulte [tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md) no Apêndice d: os tipos de dados. Para obter informações sobre tipos de dados SQL específico do driver, consulte a documentação do driver.|  
|TYPE_NAME (ODBC 2.0)|7|Varchar não nulo|Nome do tipo de dados de origem dependente de dados; Por exemplo, "CHAR", "VARCHAR", "MONEY", "VARBINARY longo" ou "CHAR () para dados BIT".|  
|COLUMN_SIZE (ODBC 2.0)|8|Integer|O tamanho da coluna da coluna de procedimento na fonte de dados. NULL é retornado para os tipos de dados em que o tamanho da coluna não é aplicável. Para obter mais informações sobre precisão, consulte [tamanho da coluna, dígitos decimais, transferir o comprimento do octeto e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice d: os tipos de dados.|  
|BUFFER_LENGTH (ODBC 2.0)|9|Integer|O comprimento em bytes de dados transferidos em um **SQLGetData** ou **SQLFetch** operação se SQL_C_DEFAULT for especificado. Para dados numéricos, esse tamanho pode ser diferente do que o tamanho dos dados armazenados na fonte de dados. Para obter mais informações, consulte [tamanho da coluna, dígitos decimais, transferir o comprimento do octeto e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md), no Apêndice d: os tipos de dados.|  
|DECIMAL_DIGITS (ODBC 2.0)|10|Smallint|Os dígitos decimais da coluna de procedimento na fonte de dados. NULL é retornado para os tipos de dados em que os dígitos decimais não é aplicáveis. Para obter mais informações sobre os dígitos decimais, consulte [tamanho da coluna, dígitos decimais, transferir o comprimento do octeto e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md), no Apêndice d: os tipos de dados.|  
|NUM_PREC_RADIX (ODBC 2.0)|11|Smallint|Para tipos de dados numéricos, 10 ou 2.<br /><br /> Se for 10, os valores de COLUMN_SIZE e DECIMAL_DIGITS forneça o número de dígitos permitido para a coluna. Por exemplo, uma coluna DECIMAL(12,5) retornaria um NUM_PREC_RADIX de 10, um COLUMN_SIZE de 12 e um DECIMAL_DIGITS de 5; uma coluna de ponto flutuante pode retornar um NUM_PREC_RADIX de 10, um COLUMN_SIZE 15 e DECIMAL_DIGITS de NULL.<br /><br /> Se for 2, os valores de COLUMN_SIZE e DECIMAL_DIGITS fornecer o número de bits permitidos na coluna. Por exemplo, uma coluna de ponto flutuante pode retornar um NUM_PREC_RADIX de 2, um COLUMN_SIZE de 53 e DECIMAL_DIGITS de NULL.<br /><br /> NULL é retornado para os tipos de dados onde NUM_PREC_RADIX não é aplicável.|  
|PERMITE VALOR NULO (ODBC 2.0)|12|Smallint não NULL|Se a coluna de procedimento aceita um valor NULL:<br /><br /> SQL_NO_NULLS: A coluna de procedimento não aceita valores NULL.<br /><br /> SQL_NULLABLE: A coluna de procedimento aceita valores nulos.<br /><br /> SQL_NULLABLE_UNKNOWN: Não se sabe se a coluna de procedimento aceita valores nulos.|  
|COMENTÁRIOS (ODBC 2.0)|13|Varchar|Uma descrição da coluna de procedimento.|  
|COLUMN_DEF (ODBC 3.0)|14|Varchar|O valor padrão da coluna.<br /><br /> Se NULL for especificado como o valor padrão, essa coluna é a palavra NULL, que não está entre aspas. Se o valor padrão não pode ser representado sem truncamento, esta coluna contém truncados, nenhum delimitador aspas simples. Se nenhum valor padrão foi especificado, essa coluna será NULL.<br /><br /> O valor de COLUMN_DEF pode ser usado para gerar uma nova definição de coluna, exceto quando ela contém o valor truncados.|  
|SQL_DATA_TYPE (ODBC 3.0)|15|Smallint não NULL|O valor do tipo de dados SQL como ele aparece no campo SQL_DESC_TYPE do descritor. Essa coluna é igual à coluna DATA_TYPE, exceto para tipos de dados de data e hora e intervalo.<br /><br /> Para tipos de dados de data e hora e intervalo, o campo SQL_DATA_TYPE no conjunto de resultados retornará SQL_INTERVAL ou SQL_DATETIME e o campo SQL_DATETIME_SUB retornará o subcódigo para o tipo de dados datetime ou de intervalo específico. (Consulte [tipos de dados do apêndice d:](../../../odbc/reference/appendixes/appendix-d-data-types.md).)|  
|SQL_DATETIME_SUB (ODBC 3.0)|16|Smallint|O código de subtipo para tipos de dados de data e hora e intervalo. Para outros tipos de dados, esta coluna retorna um valor nulo.|  
|CHAR_OCTET_LENGTH (ODBC 3.0)|17|Integer|O comprimento máximo em bytes de um caractere ou dados binários a coluna de tipo. Para todos os outros tipos de dados, esta coluna retorna um valor nulo.|  
|ORDINAL_POSITION (ODBC 3.0)|18|Integer não NULL|Para parâmetros de entrada e saídos, a posição ordinal do parâmetro na definição do procedimento (em ordem crescente de parâmetros, começando em 1). Um valor de retorno (se houver), será retornado 0. Para colunas do conjunto de resultados, defina a posição ordinal da coluna no resultado, com a primeira coluna no conjunto que está sendo de resultados número 1. Se houver vários conjuntos de resultados, posições ordinais de coluna são retornadas de uma maneira específica do driver.|  
|IS_NULLABLE (ODBC 3.0)|19|Varchar|"Não" se a coluna não incluir valores nulos.<br /><br /> "Sim" se a coluna pode incluir valores nulos.<br /><br /> Esta coluna retorna uma cadeia de caracteres de comprimento zero se a possibilidade de nulidade for desconhecida.<br /><br /> As regras ISO são seguidas para determinar a possibilidade de nulidade. Um DBMS em conformidade com ISO SQL não pode retornar uma cadeia de caracteres vazia.<br /><br /> O valor retornado para esta coluna é diferente do valor retornado para a coluna NULLABLE. (Consulte a descrição da coluna permite valor nula).|  
  
## <a name="code-example"></a>Exemplo de código  
 Consulte [chamadas de procedimento](../../../odbc/reference/develop-app/procedure-calls.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Um buffer de associação a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Buscando uma única linha ou um bloco de dados em uma direção de somente avanço|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Buscar um bloco de dados ou rolar por um resultado definido|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Retornando uma lista de procedimentos em uma fonte de dados|[Função SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
