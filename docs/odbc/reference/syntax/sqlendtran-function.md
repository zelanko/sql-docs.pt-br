---
title: Função SQLEndTran | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: af0207a5ccaa11728b0ff67a4acad75577acdca7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlendtran-function"></a>Função SQLEndTran
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 3.0 ODBC: 92 ISO  
  
 **Resumo**  
 **SQLEndTran** solicita uma operação de confirmação ou reversão de todas as operações ativas em todas as instruções associadas a uma conexão. **SQLEndTran** também pode solicitar que uma operação de confirmação ou reversão ser executada para todas as conexões associadas a um ambiente.  
  
> [!NOTE]  
>  Para obter mais informações sobre o que o Gerenciador de Driver mapeia essa função quando um ODBC 3. *x* aplicativo estiver trabalhando com um ODBC 2. *x* driver, consulte [mapeamento de funções de substituição para compatibilidade com versões anteriores de aplicativos](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLEndTran(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle,  
     SQLSMALLINT   CompletionType);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HandleType*  
 [Entrada] Tipo de identificador. Contém ambos SQL_HANDLE_ENV (se *tratar* é um identificador de ambiente) ou SQL_HANDLE_DBC (se *tratar* é um identificador de conexão).  
  
 *Handle*  
 [Entrada] O identificador do tipo indicado pelo *HandleType*, indicando que o escopo da transação. Consulte "Comentários" para obter mais informações.  
  
 *CompletionType*  
 [Entrada] Um dos seguintes valores:  
  
 SQL_COMMIT SQL_ROLLBACK  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE ou SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLEndTran** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com apropriada *HandleType*e *tratar*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLEndTran** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08003|Conexão não aberta|(DM) a *HandleType* foi SQL_HANDLE_DBC e o *tratar* não estava em um estado conectado.|  
|08007|Falha de Conexão durante a transação|O *HandleType* foi SQL_HANDLE_DBC e a conexão associada a *tratar* falha durante a execução da função, e não pode ser determinado se a solicitação  **Confirmar** ou **REVERSÃO** ocorreu antes da falha.|  
|25S01|Estado de transação desconhecido|Uma ou mais das conexões em *tratar* Falha ao concluir a transação com o resultado especificado e o resultado é desconhecido.|  
|25S02|Transação ainda está ativa|O driver não foi capaz de garantir que todo o trabalho na transação global pode ser concluído atomicamente, e a transação ainda está ativa.|  
|25S03|Transação é revertida|O driver não foi capaz de garantir que todo o trabalho na transação global pode ser concluído atomicamente, e todos eles funcionam na transação ativa no *tratar* foi revertida.|  
|40001|Falha na serialização|A transação foi revertida devido a um deadlock de recursos com outra transação.|  
|40002|Violação de restrição de integridade|O *CompletionType* foi SQL_COMMIT e a confirmação das alterações causou a violação de restrição de integridade. Como resultado, a transação foi revertida.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo **SQLGetDiagRec** no  *\*szMessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *identificador da conexão*. A função foi chamada e antes ele terminar a execução [SQLCancelHandle função](../../../odbc/reference/syntax/sqlcancelhandle-function.md) foi chamado no *identificador da conexão*. Em seguida, a função foi chamada novamente no *identificador da conexão*.<br /><br /> A função foi chamada e antes ele terminar a execução **SQLCancelHandle** foi chamado no *identificador da conexão* de um thread diferente em um aplicativo multithread.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para um identificador de instrução associado a *identificador da conexão* e ainda estava em execução quando **SQLEndTran** foi chamado.<br /><br /> (DM) uma função de execução assíncrona (não la) foi chamada para o *identificador da conexão* e ainda estava em execução quando esta função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para um identificador de instrução associado a *Identificador da conexão* e retorna SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todas as colunas ou parâmetros de dados em execução.<br /><br /> (DM) uma função de execução assíncrona (não la) foi chamada para o *tratar* com *HandleType* definido como SQL_HANDLE_DBC e ainda estava em execução quando esta função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para uma das alças de instrução associadas *tratar* e SQL_PARAM_DATA_AVAILABLE retornado. Essa função foi chamada antes de recuperação para todos os parâmetros de fluxo de dados.|  
|HY012|Código de operação da transação inválido|(DM) o valor especificado para o argumento *CompletionType* foi nem SQL_COMMIT ou SQL_ROLLBACK.|  
|HY013|Erro de gerenciamento de memória|Não foi possível processar a chamada de função porque os objetos de memória subjacente não podem ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY092|Identificador de atributo/opção inválido|(DM) o valor especificado para o argumento *HandleType* não era SQL_HANDLE_ENV nem SQL_HANDLE_DBC.|  
|HY115|SQLEndTran não é permitido para um ambiente que contém uma conexão com a execução de função assíncrona habilitada|(DM) *HandleType* não pode ser definido como SQL_HANDLE_ENV se execução assíncrona de funções de conexão está habilitada para uma conexão no ambiente.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecido. Somente Desconecte e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte a seção Comentários deste tópico.|  
|HYC00|Recurso opcional não implementado|A driver ou fonte de dados não oferece suporte a **REVERSÃO** operação.|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|O driver em (DM) associado a *identificador da conexão* não oferece suporte para a função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem está desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior na alça retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 Para ODBC 3. *x* driver, se *HandleType* é SQL_HANDLE_ENV e *tratar* é um identificador de ambiente válido, em seguida, o Gerenciador de Driver chamará **SQLEndTran**em cada driver associado ao ambiente. O *tratar* argumento para a chamada para um driver será o identificador de ambiente do driver. Para ODBC 2. *x* driver, se *HandleType* é SQL_HANDLE_ENV e *tratar* é um identificador de ambiente válido e houver várias conexões em um estado conectado no ambiente, em seguida, o Gerenciador de Driver chamará **SQLTransact** no driver de uma vez para cada conexão em um estado conectado no ambiente. O *tratar* argumento em cada chamada será o identificador da conexão. Em ambos os casos, o driver tentará confirmar ou reverter transações, dependendo do valor de *CompletionType*, em todas as conexões que estão em um estado conectado no ambiente. As conexões que não estão ativas não afetam a transação.  
  
> [!NOTE]  
>  **SQLEndTran** não pode ser usado para confirmar ou reverter as transações em um ambiente compartilhado. SQLSTATE HY092 (identificador de atributo/opção inválido) será retornado se **SQLEndTran** é chamado com *tratar* definido como ou o identificador de um ambiente compartilhado ou o identificador de uma conexão em um compartilhado ambiente.  
  
 O Gerenciador de Driver retornará SQL_SUCCESS somente se ele recebe SQL_SUCCESS para cada conexão. Se o Gerenciador de Driver recebe SQL_ERROR em uma ou mais conexões, ele retornará SQL_ERROR para o aplicativo e as informações de diagnóstico são colocadas na estrutura de dados de diagnóstico do ambiente. Para determinar quais conexões ou a conexão falharam durante a operação de confirmação ou reversão, o aplicativo pode chamar **SQLGetDiagRec** para cada conexão.  
  
> [!NOTE]  
>  O Gerenciador de Driver não simular uma transação global em todas as conexões e, portanto, não usa protocolos de confirmação de duas fases.  
  
 Se *CompletionType* é SQL_COMMIT, **SQLEndTran** emite uma solicitação de confirmação de todas as operações ativas em qualquer instrução associado a uma conexão afetado. Se *CompletionType* é SQL_ROLLBACK, **SQLEndTran** emite uma solicitação de reversão de todas as operações ativas em qualquer instrução associado a uma conexão afetado. Se não há nenhuma transação ativa, **SQLEndTran** retorna SQL_SUCCESS sem efeito em qualquer fonte de dados. Para obter mais informações, consulte [Committing e reverter transações](../../../odbc/reference/develop-app/committing-and-rolling-back-transactions.md).  
  
 Se o driver estiver no modo de confirmação manual (chamando **SQLSetConnectAttr** com o SQL_ATTR_AUTOCOMMIT atributo definido como SQL_AUTOCOMMIT_OFF), uma nova transação é iniciada implicitamente quando uma instrução SQL que pode ser contida dentro de um transação é executada em relação à fonte de dados atual. Para obter mais informações, consulte [modo de confirmação](../../../odbc/reference/develop-app/commit-mode.md).  
  
 Para determinar como as operações de transação afetam cursores, um aplicativo chama **SQLGetInfo** com as opções SQL_CURSOR_ROLLBACK_BEHAVIOR e SQL_CURSOR_COMMIT_BEHAVIOR. Para obter mais informações, consulte os parágrafos a seguir e também [efeito de transações em cursores e instruções preparadas](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md).  
  
 Se o valor SQL_CURSOR_ROLLBACK_BEHAVIOR ou SQL_CURSOR_COMMIT_BEHAVIOR for igual a SQL_CB_DELETE, **SQLEndTran** fecha e exclui todos os cursores abertos em todas as instruções associadas com a conexão e descarta todos os resultados pendentes. **SQLEndTran** deixa qualquer instrução presente em um estado (despreparado) alocado; o aplicativo pode reutilizá-los para solicitações subsequentes de SQL ou pode chamar **SQLFreeStmt** ou **SQLFreeHandle** com um *HandleType* sql_handle_stmt para desalocá-los.  
  
 Se o valor SQL_CURSOR_ROLLBACK_BEHAVIOR ou SQL_CURSOR_COMMIT_BEHAVIOR for igual a SQL_CB_CLOSE, **SQLEndTran** fecha todos os cursores abertos em todas as instruções associadas com a conexão. **SQLEndTran** deixa qualquer instrução presente em um estado preparado; o aplicativo pode chamar **SQLExecute** para uma instrução associada com a conexão sem primeiro chamar **SQLPrepare**.  
  
 Se o valor SQL_CURSOR_ROLLBACK_BEHAVIOR ou SQL_CURSOR_COMMIT_BEHAVIOR for igual a SQL_CB_PRESERVE, **SQLEndTran** não afeta cursores abertos associados a conexão. Os cursores permanecem na linha que apontada antes da chamada para **SQLEndTran**.  
  
 Para drivers e fontes de dados que oferecem suporte a transações, chamando **SQLEndTran** com SQL_COMMIT ou SQL_ROLLBACK quando nenhuma transação está ativa retorna SQL_SUCCESS (indicando que não há nenhum trabalho a ser confirmada ou revertida) e não tem nenhum efeito na fonte de dados.  
  
 Quando um driver está no modo de confirmação automática, o Gerenciador de Driver não chama **SQLEndTran** no driver. **SQLEndTran** sempre retorna SQL_SUCCESS independentemente se ele é chamado com um *CompletionType* de SQL_COMMIT ou SQL_ROLLBACK.  
  
 Fontes de dados ou drivers que não oferecem suporte a transações (**SQLGetInfo** *opção* SQL_TXN_CAPABLE é SQL_TC_NONE) são sempre efetivamente no modo de confirmação automática e, portanto, sempre retornará SQL_SUCCESS para **SQLEndTran** ou não que são chamadas com um *CompletionType* de SQL_COMMIT ou SQL_ROLLBACK. Esses drivers e fontes de dados não realmente reverter transações quando solicitado a fazê-lo.  
  
## <a name="suspended-state"></a>Estado suspenso  
 Em gerenciadores de Driver que foram lançadas antes do Windows 7, uma transação estava ativa se **SQLEndTran** retornado SQL_ERROR do driver. No entanto, é possível que a transação tivesse sido confirmada com êxito no servidor, mas o driver no cliente não tinha foi notificado (por exemplo, porque ocorreu um erro de rede). Isso deixará a conexão em um estado inválido. Começando com o Windows 7, quando **SQLEndTran** retorna SQL_ERROR, a conexão pode estar em um estado suspenso. Em um estado suspenso, é possível chamar funções de somente leitura. Por fim, o aplicativo deve chamar **SQLDisconnect** em uma conexão suspenso para liberar recursos.  
  
 Se todas as seguintes condições forem verdadeiras, a conexão será colocado em um estado suspenso:  
  
-   O driver retornará SQL_ERROR de **SQLEndTran**.  
  
-   O driver é ODBC versão 3.8 ou posterior.  
  
-   A versão do aplicativo é 3.8 ou posterior; ou o aplicativo recompilado ODBC 2. x ou 3. x com êxito cancela a **SQLEndTran** funcionar através de **SQLCancelHandle**.  
  
-   O driver não retornou uma das mensagens a seguir, que confirmar que a transação não foi concluída:  
  
    -   25S03: transação é revertida  
  
    -   40001: Falha na serialização  
  
    -   40002: restrição de integridade  
  
    -   HYC00: Recurso opcional não implementado  
  
 Se **SQLEndTran** foi chamado em um ambiente de identificador e uma de suas conexões atendida as condições acima, todas as conexões de conexão com o mesmo driver serão colocadas no estado suspenso.  
  
 Depois que um aplicativo chama **SQLDisconnect** em uma conexão suspenso, a conexão pode ser usado para reconectar-se à mesma fonte de dados ou de outra fonte de dados.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Cancelando uma função em execução assíncrona em um identificador de conexão.|[Função SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|Retornando informações sobre um driver ou fonte de dados|[Função SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|Liberando um identificador|[Função SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Liberando um identificador de instrução|[Função SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Execução assíncrona (método de sondagem)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
