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
ms.openlocfilehash: 15fa1269b733c9adc938b1880735ae2a4e5db731
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68039559"
---
# <a name="sqlspecialcolumns-function"></a>Função SQLSpecialColumns
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: abrir grupo  
  
 **Resumo**  
 **SQLSpecialColumns** recupera as seguintes informações sobre colunas em uma tabela especificada:  
  
-   O conjunto ideal de colunas que identifica exclusivamente uma linha na tabela.  
  
-   Colunas que são atualizadas automaticamente quando qualquer valor na linha é atualizado por uma transação.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
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
 Entrada Identificador de instrução.  
  
 *Identificadortype*  
 Entrada Tipo de coluna a ser retornado. Deve ser um dos seguintes valores:   
  
 SQL_BEST_ROWID: retorna a coluna ou conjunto de colunas ideal que, recuperando valores da coluna ou das colunas, permite que qualquer linha na tabela especificada seja identificada exclusivamente. Uma coluna pode ser uma pseudo-coluna projetada especificamente para essa finalidade (como no estado da Oracle ou TID de ingresso) ou a coluna ou colunas de qualquer índice exclusivo da tabela.  
  
 SQL_ROWVER: retorna a coluna ou colunas na tabela especificada, se houver, que são atualizadas automaticamente pela fonte de dados quando qualquer valor na linha é atualizado por qualquer transação (como em SQLBase ROWID ou Sybase TIMESTAMP).  
  
 *CatalogName*  
 Entrada Nome do catálogo da tabela. Se um driver oferecer suporte a catálogos para algumas tabelas, mas não para outras, como quando o driver recupera dados de DBMSs diferentes, uma cadeia de caracteres vazia ("") denota as tabelas que não têm catálogos. *CatalogName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *CatalogName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *CatalogName* será um argumento comum; Ele é tratado literalmente e seu caso é significativo. Para obter mais informações, consulte [argumentos em funções de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 Entrada Comprimento em caracteres de **nome_do_catálogo*.  
  
 *SchemaName*  
 Entrada Nome do esquema da tabela. Se um driver oferecer suporte a esquemas para algumas tabelas, mas não para outras, como quando o driver recupera dados de DBMSs diferentes, uma cadeia de caracteres vazia ("") denota as tabelas que não têm esquemas. *SchemaName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *SchemaName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *SchemaName* será um argumento comum; Ele é tratado literalmente e seu caso é significativo.  
  
 *NameLength2*  
 Entrada Comprimento em caracteres de **SchemaName*.  
  
 *TableName*  
 Entrada Nome da tabela. Este argumento não pode ser um ponteiro nulo. *TableName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *TableName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *TableName* é um argumento comum; Ele é tratado literalmente e seu caso é significativo.  
  
 *NameLength3*  
 Entrada Comprimento em caracteres de **TableName*.  
  
 *Escopo*  
 Entrada Escopo mínimo necessário do ROWID. O ROWID retornado pode ser de escopo maior. Deve ser uma destas opções:  
  
 SQL_SCOPE_CURROW: é garantido que o ROWID seja válido somente enquanto estiver posicionado nessa linha. Uma seleção posterior usando ROWID pode não retornar uma linha se a linha foi atualizada ou excluída por outra transação.  
  
 SQL_SCOPE_TRANSACTION: é garantido que o ROWID seja válido pela duração da transação atual.  
  
 SQL_SCOPE_SESSION: é garantido que o ROWID seja válido pela duração da sessão (entre os limites da transação).  
  
 *Nullable*  
 Entrada Determina se as colunas especiais que podem ter um valor nulo devem ser retornadas. Deve ser uma destas opções:  
  
 SQL_NO_NULLS: exclua colunas especiais que podem ter valores nulos. Alguns drivers não podem dar suporte a SQL_NO_NULLS, e esses drivers retornarão um conjunto de resultados vazio se SQL_NO_NULLS tiver sido especificado. Os aplicativos devem estar preparados para esse caso e solicitar SQL_NO_NULLS somente se for absolutamente necessário.  
  
 SQL_NULLABLE: retornar colunas especiais, mesmo que elas possam ter valores nulos.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLSpecialColumns** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *identificador* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLSpecialColumns** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|DESCRIÇÃO|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado falhou antes da função concluir o processamento.|  
|24.000|Estado de cursor inválido|Um cursor estava aberto no *StatementHandle*e **SQLFetch** ou **SQLFetchScroll** foi chamado. Esse erro será retornado pelo Gerenciador de driver se **SQLFetch** ou **SQLFetchScroll** não tiver retornado SQL_NO_DATA e for retornado pelo driver se **SQLFetch** ou **SQLFetchScroll** tiver retornado SQL_NO_DATA.<br /><br /> Um cursor estava aberto no *StatementHandle*, mas **SQLFetch** ou **SQLFetchScroll** não tinha sido chamado.|  
|40001|Falha de serialização|A transação foi revertida devido a um deadlock de recurso com outra transação.|  
|40003|Conclusão de instrução desconhecida|A conexão associada falhou durante a execução dessa função, e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \*MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativo multithread.|  
|HY009|Uso inválido de ponteiro nulo|O argumento *TableName* era um ponteiro nulo.<br /><br /> O atributo da instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, o argumento *CatalogName* era um ponteiro nulo e o SQL_CATALOG_NAME *InfoType* retorna que os nomes de catálogo têm suporte.<br /><br /> (DM) o atributo de instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, e o argumento *SchemaName* era um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *StatementHandle*. Esta função ainda estava em execução quando **SQLSpecialColumns** foi chamado.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para *StatementHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado para o *StatementHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|(DM) o valor de um dos argumentos de comprimento era menor que 0, mas diferente de SQL_NTS.<br /><br /> O valor de um dos argumentos de comprimento excedeu o valor de comprimento máximo para o nome correspondente. O comprimento máximo de cada nome pode ser obtido chamando **SQLGetInfo** com os valores *infotype* : SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN ou SQL_MAX_TABLE_NAME_LEN.|  
|HY097|Tipo de coluna fora do intervalo|(DM) um valor *identificadortype* inválido foi especificado.|  
|HY098|Tipo de escopo fora do intervalo|(DM) foi especificado um valor de *escopo* inválido.|  
|HY099|Tipo anulável fora do intervalo|(DM) um valor *anulável* inválido foi especificado.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|Um catálogo foi especificado e o driver ou a fonte de dados não oferece suporte a catálogos.<br /><br /> Um esquema foi especificado e o driver ou a fonte de dados não oferece suporte a esquemas.<br /><br /> A combinação das configurações atuais dos atributos de instrução SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE não era suportada pelo driver ou pela fonte de dados.<br /><br /> O atributo de instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE e o atributo de instrução SQL_ATTR_CURSOR_TYPE foi definido como um tipo de cursor para o qual o driver não dá suporte a indicadores.|  
|HYT00|Tempo limite esgotado|O período de tempo limite da consulta expirou antes que a fonte de dados retornasse o conjunto de resultados solicitado. O período de tempo limite é definido por meio de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *StatementHandle* não oferece suporte à função.|  
|IM017|A sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação for usado, a sondagem será desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesse identificador.|Se a chamada de função anterior no identificador retornar SQL_STILL_EXECUTING e se o modo de notificação estiver habilitado, **SQLCompleteAsync** deverá ser chamado na alça para executar o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 Quando o argumento *IdentifierType* é SQL_BEST_ROWID, **SQLSpecialColumns** retorna a coluna ou colunas que identificam exclusivamente cada linha na tabela. Essas colunas sempre podem ser usadas em uma cláusula *Select-List* ou **Where** . **SQLColumns**, que é usada para retornar uma variedade de informações sobre as colunas de uma tabela, não retorna necessariamente as colunas que identificam exclusivamente cada linha ou colunas que são atualizadas automaticamente quando qualquer valor na linha é atualizado por uma transação. Por exemplo, **SQLColumns** pode não retornar o ROWID da pseudo coluna Oracle. É por isso que **SQLSpecialColumns** é usado para retornar essas colunas. Para obter mais informações, consulte [usos de dados do catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
> [!NOTE]  
>  Para obter mais informações sobre o uso geral, argumentos e dados retornados de funções de catálogo ODBC, consulte [Catalog Functions](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 Se não houver nenhuma coluna que identifique exclusivamente cada linha na tabela, **SQLSpecialColumns** retornará um conjunto de linhas sem linhas; uma chamada subsequente para **SQLFetch** ou **SQLFetchScroll** na instrução retorna SQL_NO_DATA.  
  
 Se o *identificadortype*, o *escopo*ou os argumentos *anuláveis* especificarem características que não são suportadas pela fonte de dados, **SQLSpecialColumns** retornará um conjunto de resultados vazio.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, os argumentos *CatalogName*, *schemas*e *TableName* serão tratados como identificadores, para que não possam ser definidos como um ponteiro nulo em determinadas situações. (Para obter mais informações, consulte [argumentos em funções de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).)  
  
 **SQLSpecialColumns** retorna os resultados como um conjunto de resultados padrão, ordenado por escopo.  
  
 As colunas a seguir foram renomeadas para ODBC *3. x*. As alterações de nome de coluna não afetam a compatibilidade com versões anteriores porque os aplicativos são associados por número de coluna.  
  
|Coluna ODBC 2,0|Coluna ODBC *3. x*|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
  
 Para determinar o comprimento real da coluna COLUMN_NAME, um aplicativo pode chamar **SQLGetInfo** com a opção SQL_MAX_COLUMN_NAME_LEN.  
  
 A tabela a seguir lista as colunas no conjunto de resultados. Colunas adicionais além da coluna 8 (PSEUDO_COLUMN) podem ser definidas pelo driver. Um aplicativo deve obter acesso a colunas específicas do driver, contando a partir do final do conjunto de resultados em vez de especificar uma posição ordinal explícita. Para obter mais informações, consulte [dados retornados por funções de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome da coluna|Número da coluna|Tipo de dados|Comentários|  
|-----------------|-------------------|---------------|--------------|  
|ESCOPO (ODBC 1,0)|1|Smallint|Escopo real do ROWID. Contém um dos seguintes valores:<br /><br /> SQL_SCOPE_CURROW SQL_SCOPE_TRANSACTION SQL_SCOPE_SESSION<br /><br /> NULL é retornado quando *IdentifierType* é SQL_ROWVER. Para obter uma descrição de cada valor, consulte a descrição do *escopo* em "sintaxe", anteriormente nesta seção.|  
|COLUMN_NAME (ODBC 1,0)|2|Varchar não nulo|Nome da coluna. O driver retorna uma cadeia de caracteres vazia para uma coluna que não tem um nome.|  
|DATA_TYPE (ODBC 1,0)|3|Smallint não NULL|Tipo de dados SQL. Pode ser um tipo de dados ODBC do SQL ou um tipo de dados SQL específico do driver. Para obter uma lista de tipos de dados SQL ODBC válidos, consulte [tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md). Para obter informações sobre tipos de dados do SQL específicos do driver, consulte a documentação do driver.|  
|TYPE_NAME (ODBC 1,0)|4|Varchar não nulo|Nome do tipo de dados dependente de fonte de dados; por exemplo, "CHAR", "VARCHAR", "MONEY", "LONG VARBINARY" ou "CHAR () para dados de BIT".|  
|COLUMN_SIZE (ODBC 1,0)|5|Integer|O tamanho da coluna na fonte de dados. Para obter mais informações sobre o tamanho da coluna, consulte [tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).|  
|BUFFER_LENGTH (ODBC 1,0)|6|Integer|O comprimento em bytes de dados transferidos em uma operação **SQLGetData** ou **sqlfetch** se SQL_C_DEFAULT for especificado. Para dados numéricos, esse tamanho pode ser diferente do tamanho dos dados armazenados na fonte de dados. Esse valor é o mesmo que a coluna de COLUMN_SIZE para dados de caracteres ou binários. Para obter mais informações, consulte [tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).|  
|DECIMAL_DIGITS (ODBC 1,0)|7|Smallint|Os dígitos decimais da coluna na fonte de dados. NULL é retornado para os tipos de dados em que os dígitos decimais não são aplicáveis. Para obter mais informações sobre dígitos decimais, consulte [tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).|  
|PSEUDO_COLUMN (ODBC 2,0)|8|Smallint|Indica se a coluna é uma pseudo coluna, como um ROWID Oracle:<br /><br /> SQL_PC_UNKNOWN SQL_PC_NOT_PSEUDO SQL_PC_PSEUDO **Observação:** para obter a interoperabilidade máxima, as pseudovariáveis não devem ser citadas com o caractere de aspas do identificador retornado por **SQLGetInfo**.|  
  
 Depois que o aplicativo recupera valores para SQL_BEST_ROWID, o aplicativo pode usar esses valores para selecionar novamente essa linha dentro do escopo definido. A instrução **Select** é garantida para retornar não linhas ou uma linha.  
  
 Se um aplicativo selecionar novamente uma linha com base na coluna ou colunas de ROWID e a linha não for encontrada, o aplicativo poderá assumir que a linha foi excluída ou que as colunas de ROWID foram modificadas. O oposto não é verdadeiro: mesmo que ROWID não tenha sido alterado, as outras colunas na linha podem ter sido alteradas.  
  
 As colunas retornadas para o tipo de coluna SQL_BEST_ROWID são úteis para aplicativos que precisam rolar para frente e para trás dentro de um conjunto de resultados para recuperar os dados mais recentes de um conjunto de linhas. A coluna ou colunas do ROWID têm garantia de que não serão alteradas enquanto estiverem posicionadas nessa linha.  
  
 A coluna ou colunas do ROWID podem permanecer válidas mesmo quando o cursor não estiver posicionado na linha; o aplicativo pode determinar isso verificando a coluna de escopo no conjunto de resultados.  
  
 As colunas retornadas para o tipo de coluna SQL_ROWVER são úteis para aplicativos que precisam da capacidade de verificar se alguma coluna em uma determinada linha foi atualizada enquanto a linha foi reselecionada usando o ROWID. Por exemplo, depois de selecionar novamente uma linha usando ROWID, o aplicativo pode comparar os valores anteriores nas colunas SQL_ROWVER àquelas que acabamos de buscar. Se o valor em uma coluna de SQL_ROWVER diferir do valor anterior, o aplicativo poderá alertar o usuário de que os dados na exibição foram alterados.  
  
## <a name="code-example"></a>Exemplo de código  
 Para obter um exemplo de código de uma função semelhante, consulte [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Associando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Retornando as colunas em uma tabela ou tabelas|[Função SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|Buscando uma única linha ou um bloco de dados em uma direção somente de avanço|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Buscando um bloco de dados ou rolando por meio de um conjunto de resultados|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Retornando as colunas de uma chave primária|[Função SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
