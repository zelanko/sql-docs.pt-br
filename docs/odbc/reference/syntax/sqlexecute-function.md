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
manager: craigg
ms.openlocfilehash: 08eb9db7645448157a76b3bcfdd302f6654f68f5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537253"
---
# <a name="sqlexecute-function"></a>Função SQLExecute
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 1.0 ODBC: ISO 92  
  
 **Resumo**  
 **SQLExecute** executa uma instrução preparada, usando os valores atuais das variáveis de marcador de parâmetro, se existir de qualquer marcador de parâmetro na instrução.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLExecute(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrução.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR, SQL_NO_DATA, SQL_INVALID_HANDLE ou SQL_PARAM_DATA_AVAILABLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLExecute** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *manipular* dos *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLExecute** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01001|Conflito de operação do cursor|A instrução preparada associada a *StatementHandle* contidos um posicionadas instrução update ou delete, e nenhuma linha ou mais de uma linha foram atualizadas ou excluídas. (Para obter mais informações sobre atualizações de mais de uma linha, consulte a descrição do SQL_ATTR_SIMULATE_CURSOR *atributo* na **SQLSetStmtAttr**.)<br /><br /> (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01003|Valor nulo eliminado na função de conjunto|A instrução preparada associada *StatementHandle* continha uma função de conjunto (como **AVG**, **MAX**, **MIN**e assim por diante), mas não o **contagem** definir função e o argumento nulo valores foram eliminados antes que a função foi aplicada. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres truncados à direita|Cadeia de caracteres ou dados binários retornados para um parâmetro de saída resultaram em truncamento de caractere não vazios ou nulos de dados binários. Se fosse um valor de cadeia de caracteres, ele era truncados à direita. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01006|Privilégio não revogado|A instrução preparada associada a *StatementHandle* foi uma **REVOGAR** instrução e o usuário não tem o privilégio especificado. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01007|Privilégio não concedido|A instrução preparada associada a *StatementHandle* foi uma **GRANT** instrução e o usuário não foi possível conceder o privilégio especificado.|  
|01S02|Valor de opção alterado|Um atributo de declaração especificada era inválido devido a condições de trabalho de implementação, portanto, um valor semelhante foi substituído temporariamente. (**SQLGetStmtAttr** pode ser chamado para determinar o que é o valor substituído temporariamente.) O valor de substituição é válido para o *StatementHandle* até que o cursor seja fechado, ponto em que o atributo de instrução será revertido para seu valor anterior. Os atributos de instrução que podem ser alterados são: SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_KEYSET_SIZE, SQL_ATTR_MAX_LENGTH, SQL_ATTR_MAX_ROWS, SQL_ATTR_QUERY_TIMEOUT, and SQL_ATTR_SIMULATE_CURSOR. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01S07|Truncamento fracionário|Os dados retornados para uma entrada/saída ou parâmetro de saída foi truncado de modo que a parte fracionária de um tipo de dados numéricos foi truncada ou a parte fracionária do componente de tempo de um hora, o carimbo de hora ou intervalo do tipo de dados foi truncada.<br /><br /> (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|07002|Campo COUNT incorreto|O número de parâmetros especificado na **SQLBindParameter** era menor do que o número de parâmetros na instrução SQL contidos em \* *StatementText*.<br /><br /> **SQLBindParameter** foi chamado com *ParameterValuePtr* definido como um ponteiro nulo, *StrLen_or_IndPtr* não é definido como SQL_NULL_DATA ou SQL_DATA_AT_EXEC, e *InputOutputType*  não é definido como SQL_PARAM_OUTPUT, para que o número de parâmetros especificado na **SQLBindParameter** era maior que o número de parâmetros na instrução SQL que está contido em **StatementText* .|  
|07006|Violação do atributo de tipo de dados restrito|O valor de dados identificado pela *ValueType* argumento **SQLBindParameter** para o parâmetro associado não pôde ser convertido para o tipo de dados identificado pelo *ParameterType*argumento na **SQLBindParameter**.<br /><br /> O valor dos dados retornados para um parâmetro associado como SQL_PARAM_INPUT_OUTPUT ou SQL_PARAM_OUTPUT não pôde ser convertido para o tipo de dados identificado pelo *ValueType* argumento **SQLBindParameter**.<br /><br /> (Se os valores de dados para uma ou mais linhas não pôde ser convertidos, mas uma ou mais linhas foram retornadas com êxito, essa função retorna SQL_SUCCESS_WITH_INFO).|  
|07007|Violação de valor de parâmetro restrito|O tipo de parâmetro SQL_PARAM_INPUT_OUTPUT_STREAM só é usado para um parâmetro que envia e recebe dados em partes. Um buffer de entrada associado não é permitido para esse tipo de parâmetro.<br /><br /> Esse erro ocorrerá quando o tipo de parâmetro for SQL_PARAM_INPUT_OUTPUT e quando o \* *StrLen_or_IndPtr* especificado no **SQLBindParameter** não é igual a SQL_NULL_DATA, SQL_DEFAULT_ PARAM, SQL_LEN_DATA_AT_EXEC(len) ou SQL_DATA_AT_EXEC.|  
|07S01|Uso inválido de parâmetro padrão|Um valor de parâmetro definido com **SQLBindParameter**, era SQL_DEFAULT_PARAM, e o parâmetro correspondente não era um parâmetro para uma invocação de procedimento canônica ODBC.|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|21S02|Grau da tabela derivada não corresponde à lista de colunas|A instrução preparada associada a *StatementHandle* contidos um **CREATE VIEW** instrução e a lista de colunas não-qualificados (o número de colunas especificado para o modo de exibição a  *Identificador de coluna* argumentos da instrução SQL) contidos nomes mais que o número de colunas na tabela derivada definida pelo *especificação de consulta* argumento da instrução SQL.|  
|22001|Dados de cadeia de caracteres, truncamento à direita|A atribuição de um caractere ou valor binário para uma coluna resultou em truncamento de não vazio (caractere) ou não nulo caracteres (binários) ou bytes.|  
|22002|Variável de indicador necessária, mas não fornecida|Dados nulos foi associados a um parâmetro de saída cujos *StrLen_or_IndPtr* definido por **SQLBindParameter** é um ponteiro nulo.|  
|22003|Valor numérico fora do intervalo|A instrução preparada associada a *StatementHandle* continha um parâmetro numérico associado e o valor do parâmetro causou a parte inteira (em vez de fracionários) o número a ser truncado quando atribuído ao coluna de tabela.<br /><br /> Retornar um valor numérico (como numérico ou cadeia de caracteres) para um ou mais parâmetros de entrada/saída ou de saída teria causado parte inteira (em vez de fracionários) o número a ser truncado.|  
|22007|Formato de data/hora inválido|A instrução preparada associada a *StatementHandle* continha uma instrução SQL que continha uma data, hora ou estrutura de carimbo de hora como um parâmetro associado, e o parâmetro foi, respectivamente, uma data inválida, hora, ou carimbo de hora.<br /><br /> Um parâmetro de entrada/saída ou de saída foi associado a uma data, hora ou estrutura de carimbo de hora C, e um valor no parâmetro retornado era, respectivamente, uma data inválida, hora ou carimbo de hora. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|22008|Estouro no campo de data e hora|A instrução preparada associada a *StatementHandle* independente de uma instrução SQL que continha uma expressão de data e hora que, quando calculada, resultou em uma data, hora ou carimbo de hora estrutura que era inválida.<br /><br /> Uma expressão de data e hora é calculado para uma entrada/saída ou parâmetro de saída resultou em uma data, hora ou estrutura de carimbo de hora C que era inválida.|  
|22012|Divisão por zero|A instrução preparada associada a *StatementHandle* continha uma expressão aritmética que causou a divisão por zero.<br /><br /> Uma expressão aritmética é calculado para uma entrada/saída ou parâmetro de saída que resultou na divisão por zero.|  
|22015|Estouro no campo de intervalo|*\*StatementText* continha um parâmetro numérico ou de intervalo exato que, quando convertido em um intervalo de tipo de dados SQL, causou uma perda de dígitos significativos.<br /><br /> *\*StatementText* continha um parâmetro de intervalo com mais de um campo que, quando convertido em um tipo de dados numéricos em uma coluna, não teve nenhuma representação no tipo de dados numérico.<br /><br /> *\*StatementText* continha dados de parâmetro que foi atribuídos a um intervalo de tipo SQL, e não havia nenhuma representação do valor do tipo C no intervalo de tipo SQL.<br /><br /> Atribuindo um parâmetro de entrada/saída ou de saída que era um numérico exato ou o intervalo de tipo SQL para um tipo de intervalo C causado uma perda de dígitos significativos.<br /><br /> Quando um parâmetro de entrada/saída ou de saída foi atribuído a uma estrutura de intervalo de C, não havia nenhuma representação dos dados na estrutura de dados de intervalo.|  
|22018|Valor de caractere inválido para especificação de conversão|*\*StatementText* continha um tipo de C que era um valor numérico exato ou aproximado, uma data e hora ou um tipo de dados de intervalo; o tipo SQL da coluna era um tipo de dados de caractere; e o valor na coluna não era um literal válido do tipo C associado.<br /><br /> Quando um parâmetro de entrada/saída ou de saída foi retornado, o tipo SQL era um valor numérico exato ou aproximado, uma data e hora ou um tipo de dados de intervalo; o tipo C foi SQL_C_CHAR; e o valor na coluna não era um literal válido do tipo SQL associado.|  
|22019|Caractere de escape inválido|A instrução preparada associada *StatementHandle* contidos um **como** predicado com um **ESCAPE** no **onde** cláusula, e o comprimento das seguintes opções de caractere de escape **ESCAPE** não era igual a 1.|  
|22025|Sequência de escape inválida|A instrução preparada associada *StatementHandle* contido "**como** _valor de padrão_ **ESCAPE** _escape caractere_"na **onde** cláusula e o caractere que segue o caractere de escape no valor padrão não era um dos"%"ou"_".|  
|23000|Violação de restrição de integridade|A instrução preparada associada a *StatementHandle* continha um parâmetro. O valor do parâmetro era nulo para uma coluna definida como NOT NULL na coluna da tabela associada, um valor duplicado foi fornecido para uma coluna restringida para conter apenas valores exclusivos ou alguma outra restrição de integridade foi violada.|  
|24000|Estado de cursor inválido|Um cursor é posicionado sobre o *StatementHandle* pela **SQLFetch** ou **SQLFetchScroll**. Esse erro é retornado pelo Gerenciador de Driver, se **SQLFetch** ou **SQLFetchScroll** não retornou SQL_NO_DATA e é retornado pelo driver se **SQLFetch** ou **SQLFetchScroll** tem retornar SQL_NO_DATA.<br /><br /> Um cursor foi aberto sobre o *StatementHandle*.<br /><br /> A instrução preparada associada a *StatementHandle* continha uma atualização posicionada ou exclusão statemen, t e o cursor estava posicionado antes do início do conjunto de resultados ou após o final do conjunto de resultados.|  
|40001|Falha na serialização|A transação foi revertida devido a um deadlock de recursos com outra transação.|  
|40003|Conclusão desconhecida de declaração|A conexão associada falhou durante a execução dessa função e o estado da transação não pode ser determinado.|  
|42000|Sintaxe ou violação de acesso|O usuário não tem permissão para executar a instrução preparada associada com o *StatementHandle*.|  
|44000|Violação COM OPÇÃO DE VERIFICAÇÃO|A instrução preparada associada *StatementHandle* continha um **inserir** instrução executada em uma tabela exibida ou uma tabela derivada da tabela exibida que foi criada, especificando **WITH CHECK OPTION**, de modo que uma ou mais linhas afetadas pela **inserir** instrução não estará presente na tabela exibida.<br /><br /> A instrução preparada associada a *StatementHandle* continha um **atualização** instrução executada em uma tabela exibida ou uma tabela derivada da tabela exibida que foi criada, especificando **WITH CHECK OPTION**, de modo que uma ou mais linhas afetadas pela **atualização** instrução não estará presente na tabela exibida.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** na  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente na *StatementHandle*.<br /><br /> A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativos multithread.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando o **SQLExecute** função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *StatementHandle* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada antes de dados foram recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) uma função de execução assíncrona (não desse último) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retornados de SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todos os parâmetros de dados em execução ou colunas.<br /><br /> (DM) a *StatementHandle* não foi preparado.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|Um valor de parâmetro definido com **SQLBindParameter**, era um ponteiro nulo, e o valor de parâmetro de comprimento não era 0, SQL_NULL_DATA, SQL_DATA_AT_EXEC, SQL_DEFAULT_PARAM, ou menor ou igual a SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> Um valor de parâmetro definido com **SQLBindParameter**, não era um ponteiro nulo; o tipo de dados C foi SQL_C_BINARY ou SQL_C_CHAR; e o valor de comprimento do parâmetro foi menor que 0 mas não era SQL_NTS, SQL_NULL_DATA, SQL_DEFAULT_PARAM ou SQL_DATA_ AT_EXEC, ou menor ou igual a SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> Um valor de comprimento do parâmetro associado ao **SQLBindParameter** foi definido como SQL_DATA_AT_EXEC; o tipo de SQL foi SQL_LONGVARCHAR, SQL_LONGVARBINARY, ou um tipo de dados específicos da fonte de dados long; e as informações de SQL_NEED_LONG_DATA_LEN Digite **SQLGetInfo** foi "Y".|  
|HY105|Tipo de parâmetro inválido|O valor especificado para o argumento *InputOutputType* na **SQLBindParameter** era SQL_PARAM_OUTPUT, e o parâmetro foi um parâmetro de entrada.|  
|HY109|Posição do cursor inválida|A instrução preparada era uma instrução de exclusão ou atualização posicionada, e o cursor é posicionado (por **SQLSetPos** ou **SQLFetchScroll**) em uma linha que tinha sido excluída ou não pôde ser buscada.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|A combinação das configurações atuais dos atributos de instrução SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE não era compatível com a driver ou fonte de dados.<br /><br /> O atributo da instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE, e o atributo SQL_ATTR_CURSOR_TYPE de instrução foi definido como um tipo de cursor para o qual o driver não oferece suporte a indicadores.|  
|HYT00|Tempo limite esgotado|O período de tempo limite da consulta expirou antes da fonte de dados retornou o conjunto de resultados. O período de tempo limite é definido por meio **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|O driver em (DM) associado a *StatementHandle* não suporta a função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem é desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior no identificador retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado no identificador de fazer o pós-processamento e concluir a operação.|  
  
 **SQLExecute** pode retornar qualquer SQLSTATE que pode ser retornado por **SQLPrepare**, com base em quando a fonte de dados avalia a instrução SQL associada à instrução.  
  
## <a name="comments"></a>Comentários  
 **SQLExecute** executa uma instrução preparada pelo **SQLPrepare**. Depois que o aplicativo processa ou descarta os resultados de uma chamada para **SQLExecute**, o aplicativo pode chamar **SQLExecute** novamente com novos valores de parâmetro. Para obter mais informações sobre a execução preparada, consulte [execução preparada](../../../odbc/reference/develop-app/prepared-execution-odbc.md).  
  
 Para executar uma **selecionar** instrução mais de uma vez, o aplicativo deve chamar **SQLCloseCursor** antes de ser o **selecione** instrução.  
  
 Se a fonte de dados está no modo de confirmação manual (exigir a iniciação de transação explícita) e uma transação já não tenha sido iniciada, o driver iniciará uma transação antes de enviar a instrução SQL. Para obter mais informações, consulte [transações](../../../odbc/reference/develop-app/transactions-odbc.md).  
  
 Se um aplicativo usa **SQLPrepare** para se preparar e **SQLExecute** para enviar um **confirmar** ou **REVERSÃO** instrução, ele não poderá ser interoperabilidade entre os produtos DBMS. Para confirmar ou reverter uma transação, chame **SQLEndTran**.  
  
 Se **SQLExecute** encontram um parâmetro de dados em execução, ele retornará SQL_NEED_DATA. O aplicativo envia os dados usando **SQLParamData** e **SQLPutData**. Ver [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md), [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md), e [enviando dados Long](../../../odbc/reference/develop-app/sending-long-data.md).  
  
 Se **SQLExecute** executa uma atualização pesquisada, uma inserção ou uma instrução delete que não afeta nenhuma linha na fonte de dados, a chamada para **SQLExecute** retorne SQL_NO_DATA.  
  
 Se o valor do atributo de instrução SQL_ATTR_PARAMSET_SIZE é maior que 1 e a instrução SQL contiver pelo menos um marcador de parâmetro, **SQLExecute** executa a instrução SQL, uma vez para cada conjunto de valores de parâmetro nas matrizes apontando para o  *\*ParameterValuePtr* argumento nas chamadas para **SQLBindParameter**. Para obter mais informações, consulte [matrizes de valores de parâmetro](../../../odbc/reference/develop-app/arrays-of-parameter-values.md).  
  
 Se os indicadores estão habilitados e uma consulta é executada que não é possível oferecer suporte a indicadores, o driver deve tentar forçar o ambiente para um que dá suporte a indicadores alterando um valor de atributo e retornando SQLSTATE 01S02 (valor de opção alterado). Se o atributo não pode ser alterado, o driver deve retornar SQLSTATE HY024 (valor de atributo inválido).  
  
> [!NOTE]  
>  Ao usar o pooling de conexão, um aplicativo não deve executar instruções SQL que alteram o banco de dados ou o contexto do banco de dados, como o **uso** _banco de dados_ instrução no SQL Server, que é alterado o catálogo usado por uma fonte de dados.  
  
## <a name="code-example"></a>Exemplo de código  
 Ver [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md), e [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Um buffer de associação a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Fechando o cursor|[Função SQLCloseCursor](../../../odbc/reference/syntax/sqlclosecursor-function.md)|  
|Executar uma operação de confirmação ou reversão|[Função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|Executar uma instrução SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Buscar várias linhas de dados|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Buscar um bloco de dados ou rolar por um resultado definido|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Liberando um identificador de instrução|[Função SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Retornando um nome de cursor|[Função SQLGetCursorName](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|Buscando parte ou toda uma coluna de dados|[Função SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|Retornar o próximo parâmetro para enviar dados|[Função SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|Como preparar uma instrução para execução|[Função SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|Enviar dados de parâmetro em tempo de execução|[Função SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|Configuração de um nome de cursor|[Função SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
|Definir um atributo de instrução|[Função SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
