---
title: Função SQLGetTypeInfo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetTypeInfo
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetTypeInfo
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC]
ms.assetid: bdedb044-8924-4ca4-85f3-8b37578e0257
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 47273c75a005f11b33e9929977b57607b36898de
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303257"
---
# <a name="sqlgettypeinfo-function"></a>Função SQLGetTypeInfo
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: ISO 92  
  
 **Resumo**  
 **SQLGetTypeInfo** retorna informações sobre os tipos de dados com suporte pela fonte de dados. O driver retorna as informações na forma de um conjunto de resultados SQL. Os tipos de dados destinam-se ao uso em instruções DDL (linguagem de definição de dados).  
  
> [!IMPORTANT]  
>  Os aplicativos devem usar os nomes de tipos retornados na coluna TYPE_NAME do conjunto de resultados **SQLGetTypeInfo** nas instruções **ALTER TABLE** e **CREATE TABLE** . **SQLGetTypeInfo** pode retornar mais de uma linha com o mesmo valor na coluna DATA_TYPE.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLGetTypeInfo(  
     SQLHSTMT      StatementHandle,  
     SQLSMALLINT   DataType);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 Entrada Identificador de instrução para o conjunto de resultados.  
  
 *DataType*  
 Entrada O tipo de dados SQL. Isso deve ser um dos valores na seção [tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md) do Apêndice D: tipos de dados ou um tipo de dados SQL específico de driver. SQL_ALL_TYPES especifica que as informações sobre todos os tipos de dados devem ser retornadas.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLGetTypeInfo** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *identificador* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLGetTypeInfo** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01S02|Valor da opção alterado|Um atributo de instrução especificado era inválido devido a condições de trabalho de implementação; portanto, um valor semelhante foi substituído temporariamente. (Chame **SQLGetStmtAttr** para determinar o valor substituído temporariamente.) O valor de substituição é válido para o *StatementHandle* até que o cursor seja fechado. Os atributos de instrução que podem ser alterados são: SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_KEYSET_SIZE, SQL_ATTR_MAX_LENGTH, SQL_ATTR_MAX_ROWS, SQL_ATTR_QUERY_TIMEOUT e SQL_ATTR_SIMULATE_CURSOR. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado falhou antes da função concluir o processamento.|  
|24.000|Estado de cursor inválido|Um cursor estava aberto no *StatementHandle* e **SQLFetch** ou **SQLFetchScroll** foi chamado. Esse erro será retornado pelo Gerenciador de driver se **SQLFetch** ou **SQLFetchScroll** não tiver retornado SQL_NO_DATA e será retornado pelo driver se **SQLFetch** ou **SQLFetchScroll** tiver retornado SQL_NO_DATA.<br /><br /> Um conjunto de resultados foi aberto no *StatementHandle*, mas **SQLFetch** ou **SQLFetchScroll** não tinha sido chamado.|  
|40001|Falha de serialização|A transação foi revertida devido a um deadlock de recurso com outra transação.|  
|40003|Conclusão de instrução desconhecida|A conexão associada falhou durante a execução dessa função e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \*MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY004|Tipo de dados SQL inválido|O valor especificado para o argumento *DataType* não era um identificador de tipo de dados SQL ODBC válido nem um identificador de tipo de dados específico de driver com suporte no driver.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*, então a função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativo multithread.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *StatementHandle*. Esta função assíncrona ainda estava em execução quando a função **SQLGetTypeInfo** foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para *StatementHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado para o *StatementHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|A combinação das configurações atuais dos atributos de instrução SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE não era suportada pelo driver ou pela fonte de dados.<br /><br /> O atributo de instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE e o atributo de instrução SQL_ATTR_CURSOR_TYPE foi definido como um tipo de cursor para o qual o driver não dá suporte a indicadores.|  
|HYT00|Tempo limite esgotado|O período de tempo limite da consulta expirou antes que a fonte de dados retornasse o conjunto de resultados. O período de tempo limite é definido por meio de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver correspondente ao *StatementHandle* não oferece suporte à função.|  
|IM017|A sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação for usado, a sondagem será desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesse identificador.|Se a chamada de função anterior no identificador retornar SQL_STILL_EXECUTING e se o modo de notificação estiver habilitado, **SQLCompleteAsync** deverá ser chamado na alça para executar o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 **SQLGetTypeInfo** retorna os resultados como um conjunto de resultados padrão, ordenados por DATA_TYPE e, em seguida, por quão próximo o tipo de dados é mapeado para o tipo de dados SQL ODBC correspondente. Os tipos de dados definidos pela fonte de dados têm precedência sobre os tipos de dados definidos pelo usuário. Consequentemente, a ordem de classificação não é necessariamente consistente, mas pode ser generalizada como DATA_TYPE primeiro, seguido por TYPE_NAME, tanto em ordem crescente. Por exemplo, suponha que uma fonte de dados definia tipos de dados inteiros e contadores, em que o contador é incrementado automaticamente e que um tipo de dados definido pelo usuário WHOLENUM também tenha sido definido. Elas seriam retornadas no número inteiro da ordem, WHOLENUM e COUNTER, porque o WHOLENUM mapeia de acordo com o tipo de dados SQL do ODBC SQL_INTEGER, enquanto o tipo de dados de incremento automático, embora tenha suporte da fonte de dados, não é mapeado de maneira próxima para um tipo de dados ODBC SQL. Para obter informações sobre como essas informações podem ser usadas, consulte [instruções DDL](../../../odbc/reference/develop-app/ddl-statements.md).  
  
 Se o argumento *DataType* especificar um tipo de dados válido para a versão do ODBC com suporte do driver, mas não for suportado pelo driver, ele retornará um conjunto de resultados vazio.  
  
> [!NOTE]  
>  Para obter mais informações sobre o uso geral, argumentos e dados retornados de funções de catálogo ODBC, consulte [Catalog Functions](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 As colunas a seguir foram renomeadas para ODBC 3. *x*. As alterações de nome de coluna não afetam a compatibilidade com versões anteriores porque os aplicativos são associados por número de coluna.  
  
|Coluna ODBC 2,0|ODBC 3. coluna *x*|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|MONEY|FIXED_PREC_SCALE|  
|AUTO_INCREMENT|AUTO_UNIQUE_VALUE|  
  
 As colunas a seguir foram adicionadas ao conjunto de resultados retornado por **SQLGetTypeInfo** para ODBC 3. *x*:  
  
-   SQL_DATA_TYPE  
  
-   INTERVAL_PRECISION  
  
-   SQL_DATETIME_SUB  
  
-   NUM_PREC_RADIX  
  
 A tabela a seguir lista as colunas no conjunto de resultados. Colunas adicionais além da coluna 19 (INTERVAL_PRECISION) podem ser definidas pelo driver. Um aplicativo deve obter acesso a colunas específicas do driver, contando a partir do final do conjunto de resultados em vez de especificar uma posição ordinal explícita. Para obter mais informações, consulte [dados retornados por funções de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
> [!NOTE]  
>  **SQLGetTypeInfo** pode não retornar todos os tipos de dados. Por exemplo, um driver pode não retornar tipos de dados definidos pelo usuário. Os aplicativos podem usar qualquer tipo de dados válido, independentemente de terem sido retornados por **SQLGetTypeInfo**. Os tipos de dados retornados por **SQLGetTypeInfo** são aqueles com suporte na fonte de dados. Eles são destinados ao uso em instruções DDL (linguagem de definição de dados). Os drivers podem retornar dados de conjunto de resultados usando tipos de dados diferentes dos tipos retornados por **SQLGetTypeInfo**. Ao criar o conjunto de resultados para uma função de catálogo, o driver pode usar um tipo de dados que não é suportado pela fonte de dados.  
  
|Nome da coluna|Coluna<br /><br /> número|Tipo de dados|Comentários|  
|-----------------|-----------------------|---------------|--------------|  
|TYPE_NAME (ODBC 2,0)|1|Varchar não nulo|Nome do tipo de dados dependente da fonte de dados; por exemplo, "CHAR ()", "VARCHAR ()", "MONEY", "LONG VARBINARY" ou "CHAR () para dados de BIT". Os aplicativos devem usar esse nome nas instruções **CREATE TABLE** e **ALTER TABLE** .|  
|DATA_TYPE (ODBC 2,0)|2|Smallint não NULL|Tipo de dados SQL. Pode ser um tipo de dados ODBC do SQL ou um tipo de dados SQL específico do driver. Para os tipos de dados DateTime ou Interval, essa coluna retorna o tipo de dados conciso (como SQL_TYPE_TIME ou SQL_INTERVAL_YEAR_TO_MONTH). Para obter uma lista de tipos de dados SQL ODBC válidos, consulte [tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md) no Apêndice D: tipos de dados. Para obter informações sobre tipos de dados do SQL específicos do driver, consulte a documentação do driver.|  
|COLUMN_SIZE (ODBC 2,0)|3|Integer|O tamanho máximo de coluna que o servidor dá suporte para esse tipo de dados. Para dados numéricos, essa é a precisão máxima. Para dados de cadeia de caracteres, esse é o comprimento em caracteres. Para tipos de dados DateTime, esse é o comprimento em caracteres da representação de cadeia de caracteres (supondo a precisão máxima permitida do componente de segundos fracionários). NULL é retornado para os tipos de dados em que o tamanho da coluna não é aplicável. Para tipos de dados de intervalo, esse é o número de caracteres na representação de caractere do literal de intervalo (conforme definido pela precisão à esquerda do intervalo; consulte o [comprimento do tipo de dados de intervalo](../../../odbc/reference/appendixes/interval-data-type-length.md) no Apêndice D: tipos de dados).<br /><br /> Para obter mais informações sobre o tamanho da coluna, consulte [tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice D: tipos de dados.|  
|LITERAL_PREFIX (ODBC 2,0)|4|Varchar|Caractere ou caracteres usados para prefixar um literal; por exemplo, uma aspa simples (') para tipos de dados de caractere ou 0x para tipos de dados binários; NULL é retornado para os tipos de dados em que um prefixo literal não é aplicável.|  
|LITERAL_SUFFIX (ODBC 2,0)|5|Varchar|Caractere ou caracteres usados para encerrar um literal; por exemplo, uma aspa simples (') para tipos de dados de caractere; NULL é retornado para os tipos de dados em que um sufixo literal não é aplicável.|  
|CREATE_PARAMS (ODBC 2,0)|6|Varchar|Uma lista de palavras-chave, separadas por vírgulas, correspondente a cada parâmetro que o aplicativo pode especificar entre parênteses ao usar o nome retornado no campo TYPE_NAME. As palavras-chave na lista podem ser qualquer um dos seguintes: comprimento, precisão ou escala. Eles aparecem na ordem em que a sintaxe exige que sejam usados. Por exemplo, CREATE_PARAMS para DECIMAL seria "precisão, escala"; CREATE_PARAMS para VARCHAR seria igual a "Length". NULL será retornado se não houver parâmetros para a definição de tipo de dados; por exemplo, INTEGER.<br /><br /> O driver fornece o texto de CREATE_PARAMS no idioma do país/região onde ele é usado.|  
|NULLABLE (ODBC 2,0)|7|Smallint não NULL|Se o tipo de dados aceita um valor nulo:<br /><br /> SQL_NO_NULLS se o tipo de dados não aceita valores nulos.<br /><br /> SQL_NULLABLE se o tipo de dados aceita valores nulos.<br /><br /> SQL_NULLABLE_UNKNOWN se não for conhecido se a coluna aceita valores nulos.|  
|CASE_SENSITIVE (ODBC 2,0)|8|Smallint não NULL|Se um tipo de dados de caractere diferencia maiúsculas de minúsculas em agrupamentos e comparações:<br /><br /> SQL_TRUE se o tipo de dados for um tipo de dados de caractere e diferenciar maiúsculas de minúsculas.<br /><br /> SQL_FALSE se o tipo de dados não for um tipo de dados de caractere ou não diferencia maiúsculas de minúsculas.|  
|PESQUISÁVEL (ODBC 2,0)|9|Smallint não NULL|Como o tipo de dados é usado em uma cláusula **Where** :<br /><br /> SQL_PRED_NONE se a coluna não puder ser usada em uma cláusula **Where** . (Isso é o mesmo que o valor de SQL_UNSEARCHABLE no ODBC 2. *x*.)<br /><br /> SQL_PRED_CHAR se a coluna puder ser usada em uma cláusula **Where** , mas somente com o predicado **like** . (Isso é o mesmo que o valor de SQL_LIKE_ONLY no ODBC 2. *x*.)<br /><br /> SQL_PRED_BASIC se a coluna puder ser usada em uma cláusula **Where** com todos os operadores de comparação, exceto **como** (comparação, comparação quantificada, **entre**, **DISTINCT**, **in**, **Match**e **Unique**). (Isso é o mesmo que o valor de SQL_ALL_EXCEPT_LIKE no ODBC 2. *x*.)<br /><br /> SQL_SEARCHABLE se a coluna puder ser usada em uma cláusula **Where** com qualquer operador de comparação.|  
|UNSIGNED_ATTRIBUTE (ODBC 2,0)|10|Smallint|Se o tipo de dados não está assinado:<br /><br /> SQL_TRUE se o tipo de dados não estiver assinado.<br /><br /> SQL_FALSE se o tipo de dados for assinado.<br /><br /> NULL será retornado se o atributo não for aplicável ao tipo de dados ou o tipo de dados não for numérico.|  
|FIXED_PREC_SCALE (ODBC 2,0)|11|Smallint não NULL|Se o tipo de dados tem precisão fixa e escala predefinidas (que são específicas da fonte de dados), como um tipo de dados Money:<br /><br /> SQL_TRUE se ela tiver precisão fixa e escala predefinidas.<br /><br /> SQL_FALSE se não tiver precisão fixa e escala predefinidas.|  
|AUTO_UNIQUE_VALUE (ODBC 2,0)|12|Smallint|Se o tipo de dados é incrementado automaticamente:<br /><br /> SQL_TRUE se o tipo de dados for incrementado automaticamente.<br /><br /> SQL_FALSE se o tipo de dados não for incrementado automaticamente.<br /><br /> NULL será retornado se o atributo não for aplicável ao tipo de dados ou o tipo de dados não for numérico.<br /><br /> Um aplicativo pode inserir valores em uma coluna com esse atributo, mas normalmente não pode atualizar os valores na coluna.<br /><br /> Quando uma inserção é feita em uma coluna de incremento automático, um valor exclusivo é inserido na coluna no momento da inserção. O incremento não está definido, mas é específico da fonte de dados. Um aplicativo não deve supor que uma coluna de incremento automático comece em qualquer ponto específico ou seja incrementada por qualquer valor específico.|  
|LOCAL_TYPE_NAME (ODBC 2,0)|13|Varchar|Versão localizada do nome do tipo de dados dependente da fonte de dados. NULL será retornado se a fonte de dados não oferecer suporte a um nome localizado. Esse nome é destinado somente para exibição, como nas caixas de diálogo.|  
|MINIMUM_SCALE (ODBC 2,0)|14|Smallint|A escala mínima do tipo de dados na fonte de dados. Se um tipo de dados tiver uma escala fixa, as colunas MINIMUM_SCALE e MAXIMUM_SCALE conterão esse valor. Por exemplo, uma coluna SQL_TYPE_TIMESTAMP pode ter uma escala fixa para segundos fracionários. NULL será retornado onde escala não for aplicável. Para obter mais informações, consulte [tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice D: tipos de dados.|  
|MAXIMUM_SCALE (ODBC 2,0)|15|Smallint|A escala máxima do tipo de dados na fonte de dados. NULL será retornado onde escala não for aplicável. Se a escala máxima não for definida separadamente na fonte de dados, mas, em vez disso, for definida como igual à precisão máxima, essa coluna conterá o mesmo valor que a coluna COLUMN_SIZE. Para obter mais informações, consulte [tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice D: tipos de dados.|  
|SQL_DATA_TYPE (ODBC 3,0)|16|Smallint não nulo|O valor do tipo de dados SQL como ele aparece no campo SQL_DESC_TYPE do descritor. Essa coluna é igual à DATA_TYPE coluna, exceto para tipos de dados de intervalo e DateTime.<br /><br /> Para os tipos de dados Interval e DateTime, o campo SQL_DATA_TYPE no conjunto de resultados retornará SQL_INTERVAL ou SQL_DATETIME, e o campo SQL_DATETIME_SUB retornará o subcódigo para o tipo de dados Interval ou DateTime específico. (Consulte o [Apêndice D: tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).)|  
|SQL_DATETIME_SUB (ODBC 3,0)|17|Smallint|Quando o valor de SQL_DATA_TYPE for SQL_DATETIME ou SQL_INTERVAL, essa coluna conterá o subcódigo datetime/Interval. Para tipos de dados diferentes de DateTime e Interval, esse campo é nulo.<br /><br /> Para os tipos de dados Interval ou DateTime, o campo SQL_DATA_TYPE no conjunto de resultados retornará SQL_INTERVAL ou SQL_DATETIME, e o campo SQL_DATETIME_SUB retornará o subcódigo para o tipo de dados Interval ou DateTime específico. (Consulte o [Apêndice D: tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).)|  
|NUM_PREC_RADIX (ODBC 3,0)|18|Integer|Se o tipo de dados for um tipo numérico aproximado, essa coluna conterá o valor 2 para indicar que COLUMN_SIZE especifica um número de bits. Para tipos numéricos exatos, essa coluna contém o valor 10 para indicar que COLUMN_SIZE especifica um número de dígitos decimais. Caso contrário, esta coluna será NULL.|  
|INTERVAL_PRECISION (ODBC 3,0)|19|Smallint|Se o tipo de dados for um tipo de dados de intervalo, essa coluna conterá o valor da precisão à esquerda do intervalo. (Consulte [precisão de tipo de dados de intervalo](../../../odbc/reference/appendixes/interval-data-type-precision.md) no Apêndice D: tipos de dados.) Caso contrário, essa coluna será nula.|  
  
 As informações de atributo podem ser aplicadas a tipos de dados ou a colunas específicas em um conjunto de resultados. **SQLGetTypeInfo** retorna informações sobre atributos associados a tipos de dados; **SQLColAttribute** retorna informações sobre atributos associados a colunas em um conjunto de resultados.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Associando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Retornando informações sobre uma coluna em um conjunto de resultados|[Função SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|Buscando um bloco de dados ou rolando por meio de um conjunto de resultados|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Buscando uma única linha ou um bloco de dados em uma direção somente de avanço|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Retornando informações sobre um driver ou uma fonte de dados|[Função SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
