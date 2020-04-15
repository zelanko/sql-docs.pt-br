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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8ed149e125e3231d670c6ddbd4569ff5ccee5c15
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306917"
---
# <a name="sqlparamdata-function"></a>Função SQLParamData
**Conformidade**  
 Versão introduzida: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **O SQLParamData** é usado em conjunto com **o SQLPutData** para fornecer dados de parâmetros no tempo de execução da declaração e com **o SQLGetData** para recuperar dados de parâmetros de saída transmitidos.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLParamData(  
     SQLHSTMT       StatementHandle,  
     SQLPOINTER *   ValuePtrPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Alça de declaração.  
  
 *ValuePtrPtr*  
 [Saída] Pointer para um buffer no qual retornar o endereço do buffer *ParameterValuePtr* especificado no **SQLBindParameter** (para dados de parâmetros) ou no endereço do buffer *TargetValuePtr* especificado no **SQLBindCol** (para dados da coluna), conforme contido no campo de registro de descritor SQL_DESC_DATA_PTR.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_NO_DATA SQL_STILL_EXECUTING, SQL_ERROR, SQL_INVALID_HANDLE ou SQL_PARAM_DATA_AVAILABLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLParamData** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **sqlGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *alça* de *statementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLParamData** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|07006|Violação de atributo de tipo de dados restrito|O valor de dados identificado pelo argumento *ValueType* no **SQLBindParameter** para o parâmetro bound não pôde ser convertido para o tipo de dados identificado pelo argumento *ParameterType* no **SQLBindParameter**.<br /><br /> O valor dos dados retornado para um parâmetro vinculado à SQL_PARAM_INPUT_OUTPUT ou SQL_PARAM_OUTPUT não pôde ser convertido para o tipo de dados identificado pelo argumento *ValueType* no **SQLBindParameter**.<br /><br /> (Se os valores de dados de uma ou mais linhas não pudessem ser convertidos, mas uma ou mais linhas fossem devolvidas com sucesso, essa função retornará SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados à qual o driver estava conectado falhou antes da função ser concluída.|  
|22026|Incompatibilidade de comprimento de dados String|O SQL_NEED_LONG_DATA_LEN tipo de informação no **SQLGetInfo** era "Y", e menos dados foram enviados para um parâmetro longo (o tipo de dados foi SQL_LONGVARCHAR, SQL_LONGVARBINARY ou um tipo de dados específico de origem de dados longo) do que foi especificado com o *argumento StrLen_or_IndPtr* no **SQLBindParameter**.<br /><br /> O SQL_NEED_LONG_DATA_LEN tipo de informação no **SQLGetInfo** era "Y", e menos dados foram enviados para uma coluna longa (o tipo de dados era SQL_LONGVARCHAR, SQL_LONGVARBINARY ou um tipo de dados específico de origem de dados longo) do que foi especificado no buffer de comprimento correspondente a uma coluna em uma linha de dados que foi adicionado ou atualizado com **SQLBulkOperations** ou atualizado com **SQLSetPos**.|  
|40001|Falha na serialização|A transação foi revertida por causa de um impasse de recursos com outra transação.|  
|40003|Conclusão de declaração desconhecida|A conexão associada falhou durante a execução desta função, e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar memória necessária para suportar a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e, antes de concluir a execução, **sqlcancelou** ou **SQLCancelHandle** foi chamado no *StatementHandle*; a função foi então chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **sqlCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um segmento diferente em um aplicativo multithread.|  
|HY010|Erro de seqüência de função|(DM) A chamada de função anterior não era uma chamada para **SQLExecDirect,** **SQLExecute,** **SQLBulkOperations**ou **SQLSetPos** onde o código de retorno foi SQL_NEED_DATA, ou a chamada de função anterior era uma chamada para **SQLPutData**.<br /><br /> A chamada de função anterior era uma chamada para **SQLParamData**.<br /><br /> (DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *StatementHandle*. Esta função assíncrona ainda estava sendo executada quando a função **SQLParamData** foi chamada.<br /><br /> (DM) Uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava sendo executada quando esta função foi chamada.<br /><br /> **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados para o *StatementHandle* e retornaram SQL_NEED_DATA. **O SQLCancel** foi chamado antes do enviar dados para todos os parâmetros ou colunas de execução de dados.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver que corresponde ao *StatementHandle* não suporta a função.|  
|IM017|A votação é desativada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a votação é desativada.|  
|IM018|**O SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesta alça.|Se a chamada de função anterior na alça retornar SQL_STILL_EXECUTING e se o modo de notificação estiver ativado, o **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
 Se **o SQLParamData** for chamado enquanto envia dados para um parâmetro em uma declaração SQL, ele poderá retornar qualquer SQLSTATE que possa ser retornado pela função chamada para executar a declaração **(SQLExecute** ou **SQLExecDirect).** Se for chamado durante o envio de dados para uma coluna que está sendo atualizada ou adicionada com **sqlBulkOperations** ou sendo atualizada com **SQLSetPos,** ela pode retornar qualquer SQLSTATE que possa ser retornado por **SQLBulkOperations** ou **SQLSetPos**.  
  
## <a name="comments"></a>Comentários  
 **O SQLParamData** pode ser chamado para fornecer dados em execução para dois usos: dados de parâmetros que serão usados em uma chamada para **SQLExecute** ou **SQLExecDirect**, ou dados de coluna que serão usados quando uma linha for atualizada ou adicionada por uma chamada para **SQLBulkOperations** ou atualizada por uma chamada para **SQLSetPos**. No momento da execução, **o SQLParamData** retorna ao aplicativo um indicador de quais dados o driver requer.  
  
 Quando um aplicativo chama **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos,** o driver retorna SQL_NEED_DATA se precisar de dados em execução. Um aplicativo então chama **SQLParamData** para determinar quais dados enviar. Se o driver exigir dados de parâmetros, o driver retorna no buffer de saída * \*ValuePtrPtr* o valor que o aplicativo colocar no buffer de conjunto de linhas. O aplicativo pode usar esse valor para determinar quais parâmetros o driver está solicitando. Se o driver precisar de dados da coluna, o driver retorna no buffer * \*ValuePtrPtr* o endereço ao que a coluna estava originalmente vinculada, da seguinte forma:  
  
 *Bound Address* + *Deslocamento de vinculação do* endereço vinculado + ((número*da linha* - 1) x tamanho *do elemento*)  
  
 onde as variáveis são definidas conforme indicado na tabela a seguir.  
  
|Variável|Descrição|  
|--------------|-----------------|  
|*Endereço vinculado*|O endereço especificado com o argumento *TargetValuePtr* no **SQLBindCol**.|  
|*Deslocamento de vinculação*|O valor armazenado no endereço especificado com o atributo de declaração SQL_ATTR_ROW_BIND_OFFSET_PTR.|  
|*Row Number*|O número baseado em 1 da linha no conjunto de linhas. Para buscas de linha única, que são o padrão, este é 1.|  
|*Tamanho do elemento*|O valor do atributo de declaração SQL_ATTR_ROW_BIND_TYPE para os buffers de comprimento/indicador de comprimento/comprimento.|  
  
 Ele também retorna SQL_NEED_DATA, que é um indicador para o aplicativo que ele deve chamar **SQLPutData** para enviar os dados.  
  
 O aplicativo chama **SQLPutData** quantas vezes for necessário para enviar os dados em execução para a coluna ou parâmetro. Depois que todos os dados foram enviados para a coluna ou parâmetro, o aplicativo chama **SQLParamData** novamente. Se **o SQLParamData** retornar novamente SQL_NEED_DATA, os dados devem ser enviados para outro parâmetro ou coluna. Portanto, o aplicativo novamente chama **SQLPutData**. Se todos os dados em execução forem enviados para todos os parâmetros ou colunas, o **SQLParamData** retorna SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, o valor no * \*ValuePtrPtr* é indefinido e a declaração SQL pode ser executada ou a chamada **SQLBulkOperations** ou **SQLSetPos** pode ser processada.  
  
 Se **o SQLParamData** fornecer dados de parâmetros para uma atualização pesquisada ou excluir uma declaração que não afete nenhuma linha na fonte de dados, a chamada para **SQLParamData** retorna SQL_NO_DATA.  
  
 Para obter mais informações sobre como os dados dos parâmetros de execução são passados no momento da execução da declaração, consulte "Valores de parâmetro de passagem" no [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) e [no envio de dados longos](../../../odbc/reference/develop-app/sending-long-data.md). Para obter mais informações sobre como os dados da coluna de execução são atualizados ou adicionados, consulte a seção "Usando SQLSetPos" em [SQLSetPos,](../../../odbc/reference/syntax/sqlsetpos-function.md)"Realizando atualizações em massa usando marcadores" em [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)e [Long Data e SQLSetPos e SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
 **SQLParamData** pode ser chamado para recuperar parâmetros de saída streamed. Quando **SQLMoreResults,** **SQLExecute,** **SQLGetData**ou **SQLExecDirect retornar** SQL_PARAM_DATA_AVAILABLE, ligue para **o SQLParamData** para determinar qual parâmetro tem um valor disponível. Para obter mais informações sobre SQL_PARAM_DATA_AVAILABLE e parâmetros de saída transmitidos, consulte [Recuperando parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="code-example"></a>Exemplo de código  
 Consulte [SqlputData](../../../odbc/reference/syntax/sqlputdata-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Vinculando um buffer a um parâmetro|[Função SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Cancelamento do processamento de declarações|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Retornando informações sobre um parâmetro em uma declaração|[Função SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|Executando uma declaração SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executando uma declaração SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Envio de dados de parâmetros na hora da execução|[Função SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recuperar parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
