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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6cd0503b9f0169a19179bcee545132279903ea10
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53207545"
---
# <a name="sqlstatistics-function"></a>Função SQLStatistics
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 1.0 ODBC: ISO 92  
  
 **Resumo**  
 **SQLStatistics** recupera uma lista de estatísticas sobre uma única tabela e os índices associados à tabela. O driver retorna as informações como um conjunto de resultados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
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
 [Entrada] Identificador de instrução.  
  
 *CatalogName*  
 [Entrada] Nome do catálogo. Se um driver compatível com catálogos para algumas tabelas, mas não para outros, como quando o driver recupera os dados de diferentes DBMSs, uma cadeia de caracteres vazia ("") indica as tabelas que não têm catálogos. *CatalogName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *CatalogName* é tratado como um identificador e o seu caso de não é significativo. Se for SQL_FALSE, *CatalogName* é um argumento comum; ela será tratada, literalmente, e seu caso é significativo. Para obter mais informações, consulte [argumentos em funções de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Entrada] Comprimento em caracteres de **CatalogName*.  
  
 *SchemaName*  
 [Entrada] Nome do esquema. Se um driver compatível com esquemas para algumas tabelas, mas não para outros, como quando o driver recupera os dados de diferentes DBMSs, uma cadeia de caracteres vazia ("") indica as tabelas que não tem esquemas. *SchemaName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *SchemaName* é tratado como um identificador e o seu caso de não é significativo. Se for SQL_FALSE, *SchemaName* é um argumento comum; ela será tratada, literalmente, e seu caso é significativo.  
  
 *NameLength2*  
 [Entrada] Comprimento em caracteres de **SchemaName*.  
  
 *TableName*  
 [Entrada] Nome da tabela. Esse argumento não pode ser um ponteiro nulo. *SchemaName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *TableName* é tratado como um identificador e o seu caso de não é significativo. Se for SQL_FALSE, *TableName* é um argumento comum; ela será tratada, literalmente, e seu caso é significativo.  
  
 *NameLength3*  
 [Entrada] Comprimento em caracteres de **TableName*.  
  
 *Exclusivo*  
 [Entrada] Tipo de índice: SQL_INDEX_UNIQUE ou SQL_INDEX_ALL.  
  
 *Reserved*  
 [Entrada] Indica a importância das colunas CARDINALIDADE e as páginas no conjunto de resultados. As opções a seguir afetam o retorno de CARDINALIDADE e as páginas colunas somente; informações de índice são retornadas, mesmo se a CARDINALIDADE e as páginas não são retornadas.  
  
 SQL_ENSURE solicita que o driver recupere as estatísticas incondicionalmente. (Drivers de acordo apenas com o padrão Open Group e não dão suporte a extensões ODBC não será capazes de dar suporte a SQL_ENSURE.)  
  
 SQL_QUICK solicita que o driver recuperar a CARDINALIDADE e as páginas somente se elas estiverem prontamente disponíveis no servidor. Nesse caso, o driver não assegura que os valores são atuais. (Aplicativos que são gravados para o padrão Open Group sempre obterão o comportamento SQL_QUICK do ODBC 3 *. x*-drivers compatíveis.)  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLStatistics** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL _ HANDLE_STMT e uma *manipular* dos *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLStatistics** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|24000|Estado de cursor inválido|Um cursor foi aberto sobre o *StatementHandle*, e **SQLFetch** ou **SQLFetchScroll** tivesse sido chamada. Esse erro é retornado pelo Gerenciador de Driver, se **SQLFetch** ou **SQLFetchScroll** não retornou SQL_NO_DATA e é retornado pelo driver se **SQLFetch** ou **SQLFetchScroll** tem retornar SQL_NO_DATA.<br /><br /> Um cursor foi aberto sobre o *StatementHandle*, mas **SQLFetch** ou **SQLFetchScroll** não tivesse sido chamada.|  
|40001|Falha na serialização|A transação foi revertida devido a um deadlock de recursos com outra transação.|  
|40003|Conclusão desconhecida de declaração|A conexão associada falhou durante a execução dessa função e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** na  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*, e, em seguida, a função foi chamada novamente na *StatementHandle*.<br /><br /> A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativos multithread.|  
|HY009|Uso inválido de ponteiro nulo|O *TableName* argumento é um ponteiro nulo.<br /><br /> O atributo de instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, o *CatalogName* argumento era um ponteiro nulo e o SQL_CATALOG_NAME *tipo de informação* retorna nomes de catálogo têm suporte.<br /><br /> (DM) o atributo da instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE e o *SchemaName* argumento é um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando o **SQLStatistics** função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *StatementHandle* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada antes de dados foram recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) uma função de execução assíncrona (não desse último) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retornados de SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM) o valor de um dos argumentos de comprimento do nome da era menor que 0 mas não iguais a SQL_NTS.<br /><br /> O valor de um dos argumentos de comprimento de nome excedeu o valor de comprimento máximo para o nome correspondente.|  
|HY100|Tipo de opção de exclusividade fora do intervalo|(DM) inválido *Unique* valor foi especificado.|  
|HY101|Tipo de opção de exatidão fora do intervalo|(DM) inválido *reservado* valor foi especificado.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|Um catálogo foi especificado e o driver ou fonte de dados não oferece suporte a catálogos.<br /><br /> Um esquema foi especificado e o driver ou fonte de dados não oferece suporte a esquemas.<br /><br /> A combinação das configurações atuais dos atributos de instrução SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE não era compatível com a driver ou fonte de dados.<br /><br /> O atributo da instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE, e o atributo SQL_ATTR_CURSOR_TYPE de instrução foi definido como um tipo de cursor para o qual o driver não oferece suporte a indicadores.|  
|HYT00|Tempo limite esgotado|O período de tempo limite da consulta expirou antes da fonte de dados retornada um conjunto de resultado solicitada. O período de tempo limite é definido por meio **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|O driver em (DM) associado a *StatementHandle* não suporta a função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem é desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior no identificador retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado no identificador de fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 **SQLStatistics** retorna informações sobre uma única tabela como um conjunto de resultados padrão, ordenado por NON_UNIQUE, tipo, INDEX_QUALIFIER, INDEX_NAME e ORDINAL_POSITION. O conjunto de resultados combina informações de estatísticas (em colunas CARDINALIDADE e as páginas do conjunto de resultados) para a tabela com informações sobre cada índice. Para obter informações sobre como essas informações podem ser usadas, consulte [usa do catálogo de dados](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 Para determinar os comprimentos reais das colunas TABLE_CAT, por TABLE_SCHEM, TABLE_NAME e nome da coluna, um aplicativo pode chamar **SQLGetInfo** com o SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN, e opções de SQL_MAX_COLUMN_NAME_LEN.  
  
> [!NOTE]  
>  Para obter mais informações sobre o uso geral, os argumentos e os dados retornados de funções de catálogo ODBC, consulte [funções de catálogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 As seguintes colunas foram renomeadas para ODBC 3 *. x*. As alterações de nome de coluna não afetam a compatibilidade com versões anteriores, porque aplicativos associar por número de coluna.  
  
|Coluna de ODBC 2.0|3 de ODBC *. x* coluna|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|SEQ_IN_INDEX|ORDINAL_POSITION|  
|COLLATION|ASC_OR_DESC|  
  
 A tabela a seguir lista as colunas no conjunto de resultados. Colunas adicionais além da coluna 13 (FILTER_CONDITION) podem ser definidas pelo driver. Um aplicativo deve obter acesso a colunas específicas do driver, contagem regressiva do final do conjunto em vez de especificar uma posição ordinal explícita de resultados. Para obter mais informações, consulte [dados retornados pelas funções de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome da coluna|Número da coluna|Tipo de dados|Comentários|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|Nome do catálogo da tabela à qual o índice ou estatística se aplica; NULL se não for aplicável à fonte de dados. Se um driver compatível com catálogos para algumas tabelas, mas não para outras pessoas, como quando o driver recupera os dados de diferentes DBMSs, ele retorna uma cadeia de caracteres vazia ("") para as tabelas que não têm catálogos.|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|Nome do esquema da tabela à qual o índice ou estatística se aplica; NULL se não for aplicável à fonte de dados. Se um driver compatível com esquemas para algumas tabelas, mas não para outras pessoas, como quando o driver recupera os dados de diferentes DBMSs, ele retorna uma cadeia de caracteres vazia ("") para as tabelas que não tem esquemas.|  
|TABLE_NAME (ODBC 1.0)|3|Varchar não nulo|Nome da tabela da tabela à qual o índice ou estatística se aplica.|  
|NON_UNIQUE (ODBC 1.0)|4|Smallint|Indica se o índice não permite valores duplicados:<br /><br /> SQL_TRUE se os valores de índice podem ser não exclusivos.<br /><br /> SQL_FALSE se os valores de índice devem ser exclusivos.<br /><br /> NULL será retornado se o tipo é SQL_TABLE_STAT.|  
|INDEX_QUALIFIER (ODBC 1.0)|5|Varchar|O identificador que é usado para qualificar o índice nome fazer uma **DROP INDEX**; NULL será retornado se um qualificador de índice não é compatível com a fonte de dados ou se o tipo é SQL_TABLE_STAT. Se um valor não nulo é retornado nesta coluna, ele deve ser usado para qualificar o nome do índice em uma **DROP INDEX** instrução; caso contrário, o TABLE_SCHEM deve ser usado para qualificar o nome do índice.|  
|INDEX_NAME (ODBC 1.0)|6|Varchar|Nome do índice; NULL será retornado se o tipo é SQL_TABLE_STAT.|  
|TIPO (ODBC 1.0)|7|Smallint não NULL|Tipo de informação que está sendo retornado:<br /><br /> SQL_TABLE_STAT indica uma estatística para a tabela (na coluna CARDINALIDADE ou páginas).<br /><br /> SQL_INDEX_BTREE indica um índice de árvore B.<br /><br /> SQL_INDEX_CLUSTERED indica um índice clusterizado.<br /><br /> SQL_INDEX_CONTENT indica um índice de conteúdo.<br /><br /> SQL_INDEX_HASHED indica um índice de hash.<br /><br /> SQL_INDEX_OTHER indica outro tipo de índice.|  
|ORDINAL_POSITION (ODBC 1.0)|8|Smallint|Número de sequência de coluna no índice (começando com 1); NULL será retornado se o tipo é SQL_TABLE_STAT.|  
|COLUMN_NAME (ODBC 1.0)|9|Varchar|Nome da coluna. Se a coluna se baseia em uma expressão, como o SALÁRIO + benefícios, a expressão é retornada; Se a expressão não pode ser determinada, uma cadeia de caracteres vazia será retornada. NULL será retornado se o tipo é SQL_TABLE_STAT.|  
|ASC_OR_DESC (ODBC 1.0)|10|char(1)|Sequência de classificação da coluna: "A" para em ordem crescente; "D" para decrescente; NULL será retornado se a sequência de classificação de coluna não é compatível com a fonte de dados ou se o tipo é SQL_TABLE_STAT.|  
|CARDINALIDADE (ODBC 1.0)|11|Integer|Cardinalidade da tabela ou índice; número de linhas na tabela se o tipo é SQL_TABLE_STAT; número de valores exclusivos no índice se o tipo não é SQL_TABLE_STAT; NULL será retornado se o valor não está disponível da fonte de dados.|  
|PÁGINAS DE (ODBC 1.0)|12|Integer|Número de páginas usadas para armazenar o índice ou tabela; número de páginas para a tabela se o tipo é SQL_TABLE_STAT; número de páginas para o índice se o tipo não é SQL_TABLE_STAT; NULL será retornado se o valor não está disponível da fonte de dados ou se não for aplicável à fonte de dados.|  
|FILTER_CONDITION (ODBC 2.0)|13|Varchar|Se o índice for um índice filtrado, essa é a condição de filtro, como o SALÁRIO > 30000; Se a condição de filtro não pode ser determinada, isso é uma cadeia de caracteres vazia.<br /><br /> NULO se o índice não é um índice filtrado, ele não pode ser determinado se o índice é um índice filtrado ou o tipo é SQL_TABLE_STAT.|  
  
 Se a linha no conjunto de resultados corresponde a uma tabela, o driver define o tipo para SQL_TABLE_STAT e define NON_UNIQUE, INDEX_QUALIFIER, INDEX_NAME, ORDINAL_POSITION, COLUMN_NAME e ASC_OR_DESC como NULL. Se a CARDINALIDADE ou as páginas não estão disponíveis da fonte de dados, o driver os define como NULL.  
  
## <a name="code-example"></a>Exemplo de código  
 Para obter um exemplo de código de uma função semelhante, consulte [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Um buffer de associação a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Buscando uma única linha ou um bloco de dados em uma direção de somente avanço.|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Buscar um bloco de dados ou rolar por um resultado definido|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Retornando as colunas de chaves estrangeiras|[Função SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|  
|Retornando as colunas de uma chave primária|[Função SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
