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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302940"
---
# <a name="sqlstatistics-function"></a>Função SQLStatistics
**Conformidade**  
 Versão introduzida: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **O SQLStatistics** recupera uma lista de estatísticas sobre uma única tabela e os índices associados à tabela. O motorista retorna as informações como um conjunto de resultados.  
  
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
 [Entrada] Alça de declaração.  
  
 *Catalogname*  
 [Entrada] Nome do catálogo. Se um driver suporta catálogos para algumas tabelas, mas não para outras, como quando o driver recupera dados de diferentes DBMSs, uma string vazia ("") indica as tabelas que não possuem catálogos. *CatalogName* não pode conter um padrão de pesquisa de seqüência.  
  
 Se o atributo de declaração SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *o CatalogName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *CatalogName* é um argumento comum; é tratado literalmente, e seu caso é significativo. Para obter mais informações, consulte [Argumentos em Funções de Catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Entrada] Comprimento em caracteres de **CatalogName*.  
  
 *Schemaname*  
 [Entrada] Nome de Esquema. Se um driver suporta esquemas para algumas tabelas, mas não para outras, como quando o driver recupera dados de diferentes DBMSs, uma string vazia ("") indica aquelas tabelas que não possuem esquemas. *SchemaName* não pode conter um padrão de pesquisa de seqüência.  
  
 Se o atributo de declaração SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *O SchemaName* é tratado como um identificador e seu caso não é significativo. Se for SQL_FALSE, *SchemaName* é um argumento comum; é tratado literalmente, e seu caso é significativo.  
  
 *Comprimento de nome2*  
 [Entrada] Comprimento em caracteres de **SchemaName*.  
  
 *Tablename*  
 [Entrada] Nome da mesa. Este argumento não pode ser um ponteiro nulo. *SchemaName* não pode conter um padrão de pesquisa de seqüência.  
  
 Se o atributo de declaração SQL_ATTR_METADATA_ID estiver definido como SQL_TRUE, *O Nome da Tabela* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *TableName* é um argumento comum; é tratado literalmente, e seu caso é significativo.  
  
 *Comprimento de nome3*  
 [Entrada] Comprimento em caracteres de **TableName*.  
  
 *Único*  
 [Entrada] Tipo de índice: SQL_INDEX_UNIQUE ou SQL_INDEX_ALL.  
  
 *Reservado*  
 [Entrada] Indica a importância das colunas CARDINALITY e PAGES no conjunto de resultados. As seguintes opções afetam apenas o retorno das colunas CARDINALITY e PAGES; as informações do índice são devolvidas mesmo que o CARDINALITY e as PÁGINAS não sejam devolvidos.  
  
 SQL_ENSURE solicita que o motorista recupere incondicionalmente as estatísticas. (Drivers que estejam em conformidade apenas com o padrão Open Group e que não suportam extensões ODBC não poderão suportar SQL_ENSURE.)  
  
 SQL_QUICK solicita que o motorista recupere o CARDINALITY e as PÁGINAS somente se estiverem prontamente disponíveis no servidor. Nesse caso, o driver não assegura que os valores são atuais. (Os aplicativos gravados no padrão Open Group sempre receberão SQL_QUICK comportamento dos drivers compatíveis com o ODBC *3.x.)*  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLStatistics** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *alça* de *statementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados pelo **SQLStatistics** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados à qual o driver estava conectado falhou antes da função ser concluída.|  
|24.000|Estado de cursor inválido|Um cursor foi aberto no *StatementHandle*, e **SQLFetch** ou **SQLFetchScroll** foram chamados. Esse erro é devolvido pelo Gerenciador de driver se **o SQLFetch** ou **o SQLFetchScroll** não retornarem SQL_NO_DATA e forem devolvidos pelo driver se **o SQLFetch** ou **o SQLFetchScroll** retornarem SQL_NO_DATA.<br /><br /> Um cursor foi aberto no *StatementHandle,* mas **SQLFetch** ou **SQLFetchScroll** não foram chamados.|  
|40001|Falha na serialização|A transação foi revertida por causa de um impasse de recursos com outra transação.|  
|40003|Conclusão de declaração desconhecida|A conexão associada falhou durante a execução desta função, e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar memória necessária para suportar a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*e, em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **sqlCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um segmento diferente em um aplicativo multithread.|  
|HY009|Uso inválido do ponteiro nulo|O argumento *TableName* era um ponteiro nulo.<br /><br /> O SQL_ATTR_METADATA_ID atributo de declaração foi definido como SQL_TRUE, o argumento *CatalogName* era um ponteiro nulo e o SQL_CATALOG_NAME *InfoType* retorna que os nomes do catálogo são suportados.<br /><br /> (DM) O atributo de declaração SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, e o argumento *SchemaName* foi um ponteiro nulo.|  
|HY010|Erro de seqüência de função|(DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *StatementHandle*. Esta função assíncrona ainda estava sendo executada quando a função **SQLStatistics** foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foram chamados para o *StatementHandle* e retornaram SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) Uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados para o *StatementHandle* e retornaram SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY090|Comprimento de seqüência ou buffer inválido|(DM) O valor de um dos argumentos de comprimento do nome foi inferior a 0, mas não igual a SQL_NTS.<br /><br /> O valor de um dos argumentos de comprimento do nome excedeu o valor máximo de comprimento para o nome correspondente.|  
|HY100|Tipo de opção de exclusividade fora do alcance|(DM) Um valor *único* inválido foi especificado.|  
|HY101|Tipo de opção de precisão fora do alcance|(DM) Um valor *reservado* inválido foi especificado.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|Um catálogo foi especificado e o driver ou fonte de dados não suporta catálogos.<br /><br /> Um esquema foi especificado, e o driver ou fonte de dados não suporta esquemas.<br /><br /> A combinação das configurações atuais dos atributos de declaração SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE não foi suportada pelo driver ou fonte de dados.<br /><br /> O atributo de declaração SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE, e o atributo de declaração SQL_ATTR_CURSOR_TYPE foi definido como um tipo de cursor para o qual o motorista não suporta marcadores.|  
|HYT00|Tempo limite esgotado|O período de tempo de consulta expirou antes que a fonte de dados retornasse o conjunto de resultados solicitado. O período de tempo é definido através **de SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *StatementHandle* não suporta a função.|  
|IM017|A votação é desativada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a votação é desativada.|  
|IM018|**O SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesta alça.|Se a chamada de função anterior na alça retornar SQL_STILL_EXECUTING e se o modo de notificação estiver ativado, o **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 **O SQLStatistics** retorna informações sobre uma única tabela como um conjunto de resultados padrão, ordenado por NON_UNIQUE, TYPE, INDEX_QUALIFIER, INDEX_NAME e ORDINAL_POSITION. O conjunto de resultados combina informações estatísticas (nas colunas CARDINALITY e PAGES do conjunto de resultados) para a tabela com informações sobre cada índice. Para obter informações sobre como essas informações podem ser usadas, consulte [Usos de Dados de Catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 Para determinar os comprimentos reais das colunas de TABLE_CAT, TABLE_SCHEM, TABLE_NAME e COLUMN_NAME, um aplicativo pode chamar **o SQLGetInfo** com as opções de SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN e SQL_MAX_COLUMN_NAME_LEN.  
  
> [!NOTE]  
>  Para obter mais informações sobre o uso geral, argumentos e dados retornados das funções do catálogo oDBC, consulte [Funções de Catálogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 As seguintes colunas foram renomeadas para ODBC *3.x*. As alterações de nome da coluna não afetam a compatibilidade retrógrada porque os aplicativos se ligam por número de coluna.  
  
|Coluna ODBC 2.0|Coluna ODBC *3.x*|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|SEQ_IN_INDEX|ORDINAL_POSITION|  
|COLLATION|ASC_OR_DESC|  
  
 A tabela a seguir lista as colunas no conjunto de resultados. Colunas adicionais além da coluna 13 (FILTER_CONDITION) podem ser definidas pelo driver. Um aplicativo deve ter acesso a colunas específicas do driver, contando abaixo do final do conjunto de resultados, em vez de especificar uma posição ordinal explícita. Para obter mais informações, consulte [Dados Retornados por Funções de Catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome da coluna|Número da coluna|Tipo de dados|Comentários|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|Nome do catálogo da tabela à qual se aplica a estatística ou índice; NULL se não aplicável à fonte de dados. Se um driver suporta catálogos para algumas tabelas, mas não para outras, como quando o driver recupera dados de diferentes DBMSs, ele retorna uma string vazia (""" para aquelas tabelas que não possuem catálogos.|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|Nome do esquema da tabela à qual se aplica a estatística ou índice; NULL se não aplicável à fonte de dados. Se um driver suporta esquemas para algumas tabelas, mas não para outras, como quando o driver recupera dados de diferentes DBMSs, ele retorna uma string vazia (""" para aquelas tabelas que não possuem esquemas.|  
|TABLE_NAME (ODBC 1.0)|3|Varchar não É NULO|Nome da tabela à qual se aplica a estatística ou índice.|  
|NON_UNIQUE (ODBC 1.0)|4|Smallint|Indica se o índice não permite valores duplicados:<br /><br /> SQL_TRUE se os valores do índice podem ser não únicos.<br /><br /> SQL_FALSE se os valores do índice devem ser únicos.<br /><br /> NULL é devolvido se o TYPE for SQL_TABLE_STAT.|  
|INDEX_QUALIFIER (ODBC 1.0)|5|Varchar|O identificador usado para qualificar o nome do índice fazendo um **ÍNDICE DE QUEDA**; Null é devolvido se um qualificador de índice não for suportado pela fonte de dados ou se o TYPE for SQL_TABLE_STAT. Se um valor não nulo for devolvido nesta coluna, ele deve ser usado para qualificar o nome do índice em uma declaração **DE ÍNDICE DE QUEDA;** caso contrário, o TABLE_SCHEM deve ser usado para qualificar o nome do índice.|  
|INDEX_NAME (ODBC 1.0)|6|Varchar|Nome do índice; NULL é devolvido se o TYPE for SQL_TABLE_STAT.|  
|TIPO (ODBC 1.0)|7|Smallint não NULL|Tipo de informação sendo devolvida:<br /><br /> SQL_TABLE_STAT indica uma estatística para a tabela (na coluna CARDINALITY ou PAGES).<br /><br /> SQL_INDEX_BTREE indica um índice b-tree.<br /><br /> SQL_INDEX_CLUSTERED indica um índice agrupado.<br /><br /> SQL_INDEX_CONTENT indica um índice de conteúdo.<br /><br /> SQL_INDEX_HASHED indica um índice hashed.<br /><br /> SQL_INDEX_OTHER indica outro tipo de índice.|  
|ORDINAL_POSITION (ODBC 1.0)|8|Smallint|Número da seqüência da coluna no índice (começando com 1); NULL é devolvido se o TYPE for SQL_TABLE_STAT.|  
|COLUMN_NAME (ODBC 1.0)|9|Varchar|Nome da coluna. Se a coluna for baseada em uma expressão, como SALÁRIO + BENEFÍCIOS, a expressão é devolvida; se a expressão não puder ser determinada, uma seqüência vazia é devolvida. NULL é devolvido se o TYPE for SQL_TABLE_STAT.|  
|ASC_OR_DESC (ODBC 1.0)|10|Char(1)|Classificar seqüência para a coluna: "A" para ascendente; "D" para descer; NULL é devolvido se a seqüência de classificação da coluna não for suportada pela fonte de dados ou se o TYPE estiver SQL_TABLE_STAT.|  
|CARDINALIDADE (ODBC 1.0)|11|Integer|Cardinalidade de tabela ou índice; número de linhas na tabela se o TYPE for SQL_TABLE_STAT; número de valores únicos no índice se o TYPE não for SQL_TABLE_STAT; NULL é devolvido se o valor não estiver disponível na fonte de dados.|  
|PÁGINAS (ODBC 1.0)|12|Integer|Número de páginas usadas para armazenar o índice ou tabela; número de páginas para a tabela se o TYPE estiver SQL_TABLE_STAT; número de páginas para o índice se o TYPE não for SQL_TABLE_STAT; Null é devolvido se o valor não estiver disponível na fonte de dados ou se não for aplicável à fonte de dados.|  
|FILTER_CONDITION (ODBC 2.0)|13|Varchar|Se o índice for um índice filtrado, esta é a condição do filtro, como o SALÁRIO > 30000; se a condição do filtro não puder ser determinada, esta é uma seqüência vazia.<br /><br /> NULO se o índice não for um índice filtrado, não é possível determinar se o índice é um índice filtrado ou o TYPE está SQL_TABLE_STAT.|  
  
 Se a linha no conjunto de resultados corresponder a uma tabela, o driver define TYPE para SQL_TABLE_STAT e define NON_UNIQUE, INDEX_QUALIFIER, INDEX_NAME, ORDINAL_POSITION, COLUMN_NAME e ASC_OR_DESC a NULL. Se CARDINALITY ou PAGES não estiverem disponíveis na fonte de dados, o driver os define como NULA.  
  
## <a name="code-example"></a>Exemplo de código  
 Para obter um exemplo de código de uma função semelhante, consulte [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Vinculando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelamento do processamento de declarações|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Buscar uma única linha ou um bloco de dados em uma direção somente para a frente.|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Buscar um bloco de dados ou rolar através de um conjunto de resultados|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Retornando as colunas de chaves estrangeiras|[Função SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|  
|Retornando as colunas de uma chave primária|[Função SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
