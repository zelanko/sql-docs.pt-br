---
title: Execução Assíncrona (Método de Notificação) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e509dad9-5263-4a10-9a4e-03b84b66b6b3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 250e71dcb47d44a6e437d12c269ea23fa6fb3c2c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306407"
---
# <a name="asynchronous-execution-notification-method"></a>Execução assíncrona (método de notificação)
O ODBC permite a execução assíncrona das operações de conexão e declaração. Um segmento de aplicativo pode chamar uma função ODBC no modo assíncrono e a função pode retornar antes que a operação seja concluída, permitindo que o segmento do aplicativo execute outras tarefas. No SDK do Windows 7, para operações de declaração assíncrona ou conexão, um aplicativo determinou que a operação assíncrona estava completa usando o método de votação. Para obter mais informações, consulte [Execução Assíncrona (Método de Votação)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md). A partir do SDK do Windows 8, você pode determinar que uma operação assíncrona está completa usando o método de notificação.  
  
 No método de votação, os aplicativos precisam chamar a função assíncrona cada vez que deseja o status da operação. O método de notificação é semelhante ao retorno de chamada e espera em ADO.NET. O DBC, no entanto, usa os eventos Win32 como objeto de notificação.  
  
 A Biblioteca Cursor ODBC e a notificação assíncrona ODBC não podem ser usadas ao mesmo tempo. A definição de ambos os atributos retornará um erro com o SQLSTATE S1119 (a Biblioteca do Cursor e a Notificação Assíncrona não podem ser ativadas ao mesmo tempo).  
  
 Consulte [Notificação de Conclusão de Função Assíncrona](../../../odbc/reference/develop-driver/notification-of-asynchronous-function-completion.md) para obter informações para desenvolvedores de drivers.  
  
> [!NOTE]  
>  O método de notificação não é suportado com a biblioteca do cursor. Um aplicativo receberá mensagem de erro se tentar ativar a biblioteca do cursor via SQLSetConnectAttr, quando o método de notificação estiver ativado.  
  
## <a name="overview"></a>Visão geral  
 Quando uma função ODBC é chamada no modo assíncrono, o controle é retornado ao aplicativo de chamada imediatamente com o código de retorno SQL_STILL_EXECUTING. O aplicativo deve sondar repetidamente a função até que retorne algo diferente de SQL_STILL_EXECUTING. O loop de votação aumenta a utilização da CPU, causando um desempenho ruim em muitos cenários assíncronos.  
  
 Sempre que o modelo de notificação é usado, o modelo de votação é desativado. Os aplicativos não devem chamar a função original novamente. Ligue para [a função SQLCompleteAsync](../../../odbc/reference/syntax/sqlcompleteasync-function.md) para concluir a operação assíncrona. Se um aplicativo chamar a função original novamente antes da operação assíncrona ser concluída, a chamada voltará SQL_ERROR com o SQLSTATE IM017 (a votação está desativada no modo de notificação assíncrona).  
  
 Ao usar o modelo de notificação, o aplicativo pode ligar para **SQLCancel** ou **SQLCancelHandle** para cancelar uma operação de declaração ou conexão. Se a solicitação de cancelamento for bem sucedida, a ODBC voltará SQL_SUCCESS. Esta mensagem não indica que a função foi realmente cancelada; indica que o pedido de cancelamento foi processado. Se a função é realmente cancelada é dependente do driver e dependente da fonte de dados. Quando uma operação é cancelada, o Driver Manager ainda sinalizará o evento. O Driver Manager retorna SQL_ERROR no buffer de código de devolução e o estado é SQLSTATE HY008 (Operação cancelada) para indicar que o cancelamento foi bem sucedido. Se a função tiver concluído seu processamento normal, o Driver Manager retorna SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO.  
  
### <a name="downlevel-behavior"></a>Comportamento de nível de baixa  
 A versão do ODBC Driver Manager que suporta esta notificação completa é o ODBC 3.81.  
  
|Versão ODBC do aplicativo|Versão do driver manager|Versão do driver|Comportamento|  
|------------------------------|----------------------------|--------------------|--------------|  
|Nova aplicação de qualquer versão ODBC|ODBC 3.81|ODBC 3.80 Driver|O aplicativo pode usar esse recurso se o driver suportar esse recurso, caso contrário, o Gerenciador de driver saem.|  
|Nova aplicação de qualquer versão ODBC|ODBC 3.81|Driver pré-ODBC 3.80|O Gerenciador de driver saem se o driver não suportar esse recurso.|  
|Nova aplicação de qualquer versão ODBC|Pré-ODBC 3.81|Qualquer|Quando o aplicativo usa esse recurso, um antigo Driver Manager considerará os novos atributos como atributos específicos do driver, e o motorista deve errar. Um novo Driver Manager não passará esses atributos para o motorista.|  
  
 Um aplicativo deve verificar a versão driver manager antes de usar este recurso. Caso contrário, se um driver mal escrito não errar e a versão driver manager for pré ODBC 3.81, o comportamento será indefinido.  
  
## <a name="use-cases"></a>Casos de uso  
 Esta seção mostra casos de uso para execução assíncrona e mecanismo de votação.  
  
### <a name="integrate-data-from-multiple-odbc-sources"></a>Integrar dados de múltiplas fontes ODBC  
 Um aplicativo de integração de dados busca dados de várias fontes de dados. Alguns dos dados são de fontes de dados remotas e alguns dados são de arquivos locais. O aplicativo não pode continuar até que as operações assíncronas sejam concluídas.  
  
 Em vez de fazer uma pesquisa repetida de uma operação para determinar se ela está concluída, o aplicativo pode criar um objeto de evento e associá-lo a uma alça de conexão ODBC ou a uma alça de declaração ODBC. Em seguida, o aplicativo chama as APIs de sincronização do sistema operacional para aguardar em um objeto de evento ou muitos objetos de evento (tanto eventos ODBC quanto outros eventos do Windows). O ODBC sinalizará o objeto de evento quando a operação assíncrona ODBC correspondente estiver concluída.  
  
 No Windows, serão usados objetos de evento Win32 e que fornecerão ao usuário um modelo de programação unificado. Os driver managers em outras plataformas podem usar a implementação do objeto de evento específica para essas plataformas.  
  
 A amostra de código a seguir demonstra o uso de conexão e notificação assíncrona de declaração:  
  
```  
// This function opens NUMBER_OPERATIONS connections and executes one query on statement of each connection.  
// Asynchronous Notification is used  
  
#define NUMBER_OPERATIONS 5  
int AsyncNotificationSample(void)  
{  
    RETCODE     rc;  
  
    SQLHENV     hEnv              = NULL;  
    SQLHDBC     arhDbc[NUMBER_OPERATIONS]         = {NULL};  
    SQLHSTMT    arhStmt[NUMBER_OPERATIONS]        = {NULL};  
  
    HANDLE      arhDBCEvent[NUMBER_OPERATIONS]    = {NULL};  
    RETCODE     arrcDBC[NUMBER_OPERATIONS]        = {0};  
    HANDLE      arhSTMTEvent[NUMBER_OPERATIONS]   = {NULL};  
    RETCODE     arrcSTMT[NUMBER_OPERATIONS]       = {0};  
  
    rc = SQLAllocHandle(SQL_HANDLE_ENV, NULL, &hEnv);  
    if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
  
    rc = SQLSetEnvAttr(hEnv,  
        SQL_ATTR_ODBC_VERSION,  
        (SQLPOINTER) SQL_OV_ODBC3_80,  
        SQL_IS_INTEGER);  
    if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
  
    // Connection operations begin here  
  
    // Alloc NUMBER_OPERATIONS connection handles  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc = SQLAllocHandle(SQL_HANDLE_DBC, hEnv, &arhDbc[i]);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Enable DBC Async on all connection handles  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc= SQLSetConnectAttr(arhDbc[i], SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE, (SQLPOINTER)SQL_ASYNC_DBC_ENABLE_ON, SQL_IS_INTEGER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Application must create event objects  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        arhDBCEvent[i] = CreateEvent(NULL, FALSE, FALSE, NULL); // Auto-reset, initial state is not-signaled  
        if (!arhDBCEvent[i]) goto Cleanup;  
    }  
  
    // Enable notification on all connection handles  
    // Event  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc= SQLSetConnectAttr(arhDbc[i], SQL_ATTR_ASYNC_DBC_EVENT, arhDBCEvent[i], SQL_IS_POINTER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Initiate connect establishing  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLDriverConnect(arhDbc[i], NULL, (SQLTCHAR*)TEXT("Driver={ODBC Driver 11 for SQL Server};SERVER=dp-srv-sql2k;DATABASE=pubs;UID=sa;PWD=XYZ;"), SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
    }  
  
    // Can do some other staff before calling WaitForMultipleObjects  
    WaitForMultipleObjects(NUMBER_OPERATIONS, arhDBCEvent, TRUE, INFINITE); // Wait All  
  
    // Complete connect API calls  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLCompleteAsync(SQL_HANDLE_DBC, arhDbc[i], & arrcDBC[i]);  
    }  
  
    BOOL fFail = FALSE; // Whether some connection openning fails.  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if ( !SQL_SUCCEEDED(arrcDBC[i]) )   
            fFail = TRUE;  
    }  
  
    // If some SQLDriverConnect() fail, clean up.  
    if (fFail)  
    {  
        for (int i=0; i<NUMBER_OPERATIONS; i++)  
        {  
            if (SQL_SUCCEEDED(arrcDBC[i]) )   
            {  
                SQLDisconnect(arhDbc[i]); // This is also async  
            }  
            else  
            {  
                SetEvent(arhDBCEvent[i]); // Previous SQLDriverConnect() failed. No need to call SQLDisconnect().  
            }  
        }  
        WaitForMultipleObjects(NUMBER_OPERATIONS, arhDBCEvent, TRUE, INFINITE);   
        for (int i=0; i<NUMBER_OPERATIONS; i++)  
        {  
            if (SQL_SUCCEEDED(arrcDBC[i]) )   
            {     
                SQLCompleteAsync(SQL_HANDLE_DBC, arhDbc[i], &arrcDBC[i]);; // To Complete  
            }  
        }  
  
        goto Cleanup;  
    }  
  
    // Statement Operations begin here  
  
    // Alloc statement handle  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc = SQLAllocHandle(SQL_HANDLE_STMT, arhDbc[i], &arhStmt[i]);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Enable STMT Async on all statement handles  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc = SQLSetStmtAttr(arhStmt[i], SQL_ATTR_ASYNC_ENABLE, (SQLPOINTER)SQL_ASYNC_ENABLE_ON, SQL_IS_INTEGER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Create event objects  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        arhSTMTEvent[i] = CreateEvent(NULL, FALSE, FALSE, NULL); // Auto-reset, initial state is not-signaled  
        if (!arhSTMTEvent[i]) goto Cleanup;  
    }  
  
    // Enable notification on all statement handles  
    // Event  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc= SQLSetStmtAttr(arhStmt[i], SQL_ATTR_ASYNC_STMT_EVENT, arhSTMTEvent[i], SQL_IS_POINTER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Initiate SQLExecDirect() calls  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLExecDirect(arhStmt[i], (SQLTCHAR*)TEXT("select au_lname, au_fname from authors"), SQL_NTS);  
    }  
  
    // Can do some other staff before calling WaitForMultipleObjects  
    WaitForMultipleObjects(NUMBER_OPERATIONS, arhSTMTEvent, TRUE, INFINITE); // Wait All  
  
    // Now, call SQLCompleteAsync to complete the operation and get return code  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLCompleteAsync(SQL_HANDLE_STMT, arhStmt[i], &arrcSTMT[i]);  
    }  
  
    // Check return values  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if ( !SQL_SUCCEEDED(arrcSTMT[i]) ) goto Cleanup;  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        //Do some binding jobs here, set SQL_ATTR_ROW_ARRAY_SIZE   
    }  
  
    // Now, initiate fetching  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLFetch(arhStmt[i]);  
    }  
  
    // Can do some other staff before calling WaitForMultipleObjects  
    WaitForMultipleObjects(NUMBER_OPERATIONS, arhSTMTEvent, TRUE, INFINITE);   
  
    // Now, to complete the operations and get return code  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLCompleteAsync(SQL_HANDLE_STMT, arhStmt[i], &arrcSTMT[i]);  
    }  
  
    // Check return code  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if ( !SQL_SUCCEEDED(arrcSTMT[i]) ) goto Cleanup;  
    }  
  
    // USE fetched data here!!  
  
Cleanup:  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhStmt[NUMBER_OPERATIONS])  
        {  
            SQLFreeHandle(SQL_HANDLE_STMT, arhStmt[i]);  
            arhStmt[i] = NULL;  
        }  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhSTMTEvent[i])  
        {  
            CloseHandle(arhSTMTEvent[i]);  
            arhSTMTEvent[i] = NULL;  
        }  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhDbc[i])  
        {  
            SQLFreeHandle(SQL_HANDLE_DBC, arhDbc[i]);  
            arhDbc[i] = NULL;  
        }  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhDBCEvent[i])  
        {  
            CloseHandle(arhDBCEvent[i]);  
            arhDBCEvent[i] = NULL;  
        }  
    }  
  
    if (hEnv)  
    {  
        SQLFreeHandle(SQL_HANDLE_ENV, hEnv);  
        hEnv = NULL;  
    }  
  
    return 0;  
}  
  
```  
  
### <a name="determining-if-a-driver-supports-asynchronous-notification"></a>Determinar se um driver suporta notificação assíncrona  
 Um aplicativo ODBC pode determinar se um driver ODBC suporta notificação assíncrona ligando para [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md). O Gerenciador de Driver sdbc, consequentemente, chamará o **SQLGetInfo** do driver com SQL_ASYNC_NOTIFICATION.  
  
```  
SQLUINTEGER InfoValue;  
SQLLEN      cbInfoLength;  
  
SQLRETURN retcode;  
retcode = SQLGetInfo (hDbc,   
                      SQL_ASYNC_NOTIFICATION,   
                      &InfoValue,  
                      sizeof(InfoValue),  
                      NULL);  
if (SQL_SUCCEEDED(retcode))  
{  
if (SQL_ASYNC_NOTIFICATION_CAPABLE == InfoValue)  
      {  
          // The driver supports asynchronous notification  
      }  
      else if (SQL_ASYNC_NOTIFICATION_NOT_CAPABLE == InfoValue)  
      {  
          // The driver does not support asynchronous notification  
      }  
}  
```  
  
### <a name="associating-a-win32-event-handle-with-an-odbc-handle"></a>Associando uma alça de evento Win32 com uma alça ODBC  
 Os aplicativos são responsáveis pela criação de objetos de evento Win32 usando as funções Win32 correspondentes. Um aplicativo pode associar uma alça de evento Win32 com uma alça de conexão ODBC ou uma alça de declaração ODBC.  
  
 Os atributos de conexão SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE e SQL_ATTR_ASYNC_DBC_EVENT determinar se o ODBC é executado no modo assíncrono e se o ODBC habilita o modo de notificação para uma alça de conexão. Os atributos de declaração SQL_ATTR_ASYNC_ENABLE e SQL_ATTR_ASYNC_STMT_EVENT determinar se o ODBC é executado no modo assíncrono e se o ODBC habilita o modo de notificação para uma alça de declaração.  
  
|SQL_ATTR_ASYNC_ENABLE ou SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE|SQL_ATTR_ASYNC_STMT_EVENT ou SQL_ATTR_ASYNC_DBC_EVENT|Mode|  
|-------------------------------------------------------------------------|-------------------------------------------------------------------|----------|  
|Habilitar|não-nulo|Notificação Assíncrona|  
|Habilitar|nulo|Votação Assíncrona|  
|Desabilitar|any|Síncrona|  
  
 Um aplicativo pode desativar temporalmente o modo de operação assíncrona. O ODBC ignora os valores de SQL_ATTR_ASYNC_DBC_EVENT se a operação assíncrona do nível de conexão estiver desativada. O ODBC ignora os valores de SQL_ATTR_ASYNC_STMT_EVENT se a operação assíncrona do nível de declaração estiver desativada.  
  
 Chamada síncrona de **SQLSetStmtAttr** e **SQLSetConnectAttr**  
 -   **O SQLSetConnectAttr** suporta operações assíncronas, mas a invocação do **SQLSetConnectAttr** para definir SQL_ATTR_ASYNC_DBC_EVENT é sempre síncrona.  
  
-   **SQLSetStmtAttr** não suporta execução assíncrona.  
  
 Cenário de saída de erros  
 Quando **o SQLSetConnectAttr** é chamado antes de fazer uma conexão, o Gerenciador de driver não pode determinar qual driver usar. Portanto, o Driver Manager retorna o sucesso para **SQLSetConnectAttr,** mas o atributo pode não estar pronto para definir no driver. O Gerenciador de driver definirá esses atributos quando o aplicativo chamar uma função de conexão. O Driver Manager pode errar porque o driver não suporta operações assíncronas.  
  
 Herança de atributos de conexão  
 Normalmente, as declarações de uma conexão herdarão os atributos de conexão. No entanto, o atributo SQL_ATTR_ASYNC_DBC_EVENT não é hereditário e afeta apenas as operações de conexão.  
  
 Para associar uma alça de evento a uma alça de conexão ODBC, um aplicativo ODBC chama o ODBC API **SQLSetConnectAttr** e especifica SQL_ATTR_ASYNC_DBC_EVENT como o atributo e o cabo de evento como o valor do atributo. O novo atributo ODBC SQL_ATTR_ASYNC_DBC_EVENT é de tipo SQL_IS_POINTER.  
  
```  
HANDLE hEvent;  
hEvent = CreateEvent(   
            NULL,                // default security attributes  
            FALSE,               // auto-reset event  
            FALSE,               // initial state is non-signaled  
            NULL                 // no name  
            );  
```  
  
 Normalmente, os aplicativos criam objetos de evento de reset automático. O ODBC não reiniciará o objeto de evento. Os aplicativos devem certificar-se de que o objeto não está em estado sinalizado antes de chamar qualquer função ODBC assíncrona.  
  
```  
SQLRETURN retcode;  
retcode = SQLSetConnectAttr ( hDBC,  
                              SQL_ATTR_ASYNC_DBC_EVENT, // Attribute name  
                              (SQLPOINTER) hEvent,      // Win32 Event handle  
                              SQL_IS_POINTER);          // Length Indicator  
```  
  
 SQL_ATTR_ASYNC_DBC_EVENT é um atributo somente driver manager que não será definido no driver.  
  
 O valor padrão do SQL_ATTR_ASYNC_DBC_EVENT é NULO. Se o driver não suportar notificação assíncrona, a obtenção ou configuração SQL_ATTR_ASYNC_DBC_EVENT retornará SQL_ERROR com o SQLSTATE HY092 (identificador de atributo/opção inválido).  
  
 Se o último valor SQL_ATTR_ASYNC_DBC_EVENT definido em uma alça de conexão ODBC não for NULO e o aplicativo habilitado para o modo assíncrono, definindo SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE atributo com SQL_ASYNC_DBC_ENABLE_ON, chamar qualquer função de conexão ODBC que suporte o modo assíncrono receberá uma notificação de conclusão. Se o último valor de SQL_ATTR_ASYNC_DBC_EVENT definido em uma alça de conexão ODBC for NULO, a ODBC não enviará ao aplicativo qualquer notificação, independentemente de o modo assíncrono estar ativado.  
  
 Um aplicativo pode definir SQL_ATTR_ASYNC_DBC_EVENT antes ou depois de definir o atributo SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE.  
  
 Os aplicativos podem definir o atributo SQL_ATTR_ASYNC_DBC_EVENT em uma alça de conexão ODBC antes de chamar uma função de conexão **(SQLConnect,** **SQLBrowseConnect**ou **SQLDriverConnect).** Como o Gerenciador de Driver saque o ODBC não sabe qual driver ODBC o aplicativo usará, ele voltará SQL_SUCCESS. Quando o aplicativo chama uma função de conexão, o Gerenciador de Driver oDBC verificará se o driver suporta notificação assíncrona. Se o driver não suportar notificação assíncrona, o Gerenciador de Driver ODBC retornará SQL_ERROR com o SQLSTATE S1_118 (driver não suporta notificação assíncrona). Se o driver suportar uma notificação assíncrona, o Gerenciador de Driver ODBC ligará para o motorista e definirá os atributos correspondentes SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK e SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT.  
  
 Da mesma forma, um aplicativo chama **SQLSetStmtAttr** em uma alça de declaração ODBC e especifica o atributo SQL_ATTR_ASYNC_STMT_EVENT para ativar ou desativar a notificação assíncrona do nível de declaração. Como uma função de instrução é sempre chamada após a conexão ser estabelecida, **o SQLSetStmtAttr** retornará SQL_ERROR com o SQLSTATE S1_118 (driver não suporta notificação assíncrona) imediatamente se o driver correspondente não suportar operações assíncronas ou o driver suportar operação assíncrona, mas não suportar notificação assíncrona.  
  
```  
SQLRETURN retcode;  
retcode = SQLSetStmtAttr ( hSTMT,  
                           SQL_ATTR_ASYNC_STMT_EVENT, // Attribute name   
                           (SQLPOINTER) hEvent,       // Win32 Event handle  
                           SQL_IS_POINTER);           // length Indicator  
```  
  
 SQL_ATTR_ASYNC_STMT_EVENT, que pode ser definido como NULL, é um atributo somente driver Manager que não será definido no driver.  
  
 O valor padrão de SQL_ATTR_ASYNC_STMT_EVENT é NULA. Se o driver não suportar notificação assíncrona, obter ou definir o atributo SQL_ATTR_ASYNC_ STMT_EVENT retornará SQL_ERROR com sQLSTATE HY092 (identificador de atributo/opção inválido).  
  
 Um aplicativo não deve associar a mesma alça de evento com mais de uma alça ODBC. Caso contrário, uma notificação será perdida se duas invocações de função ODBC assíncronas forem concluídas em duas alças que compartilham a mesma alça de evento. Para evitar que uma alça de declaração herde a mesma alça de evento da alça de conexão, o ODBC retorna SQL_ERROR com o SQLSTATE IM016 (Não é possível definir o atributo de declaração no cabo de conexão) se um aplicativo definir SQL_ATTR_ASYNC_STMT_EVENT em uma alça de conexão.  
  
### <a name="calling-asynchronous-odbc-functions"></a>Chamando funções ODBC assíncronas  
 Depois de ativar a notificação assíncrona e iniciar uma operação assíncrona, o aplicativo pode chamar qualquer função ODBC. Se a função pertencer ao conjunto de funções que suportam a operação assíncrona, o aplicativo receberá uma notificação de conclusão quando a operação for concluída, independentemente de a função ter falhado ou sido bem sucedida.  A única exceção é que o aplicativo chama uma função ODBC com uma conexão inválida ou alça de declaração. Neste caso, a ODBC não vai pegar a alça do evento e configurá-la para o estado sinalizado.  
  
 O aplicativo deve garantir que o objeto de evento associado esteja em um estado não sinalizado antes de iniciar uma operação assíncrona na alça ODBC correspondente. O ODBC não reiniciará o objeto de evento.  
  
### <a name="getting-notification-from-odbc"></a>Obtendo notificação da ODBC  
 Um segmento de aplicativo pode chamar **waitForSingleObject** para aguardar em uma alça de evento ou chamar **WaitForMultipleObjects** para esperar em uma matriz de alças de evento e ser suspenso até que um ou todos os objetos de evento sejam sinalizados ou o intervalo de tempo de tempo se esgote.  
  
```  
DWORD dwStatus = WaitForSingleObject(  
                        hEvent,  // The event associated with the ODBC handle  
                        5000     // timeout is 5000 millisecond   
);  
  
If (dwStatus == WAIT_TIMEOUT)  
{  
    // time-out interval elapsed before all the events are signaled.   
}  
Else  
{  
    // Call the corresponding Asynchronous ODBC API to complete all processing and retrieve the return code.  
}  
```
