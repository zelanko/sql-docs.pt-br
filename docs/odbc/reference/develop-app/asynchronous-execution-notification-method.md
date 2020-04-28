---
title: Execução assíncrona (método de notificação) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306407"
---
# <a name="asynchronous-execution-notification-method"></a>Execução assíncrona (método de notificação)
O ODBC permite a execução assíncrona de operações de conexão e instrução. Um thread de aplicativo pode chamar uma função ODBC no modo assíncrono e a função pode retornar antes que a operação seja concluída, permitindo que o thread do aplicativo execute outras tarefas. No SDK do Windows 7, para instruções assíncronas ou operações de conexão, um aplicativo determinou que a operação assíncrona foi concluída usando o método de sondagem. Para obter mais informações, consulte [execução assíncrona (método de sondagem)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md). A partir do SDK do Windows 8, você pode determinar que uma operação assíncrona seja concluída usando o método de notificação.  
  
 No método de sondagem, os aplicativos precisam chamar a função assíncrona cada vez que quiserem o status da operação. O método de notificação é semelhante ao retorno de chamada e aguardar em ADO.NET. O ODBC, no entanto, usa eventos Win32 como o objeto de notificação.  
  
 A biblioteca de cursores ODBC e a notificação assíncrona ODBC não podem ser usadas ao mesmo tempo. Definir ambos os atributos retornará um erro com SQLSTATE S1119 (a biblioteca de cursores e a notificação assíncrona não podem ser habilitadas ao mesmo tempo).  
  
 Consulte [notificação de conclusão de função assíncrona](../../../odbc/reference/develop-driver/notification-of-asynchronous-function-completion.md) para obter informações para desenvolvedores de driver.  
  
> [!NOTE]  
>  Não há suporte para o método de notificação com a biblioteca de cursores. Um aplicativo receberá uma mensagem de erro se tentar habilitar a biblioteca de cursores via SQLSetConnectAttr, quando o método de notificação estiver habilitado.  
  
## <a name="overview"></a>Visão geral  
 Quando uma função ODBC é chamada no modo assíncrono, o controle é retornado para o aplicativo de chamada imediatamente com o código de retorno SQL_STILL_EXECUTING. O aplicativo deve sondar a função repetidamente até que ela retorne algo diferente de SQL_STILL_EXECUTING. O loop de sondagem aumenta a utilização da CPU, causando baixo desempenho em muitos cenários assíncronos.  
  
 Sempre que o modelo de notificação for usado, o modelo de sondagem será desabilitado. Os aplicativos não devem chamar a função original novamente. Chame a [função SQLCompleteAsync](../../../odbc/reference/syntax/sqlcompleteasync-function.md) para concluir a operação assíncrona. Se um aplicativo chamar a função original novamente antes que a operação assíncrona seja concluída, a chamada retornará SQL_ERROR com SQLSTATE IM017 (a sondagem será desabilitada no modo de notificação assíncrona).  
  
 Ao usar o modelo de notificação, o aplicativo pode chamar **SQLCancel** ou **SQLCancelHandle** para cancelar uma operação de instrução ou de conexão. Se a solicitação de cancelamento for bem-sucedida, o ODBC retornará SQL_SUCCESS. Essa mensagem não indica que a função foi realmente cancelada; Isso indica que a solicitação de cancelamento foi processada. Se a função realmente cancelada é dependente de driver e depende da fonte de dados. Quando uma operação é cancelada, o Gerenciador de driver ainda sinalizará o evento. O Gerenciador de driver retorna SQL_ERROR no buffer de código de retorno e o estado é SQLSTATE HY008 (operação cancelada) para indicar que o cancelamento foi bem-sucedido. Se a função tiver concluído seu processamento normal, o Gerenciador de driver retornará SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO.  
  
### <a name="downlevel-behavior"></a>Comportamento de nível inferior  
 A versão do Gerenciador de driver ODBC que dá suporte a essa notificação na conclusão é ODBC 3,81.  
  
|Versão do ODBC do aplicativo|Versão do Gerenciador de driver|Versão do driver|Comportamento|  
|------------------------------|----------------------------|--------------------|--------------|  
|Novo aplicativo de qualquer versão do ODBC|ODBC 3,81|Driver ODBC 3,80|O aplicativo poderá usar esse recurso se o driver oferecer suporte a esse recurso, caso contrário, o Gerenciador de driver apresentará um erro.|  
|Novo aplicativo de qualquer versão do ODBC|ODBC 3,81|Driver anterior ao ODBC 3,80|O Gerenciador de driver apresentará um erro se o driver não oferecer suporte a esse recurso.|  
|Novo aplicativo de qualquer versão do ODBC|Pré-ODBC 3,81|Qualquer|Quando o aplicativo usar esse recurso, um Gerenciador de driver antigo considerará os novos atributos como atributos específicos do driver e o driver deverá gerar um erro. Um novo Gerenciador de driver não passará esses atributos para o driver.|  
  
 Um aplicativo deve verificar a versão do Gerenciador de driver antes de usar esse recurso. Caso contrário, se um driver mal escrito não tiver erro e a versão do Gerenciador de driver for pré-ODBC 3,81, o comportamento será indefinido.  
  
## <a name="use-cases"></a>Casos de uso  
 Esta seção mostra casos de uso para execução assíncrona e o mecanismo de sondagem.  
  
### <a name="integrate-data-from-multiple-odbc-sources"></a>Integrar dados de várias fontes ODBC  
 Um aplicativo de integração de dados busca de forma assíncrona dados de várias fontes de dados. Alguns dos dados são de fontes de dados remotas e alguns dados são de arquivos locais. O aplicativo não pode continuar até que as operações assíncronas sejam concluídas.  
  
 Em vez de sondar repetidamente uma operação para determinar se ela está concluída, o aplicativo pode criar um objeto de evento e associá-lo a um identificador de conexão ODBC ou a um identificador de instrução ODBC. Em seguida, o aplicativo chama as APIs de sincronização do sistema operacional para aguardar um objeto de evento ou muitos objetos de evento (tanto eventos ODBC quanto outros eventos do Windows). O ODBC sinalizará o objeto de evento quando a operação assíncrona de ODBC correspondente for concluída.  
  
 No Windows, os objetos de evento do Win32 serão usados e fornecerão ao usuário um modelo de programação unificado. Os gerenciadores de driver em outras plataformas podem usar a implementação do objeto de evento específica para essas plataformas.  
  
 O exemplo de código a seguir demonstra o uso da notificação assíncrona de conexão e instrução:  
  
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
  
### <a name="determining-if-a-driver-supports-asynchronous-notification"></a>Determinando se um driver dá suporte à notificação assíncrona  
 Um aplicativo ODBC pode determinar se um driver ODBC dá suporte à notificação assíncrona chamando [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md). O Gerenciador de driver ODBC, consequentemente, chamará o **SQLGetInfo** do driver com SQL_ASYNC_NOTIFICATION.  
  
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
  
### <a name="associating-a-win32-event-handle-with-an-odbc-handle"></a>Associando um manipulador de eventos do Win32 a um identificador ODBC  
 Os aplicativos são responsáveis pela criação de objetos de evento do Win32 usando as funções do Win32 correspondentes. Um aplicativo pode associar um identificador de evento do Win32 a um identificador de conexão ODBC ou a um identificador de instrução ODBC.  
  
 Os atributos de conexão SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE e SQL_ATTR_ASYNC_DBC_EVENT determinam se o ODBC é executado no modo assíncrono e se o ODBC habilita o modo de notificação para um identificador de conexão. Os atributos de instrução SQL_ATTR_ASYNC_ENABLE e SQL_ATTR_ASYNC_STMT_EVENT determinam se o ODBC é executado no modo assíncrono e se o ODBC habilita o modo de notificação para um identificador de instrução.  
  
|SQL_ATTR_ASYNC_ENABLE ou SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE|SQL_ATTR_ASYNC_STMT_EVENT ou SQL_ATTR_ASYNC_DBC_EVENT|Mode|  
|-------------------------------------------------------------------------|-------------------------------------------------------------------|----------|  
|Habilitar|não nulo|Notificação assíncrona|  
|Habilitar|null|Sondagem assíncrona|  
|Desabilitar|any|Síncrona|  
  
 Um aplicativo pode desabilitar o modo de operação assíncrona temporal. O ODBC ignora valores de SQL_ATTR_ASYNC_DBC_EVENT se a operação assíncrona de nível de conexão estiver desabilitada. O ODBC ignora valores de SQL_ATTR_ASYNC_STMT_EVENT se a operação assíncrona de nível de instrução estiver desabilitada.  
  
 Chamada síncrona de **SQLSetStmtAttr** e **SQLSetConnectAttr**  
 -   O **SQLSetConnectAttr** dá suporte a operações assíncronas, mas a invocação de **SQLSetConnectAttr** para definir SQL_ATTR_ASYNC_DBC_EVENT é sempre síncrona.  
  
-   **SQLSetStmtAttr** não oferece suporte à execução assíncrona.  
  
 Cenário de erro  
 Quando **SQLSetConnectAttr** é chamado antes de fazer uma conexão, o Gerenciador de driver não pode determinar qual driver usar. Portanto, o Gerenciador de driver retorna êxito para **SQLSetConnectAttr** , mas o atributo pode não estar pronto para ser definido no driver. O Gerenciador de driver definirá esses atributos quando o aplicativo chamar uma função de conexão. O Gerenciador de driver pode ter um erro, pois o driver não oferece suporte a operações assíncronas.  
  
 Herança de atributos de conexão  
 Normalmente, as instruções de uma conexão herdarão os atributos de conexão. No entanto, o atributo SQL_ATTR_ASYNC_DBC_EVENT não é herdável e só afeta as operações de conexão.  
  
 Para associar um identificador de evento a um identificador de conexão ODBC, um aplicativo ODBC chama a API ODBC **SQLSetConnectAttr** e especifica SQL_ATTR_ASYNC_DBC_EVENT como o atributo e o identificador de evento como o valor do atributo. O novo atributo ODBC SQL_ATTR_ASYNC_DBC_EVENT é do tipo SQL_IS_POINTER.  
  
```  
HANDLE hEvent;  
hEvent = CreateEvent(   
            NULL,                // default security attributes  
            FALSE,               // auto-reset event  
            FALSE,               // initial state is non-signaled  
            NULL                 // no name  
            );  
```  
  
 Normalmente, os aplicativos criam objetos de evento de redefinição automática. O ODBC não redefinirá o objeto de evento. Os aplicativos devem garantir que o objeto não esteja no estado sinalizado antes de chamar qualquer função ODBC assíncrona.  
  
```  
SQLRETURN retcode;  
retcode = SQLSetConnectAttr ( hDBC,  
                              SQL_ATTR_ASYNC_DBC_EVENT, // Attribute name  
                              (SQLPOINTER) hEvent,      // Win32 Event handle  
                              SQL_IS_POINTER);          // Length Indicator  
```  
  
 SQL_ATTR_ASYNC_DBC_EVENT é um atributo somente do Gerenciador de driver que não será definido no driver.  
  
 O valor padrão de SQL_ATTR_ASYNC_DBC_EVENT é NULL. Se o driver não oferecer suporte à notificação assíncrona, obter ou definir SQL_ATTR_ASYNC_DBC_EVENT retornará SQL_ERROR com SQLSTATE HY092 (identificador de atributo/opção inválido).  
  
 Se o último valor de SQL_ATTR_ASYNC_DBC_EVENT definido em um identificador de conexão ODBC não for nulo e o modo assíncrono habilitado para aplicativo ao definir o atributo SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE com SQL_ASYNC_DBC_ENABLE_ON, chamar qualquer função de conexão ODBC que dê suporte ao modo assíncrono receberá uma notificação de conclusão. Se o último valor de SQL_ATTR_ASYNC_DBC_EVENT definido em um identificador de conexão ODBC for nulo, o ODBC não enviará o aplicativo a qualquer notificação, independentemente se o modo assíncrono estiver habilitado.  
  
 Um aplicativo pode definir SQL_ATTR_ASYNC_DBC_EVENT antes ou depois de definir o atributo SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE.  
  
 Os aplicativos podem definir o atributo SQL_ATTR_ASYNC_DBC_EVENT em um identificador de conexão ODBC antes de chamar uma função de conexão (**SQLConnect**, **SQLBrowseConnect**ou **SQLDriverConnect**). Como o Gerenciador de driver ODBC não sabe qual driver ODBC será usado pelo aplicativo, ele retornará SQL_SUCCESS. Quando o aplicativo chamar uma função de conexão, o Gerenciador de driver ODBC verificará se o driver dá suporte à notificação assíncrona. Se o driver não oferecer suporte à notificação assíncrona, o Gerenciador de driver ODBC retornará SQL_ERROR com SQLSTATE S1_118 (o driver não oferece suporte à notificação assíncrona). Se o driver oferecer suporte à notificação assíncrona, o Gerenciador de driver ODBC chamará o driver e definirá os atributos correspondentes SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK e SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT.  
  
 Da mesma forma, um aplicativo chama **SQLSetStmtAttr** em um identificador de instrução ODBC e especifica o atributo SQL_ATTR_ASYNC_STMT_EVENT para habilitar ou desabilitar a notificação assíncrona em nível de instrução. Como uma função de instrução é sempre chamada depois que a conexão é estabelecida, **SQLSetStmtAttr** retornará SQL_ERROR com SQLSTATE S1_118 (o driver não oferece suporte à notificação assíncrona) imediatamente se o driver correspondente não oferecer suporte a operações assíncronas ou o driver oferecer suporte à operação assíncrona, mas não oferecer suporte à notificação assíncrona.  
  
```  
SQLRETURN retcode;  
retcode = SQLSetStmtAttr ( hSTMT,  
                           SQL_ATTR_ASYNC_STMT_EVENT, // Attribute name   
                           (SQLPOINTER) hEvent,       // Win32 Event handle  
                           SQL_IS_POINTER);           // length Indicator  
```  
  
 SQL_ATTR_ASYNC_STMT_EVENT, que pode ser definido como NULL, é um atributo somente do Gerenciador de driver que não será definido no driver.  
  
 O valor padrão de SQL_ATTR_ASYNC_STMT_EVENT é NULL. Se o driver não oferecer suporte à notificação assíncrona, obter ou definir o atributo de STMT_EVENT de SQL_ATTR_ASYNC_ retornará SQL_ERROR com SQLSTATE HY092 (identificador de atributo/opção inválido).  
  
 Um aplicativo não deve associar o mesmo identificador de evento a mais de um identificador ODBC. Caso contrário, uma notificação será perdida se duas invocações de função ODBC assíncronas forem concluídas em dois identificadores que compartilham o mesmo identificador de evento. Para evitar um identificador de instrução que herde o mesmo identificador de evento do identificador de conexão, o ODBC retorna SQL_ERROR com SQLSTATE IM016 (não é possível definir o atributo de instrução no identificador de conexão) se um aplicativo definir SQL_ATTR_ASYNC_STMT_EVENT em um identificador de conexão.  
  
### <a name="calling-asynchronous-odbc-functions"></a>Chamando funções ODBC assíncronas  
 Depois de habilitar a notificação assíncrona e iniciar uma operação assíncrona, o aplicativo pode chamar qualquer função ODBC. Se a função pertencer ao conjunto de funções que dão suporte à operação assíncrona, o aplicativo receberá uma notificação de conclusão quando a operação for concluída, independentemente de a função ter falhado ou bem-sucedida.  A única exceção é que o aplicativo chama uma função ODBC com um identificador de conexão ou instrução inválido. Nesse caso, o ODBC não obterá o identificador de eventos e o definirá como o estado sinalizado.  
  
 O aplicativo deve garantir que o objeto de evento associado esteja em um estado não sinalizado antes de iniciar uma operação assíncrona no identificador ODBC correspondente. O ODBC não redefinirá o objeto de evento.  
  
### <a name="getting-notification-from-odbc"></a>Obtendo notificação do ODBC  
 Um thread de aplicativo pode chamar **WaitForSingleObject** para aguardar um identificador de evento ou chamar **WaitForMultipleObjects** para aguardar em uma matriz de identificadores de eventos e ser suspenso até que um ou todos os objetos de evento sejam sinalizados ou o intervalo de tempo limite decorrido.  
  
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
