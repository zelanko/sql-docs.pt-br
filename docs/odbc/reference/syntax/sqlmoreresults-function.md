---
title: "Função SQLMoreResults | Microsoft Docs"
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
- SQLMoreResults
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLMoreResults
helpviewer_keywords:
- SQLMoreResults function [ODBC]
ms.assetid: bf169ed5-4d55-412c-b184-12065a726e89
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 772bfd3d05d620840ea43c9f1313b4d94add10de
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlmoreresults-function"></a>Função SQLMoreResults
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 1.0 ODBC: ODBC  
  
 **Resumo**  
 **SQLMoreResults** determina se houver mais resultados disponíveis em uma instrução que contém **selecione**, **atualização**, **inserir**, ou  **Excluir** instruções e, nesse caso, inicializa o processamento para esses resultados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLMoreResults(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrução.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_NO_DATA, SQL_ERROR, SQL_INVALID_HANDLE OU SQL_PARAM_DATA_AVAILABLE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLMoreResults** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* do SQL _HANDLE_STMT e um *tratar* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLMoreResults** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01S02|Valor de opção alterado|O valor de um atributo de instrução foram alterado como o lote foi sendo processado. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|40001|Falha na serialização|A transação foi revertida devido a um deadlock de recursos com outra transação.|  
|40003|Conclusão de instrução desconhecido|Falha de conexão associado durante a execução dessa função e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo **SQLGetDiagRec** no  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. O **SQLMoreResults** função foi chamada e, antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* . Em seguida, o **SQLMoreResults** função foi chamada novamente no *StatementHandle*.<br /><br /> O **SQLMoreResults** função foi chamada e, antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*  de um thread diferente em um aplicativo multithread.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando o **SQLMoreResults** função foi chamada.<br /><br /> (DM) uma função de execução assíncrona (não la) foi chamada para o *StatementHandle* e ainda estava em execução quando esta função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retorna SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todas as colunas ou parâmetros de dados em execução.|  
|HY013|Erro de gerenciamento de memória|Não foi possível processar a chamada de função porque os objetos de memória subjacente não podem ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecido. Somente Desconecte e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|O driver em (DM) associado a *StatementHandle* não oferece suporte para a função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem está desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior na alça retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 **Selecione** instruções retornam conjuntos de resultados. **ATUALIZAÇÃO**, **inserir**, e **excluir** instruções retornam uma contagem de linhas afetadas. Se alguma dessas instruções são em lote, enviada com matrizes de parâmetros (numerados em ordem de parâmetro, na ordem em que aparecem no lote crescente), ou em procedimentos, elas podem retornar vários conjuntos de resultados ou contagens de linhas. Para obter informações sobre lotes de instruções e matrizes de parâmetros, consulte [Batches of SQL Statements](../../../odbc/reference/develop-app/batches-of-sql-statements.md) e [matrizes de valores de parâmetro](../../../odbc/reference/develop-app/arrays-of-parameter-values.md).  
  
 Depois de executar o lote, o aplicativo é posicionado no primeiro conjunto de resultados. O aplicativo pode chamar **SQLBindCol**, **SQLBulkOperations**, **SQLFetch**, **SQLGetData**, **SQLFetchScroll** , **SQLSetPos**e todas as funções de metadados, em conjuntos de resultados da primeira ou qualquer subsequentes, exatamente como faria se houver apenas um único conjunto de resultados. Quando isso é feito com o primeiro conjunto de resultados, o aplicativo chama **SQLMoreResults** para mover para o próximo conjunto de resultados. Se houver outro conjunto de resultados ou contagem, **SQLMoreResults** retorna SQL_SUCCESS e inicializa o conjunto de resultados ou a contagem para processamento adicional. Se quaisquer instruções de geração de contagem de linhas aparecem entre resultar de geração de conjunto de instruções, eles podem ser pulados pela chamada **SQLMoreResults**. Depois de chamar **SQLMoreResults** para **atualização**, **inserir**, ou **excluir** instruções, um aplicativo pode chamar **SQLRowCount**.  
  
 Se houver um atual conjunto de resultados com linhas não buscadas, **SQLMoreResults** descarta aquele conjunto de resultados e torna o próximo conjunto de resultados ou contagem disponíveis. Se todos os resultados foram processados, **SQLMoreResults** retorna SQL_NO_DATA. Para alguns drivers, valores de retorno e parâmetros de saída não estão disponíveis até que todos os conjuntos de resultados e contagens de linhas foram processadas. Para esses drivers, parâmetros de saída e retornar valores ficam disponíveis quando **SQLMoreResults** retorna SQL_NO_DATA.  
  
 Associações que foram estabelecidas anterior conjunto de resultados ainda permanecerão válidas. Se as estruturas de coluna diferentes para esse conjunto de resultados, em seguida, chamar **SQLFetch** ou **SQLFetchScroll** pode resultar em um erro ou truncamento. Para evitar isso, o aplicativo precisa chamar **SQLBindCol** explicitamente reassociar conforme apropriado (ou fazê-lo definindo campos de descritor). Como alternativa, o aplicativo pode chamar **SQLFreeStmt** com um *opção* de SQL_UNBIND para desassociar todos os buffers de coluna.  
  
 Os valores de atributos de instrução, como o tipo de cursor, simultaneidade do cursor, tamanho do conjunto de chaves ou tamanho máximo, podem alterar como o aplicativo navega pelo lote por chamadas para **SQLMoreResults**. Se isso acontecer, **SQLMoreResults** retornará SQL_SUCCESS_WITH_INFO e SQLSTATE 01S02 (o valor da opção foi alterado).  
  
 Chamando **SQLCloseCursor**, ou **SQLFreeStmt** com um *opção* de SQL_CLOSE, descarta todos os conjuntos de resultados e contagens de linha que estavam disponíveis como resultado da execução do o lote. Retorna o identificador de instrução para o estado preparado ou alocado. Chamando **SQLCancel** para cancelar uma função de execução assíncrona quando um lote foi executado e o identificador de instrução for executada, cursor posicionado ou estado assíncronas conjuntos de resultados em todos os resultados e contagens de linha gerados pelo lote que está sendo descartado se a chamada de cancelamento foi bem-sucedido. Em seguida, a instrução retorna ao estado preparado ou alocado.  
  
 Se um lote de instruções ou um procedimento mistura outras instruções SQL com **selecione**, **atualização**, **inserir**, e **excluir** instruções Essas outras instruções não afetarão **SQLMoreResults**.  
  
 Para obter mais informações, consulte [vários resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 Se um pesquisada atualizar, insere ou excluir instrução em um lote de instruções não afeta qualquer linha na fonte de dados, **SQLMoreResults** retorna SQL_SUCCESS. Isso é diferente do caso de uma atualização pesquisada, insert ou delete que é executado por meio de **SQLExecDirect**, **SQLExecute**, ou **SQLParamData**, que retorna SQL_NO_DATA se ele não afeta qualquer linha na fonte de dados. Se um aplicativo chamar **SQLRowCount** para recuperar a contagem de linhas após uma chamada para **SQLMoreResults** não afetou linhas, **SQLRowCount** irá retornar SQL_NO_DATA.  
  
 Para obter informações adicionais sobre o sequenciamento válido de funções de processamento de resultados, consulte [tabelas de transição de estado do apêndice b: ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Para obter mais informações sobre SQL_PARAM_DATA_AVAILABLE e parâmetros de saída em fluxo, consulte [recuperar parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="availability-of-row-counts"></a>Disponibilidade de contagens de linhas  
 Quando um lote contiver várias instruções de geração de contagem de linhas consecutivas, é possível que essas contagens de linha são acumuladas na contagem de apenas uma linha. Por exemplo, se um lote tem cinco instruções insert, certas fontes de dados serão capazes de retorno de cinco contagens de linhas individuais. Certas fontes de dados retornam a contagem de apenas uma linha que representa a soma das cinco contagens de linhas individuais.  
  
 Quando um lote contém uma combinação de geração de conjunto de resultados e instruções de geração de contagem de linhas, contagens de linhas podem ou não podem estar disponíveis em todos os. O comportamento do driver em relação à disponibilidade de contagens de linhas é enumerado em disponíveis por meio de uma chamada para o tipo de informação SQL_BATCH_ROW_COUNT **SQLGetInfo**. Por exemplo, suponha que o lote contém uma **selecione**, seguido por dois **inserir**s e outro **selecione**. Em seguida, os casos a seguir são possíveis:  
  
-   As contagens de linhas correspondentes para os dois **inserir** instruções não estão disponíveis em todos os. A primeira chamada para **SQLMoreResults** posição no conjunto de resultados da segunda **selecione** instrução.  
  
-   As contagens de linhas correspondentes para os dois **inserir** instruções estão disponíveis individualmente. (Uma chamada para **SQLGetInfo** não retorna o bit SQL_BRC_ROLLED_UP para o tipo de informação SQL_BATCH_ROW_COUNT.) A primeira chamada para **SQLMoreResults** posicionará na contagem de linha da primeira **inserir**, e a segunda chamada posicionará na contagem de linha da segunda **inserir**. A terceira chamada para **SQLMoreResults** posição no conjunto de resultados da segunda **selecione** instrução.  
  
-   As contagens de linhas correspondentes para os dois **insere** são acumulados em uma contagem de única linha que está disponível. (Uma chamada para **SQLGetInfo** retorna o SQL_BRC_ROLLED_UP bit para o tipo de informação SQL_BATCH_ROW_COUNT.) A primeira chamada para **SQLMoreResults** posicionar a contagem de linhas acumuladas e a segunda chamada para **SQLMoreResults** posição no conjunto de resultados da segunda **selecione**.  
  
 Determinados drivers disponibilizar contagens de linhas apenas para lotes explícitas e não para procedimentos armazenados.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Buscar um bloco de dados ou rolar por um resultado definido|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Buscando uma única linha ou um bloco de dados em uma direção de somente avanço|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Busca de parte ou toda uma coluna de dados|[Função SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recuperando parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)

