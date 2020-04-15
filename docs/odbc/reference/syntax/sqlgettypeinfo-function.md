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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303257"
---
# <a name="sqlgettypeinfo-function"></a>Função SQLGetTypeInfo
**Conformidade**  
 Versão introduzida: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **O SQLGetTypeInfo** retorna informações sobre os tipos de dados suportados pela fonte de dados. O driver retorna as informações na forma de um conjunto de resultados SQL. Os tipos de dados destinam-se a ser usados em declarações DDL (Data Definition Language, linguagem de definição de dados).  
  
> [!IMPORTANT]  
>  Os aplicativos devem usar os nomes de tipo retornados na coluna TYPE_NAME do resultado **SQLGetTypeInfo** definido nas instruções **ALTER TABLE** e **CREATE TABLE.** **SQLGetTypeInfo** pode retornar mais de uma linha com o mesmo valor na coluna DATA_TYPE.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLGetTypeInfo(  
     SQLHSTMT      StatementHandle,  
     SQLSMALLINT   DataType);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Alça de declaração para o conjunto de resultados.  
  
 *DataType*  
 [Entrada] O tipo de dados SQL. Este deve ser um dos valores na seção [SQL Data Types](../../../odbc/reference/appendixes/sql-data-types.md) do Apêndice D: Data Types ou um tipo de dados SQL específico para driver. SQL_ALL_TYPES especifica que as informações sobre todos os tipos de dados devem ser devolvidas.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLGetTypeInfo** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **sqlGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *alça* de controle de *declaração*. A tabela a seguir lista os valores SQLSTATE comumente retornados pelo **SQLGetTypeInfo** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01S02|Valor da opção alterado|Um atributo de declaração especificado foi inválido devido às condições de trabalho de implementação, de modo que um valor semelhante foi temporariamente substituído. (Ligue para **SQLGetStmtAttr** para determinar o valor substituído temporariamente.) O valor substituto é válido para o *StatementHandle* até que o cursor seja fechado. Os atributos da declaração que podem ser alterados são: SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_KEYSET_SIZE, SQL_ATTR_MAX_LENGTH, SQL_ATTR_MAX_ROWS, SQL_ATTR_QUERY_TIMEOUT e SQL_ATTR_SIMULATE_CURSOR. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados à qual o driver estava conectado falhou antes da função ser concluída.|  
|24.000|Estado de cursor inválido|Um cursor foi aberto no *StatementHandle,* e **SQLFetch** ou **SQLFetchScroll** foram chamados. Esse erro é devolvido pelo Gerenciador de driver se **o SQLFetch** ou **o SQLFetchScroll** não retornarem SQL_NO_DATA e forem devolvidos pelo driver se **o SQLFetch** ou **o SQLFetchScroll** retornarem SQL_NO_DATA.<br /><br /> Um conjunto de resultados foi aberto no *StatementHandle*, mas **SQLFetch** ou **SQLFetchScroll** não foram chamados.|  
|40001|Falha na serialização|A transação foi revertida devido a um impasse de recursos com outra transação.|  
|40003|Conclusão de declaração desconhecida|A conexão associada falhou durante a execução desta função e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY004|Tipo de dados SQL inválido|O valor especificado para o argumento *DataType* não era nem um identificador de tipo de dados ODBC SQL válido nem um identificador de tipo de dados específico do driver suportado pelo driver.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*, então a função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um segmento diferente em um aplicativo multithread.|  
|HY010|Erro de seqüência de função|(DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *StatementHandle*. Esta função assíncrona ainda estava sendo executada quando a função **SQLGetTypeInfo** foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foram chamados para o *StatementHandle* e retornaram SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) Uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados para o *StatementHandle* e retornaram SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|A combinação das configurações atuais dos atributos de declaração SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE não foi suportada pelo driver ou fonte de dados.<br /><br /> O atributo de declaração SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE, e o atributo de declaração SQL_ATTR_CURSOR_TYPE foi definido como um tipo de cursor para o qual o motorista não suporta marcadores.|  
|HYT00|Tempo limite esgotado|O período de tempo de consulta expirou antes que a fonte de dados retornasse o conjunto de resultados. O período de tempo é definido através **de SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver correspondente ao *StatementHandle* não suporta a função.|  
|IM017|A votação é desativada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a votação é desativada.|  
|IM018|**O SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesta alça.|Se a chamada de função anterior na alça retornar SQL_STILL_EXECUTING e se o modo de notificação estiver ativado, o **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 **O SQLGetTypeInfo** retorna os resultados como um conjunto de resultados padrão, ordenado por DATA_TYPE e, em seguida, pelo quão próximo o tipo de dados mapeia o tipo de dados correspondente ao tipo de dados ODBC SQL correspondente. Os tipos de dados definidos pela fonte de dados têm precedência sobre os tipos de dados definidos pelo usuário. Consequentemente, a ordem de classificação não é necessariamente consistente, mas pode ser generalizada como DATA_TYPE primeira, seguida por TYPE_NAME, ambos ascendentes. Por exemplo, suponha que uma fonte de dados definiu os tipos de dados INTEGER e COUNTER, onde o COUNTER está incrementando automaticamente e que um tipo de dados definido pelo usuário WHOLENUM também foi definido. Estes seriam devolvidos na ordem INTEGER, WHOLENUM e COUNTER, porque o WHOLENUM mapeia de perto o tipo de dados ODBC SQL SQL_INTEGER, enquanto o tipo de dados de incremento automático, embora suportado pela fonte de dados, não mapeia de perto um tipo de dados ODBC SQL. Para obter informações sobre como essas informações podem ser usadas, consulte [Demonstrações de DDL](../../../odbc/reference/develop-app/ddl-statements.md).  
  
 Se o argumento *DataType* especificar um tipo de dados válido para a versão do ODBC suportada pelo driver, mas não for suportado pelo driver, ele retornará um conjunto de resultados vazio.  
  
> [!NOTE]  
>  Para obter mais informações sobre o uso geral, argumentos e dados retornados das funções do catálogo oDBC, consulte [Funções de Catálogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 As seguintes colunas foram renomeadas para ODBC 3. *x*. As alterações de nome da coluna não afetam a compatibilidade retrógrada porque os aplicativos se ligam por número de coluna.  
  
|Coluna ODBC 2.0|ODBC 3. *x* coluna|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|MONEY|FIXED_PREC_SCALE|  
|AUTO_INCREMENT|AUTO_UNIQUE_VALUE|  
  
 As seguintes colunas foram adicionadas ao conjunto de resultados retornado pelo **SQLGetTypeInfo** para ODBC 3. *x:*  
  
-   SQL_DATA_TYPE  
  
-   INTERVAL_PRECISION  
  
-   SQL_DATETIME_SUB  
  
-   NUM_PREC_RADIX  
  
 A tabela a seguir lista as colunas no conjunto de resultados. Colunas adicionais além da coluna 19 (INTERVAL_PRECISION) podem ser definidas pelo driver. Um aplicativo deve ter acesso a colunas específicas do driver, contando abaixo do final do conjunto de resultados, em vez de especificar uma posição ordinal explícita. Para obter mais informações, consulte [Dados Retornados por Funções de Catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
> [!NOTE]  
>  **O SQLGetTypeInfo** pode não retornar todos os tipos de dados. Por exemplo, um driver pode não retornar tipos de dados definidos pelo usuário. Os aplicativos podem usar qualquer tipo de dados válido, independentemente de ser devolvido pelo **SQLGetTypeInfo**. Os tipos de dados retornados pelo **SQLGetTypeInfo** são aqueles suportados pela fonte de dados. Eles são destinados para uso em declarações DDL (Data Definition Language, linguagem de definição de dados). Os drivers podem retornar dados definidos por resultados usando tipos de dados diferentes dos tipos retornados pelo **SQLGetTypeInfo**. Ao criar o conjunto de resultados para uma função de catálogo, o driver pode usar um tipo de dados que não é suportado pela fonte de dados.  
  
|Nome da coluna|Coluna<br /><br /> número|Tipo de dados|Comentários|  
|-----------------|-----------------------|---------------|--------------|  
|TYPE_NAME (ODBC 2.0)|1|Varchar não É NULO|Nome do tipo de dados dependente da fonte de dados; por exemplo, "CHAR()", "VARCHAR()", "MONEY", "LONG VARBINARY" ou "CHAR ( ) FOR BIT DATA". Os aplicativos devem usar esse nome nas instruções **CRIAR TABELA** e **ALTERAR TABELA.**|  
|DATA_TYPE (ODBC 2.0)|2|Smallint não NULL|Tipo de dados SQL. Isso pode ser um tipo de dados SQL ODBC ou um tipo de dados SQL específico para driver. Para os tipos de dados data-hora ou intervalo, esta coluna retorna o tipo de dados concisos (como SQL_TYPE_TIME ou SQL_INTERVAL_YEAR_TO_MONTH). Para obter uma lista de tipos de dados SQL odbc válidos, consulte [Tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md) no apêndice D: Tipos de dados. Para obter informações sobre os tipos de dados SQL específicos do driver, consulte a documentação do motorista.|  
|COLUMN_SIZE (ODBC 2.0)|3|Integer|O tamanho máximo da coluna que o servidor suporta para esse tipo de dados. Para dados numéricos, esta é a precisão máxima. Para dados de seqüência, este é o comprimento dos caracteres. Para os tipos de dados datetime, este é o comprimento nos caracteres da representação de seqüência (assumindo a precisão máxima permitida do componente de segundos fracionados). NULL é devolvido para tipos de dados onde o tamanho da coluna não é aplicável. Para tipos de dados de intervalo, este é o número de caracteres na representação de caracteres do intervalo literal (conforme definido pela precisão de intervalo de liderança; consulte [Interval Data Type Length](../../../odbc/reference/appendixes/interval-data-type-length.md) in Apêndice D: Data Types).<br /><br /> Para obter mais informações sobre o tamanho da coluna, consulte [Tamanho da coluna, Dígitos decimais, Comprimento do Octeto de Transferência e Tamanho do Display](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice D: Tipos de dados.|  
|LITERAL_PREFIX (ODBC 2.0)|4|Varchar|Caracteres ou caracteres usados para prefixar um literal; por exemplo, uma única marca de cotação (') para tipos de dados de caracteres ou 0x para tipos de dados binários; NULL é devolvido para tipos de dados onde um prefixo literal não é aplicável.|  
|LITERAL_SUFFIX (ODBC 2.0)|5|Varchar|Caracteres ou caracteres usados para terminar um literal; por exemplo, uma única marca de cotação (') para tipos de dados de caracteres; NULL é devolvido para tipos de dados onde um sufixo literal não é aplicável.|  
|CREATE_PARAMS (ODBC 2.0)|6|Varchar|Uma lista de palavras-chave, separadas por commas, correspondendo a cada parâmetro que o aplicativo pode especificar entre parênteses ao usar o nome que é devolvido no campo TYPE_NAME. As palavras-chave da lista podem ser qualquer uma das seguintes: comprimento, precisão ou escala. Eles aparecem na ordem que a sintaxe exige que eles sejam usados. Por exemplo, CREATE_PARAMS para DECIMAL seria "precisão,escala"; CREATE_PARAMS para VARCHAR seria igual a "comprimento". NULL é devolvido se não houver parâmetros para a definição do tipo de dados; por exemplo, INTEGER.<br /><br /> O driver fornece o CREATE_PARAMS texto na língua do país/região onde é utilizado.|  
|ANULADO (ODBC 2.0)|7|Smallint não NULL|Se o tipo de dados aceita um valor NULL:<br /><br /> SQL_NO_NULLS se o tipo de dados não aceitar valores NULAS.<br /><br /> SQL_NULLABLE se o tipo de dados aceitar valores NULAS.<br /><br /> SQL_NULLABLE_UNKNOWN se não se sabe se a coluna aceita valores NULOS.|  
|CASE_SENSITIVE (ODBC 2.0)|8|Smallint não NULL|Se um tipo de dados de caractere é sensível a maiúsculas e minúsculas em colações e comparações:<br /><br /> SQL_TRUE se o tipo de dados é um tipo de dados de caracteree é sensível a maiúsculas e minúsculas.<br /><br /> SQL_FALSE se o tipo de dados não é um tipo de dados de caractere ou não é sensível a maiúsculas e minúsculas.|  
|PESQUISÁvel (ODBC 2.0)|9|Smallint não NULL|Como o tipo de dados é usado em uma cláusula **WHERE:**<br /><br /> SQL_PRED_NONE se a coluna não puder ser usada em uma cláusula **WHERE.** (Este é o mesmo valor SQL_UNSEARCHABLE em ODBC 2. *x*.)<br /><br /> SQL_PRED_CHAR se a coluna pode ser usada em uma cláusula **WHERE,** mas apenas com o predicado **LIKE.** (Este é o mesmo valor SQL_LIKE_ONLY em ODBC 2. *x*.)<br /><br /> SQL_PRED_BASIC se a coluna puder ser usada em uma cláusula **WHERE** com todos os operadores de comparação, exceto **LIKE** (comparação, comparação quantificada, **ENTRE,** **DISTINTO,** **IN,** **MATCH**e **UNIQUE**). (Este é o mesmo valor SQL_ALL_EXCEPT_LIKE em ODBC 2. *x*.)<br /><br /> SQL_SEARCHABLE se a coluna pode ser usada em uma cláusula **WHERE** com qualquer operador de comparação.|  
|UNSIGNED_ATTRIBUTE (ODBC 2.0)|10|Smallint|Se o tipo de dados não está assinado:<br /><br /> SQL_TRUE se o tipo de dados não estiver assinado.<br /><br /> SQL_FALSE se o tipo de dados estiver assinado.<br /><br /> NULL é devolvido se o atributo não for aplicável ao tipo de dados ou o tipo de dados não for numérico.|  
|FIXED_PREC_SCALE (ODBC 2.0)|11|Smallint não NULL|Se o tipo de dados tem precisão e escala fixas predefinidas (que são específicas da fonte de dados), como um tipo de dados de dinheiro:<br /><br /> SQL_TRUE se tiver precisão e escala fixas predefinidas.<br /><br /> SQL_FALSE se não tiver precisão e escala fixas predefinidas.|  
|AUTO_UNIQUE_VALUE (ODBC 2.0)|12|Smallint|Se o tipo de dados está incrementando automaticamente:<br /><br /> SQL_TRUE se o tipo de dados estiver se incrementando automaticamente.<br /><br /> SQL_FALSE se o tipo de dados não estiver se incrementando automaticamente.<br /><br /> NULL é devolvido se o atributo não for aplicável ao tipo de dados ou o tipo de dados não for numérico.<br /><br /> Um aplicativo pode inserir valores em uma coluna com esse atributo, mas normalmente não pode atualizar os valores na coluna.<br /><br /> Quando uma inserção é feita em uma coluna de auto-incremento, um valor único é inserido na coluna no momento da inserção. O incremento não é definido, mas é específico da fonte de dados. Um aplicativo não deve assumir que uma coluna de incremento automático é iniciada em qualquer ponto ou incrementos por qualquer valor específico.|  
|LOCAL_TYPE_NAME (ODBC 2.0)|13|Varchar|Versão localizada do nome do tipo de dados dependente da fonte de dados. NULL será retornado se a fonte de dados não oferecer suporte a um nome localizado. Este nome destina-se apenas à exibição, como em caixas de diálogo.|  
|MINIMUM_SCALE (ODBC 2.0)|14|Smallint|A escala mínima do tipo de dados na fonte de dados. Se um tipo de dados tiver uma escala fixa, as colunas MINIMUM_SCALE e MAXIMUM_SCALE conterão esse valor. Por exemplo, uma coluna SQL_TYPE_TIMESTAMP pode ter uma escala fixa para segundos fracionados. NULL será retornado onde escala não for aplicável. Para obter mais informações, consulte [Tamanho da coluna, Dígitos decimais, Comprimento do octeto de transferência e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no apêndice D: Tipos de dados.|  
|MAXIMUM_SCALE (ODBC 2.0)|15|Smallint|A escala máxima do tipo de dados na fonte de dados. NULL será retornado onde escala não for aplicável. Se a escala máxima não for definida separadamente na fonte de dados, mas for definida como sendo a mesma da precisão máxima, esta coluna contém o mesmo valor da coluna COLUMN_SIZE. Para obter mais informações, consulte [Tamanho da coluna, Dígitos decimais, Comprimento do octeto de transferência e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no apêndice D: Tipos de dados.|  
|SQL_DATA_TYPE (ODBC 3.0)|16|Smallint NÃO NULO|O valor do tipo de dados SQL como ele aparece no campo SQL_DESC_TYPE do descritor. Esta coluna é a mesma da coluna DATA_TYPE, exceto para os tipos de dados de intervalo e data.<br /><br /> Para os tipos de dados de intervalo e data, o campo SQL_DATA_TYPE no conjunto de resultados retornará SQL_INTERVAL ou SQL_DATETIME, e o campo SQL_DATETIME_SUB retornará o subcódigo para o tipo de dados de intervalo ou data específica. (Veja [o apêndice D: Tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).)|  
|SQL_DATETIME_SUB (ODBC 3.0)|17|Smallint|Quando o valor de SQL_DATA_TYPE estiver SQL_DATETIME ou SQL_INTERVAL, esta coluna contém o subcódigo data-hora/intervalo. Para tipos de dados que não sejam datae e intervalo, este campo é NULL.<br /><br /> Para os tipos de dados de intervalo ou data, o campo SQL_DATA_TYPE no conjunto de resultados retornará SQL_INTERVAL ou SQL_DATETIME, e o campo SQL_DATETIME_SUB retornará o subcódigo para o tipo de dados de intervalo ou data específica. (Veja [o apêndice D: Tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).)|  
|NUM_PREC_RADIX (ODBC 3.0)|18|Integer|Se o tipo de dados for um tipo numérico aproximado, esta coluna contém o valor 2 para indicar que COLUMN_SIZE especifica um número de bits. Para tipos numéricos exatos, esta coluna contém o valor 10 para indicar que COLUMN_SIZE especifica um número de dígitos decimais. Caso contrário, esta coluna será NULL.|  
|INTERVAL_PRECISION (ODBC 3.0)|19|Smallint|Se o tipo de dados for um tipo de dados de intervalo, esta coluna contém o valor do intervalo de precisão principal. (Ver [precisão do tipo de dados de intervalo](../../../odbc/reference/appendixes/interval-data-type-precision.md) no apêndice D: Tipos de dados.) Caso contrário, esta coluna é NULL.|  
  
 As informações de atributos podem ser aplicadas a tipos de dados ou a colunas específicas em um conjunto de resultados. **O SQLGetTypeInfo** retorna informações sobre atributos associados a tipos de dados; **SQLColAttribute** retorna informações sobre atributos associados a colunas em um conjunto de resultados.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Vinculando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelamento do processamento de declarações|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Retornando informações sobre uma coluna em um conjunto de resultados|[Função SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|Buscar um bloco de dados ou rolar através de um conjunto de resultados|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Buscar uma única linha ou um bloco de dados em uma direção somente para a frente|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Retornando informações sobre um driver ou fonte de dados|[Função SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
