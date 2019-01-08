---
title: Função SQLEndTran | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLEndTran
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLEndTran
helpviewer_keywords:
- SQLEndTran function [ODBC]
ms.assetid: ff375ce1-eb50-4693-b1e6-70181a6dbf9f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fa1b2afec38116bef3ae90d75607d21c9a92cd80
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53204555"
---
# <a name="sqlendtran-function"></a>Função SQLEndTran
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 3.0 ODBC: ISO 92  
  
 **Resumo**  
 **SQLEndTran** solicita uma operação de confirmação ou reversão para todas as operações ativas em todas as declarações associadas com uma conexão. **SQLEndTran** também pode solicitar que uma operação de confirmação ou reversão ser executada para todas as conexões associadas a um ambiente.  
  
> [!NOTE]  
>  Para obter mais informações sobre o que o Gerenciador de Driver mapeia essa função quando um ODBC 3. *x* aplicativo está funcionando com um ODBC 2. *x* driver, consulte [mapeamento de funções de substituição para compatibilidade com versões anteriores de aplicativos](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLEndTran(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle,  
     SQLSMALLINT   CompletionType);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HandleType*  
 [Entrada] Identificador de tipo de identificador. Contém qualquer SQL_HANDLE_ENV (se *manipular* é um identificador de ambiente) ou SQL_HANDLE_DBC (se *manipular* é um identificador de conexão).  
  
 *Handle*  
 [Entrada] O identificador, do tipo indicado por *HandleType*, que indica o escopo da transação. Consulte "Comentários" para obter mais informações.  
  
 *CompletionType*  
 [Entrada] Um dos dois valores a seguir:  
  
 SQL_COMMIT SQL_ROLLBACK  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE ou SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLEndTran** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com os devidos *HandleType*e *manipular*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLEndTran** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08003|Conexão não aberta|(DM) a *HandleType* foi SQL_HANDLE_DBC e o *manipular* não estava em um estado conectado.|  
|08007|Falha de Conexão durante a transação|O *HandleType* foi SQL_HANDLE_DBC e a conexão associada a *manipular* falha durante a execução da função, e não pode ser determinado se solicitado  **Confirmar** ou **ROLLBACK** ocorreu antes da falha.|  
|25S01|Estado da transação desconhecido|Um ou mais conexões no *manipular* Falha ao concluir a transação com o resultado especificado e o resultado é desconhecido.|  
|25S02|Transação ainda está ativa|O driver não foi capaz de garantir que todo o trabalho na transação global atomicamente pôde ser concluído e a transação ainda está ativa.|  
|25S03|Transação será revertida|O driver não foi capaz de garantir que todo o trabalho na transação global pôde ser concluído de forma atômica e todo o trabalho na transação ativa na *manipular* foi revertida.|  
|40001|Falha na serialização|A transação foi revertida devido a um deadlock de recursos com outra transação.|  
|40002|Violação de restrição de integridade|O *CompletionType* estava ativa, e o compromisso de alterações causou a violação de restrição de integridade. Como resultado, a transação foi revertida.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** na  *\*szMessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *ConnectionHandle*. A função foi chamada e antes ele terminou de ser executada [função SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) foi chamado na *ConnectionHandle*. Em seguida, a função foi chamada novamente na *ConnectionHandle*.<br /><br /> A função foi chamada e antes ele terminou de ser executada **SQLCancelHandle** foi chamado na *ConnectionHandle* de um thread diferente em um aplicativo multithread.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para um identificador de instrução associado a *ConnectionHandle* e ainda estava em execução quando **SQLEndTran** foi chamado.<br /><br /> (DM) uma função de execução assíncrona (não desse último) foi chamada para o *ConnectionHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para um identificador de instrução associado a *ConnectionHandle* e retornados de SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todos os parâmetros de dados em execução ou colunas.<br /><br /> (DM) uma função de execução assíncrona (não desse último) foi chamada para o *manipular* com *HandleType* definido como SQL_HANDLE_DBC e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para uma das alças de instrução associadas *manipular* e SQL_PARAM_DATA_AVAILABLE retornado. Essa função foi chamada antes de dados foram recuperados para todos os parâmetros transmitidos.|  
|HY012|Código de operação de transação inválido|(DM) o valor especificado para o argumento *CompletionType* foi nem SQL_COMMIT ou SQL_ROLLBACK.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY092|Identificador de atributo/opção inválido|(DM) o valor especificado para o argumento *HandleType* não era SQL_HANDLE_ENV nem SQL_HANDLE_DBC.|  
|HY115|SQLEndTran não é permitida para um ambiente que contém uma conexão com a execução da função assíncrona habilitada|(DM) *HandleType* não pode ser definido como SQL_HANDLE_ENV se a execução assíncrona de funções de conexão está habilitada para uma conexão no ambiente.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte a seção Comentários deste tópico.|  
|HYC00|Recurso opcional não implementado|A fonte de dados ou driver não dá suporte a **REVERSÃO** operação.|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|O driver em (DM) associado a *ConnectionHandle* não suporta a função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem é desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior no identificador retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado no identificador de fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 Para um ODBC 3. *x* driver, se *HandleType* é SQL_HANDLE_ENV e *manipular* é um identificador de ambiente válido, em seguida, o Gerenciador de Driver chamará **SQLEndTran**em cada driver associada ao ambiente. O *manipular* argumento para a chamada para um driver será o identificador de ambiente do driver. Para um ODBC 2. *x* driver, se *HandleType* é SQL_HANDLE_ENV e *manipular* é um identificador de ambiente válido, e há várias conexões em um estado conectado no ambiente, em seguida, o Gerenciador de Driver chamará **SQLTransact** no driver de uma vez para cada conexão em um estado conectado no ambiente. O *manipular* argumento em cada chamada será o identificador da conexão. Em ambos os casos, o driver tentará confirmar ou reverter transações, dependendo do valor de *CompletionType*, em todas as conexões que estão em um estado conectado no ambiente. As conexões que não estão ativas não afetam a transação.  
  
> [!NOTE]  
>  **SQLEndTran** não pode ser usado para confirmar ou reverter as transações em um ambiente compartilhado. SQLSTATE HY092 (identificador de atributo/opção inválido) será retornado se **SQLEndTran** for chamado com *manipular* definido como o identificador de uma conexão em um compartilhamento ou de ambos o identificador de um ambiente compartilhado ambiente.  
  
 O Gerenciador de Driver retornará SQL_SUCCESS somente se ela recebe SQL_SUCCESS para cada conexão. Se o Gerenciador de Driver recebe SQL_ERROR em uma ou mais conexões, ele retorna SQL_ERROR para o aplicativo e as informações de diagnóstico são colocadas na estrutura de dados de diagnóstico do ambiente. Para determinar quais conexões ou a conexão falharam durante a operação de confirmação ou reversão, o aplicativo pode chamar **SQLGetDiagRec** para cada conexão.  
  
> [!NOTE]  
>  O Gerenciador de Driver não simula uma transação global em todas as conexões e, portanto, não usa protocolos de confirmação de duas fases.  
  
 Se *CompletionType* está ativa, **SQLEndTran** emite uma solicitação de confirmação para todas as operações ativas em qualquer instrução associado com uma conexão afetado. Se *CompletionType* é SQL_ROLLBACK, **SQLEndTran** emite uma solicitação de reversão de todas as operações ativas em qualquer instrução associado com uma conexão afetado. Se não há nenhuma transação ativa, **SQLEndTran** retorna SQL_SUCCESS com nenhum efeito sobre as fontes de dados. Para obter mais informações, consulte [Committing e reverter transações](../../../odbc/reference/develop-app/committing-and-rolling-back-transactions.md).  
  
 Se o driver estiver no modo de confirmação manual (chamando **SQLSetConnectAttr** com o SQL_ATTR_AUTOCOMMIT atributo definido como SQL_AUTOCOMMIT_OFF), uma nova transação é iniciada implicitamente quando uma instrução SQL que pode estar contida em um transação é executada na fonte de dados atual. Para obter mais informações, consulte [modo de confirmação](../../../odbc/reference/develop-app/commit-mode.md).  
  
 Para determinar como as operações de transação afetam cursores, um aplicativo chama **SQLGetInfo** com as opções SQL_CURSOR_ROLLBACK_BEHAVIOR e SQL_CURSOR_COMMIT_BEHAVIOR. Para obter mais informações, consulte os parágrafos a seguir e também [efeito de transações em cursores e instruções preparadas](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md).  
  
 Se o valor SQL_CURSOR_ROLLBACK_BEHAVIOR ou SQL_CURSOR_COMMIT_BEHAVIOR for igual a SQL_CB_DELETE, **SQLEndTran** fecha e exclui todos os cursores abertos em todas as declarações associadas com a conexão e descarta todos os resultados pendentes. **SQLEndTran** deixa de qualquer instrução presente em um estado (despreparado) alocado, o aplicativo pode reutilizá-los para solicitações subsequentes de SQL ou pode chamar **SQLFreeStmt** ou **SQLFreeHandle** com uma *HandleType* sql_handle_stmt para desalocá-los.  
  
 Se o valor SQL_CURSOR_ROLLBACK_BEHAVIOR ou SQL_CURSOR_COMMIT_BEHAVIOR for igual a SQL_CB_CLOSE, **SQLEndTran** fecha todos os cursores abertos em todas as declarações associadas com a conexão. **SQLEndTran** deixa de qualquer instrução presente em um estado preparado; o aplicativo pode chamar **SQLExecute** para uma instrução associada com a conexão sem primeiro chamar **SQLPrepare**.  
  
 Se o valor SQL_CURSOR_ROLLBACK_BEHAVIOR ou SQL_CURSOR_COMMIT_BEHAVIOR for igual a SQL_CB_PRESERVE, **SQLEndTran** não afeta cursores abertos associados com a conexão. Cursores permanecerão na linha em que eles apontado antes da chamada a **SQLEndTran**.  
  
 Para drivers e fontes de dados que dão suporte a transações, chamar **SQLEndTran** com SQL_COMMIT ou SQL_ROLLBACK quando nenhuma transação estiver ativa retorna SQL_SUCCESS (indicando que não há nenhum trabalho a ser confirmada ou revertida) e não tem nenhum efeito na fonte de dados.  
  
 Quando um driver está no modo de confirmação automática, o Gerenciador de Driver não chama **SQLEndTran** no driver. **SQLEndTran** sempre retorna SQL_SUCCESS independentemente se ele for chamado com um *CompletionType* de SQL_COMMIT ou SQL_ROLLBACK.  
  
 Fontes de dados ou drivers que não dão suporte a transações (**SQLGetInfo** *opção* SQL_TXN_CAPABLE é SQL_TC_NONE) são sempre efetivamente no modo de confirmação automática e, portanto, sempre retornará SQL_SUCCESS para **SQLEndTran** ou não que são chamadas com um *CompletionType* de SQL_COMMIT ou SQL_ROLLBACK. Esses drivers e fontes de dados, na verdade, reverter transações quando solicitado a fazê-lo.  
  
## <a name="suspended-state"></a>Estado suspenso  
 Em gerenciadores de Driver que foram lançadas antes do Windows 7, uma transação estava ativa se **SQLEndTran** retornado SQL_ERROR do driver. No entanto, era possível que a transação tivesse sido confirmada com êxito no servidor, mas o driver no cliente não tinha Fui notificado (por exemplo, porque ocorreu um erro de rede). Isso deixaria a conexão em um estado inválido. Começando com o Windows 7, quando **SQLEndTran** retorna SQL_ERROR, a conexão pode estar em um estado suspenso. Em um estado suspenso, é possível chamar funções de somente leitura. Por fim, o aplicativo deve chamar **SQLDisconnect** em uma conexão suspenso para liberar recursos.  
  
 Se todas as seguintes condições forem verdadeiras, a conexão será colocado em um estado suspenso:  
  
-   O driver retornará SQL_ERROR partir **SQLEndTran**.  
  
-   O driver é ODBC versão 3.8 ou posterior.  
  
-   A versão do aplicativo é 3.8 ou posterior; ou aplicativo recompilado ODBC 2.x ou 3.x com êxito cancela a **SQLEndTran** funcionar através de **SQLCancelHandle**.  
  
-   O driver não retornou uma das seguintes mensagens, que confirmar que a transação não foi concluída:  
  
    -   25S03: Transação será revertida  
  
    -   40001: Falha na serialização  
  
    -   40002: restrição de integridade  
  
    -   HYC00: Recurso opcional não implementado  
  
 Se **SQLEndTran** foi chamado em um ambiente do identificador e uma das suas conexões atendidas as condições acima, todas as conexões de conexão com o mesmo driver entrará em estado suspenso.  
  
 Depois que um aplicativo chama **SQLDisconnect** em uma conexão suspenso, a conexão pode ser usado para se reconectar à mesma fonte de dados ou de outra fonte de dados.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Cancelando uma função em execução assíncrona em um identificador de conexão.|[Função SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|Retornando informações sobre um driver ou fonte de dados|[Função SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|Liberando um identificador|[Função SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Liberando um identificador de instrução|[Função SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Execução assíncrona (método de sondagem)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
