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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3ca7ed4f6bbcd31b8f67b95dc14a2c6c301b5a59
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138825"
---
# <a name="sqlmoreresults-function"></a>Função SQLMoreResults
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: ODBC  
  
 **Resumo**  
 **SQLMoreResults** determina se mais resultados estão disponíveis em uma instrução que contém instruções **Select**, **Update**, **Insert**ou **delete** e, em caso afirmativo, inicializa o processamento para esses resultados.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLMoreResults(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 Entrada Identificador de instrução.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_NO_DATA, SQL_ERROR, SQL_INVALID_HANDLE OU SQL_PARAM_DATA_AVAILABLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLMoreResults** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *identificador* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLMoreResults** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|DESCRIÇÃO|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01S02|O valor da opção foi alterado|O valor de um atributo de instrução foi alterado quando o lote estava sendo processado. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado falhou antes da função concluir o processamento.|  
|40001|Falha de serialização|A transação foi revertida devido a um deadlock de recurso com outra transação.|  
|40003|Conclusão de instrução desconhecida|A conexão associada falhou durante a execução dessa função e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \*MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função **SQLMoreResults** foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função **SQLMoreResults** foi chamada novamente no *StatementHandle*.<br /><br /> A função **SQLMoreResults** foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativo multithread.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *StatementHandle*. Esta função assíncrona ainda estava em execução quando a função **SQLMoreResults** foi chamada.<br /><br /> (DM) uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado para o *StatementHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *StatementHandle* não oferece suporte à função.|  
|IM017|A sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação for usado, a sondagem será desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesse identificador.|Se a chamada de função anterior no identificador retornar SQL_STILL_EXECUTING e se o modo de notificação estiver habilitado, **SQLCompleteAsync** deverá ser chamado na alça para executar o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 As instruções **Select** retornam conjuntos de resultados. As instruções **Update**, **Insert**e **delete** retornam uma contagem de linhas afetadas. Se qualquer uma dessas instruções for submetida em lote, enviada com matrizes de parâmetros (numeradas em ordem crescente de parâmetros, na ordem em que aparecem no lote) ou em procedimentos, elas poderão retornar vários conjuntos de resultados ou contagens de linhas. Para obter informações sobre lotes de instruções e matrizes de parâmetros, consulte [lotes de instruções SQL](../../../odbc/reference/develop-app/batches-of-sql-statements.md) e [matrizes de valores de parâmetro](../../../odbc/reference/develop-app/arrays-of-parameter-values.md).  
  
 Depois de executar o lote, o aplicativo é posicionado no primeiro conjunto de resultados. O aplicativo pode chamar **SQLBindCol**, **SQLBulkOperations**, **SQLFetch**, **SQLGetData**, **SQLFetchScroll**, **SQLSetPos**e todas as funções de metadados, no primeiro ou em qualquer conjunto de resultados subsequente, assim como faria se houvesse apenas um único conjunto de resultados. Assim que for feito com o primeiro conjunto de resultados, o aplicativo chamará **SQLMoreResults** para mover para o próximo conjunto de resultados. Se outro conjunto de resultados ou contagem estiver disponível, **SQLMoreResults** retornará SQL_SUCCESS e inicializará o conjunto de resultados ou a contagem para processamento adicional. Se qualquer instrução de geração de contagem de linhas aparecer entre instruções de geração de conjunto de resultados, elas poderão ser percorridas chamando **SQLMoreResults**. Depois de chamar **SQLMoreResults** para as instruções **Update**, **Insert**ou **delete** , um aplicativo pode chamar **SQLRowCount**.  
  
 Se houver um conjunto de resultados atual com linhas não buscadas, o **SQLMoreResults** descartará esse conjunto de resultados e tornará o próximo conjunto de resultados ou a contagem disponível. Se todos os resultados tiverem sido processados, **SQLMoreResults** retornará SQL_NO_DATA. Para alguns drivers, os parâmetros de saída e os valores de retorno não estão disponíveis até que todos os conjuntos de resultados e contagens de linhas tenham sido processados. Para esses drivers, os parâmetros de saída e os valores de retorno ficam disponíveis quando **SQLMoreResults** retorna SQL_NO_DATA.  
  
 Todas as associações que foram estabelecidas para o conjunto de resultados anterior ainda permanecem válidas. Se as estruturas de coluna forem diferentes para esse conjunto de resultados, chamar **SQLFetch** ou **SQLFetchScroll** poderá resultar em um erro ou truncamento. Para evitar isso, o aplicativo precisa chamar **SQLBindCol** para reassociar explicitamente conforme apropriado (ou fazer isso definindo os campos de descritor). Como alternativa, o aplicativo pode chamar **SQLFreeStmt** com uma *opção* de SQL_UNBIND para desassociar todos os buffers de coluna.  
  
 Os valores de atributos de instrução, como tipo de cursor, simultaneidade do cursor, tamanho do conjunto de chaves ou comprimento máximo, podem mudar à medida que o aplicativo navega pelo lote por chamadas para **SQLMoreResults**. Se isso acontecer, **SQLMoreResults** retornará SQL_SUCCESS_WITH_INFO e SQLSTATE 01S02 (o valor da opção será alterado).  
  
 Chamar **SQLCloseCursor**ou **SQLFreeStmt** com uma *opção* de SQL_CLOSE, descarta todos os conjuntos de resultados e contagens de linhas que estavam disponíveis como resultado da execução do lote. O identificador de instrução retorna ao estado alocado ou preparado. Chamar **SQLCancel** para cancelar uma função executando de forma assíncrona quando um lote foi executado e o identificador de instrução está no estado executado, posicionado no cursor ou assíncrono resulta em todos os conjuntos de resultados e contagens de linhas geradas pelo lote que serão descartadas se a chamada de cancelamento tiver sido bem-sucedida. Em seguida, a instrução retorna para o estado preparado ou alocado.  
  
 Se um lote de instruções ou um procedimento mixar outras instruções SQL com instruções **Select**, **Update**, **Insert**e **delete** , essas outras instruções não afetarão **SQLMoreResults**.  
  
 Para obter mais informações, consulte [vários resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 Se uma instrução UPDATE, INSERT ou DELETE pesquisada em um lote de instruções não afetar nenhuma linha na fonte de dados, **SQLMoreResults** retornará SQL_SUCCESS. Isso é diferente do caso de uma instrução UPDATE, INSERT ou DELETE pesquisada que é executada por meio de **SQLExecDirect**, **SQLExecute**ou **SQLParamData**, que retorna SQL_NO_DATA se não afetar nenhuma linha na fonte de dados. Se um aplicativo chamar **SQLRowCount** para recuperar a contagem de linhas depois que uma chamada para **SQLMoreResults** não tiver afetado nenhuma linha, **SQLRowCount** retornará SQL_NO_DATA.  
  
 Para obter informações adicionais sobre o sequenciamento válido de funções de processamento de resultado, consulte o [Apêndice B: tabelas de transição de estado ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Para obter mais informações sobre SQL_PARAM_DATA_AVAILABLE e parâmetros de saída em fluxo, consulte [recuperando parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="availability-of-row-counts"></a>Disponibilidade de contagens de linhas  
 Quando um lote contém várias instruções geradoras de contagem de linhas consecutivas, é possível que essas contagens de linhas sejam acumuladas em apenas uma contagem de linhas. Por exemplo, se um lote tiver cinco instruções INSERT, determinadas fontes de dados serão capazes de retornar cinco contagens de linhas individuais. Algumas outras fontes de dados retornam apenas uma contagem de linhas que representa a soma das cinco contagens de linhas individuais.  
  
 Quando um lote contém uma combinação de instruções de geração de conjunto de resultados e contagem de linhas, as contagens de linhas podem ou não estar disponíveis. O comportamento do driver em relação à disponibilidade de contagens de linhas é enumerado no tipo de informação SQL_BATCH_ROW_COUNT disponível por meio de uma chamada para **SQLGetInfo**. Por exemplo, suponha que o lote contenha um **Select**, seguido por dois **Insert**s e outro **Select**. Em seguida, os seguintes casos são possíveis:  
  
-   As contagens de linhas correspondentes às duas instruções **Insert** não estão disponíveis. A primeira chamada para **SQLMoreResults** irá posicioná-lo no conjunto de resultados da segunda instrução **Select** .  
  
-   As contagens de linhas correspondentes às duas instruções **Insert** estão disponíveis individualmente. (Uma chamada para **SQLGetInfo** não retorna o bit de SQL_BRC_ROLLED_UP para o tipo de informação SQL_BATCH_ROW_COUNT.) A primeira chamada para **SQLMoreResults** irá posicioná-lo na contagem de linhas da primeira **inserção**, e a segunda chamada irá posicioná-lo na contagem de linhas da segunda **inserção**. A terceira chamada para **SQLMoreResults** irá posicioná-lo no conjunto de resultados da segunda instrução **Select** .  
  
-   As contagens de linhas correspondentes às duas **inserções** são acumuladas em uma única contagem de linhas que está disponível. (Uma chamada para **SQLGetInfo** retorna o bit de SQL_BRC_ROLLED_UP para o tipo de informação SQL_BATCH_ROW_COUNT.) A primeira chamada para **SQLMoreResults** irá posicioná-lo na contagem de linhas acumuladas e a segunda chamada para **SQLMoreResults** irá posicioná-lo no conjunto de resultados da segunda **seleção**.  
  
 Determinados drivers disponibilizam contagens de linha apenas para lotes explícitos e não para procedimentos armazenados.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Buscando um bloco de dados ou rolando por meio de um conjunto de resultados|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Buscando uma única linha ou um bloco de dados em uma direção somente de avanço|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Buscando parte ou toda uma coluna de dados|[Função SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recuperar parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
