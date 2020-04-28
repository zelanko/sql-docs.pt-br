---
title: Função SQLPrimaryKeys | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLPrimaryKeys
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLPrimaryKeys
helpviewer_keywords:
- SQLPrimaryKeys function [ODBC]
ms.assetid: 3f809b09-3c1b-415e-80c5-a603e8e25d5b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 24407670ab9f1489a14bec19d910060b49d4bda0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306861"
---
# <a name="sqlprimarykeys-function"></a>Função SQLPrimaryKeys
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: ODBC  
  
 **Resumo**  
 **SQLPrimaryKeys** retorna os nomes de coluna que compõem a chave primária de uma tabela. O driver retorna as informações como um conjunto de resultados. Essa função não dá suporte ao retorno de chaves primárias de várias tabelas em uma única chamada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
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
 Entrada Identificador de instrução.  
  
 *CatalogName*  
 Entrada Nome do catálogo. Se um driver oferecer suporte a catálogos para algumas tabelas, mas não para outras, como quando o driver recupera dados de DBMSs diferentes, uma cadeia de caracteres vazia ("") denota as tabelas que não têm catálogos. *CatalogName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *CatalogName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *CatalogName* será um argumento comum; Ele é tratado literalmente e seu caso é significativo. Para obter mais informações, consulte [argumentos em funções de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 Entrada Comprimento em caracteres de **nome_do_catálogo*.  
  
 *SchemaName*  
 Entrada Nome do esquema. Se um driver oferecer suporte a esquemas para algumas tabelas, mas não para outras, como quando o driver recupera dados de DBMSs diferentes, uma cadeia de caracteres vazia ("") denota as tabelas que não têm esquemas. *SchemaName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *SchemaName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *SchemaName* será um argumento comum; Ele é tratado literalmente, e seu caso não é significativo.  
  
 *NameLength2*  
 Entrada Comprimento em caracteres de **SchemaName*.  
  
 *TableName*  
 Entrada Nome da tabela. Este argumento não pode ser um ponteiro nulo. *TableName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *TableName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *TableName* é um argumento comum; Ele é tratado literalmente, e seu caso não é significativo.  
  
 *NameLength3*  
 Entrada Comprimento em caracteres de **TableName*.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLPrimaryKeys** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *identificador* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLPrimaryKeys** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado falhou antes da função concluir o processamento.|  
|24.000|Estado de cursor inválido|(DM) um cursor foi aberto no *StatementHandle*e **SQLFetch** ou **SQLFetchScroll** foi chamado.<br /><br /> Um cursor estava aberto no *StatementHandle*, mas **SQLFetch** ou **SQLFetchScroll** não tinha sido chamado.|  
|40001|Falha de serialização|A transação foi revertida devido a um deadlock de recurso com outra transação.|  
|40003|Conclusão de instrução desconhecida|A conexão associada falhou durante a execução dessa função, e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \*MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativo multithread.|  
|HY009|Uso inválido de ponteiro nulo|(DM) o argumento *TableName* era um ponteiro nulo.<br /><br /> O atributo da instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, o argumento *CatalogName* era um ponteiro nulo e **SQLGetInfo** com o tipo de informações SQL_CATALOG_NAME retorna que os nomes de catálogo têm suporte.<br /><br /> (DM) o atributo de instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, e o argumento *SchemaName* era um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *StatementHandle*. Esta função assíncrona ainda estava em execução quando a função **SQLPrimaryKeys** foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para *StatementHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado para o *StatementHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|(DM) o valor de um dos argumentos de comprimento de nome era menor que 0, mas diferente de SQL_NTS, e o argumento de nome associado não é um ponteiro nulo.<br /><br /> O valor de um dos argumentos de comprimento do nome excedeu o valor de comprimento máximo para o nome correspondente.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|Um catálogo foi especificado e o driver ou a fonte de dados não oferece suporte a catálogos.<br /><br /> Um esquema foi especificado e o driver ou a fonte de dados não oferece suporte a esquemas.<br /><br /> A combinação das configurações atuais dos atributos de instrução SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE não era suportada pelo driver ou pela fonte de dados.<br /><br /> O atributo de instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE e o atributo de instrução SQL_ATTR_CURSOR_TYPE foi definido como um tipo de cursor para o qual o driver não dá suporte a indicadores.|  
|HYT00|Tempo limite esgotado|O período de tempo limite expirou antes que a fonte de dados retornasse o conjunto de resultados solicitado. O período de tempo limite é definido por meio de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *StatementHandle* não oferece suporte à função.|  
|IM017|A sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação for usado, a sondagem será desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesse identificador.|Se a chamada de função anterior no identificador retornar SQL_STILL_EXECUTING e se o modo de notificação estiver habilitado, **SQLCompleteAsync** deverá ser chamado na alça para executar o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 **SQLPrimaryKeys** retorna os resultados como um conjunto de resultados padrão, ordenados por TABLE_CAT, TABLE_SCHEM, TABLE_NAME e KEY_SEQ. Para obter informações sobre como essas informações podem ser usadas, consulte [usos de dados do catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 As colunas a seguir foram renomeadas para ODBC 3. *x*. As alterações de nome de coluna não afetam a compatibilidade com versões anteriores porque os aplicativos são associados por número de coluna.  
  
|Coluna ODBC 2,0|ODBC 3. coluna *x*|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 Para determinar os comprimentos reais das colunas TABLE_CAT, TABLE_SCHEM, TABLE_NAME e COLUMN_NAME, chame **SQLGetInfo** com as opções SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN e SQL_MAX_COLUMN_NAME_LEN.  
  
> [!NOTE]  
>  Para obter mais informações sobre o uso geral, argumentos e dados retornados de funções de catálogo ODBC, consulte [Catalog Functions](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 A tabela a seguir lista as colunas no conjunto de resultados. Colunas adicionais além da coluna 6 (PK_NAME) podem ser definidas pelo driver. Um aplicativo deve obter acesso a colunas específicas do driver, contando a partir do final do conjunto de resultados em vez de especificar uma posição ordinal explícita. Para obter mais informações, consulte [dados retornados por funções de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome da coluna|Número da coluna|Tipo de dados|Comentários|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1,0)|1|Varchar|Nome do catálogo da tabela de chave primária; NULL se não for aplicável à fonte de dados. Se um driver oferecer suporte a catálogos para algumas tabelas, mas não para outras, como quando o driver recupera dados de DBMSs diferentes, ele retorna uma cadeia de caracteres vazia ("") para as tabelas que não têm catálogos.|  
|TABLE_SCHEM (ODBC 1,0)|2|Varchar|Nome do esquema da tabela de chave primária; NULL se não for aplicável à fonte de dados. Se um driver oferecer suporte a esquemas para algumas tabelas, mas não para outras, como quando o driver recupera dados de DBMSs diferentes, ele retorna uma cadeia de caracteres vazia ("") para as tabelas que não têm esquemas.|  
|TABLE_NAME (ODBC 1,0)|3|Varchar não nulo|Nome da tabela de chave primária.|  
|COLUMN_NAME (ODBC 1,0)|4|Varchar não nulo|Nome da coluna de chave primária. O driver retorna uma cadeia de caracteres vazia para uma coluna que não tem um nome.|  
|KEY_SEQ (ODBC 1,0)|5|Smallint não NULL|Número de sequência da coluna na chave (começando com 1).|  
|PK_NAME (ODBC 2,0)|6|Varchar|Nome da chave primária. NULL se não for aplicável à fonte de dados.|  
  
## <a name="code-example"></a>Exemplo de código  
 Consulte [SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Associando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Buscando um bloco de dados ou rolando por meio de um conjunto de resultados|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Buscando uma única linha ou um bloco de dados em uma direção somente de avanço|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Retornando as colunas de chaves estrangeiras|[Função SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|  
|Retornando índices e estatísticas de tabela|[Função SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
