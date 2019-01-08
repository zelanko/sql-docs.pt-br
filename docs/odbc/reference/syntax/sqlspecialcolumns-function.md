---
title: Função SQLSpecialColumns | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f44ae90a82e778bf8e8564b719aa6b9f0157a05a
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53204365"
---
# <a name="sqlspecialcolumns-function"></a>Função SQLSpecialColumns
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 1.0 ODBC: Open Group  
  
 **Resumo**  
 **SQLSpecialColumns** recupera as seguintes informações sobre colunas dentro de uma tabela especificada:  
  
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
  
 SQL_BEST_ROWID: Retorna a coluna ou conjunto ideal de colunas que, pela recuperação de valores da coluna ou colunas, permite que qualquer linha na tabela especificada seja identificada de forma exclusiva. Uma coluna pode ser uma coluna de pseudo projetada especificamente para essa finalidade (como no Oracle ROWID ou TID Ingres) ou a coluna ou colunas de qualquer índice exclusivo para a tabela.  
  
 SQL_ROWVER: Retorna a coluna ou colunas na tabela especificada, se houver, que são automaticamente atualizadas pela fonte de dados quando qualquer valor na linha for atualizado por qualquer transação (como em SQLBase ROWID ou Sybase TIMESTAMP).  
  
 *CatalogName*  
 [Entrada] Nome do catálogo para a tabela. Se um driver compatível com catálogos para algumas tabelas, mas não para outros, como quando o driver recupera os dados de diferentes DBMSs, uma cadeia de caracteres vazia ("") indica que as tabelas que não têm catálogos. *CatalogName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *CatalogName* é tratado como um identificador e o seu caso de não é significativo. Se for SQL_FALSE, *CatalogName* é um argumento comum; ela será tratada, literalmente, e seu caso é significativo. Para obter mais informações, consulte [argumentos em funções de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Entrada] Comprimento em caracteres de **CatalogName*.  
  
 *SchemaName*  
 [Entrada] Nome do esquema da tabela. Se um driver compatível com esquemas para algumas tabelas, mas não para outros, como quando o driver recupera os dados de diferentes DBMSs, uma cadeia de caracteres vazia ("") indica que as tabelas que não tem esquemas. *SchemaName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *SchemaName* é tratado como um identificador e o seu caso de não é significativo. Se for SQL_FALSE, *SchemaName* é um argumento comum; ela será tratada, literalmente, e seu caso é significativo.  
  
 *NameLength2*  
 [Entrada] Comprimento em caracteres de **SchemaName*.  
  
 *TableName*  
 [Entrada] Nome da tabela. Esse argumento não pode ser um ponteiro nulo. *TableName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *TableName* é tratado como um identificador e o seu caso de não é significativo. Se for SQL_FALSE, *TableName* é um argumento comum; ela será tratada, literalmente, e seu caso é significativo.  
  
 *NameLength3*  
 [Entrada] Comprimento em caracteres de **TableName*.  
  
 *Escopo*  
 [Entrada] Escopo mínimo necessário de rowid. Rowid retornado pode ser de maior escopo. Deve ser uma destas opções:  
  
 SQL_SCOPE_CURROW: Rowid é garantido para ser válida somente quando posicionada nessa linha. Uma posterior que utilize rowid não pode retornar uma linha se a linha foi atualizada ou excluída por outra transação.  
  
 SQL_SCOPE_TRANSACTION: Rowid é garantido que seja válido para a duração da transação atual.  
  
 SQL_SCOPE_SESSION: Rowid é garantido que seja válido para a duração da sessão (nos limites da transação).  
  
 *Permite valor nulo*  
 [Entrada] Determina se é necessário retornar colunas especiais que podem ter um valor nulo. Deve ser uma destas opções:  
  
 SQL_NO_NULLS: Exclua colunas especiais que podem ter valores nulos. Alguns drivers não dá suporte ao SQL_NO_NULLS e esses drivers retornará um resultado vazio definido se SQL_NO_NULLS foi especificado. Aplicativos devem estar preparados para esse caso e a solicitação SQL_NO_NULLS somente se for absolutamente necessário.  
  
 SQL_NULLABLE: Retorne colunas especiais, mesmo se eles podem ter valores nulos.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLSpecialColumns** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *manipular* dos *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLSpecialColumns** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|24000|Estado de cursor inválido|Um cursor foi aberto sobre o *StatementHandle*, e **SQLFetch** ou **SQLFetchScroll** tivesse sido chamada. Esse erro é retornado pelo Gerenciador de Driver, se **SQLFetch** ou **SQLFetchScroll** não retornou SQL_NO_DATA e é retornado pelo driver se **SQLFetch** ou **SQLFetchScroll** tem retornar SQL_NO_DATA.<br /><br /> Um cursor foi aberto sobre o *StatementHandle*, mas **SQLFetch** ou **SQLFetchScroll** não tivesse sido chamada.|  
|40001|Falha na serialização|A transação foi revertida devido a um deadlock de recursos com outra transação.|  
|40003|Conclusão desconhecida de declaração|A conexão associada falhou durante a execução dessa função e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** na  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente na *StatementHandle*.<br /><br /> A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativos multithread.|  
|HY009|Uso inválido de ponteiro nulo|O *TableName* argumento é um ponteiro nulo.<br /><br /> O atributo de instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, o *CatalogName* argumento era um ponteiro nulo e o SQL_CATALOG_NAME *tipo de informação* retorna nomes de catálogo têm suporte.<br /><br /> (DM) o atributo da instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE e o *SchemaName* argumento é um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função ainda estava em execução quando **SQLSpecialColumns** foi chamado.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *StatementHandle* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada antes de dados foram recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) uma função de execução assíncrona (não desse último) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retornados de SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM) o valor de um dos argumentos de comprimento era menor que 0 mas não iguais a SQL_NTS.<br /><br /> O valor de um dos argumentos de comprimento excedeu o valor de comprimento máximo para o nome correspondente. O comprimento máximo de cada nome pode ser obtido chamando **SQLGetInfo** com o *tipo de informação* valores: SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN ou SQL_MAX_TABLE_NAME_LEN.|  
|HY097|Tipo de coluna fora do intervalo|(DM) inválido *IdentifierType* valor foi especificado.|  
|HY098|Tipo de escopo fora do intervalo|(DM) inválido *escopo* valor foi especificado.|  
|HY099|Tipo anulável fora do intervalo|(DM) inválido *Nullable* valor foi especificado.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|Um catálogo foi especificado e o driver ou fonte de dados não oferece suporte a catálogos.<br /><br /> Um esquema foi especificado e o driver ou fonte de dados não oferece suporte a esquemas.<br /><br /> A combinação das configurações atuais dos atributos de instrução SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE não era compatível com a driver ou fonte de dados.<br /><br /> O atributo da instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE, e o atributo SQL_ATTR_CURSOR_TYPE de instrução foi definido como um tipo de cursor para o qual o driver não oferece suporte a indicadores.|  
|HYT00|Tempo limite esgotado|O período de tempo limite da consulta expirou antes da fonte de dados retornada um conjunto de resultado solicitada. O período de tempo limite é definido por meio **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|O driver em (DM) associado a *StatementHandle* não suporta a função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem é desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior no identificador retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado no identificador de fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 Quando o *IdentifierType* argumento é SQL_BEST_ROWID, **SQLSpecialColumns** retorna a coluna ou colunas que identificam exclusivamente cada linha na tabela. Essas colunas sempre podem ser usadas em uma *select-list* ou **onde** cláusula. **SQLColumns**, que é usado para retornar uma variedade de informações nas colunas de uma tabela, não necessariamente retornar as colunas que identificam exclusivamente cada linha ou colunas que são atualizadas automaticamente quando qualquer valor na linha é atualizada por um transação. Por exemplo, **SQLColumns** não pode retornar a coluna pseudo ROWID Oracle. É por isso **SQLSpecialColumns** é usado para retornar essas colunas. Para obter mais informações, consulte [usa do catálogo de dados](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
> [!NOTE]  
>  Para obter mais informações sobre o uso geral, os argumentos e os dados retornados de funções de catálogo ODBC, consulte [funções de catálogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 Se não houver nenhuma coluna que identificam exclusivamente cada linha na tabela, **SQLSpecialColumns** retorna um conjunto de linhas com nenhuma linha; uma chamada subsequente para **SQLFetch** ou **SQLFetchScroll**na instrução retorne SQL_NO_DATA.  
  
 Se o *IdentifierType*, *escopo*, ou *Nullable* argumentos especificam características que não têm suporte pela fonte de dados, **SQLSpecialColumns**  retorna um conjunto de resultados vazio.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, o *CatalogName*, *SchemaName*, e *TableName* argumentos são tratados como identificadores, portanto, eles não pode ser definido como um ponteiro nulo em determinadas situações. (Para obter mais informações, consulte [argumentos em funções de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).)  
  
 **SQLSpecialColumns** retorna os resultados como um conjunto de resultados padrão, ordenado por SCOPE.  
  
 As seguintes colunas foram renomeadas para ODBC 3 *. x*. As alterações de nome de coluna não afetam a compatibilidade com versões anteriores, porque aplicativos associar por número de coluna.  
  
|Coluna de ODBC 2.0|3 de ODBC *. x* coluna|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
  
 Para determinar o comprimento real da coluna COLUMN_NAME, um aplicativo pode chamar **SQLGetInfo** com a opção SQL_MAX_COLUMN_NAME_LEN.  
  
 A tabela a seguir lista as colunas no conjunto de resultados. Colunas adicionais além da coluna 8 (PSEUDO_COLUMN) podem ser definidas pelo driver. Um aplicativo deve obter acesso a colunas específicas do driver, contagem regressiva do final do conjunto de resultados em vez de especificar uma posição ordinal explícita. Para obter mais informações, consulte [dados retornados pelas funções de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome da coluna|Número da coluna|Tipo de dados|Comentários|  
|-----------------|-------------------|---------------|--------------|  
|ESCOPO (ODBC 1.0)|1|Smallint|Escopo real de rowid. Contém um dos seguintes valores:<br /><br /> SQL_SCOPE_CURROW SQL_SCOPE_TRANSACTION SQL_SCOPE_SESSION<br /><br /> NULL é retornado quando *IdentifierType* é SQL_ROWVER. Para obter uma descrição de cada valor, consulte a descrição da *escopo* em "Sintaxe" no início desta seção.|  
|COLUMN_NAME (ODBC 1.0)|2|Varchar não nulo|Nome da coluna. O driver retornará uma cadeia de caracteres vazia para uma coluna que não tem um nome.|  
|DATA_TYPE (ODBC 1.0)|3|Smallint não NULL|Tipo de dados SQL. Isso pode ser um tipo de dados SQL ODBC ou um tipo de dados SQL específica do driver. Para obter uma lista dos tipos de dados SQL ODBC válidos, consulte [tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md). Para obter informações sobre tipos de dados SQL específico do driver, consulte a documentação do driver.|  
|TYPE_NAME (ODBC 1.0)|4|Varchar não nulo|Nome do tipo de dados dependente da fonte de dados; Por exemplo, "CHAR", "VARCHAR", "Dinheiro", "VARBINARY longo" ou "CHAR () para dados BIT".|  
|COLUMN_SIZE (ODBC 1.0)|5|Integer|O tamanho da coluna na fonte de dados. Para obter mais informações sobre o tamanho da coluna, consulte [tamanho da coluna, dígitos decimais, o comprimento do octeto de transferência e o tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).|  
|BUFFER_LENGTH (ODBC 1.0)|6|Integer|O comprimento em bytes dos dados transferidos em uma **SQLGetData** ou **SQLFetch** operação se SQL_C_DEFAULT for especificado. Para dados numéricos, esse tamanho pode ser diferente do que o tamanho dos dados armazenados na fonte de dados. Esse valor é o mesmo que a coluna COLUMN_SIZE para caracteres ou dados binários. Para obter mais informações, consulte [tamanho da coluna, dígitos decimais, o comprimento do octeto de transferência e o tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).|  
|DECIMAL_DIGITS (ODBC 1.0)|7|Smallint|Os dígitos decimais da coluna na fonte de dados. NULL é retornado para os tipos de dados em que os dígitos decimais não são aplicáveis. Para obter mais informações sobre os dígitos decimais, consulte [tamanho da coluna, dígitos decimais, o comprimento do octeto de transferência e o tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).|  
|PSEUDO_COLUMN (ODBC 2.0)|8|Smallint|Indica se a coluna é uma coluna de pseudo, como Oracle ROWID:<br /><br /> SQL_PC_UNKNOWN SQL_PC_NOT_PSEUDO SQL_PC_PSEUDO **Observação:**  Para interoperabilidade máxima, pseudo colunas devem não ser colocado entre aspas com o caractere de aspas de identificador retornado por **SQLGetInfo**.|  
  
 Depois que o aplicativo recupera os valores para SQL_BEST_ROWID, o aplicativo pode usar esses valores para selecionar novamente essa linha dentro do escopo definido. O **selecionar** é a garantia de instrução para retornar nenhuma linha ou uma linha.  
  
 Se um aplicativo reselects uma linha com base em rowid ou mais colunas e a linha não for encontrada, o aplicativo pode assumir que a linha foi excluída ou as colunas rowid foram modificadas. O oposto não é verdadeiro: mesmo que a rowid não foi alterado, as outras colunas na linha podem ter alterado.  
  
 Colunas retornadas para o tipo de coluna SQL_BEST_ROWID são úteis para aplicativos que precisam para Avançar e voltar dentro de um conjunto de resultados para recuperar os dados mais recentes de um conjunto de linhas. A coluna ou colunas de rowid são garantia de não alterar quando posicionada nessa linha.  
  
 A coluna ou colunas de rowid podem permanecer válidas mesmo quando o cursor não está posicionado na linha; o aplicativo pode determinar isso verificando a coluna de escopo no conjunto de resultados.  
  
 Colunas retornadas para o tipo de coluna SQL_ROWVER são úteis para aplicativos que precisam da capacidade para verificar se as colunas em uma determinada linha foram atualizadas enquanto a linha foi remarcada usando o rowid. Por exemplo, depois que você seleciona novamente uma linha usando o rowid, o aplicativo pode comparar os valores anteriores nas colunas SQL_ROWVER para aqueles apenas buscadas. Se o valor em uma coluna SQL_ROWVER for diferente do valor anterior, o aplicativo pode alertar o usuário que os dados na exibição foi alterado.  
  
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
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
