---
title: Função SQLStatistics | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLStatistics
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLStatistics
helpviewer_keywords:
- SQLStatistics function [ODBC]
ms.assetid: 45210682-cfea-4e5d-9951-bcf1cbe10f41
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c2a5ef0b0e54e17a2dc091a98efc972fa608ef15
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302940"
---
# <a name="sqlstatistics-function"></a>Função SQLStatistics
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: ISO 92  
  
 **Resumo**  
 **SQLStatistics** recupera uma lista de estatísticas sobre uma única tabela e os índices associados à tabela. O driver retorna as informações como um conjunto de resultados.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLStatistics(  
     SQLHSTMT        StatementHandle,  
     SQLCHAR *       CatalogName,  
     SQLSMALLINT     NameLength1,  
     SQLCHAR *       SchemaName,  
     SQLSMALLINT     NameLength2,  
     SQLCHAR *       TableName,  
     SQLSMALLINT     NameLength3,  
     SQLUSMALLINT    Unique,  
     SQLUSMALLINT    Reserved);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 Entrada Identificador de instrução.  
  
 *CatalogName*  
 Entrada Nome do catálogo. Se um driver oferecer suporte a catálogos para algumas tabelas, mas não para outras, como quando o driver recupera dados de DBMSs diferentes, uma cadeia de caracteres vazia ("") indicará as tabelas que não têm catálogos. *CatalogName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *CatalogName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *CatalogName* será um argumento comum; Ele é tratado literalmente e seu caso é significativo. Para obter mais informações, consulte [argumentos em funções de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 Entrada Comprimento em caracteres de **nome_do_catálogo*.  
  
 *SchemaName*  
 Entrada Nome do esquema. Se um driver oferecer suporte a esquemas para algumas tabelas, mas não para outras, como quando o driver recupera dados de DBMSs diferentes, uma cadeia de caracteres vazia ("") indicará as tabelas que não têm esquemas. *SchemaName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *SchemaName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *SchemaName* será um argumento comum; Ele é tratado literalmente e seu caso é significativo.  
  
 *NameLength2*  
 Entrada Comprimento em caracteres de **SchemaName*.  
  
 *TableName*  
 Entrada Nome da tabela. Este argumento não pode ser um ponteiro nulo. *SchemaName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *TableName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *TableName* é um argumento comum; Ele é tratado literalmente e seu caso é significativo.  
  
 *NameLength3*  
 Entrada Comprimento em caracteres de **TableName*.  
  
 *Diferente*  
 Entrada Tipo de índice: SQL_INDEX_UNIQUE ou SQL_INDEX_ALL.  
  
 *Reservado*  
 Entrada Indica a importância das colunas CARDINALIDADE e páginas no conjunto de resultados. As opções a seguir afetam apenas o retorno das colunas CARDINALIDADE e páginas; as informações de índice são retornadas mesmo se a CARDINALIDADE e as páginas não forem retornadas.  
  
 SQL_ENSURE solicita que o driver recupere incondicionalmente as estatísticas. (Os drivers que estão em conformidade apenas com o padrão de grupo aberto e não oferecem suporte a extensões ODBC não poderão dar suporte a SQL_ENSURE.)  
  
 SQL_QUICK solicita que o driver recupere a CARDINALIDADE e as páginas somente se elas estiverem prontamente disponíveis no servidor. Nesse caso, o driver não assegura que os valores são atuais. (Os aplicativos que são gravados no padrão de grupo aberto sempre terão SQL_QUICK comportamento dos drivers em conformidade com ODBC *3. x*.)  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLStatistics** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *identificador* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLStatistics** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado falhou antes da função concluir o processamento.|  
|24.000|Estado de cursor inválido|Um cursor estava aberto no *StatementHandle*e **SQLFetch** ou **SQLFetchScroll** foi chamado. Esse erro será retornado pelo Gerenciador de driver se **SQLFetch** ou **SQLFetchScroll** não tiver retornado SQL_NO_DATA e for retornado pelo driver se **SQLFetch** ou **SQLFetchScroll** tiver retornado SQL_NO_DATA.<br /><br /> Um cursor estava aberto no *StatementHandle*, mas **SQLFetch** ou **SQLFetchScroll** não tinha sido chamado.|  
|40001|Falha de serialização|A transação foi revertida devido a um deadlock de recurso com outra transação.|  
|40003|Conclusão de instrução desconhecida|A conexão associada falhou durante a execução dessa função, e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \*MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado em *StatementHandle*e, em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativo multithread.|  
|HY009|Uso inválido de ponteiro nulo|O argumento *TableName* era um ponteiro nulo.<br /><br /> O atributo da instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, o argumento *CatalogName* era um ponteiro nulo e o SQL_CATALOG_NAME *InfoType* retorna que os nomes de catálogo têm suporte.<br /><br /> (DM) o atributo de instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, e o argumento *SchemaName* era um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *StatementHandle*. Esta função assíncrona ainda estava em execução quando a função **SQLStatistics** foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para *StatementHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado para o *StatementHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|(DM) o valor de um dos argumentos de comprimento do nome era menor que 0, mas não é igual a SQL_NTS.<br /><br /> O valor de um dos argumentos de comprimento do nome excedeu o valor de comprimento máximo para o nome correspondente.|  
|HY100|Tipo de opção de exclusividade fora do intervalo|(DM) foi especificado um valor *exclusivo* inválido.|  
|HY101|Tipo de opção de exatidão fora do intervalo|(DM) foi especificado um valor *reservado* inválido.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|Um catálogo foi especificado e o driver ou a fonte de dados não oferece suporte a catálogos.<br /><br /> Um esquema foi especificado e o driver ou a fonte de dados não oferece suporte a esquemas.<br /><br /> A combinação das configurações atuais dos atributos de instrução SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE não era suportada pelo driver ou pela fonte de dados.<br /><br /> O atributo de instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE e o atributo de instrução SQL_ATTR_CURSOR_TYPE foi definido como um tipo de cursor para o qual o driver não dá suporte a indicadores.|  
|HYT00|Tempo limite esgotado|O período de tempo limite da consulta expirou antes que a fonte de dados retornasse o conjunto de resultados solicitado. O período de tempo limite é definido por meio de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *StatementHandle* não oferece suporte à função.|  
|IM017|A sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação for usado, a sondagem será desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesse identificador.|Se a chamada de função anterior no identificador retornar SQL_STILL_EXECUTING e se o modo de notificação estiver habilitado, **SQLCompleteAsync** deverá ser chamado na alça para executar o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 **SQLStatistics** retorna informações sobre uma única tabela como um conjunto de resultados padrão, ordenadas por NON_UNIQUE, TYPE, INDEX_QUALIFIER, INDEX_NAME e ORDINAL_POSITION. O conjunto de resultados combina informações de estatísticas (nas colunas CARDINALIDADE e páginas do conjunto de resultados) para a tabela com informações sobre cada índice. Para obter informações sobre como essas informações podem ser usadas, consulte [usos de dados do catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 Para determinar os comprimentos reais das colunas TABLE_CAT, TABLE_SCHEM, TABLE_NAME e COLUMN_NAME, um aplicativo pode chamar **SQLGetInfo** com as opções SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN e SQL_MAX_COLUMN_NAME_LEN.  
  
> [!NOTE]  
>  Para obter mais informações sobre o uso geral, argumentos e dados retornados de funções de catálogo ODBC, consulte [Catalog Functions](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 As colunas a seguir foram renomeadas para ODBC *3. x*. As alterações de nome de coluna não afetam a compatibilidade com versões anteriores porque os aplicativos são associados por número de coluna.  
  
|Coluna ODBC 2,0|Coluna ODBC *3. x*|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|SEQ_IN_INDEX|ORDINAL_POSITION|  
|COLLATION|ASC_OR_DESC|  
  
 A tabela a seguir lista as colunas no conjunto de resultados. Colunas adicionais além da coluna 13 (FILTER_CONDITION) podem ser definidas pelo driver. Um aplicativo deve obter acesso a colunas específicas de driver, contando a partir do final do conjunto de resultados, em vez de especificar uma posição ordinal explícita. Para obter mais informações, consulte [dados retornados por funções de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome da coluna|Número da coluna|Tipo de dados|Comentários|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1,0)|1|Varchar|Nome do catálogo da tabela à qual a estatística ou índice se aplica; NULL se não for aplicável à fonte de dados. Se um driver oferecer suporte a catálogos para algumas tabelas, mas não para outras, como quando o driver recupera dados de DBMSs diferentes, ele retorna uma cadeia de caracteres vazia ("") para as tabelas que não têm catálogos.|  
|TABLE_SCHEM (ODBC 1,0)|2|Varchar|Nome do esquema da tabela à qual a estatística ou índice se aplica; NULL se não for aplicável à fonte de dados. Se um driver oferecer suporte a esquemas para algumas tabelas, mas não para outras, como quando o driver recupera dados de DBMSs diferentes, ele retorna uma cadeia de caracteres vazia ("") para as tabelas que não têm esquemas.|  
|TABLE_NAME (ODBC 1,0)|3|Varchar não nulo|Nome da tabela à qual a estatística ou índice se aplica.|  
|NON_UNIQUE (ODBC 1,0)|4|Smallint|Indica se o índice não permite valores duplicados:<br /><br /> SQL_TRUE se os valores de índice podem ser não exclusivos.<br /><br /> SQL_FALSE se os valores de índice devem ser exclusivos.<br /><br /> NULL será retornado se o tipo for SQL_TABLE_STAT.|  
|INDEX_QUALIFIER (ODBC 1,0)|5|Varchar|O identificador usado para qualificar o nome do índice fazendo uma **drop index**; NULL será retornado se um qualificador de índice não for suportado pela fonte de dados ou se o tipo for SQL_TABLE_STAT. Se um valor não nulo for retornado nessa coluna, ele deverá ser usado para qualificar o nome do índice em uma instrução de **drop index** ; caso contrário, o TABLE_SCHEM deve ser usado para qualificar o nome do índice.|  
|INDEX_NAME (ODBC 1,0)|6|Varchar|Nome do índice; NULL será retornado se o tipo for SQL_TABLE_STAT.|  
|TIPO (ODBC 1,0)|7|Smallint não NULL|Tipo de informação que está sendo retornada:<br /><br /> SQL_TABLE_STAT indica uma estatística para a tabela (na coluna CARDINALIDADE ou páginas).<br /><br /> SQL_INDEX_BTREE indica um índice de árvore B.<br /><br /> SQL_INDEX_CLUSTERED indica um índice clusterizado.<br /><br /> SQL_INDEX_CONTENT indica um índice de conteúdo.<br /><br /> SQL_INDEX_HASHED indica um índice com hash.<br /><br /> SQL_INDEX_OTHER indica outro tipo de índice.|  
|ORDINAL_POSITION (ODBC 1,0)|8|Smallint|Número de sequência da coluna no índice (começando com 1); NULL será retornado se o tipo for SQL_TABLE_STAT.|  
|COLUMN_NAME (ODBC 1,0)|9|Varchar|Nome da coluna. Se a coluna for baseada em uma expressão, como salário + benefícios, a expressão será retornada; se a expressão não puder ser determinada, uma cadeia de caracteres vazia será retornada. NULL será retornado se o tipo for SQL_TABLE_STAT.|  
|ASC_OR_DESC (ODBC 1,0)|10|Char(1)|Sequência de classificação da coluna: "A" para crescente; "D" para decrescente; NULL será retornado se a sequência de classificação de coluna não for suportada pela fonte de dados ou se o tipo for SQL_TABLE_STAT.|  
|CARDINALIDADE (ODBC 1,0)|11|Integer|Cardinalidade da tabela ou índice; número de linhas na tabela se o tipo for SQL_TABLE_STAT; número de valores exclusivos no índice se o tipo não for SQL_TABLE_STAT; NULL será retornado se o valor não estiver disponível na fonte de dados.|  
|PÁGINAS (ODBC 1,0)|12|Integer|Número de páginas usadas para armazenar o índice ou a tabela; número de páginas para a tabela se o tipo for SQL_TABLE_STAT; número de páginas para o índice se o tipo não for SQL_TABLE_STAT; NULL será retornado se o valor não estiver disponível na fonte de dados ou se não for aplicável à fonte de dados.|  
|FILTER_CONDITION (ODBC 2,0)|13|Varchar|Se o índice for um índice filtrado, essa será a condição de filtro, como salário > 30000; se a condição de filtro não puder ser determinada, esta é uma cadeia de caracteres vazia.<br /><br /> NULL se o índice não for um índice filtrado, não será possível determinar se o índice é um índice filtrado ou se o tipo está SQL_TABLE_STAT.|  
  
 Se a linha no conjunto de resultados corresponder a uma tabela, o tipo de driver definirá como SQL_TABLE_STAT e definirá NON_UNIQUE, INDEX_QUALIFIER, INDEX_NAME, ORDINAL_POSITION, COLUMN_NAME e ASC_OR_DESC como NULL. Se a CARDINALIDADE ou as páginas não estiverem disponíveis na fonte de dados, o driver as definirá como NULL.  
  
## <a name="code-example"></a>Exemplo de código  
 Para obter um exemplo de código de uma função semelhante, consulte [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Associando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Buscando uma única linha ou um bloco de dados em uma direção somente de avanço.|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Buscando um bloco de dados ou rolando por meio de um conjunto de resultados|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Retornando as colunas de chaves estrangeiras|[Função SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|  
|Retornando as colunas de uma chave primária|[Função SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
