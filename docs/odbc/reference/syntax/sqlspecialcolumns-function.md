---
title: "Função SQLSpecialColumns | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLSpecialColumns
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSpecialColumns
helpviewer_keywords:
- SQLSpecialColumns function [ODBC]
ms.assetid: bb2d9f21-bda0-4e50-a8be-f710db660034
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ae814d95d376e928e2fafc323dedc14a3a532aa8
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlspecialcolumns-function"></a>Função SQLSpecialColumns
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 1.0 ODBC: Open Group  
  
 **Resumo**  
 **SQLSpecialColumns** recupera as seguintes informações sobre colunas em uma tabela especificada:  
  
-   O conjunto ideal de colunas que identifica exclusivamente uma linha na tabela.  
  
-   Colunas que são atualizadas automaticamente quando qualquer valor na linha é atualizada por uma transação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLSpecialColumns(  
     SQLHSTMT      StatementHandle,  
     SQLSMALLINT   IdentifierType,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     TableName,  
     SQLSMALLINT   NameLength3,  
     SQLSMALLINT   Scope,  
     SQLSMALLINT   Nullable);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrução.  
  
 *IdentifierType*  
 [Entrada] Tipo de coluna a ser retornada. Deve ser um dos seguintes valores:  
  
 SQL_BEST_ROWID: Retorna a coluna ou conjunto ideal de colunas que, pela recuperação de valores de coluna ou colunas, permite que qualquer linha da tabela especificada seja identificada de forma exclusiva. Uma coluna pode ser uma coluna de pseudo projetada especificamente para essa finalidade (como Oracle ROWID ou Ingres TID) ou a coluna ou colunas de qualquer índice exclusivo para a tabela.  
  
 SQL_ROWVER: Retorna a coluna ou colunas na tabela especificada, se houver, que são automaticamente atualizadas pela fonte de dados quando qualquer valor na linha for atualizado por qualquer transação (como SQLBase ROWID ou Sybase TIMESTAMP).  
  
 *CatalogName*  
 [Entrada] Nome do catálogo para a tabela. Se um driver dá suporte a catálogos para algumas tabelas, mas não para outras pessoas, como quando o driver recupera os dados de diferentes DBMSs, uma cadeia de caracteres vazia ("") indica que as tabelas que não possuem catálogos. *CatalogName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *CatalogName* é tratado como um identificador e o seu caso não é significativo. Se for SQL_FALSE, *CatalogName* é um argumento comum; ela será tratada literalmente e seu caso é significativo. Para obter mais informações, consulte [argumentos em funções de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Entrada] Comprimento em caracteres de **CatalogName*.  
  
 *SchemaName*  
 [Entrada] Nome do esquema da tabela. Se um driver dá suporte a esquemas para algumas tabelas, mas não para outras pessoas, como quando o driver recupera os dados de diferentes DBMSs, uma cadeia de caracteres vazia ("") indica que as tabelas que não têm esquemas. *SchemaName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *SchemaName* é tratado como um identificador e o seu caso não é significativo. Se for SQL_FALSE, *SchemaName* é um argumento comum; ela será tratada literalmente e seu caso é significativo.  
  
 *NameLength2*  
 [Entrada] Comprimento em caracteres de **SchemaName*.  
  
 *Nome de tabela*  
 [Entrada] Nome da tabela. Esse argumento não pode ser um ponteiro nulo. *TableName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *TableName* é tratado como um identificador e o seu caso não é significativo. Se for SQL_FALSE, *TableName* é um argumento comum; ela será tratada literalmente e seu caso é significativo.  
  
 *NameLength3*  
 [Entrada] Comprimento em caracteres de **TableName*.  
  
 *Escopo*  
 [Entrada] Escopo mínimo necessário de rowid. Rowid retornado pode ser maior do escopo. Deve ser uma destas opções:  
  
 SQL_SCOPE_CURROW: Rowid é garantido para ser válida somente quando posicionada nessa linha. Uma nova seleção posterior usando o rowid pode não retornar uma linha se a linha foi atualizada ou excluída por outra transação.  
  
 SQL_SCOPE_TRANSACTION: Rowid é garantido para ser válida para a duração da transação atual.  
  
 SQL_SCOPE_SESSION: Rowid é garantido para ser válida para a duração da sessão (nos limites da transação).  
  
 *Anulável*  
 [Entrada] Determina se deve retornar colunas especiais que podem ter um valor nulo. Deve ser uma destas opções:  
  
 SQL_NO_NULLS: Excluir colunas especiais que podem ter valores nulos. Alguns drivers não aceitam SQL_NO_NULLS e esses drivers retornará um resultado vazio definido se SQL_NO_NULLS foi especificado. Aplicativos devem estar preparados para esta solicitação SQL_NO_NULLS de caso e somente se ele é absolutamente necessário.  
  
 SQL_NULLABLE: Retornar colunas especiais, mesmo que eles podem ter valores nulos.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLSpecialColumns** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *tratar* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLSpecialColumns** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|24000|Estado de cursor inválido|Um cursor foi aberto o *StatementHandle*, e **SQLFetch** ou **SQLFetchScroll** tivesse sido chamada. Esse erro é retornado pelo Gerenciador de Driver se **SQLFetch** ou **SQLFetchScroll** não retornou SQL_NO_DATA e é retornada pelo driver se **SQLFetch** ou **SQLFetchScroll** retornou SQL_NO_DATA.<br /><br /> Um cursor foi aberto o *StatementHandle*, mas **SQLFetch** ou **SQLFetchScroll** não tivesse sido chamada.|  
|40001|Falha na serialização|A transação foi revertida devido a um deadlock de recursos com outra transação.|  
|40003|Conclusão de instrução desconhecido|A conexão associada falhou durante a execução dessa função e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo **SQLGetDiagRec** no  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em uma aplicativos multithread.|  
|HY009|Uso inválido de ponteiro nulo|O *TableName* argumento era um ponteiro nulo.<br /><br /> O atributo de instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, o *CatalogName* argumento era um ponteiro nulo e o SQL_CATALOG_NAME *informação* retorna nomes de catálogo é suportadas.<br /><br /> (DM), o atributo da instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE e o *SchemaName* argumento era um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função ainda estava em execução quando **SQLSpecialColumns** foi chamado.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *StatementHandle* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada antes de recuperação para todos os parâmetros de fluxo de dados.<br /><br /> (DM) uma função de execução assíncrona (não la) foi chamada para o *StatementHandle* e ainda estava em execução quando esta função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retorna SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todas as colunas ou parâmetros de dados em execução.|  
|HY013|Erro de gerenciamento de memória|Não foi possível processar a chamada de função porque os objetos de memória subjacente não podem ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM) o valor de um dos argumentos de comprimento era menor do que 0 mas não igual a SQL_NTS.<br /><br /> O valor de um dos argumentos de comprimento excedeu o valor de comprimento máximo para o nome correspondente. O comprimento máximo de cada nome pode ser obtido chamando **SQLGetInfo** com o *informação* valores: SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN ou SQL_MAX_TABLE_NAME_LEN.|  
|HY097|Tipo de coluna fora do intervalo|(DM) inválido *IdentifierType* valor foi especificado.|  
|HY098|Tipo de escopo fora do intervalo|(DM) inválido *escopo* valor foi especificado.|  
|HY099|Tipo anulável fora do intervalo|(DM) inválido *Nullable* valor foi especificado.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecido. Somente Desconecte e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|Um catálogo foi especificado e o driver ou fonte de dados não dá suporte a catálogos.<br /><br /> Foi especificado um esquema e o driver ou fonte de dados não dá suporte a esquemas.<br /><br /> A combinação das configurações atuais dos atributos de instrução SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE não era compatível com a driver ou fonte de dados.<br /><br /> O atributo da instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE, e o atributo de instrução SQL_ATTR_CURSOR_TYPE foi definido como um tipo de cursor para o qual o driver não oferecer suporte a indicadores.|  
|HYT00|Tempo limite esgotado|O período de tempo limite da consulta expirou antes da fonte de dados retornada este conjunto de resultado solicitada. O período de tempo limite é definido por meio de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|O driver em (DM) associado a *StatementHandle* não oferece suporte para a função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem está desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior na alça retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 Quando o *IdentifierType* argumento é SQL_BEST_ROWID, **SQLSpecialColumns** retorna a coluna ou colunas que identificam exclusivamente cada linha na tabela. Estas colunas sempre podem ser usadas em uma *lista de select* ou **onde** cláusula. **SQLColumns**, que é usada para retornar uma variedade de informações sobre as colunas de uma tabela, não necessariamente retornará as colunas que identificam exclusivamente cada linha ou colunas que são atualizadas automaticamente quando qualquer valor na linha é atualizada por um transação. Por exemplo, **SQLColumns** podem não retornar ROWID coluna pseudo Oracle. É por isso que **SQLSpecialColumns** é usado para retornar essas colunas. Para obter mais informações, consulte [usa do catálogo de dados](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
> [!NOTE]  
>  Para obter mais informações sobre o uso geral, os argumentos e os dados retornados de funções de catálogo ODBC, consulte [funções de catálogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 Se não houver nenhuma coluna que identificam exclusivamente cada linha na tabela, **SQLSpecialColumns** retorna um conjunto de linhas sem linhas; uma chamada subsequente para **SQLFetch** ou **SQLFetchScroll**na instrução retorna SQL_NO_DATA.  
  
 Se o *IdentifierType*, *escopo*, ou *Nullable* argumentos especificam características que não são suportadas pela fonte de dados, **SQLSpecialColumns**  retorna um conjunto de resultados vazio.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, o *CatalogName*, *SchemaName*, e *TableName* argumentos são tratados como identificadores, portanto eles não pode ser definido como um ponteiro nulo em determinadas situações. (Para obter mais informações, consulte [argumentos em funções de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).)  
  
 **SQLSpecialColumns** retorna os resultados como um conjunto de resultados padrão, ordenado por SCOPE.  
  
 As seguintes colunas foram renomeadas para ODBC 3*. x*. As alterações de nome de coluna não afetam a compatibilidade com versões anteriores, porque aplicativos associar pelo número de coluna.  
  
|Coluna de ODBC 2.0|ODBC 3*. x* coluna|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
  
 Para determinar o comprimento real da coluna Nome da coluna, um aplicativo pode chamar **SQLGetInfo** com a opção SQL_MAX_COLUMN_NAME_LEN.  
  
 A tabela a seguir lista as colunas no conjunto de resultados. Colunas adicionais além da coluna 8 (PSEUDO_COLUMN) podem ser definidas pelo driver. Um aplicativo deve acessar colunas específicas do driver por contagem regressiva do final do conjunto de resultados em vez de especificar uma posição ordinal explícita. Para obter mais informações, consulte [dados retornados pelas funções de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome da coluna|Número da coluna|Tipo de dados|Comentários|  
|-----------------|-------------------|---------------|--------------|  
|ESCOPO (ODBC 1.0)|1|Smallint|Escopo real de rowid. Contém um dos seguintes valores:<br /><br /> SQL_SCOPE_CURROW SQL_SCOPE_TRANSACTION SQL_SCOPE_SESSION<br /><br /> NULL é retornado quando *IdentifierType* é SQL_ROWVER. Para obter uma descrição de cada valor, consulte a descrição do *escopo* "Sintaxe", anteriormente nesta seção.|  
|NOME DA COLUNA (ODBC 1.0)|2|Varchar não nulo|Nome da coluna. O driver retorna uma cadeia de caracteres vazia para uma coluna que não tem um nome.|  
|DATA_TYPE (ODBC 1.0)|3|Smallint não NULL|Tipo de dados SQL. Isso pode ser um tipo de dados SQL ODBC ou um tipo de dados SQL específico do driver. Para obter uma lista de tipos de dados ODBC SQL válidos, consulte [tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md). Para obter informações sobre tipos de dados SQL específico do driver, consulte a documentação do driver.|  
|TYPE_NAME (ODBC 1.0)|4|Varchar não nulo|Nome do tipo de dados de origem dependente de dados; Por exemplo, "CHAR", "VARCHAR", "MONEY", "VARBINARY longo" ou "CHAR () para dados BIT".|  
|COLUMN_SIZE (ODBC 1.0)|5|Integer|O tamanho da coluna na fonte de dados. Para obter mais informações sobre o tamanho da coluna, consulte [tamanho da coluna, dígitos decimais, transferir o comprimento do octeto e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).|  
|BUFFER_LENGTH (ODBC 1.0)|6|Integer|O comprimento em bytes de dados transferidos em um **SQLGetData** ou **SQLFetch** operação se SQL_C_DEFAULT for especificado. Para dados numéricos, esse tamanho pode ser diferente do que o tamanho dos dados armazenados na fonte de dados. Esse valor é o mesmo que a coluna COLUMN_SIZE para caracteres ou dados binários. Para obter mais informações, consulte [tamanho da coluna, dígitos decimais, transferir o comprimento do octeto e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).|  
|DECIMAL_DIGITS (ODBC 1.0)|7|Smallint|Os dígitos decimais da coluna na fonte de dados. NULL é retornado para os tipos de dados em que os dígitos decimais não são aplicáveis. Para obter mais informações sobre os dígitos decimais, consulte [tamanho da coluna, dígitos decimais, transferir o comprimento do octeto e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).|  
|PSEUDO_COLUMN (ODBC 2.0)|8|Smallint|Indica se a coluna é uma coluna pseudo, como Oracle ROWID:<br /><br /> SQL_PC_UNKNOWN SQL_PC_NOT_PSEUDO SQL_PC_PSEUDO **Observação:** para interoperabilidade máxima, pseudo colunas não devem ser citadas com o caractere de aspas de identificador retornado por **SQLGetInfo**.|  
  
 Depois que o aplicativo recupera os valores para SQL_BEST_ROWID, o aplicativo pode usar esses valores para selecionar a linha dentro do escopo definido. O **selecione** garantia de instrução para retornar nenhuma linha ou uma linha.  
  
 Se um aplicativo reselects uma linha com base na coluna rowid ou colunas e a linha não for encontrada, o aplicativo pode assumir que a linha foi excluída ou as colunas rowid foram modificadas. O oposto não for verdadeiro: mesmo que a rowid não foi alterado, as outras colunas na linha podem ter alterado.  
  
 Colunas retornadas para o tipo de coluna SQL_BEST_ROWID são úteis para aplicativos que precisam para rolar para frente e dentro de um conjunto de resultados para recuperar os dados mais recentes de um conjunto de linhas. A coluna ou colunas de rowid têm a garantia para não alterar quando posicionada nessa linha.  
  
 A coluna ou colunas de rowid poderão permanecer válidas mesmo quando o cursor não está posicionado na linha; o aplicativo pode determinar isso verificando a coluna de escopo no conjunto de resultados.  
  
 Colunas retornadas para o tipo de coluna SQL_ROWVER são úteis para aplicativos que precisam ser capazes de verificar se qualquer coluna em uma determinada linha tiver sido atualizada enquanto a linha foi remarcada usando o rowid. Por exemplo, depois que você seleciona novamente uma linha usando o rowid, o aplicativo pode comparar os valores anteriores nas colunas SQL_ROWVER às apenas buscados. Se o valor em uma coluna SQL_ROWVER difere do valor anterior, o aplicativo pode alertar o usuário que foram alterados na exibição.  
  
## <a name="code-example"></a>Exemplo de código  
 Para obter um exemplo de código de uma função semelhante, consulte [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Um buffer de associação a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Retornando as colunas em uma tabela ou tabelas|[Função SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|Buscando uma única linha ou um bloco de dados em uma direção de somente avanço|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Buscar um bloco de dados ou rolar por um resultado definido|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Retornando as colunas de uma chave primária|[Função SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)

