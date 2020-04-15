---
title: Função Colunas Especiais SQL | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 826630e1d344322268a2f2638310b3a1e182de6d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287166"
---
# <a name="sqlspecialcolumns-function"></a>Função SQLSpecialColumns
**Conformidade**  
 Versão introduzida: ODBC 1.0 Standards Compliance: Open Group  
  
 **Resumo**  
 **SQLSpecialColumns** recupera as seguintes informações sobre colunas dentro de uma tabela especificada:  
  
-   O conjunto ideal de colunas que identifica exclusivamente uma linha na tabela.  
  
-   As colunas que são atualizadas automaticamente quando qualquer valor na linha é atualizada por uma transação.  
  
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
 [Entrada] Alça de declaração.  
  
 *IdentificadorType*  
 [Entrada] Tipo de coluna para retornar. Deve ser um dos seguintes valores:   
  
 SQL_BEST_ROWID: Retorna a coluna ou conjunto ideal de colunas que, ao recuperar valores da coluna ou colunas, permite que qualquer linha na tabela especificada seja identificada exclusivamente. Uma coluna pode ser uma pseudo-coluna especificamente projetada para este fim (como em Oracle ROWID ou Ingres TID) ou a coluna ou colunas de qualquer índice único para a tabela.  
  
 SQL_ROWVER: Retorna a coluna ou colunas na tabela especificada, se houver, que são automaticamente atualizadas pela fonte de dados quando qualquer valor na linha é atualizado por qualquer transação (como em SQLBase ROWID ou Sybase TIMESTAMP).  
  
 *Catalogname*  
 [Entrada] Nome do catálogo para a mesa. Se um driver suporta catálogos para algumas tabelas, mas não para outras, como quando o driver recupera dados de diferentes DBMSs, uma string vazia ("") denota as tabelas que não possuem catálogos. *CatalogName* não pode conter um padrão de pesquisa de seqüência.  
  
 Se o atributo de declaração SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *o CatalogName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *CatalogName* é um argumento comum; é tratado literalmente, e seu caso é significativo. Para obter mais informações, consulte [Argumentos em Funções de Catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Entrada] Comprimento em caracteres de **CatalogName*.  
  
 *Schemaname*  
 [Entrada] Nome do esquema para a mesa. Se um driver suporta esquemas para algumas tabelas, mas não para outras, como quando o driver recupera dados de diferentes DBMSs, uma string vazia ("") denota as tabelas que não possuem esquemas. *SchemaName* não pode conter um padrão de pesquisa de seqüência.  
  
 Se o atributo de declaração SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *O SchemaName* é tratado como um identificador e seu caso não é significativo. Se for SQL_FALSE, *SchemaName* é um argumento comum; é tratado literalmente, e seu caso é significativo.  
  
 *Comprimento de nome2*  
 [Entrada] Comprimento em caracteres de **SchemaName*.  
  
 *Tablename*  
 [Entrada] Nome da mesa. Este argumento não pode ser um ponteiro nulo. *O Nome da* tabela não pode conter um padrão de pesquisa de seqüência.  
  
 Se o atributo de declaração SQL_ATTR_METADATA_ID estiver definido como SQL_TRUE, *O Nome da Tabela* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *TableName* é um argumento comum; é tratado literalmente, e seu caso é significativo.  
  
 *Comprimento de nome3*  
 [Entrada] Comprimento em caracteres de **TableName*.  
  
 *Escopo*  
 [Entrada] Escopo mínimo necessário do rowid. O rowid retornado pode ser de maior alcance. Deve ser uma destas opções:  
  
 SQL_SCOPE_CURROW: O rowid é garantido ser válido apenas enquanto posicionado nessa linha. Uma reseleção posterior usando rowid pode não retornar uma linha se a linha foi atualizada ou excluída por outra transação.  
  
 SQL_SCOPE_TRANSACTION: O rowid é garantido para ser válido durante a duração da transação atual.  
  
 SQL_SCOPE_SESSION: O rowid é garantido como válido durante a sessão (além dos limites da transação).  
  
 *Permite valor nulo*  
 [Entrada] Determina se deve retornar colunas especiais que podem ter um valor NULL. Deve ser uma destas opções:  
  
 SQL_NO_NULLS: Exclua colunas especiais que podem ter valores NULL. Alguns drivers não podem suportar SQL_NO_NULLS, e esses drivers retornarão um conjunto de resultados vazio se SQL_NO_NULLS foi especificado. As inscrições devem ser preparadas para este caso e solicitar SQL_NO_NULLS somente se for absolutamente necessário.  
  
 SQL_NULLABLE: Retorne colunas especiais mesmo que possam ter valores NULL.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLSpecialColumns** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *alça* de controle de *declaração*. A tabela a seguir lista os valores SQLSTATE comumente retornados por **SQLSpecialColumns** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados à qual o driver estava conectado falhou antes da função ser concluída.|  
|24.000|Estado de cursor inválido|Um cursor foi aberto no *StatementHandle*, e **SQLFetch** ou **SQLFetchScroll** foram chamados. Esse erro é devolvido pelo Gerenciador de driver se **o SQLFetch** ou **o SQLFetchScroll** não retornarem SQL_NO_DATA e forem devolvidos pelo driver se **o SQLFetch** ou **o SQLFetchScroll** retornarem SQL_NO_DATA.<br /><br /> Um cursor foi aberto no *StatementHandle,* mas **SQLFetch** ou **SQLFetchScroll** não foram chamados.|  
|40001|Falha na serialização|A transação foi revertida devido a um impasse de recursos com outra transação.|  
|40003|Conclusão de declaração desconhecida|A conexão associada falhou durante a execução desta função, e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e, antes de concluir a execução, **sqlCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **sqlCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um segmento diferente em um aplicativo multithread.|  
|HY009|Uso inválido do ponteiro nulo|O argumento *TableName* era um ponteiro nulo.<br /><br /> O SQL_ATTR_METADATA_ID atributo de declaração foi definido como SQL_TRUE, o argumento *CatalogName* era um ponteiro nulo e o SQL_CATALOG_NAME *InfoType* retorna que os nomes do catálogo são suportados.<br /><br /> (DM) O atributo de declaração SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, e o argumento *SchemaName* foi um ponteiro nulo.|  
|HY010|Erro de seqüência de função|(DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *StatementHandle*. Esta função ainda estava sendo executada quando **SQLSpecialColumns** foi chamado.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foram chamados para o *StatementHandle* e retornaram SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) Uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados para o *StatementHandle* e retornaram SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY090|Comprimento de seqüência ou buffer inválido|(DM) O valor de um dos argumentos de comprimento foi inferior a 0, mas não igual a SQL_NTS.<br /><br /> O valor de um dos argumentos de comprimento excedeu o valor máximo de comprimento para o nome correspondente. O comprimento máximo de cada nome pode ser obtido ligando para **SQLGetInfo** com os valores *do InfoType:* SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN ou SQL_MAX_TABLE_NAME_LEN.|  
|HY097|Tipo de coluna fora do alcance|(DM) Um valor *de identificador* inválidofoi especificado.|  
|HY098|Tipo de escopo fora do alcance|(DM) Um valor *de escopo* inválido foi especificado.|  
|HY099|Tipo anulado fora do alcance|(DM) Um valor *nulo* inválido foi especificado.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|Um catálogo foi especificado e o driver ou fonte de dados não suporta catálogos.<br /><br /> Um esquema foi especificado, e o driver ou fonte de dados não suporta esquemas.<br /><br /> A combinação das configurações atuais dos atributos de declaração SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE não foi suportada pelo driver ou fonte de dados.<br /><br /> O atributo de declaração SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE, e o atributo de declaração SQL_ATTR_CURSOR_TYPE foi definido como um tipo de cursor para o qual o motorista não suporta marcadores.|  
|HYT00|Tempo limite esgotado|O período de tempo de consulta expirou antes que a fonte de dados retornasse o conjunto de resultados solicitado. O período de tempo é definido através **de SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *StatementHandle* não suporta a função.|  
|IM017|A votação é desativada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a votação é desativada.|  
|IM018|**O SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesta alça.|Se a chamada de função anterior na alça retornar SQL_STILL_EXECUTING e se o modo de notificação estiver ativado, o **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 Quando o argumento *IdentifierType* é SQL_BEST_ROWID, **SQLSpecialColumns** retorna a coluna ou colunas que identificam exclusivamente cada linha na tabela. Essas colunas sempre podem ser usadas em uma *cláusula select-list* ou **WHERE.** **SQLColumns**, que é usado para retornar uma variedade de informações nas colunas de uma tabela, não necessariamente retorna as colunas que identificam exclusivamente cada linha, ou colunas que são atualizadas automaticamente quando qualquer valor na linha é atualizado por uma transação. Por exemplo, **SQLColumns** pode não retornar a pseudocoluna ORACLE ROWID. É por isso que **o SQLSpecialColumns** é usado para retornar essas colunas. Para obter mais informações, consulte [Usos de Dados de Catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
> [!NOTE]  
>  Para obter mais informações sobre o uso geral, argumentos e dados retornados das funções do catálogo oDBC, consulte [Funções de Catálogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 Se não houver colunas que identifiquem com exclusividade cada linha na tabela, o **SQLSpecialColumns** reahde um conjunto de linhas sem linhas; uma chamada subseqüente para **SQLFetch** ou **SQLFetchScroll** na declaração retorna SQL_NO_DATA.  
  
 Se os argumentos *IdentificadorType,* *Scope*ou *Nullable* especificarem características que não são suportadas pela fonte de dados, o **SQLSpecialColumns** reahde um conjunto de resultados vazio.  
  
 Se o atributo de declaração SQL_ATTR_METADATA_ID estiver definido como SQL_TRUE, os argumentos *CatalogName*, *SchemaName*e *TableName* serão tratados como identificadores, de modo que não podem ser definidos como um ponteiro nulo em determinadas situações. (Para obter mais informações, consulte [Argumentos em Funções de Catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).)  
  
 **SQLSpecialColumns** retorna os resultados como um conjunto de resultados padrão, ordenado por SCOPE.  
  
 As seguintes colunas foram renomeadas para ODBC *3.x*. As alterações de nome da coluna não afetam a compatibilidade retrógrada porque os aplicativos se ligam por número de coluna.  
  
|Coluna ODBC 2.0|Coluna ODBC *3.x*|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
  
 Para determinar o comprimento real da coluna COLUMN_NAME, um aplicativo pode chamar **SQLGetInfo** com a opção SQL_MAX_COLUMN_NAME_LEN.  
  
 A tabela a seguir lista as colunas no conjunto de resultados. Colunas adicionais além da coluna 8 (PSEUDO_COLUMN) podem ser definidas pelo driver. Um aplicativo deve ter acesso a colunas específicas do driver, contando abaixo do final do conjunto de resultados, em vez de especificar uma posição ordinal explícita. Para obter mais informações, consulte [Dados Retornados por Funções de Catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome da coluna|Número da coluna|Tipo de dados|Comentários|  
|-----------------|-------------------|---------------|--------------|  
|ESCOPO (ODBC 1.0)|1|Smallint|Escopo real do rowid. Contém um dos seguintes valores:<br /><br /> SQL_SCOPE_CURROW SQL_SCOPE_TRANSACTION SQL_SCOPE_SESSION<br /><br /> NULL é devolvido quando *o IdentificadorType* é SQL_ROWVER. Para obter uma descrição de cada valor, consulte a descrição do *Escopo* em "Sintaxe", anteriormente nesta seção.|  
|COLUMN_NAME (ODBC 1.0)|2|Varchar não É NULO|Nome da coluna. O driver retorna uma seqüência vazia para uma coluna que não tem um nome.|  
|DATA_TYPE (ODBC 1.0)|3|Smallint não NULL|Tipo de dados SQL. Isso pode ser um tipo de dados SQL ODBC ou um tipo de dados SQL específico para driver. Para obter uma lista de tipos de dados SQL oDBC válidos, consulte [Tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md). Para obter informações sobre os tipos de dados SQL específicos do driver, consulte a documentação do motorista.|  
|TYPE_NAME (ODBC 1.0)|4|Varchar não É NULO|Nome do tipo de dados dependente da fonte de dados; por exemplo, "CHAR", "VARCHAR", "MONEY", "LONG VARBINARY" ou "CHAR ( ) FOR BIT DATA".|  
|COLUMN_SIZE (ODBC 1.0)|5|Integer|O tamanho da coluna na fonte de dados. Para obter mais informações sobre o tamanho da coluna, consulte [Tamanho da coluna, Dígitos decimais, Comprimento do Octeto de Transferência e Tamanho da Tela](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).|  
|BUFFER_LENGTH (ODBC 1.0)|6|Integer|O comprimento em bytes de dados transferidos em uma operação **SQLGetData** ou **SQLFetch** se SQL_C_DEFAULT for especificado. Para dados numéricos, esse tamanho pode ser diferente do tamanho dos dados armazenados na fonte de dados. Este valor é o mesmo que a coluna COLUMN_SIZE para dados de caracteres ou binários. Para obter mais informações, consulte [Tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho do display](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).|  
|DECIMAL_DIGITS (ODBC 1.0)|7|Smallint|Os dígitos decimais da coluna na fonte de dados. NULL é devolvido para tipos de dados onde os dígitos decimais não são aplicáveis. Para obter mais informações sobre dígitos decimais, consulte [Tamanho da coluna, Dígitos decimais, Comprimento do Octeto de Transferência e Tamanho do Display](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).|  
|PSEUDO_COLUMN (ODBC 2.0)|8|Smallint|Indica se a coluna é uma pseudo-coluna, como Oracle ROWID:<br /><br /> SQL_PC_UNKNOWN SQL_PC_NOT_PSEUDO SQL_PC_PSEUDO **Nota:** Para interoperabilidade máxima, pseudo-colunas não devem ser citadas com o caractere de citação identificador retornado pelo **SQLGetInfo**.|  
  
 Depois que o aplicativo recupera valores para SQL_BEST_ROWID, o aplicativo pode usar esses valores para reselecionar essa linha dentro do escopo definido. A declaração **SELECT** é garantida para retornar sem linhas ou uma linha.  
  
 Se um aplicativo reselecionar uma linha com base na coluna ou colunas rowid e a linha não for encontrada, o aplicativo pode assumir que a linha foi excluída ou as colunas rowid foram modificadas. O contrário não é verdade: mesmo que o rowid não tenha mudado, as outras colunas da linha podem ter mudado.  
  
 As colunas retornadas para o tipo de coluna SQL_BEST_ROWID são úteis para aplicativos que precisam rolar para frente e para trás dentro de um conjunto de resultados para recuperar os dados mais recentes de um conjunto de linhas. A coluna ou colunas do rowid são garantidas para não mudar enquanto posicionado saque nessa linha.  
  
 A coluna ou colunas do rowid pode permanecer válida mesmo quando o cursor não estiver posicionado na linha; o aplicativo pode determinar isso verificando a coluna SCOPE no conjunto de resultados.  
  
 As colunas retornadas para o tipo de coluna SQL_ROWVER são úteis para aplicativos que precisam da capacidade de verificar se alguma coluna em uma determinada linha foi atualizada enquanto a linha foi reselecionada usando o rowid. Por exemplo, depois de reselecionar uma linha usando rowid, o aplicativo pode comparar os valores anteriores nas colunas SQL_ROWVER com as que foram simplesmente buscadas. Se o valor em uma coluna de SQL_ROWVER difere do valor anterior, o aplicativo pode alertar o usuário de que os dados no display foram alterados.  
  
## <a name="code-example"></a>Exemplo de código  
 Para obter um exemplo de código de uma função semelhante, consulte [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Vinculando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelamento do processamento de declarações|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Retornando as colunas em uma tabela ou tabela|[Função SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|Buscar uma única linha ou um bloco de dados em uma direção somente para a frente|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Buscar um bloco de dados ou rolar através de um conjunto de resultados|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Retornando as colunas de uma chave primária|[Função SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
