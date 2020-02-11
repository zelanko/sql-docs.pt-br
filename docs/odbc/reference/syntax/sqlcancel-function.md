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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 94f823cdefe4b3e5a62beb62062356dad3a88a03
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036120"
---
# <a name="sqlcancel-function"></a>Função SQLCancel
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: ISO 92  
  
 **Resumo**  
 **SQLCancel** cancela o processamento em uma instrução.  
  
 Para cancelar o processamento em uma conexão ou instrução, use a [função SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLCancel(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 Entrada Identificador de instrução.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLCancel** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *identificador* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLCancel** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|DESCRIÇÃO|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) no argumento * \*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *StatementHandle*. Esta função assíncrona ainda estava em execução quando a função **SQLCancel** foi chamada.<br /><br /> (DM) falha na operação de cancelamento porque uma operação assíncrona está em andamento em um identificador de conexão associado a *StatementHandle*.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY018|Solicitação de cancelamento do servidor recusada|O servidor recusou a solicitação de cancelamento.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *StatementHandle* não oferece suporte à função.|  
  
## <a name="comments"></a>Comentários  
 **SQLCancel** pode cancelar os seguintes tipos de processamento em uma instrução:  
  
-   Uma função executada de forma assíncrona na instrução.  
  
-   Uma função em uma instrução que precisa de dados.  
  
-   Uma função em execução na instrução em outro thread.  
  
 No ODBC 2. *x*, se um aplicativo chamar **SQLCancel** quando nenhum processamento estiver sendo feito na instrução, **SQLCancel** terá o mesmo efeito que **SQLFreeStmt** com a opção SQL_CLOSE; Esse comportamento é definido apenas para fins de integridade e os aplicativos devem chamar **SQLFreeStmt** ou **SQLCloseCursor** para fechar cursores.  
  
 Quando **SQLCancel** é chamado para cancelar uma função que é executada de forma assíncrona em uma instrução ou em uma função em uma instrução que precisa de dados, os registros de diagnóstico postados pela função que está sendo cancelada são limpos e o **SQLCancel** envia seus próprios registros de diagnóstico; Quando **SQLCancel** é chamado para cancelar uma função em execução em uma instrução em outro thread, no entanto, ele não limpa os registros de diagnóstico da função que está sendo cancelada e não publica seus próprios registros de diagnóstico.  
  
## <a name="canceling-asynchronous-processing"></a>Cancelando o processamento assíncrono  
 Depois que um aplicativo chama uma função de forma assíncrona, ele chama a função repetidamente para determinar se ele concluiu o processamento. Se a função ainda estiver sendo processada, ela retornará SQL_STILL_EXECUTING. Se a função tiver terminado o processamento, ela retornará um código diferente.  
  
 Depois de qualquer chamada para a função que retorna SQL_STILL_EXECUTING, um aplicativo pode chamar **SQLCancel** para cancelar a função. Se a solicitação de cancelamento for bem-sucedida, o driver retornará SQL_SUCCESS. Essa mensagem não indica que a função foi realmente cancelada; Isso indica que a solicitação de cancelamento foi processada. Quando ou se a função for realmente cancelada, depende do driver e da fonte de dados. O aplicativo deve continuar a chamar a função original até que o código de retorno não seja SQL_STILL_EXECUTING. Se a função foi cancelada com êxito, o código de retorno será SQL_ERROR e SQLSTATE HY008 (operação cancelada). Se a função tiver concluído seu processamento normal, o código de retorno será SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO se a função tiver êxito ou SQL_ERROR e um SQLSTATE diferente de HY008 (operação cancelada) se a função falhar.  
  
> [!NOTE]  
>  No ODBC 3,5, uma chamada para **SQLCancel** quando nenhum processamento está sendo feito na instrução não é tratada como **SQLFreeStmt** com a opção SQL_CLOSE, mas não tem nenhum efeito. Para fechar um cursor, um aplicativo deve chamar **SQLCloseCursor**, e não **SQLCancel**.  
  
 Para obter mais informações sobre o processamento assíncrono, consulte [execução assíncrona](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md).  
  
## <a name="canceling-functions-that-need-data"></a>Cancelando funções que precisam de dados  
 Depois que **SQLExecute** ou **SQLExecDirect** retorna SQL_NEED_DATA e antes de os dados serem enviados para todos os parâmetros de dados em execução, um aplicativo pode chamar **SQLCancel** para cancelar a execução da instrução. Depois que a instrução for cancelada, o aplicativo poderá chamar **SQLExecute** ou **SQLExecDirect** novamente. Para obter mais informações, consulte [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md).  
  
 Depois que **SQLBulkOperations** ou **SQLSetPos** retorna SQL_NEED_DATA e antes de os dados serem enviados para todas as colunas de dados em execução, um aplicativo pode chamar **SQLCancel** para cancelar a operação. Depois que a operação for cancelada, o aplicativo poderá chamar **SQLBulkOperations** ou **SQLSetPos** novamente; o cancelamento não afeta o estado do cursor nem a posição atual do cursor. Para obter mais informações, consulte [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md) ou [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
## <a name="canceling-functions-executing-on-another-thread"></a>Cancelando funções em execução em outro thread  
 Em um aplicativo multithread, o aplicativo pode cancelar uma função que está sendo executada em outro thread. Para cancelar a função, o aplicativo chama **SQLCancel** com o mesmo identificador de instrução usado pela função de destino, mas em um thread diferente. A forma como a função é cancelada depende do driver e do sistema operacional. Como no cancelamento de uma função em execução assíncrona, o código de retorno de **SQLCancel** indica apenas se o driver processou a solicitação com êxito. Somente SQL_SUCCESS ou SQL_ERROR podem ser retornados; nenhuma informação de diagnóstico é retornada. Se a função original for cancelada, ela retornará SQL_ERROR e SQLSTATE HY008 (operação cancelada).  
  
 Se uma instrução SQL estiver sendo executada quando **SQLCancel** for chamado em outro thread para cancelar a execução da instrução, será possível que a execução seja bem-sucedida e retorne SQL_SUCCESS enquanto o cancelamento também for bem-sucedido. Nesse caso, o Gerenciador de driver assume que o cursor aberto pela execução da instrução é fechado pelo cancelamento, de modo que o aplicativo não poderá usar o cursor.  
  
 Para obter mais informações sobre Threading, consulte [multithreading](../../../odbc/reference/develop-app/multithreading.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Associando um buffer a um parâmetro|[Função SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Executando operações de inserção ou atualização em massa|[Função SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Cancela uma função que executa de forma assíncrona em um identificador de conexão, além da funcionalidade de **SQLCancel**.|[Função SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|Executando uma instrução SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executando uma instrução SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Liberando um identificador de instrução|[SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Obtendo um campo de um registro de diagnóstico ou um campo do cabeçalho de diagnóstico|[Função SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
|Obtendo vários campos de uma estrutura de dados de diagnóstico|[Função SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|  
|Retornando o próximo parâmetro para o qual enviar dados|[Função SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|Enviando dados de parâmetro em tempo de execução|[Função SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|Posicionando o cursor em um conjunto de linhas, atualizando dados no conjunto de linhas ou atualizando ou excluindo dados no conjunto de resultados|[Função SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
