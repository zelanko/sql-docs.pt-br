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
manager: craigg
ms.openlocfilehash: b9d0c756db7f84e6bcec46a61ef805f885f39d28
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63258867"
---
# <a name="sqlcancel-function"></a>Função SQLCancel
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 1.0 ODBC: ISO 92  
  
 **Resumo**  
 **SQLCancel** cancela o processamento em uma instrução.  
  
 Para cancelar o processamento em uma conexão ou instrução, use [função SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLCancel(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrução.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLCancel** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL _ HANDLE_STMT e uma *manipular* dos *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLCancel** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) no argumento  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando o **SQLCancel** função foi chamada.<br /><br /> (DM) cancelar a operação falhou porque uma operação assíncrona está em andamento em um identificador de conexão que está associado com *StatementHandle*.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY018|O servidor recusada Cancelar solicitação|O servidor recusou a solicitação de cancelamento.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|O driver em (DM) associado a *StatementHandle* não suporta a função.|  
  
## <a name="comments"></a>Comentários  
 **SQLCancel** pode cancelar os seguintes tipos de processamento em uma instrução:  
  
-   Uma função em execução assíncrona na instrução.  
  
-   Uma função em uma instrução que precisa de dados.  
  
-   Uma função em execução na instrução em outro thread.  
  
 No ODBC 2. *x*, se um aplicativo chama **SQLCancel** quando nenhum processamentos estiver sendo feito na instrução, **SQLCancel** tem o mesmo efeito que **SQLFreeStmt** com a opção SQL_CLOSE. Esse comportamento é definido apenas para fins de integridade e os aplicativos devem chamar **SQLFreeStmt** ou **SQLCloseCursor** para fechar cursores.  
  
 Quando **SQLCancel** é chamado para cancelar uma função em execução em uma instrução ou uma função de forma assíncrona em uma instrução que as necessidades de dados, registros de diagnóstico lançados pela função que está sendo cancelada são removidos, e **SQLCancel**  posta seus próprios registros de diagnóstico; quando **SQLCancel** é chamado para cancelar uma função em execução em uma instrução em outro thread, no entanto, ele não limpa o diagnóstico registros do que está sendo cancelada não função e não Poste seus próprios registros de diagnóstico.  
  
## <a name="canceling-asynchronous-processing"></a>Cancelamento de processamento assíncrono  
 Depois que um aplicativo chama uma função de forma assíncrona, ela chama a função repetidamente para determinar se ele concluiu o processamento. Se a função ainda está processando, ele retornará SQL_STILL_EXECUTING. Se a função de conclusão do processamento, ela retornará um código diferente.  
  
 Após qualquer chamada para a função que retorna SQL_STILL_EXECUTING, um aplicativo pode chamar **SQLCancel** para cancelar a função. Se a solicitação de cancelamento for bem-sucedida, o driver retornará SQL_SUCCESS. Esta mensagem não indica que a função, na verdade, foi cancelada; ele indica que a solicitação de cancelamento foi processada. Quando ou se a função será cancelada, na verdade, é dependente do driver e dependente da fonte de dados. O aplicativo deve continuar a chamar a função original até que o código de retorno não seja SQL_STILL_EXECUTING. Se a função foi cancelada com êxito, o código de retorno é SQL_ERROR e SQLSTATE HY008 (operação cancelada). Se a função concluir seu processamento normal, o código de retorno é SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO se a função foi bem-sucedida ou SQL_ERROR e um SQLSTATE diferente HY008 (operação cancelada) se a função falhou.  
  
> [!NOTE]  
>  No ODBC 3.5, uma chamada para **SQLCancel** quando nenhum processamentos estiver sendo feito na instrução não é tratado como **SQLFreeStmt** com a opção SQL_CLOSE, mas tem não é nenhum efeito em todos os. Para fechar um cursor, um aplicativo deve chamar **SQLCloseCursor**, e não **SQLCancel**.  
  
 Para obter mais informações sobre o processamento assíncrono, consulte [execução assíncrona](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md).  
  
## <a name="canceling-functions-that-need-data"></a>Cancelando a funções que precisam de dados  
 Após **SQLExecute** ou **SQLExecDirect** retorna SQL_NEED_DATA e antes de dados tem sido enviados para todos os parâmetros de dados em execução, um aplicativo pode chamar **SQLCancel** Para cancelar a execução da instrução. Depois que a instrução foi cancelada, o aplicativo pode chamar **SQLExecute** ou **SQLExecDirect** novamente. Para obter mais informações, consulte [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md).  
  
 Após **SQLBulkOperations** ou **SQLSetPos** retorna SQL_NEED_DATA e antes de dados tem sido enviados para todas as colunas de dados em execução, um aplicativo pode chamar **SQLCancel** Para cancelar a operação. Depois que a operação foi cancelada, o aplicativo pode chamar **SQLBulkOperations** ou **SQLSetPos** novamente; o cancelamento não afeta o estado de cursor ou a posição atual do cursor. Para obter mais informações, consulte [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md) ou [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
## <a name="canceling-functions-executing-on-another-thread"></a>Cancelando a funções em execução em outro Thread  
 Em um aplicativo multithread, o aplicativo pode cancelar uma função que está em execução em outro thread. Para cancelar a função, o aplicativo chama **SQLCancel** com o mesmo identificador de instrução que o usado pela função de destino, mas em um thread diferente. Como a função seja cancelada depende do driver e o sistema operacional. Como no cancelamento de uma função em execução assincronamente, o código de retorno de **SQLCancel** indica somente se o driver processa a solicitação com êxito. Somente SQL_SUCCESS ou SQL_ERROR podem ser retornados; Não há informações de diagnóstico serão retornadas. Se a função original é cancelada, ele retornará SQL_ERROR e SQLSTATE HY008 (operação cancelada).  
  
 Se uma instrução SQL está sendo executado quando **SQLCancel** é chamado em outro thread para cancelar a execução da instrução, é possível que a execução seja bem-sucedida e retorno SQL_SUCCESS durante o cancelamento também é bem-sucedida. Nesse caso, o Gerenciador de Driver pressupõe que o cursor aberto pela execução da instrução está fechado por cancelar, portanto, o aplicativo não poderá usar o cursor.  
  
 Para obter mais informações sobre threading, consulte [Multithreading](../../../odbc/reference/develop-app/multithreading.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Um buffer de associação a um parâmetro|[Função SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Em massa executando operações inserir ou atualizar|[Função SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Cancela uma função executando de maneira assíncrona em um identificador de conexão, além da funcionalidade do **SQLCancel**.|[Função SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|Executar uma instrução SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executar uma instrução SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Liberando um identificador de instrução|[SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Obtendo um campo de um registro de diagnóstico ou um campo do cabeçalho de diagnóstico|[Função SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
|Como obter vários campos de uma estrutura de dados de diagnóstico|[Função SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|  
|Retornar o próximo parâmetro para enviar dados|[Função SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|Enviar dados de parâmetro em tempo de execução|[Função SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|Posicionando o cursor em um conjunto de linhas, a atualização de dados no conjunto de linhas, ou a atualização ou exclusão de dados no conjunto de resultados|[Função SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
