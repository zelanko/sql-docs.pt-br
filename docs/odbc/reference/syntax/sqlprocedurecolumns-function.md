---
title: Função SQLProcedureColumns | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLProcedureColumns
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLProcedureColumns
helpviewer_keywords:
- SQLProcedureColumns function [ODBC]
ms.assetid: 4ca37b28-a6df-465b-8988-d422d37fc025
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3d81e44b116ed6f26319d31430999a61a8a17f21
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306847"
---
# <a name="sqlprocedurecolumns-function"></a>Função SQLProcedureColumns
**Conformidade**  
 Versão introduzida: ODBC 1.0 Normas Conformidade: ODBC  
  
 **Resumo**  
 **SQLProcedureColunas** retorna a lista de parâmetros de entrada e saída, bem como as colunas que compõem o conjunto de resultados para os procedimentos especificados. O motorista retorna as informações como resultado definido na declaração especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
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
 [Entrada] Alça de declaração.  
  
 *Catalogname*  
 [Entrada] Nome do catálogo do procedimento. Se um motorista suporta catálogos para alguns procedimentos, mas não para outros, como quando o motorista recupera dados de diferentes DBMSs, uma string vazia ("") denota os procedimentos que não possuem catálogos. *CatalogName* não pode conter um padrão de pesquisa de seqüência.  
  
 Se o atributo de declaração SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *o CatalogName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *CatalogName* é um argumento comum; é tratado literalmente, e seu caso é significativo. Para obter mais informações, consulte [Argumentos em Funções de Catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Entrada] Comprimento em caracteres de **CatalogName*.  
  
 *Schemaname*  
 [Entrada] Padrão de pesquisa de cordas para nomes de esquema de procedimento. Se um motorista suporta esquemas para alguns procedimentos, mas não para outros, como quando o motorista recupera dados de diferentes DBMSs, uma corda vazia ("") denota os procedimentos que não possuem esquemas.  
  
 Se o atributo de declaração SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *O SchemaName* é tratado como um identificador e seu caso não é significativo. Se for SQL_FALSE, *SchemaName* é um argumento de valor padrão; é tratado literalmente, e seu caso é significativo.  
  
 *Comprimento de nome2*  
 [Entrada] Comprimento em caracteres de **SchemaName*.  
  
 *Procname*  
 [Entrada] Padrão de pesquisa de cordas para nomes de procedimentos.  
  
 Se o atributo de declaração SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *ProcName* será tratado como um identificador e seu caso não é significativo. Se for SQL_FALSE, *ProcName* é um argumento de valor padrão; é tratado literalmente, e seu caso é significativo.  
  
 *Comprimento de nome3*  
 [Entrada] Comprimento em caracteres de **ProcName*.  
  
 *ColumnName*  
 [Entrada] Padrão de pesquisa de cordas para nomes de colunas.  
  
 Se o atributo de declaração SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *O Nome da Coluna* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *ColumnName* é um argumento de valor padrão; é tratado literalmente, e seu caso é significativo.  
  
 *Comprimento de nome4*  
 [Entrada] Comprimento em caracteres de **ColumnName*.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLProcedureColumns** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *alça* de *statementHandle*. A tabela a seguir lista os valores SQLSTATE comumente retornados por **SQLProcedureColumns** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados à qual o driver estava conectado falhou antes da função ser concluída.|  
|24.000|Estado de cursor inválido|Um cursor foi aberto no *StatementHandle*, e **SQLFetch** ou **SQLFetchScroll** foram chamados. Esse erro é devolvido pelo Gerenciador de driver se **o SQLFetch** ou **o SQLFetchScroll** não retornarem SQL_NO_DATA e forem devolvidos pelo driver se **o SQLFetch** ou **o SQLFetchScroll** retornarem SQL_NO_DATA.<br /><br /> Um cursor foi aberto no *StatementHandle,* mas **SQLFetch** ou **SQLFetchScroll** não foram chamados.|  
|40001|Falha na serialização|A transação foi revertida devido a um impasse de recursos com outra transação.|  
|40003|Conclusão de declaração desconhecida|A conexão associada falhou durante a execução desta função, e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada por **SQLError** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e, antes de concluir a execução, **sqlCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **sqlCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um segmento diferente em um aplicativo multithread.|  
|HY009|Uso inválido do ponteiro nulo|O SQL_ATTR_METADATA_ID atributo de declaração foi definido como SQL_TRUE, o argumento *CatalogName* era um ponteiro nulo e o SQL_CATALOG_NAME *InfoType* retorna que os nomes do catálogo são suportados.<br /><br /> (DM) O atributo de declaração SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, e o argumento *SchemaName,* *ProcName*ou *ColumnName* era um ponteiro nulo.|  
|HY010|Erro de seqüência de função|(DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *StatementHandle*. Esta função aynscrona ainda estava sendo executada quando a função SQLProcedureColumns foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foram chamados para o *StatementHandle* e retornaram SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) Uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados para o *StatementHandle* e retornaram SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.|  
|HY090|Comprimento de seqüência ou buffer inválido|(DM) O valor de um dos argumentos de comprimento do nome foi inferior a 0, mas não igual a SQL_NTS.<br /><br /> O valor de um dos argumentos de comprimento do nome excedeu o valor máximo de comprimento para o catálogo correspondente, esquema, procedimento ou nome da coluna.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|Um catálogo de procedimentos foi especificado e o driver ou fonte de dados não suporta catálogos.<br /><br /> Um esquema de procedimento foi especificado, e o driver ou fonte de dados não suporta esquemas.<br /><br /> Um padrão de pesquisa de seqüência foi especificado para o esquema de procedimento, nome do procedimento ou nome da coluna, e a fonte de dados não suporta padrões de pesquisa para um ou mais desses argumentos.<br /><br /> A combinação das configurações atuais dos atributos de declaração SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE não foi suportada pelo driver ou fonte de dados.<br /><br /> O atributo de declaração SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE, e o atributo de declaração SQL_ATTR_CURSOR_TYPE foi definido como um tipo de cursor para o qual o motorista não suporta marcadores.|  
|HYT00|Tempo limite esgotado|O período de tempo expirou antes que a fonte de dados retornasse o conjunto de resultados. O período de tempo é definido através **de SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *StatementHandle* não suporta a função.|  
|IM017|A votação é desativada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a votação é desativada.|  
|IM018|**O SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesta alça.|Se a chamada de função anterior na alça retornar SQL_STILL_EXECUTING e se o modo de notificação estiver ativado, o **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 Esta função é normalmente usada antes da execução da declaração para recuperar informações sobre parâmetros do procedimento e as colunas que compõem o conjunto de resultados ou conjuntos retornados pelo procedimento, se houver. Para obter mais informações, consulte [Procedimentos](../../../odbc/reference/develop-app/procedures-odbc.md).  
  
> [!NOTE]  
>  **SQLProcedureColunas** podem não retornar todas as colunas usadas por um procedimento. Por exemplo, um driver pode retornar apenas informações sobre os parâmetros usados por um procedimento e não as colunas em um conjunto de resultados que gera.  
  
 Os argumentos *SchemaName,* *ProcName*e *ColumnName* aceitam padrões de pesquisa. Para obter mais informações sobre padrões de pesquisa [válidos,](../../../odbc/reference/develop-app/pattern-value-arguments.md)consulte Argumentos de valor de padrão .  
  
> [!NOTE]  
>  Para obter mais informações sobre o uso geral, argumentos e dados retornados das funções do catálogo oDBC, consulte [Funções de Catálogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 **SQLProcedureColumns** retorna os resultados como um conjunto de resultados padrão, ordenado por PROCEDURE_CAT, PROCEDURE_SCHEM, PROCEDURE_NAME e COLUMN_TYPE. Os nomes da coluna são devolvidos para cada procedimento na seguinte ordem: o nome do valor de devolução, os nomes de cada parâmetro na invocação do procedimento (na ordem de chamada) e, em seguida, os nomes de cada coluna no conjunto de resultados retornado pelo procedimento (em ordem de coluna).  
  
 Os aplicativos devem vincular colunas específicas do driver em relação ao final do conjunto de resultados. Para obter mais informações, consulte [Dados Retornados por Funções de Catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
 Para determinar os comprimentos reais das colunas de PROCEDURE_CAT, PROCEDURE_SCHEM, PROCEDURE_NAME e COLUMN_NAME, um aplicativo pode chamar **sqlGetInfo** com as opções de SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_PROCEDURE_NAME_LEN e SQL_MAX_COLUMN_NAME_LEN.  
  
 As seguintes colunas foram renomeadas para ODBC 3. *x*. As alterações de nome da coluna não afetam a compatibilidade retrógrada porque os aplicativos se ligam por número de coluna.  
  
|Coluna ODBC 2.0|ODBC 3. *x* coluna|  
|---------------------|-----------------------|  
|PROCEDURE_QUALIFIER|PROCEDURE_CAT|  
|PROCEDIMENTO _OWNER|PROCEDURE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 As seguintes colunas foram adicionadas ao conjunto de resultados retornado por **SQLProcedureColumns** para ODBC 3. *x:*  
  
-   COLUMN_DEF  
  
-   DATETIME_CODE  
  
-   CHAR_OCTET_LENGTH  
  
-   ORDINAL_POSITION  
  
-   IS_NULLABLE  
  
 A tabela a seguir lista as colunas no conjunto de resultados. Colunas adicionais além da coluna 19 (IS_NULLABLE) podem ser definidas pelo driver. Um aplicativo deve ter acesso a colunas específicas do driver, contando abaixo do final do conjunto de resultados, em vez de especificar uma posição ordinal explícita. Para obter mais informações, consulte [Dados Retornados por Funções de Catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome da coluna|Número da coluna|Tipo de dados|Comentários|  
|-----------------|-------------------|---------------|--------------|  
|PROCEDURE_CAT (ODBC 2.0)|1|Varchar|Nome do catálogo do procedimento; NULL se não aplicável à fonte de dados. Se um motorista suporta catálogos para alguns procedimentos, mas não para outros, como quando o motorista recupera dados de diferentes DBMSs, ele retorna uma string vazia (""" para aqueles procedimentos que não possuem catálogos.|  
|PROCEDURE_SCHEM (ODBC 2.0)|2|Varchar|Nome do esquema do procedimento; NULL se não aplicável à fonte de dados. Se um motorista suporta esquemas para alguns procedimentos, mas não para outros, como quando o motorista recupera dados de diferentes DBMSs, ele retorna uma corda vazia (""" para aqueles procedimentos que não possuem esquemas.|  
|PROCEDURE_NAME (ODBC 2.0)|3|Varchar não É NULO|Nome do procedimento. Uma seqüência vazia é devolvida para um procedimento que não tem um nome.|  
|COLUMN_NAME (ODBC 2.0)|4|Varchar não É NULO|Nome da coluna de procedimento. O driver retorna uma seqüência vazia para uma coluna de procedimento que não tem um nome.|  
|COLUMN_TYPE (ODBC 2.0)|5|Smallint não NULL|Define a coluna de procedimento como um parâmetro ou uma coluna de conjunto de resultados:<br /><br /> SQL_PARAM_TYPE_UNKNOWN: A coluna de procedimento é um parâmetro cujo tipo é desconhecido. (ODBC 1.0)<br /><br /> SQL_PARAM_INPUT: A coluna de procedimento é um parâmetro de entrada. (ODBC 1.0)<br /><br /> SQL_PARAM_INPUT_OUTPUT: A coluna de procedimento é um parâmetro de entrada/saída. (ODBC 1.0)<br /><br /> SQL_PARAM_OUTPUT: A coluna de procedimento é um parâmetro de saída. (ODBC 2.0)<br /><br /> SQL_RETURN_VALUE: A coluna de procedimento é o valor de retorno do procedimento. (ODBC 2.0)<br /><br /> SQL_RESULT_COL: A coluna de procedimentos é uma coluna de conjunto de resultados. (ODBC 1.0)|  
|DATA_TYPE (ODBC 2.0)|6|Smallint não NULL|Tipo de dados SQL. Isso pode ser um tipo de dados SQL ODBC ou um tipo de dados SQL específico para driver. Para os tipos de dados de data e intervalo, esta coluna retorna os tipos de dados concisos (por exemplo, SQL_TYPE_TIME ou SQL_INTERVAL_YEAR_TO_MONTH). Para obter uma lista de tipos de dados SQL odbc válidos, consulte [Tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md) no apêndice D: Tipos de dados. Para obter informações sobre os tipos de dados SQL específicos do driver, consulte a documentação do motorista.|  
|TYPE_NAME (ODBC 2.0)|7|Varchar não É NULO|Nome do tipo de dados dependente da fonte de dados; por exemplo, "CHAR", "VARCHAR", "MONEY", "LONG VARBINARY" ou "CHAR ( ) FOR BIT DATA".|  
|COLUMN_SIZE (ODBC 2.0)|8|Integer|O tamanho da coluna de procedimento na fonte de dados. NULL é devolvido para tipos de dados onde o tamanho da coluna não é aplicável. Para obter mais informações sobre precisão, consulte [Tamanho da coluna, Dígitos decimais, Comprimento do Octeto de Transferência e Tamanho do Display](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice D: Tipos de dados.|  
|BUFFER_LENGTH (ODBC 2.0)|9|Integer|O comprimento em bytes de dados transferidos em uma operação **SQLGetData** ou **SQLFetch** se SQL_C_DEFAULT for especificado. Para dados numéricos, esse tamanho pode ser diferente do tamanho dos dados armazenados na fonte de dados. Para obter mais informações, consulte [Tamanho da coluna, Dígitos Decimais, Comprimento do Octeto de Transferência e Tamanho do Display,](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)no apêndice D: Tipos de dados.|  
|DECIMAL_DIGITS (ODBC 2.0)|10|Smallint|Os dígitos decimais da coluna de procedimento na fonte de dados. NULL é devolvido para tipos de dados onde dígitos decimais não são aplicáveis. Para obter mais informações sobre dígitos decimais, consulte Tamanho da [coluna, Dígitos Decimais, Comprimento do Octeto de Transferência e Tamanho do Display,](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)no apêndice D: Tipos de dados.|  
|NUM_PREC_RADIX (ODBC 2.0)|11|Smallint|Para tipos de dados numéricos, 10 ou 2.<br /><br /> Se 10, os valores em COLUMN_SIZE e DECIMAL_DIGITS dar o número de dígitos decimais permitidos para a coluna. Por exemplo, uma coluna DECIMAL (12,5) retornaria um NUM_PREC_RADIX de 10, um COLUMN_SIZE de 12 e um DECIMAL_DIGITS de 5; uma coluna FLOAT poderia retornar um NUM_PREC_RADIX de 10, um COLUMN_SIZE de 15, e um DECIMAL_DIGITS de NULL.<br /><br /> Se 2, os valores em COLUMN_SIZE e DECIMAL_DIGITS dar o número de bits permitidos na coluna. Por exemplo, uma coluna FLOAT poderia retornar uma NUM_PREC_RADIX de 2, uma COLUMN_SIZE de 53 e uma DECIMAL_DIGITS de NULL.<br /><br /> NULL é devolvido para tipos de dados quando NUM_PREC_RADIX não é aplicável.|  
|ANULADO (ODBC 2.0)|12|Smallint não NULL|Se a coluna de procedimento aceita um valor NULL:<br /><br /> SQL_NO_NULLS: A coluna procedimento não aceita valores NULAS.<br /><br /> SQL_NULLABLE: A coluna de procedimentos aceita valores NULAS.<br /><br /> SQL_NULLABLE_UNKNOWN: Não se sabe se a coluna de procedimento aceita valores NULOS.|  
|OBSERVAÇÕES (ODBC 2.0)|13|Varchar|Uma descrição da coluna de procedimentos.|  
|COLUMN_DEF (ODBC 3.0)|14|Varchar|O valor padrão da coluna.<br /><br /> Se NULL foi especificado como o valor padrão, esta coluna será a palavra NULL, não incluída entre aspas. Se o valor padrão não puder ser representado sem truncação, esta coluna contém TRUNCATED, sem que aspas únicas sejam anexadas. Se nenhum valor padrão foi especificado, esta coluna será NULL.<br /><br /> O valor de COLUMN_DEF pode ser usado na geração de uma nova definição de coluna, exceto quando contém o valor TRUNCATED.|  
|SQL_DATA_TYPE (ODBC 3.0)|15|Smallint não NULL|O valor do tipo de dados SQL como ele aparece no campo SQL_DESC_TYPE do descritor. Esta coluna é a mesma da coluna DATA_TYPE, exceto para os tipos de dados de data e intervalo.<br /><br /> Para os tipos de dados de data e intervalo, o campo de SQL_DATA_TYPE no conjunto de resultados retornará SQL_INTERVAL ou SQL_DATETIME, e o campo SQL_DATETIME_SUB retornará o subcódigo para o tipo de dados de intervalo ou data específica. (Veja [o apêndice D: Tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).)|  
|SQL_DATETIME_SUB (ODBC 3.0)|16|Smallint|O código de subtipo para os tipos de dados de data e intervalo. Para outros tipos de dados, esta coluna retorna um NULL.|  
|CHAR_OCTET_LENGTH (ODBC 3.0)|17|Integer|O comprimento máximo em bytes de uma coluna de tipo de dados de caracteres ou binários. Para todos os outros tipos de dados, esta coluna retorna um NULL.|  
|ORDINAL_POSITION (ODBC 3.0)|18|Integer não NULL|Para parâmetros de entrada e saída, a posição ordinal do parâmetro na definição do procedimento (na ordem de parâmetro sumido, a partir de 1). Para um valor de retorno (se houver), 0 é devolvido. Para colunas definidas em resultados, a posição ordinal da coluna no conjunto de resultados, com a primeira coluna no conjunto de resultados sendo o número 1. Se houver vários conjuntos de resultados, as posições ordinárias da coluna serão devolvidas de forma específica ao driver.|  
|IS_NULLABLE (ODBC 3.0)|19|Varchar|"NÃO" se a coluna não incluir NULLs.<br /><br /> "SIM" se a coluna puder incluir NULLs.<br /><br /> Esta coluna retorna uma cadeia de caracteres de comprimento zero se a possibilidade de nulidade for desconhecida.<br /><br /> As regras ISO são seguidas para determinar a possibilidade de nulidade. Um DBMS em conformidade com ISO SQL não pode retornar uma cadeia de caracteres vazia.<br /><br /> O valor retornado para esta coluna é diferente do valor retornado para a coluna NULLABLE. (Veja a descrição da coluna NULLABLE.)|  
  
## <a name="code-example"></a>Exemplo de código  
 Consulte [Chamadas de procedimento](../../../odbc/reference/develop-app/procedure-calls.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Vinculando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelamento do processamento de declarações|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Buscar uma única linha ou um bloco de dados em uma direção somente para a frente|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Buscar um bloco de dados ou rolar através de um conjunto de resultados|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Retornando uma lista de procedimentos em uma fonte de dados|[Função SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
