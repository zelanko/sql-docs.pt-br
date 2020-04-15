---
title: Função SQLendtran | Microsoft Docs
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
ms.openlocfilehash: cce7792e52fce4984f3da41e11d79c34b6b79e53
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302737"
---
# <a name="sqlendtran-function"></a>Função SQLEndTran
**Conformidade**  
 Versão introduzida: ODBC 3.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **O SQLEndTran** solicita uma operação de confirmação ou reversão para todas as operações ativas em todas as declarações associadas a uma conexão. **O SQLEndTran** também pode solicitar que uma operação de confirmação ou reversão seja realizada para todas as conexões associadas a um ambiente.  
  
> [!NOTE]  
>  Para obter mais informações sobre o que o Driver Manager mapeia essa função para quando um ODBC 3. *x* aplicativo está trabalhando com um ODBC 2. *x* driver, consulte [Funções de substituição de mapeamento para compatibilidade retrógrada de aplicativos](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLEndTran(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle,  
     SQLSMALLINT   CompletionType);  
```  
  
## <a name="arguments"></a>Argumentos  
 *Handletype*  
 [Entrada] Identificador de tipo de punho. Contém SQL_HANDLE_ENV (se *o Punho for* uma alça de ambiente) ou SQL_HANDLE_DBC (se o *Handle* for uma alça de conexão).  
  
 *Handle*  
 [Entrada] A alça, do tipo indicado pela *HandleType,* indica o escopo da transação. Consulte "Comentários" para obter mais informações.  
  
 *Tipo de conclusão*  
 [Entrada] Um dos dois valores a seguir:  
  
 SQL_COMMIT SQL_ROLLBACK  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE ou SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLEndTran** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com o *HandleType* e *Handle apropriados*. A tabela a seguir lista os valores SQLSTATE comumente devolvidos pelo **SQLEndTran** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|08003|Conexão não aberta|(DM) O *HandleType* foi SQL_HANDLE_DBC, e o *Handle* não estava em um estado conectado.|  
|08007|Falha de conexão durante a transação|O *HandleType* foi SQL_HANDLE_DBC, e a conexão associada ao *Handle* falhou durante a execução da função, e não é possível determinar se o **COMMIT** ou **ROLLBACK** solicitado ocorreram antes da falha.|  
|25S01|Estado de transação desconhecido|Uma ou mais das conexões no *Handle* não conseguiram concluir a transação com o resultado especificado, e o resultado é desconhecido.|  
|25S02|Transação ainda está ativa|O driver não foi capaz de garantir que todo o trabalho na transação global poderia ser concluído atomicamente, e a transação ainda está ativa.|  
|25S03|Transação é revertida|O driver não foi capaz de garantir que todo o trabalho na transação global poderia ser concluído atomicamente, e todo o trabalho na transação ativa na *Handle* foi revertido.|  
|40001|Falha na serialização|A transação foi revertida devido a um impasse de recursos com outra transação.|  
|40002|Violação de restrição de integridade|O *CompletionType* foi SQL_COMMIT, e o compromisso das mudanças causou violação de restrição de integridade. Como resultado, a transação foi revertida.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \*buffer szMessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *ConnectionHandle*. A função foi chamada e antes de terminar a execução da [função SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) foi chamada no *ConnectionHandle*. Em seguida, a função foi chamada novamente no *ConnectionHandle*.<br /><br /> A função foi chamada e antes de terminar de executar **o SQLCancelHandle** foi chamado no *ConnectionHandle* de um segmento diferente em um aplicativo multithread.|  
|HY010|Erro de seqüência de função|(DM) Uma função de execução assíncrona foi solicitada para uma alça de declaração associada ao *ConnectionHandle* e ainda estava sendo executada quando **o SQLEndTran** foi chamado.<br /><br /> (DM) Uma função de execução assíncrona (não esta) foi chamada para o *ConnectionHandle* e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados para uma alça de declaração associada ao *ConnectionHandle* e retornou SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.<br /><br /> (DM) Uma função de execução assíncrona (não esta) foi chamada para que o *Handle* with *HandleType* fosse SQL_HANDLE_DBC e ainda estava sendo executado quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foi chamado para uma das alças de declaração associadas ao *Handle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.|  
|HY012|Código de operação de transação inválida|(DM) O valor especificado para o argumento *CompletionType* não foi SQL_COMMIT nem SQL_ROLLBACK.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY092|Identificador de atributo/opção inválido|(DM) O valor especificado para o argumento *HandleType* não foi SQL_HANDLE_ENV nem SQL_HANDLE_DBC.|  
|HY115|SQLEndTran não é permitido para um ambiente que contém uma conexão com execução de função assíncrona ativada|(DM) *O HandleType* não pode ser definido como SQL_HANDLE_ENV se a execução assíncrona das funções de conexão estiver ativada para uma conexão no ambiente.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte a seção Comentários deste tópico.|  
|HYC00|Recurso opcional não implementado|O driver ou a fonte de dados não suportam a operação **ROLLBACK.**|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *ConnectionHandle* não suporta a função.|  
|IM017|A votação é desativada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a votação é desativada.|  
|IM018|**O SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesta alça.|Se a chamada de função anterior na alça retornar SQL_STILL_EXECUTING e se o modo de notificação estiver ativado, o **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 Para um ODBC 3. *x* driver, se *HandleType* for SQL_HANDLE_ENV e *Handle* for uma alça de ambiente válida, então o Driver Manager ligará para **o SQLEndTran** em cada driver associado ao ambiente. O argumento *handle* para a chamada para um motorista será o cabo de ambiente do motorista. Para um ODBC 2. *x* driver, se *HandleType* for SQL_HANDLE_ENV e *Handle* for uma alça de ambiente válida, e houver várias conexões em um estado conectado nesse ambiente, então o Driver Manager chamará **SQLTransact** no driver uma vez para cada conexão em um estado conectado nesse ambiente. O argumento *Handle* em cada chamada será o cabo da conexão. Em ambos os casos, o driver tentará cometer ou reverter transações, dependendo do valor de *CompletionType*, em todas as conexões que estejam em um estado conectado nesse ambiente. Conexões que não estão ativas não afetam a transação.  
  
> [!NOTE]  
>  **O SQLEndTran** não pode ser usado para cometer ou reverter transações em um ambiente compartilhado. O SQLSTATE HY092 (identificador de atributo/opção inválido) será devolvido se **o SQLEndTran** for chamado com *handle* definido para o cabo de um ambiente compartilhado ou para o cabo de uma conexão em um ambiente compartilhado.  
  
 O Driver Manager só voltará SQL_SUCCESS se receber SQL_SUCCESS para cada conexão. Se o Driver Manager receber SQL_ERROR em uma ou mais conexões, ele retorna SQL_ERROR ao aplicativo, e as informações de diagnóstico são colocadas na estrutura de dados diagnósticos do ambiente. Para determinar quais conexões ou conexões falharam durante a operação de confirmação ou reversão, o aplicativo pode chamar **sqlGetDiagRec** para cada conexão.  
  
> [!NOTE]  
>  O Driver Manager não simula uma transação global em todas as conexões e, portanto, não usa protocolos de confirmação bifásicos.  
  
 Se *o CompletionType* for SQL_COMMIT, **o SQLEndTran** emitirá uma solicitação de confirmação para todas as operações ativas em qualquer declaração associada a uma conexão afetada. Se *o CompletionType* for SQL_ROLLBACK, **o SQLEndTran** emitirá uma solicitação de reversão de todas as operações ativas em qualquer declaração associada a uma conexão afetada. Se nenhuma transação estiver ativa, **o SQLEndTran** retorna SQL_SUCCESS sem efeito sobre nenhuma fonte de dados. Para obter mais informações, consulte [Comprovida e Reverter Transações](../../../odbc/reference/develop-app/committing-and-rolling-back-transactions.md).  
  
 Se o driver estiver no modo de confirmação manual (ligando para **SQLSetConnectAttr** com o SQL_ATTR_AUTOCOMMIT atributo definido como SQL_AUTOCOMMIT_OFF), uma nova transação será iniciada implicitamente quando uma declaração SQL que pode ser contida em uma transação é executada contra a fonte de dados atual. Para obter mais informações, consulte [O modo de confirmação](../../../odbc/reference/develop-app/commit-mode.md).  
  
 Para determinar como as operações de transação afetam os cursores, um aplicativo chama **o SQLGetInfo** com as opções de SQL_CURSOR_ROLLBACK_BEHAVIOR e SQL_CURSOR_COMMIT_BEHAVIOR. Para obter mais informações, consulte os seguintes parágrafos e consulte [também O Efeito das Transações em Cursors e Declarações Preparadas](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md).  
  
 Se o valor SQL_CURSOR_ROLLBACK_BEHAVIOR ou SQL_CURSOR_COMMIT_BEHAVIOR for igual a SQL_CB_DELETE, **o SQLEndTran** fechará e excluirá todos os cursores abertos em todas as declarações associadas à conexão e descartará todos os resultados pendentes. **O SQLEndTran** deixa qualquer declaração presente em um estado alocado (despreparado); o aplicativo pode reutilizá-los para solicitações SQL subseqüentes ou pode ligar para **SQLFreeStmt** ou **SQLFreeHandle** com um *HandleType* de SQL_HANDLE_STMT para desalocá-las.  
  
 Se o valor SQL_CURSOR_ROLLBACK_BEHAVIOR ou SQL_CURSOR_COMMIT_BEHAVIOR for igual a SQL_CB_CLOSE, **o SQLEndTran** fechará todos os cursores abertos em todas as declarações associadas à conexão. **SQLEndTran** deixa qualquer declaração presente em um estado preparado; o aplicativo pode chamar **SQLExecute** para uma declaração associada à conexão sem antes chamar **SQLPrepare**.  
  
 Se o valor SQL_CURSOR_ROLLBACK_BEHAVIOR ou SQL_CURSOR_COMMIT_BEHAVIOR for igual a SQL_CB_PRESERVE, **o SQLEndTran** não afetará os cursores abertos associados à conexão. Os cursors permanecem na linha que apontaram antes da chamada para **o SQLEndTran**.  
  
 Para drivers e fontes de dados que suportam transações, ligar para **o SQLEndTran** com SQL_COMMIT ou SQL_ROLLBACK quando nenhuma transação estiver ativa retorna SQL_SUCCESS (indicando que não há trabalho a ser cometido ou revertido) e não tem efeito na fonte de dados.  
  
 Quando um motorista está no modo de confirmação automática, o Driver Manager não chama **SQLEndTran** no driver. **O SQLEndTran** sempre retorna SQL_SUCCESS independentemente de ser chamado com um Tipo de *conclusão* de SQL_COMMIT ou SQL_ROLLBACK.  
  
 Drivers ou fontes de dados que não suportam transações ( *opção* **SQLGetInfo** SQL_TXN_CAPABLE é SQL_TC_NONE) estão efetivamente sempre no modo de confirmação automática e, portanto, sempre retornam SQL_SUCCESS para **SQLEndTran,** sejam eles chamados ou não com um Tipo de *Conclusão* de SQL_COMMIT ou SQL_ROLLBACK. Esses drivers e fontes de dados não revertem as transações quando solicitados.  
  
## <a name="suspended-state"></a>Estado suspenso  
 Em Driver Managers que foram lançados antes do Windows 7, uma transação estava ativa se **o SQLEndTran** retornasse SQL_ERROR do driver. No entanto, era possível que a transação tivesse sido cometida com sucesso no servidor, mas o driver no cliente não havia sido notificado (por exemplo, porque ocorreu um erro de rede). Isso deixaria a conexão em um estado ruim. Começando com o Windows 7, quando **o SQLEndTran** retorna SQL_ERROR, a conexão pode estar em estado suspenso. Em um estado suspenso, é possível chamar funções somente leitura. Eventualmente, o aplicativo deve chamar **sqldisconnect** em uma conexão suspensa para liberar recursos.  
  
 Se todas as seguintes condições forem verdadeiras, a conexão será colocada em estado suspenso:  
  
-   O motorista retorna SQL_ERROR do **SQLEndTran**.  
  
-   O driver é o ODBC versão 3.8, ou posterior.  
  
-   A versão do aplicativo é 3.8 ou posterior; ou o aplicativo ODBC 2.x ou 3.x recompilado cancela com sucesso a função **SQLEndTran** através **do SQLCancelHandle**.  
  
-   O motorista não retornou uma das seguintes mensagens, que confirmam que a transação não foi concluída:  
  
    -   25S03: A transação é revertida  
  
    -   40001: Falha na serialização  
  
    -   40002: Restrição de integridade  
  
    -   HYC00: Recurso opcional não implementado  
  
 Se **o SQLEndTran** foi chamado para uma alça de ambiente e uma de suas conexões atendeu às condições acima, todas as conexões que se conectam ao mesmo driver serão colocadas no estado suspenso.  
  
 Depois que um aplicativo chama **SQLDisconnect** em uma conexão suspensa, a conexão pode ser usada para se reconectar a outra fonte de dados ou a mesma fonte de dados.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Cancelando uma função em execução assíncrona em uma alça de conexão.|[Função SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|Retornando informações sobre um driver ou fonte de dados|[Função SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|Liberando uma alça|[Função SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Liberando uma alça de declaração|[Função SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Execução Assíncrona (Método de Votação)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
