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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ec4b197c6c9588194531c2cc29ee1ba79d51fa6e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47669484"
---
# <a name="asynchronous-execution-notification-method"></a>Execução assíncrona (método de notificação)
ODBC permite que a execução assíncrona da conexão e as operações de instrução. Um thread de aplicativo pode chamar uma função ODBC no modo assíncrono e a função pode retornar antes da operação for concluída, permitindo que o thread do aplicativo realizar outras tarefas. No SDK do Windows 7, para as operações de conexão, ou instrução assíncrona um aplicativo determinado que a operação assíncrona foi concluída usando o método de sondagem. Para obter mais informações, consulte [execução assíncrona (método de sondagem)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md). A partir do SDK do Windows 8, você pode determinar que uma operação assíncrona foi concluída usando o método de notificação.  
  
 O método de sondagem, os aplicativos precisam chamar a função assíncrona cada vez que ele deseja que o status da operação. O método de notificação é semelhante ao retorno de chamada e espera no ADO.NET. No entanto, o ODBC, usa os eventos do Win32 como o objeto de notificação.  
  
 A biblioteca de cursores ODBC e notificação assíncrona de ODBC não podem ser usados ao mesmo tempo. Configuração de ambos os atributos retornará um erro com SQLSTATE S1119 (biblioteca de cursores e notificação assíncrona não podem ser habilitado ao mesmo tempo).  
  
 Ver [notificação de conclusão de função assíncrona](../../../odbc/reference/develop-driver/notification-of-asynchronous-function-completion.md) para obter informações para desenvolvedores de driver.  
  
> [!NOTE]  
>  Não há suporte para o método de notificação com a biblioteca de cursores. Um aplicativo receberá a mensagem de erro se tentar habilitar a biblioteca de cursores por meio do SQLSetConnectAttr, quando o método de notificação está habilitado.  
  
## <a name="overview"></a>Visão geral  
 Quando uma função ODBC é chamada no modo assíncrono, o controle é retornado ao aplicativo de chamada imediatamente com o código de retorno SQL_STILL_EXECUTING. O aplicativo repetidamente deve sondar a função até ele retornar algo diferente de SQL_STILL_EXECUTING. O loop de sondagem aumenta a utilização de CPU, fazendo com que o desempenho insatisfatório em muitos cenários assíncronos.  
  
 Sempre que o modelo de notificação é usado, o modelo de sondagem está desabilitado. Aplicativos não devem chamar a função original novamente. Chame [função SQLCompleteAsync](../../../odbc/reference/syntax/sqlcompleteasync-function.md) para concluir a operação assíncrona. Se um aplicativo chama a função original novamente antes da operação assíncrona for concluída, a chamada retornará SQL_ERROR com SQLSTATE IM017 (sondagem está desabilitada no modo de notificação assíncrona).  
  
 Ao usar o modelo de notificação, o aplicativo pode chamar **SQLCancel** ou **SQLCancelHandle** para cancelar uma operação de instrução ou a conexão. Se a solicitação de cancelamento for bem-sucedida, o ODBC retornará SQL_SUCCESS. Esta mensagem não indica que a função, na verdade, foi cancelada; ele indica que a solicitação de cancelamento foi processada. Se a função, na verdade, é cancelada é dependente do driver e dependente da fonte de dados. Quando uma operação é cancelada, o Gerenciador de Driver ainda sinalizará o evento. O Gerenciador de Driver retornará SQL_ERROR em buffer o código de retorno e o estado é SQLSTATE HY008 (operação cancelada) para indicar o cancelamento foi bem-sucedido. Se a função concluir seu processamento normal, o Gerenciador de Driver retorna SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO.  
  
### <a name="downlevel-behavior"></a>Comportamento de nível inferior  
 A versão do Gerenciador de Driver ODBC que dão suporte a essa notificação em completa é 3.81 ODBC.  
  
|Versão do aplicativo ODBC|Versão do Gerenciador de driver|Versão do driver|Comportamento|  
|------------------------------|----------------------------|--------------------|--------------|  
|Novo aplicativo de qualquer versão do ODBC|ODBC 3.81|ODBC 3,80 Driver|Aplicativo pode usar esse recurso se o driver dá suporte a esse recurso, caso contrário, o Gerenciador de Driver apresentará um erro.|  
|Novo aplicativo de qualquer versão do ODBC|ODBC 3.81|Driver ODBC 3,80 pré-|O Gerenciador de Driver apresentará um erro se o driver não dá suporte a esse recurso.|  
|Novo aplicativo de qualquer versão do ODBC|Pré-ODBC 3.81|Any (qualquer)|Quando o aplicativo usa esse recurso, um Gerenciador de Driver antigo classificará os novos atributos como atributos específicos do driver e o driver deve a um erro. Um novo Gerenciador de Driver não passa esses atributos para o driver.|  
  
 Um aplicativo deve verificar a versão do Gerenciador de Driver antes de usar esse recurso. Caso contrário, se um driver mal escrito não faz erro e a versão do Gerenciador de Driver é pré 3.81 ODBC, o comportamento será indefinido.  
  
## <a name="use-cases"></a>Casos de uso  
 Esta seção mostra casos de uso para a execução assíncrona e o mecanismo de sondagem.  
  
### <a name="integrate-data-from-multiple-odbc-sources"></a>Integrar dados de várias fontes ODBC  
 Um aplicativo de integração de dados assincronamente busca dados de várias fontes de dados. Alguns dos dados são de fontes de dados remotos e alguns dados são de arquivos locais. O aplicativo não pode continuar até que as operações assíncronas sejam concluídas.  
  
 Em vez de consultar repetidamente uma operação para determinar se ela for concluída, o aplicativo pode criar um objeto de evento e associá-la com um identificador de conexão ODBC ou um identificador de instrução ODBC. O aplicativo, em seguida, chama APIs de espera em vários objetos de evento (eventos ODBC e outros eventos do Windows) ou o objeto de um evento de sincronização do sistema operacional. ODBC sinalizará o objeto de evento quando a operação assíncrona correspondente do ODBC é concluída.  
  
 No Windows, os objetos de evento Win32 serão usados e que fornecerá ao usuário um modelo de programação unificado. Os gerentes de driver em outras plataformas podem usar a implementação do objeto de evento específica para essas plataformas.  
  
 O exemplo de código a seguir demonstra o uso de conexão e notificação assíncrona de instrução:  
  
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
  
### <a name="determining-if-a-driver-supports-asynchronous-notification"></a>Determinando se um Driver dá suporte à notificação assíncrona  
 Um aplicativo ODBC pode determinar se um driver ODBC dá suporte à notificação assíncrona chamando [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md). O Gerenciador de Driver ODBC, consequentemente, chamará o **SQLGetInfo** do driver com SQL_ASYNC_NOTIFICATION.  
  
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
  
### <a name="associating-a-win32-event-handle-with-an-odbc-handle"></a>Associando um identificador de evento do Win32 com um identificador de ODBC  
 Aplicativos são responsáveis pela criação de objetos de evento do Win32 usando as funções do Win32 correspondentes. Um aplicativo pode associar um identificador de evento do Win32 com um identificador de conexão ODBC ou um identificador de instrução ODBC.  
  
 Atributos de Conexão SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE e SQL_ATTR_ASYNC_DBC_EVENT determinam se o ODBC é executado no modo assíncrono e se o ODBC habilita o modo de notificação para um identificador de conexão. Atributos de instrução SQL_ATTR_ASYNC_ENABLE e SQL_ATTR_ASYNC_STMT_EVENT determinam se o ODBC é executado no modo assíncrono e se o ODBC habilita o modo de notificação para um identificador de instrução.  
  
|SQL_ATTR_ASYNC_ENABLE ou SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE|SQL_ATTR_ASYNC_STMT_EVENT ou SQL_ATTR_ASYNC_DBC_EVENT|Modo|  
|-------------------------------------------------------------------------|-------------------------------------------------------------------|----------|  
|Habilitar|não nulo|Notificação assíncrona|  
|Habilitar|nulo|Sondagem assíncrono|  
|Disable|any|Síncrona|  
  
 Um aplicativo temporariamente pode desabilitar o modo de operação assíncrona. ODBC ignora valores de SQL_ATTR_ASYNC_DBC_EVENT se a operação assíncrona em nível de conexão está desabilitada. ODBC ignora valores de SQL_ATTR_ASYNC_STMT_EVENT se a operação assíncrona em nível de instrução estiver desabilitada.  
  
 Chamada síncrona de **SQLSetStmtAttr** e **SQLSetConnectAttr**  
 -   **SQLSetConnectAttr** dá suporte a operações assíncronas, mas a invocação de **SQLSetConnectAttr** definir SQL_ATTR_ASYNC_DBC_EVENT sempre é síncrono.  
  
-   **SQLSetStmtAttr** não oferece suporte a execução assíncrona.  
  
 Cenário de saída de erro  
 Quando **SQLSetConnectAttr** é chamado antes de fazer uma conexão, o Gerenciador de Driver não pode determinar qual driver a ser usado. Portanto, o Gerenciador de Driver retorna sucesso para **SQLSetConnectAttr** , mas o atributo não pode estar pronto para definir no driver. O Gerenciador de Driver definirá esses atributos quando o aplicativo chama uma função de conexão. O Gerenciador de Driver pode saída de erro porque o driver não oferece suporte a operações assíncronas.  
  
 Herança de atributos de conexão  
 Geralmente, as declarações de uma conexão herdará os atributos de conexão. No entanto, o atributo SQL_ATTR_ASYNC_DBC_EVENT não é herdável e só afeta as operações de conexão.  
  
 Para associar um identificador de eventos com um identificador de conexão ODBC, um aplicativo ODBC chama a API do ODBC **SQLSetConnectAttr** e especifica SQL_ATTR_ASYNC_DBC_EVENT como lidar com o atributo e o evento como o valor do atributo. O novo atributo ODBC SQL_ATTR_ASYNC_DBC_EVENT é do tipo SQL_IS_POINTER.  
  
```  
HANDLE hEvent;  
hEvent = CreateEvent(   
            NULL,                // default security attributes  
            FALSE,               // auto-reset event  
            FALSE,               // initial state is non-signaled  
            NULL                 // no name  
            );  
```  
  
 Normalmente, os aplicativos criam objetos de evento de redefinição automática. ODBC não redefinirão o objeto de evento. Aplicativos devem fazer se o objeto não está no estado sinalizado antes de chamar qualquer função ODBC assíncrona.  
  
```  
SQLRETURN retcode;  
retcode = SQLSetConnectAttr ( hDBC,  
                              SQL_ATTR_ASYNC_DBC_EVENT, // Attribute name  
                              (SQLPOINTER) hEvent,      // Win32 Event handle  
                              SQL_IS_POINTER);          // Length Indicator  
```  
  
 SQL_ATTR_ASYNC_DBC_EVENT é um atributo de somente do Gerenciador de Driver que não será definido no driver.  
  
 O valor padrão de SQL_ATTR_ASYNC_DBC_EVENT é NULL. Se o driver não oferece suporte a notificação assíncrona, obter ou definir SQL_ATTR_ASYNC_DBC_EVENT retornará SQL_ERROR com SQLSTATE HY092 (identificador de atributo/opção inválido).  
  
 Se o último valor SQL_ATTR_ASYNC_DBC_EVENT definida em um identificador de conexão ODBC não for NULL, e o aplicativo habilitado modo assíncrono, definindo o atributo SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE com SQL_ASYNC_DBC_ENABLE_ON, chamar qualquer conexão de ODBC função que dá suporte ao modo assíncrono receberá uma notificação de conclusão. Se o último valor SQL_ATTR_ASYNC_DBC_EVENT definido em um identificador de conexão ODBC for NULL, ODBC não enviará o aplicativo qualquer notificação, independentemente se o modo assíncrono está habilitado.  
  
 Um aplicativo pode definir SQL_ATTR_ASYNC_DBC_EVENT antes ou depois de definir o atributo SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE.  
  
 Aplicativos podem definir o atributo SQL_ATTR_ASYNC_DBC_EVENT em um identificador de conexão ODBC antes de chamar uma função de conexão (**SQLConnect**, **SQLBrowseConnect**, ou  **SQLDriverConnect**). Como o Gerenciador de Driver ODBC não sabe qual driver ODBC, o aplicativo usará, ele retornará SQL_SUCCESS. Quando o aplicativo chama uma função de conexão, o Gerenciador de Driver ODBC verifica se o driver dá suporte à notificação assíncrona. Se o driver não oferece suporte a notificação assíncrona, o Gerenciador de Driver ODBC retornará SQL_ERROR com SQLSTATE S1_118 (Driver não oferece suporte a notificação assíncrona). Se o driver dá suporte à notificação assíncrona, o Gerenciador de Driver ODBC chamará o driver e definir os atributos correspondentes SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK e SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT.  
  
 Da mesma forma, um aplicativo chama **SQLSetStmtAttr** em uma instrução ODBC manipular e especifica o atributo SQL_ATTR_ASYNC_STMT_EVENT para habilitar ou desabilitar a notificação assíncrona nível de instrução. Como uma função de instrução sempre é chamada depois que a conexão é estabelecida, **SQLSetStmtAttr** retornará SQL_ERROR com SQLSTATE S1_118 (Driver não oferece suporte a notificação assíncrona) imediatamente se correspondente driver não oferece suporte a operações assíncronas ou o driver dá suporte à operação assíncrona, mas não oferece suporte a notificação assíncrona.  
  
```  
SQLRETURN retcode;  
retcode = SQLSetStmtAttr ( hSTMT,  
                           SQL_ATTR_ASYNC_STMT_EVENT, // Attribute name   
                           (SQLPOINTER) hEvent,       // Win32 Event handle  
                           SQL_IS_POINTER);           // length Indicator  
```  
  
 SQL_ATTR_ASYNC_STMT_EVENT, que pode ser definida como NULL, é um atributo de somente do Gerenciador de Driver que não será definido no driver.  
  
 O valor padrão de SQL_ATTR_ASYNC_STMT_EVENT é NULL. Se o driver não oferece suporte a notificação assíncrona, obter ou definir o atributo SQL_ATTR_ASYNC_ STMT_EVENT retornará SQL_ERROR com SQLSTATE HY092 (identificador de atributo/opção inválido).  
  
 Um aplicativo não deve associar o mesmo identificador de eventos com mais de um identificador ODBC. Caso contrário, uma notificação serão perdida se duas chamadas de função ODBC assíncronas é concluída em duas alças que compartilham o mesmo identificador de eventos. Para evitar um identificador de instrução, herdando o mesmo identificador de evento o identificador de conexão, o ODBC retornará SQL_ERROR com IM016 SQLSTATE (não é possível definir o atributo de instrução para o identificador de conexão) se um aplicativo define SQL_ATTR_ASYNC_STMT_EVENT em um identificador de conexão.  
  
### <a name="calling-asynchronous-odbc-functions"></a>Chamando funções ODBC assíncrona  
 Depois de habilitar a notificação assíncrona e iniciar uma operação assíncrona, o aplicativo pode chamar qualquer função ODBC. Se a função pertence ao conjunto de funções que dão suporte à operação assíncrona, o aplicativo receberá uma notificação de conclusão quando a operação for concluída, independentemente de se a função falhou ou foi bem-sucedida.  A única exceção é que o aplicativo chama uma função ODBC com um identificador de conexão ou instrução inválida. Nesse caso, ODBC não obter o identificador de evento e defini-lo para o estado sinalizado.  
  
 O aplicativo deve garantir que o objeto de evento associado está em um estado não sinalizado antes de iniciar uma operação assíncrona no identificador do ODBC correspondente. ODBC não redefinirão o objeto de evento.  
  
### <a name="getting-notification-from-odbc"></a>Obtendo a notificação de ODBC  
 Um thread de aplicativo pode chamar **WaitForSingleObject** para aguardar o identificador de um evento ou chamada **WaitForMultipleObjects** aguardar em uma matriz de identificadores de eventos e ser suspensa até que um ou todos os objetos de evento sinalizado ou o intervalo de tempo limite expire.  
  
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
