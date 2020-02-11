---
title: Função SQLExecute | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLExecute
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLExecute
helpviewer_keywords:
- SQLExecute function [ODBC]
ms.assetid: 9286a01d-cde2-4b90-af94-9fd7f8da48bf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 12dffe315485aadc839654996f6af3a561161246
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68003131"
---
# <a name="sqlexecute-function"></a>Função SQLExecute
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: ISO 92  
  
 **Resumo**  
 **SQLExecute** executa uma instrução preparada, usando os valores atuais das variáveis de marcador de parâmetro se existirem marcadores de parâmetro na instrução.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLExecute(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 Entrada Identificador de instrução.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR, SQL_NO_DATA, SQL_INVALID_HANDLE ou SQL_PARAM_DATA_AVAILABLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLExecute** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *identificador* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLExecute** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|DESCRIÇÃO|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01001|Conflito de operação do cursor|A instrução preparada associada ao *StatementHandle* continha uma instrução UPDATE ou DELETE posicionada, e nenhuma linha ou mais de uma fila foi atualizada ou excluída. (Para obter mais informações sobre atualizações para mais de uma linha, consulte a descrição do *atributo* SQL_ATTR_SIMULATE_CURSOR em **SQLSetStmtAttr**.)<br /><br /> (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01003|Valor nulo eliminado na função Set|A instrução preparada associada a *StatementHandle* continha uma função Set (como **AVG**, **Max**, **min**e assim por diante), mas não a função de conjunto de **contagem** , e valores de argumento nulos foram eliminados antes da aplicação da função. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres, truncados à direita|Dados de cadeia de caracteres ou binários retornados para um parâmetro de saída resultaram no truncamento de um caractere não em branco ou dados binários não nulos. Se fosse um valor de cadeia de caracteres, ele foi truncado à direita. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01006|Privilégio não revogado|A instrução preparada associada ao *StatementHandle* foi uma instrução **REVOKE** e o usuário não tinha o privilégio especificado. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01007|Privilégio não concedido|A instrução preparada associada ao *StatementHandle* foi uma instrução **Grant** e não foi possível conceder ao usuário o privilégio especificado.|  
|01S02|Valor da opção alterado|Um atributo de instrução especificado era inválido devido a condições de trabalho de implementação; portanto, um valor semelhante foi substituído temporariamente. (**SQLGetStmtAttr** pode ser chamado para determinar qual é o valor substituído temporariamente.) O valor de substituição é válido para o *StatementHandle* até que o cursor seja fechado, ponto em que o atributo de instrução reverte para seu valor anterior. Os atributos de instrução que podem ser alterados são: SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_KEYSET_SIZE, SQL_ATTR_MAX_LENGTH, SQL_ATTR_MAX_ROWS, SQL_ATTR_QUERY_TIMEOUT e SQL_ATTR_SIMULATE_CURSOR. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01S07|Truncamento fracionário|Os dados retornados para um parâmetro de entrada/saída ou saída foram truncados de modo que a parte fracionária de um tipo de dados numeric fosse truncada ou a parte fracionária do componente de tempo de um tipo de dados time, timestamp ou interval fosse truncada.<br /><br /> (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|07002|Campo de contagem incorreto|O número de parâmetros especificado em **SQLBindParameter** era menor que o número de parâmetros na instrução SQL contidas em \* *StatementText*.<br /><br /> **SQLBindParameter** foi chamado com *ParameterValuePtr* definido como um ponteiro nulo, *StrLen_or_IndPtr* não definido como SQL_NULL_DATA ou SQL_DATA_AT_EXEC e *InputOutputType* não definido como SQL_PARAM_OUTPUT, de modo que o número de parâmetros especificado em **SQLBindParameter** era maior que o número de parâmetros na instrução SQL contido em **StatementText*.|  
|07006|Violação de atributo de tipo de dados restrito|O valor de dados identificado pelo argumento *ValueType* em **SQLBindParameter** para o parâmetro associado não pôde ser convertido para o tipo de dados identificado pelo argumento *ParameterType* em **SQLBindParameter**.<br /><br /> O valor de dados retornado para um parâmetro associado como SQL_PARAM_INPUT_OUTPUT ou SQL_PARAM_OUTPUT não pôde ser convertido para o tipo de dados identificado pelo argumento *ValueType* em **SQLBindParameter**.<br /><br /> (Se os valores de dados de uma ou mais linhas não puderem ser convertidos, mas uma ou mais linhas tiverem sido retornadas com êxito, essa função retornará SQL_SUCCESS_WITH_INFO.)|  
|07007|Violação de valor de parâmetro restrito|O tipo de parâmetro SQL_PARAM_INPUT_OUTPUT_STREAM é usado somente para um parâmetro que envia e recebe dados em partes. Um buffer associado de entrada não é permitido para esse tipo de parâmetro.<br /><br /> Esse erro ocorrerá quando o tipo de parâmetro for SQL_PARAM_INPUT_OUTPUT e quando o \* *StrLen_or_IndPtr* especificado em **SQLBindParameter** não for igual a SQL_NULL_DATA, SQL_DEFAULT_PARAM, SQL_LEN_DATA_AT_EXEC (Len) ou SQL_DATA_AT_EXEC.|  
|07S01|Uso inválido do parâmetro padrão|Um valor de parâmetro, definido com **SQLBindParameter**, foi SQL_DEFAULT_PARAM e o parâmetro correspondente não era um parâmetro para uma invocação de procedimento canônico ODBC.|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado falhou antes da função concluir o processamento.|  
|21S02|O grau da tabela derivada não corresponde à lista de colunas|A instrução preparada associada ao *StatementHandle* continha uma instrução **Create View** , e a lista de colunas não qualificada (o número de colunas especificado para a exibição nos argumentos de *identificador de coluna* da instrução SQL) continha mais nomes do que o número de colunas na tabela derivada definida pelo argumento de especificação de *consulta* da instrução SQL.|  
|22001|Dados de cadeia de caracteres, truncamento à direita|A atribuição de um valor de caractere ou binário a uma coluna resultou no truncamento de caracteres ou bytes não vazios (caracteres) ou não nulos (binários).|  
|22002|Variável de indicador necessária, mas não fornecida|Dados nulos foram associados a um parâmetro de saída cujo *StrLen_or_IndPtr* definido por **SQLBindParameter** era um ponteiro nulo.|  
|22003|Valor numérico fora do intervalo|A instrução preparada associada ao *StatementHandle* continha um parâmetro numérico associado e o valor do parâmetro fez com que a parte inteira (em oposição à fracionária) do número seja truncada quando atribuída à coluna da tabela associada.<br /><br /> Retornar um valor numérico (como numérico ou cadeia de caracteres) para um ou mais parâmetros de entrada/saída ou saída teria causado a parte inteira (em oposição à fracionária) do número a ser truncado.|  
|22007|Formato de data e hora inválido|A instrução preparada associada ao *StatementHandle* continha uma instrução SQL que continha uma estrutura de data, hora ou timestamp como um parâmetro associado, e o parâmetro era, respectivamente, uma data, hora ou carimbo de hora inválido.<br /><br /> Um parâmetro de entrada/saída ou de saída foi associado a uma estrutura C de data, hora ou timestamp, e um valor no parâmetro retornado foi, respectivamente, uma data, hora ou carimbo de hora inválido. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|22008|Estouro no campo DateTime|A instrução preparada associada ao *StatementHandle* continha uma instrução SQL que continha uma expressão DateTime que, quando computada, resultou em uma estrutura de data, hora ou timestamp que era inválida.<br /><br /> Uma expressão DateTime computada para um parâmetro de entrada/saída ou de saída resultou em uma estrutura C de data, hora ou timestamp que era inválida.|  
|22012|Divisão por zero|A instrução preparada associada ao *StatementHandle* continha uma expressão aritmética que causou a divisão por zero.<br /><br /> Uma expressão aritmética calculada para um parâmetro de entrada/saída ou saída resultou em divisão por zero.|  
|22015|Estouro no campo de intervalo|StatementText continha um parâmetro numérico exato ou de intervalo que, quando convertido em um tipo de dados SQL de intervalo, causou uma perda de dígitos significativos. * \**<br /><br /> StatementText continha um parâmetro de intervalo com mais de um campo que, quando convertido em um tipo de dados numérico em uma coluna, não tinha nenhuma representação no tipo de dados numeric. * \**<br /><br /> StatementText continha dados de parâmetro que foram atribuídos a um tipo SQL de intervalo, e não havia nenhuma representação do valor do tipo C no tipo SQL de intervalo. * \**<br /><br /> A atribuição de um parâmetro de entrada/saída ou saída que foi um tipo de SQL numérico exato ou de intervalo para um tipo de intervalo C causou uma perda de dígitos significativos.<br /><br /> Quando um parâmetro de entrada/saída ou de saída foi atribuído a uma estrutura C do intervalo, não havia nenhuma representação dos dados na estrutura de dados do intervalo.|  
|22018|Valor de caractere inválido para especificação de conversão|StatementText continha um tipo C que era exato ou aproximado, um DateTime ou um tipo de dados de intervalo; * \** o tipo SQL da coluna era um tipo de dados de caractere; e o valor na coluna não era um literal válido do tipo associado de C.<br /><br /> Quando um parâmetro de entrada/saída ou saída foi retornado, o tipo SQL era um tipo de dados numérico ou exato aproximado, um DateTime ou um intervalo; o tipo C foi SQL_C_CHAR; e o valor na coluna não era um literal válido do tipo SQL associado.|  
|22019|Caractere de escape inválido|A instrução preparada associada a *StatementHandle* continha um predicado **like** com um **escape** na cláusula **Where** , e o comprimento do caractere de escape após **escape** não era igual a 1.|  
|22025|Sequência de escape inválida|A instrução preparada associada a *StatementHandle* continha " _caractere_ **de escape de** _valor de padrão_ de**escape" na** cláusula **Where** , e o caractere após o caractere de escape no valor de padrão não era um de "%" ou "_".|  
|23000|Violação de restrição de integridade|A instrução preparada associada ao *StatementHandle* continha um parâmetro. O valor do parâmetro era nulo para uma coluna definida como NOT NULL na coluna da tabela associada, um valor duplicado foi fornecido para uma coluna restrita para conter apenas valores exclusivos ou alguma outra restrição de integridade foi violada.|  
|24.000|Estado de cursor inválido|Um cursor foi posicionado no *StatementHandle* por **SQLFetch** ou **SQLFetchScroll**. Esse erro será retornado pelo Gerenciador de driver se **SQLFetch** ou **SQLFetchScroll** não tiver retornado SQL_NO_DATA e será retornado pelo driver se **SQLFetch** ou **SQLFetchScroll** tiver retornado SQL_NO_DATA.<br /><br /> Um cursor foi aberto no *StatementHandle*.<br /><br /> A instrução preparada associada ao *StatementHandle* continha uma atualização posicionada ou excluir estado, t e o cursor foi posicionado antes do início do conjunto de resultados ou após o final do conjunto de resultados.|  
|40001|Falha de serialização|A transação foi revertida devido a um deadlock de recurso com outra transação.|  
|40003|Conclusão de instrução desconhecida|A conexão associada falhou durante a execução dessa função, e o estado da transação não pode ser determinado.|  
|42000|Erro de sintaxe ou violação de acesso|O usuário não tinha permissão para executar a instrução preparada associada ao *StatementHandle*.|  
|44000|Violação COM OPÇÃO DE VERIFICAÇÃO|A instrução preparada associada a *StatementHandle* continha uma instrução **Insert** executada em uma tabela exibida ou uma tabela derivada da tabela exibida que foi criada especificando **with check option**, de modo que uma ou mais linhas afetadas pela instrução **Insert** não estarão mais presentes na tabela exibida.<br /><br /> A instrução preparada associada ao *StatementHandle* continha uma instrução **Update** executada em uma tabela exibida ou uma tabela derivada da tabela exibida que foi criada especificando **with check option**, de modo que uma ou mais linhas afetadas pela instrução **Update** não estarão mais presentes na tabela exibida.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \*MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativo multithread.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *StatementHandle*. Esta função assíncrona ainda estava em execução quando a função **SQLExecute** foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para *StatementHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado para o *StatementHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.<br /><br /> (DM) o *StatementHandle* não estava preparado.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|Um valor de parâmetro, definido com **SQLBindParameter**, era um ponteiro nulo e o valor de comprimento do parâmetro não era 0, SQL_NULL_DATA, SQL_DATA_AT_EXEC, SQL_DEFAULT_PARAM ou menor ou igual a SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> Um valor de parâmetro, definido com **SQLBindParameter**, não era um ponteiro nulo; o tipo de dados C foi SQL_C_BINARY ou SQL_C_CHAR; e o valor de comprimento do parâmetro era menor que 0, mas não foi SQL_NTS, SQL_NULL_DATA, SQL_DEFAULT_PARAM ou SQL_DATA_AT_EXEC ou menor ou igual a SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> Um valor de comprimento de parâmetro associado por **SQLBindParameter** foi definido como SQL_DATA_AT_EXEC; o tipo SQL foi SQL_LONGVARCHAR, SQL_LONGVARBINARY ou um tipo de dados específico da fonte de dados longa; e o tipo de informação SQL_NEED_LONG_DATA_LEN em **SQLGetInfo** era "Y".|  
|HY105|Tipo de parâmetro inválido|O valor especificado para o argumento *InputOutputType* em **SQLBindParameter** foi SQL_PARAM_OUTPUT e o parâmetro era um parâmetro de entrada.|  
|HY109|Posição do cursor inválida|A instrução preparada foi uma instrução UPDATE ou DELETE posicionada e o cursor foi posicionado (por **SQLSetPos** ou **SQLFetchScroll**) em uma linha que foi excluída ou não pôde ser buscada.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|A combinação das configurações atuais dos atributos de instrução SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE não era suportada pelo driver ou pela fonte de dados.<br /><br /> O atributo de instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE e o atributo de instrução SQL_ATTR_CURSOR_TYPE foi definido como um tipo de cursor para o qual o driver não dá suporte a indicadores.|  
|HYT00|Tempo limite esgotado|O período de tempo limite da consulta expirou antes que a fonte de dados retornasse o conjunto de resultados. O período de tempo limite é definido por meio de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *StatementHandle* não oferece suporte à função.|  
|IM017|A sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação for usado, a sondagem será desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesse identificador.|Se a chamada de função anterior no identificador retornar SQL_STILL_EXECUTING e se o modo de notificação estiver habilitado, **SQLCompleteAsync** deverá ser chamado na alça para executar o pós-processamento e concluir a operação.|  
  
 **SQLExecute** pode retornar qualquer SQLSTATE que possa ser retornado por **SQLPrepare**, com base em quando a fonte de dados avaliar a instrução SQL associada à instrução.  
  
## <a name="comments"></a>Comentários  
 **SQLExecute** executa uma instrução preparada por **SQLPrepare**. Depois que o aplicativo processa ou descarta os resultados de uma chamada para **SQLExecute**, o aplicativo pode chamar **SQLExecute** novamente com novos valores de parâmetro. Para obter mais informações sobre a execução preparada, consulte [execução preparada](../../../odbc/reference/develop-app/prepared-execution-odbc.md).  
  
 Para executar uma instrução **Select** mais de uma vez, o aplicativo deve chamar **SQLCloseCursor** antes de executar **novamente** a instrução SELECT.  
  
 Se a fonte de dados estiver no modo de confirmação manual (exigindo início de transação explícita) e uma transação ainda não tiver sido iniciada, o Driver iniciará uma transação antes de enviar a instrução SQL. Para obter mais informações, consulte [Transações](../../../odbc/reference/develop-app/transactions-odbc.md).  
  
 Se um aplicativo usar **SQLPrepare** para preparar e **SQLExecute** para enviar uma instrução **Commit** ou **Rollback** , ele não será interoperável entre os produtos DBMS. Para confirmar ou reverter uma transação, chame **SQLEndTran**.  
  
 Se **SQLExecute** encontrar um parâmetro de dados em execução, ele retornará SQL_NEED_DATA. O aplicativo envia os dados usando **SQLParamData** e **SQLPutData**. Consulte [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md), [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)e [enviando dados longos](../../../odbc/reference/develop-app/sending-long-data.md).  
  
 Se **SQLExecute** executar uma instrução UPDATE, INSERT ou DELETE pesquisada que não afete nenhuma linha na fonte de dados, a chamada para **SQLExecute** retornará SQL_NO_DATA.  
  
 Se o valor do atributo da instrução SQL_ATTR_PARAMSET_SIZE for maior que 1 e a instrução SQL contiver pelo menos um marcador de parâmetro, o **SQLExecute** executará a instrução SQL uma vez para cada conjunto de valores de parâmetro nas matrizes apontadas pelo argumento * \*ParameterValuePtr* nas chamadas para **SQLBindParameter**. Para obter mais informações, consulte [matrizes de valores de parâmetro](../../../odbc/reference/develop-app/arrays-of-parameter-values.md).  
  
 Se os indicadores estiverem habilitados e uma consulta for executada e não oferecer suporte a indicadores, o driver deverá tentar forçar o ambiente a um que dê suporte a indicadores alterando um valor de atributo e retornando SQLSTATE 01S02 (valor de opção alterado). Se o atributo não puder ser alterado, o driver deverá retornar SQLSTATE HY024 (valor de atributo inválido).  
  
> [!NOTE]  
>  Ao usar o pool de conexões, um aplicativo não deve executar instruções SQL que alteram o banco de dados ou o contexto do banco de dados, como a instrução **use** _Database_ no SQL Server, que altera o catálogo usado por uma fonte de dado.  
  
## <a name="code-example"></a>Exemplo de código  
 Consulte [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)e [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Associando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Fechando o cursor|[Função SQLCloseCursor](../../../odbc/reference/syntax/sqlclosecursor-function.md)|  
|Executando uma operação Commit ou ROLLBACK|[Função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|Executando uma instrução SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Buscando várias linhas de dados|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Buscando um bloco de dados ou rolando por meio de um conjunto de resultados|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Liberando um identificador de instrução|[Função SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Retornando um nome de cursor|[Função SQLGetCursorName](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|Buscando parte ou toda uma coluna de dados|[Função SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|Retornando o próximo parâmetro para o qual enviar dados|[Função SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|Preparando uma instrução para execução|[Função SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|Enviando dados de parâmetro em tempo de execução|[Função SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|Definindo um nome de cursor|[Função SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
|Definindo um atributo de instrução|[Função SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
