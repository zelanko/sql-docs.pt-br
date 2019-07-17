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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138825"
---
# <a name="sqlmoreresults-function"></a>Função SQLMoreResults
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 1.0 ODBC: ODBC  
  
 **Resumo**  
 **SQLMoreResults** determina se houver mais resultados disponíveis em uma instrução que contém **selecionar**, **UPDATE**, **inserir**, ou  **Excluir** instruções e, nesse caso, inicializa o processamento para esses resultados.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLMoreResults(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrução.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_NO_DATA, SQL_ERROR, SQL_INVALID_HANDLE OU SQL_PARAM_DATA_AVAILABLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLMoreResults** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* do SQL _HANDLE_STMT e uma *manipular* dos *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLMoreResults** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01S02|Valor de opção alterado|O valor de um atributo de instrução foram alterado como o lote estava sendo processado. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|40001|Falha na serialização|A transação foi revertida devido a um deadlock de recursos com outra transação.|  
|40003|Conclusão desconhecida de declaração|A conexão associada falhou durante a execução dessa função e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** na  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. O **SQLMoreResults** função foi chamada e, antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* . Em seguida, a **SQLMoreResults** função foi chamada novamente na *StatementHandle*.<br /><br /> O **SQLMoreResults** função foi chamada e, antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*  de um thread diferente em um aplicativo multithread.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando o **SQLMoreResults** função foi chamada.<br /><br /> (DM) uma função de execução assíncrona (não desse último) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retornados de SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|O driver em (DM) associado a *StatementHandle* não suporta a função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem é desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior no identificador retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado no identificador de fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 **Selecione** instruções retornam conjuntos de resultados. **ATUALIZAÇÃO**, **inserir**, e **excluir** instruções retornam uma contagem de linhas afetadas. Se qualquer uma dessas instruções são em lote, enviado com matrizes de parâmetros (numerados em ordem de parâmetro, na ordem em que aparecem no lote crescente) ou em procedimentos, elas podem retornar vários conjuntos de resultados ou contagens de linhas. Para obter informações sobre lotes de instruções e matrizes de parâmetros, consulte [Batches of SQL Statements](../../../odbc/reference/develop-app/batches-of-sql-statements.md) e [matrizes de valores de parâmetro](../../../odbc/reference/develop-app/arrays-of-parameter-values.md).  
  
 Depois de executar o lote, o aplicativo está posicionado no primeiro conjunto de resultados. O aplicativo pode chamar **SQLBindCol**, **SQLBulkOperations**, **SQLFetch**, **SQLGetData**, **SQLFetchScroll** , **SQLSetPos**e todas as funções de metadados, em conjuntos de resultados do primeiro ou qualquer subsequentes, assim como faria se houver apenas um único conjunto de resultados. Depois que ele é feito com o primeiro conjunto de resultados, o aplicativo chama **SQLMoreResults** para mover para o próximo conjunto de resultados. Se estiver disponível, de outro conjunto de resultados ou contagem **SQLMoreResults** retorna SQL_SUCCESS e inicializa o conjunto de resultados ou a contagem para processamento adicional. Se quaisquer instruções de geração de contagem de linha aparecem entre resultar gerar o conjunto de instruções, eles podem ser manipulados a tecla TAB chamando **SQLMoreResults**. Depois de chamar **SQLMoreResults** para **atualização**, **inserir**, ou **excluir** instruções, um aplicativo pode chamar **SQLRowCount**.  
  
 Se houvesse um atual conjunto de resultados com linhas não buscadas **SQLMoreResults** descarta esse conjunto de resultados e torna o próximo conjunto de resultados ou contar disponíveis. Se todos os resultados foram processados, **SQLMoreResults** retorne SQL_NO_DATA. Para alguns drivers, valores de retornados e parâmetros de saída não estão disponíveis até que todos os conjuntos de resultados e contagens de linhas foram processadas. Para esses drivers, parâmetros de saída e retornar valores ficam disponíveis quando **SQLMoreResults** retorne SQL_NO_DATA.  
  
 Quaisquer associações que foram estabelecidas para o resultado anterior definido ainda permanecem válidas. Se as estruturas de coluna são diferentes para esse conjunto de resultados, em seguida, chamando **SQLFetch** ou **SQLFetchScroll** pode resultar em um erro ou truncamento. Para evitar isso, o aplicativo tem que chamar **SQLBindCol** explicitamente reassociar conforme apropriado (ou fazer isso definindo campos de descritor). Como alternativa, o aplicativo pode chamar **SQLFreeStmt** com um *opção* de SQL_UNBIND para desvincular todos os buffers de coluna.  
  
 Os valores de atributos de instrução, como o tipo de cursor, simultaneidade do cursor, tamanho do conjunto de chaves ou comprimento máximo, podem mudar conforme o aplicativo navega por meio de lote por chamadas para **SQLMoreResults**. Se isso acontecer, **SQLMoreResults** retornará SQL_SUCCESS_WITH_INFO e SQLSTATE 01S02 (o valor de opção foi alterado).  
  
 Chamando **SQLCloseCursor**, ou **SQLFreeStmt** com um *opção* de SQL_CLOSE, descarta todos os conjuntos de resultados e contagens de linhas que estavam disponíveis como resultado da execução do o lote. Retorna o identificador de instrução para o estado preparado ou alocado. Chamando **SQLCancel** para cancelar uma função de forma assíncrona em execução quando um lote foi executado e o identificador de instrução está em executado, o cursor posicionado ou estado assíncrono conjuntos de resultados em todos os resultados e contagens de linhas gerado pelo lote que está sendo descartado se a chamada de cancelamento foi bem-sucedido. A instrução, em seguida, retorna para o estado preparado ou alocado.  
  
 Se um lote de instruções ou um procedimento combina outras instruções SQL com **selecionar**, **atualização**, **inserir**, e **excluir** instruções, Essas outras instruções não afetam **SQLMoreResults**.  
  
 Para obter mais informações, consulte [vários resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 Se um pesquisada, insere, instrução update ou delete em um lote de instruções não afetará quaisquer linhas na fonte de dados, **SQLMoreResults** retorna SQL_SUCCESS. Isso é diferente do caso de uma atualização pesquisada, inserir ou excluir a instrução é executada por meio **SQLExecDirect**, **SQLExecute**, ou **SQLParamData**, que retorna SQL_NO_DATA se isso não afetará quaisquer linhas na fonte de dados. Se um aplicativo chamar **SQLRowCount** para recuperar a contagem de linhas após uma chamada para **SQLMoreResults** não afetou nenhuma linha **SQLRowCount** irá retornar SQL_NO_DATA.  
  
 Para obter informações adicionais sobre o sequenciamento válido de funções de processamento de resultados, consulte [apêndice b: Tabelas de transição de estado ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Para obter mais informações sobre parâmetros de saída transmitidos e SQL_PARAM_DATA_AVAILABLE, consulte [Recuperando parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="availability-of-row-counts"></a>Disponibilidade de contagens de linhas  
 Quando um lote contiver várias instruções de geração de contagem de linhas consecutivas, é possível que essas contagens de linhas são acumuladas na contagem de apenas uma linha. Por exemplo, se um lote tiver cinco instruções insert, em seguida, certas fontes de dados são capazes de retornar contagens de linhas individuais de cinco. Determinadas fontes de dados retornam a contagem de apenas uma linha que representa a soma das cinco contagens de linha individual.  
  
 Quando um lote contém uma combinação de geração de conjunto de resultados e instruções de geração de contagem de linhas, contagens de linhas podem ou não podem estar disponíveis em todos os. O comportamento do driver em relação a disponibilidade de contagens de linhas é enumerado no disponíveis por meio de uma chamada para o tipo de informação SQL_BATCH_ROW_COUNT **SQLGetInfo**. Por exemplo, suponha que o lote contém uma **selecionar**, seguido por dois **inserir**s e outro **selecione**. Em seguida, os casos a seguir são possíveis:  
  
-   As contagens de linhas correspondentes para as duas **inserir** instruções não estão disponíveis em todos os. A primeira chamada para **SQLMoreResults** posicionar no conjunto de resultados da segunda **selecione** instrução.  
  
-   As contagens de linhas correspondentes para as duas **inserir** instruções estão disponíveis individualmente. (Uma chamada para **SQLGetInfo** não retorna o bit SQL_BRC_ROLLED_UP para o tipo de informação SQL_BATCH_ROW_COUNT.) A primeira chamada para **SQLMoreResults** posicionar na contagem de linha da primeira **inserir**, e a segunda chamada irá posicionar na contagem de linha da segunda **inserir**. A terceira chamada para **SQLMoreResults** posicionar no conjunto de resultados da segunda **selecione** instrução.  
  
-   As contagens de linhas correspondentes para as duas **insere** são acumulados em uma contagem de única linha que está disponível. (Uma chamada para **SQLGetInfo** retorna o SQL_BRC_ROLLED_UP de bits para o tipo de informação SQL_BATCH_ROW_COUNT.) A primeira chamada para **SQLMoreResults** posicionar a contagem de linhas da acumulados e a segunda chamada para **SQLMoreResults** posicionar no conjunto de resultados da segunda **SELECT**.  
  
 Determinados drivers disponibilizar contagens de linhas somente lotes explícitos e não de procedimentos armazenados.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Buscar um bloco de dados ou rolar por um resultado definido|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Buscando uma única linha ou um bloco de dados em uma direção de somente avanço|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Buscando parte ou toda uma coluna de dados|[Função SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recuperando parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
