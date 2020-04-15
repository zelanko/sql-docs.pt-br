---
title: Função SQLCancel | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCancel
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLCancel
helpviewer_keywords:
- SQLCancel function [ODBC]
ms.assetid: ac0b5972-627f-4440-8c5a-0e8da728726d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fcc2afce495a1481692ba1f20162a2df5d9a9458
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301306"
---
# <a name="sqlcancel-function"></a>Função SQLCancel
**Conformidade**  
 Versão introduzida: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **O SQLCancel** cancela o processamento em uma declaração.  
  
 Para cancelar o processamento em uma conexão ou declaração, use [a função SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLCancel(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Alça de declaração.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLCancel** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *alça* de *statementHandle*. A tabela a seguir lista os valores SQLSTATE comumente retornados pelo **SQLCancel** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) no argumento * \*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY010|Erro de seqüência de função|(DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *StatementHandle*. Esta função assíncrona ainda estava sendo executada quando a função **SQLCancel** foi chamada.<br /><br /> (DM) A operação de cancelamento falhou porque uma operação assíncrona está em andamento em uma alça de conexão associada ao *StatementHandle*.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY018|Servidor recusou pedido de cancelamento|O servidor recusou o pedido de cancelamento.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *StatementHandle* não suporta a função.|  
  
## <a name="comments"></a>Comentários  
 **O SQLCancel** pode cancelar os seguintes tipos de processamento em uma declaração:  
  
-   Uma função em execução assíncrona na declaração.  
  
-   Uma função em uma declaração que precisa de dados.  
  
-   Uma função em execução na declaração em outro segmento.  
  
 Em ODBC 2. *x*, se um aplicativo chamar **SQLCancel** quando nenhum processamento está sendo feito na declaração, o **SQLCancel** tem o mesmo efeito que **o SQLFreeStmt** com a opção SQL_CLOSE; esse comportamento é definido apenas para completude e os aplicativos devem chamar **SQLFreeStmt** ou **SQLCloseCursor** para fechar cursores.  
  
 Quando **o SQLCancel** é chamado a cancelar uma função em execução assíncrona em uma declaração ou uma função em uma declaração que precisa de dados, registros de diagnóstico publicados pela função que está sendo cancelada são apagados e **o SQLCancel** publica seus próprios registros de diagnóstico; quando **o SQLCancel** é chamado a cancelar uma função em execução em uma declaração em outro segmento, no entanto, ele não limpa os registros de diagnóstico da função sendo cancelada e não publica seus próprios registros de diagnóstico.  
  
## <a name="canceling-asynchronous-processing"></a>Cancelando o Processamento Assíncrono  
 Depois que um aplicativo chama uma função assíncronamente, ele chama a função repetidamente para determinar se ele terminou o processamento. Se a função ainda estiver em processo, ela retorna SQL_STILL_EXECUTING. Se a função tiver concluído o processamento, ela retorna um código diferente.  
  
 Após qualquer chamada para a função que retorna SQL_STILL_EXECUTING, um aplicativo pode ligar para **o SQLCancel** para cancelar a função. Se a solicitação de cancelamento for bem sucedida, o motorista retorna SQL_SUCCESS. Esta mensagem não indica que a função foi realmente cancelada; indica que o pedido de cancelamento foi processado. Quando ou se a função for realmente cancelada é dependente do driver e dependente da fonte de dados. O aplicativo deve continuar a chamar a função original até que o código de retorno não seja SQL_STILL_EXECUTING. Se a função foi cancelada com sucesso, o código de devolução será SQL_ERROR e SQLSTATE HY008 (Operação cancelada). Se a função completou seu processamento normal, o código de retorno será SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO se a função tiver êxito ou SQL_ERROR e um SQLSTATE diferente do HY008 (Operação cancelada) se a função falhar.  
  
> [!NOTE]  
>  No ODBC 3.5, uma chamada para **sqlcancel** quando nenhum processamento está sendo feito na declaração não é tratada como **SQLFreeStmt** com a opção SQL_CLOSE, mas não tem nenhum efeito. Para fechar um cursor, um aplicativo deve chamar **SQLCloseCursor**, não **SQLCancel**.  
  
 Para obter mais informações sobre processamento assíncrono, consulte [Execução Assíncrona](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md).  
  
## <a name="canceling-functions-that-need-data"></a>Cancelando funções que precisam de dados  
 Depois **que SQLExecute** ou **SQLExecDirect** retornar SQL_NEED_DATA e antes que os dados sejam enviados para todos os parâmetros de execução de dados, um aplicativo pode chamar **o SQLCancel** para cancelar a execução da declaração. Depois que a declaração foi cancelada, o aplicativo pode chamar **SQLExecute** ou **SQLExecDirect** novamente. Para obter mais informações, consulte [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md).  
  
 Depois **que sqlBulkOperations** ou **SQLSetPos** retornar SQL_NEED_DATA e antes que os dados sejam enviados para todas as colunas de dados em execução, um aplicativo pode chamar **o SQLCancel** para cancelar a operação. Depois que a operação foi cancelada, o aplicativo pode chamar **SQLBulkOperations** ou **SQLSetPos** novamente; o cancelamento não afeta o estado do cursor ou a posição atual do cursor. Para obter mais informações, consulte [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md) ou [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
## <a name="canceling-functions-executing-on-another-thread"></a>Cancelando funções executando em outro segmento  
 Em um aplicativo multithread, o aplicativo pode cancelar uma função que está sendo executado em outro segmento. Para cancelar a função, o aplicativo chama **SQLCancel** com o mesmo cabo de declaração usado pela função de destino, mas em um segmento diferente. Como a função é cancelada depende do driver e do sistema operacional. Como ao cancelar uma função em execução assíncrona, o código de retorno do **SQLCancel** indica apenas se o driver processou a solicitação com sucesso. Apenas SQL_SUCCESS ou SQL_ERROR podem ser devolvidos; nenhuma informação de diagnóstico é devolvida. Se a função original for cancelada, ela retorna SQL_ERROR e SQLSTATE HY008 (Operação cancelada).  
  
 Se uma declaração SQL estiver sendo executada quando o **SQLCancel** for chamado por outro segmento para cancelar a execução da declaração, é possível que a execução tenha sucesso e retorne SQL_SUCCESS enquanto o cancelamento também for bem sucedido. Neste caso, o Driver Manager assume que o cursor aberto pela execução da declaração é fechado pelo cancelamento, de modo que o aplicativo não poderá usar o cursor.  
  
 Para obter mais informações sobre threading, consulte [Multithreading](../../../odbc/reference/develop-app/multithreading.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Vinculando um buffer a um parâmetro|[Função SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Realizando operações de inserção ou atualização em massa|[Função SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Cancela uma função em execução assíncrona em uma alça de conexão, além da funcionalidade do **SQLCancel**.|[Função SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|Executando uma declaração SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executando uma declaração SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Liberando uma alça de declaração|[SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Obtenção de um campo de um registro de diagnóstico ou um campo do cabeçalho de diagnóstico|[Função SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
|Obtenção de múltiplos campos de uma estrutura de dados diagnósticos|[Função SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|  
|Retornando o próximo parâmetro para enviar dados para|[Função SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|Envio de dados de parâmetros na hora da execução|[Função SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|Posicionando o cursor em um conjunto de linhas, atualizando dados no conjunto de linhas ou atualizando ou excluindo dados no conjunto de resultados|[Função SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
