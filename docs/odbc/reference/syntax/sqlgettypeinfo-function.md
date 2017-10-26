---
title: "Função SQLGetTypeInfo | Microsoft Docs"
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
- SQLGetTypeInfo
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetTypeInfo
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC]
ms.assetid: bdedb044-8924-4ca4-85f3-8b37578e0257
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7411a992bfbcb56a05e8ada5e4849a24ab8d2894
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgettypeinfo-function"></a>Função SQLGetTypeInfo
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 1.0 ODBC: 92 ISO  
  
 **Resumo**  
 **SQLGetTypeInfo** retorna informações sobre tipos de dados suportados pela fonte de dados. O driver retorna as informações na forma de um conjunto de resultados SQL. Os tipos de dados são destinados a uso em instruções de linguagem de definição de dados (DDL).  
  
> [!IMPORTANT]  
>  Os aplicativos devem usar os nomes de tipo retornados na coluna de TYPE_NAME o **SQLGetTypeInfo** conjunto de resultados em **ALTER TABLE** e **CREATE TABLE** instruções. **SQLGetTypeInfo** pode retornar mais de uma linha com o mesmo valor na coluna DATA_TYPE.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLGetTypeInfo(  
     SQLHSTMT      StatementHandle,  
     SQLSMALLINT   DataType);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrução para o conjunto de resultados.  
  
 *Tipo de dados*  
 [Entrada] O tipo de dados SQL. Deve ser um dos valores a [tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md) seção de apêndice d: os tipos de dados ou um tipo de dados SQL específico do driver. SQL_ALL_TYPES Especifica que as informações sobre todos os tipos de dados devem ser retornadas.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLGetTypeInfo** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* do SQL _HANDLE_STMT e um *tratar* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLGetTypeInfo** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01S02|Valor de opção alterado|Um atributo de instrução especificada era inválido devido a condições de trabalho de implementação para que um valor semelhante temporariamente foi substituído. (Chamar **SQLGetStmtAttr** para determinar o valor substituído temporariamente.) O valor de substituição é válido para o *StatementHandle* até que o cursor seja fechado. Os atributos de instrução que podem ser alterados são: SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_KEYSET_SIZE, SQL_ATTR_MAX_LENGTH, SQL_ATTR_MAX_ROWS, SQL_ATTR_QUERY_TIMEOUT e SQL_ATTR_SIMULATE_CURSOR. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|24000|Estado de cursor inválido|Um cursor foi aberto o *StatementHandle,* e **SQLFetch** ou **SQLFetchScroll** tivesse sido chamada. Esse erro é retornado pelo Gerenciador de Driver se **SQLFetch** ou **SQLFetchScroll** não retornou SQL_NO_DATA e é retornada pelo driver se **SQLFetch** ou **SQLFetchScroll** retornou SQL_NO_DATA.<br /><br /> Um conjunto de resultados foi aberto o *StatementHandle*, mas **SQLFetch** ou **SQLFetchScroll** não tivesse sido chamada.|  
|40001|Falha na serialização|A transação foi revertida devido a um deadlock de recursos com outra transação.|  
|40003|Conclusão de instrução desconhecido|Falha de conexão associado durante a execução dessa função e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY004|Tipo de dados SQL inválido|O valor especificado para o argumento *DataType* não era um identificador de tipo de dados SQL ODBC válido nem um identificador de tipo de dados específica do driver com suporte pelo driver.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*, em seguida, a função foi chamada e, antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em uma aplicativos multithread.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando o **SQLGetTypeInfo** função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *StatementHandle* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada antes de recuperação para todos os parâmetros de fluxo de dados.<br /><br /> (DM) uma função de execução assíncrona (não la) foi chamada para o *StatementHandle* e ainda estava em execução quando esta função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o * StatementHandle* e retorna SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todas as colunas ou parâmetros de dados em execução.|  
|HY013|Erro de gerenciamento de memória|Não foi possível processar a chamada de função porque os objetos de memória subjacente não podem ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecido. Somente Desconecte e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|A combinação das configurações atuais dos atributos de instrução SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE não era compatível com a driver ou fonte de dados.<br /><br /> O atributo da instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE, e o atributo de instrução SQL_ATTR_CURSOR_TYPE foi definido como um tipo de cursor para o qual o driver não oferecer suporte a indicadores.|  
|HYT00|Tempo limite esgotado|O período de tempo limite da consulta expirou antes que a fonte de dados retornou o conjunto de resultados. O período de tempo limite é definido por meio de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|(DM) o driver correspondente a *StatementHandle* não oferece suporte para a função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem está desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior na alça retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 **SQLGetTypeInfo** retorna os resultados como um conjunto de resultados padrão, ordenado por DATA_TYPE e depois pela proximidade com o tipo de dados é mapeado para o tipo de dados ODBC SQL correspondente. Tipos de dados definidos pela fonte de dados têm precedência sobre os tipos de dados definidos pelo usuário. Consequentemente, a ordem de classificação não é necessariamente consistente, mas pode ser generalizada como DATA_TYPE primeiro, seguida pelo TYPE_NAME, ambos em ordem crescente. Por exemplo, suponha que uma fonte de dados definido tipos de dados inteiro e um CONTADOR, onde o CONTADOR é o incremento automático, e um tipo de dados definido pelo usuário WHOLENUM também foi definido. Esses seriam retornados na ordem inteiro, WHOLENUM e o CONTADOR, porque WHOLENUM maps junto com os dados de ODBC SQL tipo SQL_INTEGER, enquanto o incremento automático tipo de dados, mesmo que suporte pela fonte de dados, não mapeiam com precisão para um tipo de dados SQL ODBC. Para obter informações sobre como essas informações podem ser usadas, consulte [instruções DDL](../../../odbc/reference/develop-app/ddl-statements.md).  
  
 Se o *DataType* argumento especifica um tipo de dados que é válido para a versão do ODBC com suporte pelo driver, mas não é suportado pelo driver, ela retornará um conjunto de resultados vazio.  
  
> [!NOTE]  
>  Para obter mais informações sobre o uso geral, os argumentos e os dados retornados de funções de catálogo ODBC, consulte [funções de catálogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 As seguintes colunas foram renomeadas para ODBC 3. *x*. As alterações de nome de coluna não afetam a compatibilidade com versões anteriores, porque aplicativos associar pelo número de coluna.  
  
|Coluna de ODBC 2.0|ODBC 3. *x* coluna|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|MONEY|FIXED_PREC_SCALE|  
|AUTO_INCREMENT|AUTO_UNIQUE_VALUE|  
  
 As colunas a seguir foram adicionadas ao conjunto de resultados retornado por **SQLGetTypeInfo** para ODBC 3.* x*:  
  
-   SQL_DATA_TYPE  
  
-   INTERVAL_PRECISION  
  
-   SQL_DATETIME_SUB  
  
-   NUM_PREC_RADIX  
  
 A tabela a seguir lista as colunas no conjunto de resultados. Colunas adicionais além da coluna 19 (INTERVAL_PRECISION) podem ser definidas pelo driver. Um aplicativo deve acessar colunas específicas do driver por contagem regressiva do final do conjunto de resultados em vez de especificar uma posição ordinal explícita. Para obter mais informações, consulte [dados retornados pelas funções de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
> [!NOTE]  
>  **SQLGetTypeInfo** podem não retornar todos os tipos de dados. Por exemplo, um driver pode não retornar tipos de dados definidos pelo usuário. Aplicativos podem usar qualquer tipo de dados válido, independentemente se ele é retornado por **SQLGetTypeInfo**. Os tipos de dados retornados por **SQLGetTypeInfo** são aquelas com suporte pela fonte de dados. Eles são destinados a uso em instruções de linguagem de definição de dados (DDL). Drivers podem retornar dados de conjunto de resultados usando tipos de dados que não sejam os tipos retornados pela **SQLGetTypeInfo**. Ao criar o conjunto de resultados de uma função de catálogo, o driver pode usar um tipo de dados que não é suportado pela fonte de dados.  
  
|Nome da coluna|Coluna<br /><br /> number|Tipo de dados|Comentários|  
|-----------------|-----------------------|---------------|--------------|  
|TYPE_NAME (ODBC 2.0)|1|Varchar não nulo|Nome do tipo de dados de origem dependente de dados; Por exemplo, "Char ()", "Varchar ()", "MONEY", "VARBINARY longo" ou "CHAR () para dados BIT". Aplicativos devem usar esse nome no **CREATE TABLE** e **ALTER TABLE** instruções.|  
|DATA_TYPE (ODBC 2.0)|2|Smallint não NULL|Tipo de dados SQL. Isso pode ser um tipo de dados SQL ODBC ou um tipo de dados SQL específico do driver. Para tipos de dados datetime ou intervalo, esta coluna retorna o tipo de dados conciso (como SQL_TYPE_TIME ou SQL_INTERVAL_YEAR_TO_MONTH). Para obter uma lista de tipos de dados ODBC SQL válidos, consulte [tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md) no Apêndice d: os tipos de dados. Para obter informações sobre tipos de dados SQL específico do driver, consulte a documentação do driver.|  
|COLUMN_SIZE (ODBC 2.0)|3|Integer|O tamanho máximo de coluna que o servidor oferece suporte para esse tipo de dados. Para dados numéricos, esta é a precisão máxima. Para dados de cadeia de caracteres, esse é o comprimento em caracteres. Para tipos de dados de data e hora, este é o comprimento de caracteres da representação de cadeia de caracteres (supondo que a precisão máxima permitida do componente frações de segundo). NULL é retornado para os tipos de dados em que o tamanho da coluna não é aplicável. Para tipos de dados de intervalo, este é o número de caracteres na representação do intervalo de literal de caractere (conforme definido pelo intervalo de precisão; principal consulte [comprimento do intervalo do tipo de dados](../../../odbc/reference/appendixes/interval-data-type-length.md) no Apêndice d: os tipos de dados).<br /><br /> Para obter mais informações sobre o tamanho da coluna, consulte [tamanho da coluna, dígitos decimais, transferir o comprimento do octeto e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice d: os tipos de dados.|  
|LITERAL_PREFIX (ODBC 2.0)|4|Varchar|Caractere ou caracteres usados para prefixar um literal; Por exemplo, uma aspa simples (') para tipos de dados de caractere ou 0x para tipos de dados binários. NULL é retornado para os tipos de dados onde um prefixo de literal não é aplicável.|  
|LITERAL_SUFFIX (ODBC 2.0)|5|Varchar|Um ou mais caracteres usados para terminar um literal; Por exemplo, uma aspa simples (') para tipos de dados de caractere. NULL é retornado para os tipos de dados onde um sufixo literal não é aplicável.|  
|CREATE_PARAMS (ODBC 2.0)|6|Varchar|Uma lista de palavras-chave, separados por vírgulas, que correspondem a cada parâmetro que o aplicativo pode especificar entre parênteses ao usar o nome que é retornado no campo TYPE_NAME. As palavras-chave na lista podem ser qualquer um dos seguintes: comprimento, precisão ou escala. Eles aparecem na ordem em que a sintaxe precisa deles para ser usado. Por exemplo, seria CREATE_PARAMS para DECIMAL "precisão, escala"; CREATE_PARAMS para VARCHAR seria igual a "comprimento". NULL será retornado se não existem parâmetros para a definição de tipo de dados; Por exemplo, número inteiro.<br /><br /> O driver fornece o texto CREATE_PARAMS no idioma do país/região em que ele é usado.|  
|PERMITE VALOR NULO (ODBC 2.0)|7|Smallint não NULL|Se o tipo de dados aceita um valor NULL:<br /><br /> SQL_NO_NULLS se o tipo de dados não aceita valores nulos.<br /><br /> SQL_NULLABLE se o tipo de dados aceita valores nulos.<br /><br /> SQL_NULLABLE_UNKNOWN se não se sabe se a coluna aceita valores nulos.|  
|CASE_SENSITIVE (ODBC 2.0)|8|Smallint não NULL|Se um tipo de dados de caractere diferencia maiusculas de minúsculas em agrupamentos e comparações:<br /><br /> SQL_TRUE se o tipo de dados é um tipo de dados de caracteres e diferencia maiusculas de minúsculas.<br /><br /> SQL_FALSE se o tipo de dados não é um tipo de dados de caractere ou não diferencia maiusculas de minúsculas.|  
|RECURSO DE PESQUISA (ODBC 2.0)|9|Smallint não NULL|Como o tipo de dados é usado em uma **onde** cláusula:<br /><br /> SQL_PRED_NONE se a coluna não pode ser usada em uma **onde** cláusula. (Isso é igual ao valor SQL_UNSEARCHABLE no ODBC 2. *x*.)<br /><br /> SQL_PRED_CHAR se a coluna pode ser usada em uma **onde** cláusula, mas apenas com o **como** predicado. (Isso é igual ao valor SQL_LIKE_ONLY no ODBC 2. *x*.)<br /><br /> SQL_PRED_BASIC se a coluna pode ser usada em uma **onde** cláusula com todos os operadores de comparação exceto **como** (comparação, comparação quantificada, **entre**, ** DISTINCT**, **na**, **correspondência**, e **UNIQUE**). (Isso é igual ao valor SQL_ALL_EXCEPT_LIKE no ODBC 2. *x*.)<br /><br /> SQL_SEARCHABLE se a coluna pode ser usada em uma **onde** cláusula com qualquer operador de comparação.|  
|UNSIGNED_ATTRIBUTE (ODBC 2.0)|10|Smallint|Se o tipo de dados é não assinado:<br /><br /> SQL_TRUE se o tipo de dados não está assinado.<br /><br /> SQL_FALSE se o tipo de dados é assinado.<br /><br /> NULL será retornado se o atributo não é aplicável ao tipo de dados ou o tipo de dados não for numérico.|  
|FIXED_PREC_SCALE (ODBC 2.0)|11|Smallint não NULL|Se o tipo de dados tem predefinidos fixa precisão e escala (que são específico da fonte de dados), como um tipo de dados money:<br /><br /> Precisão e escala fixos SQL_TRUE se ele tem predefinidos.<br /><br /> Precisão e escala fixos SQL_FALSE se não tiver predefinidos.|  
|AUTO_UNIQUE_VALUE (ODBC 2.0)|12|Smallint|Se o tipo de dados é incrementado automaticamente:<br /><br /> SQL_TRUE se o tipo de dados é incrementado automaticamente.<br /><br /> SQL_FALSE se o tipo de dados não é incrementado automaticamente.<br /><br /> NULL será retornado se o atributo não é aplicável ao tipo de dados ou o tipo de dados não for numérico.<br /><br /> Um aplicativo pode inserir valores em uma coluna com esse atributo, mas geralmente não é possível atualizar os valores na coluna.<br /><br /> Quando uma inserção é feita em uma coluna de incremento automático, um valor exclusivo é inserido na coluna em tempo de inserção. O incremento não está definido, mas é específico da fonte de dados. Um aplicativo não deve presumir que uma coluna de incremento automático inicia em qualquer momento determinado ou incrementos de qualquer valor específico.|  
|LOCAL_TYPE_NAME (ODBC 2.0)|13|Varchar|Versão localizada do nome da fonte dependente de dados do tipo de dados. NULL será retornado se a fonte de dados não oferecer suporte a um nome localizado. Esse nome destina-se a exibição única, como caixas de diálogo.|  
|MINIMUM_SCALE (ODBC 2.0)|14|Smallint|A escala mínima do tipo de dados na fonte de dados. Se um tipo de dados tiver uma escala fixa, as colunas MINIMUM_SCALE e MAXIMUM_SCALE conterão esse valor. Por exemplo, uma coluna SQL_TYPE_TIMESTAMP pode ter uma escala fixa para segundos fracionários. NULL será retornado onde escala não for aplicável. Para obter mais informações, consulte [tamanho da coluna, dígitos decimais, transferir o comprimento do octeto e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice d: os tipos de dados.|  
|MAXIMUM_SCALE (ODBC 2.0)|15|Smallint|A escala máxima do tipo de dados na fonte de dados. NULL será retornado onde escala não for aplicável. Se a escala máxima não estiver definida separadamente na fonte de dados, mas em vez disso, é definida para ser o mesmo que a precisão máxima, esta coluna contém o mesmo valor que a coluna COLUMN_SIZE. Para obter mais informações, consulte [tamanho da coluna, dígitos decimais, transferir o comprimento do octeto e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice d: os tipos de dados.|  
|SQL_DATA_TYPE (ODBC 3.0)|16|Smallint não NULL|O valor do tipo de dados SQL como ele aparece no campo SQL_DESC_TYPE do descritor. Essa coluna é igual à coluna DATA_TYPE, exceto para tipos de dados de intervalo e datetime.<br /><br /> Para tipos de dados de intervalo e datetime, o campo SQL_DATA_TYPE no conjunto de resultados retornará SQL_INTERVAL ou SQL_DATETIME e o campo SQL_DATETIME_SUB retornará o subcódigo para o tipo de dados datetime ou de intervalo específico. (Consulte [tipos de dados do apêndice d:](../../../odbc/reference/appendixes/appendix-d-data-types.md).)|  
|SQL_DATETIME_SUB (ODBC 3.0)|17|Smallint|Quando o valor de SQL_DATA_TYPE for SQL_DATETIME ou SQL_INTERVAL, esta coluna contém o subcódigo de intervalo/datetime. Para tipos de dados diferentes de data/hora e intervalo, este campo é NULL.<br /><br /> Para tipos de dados de intervalo ou data/hora, o campo SQL_DATA_TYPE no conjunto de resultados retornará SQL_INTERVAL ou SQL_DATETIME e o campo SQL_DATETIME_SUB retornará o subcódigo para o tipo de dados datetime ou de intervalo específico. (Consulte [tipos de dados do apêndice d:](../../../odbc/reference/appendixes/appendix-d-data-types.md).)|  
|NUM_PREC_RADIX (ODBC 3.0)|18|Integer|Se o tipo de dados é um tipo numérico aproximado, esta coluna contém o valor 2 para indicar que o COLUMN_SIZE Especifica um número de bits. Para tipos numéricos exatos, esta coluna contém o valor 10 para indicar que o COLUMN_SIZE Especifica um número de dígitos decimais. Caso contrário, esta coluna será NULL.|  
|INTERVAL_PRECISION (ODBC 3.0)|19|Smallint|Se o tipo de dados é um tipo de dados de intervalo, esta coluna contém o valor de precisão intervalo à esquerda. (Consulte [precisão do tipo de dados de intervalo](../../../odbc/reference/appendixes/interval-data-type-precision.md) no Apêndice d: os tipos de dados.) Caso contrário, esta coluna será NULL.|  
  
 Informações de atributo podem aplicar para tipos de dados ou colunas específicas em um conjunto de resultados. **SQLGetTypeInfo** retorna informações sobre atributos associados a tipos de dados. **SQLColAttribute** retorna informações sobre atributos associados a colunas em um conjunto de resultados.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Um buffer de associação a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Retornando informações sobre uma coluna em um conjunto de resultados|[Função SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|Buscar um bloco de dados ou rolar por um resultado definido|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Buscando uma única linha ou um bloco de dados em uma direção de somente avanço|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Retornando informações sobre um driver ou fonte de dados|[Função SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)

