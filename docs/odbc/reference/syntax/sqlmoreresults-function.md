---
title: Função SQLMoreResults | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 78bbb277e4b783eb46c79f59939a1080feae2b60
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304737"
---
# <a name="sqlmoreresults-function"></a>Função SQLMoreResults
**Conformidade**  
 Versão introduzida: ODBC 1.0 Normas Conformidade: ODBC  
  
 **Resumo**  
 **O SQLMoreResults** determina se mais resultados estão disponíveis em uma instrução contendo **instruções SELECT,** **UPDATE,** **INSERT**ou **DELETE** e, se for o caso, inicia o processamento desses resultados.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLMoreResults(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Alça de declaração.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_NO_DATA SQL_ERROR, SQL_INVALID_HANDLE ou SQL_PARAM_DATA_AVAILABLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLMoreResults** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *alça* de controle de *declaração*. A tabela a seguir lista os valores SQLSTATE comumente retornados por **SQLMoreResults** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01S02|O valor da opção mudou|O valor de um atributo de declaração mudou à medida que o lote estava sendo processado. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados à qual o driver estava conectado falhou antes da função ser concluída.|  
|40001|Falha na serialização|A transação foi revertida devido a um impasse de recursos com outra transação.|  
|40003|Conclusão de declaração desconhecida|A conexão associada falhou durante a execução desta função e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função **SQLMoreResults** foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função **SQLMoreResults** foi chamada novamente no *StatementHandle*.<br /><br /> A função **SQLMoreResults** foi chamada e, antes de ser concluída, **SQLCancel** ou **SQLCancelHandle** foi chamada no *StatementHandle* de um segmento diferente em um aplicativo multithread.|  
|HY010|Erro de seqüência de função|(DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *StatementHandle*. Esta função assíncrona ainda estava sendo executada quando a função **SQLMoreResults** foi chamada.<br /><br /> (DM) Uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados para o *StatementHandle* e retornaram SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *StatementHandle* não suporta a função.|  
|IM017|A votação é desativada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a votação é desativada.|  
|IM018|**O SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesta alça.|Se a chamada de função anterior na alça retornar SQL_STILL_EXECUTING e se o modo de notificação estiver ativado, o **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 **Conjuntos** de resultados de retorno de instruções SELECT. **AS instruções UPDATE,** **INSERT**e **DELETE** retornam uma contagem de linhas afetadas. Se alguma dessas instruções for em lote, submetida a matrizes de parâmetros (numeradas na ordem de parâmetros crescentes, na ordem em que aparecem no lote), ou em procedimentos, elas podem retornar vários conjuntos de resultados ou contagem de linhas. Para obter informações sobre lotes de instruções e matrizes de parâmetros, consulte [Lotes de Declarações SQL](../../../odbc/reference/develop-app/batches-of-sql-statements.md) e [Matrizes de Valores de Parâmetros](../../../odbc/reference/develop-app/arrays-of-parameter-values.md).  
  
 Após a execução do lote, a aplicação é posicionada no primeiro conjunto de resultados. O aplicativo pode chamar **SQLBindCol,** **SQLBulkOperations,** **SQLFetch,** **SQLGetData,** **SQLFetchScroll,** **SQLSetPos**e todas as funções de metadados, no primeiro ou em qualquer conjunto de resultados subsequentes, assim como seria se houvesse apenas um único conjunto de resultados. Uma vez feito o primeiro conjunto de resultados, o aplicativo chama **SQLMoreResults** para passar para o próximo conjunto de resultados. Se outro conjunto de resultados ou contagem estiver disponível, **o SQLMoreResults** retorna SQL_SUCCESS e inicializa o conjunto de resultados ou a contagem para processamento adicional. Se quaisquer instruções geradoras de contagem de linhas aparecerem entre as instruções de geração de conjuntos de resultados, elas podem ser ultrapassadas ligando para **SQLMoreResults**. Depois de chamar **SQLMoreResults** para **instruções UPDATE,** **INSERT**ou **DELETE,** um aplicativo pode chamar **SQLRowCount**.  
  
 Se houvesse um conjunto de resultados atual com linhas não buscadas, **o SQLMoreResults** descartaria esse conjunto de resultados e torna o próximo conjunto de resultados ou contagem disponível. Se todos os resultados forem processados, **o SQLMoreResults** retorna SQL_NO_DATA. Para alguns drivers, os parâmetros de saída e os valores de retorno não estão disponíveis até que todos os conjuntos de resultados e contagem de linhas tenham sido processados. Para esses drivers, parâmetros de saída e valores de retorno ficam disponíveis quando **o SQLMoreResults** retorna SQL_NO_DATA.  
  
 As vinculações estabelecidas para o conjunto de resultados anteriores ainda permanecem válidas. Se as estruturas da coluna forem diferentes para este conjunto de resultados, então chamar **SQLFetch** ou **SQLFetchScroll** pode resultar em um erro ou truncamento. Para evitar isso, o aplicativo deve chamar **o SQLBindCol** para revincular explicitamente conforme apropriado (ou fazê-lo definindo campos descritores). Alternativamente, o aplicativo pode chamar **SQLFreeStmt** com uma *opção* de SQL_UNBIND desvincular todos os buffers de coluna.  
  
 Os valores dos atributos de declaração, como tipo de cursor, concorrência do cursor, tamanho do conjunto de chaves ou comprimento máximo, podem mudar à medida que o aplicativo navega através do lote por chamadas para **SQLMoreResults**. Se isso acontecer, **o SQLMoreResults** retornará SQL_SUCCESS_WITH_INFO e SQLSTATE 01S02 (o valor da opção foi alterado).  
  
 Chamando **SQLCloseCursor**, ou **SQLFreeStmt** com uma *opção* de SQL_CLOSE, descarta todos os conjuntos de resultados e contagens de linha que estavam disponíveis como resultado da execução do lote. A alça da declaração retorna ao estado alocado ou preparado. Chamar **o SQLCancel** para cancelar uma função de execução assíncrona quando um lote foi executado e a alça de declaração estiver no estado executado, posicionado no cursor ou no estado assíncrono resulta em todos os conjuntos de resultados e contagens de linhas geradas pelo lote sendo descartado se a chamada de cancelamento for bem sucedida. A declaração então retorna ao estado preparado ou alocado.  
  
 Se um lote de declarações ou um procedimento misturar outras instruções SQL com **instruções SELECT,** **UPDATE,** **INSERT**e **DELETE,** essas outras instruções não afetam **o SQLMoreResults**.  
  
 Para obter mais informações, consulte [Múltiplos Resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 Se uma atualização pesquisada, inserir ou excluir a instrução em um lote de declarações não afetar nenhuma linha na fonte de dados, o **SQLMoreResults** retorna SQL_SUCCESS. Isso é diferente do caso de uma instrução de atualização, inserção ou exclusão pesquisada que é executada através **de SQLExecDirect,** **SQLExecute**ou **SQLParamData,** que retorna SQL_NO_DATA se não afetar nenhuma linha na fonte de dados. Se um aplicativo chamar **o SQLRowCount** para recuperar a contagem de linhas após uma chamada para **SQLMoreResults** não tiver afetado nenhuma linha, **o SQLRowCount** retornará SQL_NO_DATA.  
  
 Para obter informações adicionais sobre o sequenciamento válido das funções de processamento de resultados, consulte [o apêndice B: Tabelas de Transição do Estado ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Para obter mais informações sobre SQL_PARAM_DATA_AVAILABLE e parâmetros de saída transmitidos, consulte [Recuperando parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="availability-of-row-counts"></a>Disponibilidade de contagens de linhas  
 Quando um lote contém várias instruções consecutivas de geração de contagem de linhas, é possível que essas contagens de linha sejam enroladas em apenas uma contagem de linhas. Por exemplo, se um lote tiver cinco instruções de inserção, então certas fontes de dados são capazes de retornar cinco contagens individuais de linha. Certas outras fontes de dados retornam apenas uma contagem de linhas que representa a soma das cinco contagens de linha individuais.  
  
 Quando um lote contém uma combinação de demonstrações de geração de conjuntos de resultados e geração de contagem de linhas, as contagens de linha podem ou não estar disponíveis. O comportamento do motorista em relação à disponibilidade de contagem de linhas é enumerado no SQL_BATCH_ROW_COUNT tipo de informação disponível através de uma chamada para **SQLGetInfo**. Por exemplo, suponha que o lote contenha um **SELECT**, seguido por dois **INSERT**s e outro **SELECT**. Em seguida, os seguintes casos são possíveis:  
  
-   As contagens de linha correspondentes às duas instruções **INSERT** não estão disponíveis. A primeira chamada para **SQLMoreResults** irá posicioná-lo no conjunto de resultados da segunda declaração **SELECT.**  
  
-   As contagens de linha correspondentes às duas instruções **INSERT** estão disponíveis individualmente. (Uma chamada para **SQLGetInfo** não retorna o SQL_BRC_ROLLED_UP bit para o SQL_BATCH_ROW_COUNT tipo de informação.) A primeira chamada para **SQLMoreResults** irá posicioná-lo na contagem de linhas do primeiro **INSERT**, e a segunda chamada irá posicioná-lo na contagem de linhas do segundo **INSERT**. A terceira chamada para **SQLMoreResults** irá posicioná-lo no conjunto de resultados da segunda declaração **SELECT.**  
  
-   As contagens de linha correspondentes aos dois **INSERTs** são enroladas em uma única contagem de linhas que está disponível. (Uma chamada para **SQLGetInfo** retorna o SQL_BRC_ROLLED_UP bit para o SQL_BATCH_ROW_COUNT tipo de informação.) A primeira chamada para **SQLMoreResults** irá posicioná-lo na contagem de linhas enroladas, e a segunda chamada para **SQLMoreResults** irá posicioná-lo no conjunto de resultados do segundo **SELECT**.  
  
 Certos drivers disponibilizam a contagem de linhas apenas para lotes explícitos e não para procedimentos armazenados.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Cancelamento do processamento de declarações|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Buscar um bloco de dados ou rolar através de um conjunto de resultados|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Buscar uma única linha ou um bloco de dados em uma direção somente para a frente|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Buscar parte ou toda uma coluna de dados|[Função SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recuperar parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
