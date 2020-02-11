---
title: Função SQLSetPos | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetPos
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLSetPos
helpviewer_keywords:
- SQLSetPos function [ODBC]
ms.assetid: 80190ee7-ae3b-45e5-92a9-693eb558f322
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 80f14b99d2c7dac91116186fdcf53ff77ee6c2c0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68343068"
---
# <a name="sqlsetpos-function"></a>Função SQLSetPos
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: ODBC  
  
 **Resumo**  
 **SQLSetPos** define a posição do cursor em um conjunto de linhas e permite que um aplicativo atualize os dados do conjunto de linhas ou atualize ou exclua dados no conjunto de resultados.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLSetPos(  
      SQLHSTMT        StatementHandle,  
      SQLSETPOSIROW   RowNumber,  
      SQLUSMALLINT    Operation,  
      SQLUSMALLINT    LockType);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 Entrada Identificador de instrução.  
  
 *RowNumber*  
 Entrada Posição da linha no conjunto de linhas no qual executar a operação especificada com o argumento de *operação* . Se *RowNumber* for 0, a operação se aplicará a todas as linhas no conjunto de linhas.  
  
 Para obter informações adicionais, consulte "Comentários".  
  
 *Operação*  
 Entrada Operação a ser executada:  
  
 SQL_POSITION SQL_REFRESH SQL_UPDATE SQL_DELETE  
  
> [!NOTE]
>  O valor de SQL_ADD para o argumento de *operação* foi preterido para ODBC *3. x*. Os drivers ODBC *3. x* precisarão dar suporte a SQL_ADD para compatibilidade com versões anteriores. Essa funcionalidade foi substituída por uma chamada para **SQLBulkOperations** com uma *operação* de SQL_ADD. Quando um aplicativo ODBC *3. x* funciona com um driver *ODBC 2. x* , o Gerenciador de driver mapeia uma chamada para **SQLBulkOperations** com uma *operação* de SQL_ADD para **SQLSetPos** com uma *operação* de SQL_ADD.  
  
 Para obter mais informações, consulte "Comentários".  
  
 *LockType*  
 Entrada Especifica como bloquear a linha depois de executar a operação especificada no argumento *Operation* .  
  
 SQL_LOCK_NO_CHANGE SQL_LOCK_EXCLUSIVE SQL_LOCK_UNLOCK  
  
 Para obter mais informações, consulte "Comentários".  
  
 **Retornos**  
  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLSetPos** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *identificador* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLSetPos** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
 Para todos os hiperestados que podem retornar SQL_SUCCESS_WITH_INFO ou SQL_ERROR (exceto 01xxx sqlstates), SQL_SUCCESS_WITH_INFO será retornado se ocorrer um erro em uma ou mais, mas não em todas as linhas de uma operação multirow, e SQL_ERROR será retornado se ocorrer um erro em um operação de linha única.  
  
|SQLSTATE|Erro|DESCRIÇÃO|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01001|Conflito de operação do cursor|O argumento de *operação* foi SQL_DELETE ou SQL_UPDATE, e nenhuma linha ou mais de uma fila foi excluída ou atualizada. (Para obter mais informações sobre atualizações para mais de uma linha, consulte a descrição do *atributo* SQL_ATTR_SIMULATE_CURSOR em **SQLSetStmtAttr**.) (A função retorna SQL_SUCCESS_WITH_INFO.)<br /><br /> O argumento da *operação* foi SQL_DELETE ou SQL_UPDATE e a operação falhou devido a uma simultaneidade otimista. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Truncamento direito de dados de cadeia de caracteres|O argumento da *operação* foi SQL_REFRESH, e os dados de cadeia de caracteres ou binários retornados para uma coluna ou colunas com um tipo de dados de SQL_C_CHAR ou SQL_C_BINARY resultaram no truncamento de um caractere não em branco ou dados binários não nulos.|  
|01S01|Erro na linha|O argumento *RowNumber* era 0 e ocorreu um erro em uma ou mais linhas ao executar a operação especificada com o argumento *Operation* .<br /><br /> (SQL_SUCCESS_WITH_INFO será retornado se ocorrer um erro em uma ou mais, mas não em todas as linhas de uma operação multirow, e SQL_ERROR será retornado se ocorrer um erro em uma operação de linha única.)<br /><br /> (Esse SQLSTATE é retornado somente quando **SQLSetPos** é chamado após **SQLExtendedFetch**, se o driver for um driver ODBC *2. x* e a biblioteca de cursores não for usada.)|  
|01S07|Truncamento fracionário|O argumento de *operação* foi SQL_REFRESH, o tipo de dados do buffer de aplicativo não foi SQL_C_CHAR ou SQL_C_BINARY e os dados retornados aos buffers de aplicativo para uma ou mais colunas foram truncados. Para tipos de dados numéricos, a parte fracionária do número foi truncada. Para os tipos de dados time, timestamp e Interval que contêm um componente de tempo, a parte fracionária do tempo foi truncada.<br /><br /> (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|07006|Violação de atributo de tipo de dados restrito|Não foi possível converter o valor de dados de uma coluna no conjunto de resultados no tipo de dados especificado por *TargetType* na chamada de **SQLBindCol**.|  
|07009|Índice de descritor inválido|A *operação* de argumento foi SQL_REFRESH ou SQL_UPDATE e uma coluna foi associada a um número de coluna maior que o número de colunas no conjunto de resultados.|  
|21S02|O grau da tabela derivada não corresponde à lista de colunas|A *operação* de argumento foi SQL_UPDATE e nenhuma coluna foi atualizável porque todas as colunas estavam desvinculadas, somente leitura ou o valor no buffer de indicador/comprimento de limite foi SQL_COLUMN_IGNORE.|  
|22001|Dados de cadeia de caracteres, truncamento à direita|O argumento da *operação* foi SQL_UPDATE, e a atribuição de um valor de caractere ou binário a uma coluna resultou no truncamento de caracteres não vazios (para caracteres) ou não nulos (para binários) ou bytes.|  
|22003|Valor numérico fora do intervalo|A *operação* de argumento foi SQL_UPDATE e a atribuição de um valor numérico a uma coluna no conjunto de resultados fez com que a parte inteira (em oposição à fracionária) do número seja truncada.<br /><br /> A *operação* de argumento foi SQL_REFRESH e o retorno do valor numérico de uma ou mais colunas associadas causaria uma perda de dígitos significativos.|  
|22007|Formato de data e hora inválido|A *operação* de argumento foi SQL_UPDATEda e a atribuição de um valor de data ou timestamp a uma coluna no conjunto de resultados fez com que o campo ano, mês ou dia estivesse fora do intervalo.<br /><br /> A *operação* de argumento foi SQL_REFRESH e retornando o valor de data ou timestamp para uma ou mais colunas associadas teria feito com que o campo ano, mês ou dia estivesse fora do intervalo.|  
|22008|Estouro de campo de data/hora|O argumento da *operação* foi SQL_UPDATE e o desempenho da aritmética de DateTime nos dados enviados a uma coluna no conjunto de resultados resultou em um campo DateTime (ano, mês, dia, hora, minuto ou segundo campo) do resultado que está fora do intervalo permitido de valores para o campo ou sendo inválido com base nas regras naturais do calendário gregoriano para DateTimes.<br /><br /> O argumento da *operação* foi SQL_REFRESH e o desempenho da aritmética de DateTime nos dados que estão sendo recuperados do conjunto de resultados resultou em um campo DateTime (ano, mês, dia, hora, minuto ou segundo campo) do resultado que está fora do intervalo permitido de valores para o campo ou sendo inválido com base nas regras naturais do calendário gregoriano para DateTimes.|  
|22015|Estouro no campo de intervalo|O argumento de *operação* foi SQL_UPDATE e a atribuição de um tipo numérico exato ou de C de intervalo a um tipo de dados SQL de intervalo causou uma perda de dígitos significativos.<br /><br /> O argumento da *operação* foi SQL_UPDATE; ao atribuir a um tipo SQL de intervalo, não havia nenhuma representação do valor do tipo C no tipo SQL de intervalo.<br /><br /> O argumento de *operação* foi SQL_REFRESH e a atribuição de um tipo de SQL numérico ou de intervalo exato a um tipo de intervalo C causou uma perda de dígitos significativos no campo à esquerda.<br /><br /> O argumento da *operação* foi SQL_ atualização; ao atribuir a um tipo de intervalo C, não havia nenhuma representação do valor do tipo SQL no tipo de intervalo C.|  
|22018|Valor de caractere inválido para especificação de conversão|O argumento da *operação* foi SQL_REFRESH; o tipo C era um tipo de dados numérico exato ou aproximado, um DateTime ou um intervalo; o tipo SQL da coluna era um tipo de dados de caractere; e o valor na coluna não era um literal válido do tipo associado de C.<br /><br /> A *operação* de argumento foi SQL_UPDATE; o tipo SQL era um tipo de dados numérico exato ou aproximado, um DateTime ou um intervalo; o tipo C foi SQL_C_CHAR; e o valor na coluna não era um literal válido do tipo SQL associado.|  
|23000|Violação de restrição de integridade|A *operação* de argumento foi SQL_DELETE ou SQL_UPDATE e uma restrição de integridade foi violada.|  
|24.000|Estado de cursor inválido|O *StatementHandle* estava em um estado executado, mas nenhum conjunto de resultados foi associado ao *StatementHandle*.<br /><br /> (DM) um cursor foi aberto no *StatementHandle*, mas **SQLFetch** ou **SQLFetchScroll** não tinha sido chamado.<br /><br /> Um cursor estava aberto no *StatementHandle*, e **SQLFetch** ou **SQLFetchScroll** foi chamado, mas o cursor foi posicionado antes do início do conjunto de resultados ou após o final do conjunto de resultados.<br /><br /> A *operação* de argumento foi SQL_DELETE, SQL_REFRESH ou SQL_UPDATE e o cursor foi posicionado antes do início do conjunto de resultados ou após o final do conjunto de resultados.|  
|40001|Falha de serialização|A transação foi revertida devido a um deadlock de recurso com outra transação.|  
|40003|Conclusão de instrução desconhecida|A conexão associada falhou durante a execução dessa função, e o estado da transação não pode ser determinado.|  
|42000|Erro de sintaxe ou violação de acesso|O driver não pôde bloquear a linha conforme necessário para executar a operação solicitada na *operação*de argumento.<br /><br /> O driver não pôde bloquear a linha conforme solicitado no *Delocktype*do argumento.|  
|44000|Violação COM OPÇÃO DE VERIFICAÇÃO|O argumento de *operação* foi SQL_UPDATE e a atualização foi executada em uma tabela exibida ou uma tabela derivada da tabela exibida que foi criada ESPECIFICANDO **with check option**, de modo que uma ou mais linhas afetadas pela atualização não estarão mais presentes na tabela exibida.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \*MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado em *StatementHandle*e, em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativo multithread.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *StatementHandle*. Esta função assíncrona ainda estava em execução quando a função SQLSetPos foi chamada.<br /><br /> (DM) o *StatementHandle* especificado não estava em um estado executado. A função foi chamada sem primeiro chamar **SQLExecDirect**, **SQLExecute**ou uma função de catálogo.<br /><br /> (DM) uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado para o *StatementHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.<br /><br /> (DM) o driver era um driver ODBC *2. x* e **SQLSetPos** foi chamado para um *StatementHandle* depois que **SQLFetch** foi chamado.|  
|HY011|O atributo não pode ser definido agora|(DM) o driver era um driver ODBC *2. x* ; o atributo da instrução SQL_ATTR_ROW_STATUS_PTR foi definido; em seguida, **SQLSetPos** foi chamado antes de **SQLFetch**, **SQLFetchScroll**ou **SQLExtendedFetch** ser chamado.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|O argumento da *operação* foi SQL_UPDATE, um valor de dados era um ponteiro nulo e o valor de comprimento da coluna não era 0, SQL_DATA_AT_EXEC, SQL_COLUMN_IGNORE, SQL_NULL_DATA ou menor ou igual a SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> O argumento da *operação* foi SQL_UPDATE; um valor de dados não era um ponteiro nulo; o tipo de dados C foi SQL_C_BINARY ou SQL_C_CHAR; e o valor de comprimento da coluna era menor que 0, mas não igual a SQL_DATA_AT_EXEC, SQL_COLUMN_IGNORE, SQL_NTS ou SQL_NULL_DATA ou menor ou igual a SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> O valor em um buffer de comprimento/indicador foi SQL_DATA_AT_EXEC; o tipo SQL foi SQL_LONGVARCHAR, SQL_LONGVARBINARY ou um tipo de dados específico da fonte de dados longa; e o tipo de informação SQL_NEED_LONG_DATA_LEN em **SQLGetInfo** era "Y".|  
|HY092|Identificador de atributo inválido|(DM) o valor especificado para o argumento de *operação* era inválido.<br /><br /> (DM) o valor especificado para o argumento *LockType* era inválido.<br /><br /> O argumento de *operação* foi SQL_UPDATE ou SQL_DELETE e o atributo de instrução SQL_ATTR_CONCURRENCY foi SQL_ATTR_CONCUR_READ_ONLY.|  
|HY107|Valor da linha fora do intervalo|O valor especificado para o argumento *RowNumber* era maior que o número de linhas no conjunto de linhas.|  
|HY109|Posição do cursor inválida|O cursor associado ao *StatementHandle* foi definido como somente de encaminhamento, portanto, o cursor não pôde ser posicionado dentro do conjunto de linhas. Consulte a descrição para o atributo SQL_ATTR_CURSOR_TYPE em **SQLSetStmtAttr**.<br /><br /> O argumento da *operação* foi SQL_UPDATE, SQL_DELETE ou SQL_REFRESH, e a linha identificada pelo argumento *RowNumber* foi excluída ou não tinha sido buscada.<br /><br /> (DM) o argumento *RowNumber* era 0 e o argumento *Operation* foi SQL_POSITION.<br /><br /> **SQLSetPos** foi chamado depois de **SQLBulkOperations** ser chamado e antes de **SQLFetchScroll** ou **SQLFetch** ser chamado.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|O driver ou a fonte de dados não oferece suporte à operação solicitada no argumento de *operação* ou no argumento *LockType* .|  
|HYT00|Tempo limite esgotado|O período de tempo limite da consulta expirou antes que a fonte de dados retornasse o conjunto de resultados. O período de tempo limite é definido por meio de **SQLSetStmtAttr** com um *atributo* de SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *StatementHandle* não oferece suporte à função.|  
|IM017|A sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação for usado, a sondagem será desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesse identificador.|Se a chamada de função anterior no identificador retornar SQL_STILL_EXECUTING e se o modo de notificação estiver habilitado, **SQLCompleteAsync** deverá ser chamado na alça para executar o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
  
> [!CAUTION]
>  Para obter informações sobre a instrução, o **SQLSetPos** pode ser chamado no e o que ele precisa fazer para compatibilidade com aplicativos ODBC *2. x* , consulte [cursores de bloco, cursores roláveis e compatibilidade com versões anteriores](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md).  
  
## <a name="rownumber-argument"></a>Argumento RowNumber  
 O argumento *RowNumber* especifica o número da linha no conjunto de linhas no qual executar a operação especificada pelo argumento *Operation* . Se *RowNumber* for 0, a operação se aplicará a todas as linhas no conjunto de linhas. *RowNumber* deve ser um valor de 0 até o número de linhas no conjunto de linhas.  
  
> [!NOTE]  
>  Na linguagem C, as matrizes são baseadas em 0 e o argumento *RowNumber* é baseado em 1. Por exemplo, para atualizar a quinta linha do conjunto de linhas, um aplicativo modifica os buffers de conjunto de linhas no índice de matriz 4, mas especifica um *RowNumber* de 5.  
  
 Todas as operações posicionam o cursor na linha especificada por *RowNumber*. As seguintes operações exigem uma posição de cursor:  
  
-   Instruções UPDATE e DELETE posicionadas.  
  
-   Chamadas para **SQLGetData**.  
  
-   Chamadas para **SQLSetPos** com as opções SQL_DELETE, SQL_REFRESH e SQL_UPDATE.  
  
 Por exemplo, se *RowNumber* for 2 para uma chamada para **SQLSetPos** com uma *operação* de SQL_DELETE, o cursor será posicionado na segunda linha do conjunto de linhas e essa linha será excluída. A entrada na matriz de status da linha de implementação (apontada pelo atributo instrução SQL_ATTR_ROW_STATUS_PTR) para a segunda linha é alterada para SQL_ROW_DELETED.  
  
 Um aplicativo pode especificar uma posição de cursor quando chama **SQLSetPos**. Geralmente, ele chama **SQLSetPos** com a operação SQL_POSITION ou SQL_REFRESH para posicionar o cursor antes de executar uma instrução UPDATE ou DELETE posicionada ou chamar **SQLGetData**.  
  
## <a name="operation-argument"></a>Argumento de operação  
 O argumento *Operation* dá suporte às operações a seguir. Para determinar quais opções são suportadas por uma fonte de dados, um aplicativo chama **SQLGetInfo** com o tipo de informação SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 ou SQL_STATIC_CURSOR_ATTRIBUTES1 (dependendo do tipo do cursor).  
  
|*Operação*<br /><br /> argumento|Operação|  
|------------------------------|---------------|  
|SQL_POSITION|O driver posiciona o cursor na linha especificada por *RowNumber*.<br /><br /> O conteúdo da matriz de status de linha apontada pelo atributo de instrução SQL_ATTR_ROW_OPERATION_PTR é ignorado para a *operação*de SQL_POSITION.|  
|SQL_REFRESH|O driver posiciona o cursor na linha especificada por *RowNumber* e atualiza os dados nos buffers de conjunto de linhas para essa linha. Para obter mais informações sobre como o driver retorna dados nos buffers de conjunto de linhas, consulte as descrições de associação de linha e coluna em **SQLBindCol**.<br /><br /> **SQLSetPos** com uma *operação* de SQL_REFRESH atualiza o status e o conteúdo das linhas dentro do conjunto de linhas buscado atual. Isso inclui a atualização dos indicadores. Como os dados nos buffers são atualizados, mas não são rebuscados, a associação no conjunto de linhas é corrigida. Isso é diferente da atualização executada por uma chamada para **SQLFetchScroll** com um *FetchOrientation* de SQL_FETCH_RELATIVE e um *RowNumber* igual a 0, que busca novamente o conjunto de linhas do conjunto de resultados para que ele possa mostrar dados adicionados e remover dados excluídos se essas operações forem compatíveis com o driver e o cursor.<br /><br /> Uma atualização bem-sucedida com **SQLSetPos** não alterará o status de uma linha de SQL_ROW_DELETED. As linhas excluídas dentro do conjunto de linhas continuarão sendo marcadas como excluídas até a próxima busca. As linhas desaparecerão na próxima busca se o cursor der suporte à embalagem (em que um **SQLFetch** ou **SQLFetchScroll** subsequente não retorna linhas excluídas).<br /><br /> Linhas adicionadas não aparecem quando uma atualização com **SQLSetPos** é executada. Esse comportamento é diferente de **SQLFetchScroll** com um *fetchtype* de SQL_FETCH_RELATIVE e um *RowNumber* igual a 0, que também atualiza o conjunto de linhas atual, mas mostrará registros adicionados ou pacotes de registros excluídos se essas operações forem suportadas pelo cursor.<br /><br /> Uma atualização bem-sucedida com **SQLSetPos** alterará um status de linha de SQL_ROW_ADDED para SQL_ROW_SUCCESS (se existir a matriz de status de linha).<br /><br /> Uma atualização bem-sucedida com **SQLSetPos** alterará um status de linha de SQL_ROW_UPDATED para o novo status da linha (se existir a matriz de status de linha).<br /><br /> Se ocorrer um erro em uma operação **SQLSetPos** em uma linha, o status da linha será definido como SQL_ROW_ERROR (se existir a matriz de status de linha).<br /><br /> Para um cursor aberto com um atributo de instrução SQL_ATTR_CONCURRENCY de SQL_CONCUR_ROWVER ou SQL_CONCUR_VALUES, uma atualização com **SQLSetPos** pode atualizar os valores de simultaneidade otimista usados pela fonte de dados para detectar que a linha foi alterada. Se isso ocorrer, as versões de linha ou os valores usados para garantir a simultaneidade do cursor serão atualizados sempre que os buffers de conjunto de linhas forem atualizados do servidor. Isso ocorre para cada linha que é atualizada.<br /><br /> O conteúdo da matriz de status de linha apontada pelo atributo de instrução SQL_ATTR_ROW_OPERATION_PTR é ignorado para a *operação*de SQL_REFRESH.|  
|SQL_UPDATE|O driver posiciona o cursor na linha especificada por *RowNumber* e atualiza a linha de dados subjacente com os valores nos buffers de conjunto de linhas (o argumento *TargetValuePtr* em **SQLBindCol**). Ele recupera os comprimentos dos dados dos buffers de comprimento/indicador (o argumento *StrLen_or_IndPtr* em **SQLBindCol**). Se o comprimento de qualquer coluna for SQL_COLUMN_IGNORE, a coluna não será atualizada. Depois de atualizar a linha, o driver altera o elemento correspondente da matriz de status de linha para SQL_ROW_UPDATED ou SQL_ROW_SUCCESS_WITH_INFO (se existir a matriz de status de linha).<br /><br /> É definido pelo driver qual é o comportamento se **SQLSetPos** com um argumento de *operação* de SQL_UPDATE é chamado em um cursor que contém colunas duplicadas. O driver pode retornar um SQLSTATE definido pelo driver, pode atualizar a primeira coluna que aparece no conjunto de resultados ou executar outro comportamento definido pelo driver.<br /><br /> A matriz de operação de linha apontada pelo atributo instrução SQL_ATTR_ROW_OPERATION_PTR pode ser usada para indicar que uma linha no conjunto de linhas atual deve ser ignorada durante uma atualização em massa. Para obter mais informações, consulte "matrizes de status e de operação" mais adiante nesta referência de função.|  
|SQL_DELETE|O driver posiciona o cursor na linha especificada por *RowNumber* e exclui a linha de dados subjacente. Ele altera o elemento correspondente da matriz de status de linha para SQL_ROW_DELETED. Depois que a linha tiver sido excluída, o seguinte não será válido para a linha: as instruções UPDATE e DELETE posicionadas, chamadas para **SQLGetData**e chamadas para **SQLSetPos** com a *operação* definida como qualquer coisa, exceto SQL_POSITION. Para drivers que dão suporte à embalagem, a linha é excluída do cursor quando novos dados são recuperados da fonte de dados.<br /><br /> Se a linha permanece visível depende do tipo de cursor. Por exemplo, as linhas excluídas são visíveis para cursores estáticos e controlados por conjunto de chaves, mas invisíveis para cursores dinâmicos.<br /><br /> A matriz de operação de linha apontada pelo atributo instrução SQL_ATTR_ROW_OPERATION_PTR pode ser usada para indicar que uma linha no conjunto de linhas atual deve ser ignorada durante uma exclusão em massa. Para obter mais informações, consulte "matrizes de status e de operação" mais adiante nesta referência de função.|  
  
## <a name="locktype-argument"></a>Argumento LockType  
 O argumento *LockType* fornece uma maneira para que os aplicativos controlem a simultaneidade. Na maioria dos casos, as fontes de dados que dão suporte a níveis de simultaneidade e transações terão suporte apenas ao valor SQL_LOCK_NO_CHANGE do argumento *LockType* . O argumento *LockType* geralmente é usado apenas para suporte baseado em arquivo.  
  
 O argumento *LockType* especifica o estado de bloqueio da linha após a execução de **SQLSetPos** . Se o driver não puder bloquear a linha para executar a operação solicitada ou para satisfazer o argumento *LockType* , ele retornará SQL_ERROR e SQLSTATE 42000 (erro de sintaxe ou violação de acesso).  
  
 Embora o argumento *LockType* seja especificado para uma única instrução, o bloqueio se acordeá com os mesmos privilégios de todas as instruções na conexão. Em particular, um bloqueio adquirido por uma instrução em uma conexão pode ser desbloqueado por uma instrução diferente na mesma conexão.  
  
 Uma linha bloqueada por meio de **SQLSetPos** permanece bloqueada até que o aplicativo chame **SQLSetPos** para a linha com *LockType* definido como SQL_LOCK_UNLOCK ou até que o aplicativo chame **SQLFreeHandle** para a instrução ou **SQLFreeStmt** com a opção SQL_CLOSE. Para um driver que dá suporte a transações, uma linha bloqueada por meio de **SQLSetPos** é desbloqueada quando o aplicativo chama **SQLEndTran** para confirmar ou reverter uma transação na conexão (se um cursor for fechado quando uma transação for confirmada ou revertida, conforme indicado pelo SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR tipos de informações retornados pelo **SQLGetInfo**).  
  
 O argumento *LockType* dá suporte aos seguintes tipos de bloqueios. Para determinar quais bloqueios têm suporte por uma fonte de dados, um aplicativo chama **SQLGetInfo** com o tipo de informação SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 ou SQL_STATIC_CURSOR_ATTRIBUTES1 (dependendo do tipo de cursor).  
  
|Argumento *LockType*|Tipo de bloqueio|  
|-------------------------|---------------|  
|SQL_LOCK_NO_CHANGE|O driver ou a fonte de dados garante que a linha esteja no mesmo estado bloqueado ou desbloqueado, uma vez que o **SQLSetPos** foi chamado. Esse valor de *LockType* permite que as fontes de dados que não dão suporte ao bloqueio explícito em nível de linha usem qualquer bloqueio exigido pelos níveis atuais de isolamento de simultaneidade e transação.|  
|SQL_LOCK_EXCLUSIVE|O driver ou a fonte de dados bloqueia a linha exclusivamente. Uma instrução em uma conexão diferente ou em um aplicativo diferente não pode ser usada para adquirir bloqueios na linha.|  
|SQL_LOCK_UNLOCK|O driver ou a fonte de dados desbloqueia a linha.|  
  
 Se um driver oferecer suporte a SQL_LOCK_EXCLUSIVE mas não oferecer suporte a SQL_LOCK_UNLOCK, uma linha bloqueada permanecerá bloqueada até que uma das chamadas de função descritas no parágrafo anterior ocorra.  
  
 Se um driver oferecer suporte a SQL_LOCK_EXCLUSIVE mas não oferecer suporte a SQL_LOCK_UNLOCK, uma linha bloqueada permanecerá bloqueada até que o aplicativo chame **SQLFreeHandle** para a instrução ou **SQLFreeStmt** com a opção SQL_CLOSE. Se o driver oferecer suporte a transações e fechar o cursor após a confirmação ou reversão da transação, o aplicativo chamará **SQLEndTran**.  
  
 Para as operações de atualização e exclusão no **SQLSetPos**, o aplicativo usa o argumento *LockType* da seguinte maneira:  
  
-   Para garantir que uma linha não seja alterada depois de ser recuperada, um aplicativo chama **SQLSetPos** com a *operação* definida como SQL_REFRESH e o *LockType* definido como SQL_LOCK_EXCLUSIVE.  
  
-   Se o aplicativo definir *LockType* como SQL_LOCK_NO_CHANGE, o driver garante que uma operação de atualização ou exclusão terá sucesso somente se o aplicativo especificado SQL_CONCUR_LOCK para o atributo de instrução SQL_ATTR_CONCURRENCY.  
  
-   Se o aplicativo especificar SQL_CONCUR_ROWVER ou SQL_CONCUR_VALUES para o atributo de instrução SQL_ATTR_CONCURRENCY, o driver comparará versões de linha ou valores e rejeitará a operação se a linha tiver sido alterada desde que o aplicativo busque a linha.  
  
-   Se o aplicativo especificar SQL_CONCUR_READ_ONLY para o atributo SQL_ATTR_CONCURRENCY instrução, o driver rejeitará qualquer operação de atualização ou exclusão.  
  
 Para obter mais informações sobre o atributo de instrução SQL_ATTR_CONCURRENCY, consulte [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
## <a name="status-and-operation-arrays"></a>Matrizes de status e de operação  
 O status e as matrizes de operação a seguir são usados ao chamar **SQLSetPos**:  
  
-   A matriz de status de linha (conforme apontado pelo campo SQL_DESC_ARRAY_STATUS_PTR no IRD e o atributo de instrução SQL_ATTR_ROW_STATUS_ARRAY) contém valores de status para cada linha de dados no conjunto de linhas. O driver define os valores de status nesta matriz após uma chamada para **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**ou **SQLSetPos**. Essa matriz é apontada pelo atributo da instrução SQL_ATTR_ROW_STATUS_PTR.  
  
-   A matriz de operação de linha (conforme apontado pelo campo SQL_DESC_ARRAY_STATUS_PTR no atributo de instrução ARD e SQL_ATTR_ROW_OPERATION_ARRAY) contém um valor para cada linha no conjunto de linhas que indica se uma chamada para **SQLSetPos** para uma operação em massa é ignorada ou executada. Cada elemento na matriz é definido como SQL_ROW_PROCEED (o padrão) ou SQL_ROW_IGNORE. Essa matriz é apontada pelo atributo da instrução SQL_ATTR_ROW_OPERATION_PTR.  
  
 O número de elementos no status e nas matrizes de operação deve ser igual ao número de linhas no conjunto de linhas (conforme definido pelo atributo da instrução SQL_ATTR_ROW_ARRAY_SIZE).  
  
 Para obter informações sobre a matriz de status de linha, consulte [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md). Para obter informações sobre a matriz de operações de linha, consulte "ignorando uma linha em uma operação em massa", mais adiante nesta seção.  
  
## <a name="using-sqlsetpos"></a>Usando SQLSetPos  
 Antes que um aplicativo chame **SQLSetPos**, ele deve executar a seguinte sequência de etapas:  
  
1.  Se o aplicativo chamará **SQLSetPos** com a *operação* definida como SQL_UPDATE, chame **SQLBindCol** (ou **SQLSetDescRec**) para cada coluna para especificar seu tipo de dados e os buffers de associação para os dados e o comprimento da coluna.  
  
2.  Se o aplicativo chamar **SQLSetPos** com a *operação* definida como SQL_DELETE ou SQL_UPDATE, chame **SQLColAttribute** para certificar-se de que as colunas a serem excluídas ou atualizadas sejam atualizáveis.  
  
3.  Chame **SQLExecDirect**, **SQLExecute**ou uma função de catálogo para criar um conjunto de resultados.  
  
4.  Chame **SQLFetch** ou **SQLFetchScroll** para recuperar os dados.  
  
 Para obter mais informações sobre como usar o **SQLSetPos**, consulte [atualizando dados com o SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md).  
  
## <a name="deleting-data-using-sqlsetpos"></a>Excluindo dados usando SQLSetPos  
 Para excluir dados com **SQLSetPos**, um aplicativo chama **SQLSetPos** com *RowNumber* definido como o número da linha a ser excluída e a *operação* definida como SQL_DELETE.  
  
 Depois que os dados tiverem sido excluídos, o driver altera o valor na matriz de status da linha de implementação da linha apropriada para SQL_ROW_DELETED (ou SQL_ROW_ERROR).  
  
## <a name="updating-data-using-sqlsetpos"></a>Atualizando dados usando SQLSetPos  
 Um aplicativo pode passar o valor de uma coluna no buffer de dados vinculados ou com uma ou mais chamadas para **SQLPutData**. As colunas cujos dados são passados com **SQLPutData** são conhecidas como *colunas*de *dados em execução* . Normalmente, eles são usados para enviar dados para SQL_LONGVARBINARY e SQL_LONGVARCHAR colunas e podem ser misturados com outras colunas.  
  
#### <a name="to-update-data-with-sqlsetpos-an-application"></a>Para atualizar dados com o SQLSetPos, um aplicativo:  
  
1.  Coloca valores nos buffers de dados e de comprimento/indicador associados a **SQLBindCol**:  
  
    -   Para colunas normais, o aplicativo coloca o novo valor de coluna no buffer * \*TargetValuePtr* e o comprimento desse valor no buffer de * \*StrLen_or_IndPtr* . Se a linha não deve ser atualizada, o aplicativo coloca SQL_ROW_IGNORE no elemento dessa linha da matriz de operação de linha.  
  
    -   Para as colunas de dados em execução, o aplicativo coloca um valor definido pelo aplicativo, como o número da coluna, no buffer * \*TargetValuePtr* . O valor pode ser usado posteriormente para identificar a coluna.  
  
         O aplicativo coloca o resultado da macro SQL_LEN_DATA_AT_EXEC (*comprimento*) no buffer **StrLen_or_IndPtr* . Se o tipo de dados SQL da coluna for SQL_LONGVARBINARY, SQL_LONGVARCHAR ou um tipo de dados específico da fonte de dados longa e o driver retornar "Y" para o tipo de informação SQL_NEED_LONG_DATA_LEN em **SQLGetInfo**, *Length* será o número de bytes de dados a serem enviados para o parâmetro; caso contrário, ele deve ser um valor não negativo e será ignorado.  
  
2.  Chama **SQLSetPos** com o argumento de *operação* definido como SQL_UPDATE para atualizar a linha de dados.  
  
    -   Se não houver nenhuma coluna de dados em execução, o processo será concluído.  
  
    -   Se houver qualquer coluna de dados em execução, a função retornará SQL_NEED_DATA e passará para a etapa 3.  
  
3.  Chama **SQLParamData** para recuperar o endereço do buffer * \*TargetValuePtr* para a primeira coluna de dados em execução a ser processada. **SQLParamData** retorna SQL_NEED_DATA. O aplicativo recupera o valor definido pelo aplicativo do buffer * \*TargetValuePtr* .  
  
    > [!NOTE]  
    >  Embora os parâmetros de dados em execução sejam semelhantes a colunas de dados em execução, o valor retornado por **SQLParamData** é diferente para cada um.  
  
    > [!NOTE]  
    >  Os parâmetros de dados em execução são parâmetros em uma instrução SQL para a qual os dados serão enviados com **SQLPutData** quando a instrução for executada com **SQLExecDirect** ou **SQLExecute**. Eles são associados a **SQLBindParameter** ou configurando descritores com **SQLSetDescRec**. O valor retornado por **SQLParamData** é um valor de 32 bits passado para **SQLBindParameter** no argumento *ParameterValuePtr* .  
  
    > [!NOTE]  
    >  As colunas de dados em execução são colunas em um conjunto de linhas para o qual os dados serão enviados com **SQLPutData** quando uma linha for atualizada com **SQLSetPos**. Eles são associados a **SQLBindCol**. O valor retornado por **SQLParamData** é o endereço da linha no buffer **TargetValuePtr* que está sendo processado.  
  
4.  Chama **SQLPutData** uma ou mais vezes para enviar dados para a coluna. Mais de uma chamada será necessária se todos os valores de dados não puderem ser retornados no buffer * \*TargetValuePtr* especificado em **SQLPutData**; várias chamadas para **SQLPutData** para a mesma coluna são permitidas somente ao enviar dados de caractere C para uma coluna com um tipo de dados específico de fonte de caracteres, binário ou de dados ou ao enviar dados binários c para uma coluna com um tipo de dados de caractere, binário ou específico de fonte de dados.  
  
5.  Chama **SQLParamData** novamente para sinalizar que todos os dados foram enviados para a coluna.  
  
    -   Se houver mais colunas de dados em execução, **SQLParamData** retornará SQL_NEED_DATA e o endereço do buffer *TargetValuePtr* para a próxima coluna de dados em execução a ser processada. O aplicativo repete as etapas 4 e 5.  
  
    -   Se não houver mais colunas de dados em execução, o processo será concluído. Se a instrução foi executada com êxito, **SQLParamData** retornará SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO; se a execução falhar, ela retornará SQL_ERROR. Neste ponto, **SQLParamData** pode retornar qualquer SQLSTATE que possa ser retornado por **SQLSetPos**.  
  
 Se os dados tiverem sido atualizados, o driver alterará o valor na matriz de status da linha de implementação da linha apropriada para SQL_ROW_UPDATED.  
  
 Se a operação for cancelada ou ocorrer um erro em **SQLParamData** ou **SQLPutData**, depois que **SQLSetPos** retornar SQL_NEED_DATA e antes de os dados serem enviados para todas as colunas de dados em execução, o aplicativo poderá chamar apenas **SQLCancel**, **SQLGetDiagField**, **SQLGetDiagRec**, **SQLGetFunctions**, **SQLParamData**ou **SQLPutData** para a instrução ou a conexão associada à instrução. Se ele chamar qualquer outra função para a instrução ou a conexão associada à instrução, a função retornará SQL_ERROR e SQLSTATE HY010 (erro de sequência de função).  
  
 Se o aplicativo chamar **SQLCancel** enquanto o driver ainda precisar de dados para as colunas de dados em execução, o driver cancelará a operação. O aplicativo pode então chamar **SQLSetPos** novamente; o cancelamento não afeta o estado do cursor nem a posição atual do cursor.  
  
 Quando a lista de seleção da especificação de consulta associada ao cursor contém mais de uma referência à mesma coluna, se um erro é gerado ou o driver ignora as referências duplicadas e executa as operações solicitadas é definido pelo driver.  
  
## <a name="performing-bulk-operations"></a>Executando operações em massa  
 Se o argumento *RowNumber* for 0, o driver executará a operação especificada no argumento *Operation* para cada linha no conjunto de linhas que tem um valor de SQL_ROW_PROCEED em seu campo na matriz de operação de linha apontada por SQL_ATTR_ROW_OPERATION_PTR atributo de instrução. Este é um valor válido do argumento *RowNumber* para um argumento de *operação* de SQL_DELETE, SQL_REFRESH ou SQL_UPDATE, mas não SQL_POSITION. **SQLSetPos** com uma *operação* de SQL_POSITION e um *RowNumber* igual a 0 retornará SQLSTATE HY109 (posição de cursor inválida).  
  
 Se ocorrer um erro que pertença a todo o conjunto de linhas, como SQLSTATE HYT00 (timeout expirado), o driver retornará SQL_ERROR e o SQLSTATE apropriado. O conteúdo dos buffers de conjunto de linhas é indefinido e a posição do cursor não é alterada.  
  
 Se ocorrer um erro que pertença a uma única linha, o driver:  
  
-   Define o elemento para a linha na matriz de status de linha apontada pelo atributo SQL_ATTR_ROW_STATUS_PTR Statement para SQL_ROW_ERROR.  
  
-   Posta um ou mais hiperestados adicionais para o erro na fila de erros e define o campo SQL_DIAG_ROW_NUMBER na estrutura de dados de diagnóstico.  
  
 Depois de processar o erro ou aviso, se o driver concluir a operação para as linhas restantes no conjunto de linhas, ele retornará SQL_SUCCESS_WITH_INFO. Portanto, para cada linha que retornou um erro, a fila de erros contém zero ou mais sqlstates adicionais. Se o driver parar a operação depois de processar o erro ou aviso, ele retornará SQL_ERROR.  
  
 Se o driver retornar quaisquer avisos, como SQLSTATE 01004 (dados truncados), ele retornará avisos que se aplicam a todo o conjunto de linhas ou a linhas desconhecidas no conjunto de linhas antes de retornar as informações de erro que se aplicam a linhas específicas. Ele retorna avisos para linhas específicas junto com outras informações de erro sobre essas linhas.  
  
 Se *RowNumber* for igual a 0 e a *operação* for SQL_UPDATE, SQL_REFRESH ou SQL_DELETE, o número de linhas em que **SQLSetPos** Opera é apontado pelo atributo da instrução SQL_ATTR_ROWS_FETCHED_PTR.  
  
 Se *RowNumber* for igual a 0 e a *operação* for SQL_DELETE, SQL_REFRESH ou SQL_UPDATE, a linha atual após a operação será a mesma que a linha atual antes da operação.  
  
## <a name="ignoring-a-row-in-a-bulk-operation"></a>Ignorando uma linha em uma operação em massa  
 A matriz de operação de linha pode ser usada para indicar que uma linha no conjunto de linhas atual deve ser ignorada durante uma operação em massa usando **SQLSetPos**. Para instruir o driver a ignorar uma ou mais linhas durante uma operação em massa, um aplicativo deve executar as seguintes etapas:  
  
1.  Chame **SQLSetStmtAttr** para definir o atributo de instrução SQL_ATTR_ROW_OPERATION_PTR para apontar para uma matriz de SQLUSMALLINTs. Esse campo também pode ser definido chamando **SQLSetDescField** para definir o campo de cabeçalho de SQL_DESC_ARRAY_STATUS_PTR do ARD, que exige que um aplicativo obtenha o identificador do descritor.  
  
2.  Defina cada elemento da matriz de operação de linha como um dos dois valores:  
  
    -   SQL_ROW_IGNORE, para indicar que a linha foi excluída para a operação em massa.  
  
    -   SQL_ROW_PROCEED, para indicar que a linha está incluída na operação em massa. (Esse é o valor padrão.)  
  
3.  Chame **SQLSetPos** para executar a operação em massa.  
  
 As regras a seguir se aplicam à matriz de operações de linha:  
  
-   SQL_ROW_IGNORE e SQL_ROW_PROCEED afetam apenas as operações em massa usando **SQLSetPos** com uma *operação* de SQL_DELETE ou SQL_UPDATE. Eles não afetam as chamadas para **SQLSetPos** com uma *operação* de SQL_REFRESH ou SQL_POSITION.  
  
-   O ponteiro é definido como NULL por padrão.  
  
-   Se o ponteiro for nulo, todas as linhas serão atualizadas como se todos os elementos fossem definidos como SQL_ROW_PROCEED.  
  
-   Definir um elemento como SQL_ROW_PROCEED não garante que a operação ocorra nessa linha específica. Por exemplo, se uma determinada linha no conjunto de linhas tiver o status SQL_ROW_ERROR, o driver poderá não ser capaz de atualizar essa linha, independentemente de o aplicativo especificado SQL_ROW_PROCEED. Um aplicativo sempre deve verificar a matriz de status de linha para ver se a operação foi bem-sucedida.  
  
-   SQL_ROW_PROCEED é definido como 0 no arquivo de cabeçalho. Um aplicativo pode inicializar a matriz de operações de linha para 0 a fim de processar todas as linhas.  
  
-   Se o número do elemento "n" na matriz de operação de linha for definido como SQL_ROW_IGNORE e **SQLSetPos** for chamado para executar uma operação de exclusão ou atualização em massa, a enésima linha no conjunto de linhas permanecerá inalterada após a chamada para **SQLSetPos**.  
  
-   Um aplicativo deve definir automaticamente uma coluna somente leitura para SQL_ROW_IGNORE.  
  
## <a name="ignoring-a-column-in-a-bulk-operation"></a>Ignorando uma coluna em uma operação em massa  
 Para evitar o diagnóstico de processamento desnecessário gerado por tentativas de atualizações em uma ou mais colunas somente leitura, um aplicativo pode definir o valor no buffer de indicador/comprimento limite para SQL_COLUMN_IGNORE. Para obter mais informações, consulte [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
## <a name="code-example"></a>Exemplo de código  
 No exemplo a seguir, um aplicativo permite que um usuário procure a tabela ORDERs e atualize o status da ordem. O cursor é controlado por conjuntos de linhas com um tamanho de conjunto de linha de 20 e usa controle de simultaneidade otimista comparando versões de linha. Depois que cada conjunto de linhas é buscado, o aplicativo o imprime e permite que o usuário selecione e atualize o status de um pedido. O aplicativo usa **SQLSetPos** para posicionar o cursor na linha selecionada e executa uma atualização posicionada da linha. (O tratamento de erros é omitido para fins de clareza.)  
  
```cpp  
#define ROWS 20  
#define STATUS_LEN 6  
  
SQLCHAR        szStatus[ROWS][STATUS_LEN], szReply[3];  
SQLINTEGER     cbStatus[ROWS], cbOrderID;  
SQLUSMALLINT   rgfRowStatus[ROWS];  
SQLUINTEGER    sOrderID, crow = ROWS, irow;  
SQLHSTMT       hstmtS, hstmtU;  
  
SQLSetStmtAttr(hstmtS, SQL_ATTR_CONCURRENCY, (SQLPOINTER) SQL_CONCUR_ROWVER, 0);  
SQLSetStmtAttr(hstmtS, SQL_ATTR_CURSOR_TYPE, (SQLPOINTER) SQL_CURSOR_KEYSET_DRIVEN, 0);  
SQLSetStmtAttr(hstmtS, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER) ROWS, 0);  
SQLSetStmtAttr(hstmtS, SQL_ATTR_ROW_STATUS_PTR, (SQLPOINTER) rgfRowStatus, 0);  
SQLSetCursorName(hstmtS, "C1", SQL_NTS);  
SQLExecDirect(hstmtS, "SELECT ORDERID, STATUS FROM ORDERS ", SQL_NTS);  
  
SQLBindCol(hstmtS, 1, SQL_C_ULONG, &sOrderID, 0, &cbOrderID);  
SQLBindCol(hstmtS, 2, SQL_C_CHAR, szStatus, STATUS_LEN, &cbStatus);  
  
while ((retcode == SQLFetchScroll(hstmtS, SQL_FETCH_NEXT, 0)) != SQL_ERROR) {  
   if (retcode == SQL_NO_DATA_FOUND)  
      break;  
   for (irow = 0; irow < crow; irow++) {  
      if (rgfRowStatus[irow] != SQL_ROW_DELETED)  
         printf("%2d %5d %*s\n", irow+1, sOrderID, NAME_LEN-1, szStatus[irow]);  
   }  
   while (TRUE) {  
      printf("\nRow number to update?");  
      gets_s(szReply, 3);  
      irow = atoi(szReply);  
      if (irow > 0 && irow <= crow) {  
         printf("\nNew status?");  
         gets_s(szStatus[irow-1], (ROWS * STATUS_LEN));  
         SQLSetPos(hstmtS, irow, SQL_POSITION, SQL_LOCK_NO_CHANGE);  
         SQLPrepare(hstmtU,  
          "UPDATE ORDERS SET STATUS=? WHERE CURRENT OF C1", SQL_NTS);  
         SQLBindParameter(hstmtU, 1, SQL_PARAM_INPUT,  
            SQL_C_CHAR, SQL_CHAR,  
            STATUS_LEN, 0, szStatus[irow], 0, NULL);  
         SQLExecute(hstmtU);  
      } else if (irow == 0) {  
         break;  
      }  
   }  
}  
```  
  
 Para obter mais exemplos, consulte as [instruções UPDATE e DELETE posicionadas](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md) e [atualizando linhas no conjunto de linhas com SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Associando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Executando operações em massa que não estão relacionadas à posição do cursor de bloco|[Função SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Buscando um bloco de dados ou rolando por meio de um conjunto de resultados|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Obtendo um único campo de um descritor|[Função SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Obtendo vários campos de um descritor|[Função SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Definindo um único campo de um descritor|[Função SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Configurando vários campos de um descritor|[Função SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|Definindo um atributo de instrução|[Função SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
