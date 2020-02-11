---
title: Função SQLParamData | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLParamData
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLParamData
helpviewer_keywords:
- SQLParamData function [ODBC]
ms.assetid: 68fe010d-9539-4e5b-a260-c8d32423b1db
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 41cb718b5425315856fe4db27658cce873f90e6b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68018945"
---
# <a name="sqlparamdata-function"></a>Função SQLParamData
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: ISO 92  
  
 **Resumo**  
 **SQLParamData** é usado junto com **SQLPutData** para fornecer dados de parâmetro no tempo de execução da instrução e com **SQLGetData** para recuperar dados de parâmetro de saída transmitidos.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLParamData(  
     SQLHSTMT       StatementHandle,  
     SQLPOINTER *   ValuePtrPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 Entrada Identificador de instrução.  
  
 *ValuePtrPtr*  
 Der Ponteiro para um buffer no qual retornar o endereço do buffer *ParameterValuePtr* especificado em **SQLBindParameter** (para dados de parâmetro) ou o endereço do buffer de *TargetValuePtr* especificado em **SQLBindCol** (para dados de coluna), conforme contido no campo de registro de descritor de SQL_DESC_DATA_PTR.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR, SQL_INVALID_HANDLE ou SQL_PARAM_DATA_AVAILABLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLParamData** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *identificador* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLParamData** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|DESCRIÇÃO|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|07006|Violação de atributo de tipo de dados restrito|O valor de dados identificado pelo argumento *ValueType* em **SQLBindParameter** para o parâmetro associado não pôde ser convertido para o tipo de dados identificado pelo argumento *ParameterType* em **SQLBindParameter**.<br /><br /> O valor de dados retornado para um parâmetro associado como SQL_PARAM_INPUT_OUTPUT ou SQL_PARAM_OUTPUT não pôde ser convertido para o tipo de dados identificado pelo argumento *ValueType* em **SQLBindParameter**.<br /><br /> (Se os valores de dados de uma ou mais linhas não puderem ser convertidos, mas uma ou mais linhas tiverem sido retornadas com êxito, essa função retornará SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado falhou antes da função concluir o processamento.|  
|22026|Incompatibilidade de comprimento de dados String|O tipo de informação SQL_NEED_LONG_DATA_LEN em **SQLGetInfo** era "Y" e menos dados foram enviados para um parâmetro longo (o tipo de dados era SQL_LONGVARCHAR, SQL_LONGVARBINARY ou um tipo de dados específico da fonte de dados longa) do que foi especificado com o argumento *StrLen_or_IndPtr* em **SQLBindParameter**.<br /><br /> O tipo de informação SQL_NEED_LONG_DATA_LEN em **SQLGetInfo** era "Y" e menos dados foram enviados para uma coluna longa (o tipo de dados era SQL_LONGVARCHAR, SQL_LONGVARBINARY ou um tipo de dados específico da fonte de dados longa) do que foi especificado no buffer de comprimento correspondente a uma coluna em uma linha de dados que foi adicionada ou atualizada com **SQLBulkOperations** ou atualizada com **SQLSetPos**.|  
|40001|Falha de serialização|A transação foi revertida devido a um deadlock de recurso com outra transação.|  
|40003|Conclusão de instrução desconhecida|A conexão associada falhou durante a execução dessa função, e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \*MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*; a função foi então chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativo multithread.|  
|HY010|Erro de sequência de função|(DM) a chamada de função anterior não era uma chamada para **SQLExecDirect**, **SQLExecute**, **SQLBulkOperations**ou **SQLSetPos** em que o código de retorno foi SQL_NEED_DATA ou a chamada de função anterior era uma chamada para **SQLPutData**.<br /><br /> A chamada de função anterior era uma chamada para **SQLParamData**.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *StatementHandle*. Esta função assíncrona ainda estava em execução quando a função **SQLParamData** foi chamada.<br /><br /> (DM) uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado para *StatementHandle* e retornou SQL_NEED_DATA. **SQLCancel** foi chamado antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver que corresponde ao *StatementHandle* não oferece suporte à função.|  
|IM017|A sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação for usado, a sondagem será desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesse identificador.|Se a chamada de função anterior no identificador retornar SQL_STILL_EXECUTING e se o modo de notificação estiver habilitado, **SQLCompleteAsync** deverá ser chamado na alça para executar o pós-processamento e concluir a operação.|  
  
 Se **SQLParamData** for chamado durante o envio de dados para um parâmetro em uma instrução SQL, ele poderá retornar qualquer SQLSTATE que possa ser retornado pela função chamada para executar a instrução (**SQLExecute** ou **SQLExecDirect**). Se for chamado durante o envio de dados para uma coluna sendo atualizada ou adicionada com **SQLBulkOperations** ou atualizada com **SQLSetPos**, ela poderá retornar qualquer SQLSTATE que possa ser retornado por **SQLBulkOperations** ou **SQLSetPos**.  
  
## <a name="comments"></a>Comentários  
 **SQLParamData** pode ser chamado para fornecer dados em execução para dois usos: dados de parâmetro que serão usados em uma chamada para **SQLExecute** ou **SQLExecDirect**, ou dados de coluna que serão usados quando uma linha for atualizada ou adicionada por uma chamada para **SQLBulkOperations** ou atualizada por uma chamada para **SQLSetPos**. No momento da execução, **SQLParamData** retorna ao aplicativo um indicador de quais dados o driver requer.  
  
 Quando um aplicativo chama **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos**, o driver retorna SQL_NEED_DATA se precisar de dados de dados em execução. Em seguida, um aplicativo chama **SQLParamData** para determinar quais dados enviar. Se o driver exigir dados de parâmetro, o driver retornará no buffer de saída * \*ValuePtrPtr* o valor que o aplicativo colocou no buffer do conjunto de linhas. O aplicativo pode usar esse valor para determinar quais dados de parâmetro o driver está solicitando. Se o driver exigir dados de coluna, o driver retornará no buffer * \*ValuePtrPtr* o endereço ao qual a coluna foi vinculada originalmente, da seguinte maneira:  
  
 *Limite* + de*Associação* de endereço associado + ((*número da linha* -1) x tamanho do *elemento*)  
  
 onde as variáveis são definidas conforme indicado na tabela a seguir.  
  
|Variável|DESCRIÇÃO|  
|--------------|-----------------|  
|*Endereço associado*|O endereço especificado com o argumento *TargetValuePtr* em **SQLBindCol**.|  
|*Deslocamento de associação*|O valor armazenado no endereço especificado com o atributo de instrução SQL_ATTR_ROW_BIND_OFFSET_PTR.|  
|*Row Number*|O número de base 1 da linha no conjunto de linhas. Para buscas de linha única, que são o padrão, isso é 1.|  
|*Tamanho do elemento*|O valor do atributo de instrução SQL_ATTR_ROW_BIND_TYPE para os buffers de dados e de comprimento/indicador.|  
  
 Ele também retorna SQL_NEED_DATA, que é um indicador para o aplicativo que ele deve chamar **SQLPutData** para enviar os dados.  
  
 O aplicativo chama **SQLPutData** quantas vezes forem necessárias para enviar os dados em execução para a coluna ou o parâmetro. Depois que todos os dados forem enviados para a coluna ou parâmetro, o aplicativo chamará **SQLParamData** novamente. Se **SQLParamData** retornar novamente SQL_NEED_DATA, os dados deverão ser enviados para outro parâmetro ou coluna. Portanto, o aplicativo novamente chama **SQLPutData**. Se todos os dados em execução forem enviados para todos os parâmetros ou colunas, **SQLParamData** retornará SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, o valor em * \*ValuePtrPtr* será indefinido e a instrução SQL poderá ser executada, ou a chamada **SQLBulkOperations** ou **SQLSetPos** poderá ser processada.  
  
 Se **SQLParamData** fornecer dados de parâmetro para uma instrução UPDATE ou DELETE pesquisada que não afete nenhuma linha na fonte de dados, a chamada para **SQLParamData** retornará SQL_NO_DATA.  
  
 Para obter mais informações sobre como os dados de parâmetro de dados em execução são passados no momento da execução da instrução, consulte "passando valores de parâmetro" em [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) e [enviando dados longos](../../../odbc/reference/develop-app/sending-long-data.md). Para obter mais informações sobre como os dados de coluna de dados em execução são atualizados ou adicionados, consulte a seção "usando SQLSetPos" em [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md), "executando atualizações em massa usando indicadores" em [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)e [Long data e SQLSetPos e SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
 **SQLParamData** pode ser chamado para recuperar parâmetros de saída transmitidos. Quando **SQLMoreResults**, **SQLExecute**, **SQLGetData**ou **SQLExecDirect** retorna SQL_PARAM_DATA_AVAILABLE, chame **SQLParamData** para determinar qual parâmetro tem um valor disponível. Para obter mais informações sobre SQL_PARAM_DATA_AVAILABLE e parâmetros de saída em fluxo, consulte [recuperando parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="code-example"></a>Exemplo de código  
 Consulte [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Associando um buffer a um parâmetro|[Função SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Retornando informações sobre um parâmetro em uma instrução|[Função SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|Executando uma instrução SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executando uma instrução SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Enviando dados de parâmetro em tempo de execução|[Função SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recuperar parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
