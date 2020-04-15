---
title: Função SQLBulkOperations | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLBulkOperations
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBulkOperations
helpviewer_keywords:
- SQLBulkOperations function [ODBC]
ms.assetid: 7029d0da-b0f2-44e6-9114-50bd96f47196
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 61f4f294a6d84856bc3065b599a370bb5658e3ca
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301326"
---
# <a name="sqlbulkoperations-function"></a>Função SQLBulkOperations
**Conformidade**  
 Versão introduzida: ODBC 3.0 Normas Conformidade: ODBC  
  
 **Resumo**  
 **A SQLBulkOperations** executa inserções em massa e operações de marcação em massa, incluindo atualização, exclusão e busca por marcador.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLBulkOperations(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Operation);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Alça de declaração.  
  
 *Operação*  
 [Entrada] Operação a ser realizado:  
  
 SQL_ADD SQL_UPDATE_BY_BOOKMARK SQL_DELETE_BY_BOOKMARK SQL_FETCH_BY_BOOKMARK  
  
 Para obter mais informações, consulte "Comentários".  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **a SQLBulkOperations** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *alça* de *statementhandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados pela **SQLBulkOperations** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
 Para todos os SQLSTATEs que podem retornar SQL_SUCCESS_WITH_INFO ou SQL_ERROR (exceto 01xxx SQLSTATEs), SQL_SUCCESS_WITH_INFO é devolvido se ocorrer um erro em uma ou mais linhas, mas não todas, linhas de uma operação multirow, e SQL_ERROR é devolvida se ocorrer um erro em uma operação de linha única.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Truncação de dados de seqüência|O argumento *Operação* foi SQL_FETCH_BY_BOOKMARK, e os dados de seqüência ou binário retornados para uma coluna ou colunas com um tipo de SQL_C_CHAR ou SQL_C_BINARY resultaram na truncação de caracteres não em branco ou dados binários não-NULOS.|  
|01S01|Erro na linha|O argumento *da Operação* foi SQL_ADD, e um erro ocorreu em uma ou mais linhas durante a execução da operação, mas pelo menos uma linha foi adicionada com sucesso. (Função retorna SQL_SUCCESS_WITH_INFO.)<br /><br /> (Este erro só é levantado quando um aplicativo está trabalhando com um ODBC 2. *x* driver.)|  
|01S07|Truncação fracionada|O argumento *da Operação* era SQL_FETCH_BY_BOOKMARK, o tipo de dados do buffer do aplicativo não era SQL_C_CHAR ou SQL_C_BINARY, e os dados devolvidos aos buffers de aplicativos para uma ou mais colunas eram truncados. (Para os tipos de dados numéricos C, a parte fracionada do número foi truncada. Por tempo, carimbo de tempo e tipos de dados do intervalo C que contenham um componente de tempo, a parte fracionada do tempo foi truncada.)<br /><br /> (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|07006|Violação de atributo de tipo de dados restrito|O argumento *Operação* foi SQL_FETCH_BY_BOOKMARK, e o valor de dados de uma coluna no conjunto de resultados não pôde ser convertido para o tipo de dados especificado pelo argumento *TargetType* na chamada para **SQLBindCol**.<br /><br /> O argumento *Operação* foi SQL_UPDATE_BY_BOOKMARK ou SQL_ADD, e o valor dos dados nos buffers do aplicativo não pôde ser convertido para o tipo de dados de uma coluna no conjunto de resultados.|  
|07009|Índice de descritor inválido|O argumento *Operação* foi SQL_ADD, e uma coluna foi vinculada com um número de coluna maior do que o número de colunas no conjunto de resultados.|  
|21S02|Grau de tabela derivada não corresponde à lista de colunas|O argumento *operação* foi SQL_UPDATE_BY_BOOKMARK; e nenhuma coluna era updatable porque todas as colunas estavam desvinculadas ou somente leitura, ou o valor no buffer de comprimento/indicador de limite era SQL_COLUMN_IGNORE.|  
|22001|Truncação de dados de seqüência|A atribuição de um caractere ou valor binário para uma coluna no conjunto de resultados resultou na truncação de caracteres ou bytes não em branco (para caracteres) ou não nulos (para binários).|  
|22003|Valor numérico fora do alcance|O argumento *da Operação* foi SQL_ADD ou SQL_UPDATE_BY_BOOKMARK, e a atribuição de um valor numérico a uma coluna no conjunto de resultados fez com que a parte total (em oposição à fracionária) do número fosse truncada.<br /><br /> O argumento *operação* foi SQL_FETCH_BY_BOOKMARK, e devolver o valor numérico para uma ou mais colunas vinculadas teria causado uma perda de dígitos significativos.|  
|22007|Formato de data-hora inválido|O argumento *da Operação* foi SQL_ADD ou SQL_UPDATE_BY_BOOKMARK, e a atribuição de um valor de data ou carimbo de data para uma coluna no conjunto de resultados fez com que o campo de ano, mês ou dia ficasse fora de alcance.<br /><br /> O argumento *Operação* foi SQL_FETCH_BY_BOOKMARK, e devolver o valor de data ou carimbo de data para uma ou mais colunas vinculadas teria feito com que o campo de ano, mês ou dia estivesse fora de alcance.|  
|22008|Estouro do campo de data/hora|O argumento *da Operação* foi SQL_ADD ou SQL_UPDATE_BY_BOOKMARK, e o desempenho da aritmética data-hora sobre os dados enviados a uma coluna no conjunto de resultados resultou em um campo de data-hora (o ano, dia, hora, minuto ou segundo campo) do resultado que está fora da faixa de valores admissível para o campo ou sendo inválido com base nas regras naturais do calendário gregoriano para datas.<br /><br /> O argumento *da Operação* foi SQL_FETCH_BY_BOOKMARK, e o desempenho da aritmética data-hora sobre os dados recuperados do conjunto de resultados resultou em um campo de data (ano, mês, dia, hora, minuto ou segundo campo) do resultado que está fora da faixa de valores admissível para o campo ou sendo inválido com base nas regras naturais do calendário gregoriano para datas.|  
|22015|Estouro do campo de intervalo|O argumento *operação* foi SQL_ADD ou SQL_UPDATE_BY_BOOKMARK, e a atribuição de um tipo numérico exato ou de intervalo C para um tipo de dados SQL intervalado causou uma perda de dígitos significativos.<br /><br /> O argumento da *Operação* foi SQL_ADD ou SQL_UPDATE_BY_BOOKMARK; ao atribuir a um tipo SQL de intervalo, não houve representação do valor do tipo C no tipo SQL de intervalo.<br /><br /> O argumento *operação* foi SQL_FETCH_BY_BOOKMARK, e atribuir de um tipo sql numérico ou intervalado exato para um tipo de intervalo C causou uma perda de dígitos significativos no campo principal.<br /><br /> O argumento *da Operação* foi SQL_FETCH_BY_BOOKMARK; ao atribuir a um tipo de intervalo C, não houve representação do valor do tipo SQL no tipo C do intervalo.|  
|22018|Valor de caractere inválido para especificação do elenco|O argumento *da Operação* foi SQL_FETCH_BY_BOOKMARK; o tipo C era um numérico exato ou aproximado, um período de data ou um tipo de dados de intervalo; o tipo SQL da coluna era um tipo de dados de caracteres; e o valor na coluna não era um literal válido do tipo C ligado.<br /><br /> O argumento *Operação* foi SQL_ADD ou SQL_UPDATE_BY_BOOKMARK; o tipo SQL era um numérico exato ou aproximado, um período de data ou um tipo de dados de intervalo; o tipo C foi SQL_C_CHAR; e o valor na coluna não era um literal válido do tipo SQL vinculado.|  
|23000|Violação de restrição de integridade|O argumento da *Operação* foi SQL_ADD, SQL_DELETE_BY_BOOKMARK ou SQL_UPDATE_BY_BOOKMARK, e uma restrição de integridade foi violada.<br /><br /> O argumento *da Operação* foi SQL_ADD, e uma coluna que não estava vinculada é definida como NÃO NULA e não tem inadimplência.<br /><br /> O argumento *da Operação* foi SQL_ADD, o comprimento especificado no buffer *de StrLen_or_IndPtr* foi SQL_COLUMN_IGNORE, e a coluna não tinha um valor padrão.|  
|24.000|Estado de cursor inválido|O *StatementHandle* estava em um estado executado, mas nenhum conjunto de resultados foi associado ao *StatementHandle*.|  
|40001|Falha na serialização|A transação foi revertida por causa de um impasse de recursos com outra transação.|  
|40003|Conclusão de declaração desconhecida|A conexão associada falhou durante a execução desta função, e o estado da transação não pode ser determinado.|  
|42000|Erro de sintaxe ou violação de acesso|O motorista não conseguiu travar a linha conforme necessário para realizar a operação solicitada no argumento da *Operação.*|  
|44000|Violação COM OPÇÃO DE VERIFICAÇÃO|O argumento *Operação* foi SQL_ADD ou SQL_UPDATE_BY_BOOKMARK, e a inserção ou atualização foi realizada em uma tabela visualizada (ou uma tabela derivada da tabela visualizada) que foi criada especificando **COM OPÇÃO DE VERIFICAÇÃO,** de modo que uma ou mais linhas afetadas pela inserção ou atualização não estarão mais presentes na tabela visualizada.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e, antes de concluir a execução, **sqlCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **sqlCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um segmento diferente em um aplicativo multithread.|  
|HY010|Erro de seqüência de função|(DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *StatementHandle*. Esta função assíncrona ainda estava sendo executada quando a função **SQLBulkOperations** foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foram chamados para o *StatementHandle* e retornaram SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) O *StatementHandle* especificado não estava em um estado executado. A função foi chamada sem antes chamar **SQLExecDirect,** **SQLExecute**ou uma função de catálogo.<br /><br /> (DM) Uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect**ou **SQLSetPos** foram chamados para o *StatementHandle* e retornaram SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.<br /><br /> (DM) O motorista era um ODBC 2. *x* driver, e **SQLBulkOperations** foi chamado para um *StatementHandle* antes **de SQLFetchScroll** ou **SQLFetch** foi chamado.<br /><br /> (DM) **SQLBulkOperations** foi chamado depois que **sQLExtendedFetch** foi chamado no *StatementHandle*.|  
|HY011|Atributo não pode ser definido agora|(DM) O motorista era um ODBC 2. *x* driver, e o atributo de declaração SQL_ATTR_ROW_STATUS_PTR foi definido entre chamadas para **SQLFetch** ou **SQLFetchScroll** e **SQLBulkOperations**.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY090|Comprimento de seqüência ou buffer inválido|O argumento da *Operação* foi SQL_ADD ou SQL_UPDATE_BY_BOOKMARK; um valor de dados não era um ponteiro nulo; o tipo de dados C foi SQL_C_BINARY ou SQL_C_CHAR; e o valor do comprimento da coluna foi inferior a 0, mas não igual a SQL_DATA_AT_EXEC, SQL_COLUMN_IGNORE, SQL_NTS ou SQL_NULL_DATA, ou menor ou igual a SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> O valor em um buffer de comprimento/indicador foi SQL_DATA_AT_EXEC; o tipo SQL foi SQL_LONGVARCHAR, SQL_LONGVARBINARY ou um tipo de dados específico de origem de dados longos; e o SQL_NEED_LONG_DATA_LEN tipo de informação no **SQLGetInfo** foi "Y".<br /><br /> O argumento *da Operação* foi SQL_ADD, o atributo de declaração SQL_ATTR_USE_BOOKMARK foi definido para SQL_UB_VARIABLE, e a coluna 0 estava vinculada a um buffer cujo comprimento não era igual ao comprimento máximo do marcador para este conjunto de resultados. (Este comprimento está disponível no campo SQL_DESC_OCTET_LENGTH do IRD e pode ser obtido ligando para **SQLDescribeCol,** **SQLColAttribute**ou **SQLGetDescField**.)|  
|HY092|Identificador de atributo inválido|(DM) O valor especificado para o argumento da *Operação* era inválido.<br /><br /> O argumento da *Operação* foi SQL_ADD, SQL_UPDATE_BY_BOOKMARK ou SQL_DELETE_BY_BOOKMARK, e o atributo de declaração SQL_ATTR_CONCURRENCY foi definido para SQL_CONCUR_READ_ONLY.<br /><br /> O argumento *da Operação* era SQL_DELETE_BY_BOOKMARK, SQL_FETCH_BY_BOOKMARK ou SQL_UPDATE_BY_BOOKMARK, e a coluna de marcadores não estava vinculada ou o atributo de declaração SQL_ATTR_USE_BOOKMARKS foi definido para SQL_UB_OFF.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|O driver ou fonte de dados não suporta a operação solicitada no argumento da *Operação.*|  
|HYT00|Tempo limite esgotado|O período de tempo de consulta expirou antes que a fonte de dados retornasse o conjunto de resultados. O período de tempo é definido através **de SQLSetStmtAttr** com um argumento *de atributo* de SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *StatementHandle* não suporta a função.|  
|IM017|A votação é desativada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a votação é desativada.|  
|IM018|**O SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesta alça.|Se a chamada de função anterior na alça retornar SQL_STILL_EXECUTING e se o modo de notificação estiver ativado, o **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
  
> [!CAUTION]  
>  Para obter informações sobre quais afirmações, as **SQLBulkOperations** podem ser chamadas e o que deve fazer para compatibilidade com o ODBC 2. *x* aplicativos, consulte os [cursores de bloco, cursores roláveis e a](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) seção Retrocompatibilidade no apêndice G: Diretrizes do driver para compatibilidade retrógrada.  
  
 Um aplicativo usa **SQLBulkOperations** para executar as seguintes operações na tabela base ou exibição que corresponde à consulta atual:  
  
-   Adicione novas linhas.  
  
-   Atualize um conjunto de linhas onde cada linha é identificada por um marcador.  
  
-   Exclua um conjunto de linhas onde cada linha é identificada por um marcador.  
  
-   Busque um conjunto de linhas onde cada linha é identificada por um marcador.  
  
 Após uma chamada para **SQLBulkOperations,** a posição do cursor de bloco é indefinida. O aplicativo deve chamar **SQLFetchScroll** para definir a posição do cursor. Um aplicativo deve chamar **SQLFetchScroll** apenas com um argumento *FetchOrientation* de SQL_FETCH_FIRST, SQL_FETCH_LAST, SQL_FETCH_ABSOLUTE ou SQL_FETCH_BOOKMARK. A posição do cursor é indefinida se o aplicativo chama **SQLFetch** ou **SQLFetchScroll** com um argumento *FetchOrientation* de SQL_FETCH_PRIOR, SQL_FETCH_NEXT ou SQL_FETCH_RELATIVE.  
  
 Uma coluna pode ser ignorada em operações em massa realizadas por uma chamada para **SQLBulkOperations** definindo o buffer de comprimento/indicador da coluna especificado na chamada para **SQLBindCol**, para SQL_COLUMN_IGNORE.  
  
 Não é necessário que o aplicativo defina o atributo de declaração SQL_ATTR_ROW_OPERATION_PTR quando ele chama **SQLBulkOperations** porque as linhas não podem ser ignoradas ao executar operações em massa com esta função.  
  
 O buffer apontado pelo atributo de declaração SQL_ATTR_ROWS_FETCHED_PTR contém o número de linhas afetadas por uma chamada para **SQLBulkOperations**.  
  
 Quando o argumento *Operação* é SQL_ADD ou SQL_UPDATE_BY_BOOKMARK e a lista selecionada da especificação de consulta associada ao cursor contém mais de uma referência à mesma coluna, é definido pelo driver se um erro é gerado ou o motorista ignora as referências duplicadas e executa as operações solicitadas.  
  
 Para obter mais informações sobre como usar **o SQLBulkOperations,** consulte [Atualizar dados com sqlbulkoperations](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md).  
  
## <a name="performing-bulk-inserts"></a>Realizando inserções a granel  
 Para inserir dados com **sqlbulkoperations,** um aplicativo executa a seguinte seqüência de etapas:  
  
1.  Executa uma consulta que retorna um conjunto de resultados.  
  
2.  Define o SQL_ATTR_ROW_ARRAY_SIZE atributo de declaração ao número de linhas que deseja inserir.  
  
3.  Chama **o SQLBindCol** para vincular os dados que deseja inserir. Os dados estão vinculados a uma matriz com um tamanho igual ao valor de SQL_ATTR_ROW_ARRAY_SIZE.  
  
    > [!NOTE]  
    >  O tamanho da matriz apontada pelo atributo de declaração SQL_ATTR_ROW_STATUS_PTR deve ser igual a SQL_ATTR_ROW_ARRAY_SIZE ou SQL_ATTR_ROW_STATUS_PTR deve ser um ponteiro nulo.  
  
4.  Chama **SQLBulkOperations***(StatementHandle,* SQL_ADD) para realizar a inserção.  
  
5.  Se o aplicativo tiver definido o atributo de declaração SQL_ATTR_ROW_STATUS_PTR, ele poderá inspecionar esta matriz para ver o resultado da operação.  
  
 Se um aplicativo vincular a coluna 0 antes de chamar **SQLBulkOperations** com um argumento de *operação* de SQL_ADD, o driver atualizará os buffers da coluna 0 vinculada com os valores de marcador para a linha recém-inserida. Para que isso ocorra, o aplicativo deve ter definido o atributo de declaração SQL_ATTR_USE_BOOKMARKS para SQL_UB_VARIABLE antes de executar a declaração. (Isso não funciona com um ODBC 2. *x* driver.)  
  
 Dados longos podem ser adicionados em partes pelo SQLBulkOperations, usando chamadas para SQLParamData e SQLPutData. Para obter mais informações, consulte "Fornecendo dados longos para inserções e atualizações em massa" mais tarde nesta referência de função.  
  
 Não é necessário que o aplicativo chame **SQLFetch** ou **SQLFetchScroll** antes de chamar **SQLBulkOperations** (exceto quando for contra um ODBC 2.* x* driver; veja [Retrocompatibilidade e Conformidade de Padrões](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)).  
  
 O comportamento é definido pelo driver se **o SQLBulkOperations**, com um argumento de *Operação* de SQL_ADD, é chamado em um cursor que contém colunas duplicadas. O driver pode retornar um SQLSTATE definido pelo driver, adicionar os dados à primeira coluna que aparece no conjunto de resultados ou executar outro comportamento definido pelo driver.  
  
## <a name="performing-bulk-updates-by-using-bookmarks"></a>Realizando atualizações em massa usando marcadores  
 Para realizar atualizações em massa usando marcadores com **SQLBulkOperations,** um aplicativo executa as seguintes etapas em seqüência:  
  
1.  Define o atributo de declaração SQL_ATTR_USE_BOOKMARKS para SQL_UB_VARIABLE.  
  
2.  Executa uma consulta que retorna um conjunto de resultados.  
  
3.  Define o atributo de declaração SQL_ATTR_ROW_ARRAY_SIZE ao número de linhas que deseja atualizar.  
  
4.  Chama **o SQLBindCol** para vincular os dados que deseja atualizar. Os dados estão vinculados a uma matriz com um tamanho igual ao valor de SQL_ATTR_ROW_ARRAY_SIZE. Ele também chama **SQLBindCol** para vincular a coluna 0 (a coluna marcador).  
  
5.  Copia os marcadores para linhas que ele está interessado em atualizar na matriz vinculada à coluna 0.  
  
6.  Atualiza os dados nos buffers vinculados.  
  
    > [!NOTE]  
    >  O tamanho da matriz apontada pelo atributo de declaração SQL_ATTR_ROW_STATUS_PTR deve ser igual a SQL_ATTR_ROW_ARRAY_SIZE ou SQL_ATTR_ROW_STATUS_PTR deve ser um ponteiro nulo.  
  
7.  Chamadas **SQLBulkOperations**(*StatementHandle,* SQL_UPDATE_BY_BOOKMARK).  
  
    > [!NOTE]  
    >  Se o aplicativo tiver definido o atributo de declaração SQL_ATTR_ROW_STATUS_PTR, ele poderá inspecionar esta matriz para ver o resultado da operação.  
  
8.  Opcionalmente, chama **o SQLBulkOperations***(StatementHandle*, SQL_FETCH_BY_BOOKMARK) para buscar dados nos buffers de aplicativos vinculados para verificar se a atualização ocorreu.  
  
9. Se os dados forem atualizados, o driver altera o valor na matriz de status da linha para as linhas apropriadas para SQL_ROW_UPDATED.  
  
 Atualizações em massa realizadas pelo **SQLBulkOperations** podem incluir dados longos usando chamadas para **SQLParamData** e **SQLPutData**. Para obter mais informações, consulte "Fornecendo dados longos para inserções e atualizações em massa" mais tarde nesta referência de função.  
  
 Se os marcadores persistirem entre os cursores, o aplicativo não precisa chamar **SQLFetch** ou **SQLFetchScroll** antes de atualizar por marcadores. Ele pode usar marcadores que ele tenha armazenado de um cursor anterior. Se os marcadores não persistirem entre os cursores, o aplicativo deve chamar **SQLFetch** ou **SQLFetchScroll** para recuperar os marcadores.  
  
 O comportamento é definido pelo driver se **o SQLBulkOperations**, com um argumento de *Operação* de SQL_UPDATE_BY_BOOKMARK, é chamado em um cursor que contém colunas duplicadas. O driver pode retornar um SQLSTATE definido pelo driver, atualizar a primeira coluna que aparece no conjunto de resultados ou executar outro comportamento definido pelo driver.  
  
## <a name="performing-bulk-fetches-using-bookmarks"></a>Realizando buscas em massa usando marcadores  
 Para realizar buscas em massa usando marcadores com **SQLBulkOperations,** um aplicativo executa as seguintes etapas em seqüência:  
  
1.  Define o atributo de declaração SQL_ATTR_USE_BOOKMARKS para SQL_UB_VARIABLE.  
  
2.  Executa uma consulta que retorna um conjunto de resultados.  
  
3.  Define o SQL_ATTR_ROW_ARRAY_SIZE atributo de declaração ao número de linhas que deseja buscar.  
  
4.  Chama **o SQLBindCol** para vincular os dados que ele deseja buscar. Os dados estão vinculados a uma matriz com um tamanho igual ao valor de SQL_ATTR_ROW_ARRAY_SIZE. Ele também chama **SQLBindCol** para vincular a coluna 0 (a coluna marcador).  
  
5.  Copia os marcadores para linhas que ele está interessado em buscar na matriz vinculada à coluna 0. (Isso pressupõe que o aplicativo já obteve os marcadores separadamente.)  
  
    > [!NOTE]  
    >  O tamanho da matriz apontada pelo atributo de declaração SQL_ATTR_ROW_STATUS_PTR deve ser igual a SQL_ATTR_ROW_ARRAY_SIZE ou SQL_ATTR_ROW_STATUS_PTR deve ser um ponteiro nulo.  
  
6.  Chama **sqlbulkoperations***(StatementHandle,* SQL_FETCH_BY_BOOKMARK).  
  
7.  Se o aplicativo tiver definido o atributo de declaração SQL_ATTR_ROW_STATUS_PTR, ele poderá inspecionar esta matriz para ver o resultado da operação.  
  
 Se os marcadores persistirem entre os cursores, o aplicativo não precisa chamar **SQLFetch** ou **SQLFetchScroll** antes de buscar por marcadores. Ele pode usar marcadores que ele tenha armazenado de um cursor anterior. Se os marcadores não persistirem entre os cursores, o aplicativo deve chamar **SQLFetch** ou **SQLFetchScroll** uma vez para recuperar os marcadores.  
  
## <a name="performing-bulk-deletes-using-bookmarks"></a>Realizando exclusões em massa usando marcadores  
 Para realizar exclusões em massa usando marcadores com **SQLBulkOperations,** um aplicativo executa as seguintes etapas em seqüência:  
  
1.  Define o atributo de declaração SQL_ATTR_USE_BOOKMARKS para SQL_UB_VARIABLE.  
  
2.  Executa uma consulta que retorna um conjunto de resultados.  
  
3.  Define o atributo de declaração SQL_ATTR_ROW_ARRAY_SIZE ao número de linhas que deseja excluir.  
  
4.  Chama **SQLBindCol** para vincular a coluna 0 (a coluna marcador).  
  
5.  Copia os marcadores para linhas que ele está interessado em excluir na matriz vinculada à coluna 0.  
  
    > [!NOTE]  
    >  O tamanho da matriz apontada pelo atributo de declaração SQL_ATTR_ROW_STATUS_PTR deve ser igual a SQL_ATTR_ROW_ARRAY_SIZE ou SQL_ATTR_ROW_STATUS_PTR deve ser um ponteiro nulo.  
  
6.  Chamadas **SQLBulkOperations***(StatementHandle,* SQL_DELETE_BY_BOOKMARK).  
  
7.  Se o aplicativo tiver definido o atributo de declaração SQL_ATTR_ROW_STATUS_PTR, ele poderá inspecionar esta matriz para ver o resultado da operação.  
  
 Se os marcadores persistirem entre os cursores, o aplicativo não precisa chamar **SQLFetch** ou **SQLFetchScroll** antes de excluir por marcadores. Ele pode usar marcadores que ele tenha armazenado de um cursor anterior. Se os marcadores não persistirem entre os cursores, o aplicativo deve chamar **SQLFetch** ou **SQLFetchScroll** uma vez para recuperar os marcadores.  
  
## <a name="providing-long-data-for-bulk-inserts-and-updates"></a>Fornecendo dados longos para inserções e atualizações em massa  
 Dados longos podem ser fornecidos para inserções em massa e atualizações realizadas por chamadas para **SQLBulkOperations**. Para inserir ou atualizar dados longos, um aplicativo executa as seguintes etapas, além das etapas descritas nas seções "Realizando inserções em massa" e "Realizando atualizações em massa usando marcadores" anteriormente neste tópico.  
  
1.  Quando ele vincula os dados usando **o SQLBindCol,** o aplicativo coloca um valor definido pelo aplicativo, como o número da coluna, no buffer * \*TargetValuePtr* para colunas de dados em execução. O valor pode ser usado posteriormente para identificar a coluna.  
  
     O aplicativo coloca o resultado da macro SQL_LEN_DATA_AT_EXEC *(comprimento)* no * \** tampão StrLen_or_IndPtr. Se o tipo de dados SQL da coluna for SQL_LONGVARBINARY, SQL_LONGVARCHAR ou um tipo de dados específico de origem de dados longo e o driver retornar "Y" para o SQL_NEED_LONG_DATA_LEN tipo de informação no **SQLGetInfo,** *o comprimento* é o número de bytes de dados a serem enviados para o parâmetro; caso contrário, deve ser um valor não negativo e é ignorado.  
  
2.  Quando **o SQLBulkOperations** é chamado, se houver colunas de dados em execução, a função retorna SQL_NEED_DATA e segue para a etapa 3, que se segue. (Se não houver colunas de dados em execução, o processo será concluído.)  
  
3.  O aplicativo chama **sqlParamData** para recuperar o endereço do buffer * \*TargetValuePtr* para que a primeira coluna de dados em execução seja processada. **SQLParamData** retorna SQL_NEED_DATA. O aplicativo recupera o valor definido * \** pelo aplicativo a partir do buffer TargetValuePtr.  
  
    > [!NOTE]  
    >  Embora os parâmetros de data-at-execution se assemelham às colunas de dados em execução, o valor retornado pelo **SQLParamData** é diferente para cada um.  
  
     As colunas de dados em execução são colunas em um conjunto de linhas para os quais os dados serão enviados com **sQLPutData** quando uma linha é atualizada ou inserida com **sqlBulkOperations**. Eles estão ligados ao **SQLBindCol**. O valor retornado pelo **SQLParamData** é o endereço da linha no buffer ** TargetValuePtr* que está sendo processado.  
  
4.  O aplicativo chama **SQLPutData** uma ou mais vezes para enviar dados para a coluna. Mais de uma chamada é necessária se todo o valor de dados não puder ser retornado no buffer * \*TargetValuePtr* especificado no **SQLPutData**; várias chamadas para **SQLPutData** para a mesma coluna são permitidas apenas ao enviar dados c de caracteres para uma coluna com um tipo de dados específico de origem de caracteres, binários ou de origem de dados ou ao enviar dados C binários para uma coluna com um tipo de dados específico de origem de caracteres, binários ou de origem de dados.  
  
5.  O aplicativo chama **SQLParamData** novamente para sinalizar que todos os dados foram enviados para a coluna.  
  
    -   Se houver mais colunas de dados em execução, **o SQLParamData** retorna SQL_NEED_DATA e o endereço do buffer *TargetValuePtr* para que a próxima coluna data-at-execution seja processada. O aplicativo repete as etapas 4 e 5.  
  
    -   Se não houver mais colunas de dados em execução, o processo será concluído. Se a declaração foi executada com sucesso, **o SQLParamData** retorna SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO; se a execução falhar, ela retorna SQL_ERROR. Neste ponto, **o SQLParamData** pode retornar qualquer SQLSTATE que possa ser devolvido pela **SQLBulkOperations**.  
  
 Se a operação for cancelada ou ocorrer um erro no **SQLParamData** ou **no SQLPutData** após o **Retorno do SQLBulkOperations** SQL_NEED_DATA e antes que os dados sejam enviados para todas as colunas de dados em execução, o aplicativo pode chamar apenas **SQLCancel,** **SQLGetDiagField,** **SQLGetDiagRec,** **SQLGetFunctions,** **SQLParamData**ou **SQLPutData** para a declaração ou a conexão associada à declaração. Se ele chamar qualquer outra função para a declaração ou a conexão associada à declaração, a função retorna SQL_ERROR e SQLSTATE HY010 (erro de seqüência de função).  
  
 Se o aplicativo chamar **SQLCancel** enquanto o driver ainda precisa de dados para colunas de dados em execução, o driver cancelará a operação. O aplicativo pode então chamar **sqlbulkoperations** novamente; o cancelamento não afeta o estado do cursor ou a posição atual do cursor.  
  
## <a name="row-status-array"></a>Matriz de status da linha  
 A matriz de status da linha contém valores de status para cada linha de dados no conjunto de linhas após uma chamada para **SQLBulkOperations**. O driver define os valores de status nesta matriz após uma chamada para **SQLFetch,** **SQLFetchScroll,** **SQLSetPos**ou **SQLBulkOperations**. Esta matriz é inicialmente preenchida por uma chamada para **SQLBulkOperations** se **SQLFetch** ou **SQLFetchScroll** não tiver sido chamado antes **do SQLBulkOperations**. Esta matriz é apontada pelo atributo de declaração SQL_ATTR_ROW_STATUS_PTR. O número de elementos nas matrizes de status da linha deve ser igual ao número de linhas no conjunto de linhas (conforme definido pelo atributo de declaração SQL_ATTR_ROW_ARRAY_SIZE). Para obter informações sobre essa matriz de status de linha, consulte [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
## <a name="code-example"></a>Exemplo de código  
 O exemplo a seguir busca 10 linhas de dados por vez da tabela Clientes. Em seguida, ele solicita ao usuário uma ação a ser tomada. Para reduzir o tráfego de rede, o exemplo de buffer atualiza, exclui e insere localmente nos arrays vinculados, mas em deslocamentos passados os dados do conjunto de linhas. Quando o usuário opta por enviar atualizações, exclusões e inserções na fonte de dados, o código define a compensação de vinculação adequadamente e chama **SQLBulkOperations**. Para simplificar, o usuário não pode tamponar mais de 10 atualizações, exclusões ou inserções.  
  
```cpp  
// SQLBulkOperations_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqlext.h>  
#include "stdio.h"  
  
#define UPDATE_ROW 100  
#define DELETE_ROW 101  
#define ADD_ROW 102  
#define SEND_TO_DATA_SOURCE 103  
#define UPDATE_OFFSET 10  
#define INSERT_OFFSET 20  
#define DELETE_OFFSET 30  
  
// Define structure for customer data (assume 10 byte maximum bookmark size).  
typedef struct tagCustStruct {  
   SQLCHAR Bookmark[10];  
   SQLINTEGER BookmarkLen;  
   SQLUINTEGER CustomerID;  
   SQLINTEGER CustIDInd;  
   SQLCHAR CompanyName[51];  
   SQLINTEGER NameLenOrInd;  
   SQLCHAR Address[51];  
   SQLINTEGER AddressLenOrInd;  
   SQLCHAR Phone[11];  
   SQLINTEGER PhoneLenOrInd;  
} CustStruct;  
  
// Allocate 40 of these structures. Elements 0-9 are for the current rowset,  
// elements 10-19 are for the buffered updates, elements 20-29 are for  
// the buffered inserts, and elements 30-39 are for the buffered deletes.  
CustStruct CustArray[40];  
SQLUSMALLINT RowStatusArray[10], Action, RowNum, NumUpdates = 0, NumInserts = 0,  
NumDeletes = 0;  
SQLLEN BindOffset = 0;  
SQLRETURN retcode;  
SQLHENV henv = NULL;  
SQLHDBC hdbc = NULL;  
SQLHSTMT hstmt = NULL;  
  
int main() {  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   // Set the following statement attributes:  
   // SQL_ATTR_CURSOR_TYPE:           Keyset-driven  
   // SQL_ATTR_ROW_BIND_TYPE:         Row-wise  
   // SQL_ATTR_ROW_ARRAY_SIZE:        10  
   // SQL_ATTR_USE_BOOKMARKS:         Use variable-length bookmarks  
   // SQL_ATTR_ROW_STATUS_PTR:        Points to RowStatusArray  
   // SQL_ATTR_ROW_BIND_OFFSET_PTR:   Points to BindOffset  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_CURSOR_TYPE, (SQLPOINTER)SQL_CURSOR_KEYSET_DRIVEN, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_TYPE, (SQLPOINTER)sizeof(CustStruct), 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)10, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_USE_BOOKMARKS, (SQLPOINTER)SQL_UB_VARIABLE, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_OFFSET_PTR, &BindOffset, 0);  
  
   // Bind arrays to the bookmark, CustomerID, CompanyName, Address, and Phone columns.  
   retcode = SQLBindCol(hstmt, 0, SQL_C_VARBOOKMARK, CustArray[0].Bookmark, sizeof(CustArray[0].Bookmark), &CustArray[0].BookmarkLen);  
   retcode = SQLBindCol(hstmt, 1, SQL_C_ULONG, &CustArray[0].CustomerID, 0, &CustArray[0].CustIDInd);  
   retcode = SQLBindCol(hstmt, 2, SQL_C_CHAR, CustArray[0].CompanyName, sizeof(CustArray[0].CompanyName), &CustArray[0].NameLenOrInd);  
   retcode = SQLBindCol(hstmt, 3, SQL_C_CHAR, CustArray[0].Address, sizeof(CustArray[0].Address), &CustArray[0].AddressLenOrInd);  
   retcode = SQLBindCol(hstmt, 4, SQL_C_CHAR, CustArray[0].Phone, sizeof(CustArray[0].Phone), &CustArray[0].PhoneLenOrInd);  
  
   // Execute a statement to retrieve rows from the Customers table.  
   retcode = SQLExecDirect(hstmt, (SQLCHAR*)"SELECT CustomerID, CompanyName, Address, Phone FROM Customers", SQL_NTS);  
  
   // Fetch and display the first 10 rows.  
   retcode = SQLFetchScroll(hstmt, SQL_FETCH_NEXT, 0);  
   // DisplayCustData(CustArray, 10);  
  
   // Call GetAction to get an action and a row number from the user.  
   // while (GetAction(&Action, &RowNum)) {  
   Action = SQL_FETCH_NEXT;  
   RowNum = 2;  
   switch (Action) {  
      case SQL_FETCH_NEXT:  
      case SQL_FETCH_PRIOR:  
      case SQL_FETCH_FIRST:  
      case SQL_FETCH_LAST:  
      case SQL_FETCH_ABSOLUTE:  
      case SQL_FETCH_RELATIVE:  
         // Fetch and display the requested data.  
         SQLFetchScroll(hstmt, Action, RowNum);  
         // DisplayCustData(CustArray, 10);  
         break;  
  
      case UPDATE_ROW:  
         // Check if we have reached the maximum number of buffered updates.  
         if (NumUpdates < 10) {  
            // Get the new customer data and place it in the next available element of  
            // the buffered updates section of CustArray, copy the bookmark of the row  
            // being updated to the same element, and increment the update counter.  
            // Checking to see we have not already buffered an update for this  
            // row not shown.  
            // GetNewCustData(CustArray, UPDATE_OFFSET + NumUpdates);  
            memcpy(CustArray[UPDATE_OFFSET + NumUpdates].Bookmark,  
               CustArray[RowNum - 1].Bookmark,  
               CustArray[RowNum - 1].BookmarkLen);  
            CustArray[UPDATE_OFFSET + NumUpdates].BookmarkLen =  
               CustArray[RowNum - 1].BookmarkLen;  
            NumUpdates++;  
         } else {  
            printf("Buffers full. Send buffered changes to the data source.");  
         }  
         break;  
      case DELETE_ROW:  
         // Check if we have reached the maximum number of buffered deletes.  
         if (NumDeletes < 10) {  
            // Copy the bookmark of the row being deleted to the next available element  
            // of the buffered deletes section of CustArray and increment the delete  
            // counter. Checking to see we have not already buffered an update for  
            // this row not shown.  
            memcpy(CustArray[DELETE_OFFSET + NumDeletes].Bookmark,  
               CustArray[RowNum - 1].Bookmark,  
               CustArray[RowNum - 1].BookmarkLen);  
  
            CustArray[DELETE_OFFSET + NumDeletes].BookmarkLen =  
               CustArray[RowNum - 1].BookmarkLen;  
  
            NumDeletes++;  
         } else  
            printf("Buffers full. Send buffered changes to the data source.");  
         break;  
  
      case ADD_ROW:  
         // reached maximum number of buffered inserts?  
         if (NumInserts < 10) {  
            // Get the new customer data and place it in the next available element of  
            // the buffered inserts section of CustArray and increment insert counter.  
            // GetNewCustData(CustArray, INSERT_OFFSET + NumInserts);  
            NumInserts++;  
         } else  
            printf("Buffers full. Send buffered changes to the data source.");  
         break;  
  
      case SEND_TO_DATA_SOURCE:  
         // If there are any buffered updates, inserts, or deletes, set the array size  
         // to that number, set the binding offset to use the data in the buffered  
         // update, insert, or delete part of CustArray, and call SQLBulkOperations to  
         // do the updates, inserts, or deletes. Because we will never have more than  
         // 10 updates, inserts, or deletes, we can use the same row status array.  
         if (NumUpdates) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)NumUpdates, 0);  
            BindOffset = UPDATE_OFFSET * sizeof(CustStruct);  
            SQLBulkOperations(hstmt, SQL_UPDATE_BY_BOOKMARK);  
            NumUpdates = 0;  
         }  
  
         if (NumInserts) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)NumInserts, 0);  
            BindOffset = INSERT_OFFSET * sizeof(CustStruct);  
            SQLBulkOperations(hstmt, SQL_ADD);  
            NumInserts = 0;  
         }  
  
         if (NumDeletes) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)NumDeletes, 0);  
            BindOffset = DELETE_OFFSET * sizeof(CustStruct);  
            SQLBulkOperations(hstmt, SQL_DELETE_BY_BOOKMARK);  
            NumDeletes = 0;  
         }  
  
         // If there were any updates, inserts, or deletes, reset the binding offset  
         // and array size to their original values.  
         if (NumUpdates || NumInserts || NumDeletes) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)10, 0);  
            BindOffset = 0;  
         }  
         break;  
   }  
   // }  
  
   // Close the cursor.  
   SQLFreeStmt(hstmt, SQL_CLOSE);  
}  
```  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Vinculando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelamento do processamento de declarações|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Buscar um bloco de dados ou rolar através de um conjunto de resultados|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Obtendo um único campo de um descritor|[Função SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Obtendo vários campos de um descritor|[Função SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Definindo um único campo de um descritor|[Função SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Definindo vários campos de um descritor|[Função SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|Posicionando o cursor, atualizando dados no conjunto de linhas ou atualizando ou excluindo dados no conjunto de linhas|[Função SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|Definindo um atributo de declaração|[Função SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
