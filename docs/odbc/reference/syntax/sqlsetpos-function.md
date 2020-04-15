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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7a8839f1ae540ac9e5f29e144f7f57fb754e50ff
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287326"
---
# <a name="sqlsetpos-function"></a>Função SQLSetPos
**Conformidade**  
 Versão introduzida: ODBC 1.0 Normas Conformidade: ODBC  
  
 **Resumo**  
 **SQLSetPos** define a posição do cursor em um conjunto de linhas e permite que um aplicativo atualize dados no conjunto de linhas ou atualize ou exclua dados no conjunto de resultados.  
  
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
 [Entrada] Alça de declaração.  
  
 *Rownumber*  
 [Entrada] Posição da linha no conjunto de linhas para executar a operação especificada com o argumento *Operação.* Se *O Número de* linhas for 0, a operação se aplica a todas as linhas do conjunto de linhas.  
  
 Para obter informações adicionais, consulte "Comentários".  
  
 *Operação*  
 [Entrada] Operação a ser realizado:  
  
 SQL_POSITION SQL_REFRESH SQL_UPDATE SQL_DELETE  
  
> [!NOTE]
>  O valor SQL_ADD para o argumento da *Operação* foi preterido para o ODBC *3.x*. Os drivers ODBC *3.x* precisarão suportar SQL_ADD para compatibilidade retrógrada. Essa funcionalidade foi substituída por uma chamada para **SQLBulkOperations** por uma *operação* de SQL_ADD. Quando um aplicativo ODBC *3.x* funciona com um driver ODBC *2.x,* o Driver Manager mapeia uma chamada para **SQLBulkOperations** com uma *operação* de SQL_ADD para **SQLSetPos** com uma *operação* de SQL_ADD.  
  
 Para obter mais informações, consulte "Comentários".  
  
 *Locktype*  
 [Entrada] Especifica como bloquear a linha após a execução da operação especificada no argumento *Operação.*  
  
 SQL_LOCK_NO_CHANGE SQL_LOCK_EXCLUSIVE SQL_LOCK_UNLOCK  
  
 Para obter mais informações, consulte "Comentários".  
  
 **Retorna**  
  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLSetPos** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **sqlGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *alça* de *statementHandle*. A tabela a seguir lista os valores SQLSTATE comumente retornados por **SQLSetPos** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
 Para todos os SQLSTATEs que podem retornar SQL_SUCCESS_WITH_INFO ou SQL_ERROR (exceto 01xxx SQLSTATEs), SQL_SUCCESS_WITH_INFO é devolvido se ocorrer um erro em uma ou mais linhas, mas não todas, linhas de uma operação multirow, e SQL_ERROR é devolvida se ocorrer um erro em uma operação de linha única.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01001|Conflito de operação do cursor|O argumento *da Operação* foi SQL_DELETE ou SQL_UPDATE, e nenhuma linha ou mais de uma linha foi excluída ou atualizada. (Para obter mais informações sobre atualizações em mais de uma linha, consulte a descrição do *atributo* SQL_ATTR_SIMULATE_CURSOR em **SQLSetStmtAttr**.) (Função retorna SQL_SUCCESS_WITH_INFO.)<br /><br /> O argumento *da Operação* foi SQL_DELETE ou SQL_UPDATE, e a operação falhou por causa da concorrência otimista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Truncação de dados de seqüência|O argumento *Operação* foi SQL_REFRESH, e os dados de seqüência ou binário retornados para uma coluna ou colunas com um tipo de SQL_C_CHAR ou SQL_C_BINARY resultaram na truncação de caracteres não em branco ou dados binários não-NULOS.|  
|01S01|Erro na linha|O argumento *'Número de linhas'* foi 0, e ocorreu um erro em uma ou mais linhas durante a execução da operação especificada com o argumento *Operação.*<br /><br /> (SQL_SUCCESS_WITH_INFO é devolvido se ocorrer um erro em uma ou mais linhas, mas não todas, linhas de uma operação multirow e SQL_ERROR é devolvida se ocorrer um erro em uma operação de linha única.)<br /><br /> (Este SQLSTATE é retornado somente quando **o SQLSetPos** é chamado após **o SQLExtendedFetch,** se o driver for um driver ODBC *2.x* e a biblioteca do cursor não for usada.)|  
|01S07|Truncação fracionada|O argumento *da Operação* era SQL_REFRESH, o tipo de dados do buffer do aplicativo não era SQL_C_CHAR ou SQL_C_BINARY, e os dados devolvidos aos buffers de aplicativos para uma ou mais colunas eram truncados. Para os tipos de dados numéricos, a parte fracionada do número foi truncada. Por tempo, carimbo de tempo e tipos de dados de intervalo contendo um componente de tempo, a parte fracionada do tempo foi truncada.<br /><br /> (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|07006|Violação de atributo de tipo de dados restrito|O valor de dados de uma coluna no conjunto de resultados não pôde ser convertido para o tipo de dados especificado pelo *TargetType* na chamada para **SQLBindCol**.|  
|07009|Índice de descritor inválido|O argumento *Operação* era SQL_REFRESH ou SQL_UPDATE, e uma coluna estava vinculada com um número de coluna maior do que o número de colunas no conjunto de resultados.|  
|21S02|Grau de tabela derivada não corresponde à lista de colunas|O argumento *Operação* foi SQL_UPDATE, e nenhuma coluna foi updatable porque todas as colunas estavam desvinculadas, somente leitura, ou o valor no buffer de comprimento/indicador de limite estava SQL_COLUMN_IGNORE.|  
|22001|Dados de cordas, truncação direita|O argumento *Operação* foi SQL_UPDATE, e a atribuição de um caractere ou valor binário para uma coluna resultou na truncação de caracteres ou bytes não em branco (para caracteres) ou não nulos (para binários).|  
|22003|Valor numérico fora do alcance|O argumento *da Operação* foi SQL_UPDATE, e a atribuição de um valor numérico a uma coluna no conjunto de resultados fez com que a parte total (em oposição à fracionária) do número fosse truncada.<br /><br /> O argumento *operação* foi SQL_REFRESH, e devolver o valor numérico para uma ou mais colunas vinculadas teria causado uma perda de dígitos significativos.|  
|22007|Formato de data-hora inválido|O argumento *Operação* foi SQL_UPDATE, e a atribuição de um valor de data ou carimbo de data para uma coluna no conjunto de resultados fez com que o campo de ano, mês ou dia ficasse fora de alcance.<br /><br /> O argumento *Operação* foi SQL_REFRESH, e devolver o valor da data ou carimbo de data para uma ou mais colunas vinculadas teria feito com que o campo de ano, mês ou dia estivesse fora de alcance.|  
|22008|Estouro do campo de data/hora|O argumento *da Operação* foi SQL_UPDATE, e o desempenho da aritmética data-hora sobre os dados enviados a uma coluna no conjunto de resultados resultou em um campo de data-hora (ano, mês, dia, hora, minuto ou segundo campo) do resultado estar fora da faixa de valores admissível para o campo, ou ser inválido com base nas regras naturais do calendário gregoriano para datas.<br /><br /> O argumento *da Operação* foi SQL_REFRESH, e o desempenho da aritmética data-hora sobre os dados recuperados do conjunto de resultados resultou em um campo de data (ano, mês, dia, hora, minuto ou segundo campo) do resultado estar fora da faixa de valores permitida para o campo, ou ser inválido com base nas regras naturais do calendário gregoriano para datas.|  
|22015|Estouro do campo de intervalo|O argumento *operação* foi SQL_UPDATE, e a atribuição de um tipo c numérico ou intervalo exato para um tipo de dados SQL intervalado causou uma perda de dígitos significativos.<br /><br /> O argumento *da Operação* foi SQL_UPDATE; ao atribuir a um tipo SQL de intervalo, não houve representação do valor do tipo C no tipo SQL de intervalo.<br /><br /> O argumento *operação* foi SQL_REFRESH, e atribuir de um tipo sql numérico ou intervalado exato para um tipo de intervalo C causou uma perda de dígitos significativos no campo principal.<br /><br /> O argumento *da Operação* foi SQL_ REFRESH; ao atribuir a um tipo de intervalo C, não houve representação do valor do tipo SQL no tipo C do intervalo.|  
|22018|Valor de caractere inválido para especificação do elenco|O argumento *da Operação* foi SQL_REFRESH; o tipo C era um numérico exato ou aproximado, um período de data ou um tipo de dados de intervalo; o tipo SQL da coluna era um tipo de dados de caracteres; e o valor na coluna não era um literal válido do tipo C ligado.<br /><br /> O argumento *operação* foi SQL_UPDATE; o tipo SQL era um numérico exato ou aproximado, um período de data ou um tipo de dados de intervalo; o tipo C foi SQL_C_CHAR; e o valor na coluna não era um literal válido do tipo SQL vinculado.|  
|23000|Violação de restrição de integridade|O argumento *da Operação* foi SQL_DELETE ou SQL_UPDATE, e uma restrição de integridade foi violada.|  
|24.000|Estado de cursor inválido|O *StatementHandle* estava em um estado executado, mas nenhum conjunto de resultados foi associado ao *StatementHandle*.<br /><br /> (DM) Um cursor foi aberto no *StatementHandle,* mas **sQLFetchou-se** não havia sido chamado. **SQLFetchScroll**<br /><br /> Um cursor foi aberto no *StatementHandle*, e **SQLFetch** ou **SQLFetchScroll** foram chamados, mas o cursor foi posicionado antes do início do conjunto de resultados ou após o fim do conjunto de resultados.<br /><br /> O argumento *Operação* foi SQL_DELETE, SQL_REFRESH ou SQL_UPDATE, e o cursor foi posicionado antes do início do conjunto de resultados ou após o término do conjunto de resultados.|  
|40001|Falha na serialização|A transação foi revertida devido a um impasse de recursos com outra transação.|  
|40003|Conclusão de declaração desconhecida|A conexão associada falhou durante a execução desta função, e o estado da transação não pode ser determinado.|  
|42000|Erro de sintaxe ou violação de acesso|O motorista não conseguiu travar a linha conforme necessário para realizar a operação solicitada no argumento *Operação*.<br /><br /> O driver não conseguiu bloquear a linha conforme solicitado no argumento *LockType*.|  
|44000|Violação COM OPÇÃO DE VERIFICAÇÃO|O argumento *Operação* foi SQL_UPDATE, e a atualização foi realizada em uma tabela visualizada ou em uma tabela derivada da tabela visualizada que foi criada especificando **COM OPÇÃO DE VERIFICAÇÃO,** de tal forma que uma ou mais linhas afetadas pela atualização não estarão mais presentes na tabela visualizada.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*e, em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **sqlCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um segmento diferente em um aplicativo multithread.|  
|HY010|Erro de seqüência de função|(DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *StatementHandle*. Esta função assíncrona ainda estava sendo executada quando a função SQLSetPos foi chamada.<br /><br /> (DM) O *StatementHandle* especificado não estava em um estado executado. A função foi chamada sem antes chamar **SQLExecDirect,** **SQLExecute**ou uma função de catálogo.<br /><br /> (DM) Uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados para o *StatementHandle* e retornaram SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.<br /><br /> (DM) O driver era um Driver ODBC *2.x,* e **o SQLSetPos** foi chamado para um *StatementHandle* depois que **o SQLFetch** foi chamado.|  
|HY011|Atributo não pode ser definido agora|(DM) O motorista era um driver ODBC *2.x;* o SQL_ATTR_ROW_STATUS_PTR atributo de declaração foi definido; em seguida, **SQLSetPos** foi chamado antes **de SQLFetch**, **SQLFetchScroll**, ou **SQLExtendedFetch** foi chamado.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY090|Comprimento de seqüência ou buffer inválido|O argumento *da Operação* era SQL_UPDATE, um valor de dados era nulo, e o valor do comprimento da coluna não era 0, SQL_DATA_AT_EXEC, SQL_COLUMN_IGNORE, SQL_NULL_DATA ou menor ou igual a SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> O argumento *da Operação* foi SQL_UPDATE; um valor de dados não era um ponteiro nulo; o tipo de dados C foi SQL_C_BINARY ou SQL_C_CHAR; e o valor do comprimento da coluna foi inferior a 0, mas não igual a SQL_DATA_AT_EXEC, SQL_COLUMN_IGNORE, SQL_NTS ou SQL_NULL_DATA, ou menor ou igual a SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> O valor em um buffer de comprimento/indicador foi SQL_DATA_AT_EXEC; o tipo SQL foi SQL_LONGVARCHAR, SQL_LONGVARBINARY ou um tipo de dados específico de origem de dados longos; e o SQL_NEED_LONG_DATA_LEN tipo de informação no **SQLGetInfo** foi "Y".|  
|HY092|Identificador de atributo inválido|(DM) O valor especificado para o argumento da *Operação* era inválido.<br /><br /> (DM) O valor especificado para o argumento *LockType* era inválido.<br /><br /> O argumento da *Operação* foi SQL_UPDATE ou SQL_DELETE, e o atributo de declaração SQL_ATTR_CONCURRENCY foi SQL_ATTR_CONCUR_READ_ONLY.|  
|HY107|Valor da linha fora do alcance|O valor especificado para o argumento *RowNumber* foi maior do que o número de linhas no conjunto de linhas.|  
|HY109|Posição do cursor inválido|O cursor associado ao *StatementHandle* foi definido como somente para a frente, de modo que o cursor não poderia ser posicionado dentro do conjunto de linhas. Consulte a descrição do atributo SQL_ATTR_CURSOR_TYPE em **SQLSetStmtAttr**.<br /><br /> O argumento *da Operação* foi SQL_UPDATE, SQL_DELETE ou SQL_REFRESH, e a linha identificada pelo argumento *RowNumber* havia sido excluída ou não havia sido buscada.<br /><br /> (DM) O argumento *RowNumber* era 0, e o argumento da *Operação* foi SQL_POSITION.<br /><br /> **SQLSetPos** foi chamado depois **que sqlBulkOperations** foi chamado e antes **de SQLFetchScroll** ou **SQLFetch** foi chamado.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|O driver ou a fonte de dados não suportam a operação solicitada no argumento *operação* ou no argumento *LockType.*|  
|HYT00|Tempo limite esgotado|O período de tempo de consulta expirou antes que a fonte de dados retornasse o conjunto de resultados. O período de tempo é definido através **de SQLSetStmtAttr** com um *atributo* de SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *StatementHandle* não suporta a função.|  
|IM017|A votação é desativada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a votação é desativada.|  
|IM018|**O SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesta alça.|Se a chamada de função anterior na alça retornar SQL_STILL_EXECUTING e se o modo de notificação estiver ativado, o **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
  
> [!CAUTION]
>  Para obter informações sobre a declaração, afirma que os **SQLSetPos** podem ser chamados e o que ele precisa fazer para compatibilidade com aplicativos ODBC *2.x,* consulte [Cursors de bloco, cursors roláveis e compatibilidade retrógrada.](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)  
  
## <a name="rownumber-argument"></a>Argumento de número de linha  
 O argumento *''''Número de* linhas' especifica o número da linha no conjunto de linhas para executar a operação especificada pelo argumento *Operação.* Se *O Número de* linhas for 0, a operação se aplica a todas as linhas do conjunto de linhas. *RowNumber* deve ser um valor de 0 para o número de linhas no conjunto de linhas.  
  
> [!NOTE]  
>  No idioma C, as matrizes são baseadas em 0 e o argumento *RowNumber* é baseado em 1. Por exemplo, para atualizar a quinta linha do conjunto de linhas, um aplicativo modifica os buffers de conjunto de linhas no índice de array 4, mas especifica uma *linhaNúmero* de 5.  
  
 Todas as operações posicionam o cursor na linha especificada por *RowNumber*. As seguintes operações requerem uma posição cursor:  
  
-   Atualização posicionada e exclusão de declarações.  
  
-   Chamadas para **SQLGetData**.  
  
-   Chamadas para **SQLSetPos** com as opções de SQL_DELETE, SQL_REFRESH e SQL_UPDATE.  
  
 Por exemplo, se *RowNumber* for 2 para uma chamada para **SQLSetPos** com uma *operação* de SQL_DELETE, o cursor será posicionado na segunda linha do conjunto de linhas e essa linha será excluída. A entrada na matriz de status da linha de implementação (apontada pelo atributo de declaração SQL_ATTR_ROW_STATUS_PTR) para a segunda linha é alterada para SQL_ROW_DELETED.  
  
 Um aplicativo pode especificar uma posição do cursor quando ele chama **SQLSetPos**. Geralmente, ele chama **SQLSetPos** com a operação SQL_POSITION ou SQL_REFRESH para posicionar o cursor antes de executar uma atualização posicionada ou excluir declaração ou ligar para **sQLGetData**.  
  
## <a name="operation-argument"></a>Argumento da Operação  
 O argumento *da Operação* apoia as seguintes operações. Para determinar quais opções são suportadas por uma fonte de dados, um aplicativo chama **SQLGetInfo** com o SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 ou SQL_STATIC_CURSOR_ATTRIBUTES1 tipo de informação (dependendo do tipo do cursor).  
  
|*Operação*<br /><br /> argumento|Operação|  
|------------------------------|---------------|  
|SQL_POSITION|O driver posiciona o cursor na linha especificada por *RowNumber*.<br /><br /> O conteúdo da matriz de status da linha apontada pelo atributo de declaração SQL_ATTR_ROW_OPERATION_PTR é ignorado para a *Operação*SQL_POSITION .|  
|SQL_REFRESH|O driver posiciona o cursor na linha especificada por *RowNumber* e atualiza os dados nos buffers do conjunto de linhas para essa linha. Para obter mais informações sobre como o driver retorna os dados nos buffers do conjunto de linhas, consulte as descrições de vinculação em termos de linha e em termos de coluna no **SQLBindCol**.<br /><br /> **SQLSetPos** com uma *operação* de SQL_REFRESH atualiza o status e o conteúdo das linhas dentro do conjunto de linhas buscadas atual. Isso inclui refrescar os marcadores. Como os dados nos buffers são atualizados, mas não rebuscados, a adesão no conjunto de linhas é corrigida. Isso é diferente da atualização realizada por uma chamada para **SQLFetchScroll** com uma *Orientação de SQL_FETCH_RELATIVE* e um Número de *Linha* igual a 0, que rebusca o conjunto de linhas do conjunto de resultados para que ele possa mostrar dados adicionados e remover dados excluídos se essas operações forem suportadas pelo driver e pelo cursor.<br /><br /> Uma atualização bem-sucedida com **SQLSetPos** não mudará o status de linha de SQL_ROW_DELETED. As linhas excluídas dentro do conjunto de linhas continuarão a ser marcadas como excluídas até a próxima busca. As linhas desaparecerão na próxima busca se o cursor suportar a embalagem (na qual um **SQLFetchScroll** ou **SQLFetchScroll** subseqüente não retorna linhas excluídas).<br /><br /> As linhas adicionadas não aparecem quando uma atualização com **SQLSetPos** é executada. Esse comportamento é diferente do **SQLFetchScroll** com um *FetchType* de SQL_FETCH_RELATIVE e um *RowNumber* igual a 0, que também atualiza o conjunto de linhas atual, mas mostrará registros adicionados ou registros excluídos se essas operações forem suportadas pelo cursor.<br /><br /> Uma atualização bem-sucedida com **SQLSetPos** mudará o status de linha de SQL_ROW_ADDED para SQL_ROW_SUCCESS (se a matriz de status da linha existir).<br /><br /> Uma atualização bem-sucedida com **SQLSetPos** mudará o status de linha de SQL_ROW_UPDATED para o novo status da linha (se a matriz de status da linha existir).<br /><br /> Se ocorrer um erro em uma operação **SQLSetPos** em uma linha, o status da linha será definido como SQL_ROW_ERROR (se a matriz de status da linha existir).<br /><br /> Para um cursor aberto com um atributo de declaração SQL_ATTR_CONCURRENCY de SQL_CONCUR_ROWVER ou SQL_CONCUR_VALUES, uma atualização com **SQLSetPos** pode atualizar os valores de concorrência otimistas usados pela fonte de dados para detectar que a linha foi alterada. Se isso ocorrer, as versões de linha ou valores usados para garantir que a concorrência do cursor seja atualizada sempre que os buffers do conjunto de linhas forem atualizados do servidor. Isso ocorre para cada linha que é atualizada.<br /><br /> O conteúdo da matriz de status da linha apontada pelo atributo de declaração SQL_ATTR_ROW_OPERATION_PTR é ignorado para a *Operação*SQL_REFRESH .|  
|SQL_UPDATE|O driver posiciona o cursor na linha especificada por *RowNumber* e atualiza a linha de dados subjacente com os valores nos buffers de conjunto de linhas (o argumento *TargetValuePtr* no **SQLBindCol**). Ele recupera os comprimentos dos dados dos buffers de comprimento/indicador (o *StrLen_or_IndPtr* argumento no **SQLBindCol**). Se o comprimento de qualquer coluna for SQL_COLUMN_IGNORE, a coluna não será atualizada. Após atualizar a linha, o driver altera o elemento correspondente da matriz de status da linha para SQL_ROW_UPDATED ou SQL_ROW_SUCCESS_WITH_INFO (se a matriz de status da linha existir).<br /><br /> É definido pelo driver qual é o comportamento se **SQLSetPos** com um argumento de *Operação* de SQL_UPDATE é chamado em um cursor que contém colunas duplicadas. O driver pode retornar um SQLSTATE definido pelo driver, atualizar a primeira coluna que aparece no conjunto de resultados ou executar outro comportamento definido pelo driver.<br /><br /> O array de operação de linha apontado pelo atributo de declaração SQL_ATTR_ROW_OPERATION_PTR pode ser usado para indicar que uma linha no conjunto de linhas atual deve ser ignorada durante uma atualização em massa. Para obter mais informações, consulte "Matrizes de status e operação" mais tarde nesta referência de função.|  
|SQL_DELETE|O driver posiciona o cursor na linha especificada por *RowNumber* e exclui a linha de dados subjacente. Ele altera o elemento correspondente da matriz de status da linha para SQL_ROW_DELETED. Depois que a linha foi excluída, as seguintes não são válidas para a linha: instruções de atualização e exclusão posicionadas, chamadas para **SQLGetData**e chamadas para **SQLSetPos** com *Operação* definida sem qualquer SQL_POSITION. Para os drivers que suportam a embalagem, a linha é excluída do cursor quando novos dados são recuperados da fonte de dados.<br /><br /> Se a linha permanece visível depende do tipo do cursor. Por exemplo, as linhas excluídas são visíveis para cursores estáticos e orientados por conjuntos de chaves, mas invisíveis aos cursores dinâmicos.<br /><br /> O array de operação de linha apontado pelo atributo de declaração SQL_ATTR_ROW_OPERATION_PTR pode ser usado para indicar que uma linha no conjunto de linhas atual deve ser ignorada durante uma exclusão em massa. Para obter mais informações, consulte "Matrizes de status e operação" mais tarde nesta referência de função.|  
  
## <a name="locktype-argument"></a>Argumento locktype  
 O argumento *LockType* fornece uma maneira de os aplicativos controlarem a concorrência. Na maioria dos casos, as fontes de dados que suportam níveis de sie e transações suportarão apenas o valor SQL_LOCK_NO_CHANGE do argumento *LockType.* O argumento *LockType* é geralmente usado apenas para suporte baseado em arquivos.  
  
 O argumento *LockType* especifica o estado de bloqueio da linha após a execução **de SQLSetPos.** Se o driver não conseguir bloquear a linha para realizar a operação solicitada ou para satisfazer o argumento *LockType,* ele retorna SQL_ERROR e SQLSTATE 42000 (erro de sintaxe ou violação de acesso).  
  
 Embora o argumento *LockType* seja especificado para uma única instrução, o bloqueio concede os mesmos privilégios a todas as declarações sobre a conexão. Em particular, um bloqueio adquirido por uma declaração em uma conexão pode ser desbloqueado por uma declaração diferente na mesma conexão.  
  
 Uma linha bloqueada através **de SQLSetPos** permanece bloqueada até que o aplicativo chame **SQLSetPos** para a linha com *LockType* definida como SQL_LOCK_UNLOCK, ou até que o aplicativo chame **SQLFreeHandle** para a declaração ou **SQLFreeStmt** com a opção SQL_CLOSE. Para um driver que suporta transações, uma linha bloqueada através de **SQLSetPos é desbloqueada** quando o aplicativo chama **o SQLEndTran** para cometer ou reverter uma transação na conexão (se um cursor for fechado quando uma transação for realizada ou revertida, conforme indicado pelo SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR tipos de informações devolvidos pelo **SQLGetInfo**).  
  
 O argumento *LockType* suporta os seguintes tipos de bloqueios. Para determinar quais bloqueios são suportados por uma fonte de dados, um aplicativo chama **SQLGetInfo** com o SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 ou SQL_STATIC_CURSOR_ATTRIBUTES1 tipo de informação (dependendo do tipo do cursor).  
  
|*Argumento LockType*|Tipo de bloqueio|  
|-------------------------|---------------|  
|SQL_LOCK_NO_CHANGE|O driver ou a fonte de dados garante que a linha esteja no mesmo estado bloqueado ou desbloqueado que era antes **de SQLSetPos** ser chamado. Esse valor do *LockType* permite que fontes de dados que não suportam bloqueio explícito em nível de linha usem o bloqueio necessário pelos níveis de sionismo e isolamento de transações atuais.|  
|SQL_LOCK_EXCLUSIVE|O driver ou a fonte de dados bloqueia a linha exclusivamente. Uma declaração em uma conexão diferente ou em um aplicativo diferente não pode ser usada para adquirir quaisquer bloqueios na linha.|  
|SQL_LOCK_UNLOCK|O driver ou fonte de dados desbloqueia a linha.|  
  
 Se um driver suportar SQL_LOCK_EXCLUSIVE mas não suportar SQL_LOCK_UNLOCK, uma linha bloqueada permanecerá bloqueada até que ocorra uma das chamadas de função descritas no parágrafo anterior.  
  
 Se um driver suportar SQL_LOCK_EXCLUSIVE mas não tiver suporte SQL_LOCK_UNLOCK, uma linha bloqueada permanecerá bloqueada até que o aplicativo ligue para **o SQLFreeHandle** para a declaração ou **SQLFreeStmt** com a opção SQL_CLOSE. Se o driver suportar transações e fechar o cursor ao cometer ou reverter a transação, o aplicativo chamará **SQLEndTran**.  
  
 Para as operações de atualização e exclusão em **SQLSetPos,** o aplicativo usa o argumento *LockType* da seguinte forma:  
  
-   Para garantir que uma linha não mude depois de recuperada, um aplicativo chama **SQLSetPos** com *Operação* definida para SQL_REFRESH e *LockType* definido como SQL_LOCK_EXCLUSIVE.  
  
-   Se o aplicativo definir *LockType* como SQL_LOCK_NO_CHANGE, o driver garante que uma operação de atualização ou exclusão só será bem sucedida se o aplicativo especificado SQL_CONCUR_LOCK para o atributo de declaração SQL_ATTR_CONCURRENCY.  
  
-   Se o aplicativo especificar SQL_CONCUR_ROWVER ou SQL_CONCUR_VALUES para o atributo de declaração SQL_ATTR_CONCURRENCY, o motorista compara versões ou valores da linha e rejeita a operação se a linha tiver sido alterada desde que o aplicativo buscou a linha.  
  
-   Se o aplicativo especificar SQL_CONCUR_READ_ONLY para o atributo de declaração SQL_ATTR_CONCURRENCY, o driver rejeitará qualquer operação de atualização ou exclusão.  
  
 Para obter mais informações sobre o atributo de declaração SQL_ATTR_CONCURRENCY, consulte [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
## <a name="status-and-operation-arrays"></a>Matrizes de status e operação  
 Os seguintes arrays de status e operação são usados ao ligar para **SQLSetPos:**  
  
-   O array de status da linha (conforme apontado pelo campo SQL_DESC_ARRAY_STATUS_PTR no IRD e o atributo de declaração SQL_ATTR_ROW_STATUS_ARRAY) contém valores de status para cada linha de dados no conjunto de linhas. O driver define os valores de status nesta matriz após uma chamada para **SQLFetch,** **SQLFetchScroll,** **SQLBulkOperations**ou **SQLSetPos**. Esta matriz é apontada pelo atributo de declaração SQL_ATTR_ROW_STATUS_PTR.  
  
-   O array de operação de linha (como apontado pelo campo SQL_DESC_ARRAY_STATUS_PTR no ARD e o atributo de declaração SQL_ATTR_ROW_OPERATION_ARRAY) contém um valor para cada linha no conjunto de linhas que indica se uma chamada para **SQLSetPos** para uma operação em massa é ignorada ou realizada. Cada elemento na matriz é definido como SQL_ROW_PROCEED (o padrão) ou SQL_ROW_IGNORE. Esta matriz é apontada pelo atributo de declaração SQL_ATTR_ROW_OPERATION_PTR.  
  
 O número de elementos nos arrays de status e operação deve ser igual ao número de linhas no conjunto de linhas (conforme definido pelo atributo de declaração SQL_ATTR_ROW_ARRAY_SIZE).  
  
 Para obter informações sobre a matriz de status da linha, consulte [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md). Para obter informações sobre o array de operação de linha, consulte "Ignorando uma linha em uma operação em massa", mais tarde nesta seção.  
  
## <a name="using-sqlsetpos"></a>Usando SQLSetPos  
 Antes que um aplicativo chame **SQLSetPos,** ele deve executar a seguinte seqüência de etapas:  
  
1.  Se o aplicativo chamar **SQLSetPos** com *operação* definida para SQL_UPDATE, ligue para **SQLBindCol** (ou **SQLSetDescRec)** para que cada coluna especifique seu tipo de dados e vincule buffers para os dados e comprimento da coluna.  
  
2.  Se o aplicativo chamar **SQLSetPos** com *Operação* definida para SQL_DELETE ou SQL_UPDATE, ligue para **o SQLColAttribute** para garantir que as colunas a serem excluídas ou atualizadas sejam atualizadas.  
  
3.  Ligue para **SQLExecDirect,** **SQLExecute**ou para criar um conjunto de resultados.  
  
4.  Ligue para **SQLFetch** ou **SQLFetchScroll** para recuperar os dados.  
  
 Para obter mais informações sobre o uso de **SQLSetPos,** consulte [Atualizar dados com SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md).  
  
## <a name="deleting-data-using-sqlsetpos"></a>Excluindo dados usando SQLSetPos  
 Para excluir dados com **SQLSetPos,** um aplicativo chama **SQLSetPos** com *RowNumber* definido para o número da linha a ser excluída e *operação* definida como SQL_DELETE.  
  
 Depois que os dados foram excluídos, o driver altera o valor na matriz de status da linha de implementação para a linha apropriada para SQL_ROW_DELETED (ou SQL_ROW_ERROR).  
  
## <a name="updating-data-using-sqlsetpos"></a>Atualizando dados usando SQLSetPos  
 Um aplicativo pode passar o valor para uma coluna no buffer de dados vinculado ou com uma ou mais chamadas para **SQLPutData**. As colunas cujos dados são passados com **sqlPutData** são conhecidas como *colunas* *de data-in-execution* . Estes são comumente usados para enviar dados para colunas SQL_LONGVARBINARY e SQL_LONGVARCHAR e podem ser misturados com outras colunas.  
  
#### <a name="to-update-data-with-sqlsetpos-an-application"></a>Para atualizar dados com SQLSetPos, um aplicativo:  
  
1.  Coloca valores nos buffers de dados e comprimento/indicador vinculados ao **SQLBindCol**:  
  
    -   Para colunas normais, o aplicativo coloca o novo valor de coluna no buffer * \*TargetValuePtr* e o comprimento desse valor no * \** buffer de StrLen_or_IndPtr. Se a linha não for atualizada, o aplicativo colocará SQL_ROW_IGNORE no elemento dessa linha do array de operação de linha.  
  
    -   Para colunas de dados em execução, o aplicativo coloca um valor definido pelo aplicativo, como o número da coluna, no * \*buffer TargetValuePtr.* O valor pode ser usado posteriormente para identificar a coluna.  
  
         O aplicativo coloca o resultado da macro SQL_LEN_DATA_AT_EXEC *(comprimento)* no tampão*de StrLen_or_IndPtr* * . Se o tipo de dados SQL da coluna for SQL_LONGVARBINARY, SQL_LONGVARCHAR ou um tipo de dados específico de origem de dados longo e o driver retornar "Y" para o SQL_NEED_LONG_DATA_LEN tipo de informação no **SQLGetInfo,** *o comprimento* é o número de bytes de dados a serem enviados para o parâmetro; caso contrário, deve ser um valor não negativo e é ignorado.  
  
2.  Chama **SQLSetPos** com o argumento *Operação* definido para SQL_UPDATE atualizar a linha de dados.  
  
    -   Se não houver colunas de dados em execução, o processo será concluído.  
  
    -   Se houver colunas de dados em execução, a função retorna SQL_NEED_DATA e segue para a etapa 3.  
  
3.  Chama **SQLParamData** para recuperar o endereço do buffer * \*TargetValuePtr* para que a primeira coluna de dados em execução seja processada. **SQLParamData** retorna SQL_NEED_DATA. O aplicativo recupera o valor definido * \** pelo aplicativo a partir do buffer TargetValuePtr.  
  
    > [!NOTE]  
    >  Embora os parâmetros de data-at-execution sejam semelhantes às colunas de dados em execução, o valor retornado pelo **SQLParamData** é diferente para cada um.  
  
    > [!NOTE]  
    >  Os parâmetros de data-at-execution são parâmetros em uma declaração SQL para a qual os dados serão enviados com **sQLPutData** quando a declaração for executada com **SQLExecDirect** ou **SQLExecute**. Eles estão vinculados ao **SQLBindParameter** ou pela definição de descritores com **SQLSetDescRec**. O valor retornado pelo **SQLParamData** é um valor de 32 bits passado para **SQLBindParameter** no argumento *ParameterValuePtr.*  
  
    > [!NOTE]  
    >  As colunas de dados em execução são colunas em um conjunto de linhas para os quais os dados serão enviados com **sQLPutData** quando uma linha é atualizada com **SQLSetPos**. Eles estão ligados ao **SQLBindCol**. O valor retornado pelo **SQLParamData** é o endereço da linha no buffer ** TargetValuePtr* que está sendo processado.  
  
4.  Chama **sqlPutData** uma ou mais vezes para enviar dados para a coluna. Mais de uma chamada é necessária se todos os valores de dados não puderem ser retornados no buffer * \*TargetValuePtr* especificado no **SQLPutData;** várias chamadas para **SQLPutData** para a mesma coluna são permitidas apenas ao enviar dados c de caracteres para uma coluna com um tipo de dados específico de origem de caracteres, binários ou de origem de dados ou ao enviar dados C binários para uma coluna com um tipo de dados específico de origem de caracteres, binários ou de origem de dados.  
  
5.  Chama **sqlParamData** novamente para sinalizar que todos os dados foram enviados para a coluna.  
  
    -   Se houver mais colunas de dados em execução, **o SQLParamData** retorna SQL_NEED_DATA e o endereço do buffer *TargetValuePtr* para que a próxima coluna data-at-execution seja processada. O aplicativo repete as etapas 4 e 5.  
  
    -   Se não houver mais colunas de dados em execução, o processo será concluído. Se a declaração foi executada com sucesso, **o SQLParamData** retorna SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO; se a execução falhar, ela retorna SQL_ERROR. Neste ponto, **o SQLParamData** pode retornar qualquer SQLSTATE que possa ser devolvido por **SQLSetPos**.  
  
 Se os dados forem atualizados, o driver altera o valor na matriz de status da linha de implementação para a linha apropriada para SQL_ROW_UPDATED.  
  
 Se a operação for cancelada ou ocorrer um erro no **SQLParamData** ou **no SQLPutData,** após o **Retorno do SQLSetPos** SQL_NEED_DATA e antes que os dados sejam enviados para todas as colunas de dados em execução, o aplicativo pode chamar apenas **SQLCancel,** **SQLGetDiagField,** **SQLGetDiagRec**, **SQLGetFunctions**, **SQLParamData**, ou **SQLPutData** para a declaração Se ele chamar qualquer outra função para a declaração ou a conexão associada à declaração, a função retorna SQL_ERROR e SQLSTATE HY010 (erro de seqüência de função).  
  
 Se o aplicativo chamar **SQLCancel** enquanto o driver ainda precisa de dados para colunas de dados em execução, o driver cancelará a operação. O aplicativo pode então chamar **SQLSetPos** novamente; o cancelamento não afeta o estado do cursor ou a posição atual do cursor.  
  
 Quando a lista SELECT da especificação de consulta associada ao cursor contém mais de uma referência à mesma coluna, se um erro é gerado ou o driver ignora as referências duplicadas e executa as operações solicitadas é definido pelo driver.  
  
## <a name="performing-bulk-operations"></a>Realização de Operações em Massa  
 Se o argumento *'RowNumber'* for 0, o driver executa a operação especificada no argumento *Operação* para cada linha no conjunto de linhas que tenha um valor de SQL_ROW_PROCEED em seu campo na matriz de operação de linha apontada pelo atributo de declaração SQL_ATTR_ROW_OPERATION_PTR. Este é um valor válido do argumento *RowNumber* para um argumento de *Operação* de SQL_DELETE, SQL_REFRESH ou SQL_UPDATE, mas não SQL_POSITION. **SQLSetPos** com uma *operação* de SQL_POSITION e um Número de *Linha* igual a 0 retornará SQLSTATE HY109 (posição de cursor inválido).  
  
 Se ocorrer um erro que diz respeito a todo o conjunto de linhas, como o SQLSTATE HYT00 (Timeout expirou), o driver retorna SQL_ERROR e o SQLSTATE apropriado. O conteúdo dos buffers de conjunto de linhas é indefinido e a posição do cursor está inalterada.  
  
 Se ocorrer um erro que diz respeito a uma única linha, o driver:  
  
-   Define o elemento para a linha na matriz de status da linha apontada pelo atributo de declaração SQL_ATTR_ROW_STATUS_PTR para SQL_ROW_ERROR.  
  
-   Posta um ou mais SQLSTATEs adicionais para o erro na fila de erros e define o campo SQL_DIAG_ROW_NUMBER na estrutura de dados de diagnóstico.  
  
 Depois de processado o erro ou aviso, se o motorista completar a operação para as linhas restantes no conjunto de linhas, ele retorna SQL_SUCCESS_WITH_INFO. Assim, para cada linha que retornou um erro, a fila de erro contém zero ou mais SQLSTATEs adicionais. Se o motorista parar a operação depois de ter processado o erro ou aviso, ele retorna SQL_ERROR.  
  
 Se o driver retornar quaisquer avisos, como SQLSTATE 01004 (Dados truncados), ele reameda avisos que se aplicam a todo o conjunto de linhas ou a linhas desconhecidas no conjunto de linhas antes de retornar as informações de erro que se aplicam a linhas específicas. Ele retorna avisos para linhas específicas, juntamente com quaisquer outras informações de erro sobre essas linhas.  
  
 Se *o RowNumber* for igual a 0 e *a Operação* for SQL_UPDATE, SQL_REFRESH ou SQL_DELETE, o número de linhas em que o **SQLSetPos** opera é apontado pelo atributo de declaração SQL_ATTR_ROWS_FETCHED_PTR.  
  
 Se *o Número* de Linha for igual a 0 e a *operação* for SQL_DELETE, SQL_REFRESH ou SQL_UPDATE, a linha atual após a operação é a mesma da linha atual antes da operação.  
  
## <a name="ignoring-a-row-in-a-bulk-operation"></a>Ignorando uma linha em uma operação em massa  
 O array de operação de linha pode ser usado para indicar que uma linha no conjunto de linhas atual deve ser ignorada durante uma operação em massa usando **SQLSetPos**. Para orientar o motorista a ignorar uma ou mais linhas durante uma operação em massa, um aplicativo deve executar as seguintes etapas:  
  
1.  Ligue para **sqlsetstmtAttr** para definir o atributo de declaração SQL_ATTR_ROW_OPERATION_PTR para apontar para uma matriz de SQLUSMALLINTs. Este campo também pode ser definido ligando para **SQLSetDescField** para definir o campo de cabeçalho SQL_DESC_ARRAY_STATUS_PTR do ARD, o que requer que um aplicativo obtenha a alça do descritor.  
  
2.  Defina cada elemento da matriz de operação de linha como um dos dois valores:  
  
    -   SQL_ROW_IGNORE, para indicar que a linha está excluída para a operação em massa.  
  
    -   SQL_ROW_PROCEED, para indicar que a linha está incluída na operação a granel. (Esse é o valor padrão.)  
  
3.  Ligue para **sqlsetpos** para executar a operação em massa.  
  
 As seguintes regras se aplicam ao array de operação de linha:  
  
-   SQL_ROW_IGNORE e SQL_ROW_PROCEED afetam apenas as operações em massa usando **SQLSetPos** com uma *operação* de SQL_DELETE ou SQL_UPDATE. Elas não afetam chamadas para **SQLSetPos** com uma *operação* de SQL_REFRESH ou SQL_POSITION.  
  
-   O ponteiro está definido como nulo por padrão.  
  
-   Se o ponteiro for nulo, todas as linhas serão atualizadas como se todos os elementos fossem definidos como SQL_ROW_PROCEED.  
  
-   Definir um elemento para SQL_ROW_PROCEED não garante que a operação ocorra nessa linha específica. Por exemplo, se uma certa linha no conjunto de linhas tiver o status SQL_ROW_ERROR, o driver pode não ser capaz de atualizar essa linha, independentemente de o aplicativo especificado SQL_ROW_PROCEED. Um aplicativo deve sempre verificar a matriz de status da linha para ver se a operação foi bem sucedida.  
  
-   SQL_ROW_PROCEED é definido como 0 no arquivo de cabeçalho. Um aplicativo pode inicializar o array de operação de linha para 0, a fim de processar todas as linhas.  
  
-   Se o número de elemento "n" na matriz de operação de linha estiver definido para SQL_ROW_IGNORE e **SQLSetPos** for chamado para executar uma operação de atualização ou exclusão em massa, a nésima linha no conjunto de linhas permanece inalterada após a chamada para **SQLSetPos**.  
  
-   Um aplicativo deve definir automaticamente uma coluna somente leitura para SQL_ROW_IGNORE.  
  
## <a name="ignoring-a-column-in-a-bulk-operation"></a>Ignorando uma coluna em uma operação em massa  
 Para evitar diagnósticos desnecessários de processamento gerados por tentativas de atualizações em uma ou mais colunas somente leitura, um aplicativo pode definir o valor no buffer de comprimento/indicador de destino para SQL_COLUMN_IGNORE. Para obter mais informações, consulte [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
## <a name="code-example"></a>Exemplo de código  
 No exemplo a seguir, um aplicativo permite que um usuário navegue pela tabela ORDERS e atualize o status do pedido. O cursor é orientado por conjuntos de tecla com um tamanho de conjunto de linhas de 20 e usa controle de concorrência otimista comparando versões de linha. Depois que cada conjunto de linhas é buscado, o aplicativo imprime-o e permite que o usuário selecione e atualize o status de um pedido. O aplicativo usa **SQLSetPos** para posicionar o cursor na linha selecionada e executa uma atualização posicionada da linha. (O manuseio de erros é omitido para clareza.)  
  
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
  
 Para obter mais exemplos, consulte [Instruções posicionadas e exclusão de declarações](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md) e [linhas de atualização no conjunto de linhas de linha com SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Vinculando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Realizando operações em massa que não se relacionam com a posição do cursor de bloco|[Função SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Cancelamento do processamento de declarações|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Buscar um bloco de dados ou rolar através de um conjunto de resultados|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Obtendo um único campo de um descritor|[Função SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Obtendo vários campos de um descritor|[Função SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Definindo um único campo de um descritor|[Função SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Definindo vários campos de um descritor|[Função SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|Definindo um atributo de declaração|[Função SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
