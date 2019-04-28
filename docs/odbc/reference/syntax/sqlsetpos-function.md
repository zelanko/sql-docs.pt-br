---
title: Função SQLSetPos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetPos
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetPos
helpviewer_keywords:
- SQLSetPos function [ODBC]
ms.assetid: 80190ee7-ae3b-45e5-92a9-693eb558f322
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e769949c8c57bbec56055c58c9002494fc6d37be
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62982392"
---
# <a name="sqlsetpos-function"></a>Função SQLSetPos
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 1.0 ODBC: ODBC  
  
 **Resumo**  
 **SQLSetPos** define a posição do cursor em um conjunto de linhas e permite que um aplicativo para atualizar dados no conjunto de linhas ou atualizar ou excluir dados no conjunto de resultados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLSetPos(  
      SQLHSTMT        StatementHandle,  
      SQLSETPOSIROW   RowNumber,  
      SQLUSMALLINT    Operation,  
      SQLUSMALLINT    LockType);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrução.  
  
 *RowNumber*  
 [Entrada] Posição da linha no conjunto de linhas nas quais executar a operação especificada com o *operação* argumento. Se *RowNumber* for 0, a operação se aplica a todas as linhas no conjunto de linhas.  
  
 Para obter mais informações, consulte "Comentários".  
  
 *Operação*  
 [Entrada] Operação a ser executada:  
  
 SQL_POSITION SQL_REFRESH SQL_UPDATE SQL_DELETE  
  
> [!NOTE]
>  O valor SQL_ADD para o *operação* argumento foi preterido para ODBC 3 *. x*. ODBC 3. *x* drivers serão necessário dar suporte a SQL_ADD para compatibilidade com versões anteriores. Essa funcionalidade foi substituída por uma chamada para **SQLBulkOperations** com um *operação* de SQL_ADD. Quando um ODBC 3. *x* aplicativo funciona com um ODBC 2. *x* driver, o Gerenciador de Driver mapeia uma chamada para **SQLBulkOperations** com um *operação* de SQL_ADD para **SQLSetPos** com um  *Operação* de SQL_ADD.  
  
 Para obter mais informações, consulte "Comentários".  
  
 *LockType*  
 [Entrada] Especifica como bloquear a linha após a operação especificada na *operação* argumento.  
  
 SQL_LOCK_NO_CHANGE SQL_LOCK_EXCLUSIVE SQL_LOCK_UNLOCK  
  
 Para obter mais informações, consulte "Comentários".  
  
 **Retorna**  
  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLSetPos** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL _ HANDLE_STMT e uma *manipular* dos *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLSetPos** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
 Para todos esses SQLSTATEs que podem retornar SQL_SUCCESS_WITH_INFO ou SQL_ERROR (exceto 01xxx SQLSTATEs), SQL_SUCCESS_WITH_INFO será retornado se ocorrer um erro em um ou mais, mas nem todas as linhas de uma operação de várias linhas, e SQL_ERROR será retornado se ocorrer um erro em um operação de uma única linha.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01001|Conflito de operação do cursor|O *operação* argumento era SQL_DELETE ou SQL_UPDATE e nenhuma linha ou mais de uma linha foi excluída ou atualizada. (Para obter mais informações sobre atualizações de mais de uma linha, consulte a descrição do SQL_ATTR_SIMULATE_CURSOR *atributo* na **SQLSetStmtAttr**.) (A função retornará SQL_SUCCESS_WITH_INFO.)<br /><br /> O *operação* argumento era SQL_DELETE ou SQL_UPDATE, e a operação falhou devido a simultaneidade otimista. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01004|Truncamento à direita de dados de cadeia de caracteres|O *operação* argumento era SQL_REFRESH e cadeia de caracteres ou dados binários retornados para uma coluna ou colunas com um tipo de dados de SQL_C_CHAR ou SQL_C_BINARY resultaram em truncamento de caractere não vazios ou nulos de dados binários.|  
|01S01|Erro na linha|O *RowNumber* argumento era 0 e ocorreu um erro em uma ou mais linhas ao executar a operação especificada com o *operação* argumento.<br /><br /> (SQL_SUCCESS_WITH_INFO será retornado se ocorrer um erro em um ou mais, mas nem todas as linhas de uma operação de várias linhas, e SQL_ERROR será retornado se ocorrer um erro em uma operação de uma única linha).<br /><br /> (Esse SQLSTATE é retornado somente quando **SQLSetPos** é chamado após **SQLExtendedFetch**, se o driver é um ODBC 2. *x* driver e a biblioteca de cursores não é usado.)|  
|01S07|Truncamento fracionário|O *operação* argumento era SQL_REFRESH, o tipo de dados do buffer de aplicativo não era SQL_C_CHAR ou SQL_C_BINARY e os dados retornados aos buffers de aplicativo para uma ou mais colunas foi truncados. Para tipos de dados numéricos, a parte fracionária do número foi truncada. Para o tempo, carimbo de hora e tipos de dados de intervalo que contém um componente de tempo, a parte fracionária do tempo foi truncada.<br /><br /> (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|07006|Violação do atributo de tipo de dados restrito|O valor de dados de uma coluna no conjunto de resultados não pôde ser convertido para o tipo de dados especificado por *TargetType* na chamada para **SQLBindCol**.|  
|07009|Índice de descritor inválido|O argumento *operação* era SQL_REFRESH ou SQL_UPDATE e uma coluna foi associada com um número de coluna maior que o número de colunas no conjunto de resultados.|  
|21S02|Grau da tabela derivada não corresponde à lista de colunas|O argumento *operação* era SQL_UPDATE, e não há colunas eram atualizáveis porque todas as colunas foram talvez não associado, somente leitura, ou o valor no buffer de comprimento/indicador associado foi SQL_COLUMN_IGNORE.|  
|22001|Dados de cadeia de caracteres, truncamento à direita|O *operação* argumento era SQL_UPDATE e a atribuição de um caractere ou valor binário para uma coluna resultou em truncamento de não vazio (para caracteres) ou caracteres nulos (para binário) ou bytes.|  
|22003|Valor numérico fora do intervalo|O argumento *operação* era SQL_UPDATE e a atribuição de um valor numérico para uma coluna no conjunto de resultados causou a parte inteira (em vez de fracionários) o número a ser truncado.<br /><br /> O argumento *operação* era SQL_REFRESH e retornar o valor numérico de uma ou mais colunas associadas causaria uma perda de dígitos significativos.|  
|22007|Formato de data/hora inválido|O argumento *operação* estava SQL_UPDATE e a atribuição de um valor de data ou carimbo de hora a uma coluna no conjunto de resultados causou o ano, mês, dia campo ou para estar fora do intervalo.<br /><br /> O argumento *operação* era SQL_REFRESH e retornando o valor de data ou carimbo de data para um ou mais colunas associadas teria causado o ano, mês, dia campo ou para estar fora do intervalo.|  
|22008|Estouro no campo de data/hora|O *operação* argumento era SQL_UPDATE, e o desempenho das operações aritméticas com dados que estão sendo enviados a uma coluna no conjunto de resultados de datetime resultou em um campo de data e hora (o ano, mês, dia, hora, minuto ou segundo campo) do resultado que está sendo fora do intervalo permitido de valores para o campo ou sendo inválido com base nas regras de natural do calendário gregoriano para datetimes.<br /><br /> O *operação* argumento era SQL_REFRESH, e o desempenho das operações aritméticas com dados que estão sendo recuperados do conjunto de resultados de datetime resultou em um campo de data e hora (o ano, mês, dia, hora, minuto ou segundo campo) do resultado que está sendo fora do intervalo permitido de valores para o campo ou sendo inválido com base nas regras de natural do calendário gregoriano para datetimes.|  
|22015|Estouro no campo de intervalo|O *operação* argumento era SQL_UPDATE e a atribuição de um valor numérico exato ou o tipo de intervalo de C para um intervalo de tipo de dados SQL causou uma perda de dígitos significativos.<br /><br /> O *operação* argumento era SQL_UPDATE; ao atribuir a um intervalo de tipo SQL, não havia nenhuma representação do valor do tipo C no intervalo de tipo SQL.<br /><br /> O *operação* argumento era SQL_REFRESH e atribuição de um numérico exato ou o intervalo de tipo SQL para um tipo de intervalo C causou uma perda de dígitos significativos no campo à esquerda.<br /><br /> O *operação* argumento era SQL _ atualizar; ao atribuir a um tipo de intervalo de C, não havia nenhuma representação do valor do tipo SQL no tipo de intervalo de C.|  
|22018|Valor de caractere inválido para especificação de conversão|O *operação* argumento era SQL_REFRESH; o tipo C era um valor numérico exato ou aproximado, uma data e hora ou um tipo de dados de intervalo; o tipo SQL da coluna era um tipo de dados de caractere; e o valor na coluna não era um literal válido das tipo de C associado.<br /><br /> O argumento *operação* foi SQL_UPDATE; o tipo SQL era um valor numérico exato ou aproximado, uma data e hora ou um tipo de dados de intervalo; o tipo C foi SQL_C_CHAR; e o valor na coluna não era um literal válido do tipo SQL associado.|  
|23000|Violação de restrição de integridade|O argumento *operação* era SQL_DELETE ou SQL_UPDATE e uma restrição de integridade foi violada.|  
|24000|Estado de cursor inválido|O *StatementHandle* estava em um estado de executado, mas nenhum conjunto de resultados foi associado a *StatementHandle*.<br /><br /> (DM) um cursor foi aberto sobre o *StatementHandle*, mas **SQLFetch** ou **SQLFetchScroll** não tivesse sido chamada.<br /><br /> Um cursor foi aberto na *StatementHandle*, e **SQLFetch** ou **SQLFetchScroll** tivesse sido chamada, mas o cursor é posicionado antes do início do conjunto de resultados ou após o fim do conjunto de resultados.<br /><br /> O argumento *operação* era SQL_DELETE, SQL_REFRESH ou SQL_UPDATE e o cursor é posicionado antes do início do conjunto de resultados ou após o final do conjunto de resultados.|  
|40001|Falha na serialização|A transação foi revertida devido a um deadlock de recursos com outra transação.|  
|40003|Conclusão desconhecida de declaração|A conexão associada falhou durante a execução dessa função e o estado da transação não pode ser determinado.|  
|42000|Sintaxe ou violação de acesso|O driver não foi possível bloquear a linha conforme necessário para executar a operação solicitada no argumento *operação*.<br /><br /> O driver não foi possível bloquear a linha conforme solicitado no argumento *LockType*.|  
|44000|Violação COM OPÇÃO DE VERIFICAÇÃO|O *operação* argumento era SQL_UPDATE e a atualização foi executada em uma tabela visualizada ou uma tabela derivada da tabela exibida que foi criada com a especificação **WITH CHECK OPTION**, de modo que uma ou mais linhas afetado pela atualização não estará presente na tabela exibida.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** na  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*, e, em seguida, a função foi chamada novamente na *StatementHandle*.<br /><br /> A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativos multithread.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando a função SQLSetPos foi chamada.<br /><br /> (DM) especificado *StatementHandle* não estava em um estado executado. A função foi chamada sem primeiro chamar **SQLExecDirect**, **SQLExecute**, ou uma função de catálogo.<br /><br /> (DM) uma função de execução assíncrona (não desse último) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retornados de SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todos os parâmetros de dados em execução ou colunas.<br /><br /> (DM) o driver foi um ODBC 2. *x* driver, e **SQLSetPos** foi chamado para um *StatementHandle* depois **SQLFetch** foi chamado.|  
|HY011|Atributo não pode ser definido agora|(DM) o driver foi um ODBC 2. *x* driver; o SQL_ATTR_ROW_STATUS_PTR atributo de instrução foi definido; em seguida, **SQLSetPos** foi chamado antes **SQLFetch**, **SQLFetchScroll**, ou **SQLExtendedFetch** foi chamado.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|O *operação* argumento era SQL_UPDATE, um valor de dados é um ponteiro nulo e o valor de comprimento de coluna não era 0, SQL_DATA_AT_EXEC, SQL_COLUMN_IGNORE, SQL_NULL_DATA, ou menor ou igual a SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> O *operação* argumento era SQL_UPDATE; um valor de dados não é um ponteiro nulo; o tipo de dados C foi SQL_C_BINARY ou SQL_C_CHAR; e o valor de comprimento de coluna era menor que 0 mas não iguais a SQL_DATA_AT_EXEC, SQL_COLUMN_IGNORE , SQL_NTS ou SQL_NULL_DATA, ou menor ou igual a SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> O valor em um buffer de comprimento/indicador foi SQL_DATA_AT_EXEC; o tipo de SQL era SQL_LONGVARCHAR, SQL_LONGVARBINARY ou um tipo de dados específicos da fonte de dados long; e o tipo de informação no SQL_NEED_LONG_DATA_LEN **SQLGetInfo** foi "Y".|  
|HY092|Identificador de atributo inválido|(DM) o valor especificado para o *operação* argumento era inválido.<br /><br /> (DM) o valor especificado para o *LockType* argumento era inválido.<br /><br /> O *operação* argumento era SQL_UPDATE ou SQL_DELETE e o atributo de instrução SQL_ATTR_CONCURRENCY foi SQL_ATTR_CONCUR_READ_ONLY.|  
|HY107|Valor de linha fora do intervalo|O valor especificado para o argumento *RowNumber* era maior que o número de linhas no conjunto de linhas.|  
|HY109|Posição do cursor inválida|O cursor associado a *StatementHandle* foi definida como somente de avanço, portanto, o cursor não pode ser posicionado dentro do conjunto de linhas. Consulte a descrição para o atributo SQL_ATTR_CURSOR_TYPE na **SQLSetStmtAttr**.<br /><br /> O *operação* argumento era SQL_UPDATE, SQL_DELETE ou SQL_REFRESH e a linha identificada pela *RowNumber* argumento tivesse sido excluído ou não tinha sido buscado.<br /><br /> (DM) a *RowNumber* argumento era 0 e o *operação* argumento era SQL_POSITION.<br /><br /> **SQLSetPos** foi chamado após **SQLBulkOperations** foi chamado e antes **SQLFetchScroll** ou **SQLFetch** foi chamado.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|A driver ou fonte de dados não oferece suporte para a operação solicitada na *operação* argumento ou o *LockType* argumento.|  
|HYT00|Tempo limite esgotado|O período de tempo limite da consulta expirou antes da fonte de dados retornou o conjunto de resultados. O período de tempo limite é definido por meio **SQLSetStmtAttr** com um *atributo* de SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|O driver em (DM) associado a *StatementHandle* não suporta a função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem é desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior no identificador retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado no identificador de fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
  
> [!CAUTION]
>  Para obter informações sobre a instrução declara que **SQLSetPos** pode ser chamada e o que precisa fazer para compatibilidade com o ODBC 2 *. x* aplicativos, consulte [cursores em bloco, cursores roláveis, e Compatibilidade com versões anteriores](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md).  
  
## <a name="rownumber-argument"></a>Argumento RowNumber  
 O *RowNumber* argumento especifica o número da linha no conjunto de linhas nas quais executar a operação especificada pelo *operação* argumento. Se *RowNumber* for 0, a operação se aplica a todas as linhas no conjunto de linhas. *RowNumber* deve ser um valor de 0 ao número de linhas no conjunto de linhas.  
  
> [!NOTE]  
>  Na linguagem C, matrizes são baseadas em 0 e o *RowNumber* argumento é baseado em 1. Por exemplo, para atualizar a quinta linha do conjunto de linhas, um aplicativo modifica os buffers de conjunto de linhas no índice de matriz 4, mas Especifica um *RowNumber* de 5.  
  
 Todas as operações de posicionar o cursor na linha especificada por *RowNumber*. As operações a seguir exigem uma posição do cursor:  
  
-   Posicionado atualizar e excluir instruções.  
  
-   Chamadas para **SQLGetData**.  
  
-   Chamadas para **SQLSetPos** com as opções SQL_DELETE, SQL_REFRESH e SQL_UPDATE.  
  
 Por exemplo, se *RowNumber* é 2 para uma chamada para **SQLSetPos** com um *operação* de SQL_DELETE, o cursor é posicionado na segunda linha do conjunto de linhas e que a linha é excluída. A entrada da implementação linha status matriz (apontada para o atributo da instrução SQL_ATTR_ROW_STATUS_PTR) para a segunda linha é alterada para SQL_ROW_DELETED.  
  
 Um aplicativo pode especificar uma posição do cursor quando ele chama **SQLSetPos**. Em geral, ele chama **SQLSetPos** com a operação SQL_POSITION ou SQL_REFRESH para posicionar o cursor antes de executar um posicionadas de atualização ou exclusão da instrução ou chamar **SQLGetData**.  
  
## <a name="operation-argument"></a>Argumento de operação  
 O *operação* argumento suporta as seguintes operações. Para determinar quais opções têm suporte por uma fonte de dados, um aplicativo chama **SQLGetInfo** com o SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 ou SQL_STATIC_ Tipo de informação CURSOR_ATTRIBUTES1 (dependendo do tipo de cursor).  
  
|*Operação*<br /><br /> argumento|Operação|  
|------------------------------|---------------|  
|SQL_POSITION|O driver posiciona o cursor na linha especificada por *RowNumber*.<br /><br /> O conteúdo da matriz de status de linha apontado pelo atributo de instrução SQL_ATTR_ROW_OPERATION_PTR é ignorado para a SQL_POSITION *operação*.|  
|SQL_REFRESH|O driver posiciona o cursor na linha especificada por *RowNumber* e atualiza os dados nos buffers de conjunto de linhas para aquela linha. Para obter mais informações sobre como o driver retorna dados nos buffers de conjunto de linhas, consulte as descrições de linha e coluna de associação no **SQLBindCol**.<br /><br /> **SQLSetPos** com um *operação* de SQL_REFRESH atualiza o status e o conteúdo das linhas dentro do conjunto de linhas busca atual. Isso inclui a atualizar os indicadores. Como os dados nos buffers são atualizados, mas não refetched, a associação no conjunto de linhas é fixa. Isso é diferente da atualização executada por uma chamada para **SQLFetchScroll** com um *FetchOrientation* de SQL_FETCH_RELATIVE e uma *RowNumber* igual a 0, o que refetches o conjunto de linhas do resultado definido para que ele possa mostrar dados adicionados e remover dados excluídos se essas operações são compatíveis com o driver e o cursor.<br /><br /> Uma atualização bem-sucedida com o **SQLSetPos** não alterará o status de uma linha de SQL_ROW_DELETED. Linhas excluídas no conjunto de linhas continuarão a ser marcado como excluído até que a próxima busca. As linhas estará disponível na próxima busca, se o cursor dá suporte a remessa (no qual um subsequentes **SQLFetch** ou **SQLFetchScroll** não retorna linhas excluídas).<br /><br /> Adicionada a linhas não aparecem quando uma atualização com o **SQLSetPos** é executada. Esse comportamento é diferente do **SQLFetchScroll** com um *FetchType* de SQL_FETCH_RELATIVE e uma *RowNumber* igual a 0, que também atualiza o conjunto de linhas atual, mas serão Mostrar registros adicionados ou os registros excluídos do pacote se essas operações são suportadas pelo cursor.<br /><br /> Uma atualização bem-sucedida com o **SQLSetPos** será alterado um status de linha de SQL_ROW_ADDED SQL_ROW_SUCCESS (se existir a matriz de status de linha).<br /><br /> Uma atualização bem-sucedida com o **SQLSetPos** será alterado um status de linha de SQL_ROW_UPDATED novo de status da linha (se existir a matriz de status de linha).<br /><br /> Se ocorrer um erro em uma **SQLSetPos** operação em uma linha, o status de linha é definido como SQL_ROW_ERROR (se existir a matriz de status de linha).<br /><br /> Para um cursor aberto com um atributo de instrução SQL_ATTR_CONCURRENCY de SQL_CONCUR_ROWVER ou SQL_CONCUR_VALUES, uma atualização com o **SQLSetPos** podem atualizar os valores de simultaneidade otimista usados pela fonte de dados para detectar que o linha foi alterada. Se isso ocorrer, os valores usados para garantir que a simultaneidade do cursor ou versões de linha são atualizados sempre que os buffers de conjunto de linhas são atualizados a partir do servidor. Isso ocorre para cada linha que é atualizada.<br /><br /> O conteúdo da matriz de status de linha apontado pelo atributo de instrução SQL_ATTR_ROW_OPERATION_PTR é ignorado para a SQL_REFRESH *operação*.|  
|SQL_UPDATE|O driver posiciona o cursor na linha especificada por *RowNumber* e atualiza a linha de base de dados com os valores nos buffers de conjunto de linhas (a *TargetValuePtr* argumento em  **SQLBindCol**). Ele recupera os comprimentos dos dados dos buffers de comprimento/indicador (o *StrLen_or_IndPtr* argumento **SQLBindCol**). Se o comprimento de qualquer coluna for SQL_COLUMN_IGNORE, a coluna não é atualizada. Depois de atualizar a linha, o driver altera o elemento correspondente da matriz de status de linha para SQL_ROW_UPDATED ou SQL_ROW_SUCCESS_WITH_INFO (se existir a matriz de status de linha).<br /><br /> Ele é definido pelo driver o que é o comportamento se **SQLSetPos** com um *operação* argumento de SQL_UPDATE é chamado em um cursor que contém colunas duplicadas. O driver pode retornar um SQLSTATE definido pelo driver, pode atualizar a primeira coluna que aparece no conjunto de resultados ou realizar outro comportamento definido pelo driver.<br /><br /> A matriz de operação de linha apontada pelo atributo SQL_ATTR_ROW_OPERATION_PTR instrução pode ser usada para indicar que uma linha no conjunto de linhas atual deve ser ignorada durante uma atualização em massa. Para obter mais informações, consulte a seção "Matrizes de Status e de operação", mais adiante essa referência de função.|  
|SQL_DELETE|O driver posiciona o cursor na linha especificada por *RowNumber* e exclui a linha de base de dados. Ele altera o elemento correspondente da matriz de status de linha para SQL_ROW_DELETED. Depois que a linha foi excluída, a seguir não é válida para a linha: posicionado atualizar e excluir instruções, chamadas para **SQLGetData**e chamadas para **SQLSetPos** com *operação* definido como qualquer coisa, exceto SQL_POSITION. Para os drivers que dão suporte ao empacotamento, a linha é excluída do cursor quando novos dados são recuperados da fonte de dados.<br /><br /> Se a linha permanece visível depende do tipo cursor. Por exemplo, linhas excluídas são visíveis para Cursores estáticos e controlados por mas invisível para cursores dinâmicos.<br /><br /> A matriz de operação de linha apontada pelo atributo SQL_ATTR_ROW_OPERATION_PTR instrução pode ser usada para indicar que uma linha no conjunto de linhas atual deve ser ignorada durante uma exclusão em massa. Para obter mais informações, consulte a seção "Matrizes de Status e de operação", mais adiante essa referência de função.|  
  
## <a name="locktype-argument"></a>Argumento LockType  
 O *LockType* argumento fornece uma maneira para os aplicativos controlar a simultaneidade. Na maioria dos casos, as fontes de dados que dão suporte a transações e os níveis de simultaneidade dará suporte somente o valor SQL_LOCK_NO_CHANGE do *LockType* argumento. O *LockType* argumento geralmente é usado somente para o suporte baseado em arquivo.  
  
 O *LockType* argumento especifica o estado de bloqueio da linha após **SQLSetPos** foi executado. Se o driver não foi possível bloquear a linha para executar a operação solicitada ou para satisfazer a *LockType* argumento, ele retornará SQL_ERROR e SQLSTATE 42000 (sintaxe ou violação de acesso).  
  
 Embora o *LockType* argumento é especificado para uma única instrução, o bloqueio accords os mesmos privilégios para todas as instruções sobre a conexão. Em particular, um bloqueio adquirido por uma instrução em uma conexão pode ser desbloqueado por uma instrução diferente sobre a mesma conexão.  
  
 Uma linha bloqueada por meio **SQLSetPos** permanecerá bloqueado até que o aplicativo chame **SQLSetPos** para a linha com *LockType* definido como SQL_LOCK_UNLOCK, ou até que o aplicativo chamadas **SQLFreeHandle** para a instrução ou **SQLFreeStmt** com a opção SQL_CLOSE. Um driver que oferece suporte a transações, uma linha bloqueada por meio **SQLSetPos** é desbloqueada quando o aplicativo chama **SQLEndTran** para confirmar ou reverter uma transação em que a conexão (se um cursor é fechado Quando uma transação é confirmada ou revertida, conforme indicado pelos tipos de informações SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR retornados por **SQLGetInfo**).  
  
 O *LockType* argumento suporta os seguintes tipos de bloqueios. Para determinar quais bloqueios são compatíveis com uma fonte de dados, um aplicativo chama **SQLGetInfo** com o SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 ou SQL_STATIC_ Tipo de informação CURSOR_ATTRIBUTES1 (dependendo do tipo de cursor).  
  
|*LockType* argumento|Tipo de bloqueio|  
|-------------------------|---------------|  
|SQL_LOCK_NO_CHANGE|A driver ou fonte de dados garante que a linha é o mesmo estado bloqueado ou desbloqueado como era antes **SQLSetPos** foi chamado. Esse valor de *LockType* permite que fontes de dados que não dão suporte a bloqueio em nível de linha explícita para usar qualquer bloqueio é exigido pelos níveis de isolamento simultaneidade e a transação atuais.|  
|SQL_LOCK_EXCLUSIVE|A driver ou fonte de dados bloqueia a linha exclusivamente. Uma instrução em uma conexão diferente ou em um aplicativo diferente não pode ser usada para adquirir todos os bloqueios na linha.|  
|SQL_LOCK_UNLOCK|A fonte de dados ou driver desbloqueia a linha.|  
  
 Se um driver dá suporte a SQL_LOCK_EXCLUSIVE, mas não oferece suporte a SQL_LOCK_UNLOCK, uma linha que está bloqueada permanecerá bloqueada até que ocorra um as chamadas de função descritas no parágrafo anterior.  
  
 Se um driver dá suporte a SQL_LOCK_EXCLUSIVE, mas não oferece suporte a SQL_LOCK_UNLOCK, uma linha que está bloqueada permanecerá bloqueada até que o aplicativo chame **SQLFreeHandle** para a instrução ou **SQLFreeStmt** com a opção SQL_CLOSE. Se o driver oferece suporte a transações e fecha o cursor ao confirmar ou reverter a transação, o aplicativo chama **SQLEndTran**.  
  
 Para as operações update e delete no **SQLSetPos**, o aplicativo usa o *LockType* argumento da seguinte maneira:  
  
-   Para garantir que uma linha não seja alterado depois de recuperados, um aplicativo chama **SQLSetPos** com *operação* definido como SQL_REFRESH e *LockType* definido como SQL_LOCK_ EXCLUSIVO.  
  
-   Se o aplicativo define *LockType* para SQL_LOCK_NO_CHANGE, o driver garante que uma operação de atualização ou exclusão terá êxito apenas se o aplicativo especificado SQL_CONCUR_LOCK para o atributo de instrução SQL_ATTR_CONCURRENCY.  
  
-   Se o aplicativo especifica SQL_CONCUR_ROWVER ou SQL_CONCUR_VALUES para o atributo de instrução SQL_ATTR_CONCURRENCY, o driver compara as versões de linha ou valores e rejeitará a operação se a linha foi alterada desde que o aplicativo buscado a linha.  
  
-   Se o aplicativo especificar SQL_CONCUR_READ_ONLY para o atributo de instrução SQL_ATTR_CONCURRENCY, o driver rejeita qualquer atualização ou operação de exclusão.  
  
 Para obter mais informações sobre o atributo de instrução SQL_ATTR_CONCURRENCY, consulte [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
## <a name="status-and-operation-arrays"></a>Status e as matrizes de operação  
 As seguintes matrizes de status e a operação são usadas ao chamar **SQLSetPos**:  
  
-   A matriz de status de linha (conforme apontado pelo campo SQL_DESC_ARRAY_STATUS_PTR do IRD e o atributo da instrução SQL_ATTR_ROW_STATUS_ARRAY) contém os valores de status para cada linha de dados no conjunto de linhas. O driver define os valores de status nessa matriz após uma chamada para **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**, ou **SQLSetPos** . Essa matriz é apontada pelo atributo de instrução SQL_ATTR_ROW_STATUS_PTR.  
  
-   A matriz de operação de linha (conforme apontado pelo campo SQL_DESC_ARRAY_STATUS_PTR a descartar e o atributo da instrução SQL_ATTR_ROW_OPERATION_ARRAY) contém um valor para cada linha no conjunto de linhas que indica se uma chamada para **SQLSetPos**para uma operação em massa é ignorada ou executada. Cada elemento da matriz é definido como SQL_ROW_PROCEED (o padrão) ou SQL_ROW_IGNORE. Essa matriz é apontada pelo atributo de instrução SQL_ATTR_ROW_OPERATION_PTR.  
  
 O número de elementos nas matrizes de status e a operação deve ser igual ao número de linhas no conjunto de linhas (conforme definido pelo atributo SQL_ATTR_ROW_ARRAY_SIZE instrução).  
  
 Para obter informações sobre a matriz de status de linha, consulte [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md). Para obter informações sobre a matriz de operação de linha, consulte "Ignorando uma linha em uma operação em massa," nesta seção.  
  
## <a name="using-sqlsetpos"></a>Usando SQLSetPos  
 Antes de um aplicativo chama **SQLSetPos**, ele deve executar a seguinte sequência de etapas:  
  
1.  Se o aplicativo chamará **SQLSetPos** com *operação* definido como SQL_UPDATE, chamada **SQLBindCol** (ou **SQLSetDescRec**) para cada coluna para especificar seu tipo de dados e associar os buffers de dados e o comprimento da coluna.  
  
2.  Se o aplicativo chamará **SQLSetPos** com *operação* definido como SQL_DELETE ou SQL_UPDATE, chamada **SQLColAttribute** para certificar-se de que as colunas a ser excluída ou atualizada são atualizáveis.  
  
3.  Chame **SQLExecDirect**, **SQLExecute**, ou uma função de catálogo para criar um conjunto de resultados.  
  
4.  Chame **SQLFetch** ou **SQLFetchScroll** para recuperar os dados.  
  
 Para obter mais informações sobre como usar **SQLSetPos**, consulte [atualizando dados com SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md).  
  
## <a name="deleting-data-using-sqlsetpos"></a>Excluindo dados usando SQLSetPos  
 Para excluir dados com **SQLSetPos**, um aplicativo chama **SQLSetPos** com *RowNumber* definido como o número da linha para excluir e *operação*definido como SQL_DELETE.  
  
 Depois que os dados foram excluídos, o driver altera o valor na matriz de status de linha de implementação para a linha apropriada SQL_ROW_DELETED (ou SQL_ROW_ERROR).  
  
## <a name="updating-data-using-sqlsetpos"></a>Atualizando dados com SQLSetPos  
 Um aplicativo pode passar o valor para uma coluna no buffer de dados associada ou com um ou mais chamadas para **SQLPutData**. Colunas cujos dados são passados com **SQLPutData** são conhecidos como *dados em execução* *colunas*. Elas são comumente usadas para enviar dados para colunas SQL_LONGVARBINARY e SQL_LONGVARCHAR e podem ser combinadas com outras colunas.  
  
#### <a name="to-update-data-with-sqlsetpos-an-application"></a>Para atualizar dados com SQLSetPos, um aplicativo:  
  
1.  Coloca os valores nos buffers de dados e comprimento/indicador associado com **SQLBindCol**:  
  
    -   Para colunas normais, o aplicativo coloca o novo valor de coluna na  *\*TargetValuePtr* buffer e o comprimento desse valor no  *\*StrLen_or_IndPtr* buffer. Se a linha não deve ser atualizada, o aplicativo coloca SQL_ROW_IGNORE no elemento dessa linha da matriz de operação de linha.  
  
    -   Para colunas de dados em execução, o aplicativo coloca um valor definido pelo aplicativo, como o número da coluna, na  *\*TargetValuePtr* buffer. O valor pode ser usado posteriormente para identificar a coluna.  
  
         O aplicativo coloca o resultado do SQL_LEN_DATA_AT_EXEC (*comprimento*) macro no **StrLen_or_IndPtr* buffer. Se o tipo de dados SQL da coluna for SQL_LONGVARBINARY, SQL_LONGVARCHAR ou um tipo de dados específicos da fonte de dados longos e o driver retorna "Y" para o tipo de informação SQL_NEED_LONG_DATA_LEN em **SQLGetInfo**, *comprimento*  é o número de bytes de dados a serem enviados para o parâmetro; caso contrário, ele deve ser um valor não negativo e será ignorado.  
  
2.  Chamadas **SQLSetPos** com o *operação* argumento definido como SQL_UPDATE para atualizar a linha de dados.  
  
    -   Se não houver nenhuma coluna de dados em execução, o processo for concluído.  
  
    -   Se houver qualquer coluna de dados em execução, a função retornará SQL_NEED_DATA e prossegue para a etapa 3.  
  
3.  Chamadas **SQLParamData** para recuperar o endereço da  *\*TargetValuePtr* buffer para a primeira coluna de dados em execução a ser processado. **SQLParamData** retornará SQL_NEED_DATA. O aplicativo recupera o valor definido pelo aplicativo do  *\*TargetValuePtr* buffer.  
  
    > [!NOTE]  
    >  Embora os parâmetros de dados em execução são semelhantes às colunas de dados em execução, o valor retornado por **SQLParamData** é diferente para cada um.  
  
    > [!NOTE]  
    >  Parâmetros de dados em execução são parâmetros em uma instrução SQL para o qual os dados serão enviados com **SQLPutData** quando a instrução é executada com **SQLExecDirect** ou **SQLExecute**. Eles são associados com **SQLBindParameter** ou definindo descritores com **SQLSetDescRec**. O valor retornado por **SQLParamData** é um valor de 32 bits passado para **SQLBindParameter** no *ParameterValuePtr* argumento.  
  
    > [!NOTE]  
    >  Colunas de dados em execução são colunas em um conjunto de linhas para o qual os dados serão enviados com **SQLPutData** quando uma linha é atualizada com **SQLSetPos**. Eles são associados com **SQLBindCol**. O valor retornado por **SQLParamData** é o endereço da linha no **TargetValuePtr* buffer que está sendo processada.  
  
4.  Chamadas **SQLPutData** uma ou mais vezes para enviar dados para a coluna. Mais de uma chamada é necessária se todos os valores de dados não podem ser retornados na  *\*TargetValuePtr* buffer especificado na **SQLPutData**; diversas chamadas para **SQLPutData** para a mesma coluna são permitidas somente quando o envio de dados de caractere C para uma coluna com um tipo específico de fonte de dados character, binary ou dados ou ao enviar dados binários de C para uma coluna com um caractere, binária, ou tipo de dados específico de fonte de dados.  
  
5.  Chamadas **SQLParamData** novamente para sinalizar que todos os dados foram enviados para a coluna.  
  
    -   Se houver mais colunas de dados em execução, **SQLParamData** retorna SQL_NEED_DATA e o endereço do *TargetValuePtr* buffer para a próxima coluna de dados em execução a ser processado. O aplicativo se repete as etapas 4 e 5.  
  
    -   Se não houver nada mais colunas de dados em execução, o processo for concluído. Se a instrução foi executada com êxito, **SQLParamData** retorna SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO; se a execução falhar, ele retornará SQL_ERROR. Neste ponto, **SQLParamData** pode retornar qualquer SQLSTATE que pode ser retornado por **SQLSetPos**.  
  
 Se dados foram atualizados, o driver altera o valor na matriz de status de linha de implementação para a linha apropriada para SQL_ROW_UPDATED.  
  
 Se a operação for cancelada ou ocorre um erro no **SQLParamData** ou **SQLPutData**após **SQLSetPos** retornará SQL_NEED_DATA e antes de dados são enviados para todos colunas de dados em execução, o aplicativo pode chamar apenas **SQLCancel**, **SQLGetDiagField**, **SQLGetDiagRec**, **SQLGetFunctions** , **SQLParamData**, ou **SQLPutData** para a instrução ou a conexão associada com a instrução. Se ele chamar qualquer outra função para a instrução ou a conexão associada com a instrução, a função retornará SQL_ERROR e SQLSTATE HY010 (erro de sequência de função).  
  
 Se o aplicativo chamar **SQLCancel** enquanto o driver ainda precisa de dados para colunas de dados em execução, o driver cancela a operação. O aplicativo pode, em seguida, chamar **SQLSetPos** novamente; o cancelamento não afeta o estado de cursor ou a posição atual do cursor.  
  
 Quando a lista de seleção da especificação de consulta associada com o cursor contém mais de uma referência para a mesma coluna, se um erro é gerado ou o driver ignora as referências duplicadas e executa as operações solicitadas é definido pelo driver.  
  
## <a name="performing-bulk-operations"></a>Executando operações em massa  
 Se o *RowNumber* argumento for 0, o driver executa a operação especificada na *operação* argumento para cada linha no conjunto de linhas que tem um valor de SQL_ROW_PROCEED em seu campo na operação de linha matriz apontado pelo atributo de instrução SQL_ATTR_ROW_OPERATION_PTR. Este é um valor válido do *RowNumber* argumento para uma *operação* argumento de SQL_DELETE, SQL_REFRESH, ou SQL_UPDATE, mas não SQL_POSITION. **SQLSetPos** com um *operação* de SQL_POSITION e uma *RowNumber* igual a 0 retornará SQLSTATE HY109 (posição do cursor inválida).  
  
 Se ocorrer um erro que diz respeito ao conjunto de linhas inteiro, como o SQLSTATE HYT00 (tempo limite expirado), o driver retornará SQL_ERROR e o SQLSTATE apropriado. O conteúdo dos buffers de linhas é indefinido e a posição do cursor é alterada.  
  
 Se ocorrer um erro que pertence a uma única linha, o driver:  
  
-   Define o elemento para a linha na matriz de status de linha apontado pelo atributo de instrução SQL_ATTR_ROW_STATUS_PTR para SQL_ROW_ERROR.  
  
-   Posta um ou mais SQLSTATEs adicionais para o erro na fila de erros e define o campo SQL_DIAG_ROW_NUMBER na estrutura de dados de diagnóstico.  
  
 Depois de processar o erro ou aviso, se o driver conclui a operação para as linhas restantes no conjunto de linhas, ele retornará SQL_SUCCESS_WITH_INFO. Portanto, para cada linha que retornou um erro, a fila de erros contém zero ou mais SQLSTATEs adicionais. Se o driver para a operação depois de processar o erro ou aviso, ele retornará SQL_ERROR.  
  
 Se o driver retorna todos os avisos, como o SQLSTATE 01004 (dados truncados), ele retornará avisos que se aplicam a todo o conjunto de linhas ou desconhecidas linhas no conjunto de linhas antes de retornar as informações de erro que se aplica a linhas específicas. Retorna avisos para linhas específicas, juntamente com quaisquer outras informações de erro sobre essas linhas.  
  
 Se *RowNumber* é igual a 0 e *operação* é SQL_UPDATE, SQL_REFRESH ou SQL_DELETE, o número de linhas que **SQLSetPos** opera na é apontada pelo que Atributo de instrução _FETCHED_PTR.  
  
 Se *RowNumber* é igual a 0 e *operação* é SQL_DELETE, SQL_REFRESH ou SQL_UPDATE, a linha atual depois que a operação é o mesmo que a linha atual antes da operação.  
  
## <a name="ignoring-a-row-in-a-bulk-operation"></a>Ignorando uma linha em uma operação em massa  
 A matriz de operação de linha pode ser usada para indicar que uma linha no conjunto de linhas atual deve ser ignorada durante uma operação em massa usando **SQLSetPos**. Para direcionar o driver para ignorar uma ou mais linhas durante uma operação em massa, um aplicativo deve realizar as seguintes etapas:  
  
1.  Chame **SQLSetStmtAttr** para definir o atributo de instrução SQL_ATTR_ROW_OPERATION_PTR para apontar para uma matriz de SQLUSMALLINTs. Este campo também pode ser definido chamando **SQLSetDescField** para definir o campo de cabeçalho SQL_DESC_ARRAY_STATUS_PTR de descartar, que exige que um aplicativo obtém o identificador do descritor.  
  
2.  Defina cada elemento da matriz de operação de linha para um dos dois valores:  
  
    -   SQL_ROW_IGNORE, para indicar que a linha foi excluída para a operação em massa.  
  
    -   SQL_ROW_PROCEED, para indicar que a linha é incluída na operação em massa. (Esse é o valor padrão.)  
  
3.  Chame **SQLSetPos** para executar a operação em massa.  
  
 As seguintes regras se aplicam à matriz de operação de linha:  
  
-   SQL_ROW_IGNORE e SQL_ROW_PROCEED afetam apenas as operações em massa usando **SQLSetPos** com um *operação* de SQL_DELETE ou SQL_UPDATE. Elas não afetam a chamadas para **SQLSetPos** com um *operação* de SQL_REFRESH ou SQL_POSITION.  
  
-   O ponteiro é definido como null por padrão.  
  
-   Se o ponteiro for nulo, todas as linhas são atualizadas como se todos os elementos foram definidos como SQL_ROW_PROCEED.  
  
-   A definição de um elemento para SQL_ROW_PROCEED não garante que a operação ocorrerá nessa linha específica. Por exemplo, se uma certa linha no conjunto de linhas tiver o status SQL_ROW_ERROR, o driver não poderá atualizar essa linha, independentemente se o aplicativo especificado SQL_ROW_PROCEED. Um aplicativo sempre deve verificar a matriz de status de linha para ver se a operação foi bem-sucedida.  
  
-   SQL_ROW_PROCEED é definido como 0 no arquivo de cabeçalho. Um aplicativo pode inicializar a matriz de operação de linha como 0 para processar todas as linhas.  
  
-   Se o número do elemento "n" na matriz de operação de linha é definido como SQL_ROW_IGNORE e **SQLSetPos** é chamado para realizar uma atualização em massa ou operação de exclusão, a enésima linha no conjunto de linhas permanece inalterado após a chamada para **SQLSetPos**.  
  
-   Um aplicativo automaticamente deve definir uma coluna somente leitura para SQL_ROW_IGNORE.  
  
## <a name="ignoring-a-column-in-a-bulk-operation"></a>Ignorando a uma coluna em uma operação em massa  
 Para evitar o diagnóstico de processamento desnecessária gerado pelas tentativas atualizações para uma ou mais colunas somente leitura, um aplicativo pode definir o valor no buffer de comprimento/indicador associado para SQL_COLUMN_IGNORE. Para obter mais informações, consulte [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
## <a name="code-example"></a>Exemplo de código  
 No exemplo a seguir, um aplicativo permite que um usuário procurar a tabela de pedidos e atualizar o status do pedido. O cursor é controlado por conjunto de chaves com um tamanho de conjunto de linhas de 20 e usa o controle de simultaneidade otimista comparando versões de linha. Depois de cada conjunto de linhas é buscado, o aplicativo imprime e permite que o usuário selecione e atualizar o status de um pedido. O aplicativo usa **SQLSetPos** para posicionar o cursor na linha selecionada e executa uma atualização posicionada da linha. (Tratamento de erros é omitido por motivos de clareza).  
  
```  
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
  
 Para obter mais exemplos, consulte [posicionado instruções Update e excluir](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md) e [atualizando linhas no conjunto de linhas com SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Um buffer de associação a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Executando operações em massa que não estão relacionados à posição do bloco de cursor|[Função SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Buscar um bloco de dados ou rolar por um resultado definido|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Obter um único campo de um descritor de|[Função SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Introdução a vários campos de um descritor de|[Função SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Configuração de um único campo de um descritor de|[Função SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Configuração de vários campos de um descritor de|[Função SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|Definir um atributo de instrução|[Função SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
