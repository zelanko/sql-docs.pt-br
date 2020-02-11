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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 60bcb6851adeba08105dabd6fb0800d2e969a04e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68343176"
---
# <a name="sqlbulkoperations-function"></a>Função SQLBulkOperations
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 3,0: ODBC  
  
 **Resumo**  
 O **SQLBulkOperations** executa inserções em massa e operações de marcador em massa, incluindo atualizar, excluir e buscar por indicador.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLBulkOperations(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Operation);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 Entrada Identificador de instrução.  
  
 *Operação*  
 Entrada Operação a ser executada:  
  
 SQL_ADD SQL_UPDATE_BY_BOOKMARK SQL_DELETE_BY_BOOKMARK SQL_FETCH_BY_BOOKMARK  
  
 Para obter mais informações, consulte "Comentários".  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLBulkOperations** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *identificador* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLBulkOperations** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
 Para todos os hiperestados que podem retornar SQL_SUCCESS_WITH_INFO ou SQL_ERROR (exceto 01xxx sqlstates), SQL_SUCCESS_WITH_INFO será retornado se ocorrer um erro em uma ou mais, mas não em todas as linhas de uma operação multirow, e SQL_ERROR será retornado se ocorrer um erro em um operação de linha única.  
  
|SQLSTATE|Erro|DESCRIÇÃO|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Truncamento direito de dados de cadeia de caracteres|O argumento da *operação* foi SQL_FETCH_BY_BOOKMARK, e os dados de cadeia de caracteres ou binários retornados para uma coluna ou colunas com um tipo de dados de SQL_C_CHAR ou SQL_C_BINARY resultaram no truncamento de um caractere não em branco ou dados binários não nulos.|  
|01S01|Erro na linha|O argumento da *operação* foi SQL_ADD e ocorreu um erro em uma ou mais linhas ao executar a operação, mas pelo menos uma linha foi adicionada com êxito. (A função retorna SQL_SUCCESS_WITH_INFO.)<br /><br /> (Esse erro é gerado somente quando um aplicativo está trabalhando com um ODBC 2. Driver *x* .)|  
|01S07|Truncamento fracionário|O argumento de *operação* foi SQL_FETCH_BY_BOOKMARK, o tipo de dados do buffer de aplicativo não foi SQL_C_CHAR ou SQL_C_BINARY e os dados retornados aos buffers de aplicativo para uma ou mais colunas foram truncados. (Para tipos de dados C numéricos, a parte fracionária do número foi truncada. Para os tipos de dados time, timestamp e Interval C que contêm um componente de tempo, a parte fracionária do tempo foi truncada.)<br /><br /> (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|07006|Violação de atributo de tipo de dados restrito|O argumento de *operação* foi SQL_FETCH_BY_BOOKMARK, e o valor de dados de uma coluna no conjunto de resultados não pôde ser convertido para o tipo de dados especificado pelo argumento *TargetType* na chamada para **SQLBindCol**.<br /><br /> O argumento da *operação* foi SQL_UPDATE_BY_BOOKMARK ou SQL_ADD, e o valor dos dados nos buffers do aplicativo não pôde ser convertido para o tipo de dados de uma coluna no conjunto de resultados.|  
|07009|Índice de descritor inválido|A *operação* de argumento foi SQL_ADD e uma coluna foi associada a um número de coluna maior que o número de colunas no conjunto de resultados.|  
|21S02|O grau da tabela derivada não corresponde à lista de colunas|A *operação* de argumento foi SQL_UPDATE_BY_BOOKMARK; e nenhuma coluna era atualizável porque todas as colunas estavam desvinculadas ou somente leitura ou o valor no buffer de comprimento/indicador de limite foi SQL_COLUMN_IGNORE.|  
|22001|Truncamento direito de dados de cadeia de caracteres|A atribuição de um valor de caractere ou binário a uma coluna no conjunto de resultados resultou no truncamento de caracteres não vazios (para caracteres) ou não nulos (para binário) ou bytes.|  
|22003|Valor numérico fora do intervalo|O argumento da *operação* foi SQL_ADD ou SQL_UPDATE_BY_BOOKMARK, e a atribuição de um valor numérico a uma coluna no conjunto de resultados causou a truncamento da parte inteira (em oposição à fracionária) do número.<br /><br /> A *operação* de argumento foi SQL_FETCH_BY_BOOKMARK e o retorno do valor numérico de uma ou mais colunas associadas causaria uma perda de dígitos significativos.|  
|22007|Formato de data e hora inválido|O argumento da *operação* foi SQL_ADD ou SQL_UPDATE_BY_BOOKMARK, e a atribuição de um valor de data ou timestamp a uma coluna no conjunto de resultados fez com que o campo ano, mês ou dia estivesse fora do intervalo.<br /><br /> A *operação* de argumento foi SQL_FETCH_BY_BOOKMARK e retornando o valor de data ou timestamp para uma ou mais colunas associadas teria feito com que o campo ano, mês ou dia estivesse fora do intervalo.|  
|22008|Estouro de campo de data/hora|O argumento da *operação* foi SQL_ADD ou SQL_UPDATE_BY_BOOKMARK e o desempenho da aritmética de DateTime nos dados enviados para uma coluna no conjunto de resultados resultou em um campo DateTime (o campo year, month, Day, hour, minute ou Second) do resultado que está fora do intervalo permitido de valores para o campo ou sendo inválido com base nas regras naturais do calendário gregoriano para DateTimes.<br /><br /> O argumento da *operação* foi SQL_FETCH_BY_BOOKMARK, e o desempenho da aritmética de DateTime nos dados que estão sendo recuperados do conjunto de resultados resultou em um campo DateTime (ano, mês, dia, hora, minuto ou segundo campo) do resultado que está fora do intervalo permitido de valores para o campo ou sendo inválido com base nas regras naturais do calendário gregoriano para DateTimes.|  
|22015|Estouro no campo de intervalo|O argumento da *operação* foi SQL_ADD ou SQL_UPDATE_BY_BOOKMARK e a atribuição de um tipo numérico exato ou de C de intervalo a um tipo de dados SQL de intervalo causou uma perda de dígitos significativos.<br /><br /> O argumento da *operação* foi SQL_ADD ou SQL_UPDATE_BY_BOOKMARK; ao atribuir a um tipo SQL de intervalo, não havia nenhuma representação do valor do tipo C no tipo SQL de intervalo.<br /><br /> O argumento de *operação* foi SQL_FETCH_BY_BOOKMARK e a atribuição de um tipo de SQL numérico ou de intervalo exato a um tipo de intervalo C causou uma perda de dígitos significativos no campo à esquerda.<br /><br /> O argumento da *operação* foi SQL_FETCH_BY_BOOKMARK; ao atribuir a um tipo de intervalo C, não havia nenhuma representação do valor do tipo SQL no tipo de intervalo C.|  
|22018|Valor de caractere inválido para especificação de conversão|O argumento da *operação* foi SQL_FETCH_BY_BOOKMARK; o tipo C era um tipo de dados numérico exato ou aproximado, um DateTime ou um intervalo; o tipo SQL da coluna era um tipo de dados de caractere; e o valor na coluna não era um literal válido do tipo associado de C.<br /><br /> A *operação* de argumento foi SQL_ADD ou SQL_UPDATE_BY_BOOKMARK; o tipo SQL era um tipo de dados numérico exato ou aproximado, um DateTime ou um intervalo; o tipo C foi SQL_C_CHAR; e o valor na coluna não era um literal válido do tipo SQL associado.|  
|23000|Violação de restrição de integridade|O argumento da *operação* foi SQL_ADD, SQL_DELETE_BY_BOOKMARK ou SQL_UPDATE_BY_BOOKMARK e uma restrição de integridade foi violada.<br /><br /> O argumento da *operação* foi SQL_ADD e uma coluna que não foi associada está definida como NOT NULL e não tem padrão.<br /><br /> O argumento de *operação* foi SQL_ADD, o comprimento especificado no buffer de *StrLen_or_IndPtr* associado foi SQL_COLUMN_IGNORE e a coluna não tinha um valor padrão.|  
|24.000|Estado de cursor inválido|O *StatementHandle* estava em um estado executado, mas nenhum conjunto de resultados foi associado ao *StatementHandle*.|  
|40001|Falha de serialização|A transação foi revertida devido a um deadlock de recurso com outra transação.|  
|40003|Conclusão de instrução desconhecida|A conexão associada falhou durante a execução dessa função, e o estado da transação não pode ser determinado.|  
|42000|Erro de sintaxe ou violação de acesso|O driver não pôde bloquear a linha conforme necessário para executar a operação solicitada no argumento de *operação* .|  
|44000|Violação COM OPÇÃO DE VERIFICAÇÃO|O argumento da *operação* foi SQL_ADD ou SQL_UPDATE_BY_BOOKMARK e a inserção ou atualização foi executada em uma tabela exibida (ou uma tabela derivada da tabela exibida) que foi criada ESPECIFICANDO **with check option**, de forma que uma ou mais linhas afetadas pela inserção ou atualização não estarão mais presentes na tabela exibida.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \*MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativo multithread.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *StatementHandle*. Esta função assíncrona ainda estava em execução quando a função **SQLBulkOperations** foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para *StatementHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) o *StatementHandle* especificado não estava em um estado executado. A função foi chamada sem primeiro chamar **SQLExecDirect**, **SQLExecute**ou uma função de catálogo.<br /><br /> (DM) uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**ou **SQLSetPos** foi chamado para *StatementHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.<br /><br /> (DM) o driver era um ODBC 2. o driver *x* e **SQLBulkOperations** foi chamado para um *StatementHandle* antes de **SQLFetchScroll** ou **SQLFetch** ser chamado.<br /><br /> (DM) **SQLBulkOperations** foi chamado depois que **SQLExtendedFetch** foi chamado no *StatementHandle*.|  
|HY011|O atributo não pode ser definido agora|(DM) o driver era um ODBC 2. *x* , e o atributo de instrução SQL_ATTR_ROW_STATUS_PTR foi definido entre as chamadas para **SQLFetch** ou **SQLFetchScroll** e **SQLBulkOperations**.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|O argumento da *operação* foi SQL_ADD ou SQL_UPDATE_BY_BOOKMARK; um valor de dados não era um ponteiro nulo; o tipo de dados C foi SQL_C_BINARY ou SQL_C_CHAR; e o valor de comprimento da coluna era menor que 0, mas não é igual a SQL_DATA_AT_EXEC, SQL_COLUMN_IGNORE, SQL_NTS ou SQL_NULL_DATA ou menor ou igual a SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> O valor em um buffer de comprimento/indicador foi SQL_DATA_AT_EXEC; o tipo SQL foi SQL_LONGVARCHAR, SQL_LONGVARBINARY ou um tipo de dados específico da fonte de dados longa; e o tipo de informação SQL_NEED_LONG_DATA_LEN em **SQLGetInfo** era "Y".<br /><br /> O argumento da *operação* foi SQL_ADD, o atributo da instrução SQL_ATTR_USE_BOOKMARK foi definido como SQL_UB_VARIABLE e a coluna 0 estava associada a um buffer cujo comprimento não era igual ao tamanho máximo do indicador para esse conjunto de resultados. (Esse comprimento está disponível no campo SQL_DESC_OCTET_LENGTH do IRD e pode ser obtido chamando **SQLDescribeCol**, **SQLColAttribute**ou **SQLGetDescField**.)|  
|HY092|Identificador de atributo inválido|(DM) o valor especificado para o argumento de *operação* era inválido.<br /><br /> O argumento de *operação* foi SQL_ADD, SQL_UPDATE_BY_BOOKMARK ou SQL_DELETE_BY_BOOKMARK e o atributo de instrução SQL_ATTR_CONCURRENCY foi definido como SQL_CONCUR_READ_ONLY.<br /><br /> O argumento de *operação* foi SQL_DELETE_BY_BOOKMARK, SQL_FETCH_BY_BOOKMARK ou SQL_UPDATE_BY_BOOKMARK, e a coluna de indicadores não foi associada ou o atributo de instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_OFF.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|O driver ou a fonte de dados não oferece suporte à operação solicitada no argumento de *operação* .|  
|HYT00|Tempo limite esgotado|O período de tempo limite da consulta expirou antes que a fonte de dados retornasse o conjunto de resultados. O período de tempo limite é definido por meio de **SQLSetStmtAttr** com um argumento de *atributo* de SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *StatementHandle* não oferece suporte à função.|  
|IM017|A sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação for usado, a sondagem será desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesse identificador.|Se a chamada de função anterior no identificador retornar SQL_STILL_EXECUTING e se o modo de notificação estiver habilitado, **SQLCompleteAsync** deverá ser chamado na alça para executar o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
  
> [!CAUTION]  
>  Para obter informações sobre como os Estados de instrução **SQLBulkOperations** podem ser chamados e o que ele deve fazer para compatibilidade com o ODBC 2. aplicativos *x* , consulte a seção [cursores de bloco, cursores roláveis e compatibilidade com versões anteriores](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) no apêndice G: diretrizes de driver para compatibilidade com versões anteriores.  
  
 Um aplicativo usa **SQLBulkOperations** para executar as seguintes operações na tabela base ou exibição que corresponde à consulta atual:  
  
-   Adicionar novas linhas.  
  
-   Atualizar um conjunto de linhas em que cada linha é identificada por um indicador.  
  
-   Excluir um conjunto de linhas em que cada linha é identificada por um indicador.  
  
-   Busque um conjunto de linhas em que cada linha é identificada por um indicador.  
  
 Após uma chamada para **SQLBulkOperations**, a posição do cursor de bloco é indefinida. O aplicativo precisa chamar **SQLFetchScroll** para definir a posição do cursor. Um aplicativo deve chamar **SQLFetchScroll** somente com um argumento *FetchOrientation* de SQL_FETCH_FIRST, SQL_FETCH_LAST, SQL_FETCH_ABSOLUTE ou SQL_FETCH_BOOKMARK. A posição do cursor será indefinida se o aplicativo chamar **SQLFetch** ou **SQLFetchScroll** com um argumento *FetchOrientation* de SQL_FETCH_PRIOR, SQL_FETCH_NEXT ou SQL_FETCH_RELATIVE.  
  
 Uma coluna pode ser ignorada em operações em massa executadas por uma chamada para **SQLBulkOperations** definindo o tamanho da coluna/buffer do indicador especificado na chamada para **SQLBindCol**, para SQL_COLUMN_IGNORE.  
  
 Não é necessário que o aplicativo defina o atributo de instrução SQL_ATTR_ROW_OPERATION_PTR ao chamar **SQLBulkOperations** porque as linhas não podem ser ignoradas ao executar operações em massa com essa função.  
  
 O buffer apontado pelo atributo instrução SQL_ATTR_ROWS_FETCHED_PTR contém o número de linhas afetadas por uma chamada para **SQLBulkOperations**.  
  
 Quando o argumento da *operação* é SQL_ADD ou SQL_UPDATE_BY_BOOKMARK e a lista de seleção da especificação de consulta associada ao cursor contém mais de uma referência à mesma coluna, é definido pelo driver se um erro é gerado ou o driver ignora as referências duplicadas e executa as operações solicitadas.  
  
 Para obter mais informações sobre como usar o **SQLBulkOperations**, consulte [atualizando dados com o SQLBulkOperations](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md).  
  
## <a name="performing-bulk-inserts"></a>Executando inserções em massa  
 Para inserir dados com o **SQLBulkOperations**, um aplicativo executa a seguinte sequência de etapas:  
  
1.  Executa uma consulta que retorna um conjunto de resultados.  
  
2.  Define o atributo de instrução SQL_ATTR_ROW_ARRAY_SIZE como o número de linhas que deseja inserir.  
  
3.  Chama **SQLBindCol** para associar os dados que deseja inserir. Os dados são associados a uma matriz com um tamanho igual ao valor de SQL_ATTR_ROW_ARRAY_SIZE.  
  
    > [!NOTE]  
    >  O tamanho da matriz apontada pelo atributo da instrução SQL_ATTR_ROW_STATUS_PTR deve ser igual a SQL_ATTR_ROW_ARRAY_SIZE ou SQL_ATTR_ROW_STATUS_PTR deve ser um ponteiro nulo.  
  
4.  Chama **SQLBulkOperations**(*StatementHandle,* SQL_ADD) para executar a inserção.  
  
5.  Se o aplicativo tiver definido o atributo instrução SQL_ATTR_ROW_STATUS_PTR, ele poderá inspecionar essa matriz para ver o resultado da operação.  
  
 Se um aplicativo associar a coluna 0 antes de chamar **SQLBulkOperations** com um argumento de *operação* de SQL_ADD, o driver atualizará os buffers da coluna associada 0 com os valores de indicador para a linha recentemente inserida. Para que isso ocorra, o aplicativo deve ter definido o atributo de instrução SQL_ATTR_USE_BOOKMARKS como SQL_UB_VARIABLE antes de executar a instrução. (Isso não funciona com um ODBC 2. Driver *x* .)  
  
 Os dados longos podem ser adicionados em partes por SQLBulkOperations, usando chamadas para SQLParamData e SQLPutData. Para obter mais informações, consulte "fornecendo dados longos para inserções e atualizações em massa" posteriormente nesta referência de função.  
  
 Não é necessário que o aplicativo chame **SQLFetch** ou **SQLFetchScroll** antes de chamar **SQLBulkOperations** (exceto ao entrar em um ODBC 2.* Driver x* ; consulte [compatibilidade com versões anteriores e conformidade com padrões](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)).  
  
 O comportamento é definido por driver se **SQLBulkOperations**, com um argumento de *operação* de SQL_ADD, é chamado em um cursor que contém colunas duplicadas. O driver pode retornar um SQLSTATE definido pelo driver, adicionar os dados à primeira coluna que aparece no conjunto de resultados ou executar outro comportamento definido pelo driver.  
  
## <a name="performing-bulk-updates-by-using-bookmarks"></a>Executando atualizações em massa usando indicadores  
 Para executar atualizações em massa usando indicadores com **SQLBulkOperations**, um aplicativo executa as seguintes etapas em sequência:  
  
1.  Define o atributo da instrução SQL_ATTR_USE_BOOKMARKS como SQL_UB_VARIABLE.  
  
2.  Executa uma consulta que retorna um conjunto de resultados.  
  
3.  Define o atributo de instrução SQL_ATTR_ROW_ARRAY_SIZE como o número de linhas que deseja atualizar.  
  
4.  Chama **SQLBindCol** para associar os dados que deseja atualizar. Os dados são associados a uma matriz com um tamanho igual ao valor de SQL_ATTR_ROW_ARRAY_SIZE. Ele também chama **SQLBindCol** para associar a coluna 0 (a coluna de indicadores).  
  
5.  Copia os indicadores para as linhas que ele está interessado em atualizar na matriz associada à coluna 0.  
  
6.  Atualiza os dados nos buffers associados.  
  
    > [!NOTE]  
    >  O tamanho da matriz apontada pelo atributo da instrução SQL_ATTR_ROW_STATUS_PTR deve ser igual a SQL_ATTR_ROW_ARRAY_SIZE ou SQL_ATTR_ROW_STATUS_PTR deve ser um ponteiro nulo.  
  
7.  Chama **SQLBulkOperations**(*StatementHandle,* SQL_UPDATE_BY_BOOKMARK).  
  
    > [!NOTE]  
    >  Se o aplicativo tiver definido o atributo instrução SQL_ATTR_ROW_STATUS_PTR, ele poderá inspecionar essa matriz para ver o resultado da operação.  
  
8.  Opcionalmente, chama **SQLBulkOperations**(*StatementHandle*, SQL_FETCH_BY_BOOKMARK) para buscar dados nos buffers de aplicativo associados para verificar se a atualização ocorreu.  
  
9. Se os dados tiverem sido atualizados, o driver altera o valor na matriz de status de linha para as linhas apropriadas para SQL_ROW_UPDATED.  
  
 As atualizações em massa executadas pelo **SQLBulkOperations** podem incluir dados longos usando chamadas para **SQLParamData** e **SQLPutData**. Para obter mais informações, consulte "fornecendo dados longos para inserções e atualizações em massa" posteriormente nesta referência de função.  
  
 Se os indicadores persistirem entre cursores, o aplicativo não precisará chamar **SQLFetch** ou **SQLFetchScroll** antes de atualizar por indicadores. Ele pode usar indicadores que foram armazenados de um cursor anterior. Se os indicadores não persistirem entre cursores, o aplicativo precisará chamar **SQLFetch** ou **SQLFetchScroll** para recuperar os indicadores.  
  
 O comportamento é definido por driver se **SQLBulkOperations**, com um argumento de *operação* de SQL_UPDATE_BY_BOOKMARK, é chamado em um cursor que contém colunas duplicadas. O driver pode retornar um SQLSTATE definido pelo driver, atualizar a primeira coluna que aparece no conjunto de resultados ou executar outro comportamento definido pelo driver.  
  
## <a name="performing-bulk-fetches-using-bookmarks"></a>Executando buscas em massa usando indicadores  
 Para executar buscas em massa usando indicadores com **SQLBulkOperations**, um aplicativo executa as seguintes etapas em sequência:  
  
1.  Define o atributo da instrução SQL_ATTR_USE_BOOKMARKS como SQL_UB_VARIABLE.  
  
2.  Executa uma consulta que retorna um conjunto de resultados.  
  
3.  Define o atributo de instrução SQL_ATTR_ROW_ARRAY_SIZE como o número de linhas que deseja buscar.  
  
4.  Chama **SQLBindCol** para associar os dados que deseja buscar. Os dados são associados a uma matriz com um tamanho igual ao valor de SQL_ATTR_ROW_ARRAY_SIZE. Ele também chama **SQLBindCol** para associar a coluna 0 (a coluna de indicadores).  
  
5.  Copia os indicadores de linhas em que está interessado em buscar na matriz associada à coluna 0. (Isso pressupõe que o aplicativo já tenha obtido os indicadores separadamente.)  
  
    > [!NOTE]  
    >  O tamanho da matriz apontada pelo atributo da instrução SQL_ATTR_ROW_STATUS_PTR deve ser igual a SQL_ATTR_ROW_ARRAY_SIZE ou SQL_ATTR_ROW_STATUS_PTR deve ser um ponteiro nulo.  
  
6.  Chama **SQLBulkOperations**(*StatementHandle,* SQL_FETCH_BY_BOOKMARK).  
  
7.  Se o aplicativo tiver definido o atributo instrução SQL_ATTR_ROW_STATUS_PTR, ele poderá inspecionar essa matriz para ver o resultado da operação.  
  
 Se os indicadores persistirem entre cursores, o aplicativo não precisará chamar **SQLFetch** ou **SQLFetchScroll** antes de buscar por indicadores. Ele pode usar indicadores que foram armazenados de um cursor anterior. Se os indicadores não persistirem entre cursores, o aplicativo precisará chamar **SQLFetch** ou **SQLFetchScroll** uma vez para recuperar os indicadores.  
  
## <a name="performing-bulk-deletes-using-bookmarks"></a>Executando exclusões em massa usando indicadores  
 Para executar exclusões em massa usando indicadores com **SQLBulkOperations**, um aplicativo executa as seguintes etapas em sequência:  
  
1.  Define o atributo da instrução SQL_ATTR_USE_BOOKMARKS como SQL_UB_VARIABLE.  
  
2.  Executa uma consulta que retorna um conjunto de resultados.  
  
3.  Define o atributo de instrução SQL_ATTR_ROW_ARRAY_SIZE como o número de linhas que deseja excluir.  
  
4.  Chama **SQLBindCol** para associar a coluna 0 (a coluna de indicadores).  
  
5.  Copia os indicadores para as linhas que estão interessadas em excluir na matriz associada à coluna 0.  
  
    > [!NOTE]  
    >  O tamanho da matriz apontada pelo atributo da instrução SQL_ATTR_ROW_STATUS_PTR deve ser igual a SQL_ATTR_ROW_ARRAY_SIZE ou SQL_ATTR_ROW_STATUS_PTR deve ser um ponteiro nulo.  
  
6.  Chama **SQLBulkOperations**(*StatementHandle,* SQL_DELETE_BY_BOOKMARK).  
  
7.  Se o aplicativo tiver definido o atributo instrução SQL_ATTR_ROW_STATUS_PTR, ele poderá inspecionar essa matriz para ver o resultado da operação.  
  
 Se os indicadores persistirem entre cursores, o aplicativo não precisará chamar **SQLFetch** ou **SQLFetchScroll** antes da exclusão por indicadores. Ele pode usar indicadores que foram armazenados de um cursor anterior. Se os indicadores não persistirem entre cursores, o aplicativo precisará chamar **SQLFetch** ou **SQLFetchScroll** uma vez para recuperar os indicadores.  
  
## <a name="providing-long-data-for-bulk-inserts-and-updates"></a>Fornecendo dados longos para inserções e atualizações em massa  
 Os dados longos podem ser fornecidos para inserções e atualizações em massa executadas por chamadas para **SQLBulkOperations**. Para inserir ou atualizar dados longos, um aplicativo executa as etapas a seguir, além das etapas descritas nas seções "executando inserções em massa" e "executando atualizações em massa usando indicadores" anteriormente neste tópico.  
  
1.  Quando ele associa os dados usando **SQLBindCol**, o aplicativo coloca um valor definido pelo aplicativo, como o número da coluna, no buffer * \*TargetValuePtr* para as colunas de dados em execução. O valor pode ser usado posteriormente para identificar a coluna.  
  
     O aplicativo coloca o resultado da macro SQL_LEN_DATA_AT_EXEC (*comprimento*) no buffer de * \*StrLen_or_IndPtr* . Se o tipo de dados SQL da coluna for SQL_LONGVARBINARY, SQL_LONGVARCHAR ou um tipo de dados específico da fonte de dados longa e o driver retornar "Y" para o tipo de informação SQL_NEED_LONG_DATA_LEN em **SQLGetInfo**, *Length* será o número de bytes de dados a serem enviados para o parâmetro; caso contrário, ele deve ser um valor não negativo e será ignorado.  
  
2.  Quando **SQLBulkOperations** é chamado, se houver colunas de dados em execução, a função retornará SQL_NEED_DATA e prosseguirá para a etapa 3, que segue. (Se não houver nenhuma coluna de dados em execução, o processo será concluído.)  
  
3.  O aplicativo chama **SQLParamData** para recuperar o endereço do buffer * \*TargetValuePtr* para a primeira coluna de dados em execução a ser processada. **SQLParamData** retorna SQL_NEED_DATA. O aplicativo recupera o valor definido pelo aplicativo do buffer * \*TargetValuePtr* .  
  
    > [!NOTE]  
    >  Embora os parâmetros de dados em execução se assemelham a colunas de dados em execução, o valor retornado por **SQLParamData** é diferente para cada um.  
  
     As colunas de dados em execução são colunas em um conjunto de linhas para o qual os dados serão enviados com **SQLPutData** quando uma linha é atualizada ou inserida com **SQLBulkOperations**. Eles são associados a **SQLBindCol**. O valor retornado por **SQLParamData** é o endereço da linha no buffer **TargetValuePtr* que está sendo processado.  
  
4.  O aplicativo chama **SQLPutData** uma ou mais vezes para enviar dados para a coluna. Mais de uma chamada será necessária se o valor de dados não puder ser retornado no buffer * \*TargetValuePtr* especificado em **SQLPutData**; várias chamadas para **SQLPutData** para a mesma coluna são permitidas somente ao enviar dados de caractere C para uma coluna com um tipo de dados específico de fonte de caracteres, binário ou de dados ou ao enviar dados binários c para uma coluna com um tipo de dados de caractere, binário ou específico de fonte de dados.  
  
5.  O aplicativo chama **SQLParamData** novamente para sinalizar que todos os dados foram enviados para a coluna.  
  
    -   Se houver mais colunas de dados em execução, **SQLParamData** retornará SQL_NEED_DATA e o endereço do buffer *TargetValuePtr* para a próxima coluna de dados em execução a ser processada. O aplicativo repete as etapas 4 e 5.  
  
    -   Se não houver mais colunas de dados em execução, o processo será concluído. Se a instrução foi executada com êxito, **SQLParamData** retornará SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO; se a execução falhar, ela retornará SQL_ERROR. Neste ponto, **SQLParamData** pode retornar qualquer SQLSTATE que possa ser retornado por **SQLBulkOperations**.  
  
 Se a operação for cancelada ou um erro ocorrer em **SQLParamData** ou **SQLPutData** depois que **SQLBulkOperations** retornar SQL_NEED_DATA e antes de os dados serem enviados para todas as colunas de dados em execução, o aplicativo poderá chamar somente **SQLCancel**, **SQLGetDiagField**, **SQLGetDiagRec**, **SQLGetFunctions**, **SQLParamData**ou **SQLPutData** para a instrução ou a conexão associada à instrução. Se ele chamar qualquer outra função para a instrução ou a conexão associada à instrução, a função retornará SQL_ERROR e SQLSTATE HY010 (erro de sequência de função).  
  
 Se o aplicativo chamar **SQLCancel** enquanto o driver ainda precisar de dados para as colunas de dados em execução, o driver cancelará a operação. O aplicativo pode então chamar **SQLBulkOperations** novamente; o cancelamento não afeta o estado do cursor nem a posição atual do cursor.  
  
## <a name="row-status-array"></a>Matriz de status da linha  
 A matriz de status de linha contém valores de status para cada linha de dados no conjunto de linhas após uma chamada para **SQLBulkOperations**. O driver define os valores de status nesta matriz após uma chamada para **SQLFetch**, **SQLFetchScroll**, **SQLSetPos**ou **SQLBulkOperations**. Essa matriz é inicialmente populada por uma chamada para **SQLBulkOperations** se **SQLFetch** ou **SQLFetchScroll** não foi chamado antes de **SQLBulkOperations**. Essa matriz é apontada pelo atributo da instrução SQL_ATTR_ROW_STATUS_PTR. O número de elementos nas matrizes de status de linha deve ser igual ao número de linhas no conjunto de linhas (conforme definido pelo atributo de instrução SQL_ATTR_ROW_ARRAY_SIZE). Para obter informações sobre essa matriz de status de linha, consulte [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
## <a name="code-example"></a>Exemplo de código  
 O exemplo a seguir busca 10 linhas de dados por vez da tabela Customers. Em seguida, ele solicita ao usuário uma ação a ser tomada. Para reduzir o tráfego de rede, o exemplo de atualizações de buffer, exclusões e inserções localmente nas matrizes associadas, mas em deslocamentos além dos dados do conjunto de linhas. Quando o usuário opta por enviar atualizações, exclusões e inserções para a fonte de dados, o código define o deslocamento de associação adequadamente e chama **SQLBulkOperations**. Para simplificar, o usuário não pode armazenar em buffer mais de 10 atualizações, exclusões ou inserções.  
  
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
|Associando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Buscando um bloco de dados ou rolando por meio de um conjunto de resultados|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Obtendo um único campo de um descritor|[Função SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Obtendo vários campos de um descritor|[Função SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Definindo um único campo de um descritor|[Função SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Configurando vários campos de um descritor|[Função SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|Posicionando o cursor, atualizando os dados no conjunto de linhas ou atualizando ou excluindo dados no conjunto de linhas|[Função SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|Definindo um atributo de instrução|[Função SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
