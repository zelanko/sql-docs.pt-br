---
description: Função SQLEndTran
title: Função SQLEndTran | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLEndTran
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLEndTran
helpviewer_keywords:
- SQLEndTran function [ODBC]
ms.assetid: ff375ce1-eb50-4693-b1e6-70181a6dbf9f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fea27beb03c19dd9499175678ecfdcb7759a73f4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461126"
---
# <a name="sqlendtran-function"></a>Função SQLEndTran
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 3,0: ISO 92  
  
 **Resumo**  
 **SQLEndTran** solicita uma operação de confirmação ou reversão para todas as operações ativas em todas as instruções associadas a uma conexão. O **SQLEndTran** também pode solicitar que uma operação de confirmação ou reversão seja executada para todas as conexões associadas a um ambiente.  
  
> [!NOTE]  
>  Para obter mais informações sobre como o Gerenciador de driver mapeia essa função quando um ODBC 3. o aplicativo *x* está funcionando com um ODBC 2. Driver *x* , consulte [mapeando funções de substituição para compatibilidade com versões anteriores de aplicativos](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLEndTran(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle,  
     SQLSMALLINT   CompletionType);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HandleType*  
 Entrada Identificador de tipo de identificador. Contém SQL_HANDLE_ENV (se o *identificador* for um identificador de ambiente) ou SQL_HANDLE_DBC (se o *identificador* for um identificador de conexão).  
  
 *Handle*  
 Entrada O identificador do tipo indicado por *HandleType*, que indica o escopo da transação. Consulte "Comentários" para obter mais informações.  
  
 *Complettype*  
 Entrada Um dos dois valores a seguir:  
  
 SQL_COMMIT SQL_ROLLBACK  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE ou SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLEndTran** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com o *identificador* e *identificador*apropriados. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLEndTran** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|08003|Conexão não aberta|(DM) o *identificadortype* foi SQL_HANDLE_DBC e o *identificador* não estava em um estado conectado.|  
|08007|Falha na conexão durante a transação|O *identificadortype* foi SQL_HANDLE_DBC, e a conexão associada ao *identificador* falhou durante a execução da função e não pode ser determinada se a **confirmação** ou **reversão** solicitada ocorreu antes da falha.|  
|25S01|Estado de transação desconhecido|Uma ou mais das conexões no *identificador* não puderam concluir a transação com o resultado especificado e o resultado é desconhecido.|  
|25S02|A transação ainda está ativa|O driver não pôde garantir que todo o trabalho na transação global pudesse ser concluído atomicamente e a transação ainda esteja ativa.|  
|25S03|A transação é revertida|O driver não pôde garantir que todo o trabalho na transação global pudesse ser concluído atomicamente, e todo o trabalho na transação ativa no *identificador* foi revertido.|  
|40001|Falha de serialização|A transação foi revertida devido a um deadlock de recurso com outra transação.|  
|40002|Violação de restrição de integridade|O *complettype* foi SQL_COMMIT e o compromisso das alterações causou a violação da restrição de integridade. Como resultado, a transação foi revertida.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \* szMessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *ConnectionHandle*. A função foi chamada e antes de concluir a execução da [função SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) foi chamada no *ConnectionHandle*. Em seguida, a função foi chamada novamente no *ConnectionHandle*.<br /><br /> A função foi chamada e antes de concluir a execução de **SQLCancelHandle** foi chamada no *ConnectionHandle* de um thread diferente em um aplicativo multithread.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para um identificador de instrução associado ao *ConnectionHandle* e ainda estava em execução quando **SQLEndTran** foi chamado.<br /><br /> (DM) uma função de execução assíncrona (não esta) foi chamada para o *ConnectionHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado para um identificador de instrução associado ao *ConnectionHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.<br /><br /> (DM) uma função de execução assíncrona (não esta) foi chamada para o *identificador* com *HandleType* definido como SQL_HANDLE_DBC e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para um dos identificadores de instrução associados a *Handle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.|  
|HY012|Código de operação de transação inválido|(DM) o valor especificado para o argumento *complettype* não era SQL_COMMIT nem SQL_ROLLBACK.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY092|Identificador de atributo/opção inválido|(DM) o valor especificado para o argumento *HandleType* nem SQL_HANDLE_ENV nem SQL_HANDLE_DBC.|  
|HY115|SQLEndTran não é permitido para um ambiente que contém uma conexão com execução de função assíncrona habilitada|O *identificadortype* (DM) não pode ser definido como SQL_HANDLE_ENV se a execução assíncrona de funções de conexão está habilitada para uma conexão no ambiente.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte a seção comentários deste tópico.|  
|HYC00|Recurso opcional não implementado|O driver ou a fonte de dados não oferece suporte à operação de **reversão** .|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *ConnectionHandle* não oferece suporte à função.|  
|IM017|A sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação for usado, a sondagem será desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesse identificador.|Se a chamada de função anterior no identificador retornar SQL_STILL_EXECUTING e se o modo de notificação estiver habilitado, **SQLCompleteAsync** deverá ser chamado na alça para executar o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 Para um ODBC 3. *x* Driver, se *handletype* for SQL_HANDLE_ENV e o *identificador* for um identificador de ambiente válido, o Gerenciador de driver chamará **SQLEndTran** em cada driver associado ao ambiente. O argumento *Handle* para a chamada para um driver será o identificador de ambiente do driver. Para um ODBC 2. *x* Driver, se *handletype* for SQL_HANDLE_ENV e *tratar* for um identificador de ambiente válido e houver várias conexões em um estado conectado nesse ambiente, o Gerenciador de driver chamará **SQLTransact** no driver uma vez para cada conexão em um estado conectado nesse ambiente. O argumento *Handle* em cada chamada será o identificador da conexão. Em ambos os casos, o driver tentará confirmar ou reverter transações, dependendo do valor de *complettype*, em todas as conexões que estão em um estado conectado nesse ambiente. As conexões que não estão ativas não afetam a transação.  
  
> [!NOTE]  
>  **SQLEndTran** não pode ser usado para confirmar ou reverter transações em um ambiente compartilhado. SQLSTATE HY092 (identificador de atributo/opção inválido) será retornado se **SQLEndTran** for chamado com identificador definido como *o identificador de* um ambiente compartilhado ou o identificador de uma conexão em um ambiente compartilhado.  
  
 O Gerenciador de driver retornará SQL_SUCCESS somente se receber SQL_SUCCESS para cada conexão. Se o Gerenciador de driver receber SQL_ERROR em uma ou mais conexões, ele retornará SQL_ERROR ao aplicativo e as informações de diagnóstico serão colocadas na estrutura de dados de diagnóstico do ambiente. Para determinar quais conexões falharam durante a operação de confirmação ou reversão, o aplicativo pode chamar **SQLGetDiagRec** para cada conexão.  
  
> [!NOTE]  
>  O Gerenciador de driver não simula uma transação global em todas as conexões e, portanto, não usa protocolos de confirmação de duas fases.  
  
 Se *complettype* for SQL_COMMIT, **SQLEndTran** emitirá uma solicitação de confirmação para todas as operações ativas em qualquer instrução associada a uma conexão afetada. Se *complettype* for SQL_ROLLBACK, **SQLEndTran** emitirá uma solicitação de reversão para todas as operações ativas em qualquer instrução associada a uma conexão afetada. Se nenhuma transação estiver ativa, **SQLEndTran** retornará SQL_SUCCESS sem nenhum efeito em nenhuma fonte de dados. Para obter mais informações, consulte [confirmando e revertendo transações](../../../odbc/reference/develop-app/committing-and-rolling-back-transactions.md).  
  
 Se o driver estiver no modo de confirmação manual (chamando **SQLSetConnectAttr** com o atributo SQL_ATTR_AUTOCOMMIT definido como SQL_AUTOCOMMIT_OFF), uma nova transação será iniciada implicitamente quando uma instrução SQL que pode ser contida em uma transação for executada na fonte de dados atual. Para obter mais informações, consulte [modo de confirmação](../../../odbc/reference/develop-app/commit-mode.md).  
  
 Para determinar como as operações de transação afetam os cursores, um aplicativo chama **SQLGetInfo** com as opções SQL_CURSOR_ROLLBACK_BEHAVIOR e SQL_CURSOR_COMMIT_BEHAVIOR. Para obter mais informações, consulte os parágrafos a seguir e também ver o [efeito de transações em cursores e instruções](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)preparadas.  
  
 Se o valor de SQL_CURSOR_ROLLBACK_BEHAVIOR ou SQL_CURSOR_COMMIT_BEHAVIOR for igual a SQL_CB_DELETE, **SQLEndTran** fechará e excluirá todos os cursores abertos em todas as instruções associadas à conexão e descartará todos os resultados pendentes. **SQLEndTran** deixa qualquer instrução presente em um estado alocado (despreparado); o aplicativo pode reutilizá-los para solicitações SQL subsequentes ou pode chamar **SQLFreeStmt** ou **SQLFreeHandle** com um *HandleType* de SQL_HANDLE_STMT para desalocá-los.  
  
 Se o valor de SQL_CURSOR_ROLLBACK_BEHAVIOR ou SQL_CURSOR_COMMIT_BEHAVIOR for igual a SQL_CB_CLOSE, **SQLEndTran** fechará todos os cursores abertos em todas as instruções associadas à conexão. **SQLEndTran** deixa qualquer instrução presente em um estado preparado; o aplicativo pode chamar **SQLExecute** para uma instrução associada à conexão sem primeiro chamar **SQLPrepare**.  
  
 Se o valor de SQL_CURSOR_ROLLBACK_BEHAVIOR ou SQL_CURSOR_COMMIT_BEHAVIOR for igual a SQL_CB_PRESERVE, **SQLEndTran** não afetará os cursores abertos associados à conexão. Os cursores permanecem na linha à qual apontavam antes da chamada para **SQLEndTran**.  
  
 Para drivers e fontes de dados que dão suporte a transações, chamar **SQLEndTran** com SQL_COMMIT ou SQL_ROLLBACK quando nenhuma transação está ativa retorna SQL_SUCCESS (indicando que não há trabalho a ser confirmado ou revertido) e não tem efeito sobre a fonte de dados.  
  
 Quando um driver está no modo de confirmação automática, o Gerenciador de driver não chama **SQLEndTran** no driver. **SQLEndTran** sempre retorna SQL_SUCCESS, independentemente de ser chamado com um *complettype* de SQL_COMMIT ou SQL_ROLLBACK.  
  
 Os drivers ou fontes de dados que não dão suporte a transações (a *opção* **SQLGetInfo** SQL_TXN_CAPABLE é SQL_TC_NONE) são efetivamente sempre no modo de confirmação automática e, portanto, sempre retornam SQL_SUCCESS para **SQLEndTran** se eles são chamados com um *complettype* de SQL_COMMIT ou SQL_ROLLBACK. Tais drivers e fontes de dados não revertem transações quando solicitados a fazê-lo.  
  
## <a name="suspended-state"></a>Estado suspenso  
 Em gerenciadores de driver que foram lançados antes do Windows 7, uma transação estava ativa se **SQLEndTran** retornou SQL_ERROR do driver. No entanto, era possível que a transação tenha sido confirmada com êxito no servidor, mas o driver no cliente não foi notificado (por exemplo, porque ocorreu um erro de rede). Isso deixaria a conexão em um estado inadequado. A partir do Windows 7, quando **SQLEndTran** retorna SQL_ERROR, a conexão pode estar em um estado suspenso. Em um estado suspenso, é possível chamar funções somente leitura. Eventualmente, o aplicativo deve chamar **SQLDisconnect** em uma conexão suspensa para liberar recursos.  
  
 Se todas as condições a seguir forem verdadeiras, a conexão será colocada em um estado suspenso:  
  
-   O driver retorna SQL_ERROR de **SQLEndTran**.  
  
-   O driver é ODBC versão 3,8 ou posterior.  
  
-   A versão do aplicativo é 3,8 ou posterior; ou o aplicativo ODBC 2. x ou 3. x recompilado com êxito cancela a função **SQLEndTran** por meio de **SQLCancelHandle**.  
  
-   O driver não retornou uma das mensagens a seguir, que confirmaram que a transação não foi concluída:  
  
    -   25S03: a transação é revertida  
  
    -   40001: falha de serialização  
  
    -   40002: restrição de integridade  
  
    -   HYC00: recurso opcional não implementado  
  
 Se **SQLEndTran** foi chamado em um identificador de ambiente e uma de suas conexões atendeu às condições acima, todas as conexões que se conectam ao mesmo driver serão colocadas no estado suspenso.  
  
 Depois que um aplicativo chama **SQLDisconnect** em uma conexão suspensa, a conexão pode ser usada para se reconectar a outra fonte de dados ou à mesma fonte de dados.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Cancelando uma função que executa de forma assíncrona em um identificador de conexão.|[Função SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|Retornando informações sobre um driver ou uma fonte de dados|[Função SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|Liberando um identificador|[Função SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Liberando um identificador de instrução|[Função SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Execução assíncrona (método de sondagem)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
