---
title: "Função SQLPrimaryKeys | Microsoft Docs"
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
apiname: SQLPrimaryKeys
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLPrimaryKeys
helpviewer_keywords: SQLPrimaryKeys function [ODBC]
ms.assetid: 3f809b09-3c1b-415e-80c5-a603e8e25d5b
caps.latest.revision: "22"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 597ccf9143957c0d7f2ad1dbe29b77636eb54b49
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="sqlprimarykeys-function"></a>Função SQLPrimaryKeys
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 1.0 ODBC: ODBC  
  
 **Resumo**  
 **SQLPrimaryKeys** retorna os nomes das colunas que constituem o principal da chave para uma tabela. O driver retorna as informações como um conjunto de resultados. Essa função não oferece suporte para retornar as chaves primárias de várias tabelas em uma única chamada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLPrimaryKeys(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      CatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      SchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      TableName,  
     SQLSMALLINT    NameLength3);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrução.  
  
 *CatalogName*  
 [Entrada] Nome do catálogo. Se um driver dá suporte a catálogos para algumas tabelas, mas não para outras pessoas, como quando o driver recupera os dados de diferentes DBMSs, uma cadeia de caracteres vazia ("") indica que as tabelas que não possuem catálogos. *CatalogName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *CatalogName* é tratado como um identificador e o seu caso não é significativo. Se for SQL_FALSE, *CatalogName* é um argumento comum; ela será tratada literalmente e seu caso é significativo. Para obter mais informações, consulte [argumentos em funções de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Entrada] Comprimento em caracteres de **CatalogName*.  
  
 *SchemaName*  
 [Entrada] Nome do esquema. Se um driver dá suporte a esquemas para algumas tabelas, mas não para outras pessoas, como quando o driver recupera os dados de diferentes DBMSs, uma cadeia de caracteres vazia ("") indica que as tabelas que não têm esquemas. *SchemaName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *SchemaName* é tratado como um identificador e o seu caso não é significativo. Se for SQL_FALSE, *SchemaName* é um argumento comum; ela será tratada literalmente e seu caso não é significativo.  
  
 *NameLength2*  
 [Entrada] Comprimento em caracteres de **SchemaName*.  
  
 *Nome de tabela*  
 [Entrada] Nome da tabela. Esse argumento não pode ser um ponteiro nulo. *TableName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *TableName* é tratado como um identificador e o seu caso não é significativo. Se for SQL_FALSE, *TableName* é um argumento comum; ela será tratada literalmente e seu caso não é significativo.  
  
 *NameLength3*  
 [Entrada] Comprimento em caracteres de **TableName*.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLPrimaryKeys** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* do SQL _HANDLE_STMT e um *tratar* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLPrimaryKeys** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|24000|Estado de cursor inválido|(DM) um cursor foi aberto o *StatementHandle*, e **SQLFetch** ou **SQLFetchScroll** tivesse sido chamada.<br /><br /> Um cursor foi aberto o *StatementHandle*, mas **SQLFetch** ou **SQLFetchScroll** não tivesse sido chamada.|  
|40001|Falha na serialização|A transação foi revertida devido a um deadlock de recursos com outra transação.|  
|40003|Conclusão de instrução desconhecido|A conexão associada falhou durante a execução dessa função e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo **SQLGetDiagRec** no  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em uma aplicativos multithread.|  
|HY009|Uso inválido de ponteiro nulo|(DM) a *TableName* argumento era um ponteiro nulo.<br /><br /> O atributo de instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, o *CatalogName* argumento era um ponteiro nulo, e **SQLGetInfo** com as informações de SQL_CATALOG_NAME tipo retorna esse catálogo há suporte para nomes.<br /><br /> (DM), o atributo da instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE e o *SchemaName* argumento era um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando o **SQLPrimaryKeys** função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *StatementHandle* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada antes de recuperação para todos os parâmetros de fluxo de dados.<br /><br /> (DM) uma função de execução assíncrona (não la) foi chamada para o *StatementHandle* e ainda estava em execução quando esta função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retorna SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todas as colunas ou parâmetros de dados em execução.|  
|HY013|Erro de gerenciamento de memória|Não foi possível processar a chamada de função porque os objetos de memória subjacente não podem ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM) o valor de um dos argumentos de comprimento de nome era menor do que 0 mas não igual a SQL_NTS e o argumento de nome de associado é não um ponteiro nulo.<br /><br /> O valor de um dos argumentos de comprimento de nome excedeu o valor de comprimento máximo para o nome correspondente.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecido. Somente Desconecte e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|Um catálogo foi especificado e o driver ou fonte de dados não dá suporte a catálogos.<br /><br /> Foi especificado um esquema e o driver ou fonte de dados não dá suporte a esquemas.<br /><br /> A combinação das configurações atuais dos atributos de instrução SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE não era compatível com a driver ou fonte de dados.<br /><br /> O atributo da instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE, e o atributo de instrução SQL_ATTR_CURSOR_TYPE foi definido como um tipo de cursor para o qual o driver não oferecer suporte a indicadores.|  
|HYT00|Tempo limite esgotado|O período de tempo limite expirou antes da fonte de dados retornada este conjunto de resultado solicitada. O período de tempo limite é definido por meio de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|O driver em (DM) associado a *StatementHandle* não oferece suporte para a função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem está desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior na alça retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 **SQLPrimaryKeys** retorna os resultados como um conjunto de resultados padrão, ordenado por TABLE_CAT, TABLE_SCHEM, TABLE_NAME e KEY_SEQ. Para obter informações sobre como essas informações podem ser usadas, consulte [usa do catálogo de dados](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 As seguintes colunas foram renomeadas para ODBC 3. *x*. As alterações de nome de coluna não afetam a compatibilidade com versões anteriores, porque aplicativos associar pelo número de coluna.  
  
|Coluna de ODBC 2.0|ODBC 3. *x* coluna|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 Para determinar os comprimentos reais das colunas TABLE_CAT, TABLE_SCHEM, TABLE_NAME e nome da coluna, chame **SQLGetInfo** com o SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN e SQL_MAX_COLUMN Opções de _NAME_LEN.  
  
> [!NOTE]  
>  Para obter mais informações sobre o uso geral, os argumentos e os dados retornados de funções de catálogo ODBC, consulte [funções de catálogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 A tabela a seguir lista as colunas no conjunto de resultados. Colunas adicionais além da coluna 6 (PK_NAME) podem ser definidas pelo driver. Um aplicativo deve acessar colunas específicas do driver por contagem regressiva do final do conjunto de resultados em vez de especificar uma posição ordinal explícita. Para obter mais informações, consulte [dados retornados pelas funções de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome da coluna|Número da coluna|Tipo de dados|Comentários|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|Nome de catálogo da tabela de chave primária; NULL se não for aplicável à fonte de dados. Se um driver dá suporte a catálogos para algumas tabelas, mas não para outras pessoas, como quando o driver recupera os dados de diferentes DBMSs, ele retorna uma cadeia de caracteres vazia ("") para as tabelas que não possuem catálogos.|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|Nome do esquema de tabela de chave primária; NULL se não for aplicável à fonte de dados. Se um driver dá suporte a esquemas para algumas tabelas, mas não para outras pessoas, como quando o driver recupera os dados de diferentes DBMSs, ele retorna uma cadeia de caracteres vazia ("") para as tabelas que não têm esquemas.|  
|TABLE_NAME (ODBC 1.0)|3|Varchar não nulo|Nome da tabela de chave primária.|  
|NOME DA COLUNA (ODBC 1.0)|4|Varchar não nulo|Nome da coluna de chave primária. O driver retorna uma cadeia de caracteres vazia para uma coluna que não tem um nome.|  
|KEY_SEQ (ODBC 1.0)|5|Smallint não NULL|Número de sequência da coluna na chave (começando com 1).|  
|PK_NAME (ODBC 2.0)|6|Varchar|Nome da chave primária. NULL se não for aplicável à fonte de dados.|  
  
## <a name="code-example"></a>Exemplo de código  
 Consulte [SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Um buffer de associação a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Buscar um bloco de dados ou rolar por um resultado definido|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Buscando uma única linha ou um bloco de dados em uma direção de somente avanço|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Retornando as colunas de chaves estrangeiras|[Função SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|  
|Retornando estatísticas de tabela e índices|[Função SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
