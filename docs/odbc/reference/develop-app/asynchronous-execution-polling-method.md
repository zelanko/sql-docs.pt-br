---
title: Execução assíncrona (método de sondagem) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- asynchronous execution [ODBC]
ms.assetid: 8cd21734-ef8e-4066-afd5-1f340e213f9c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a188c607c499e16652e314c67c37914f6cc9b85f
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87362764"
---
# <a name="asynchronous-execution-polling-method"></a>Execução assíncrona (Método de Sondagem)
Antes do ODBC 3,8 e do SDK do Windows 7, as operações assíncronas eram permitidas apenas em funções de instrução. Para obter mais informações, consulte a seção **executando operações de forma assíncrona**, mais adiante neste tópico.  
  
 O ODBC 3,8 no SDK do Windows 7 introduziu a execução assíncrona em operações relacionadas à conexão. Para obter mais informações, consulte a seção **executando operações de conexão assíncronas** , mais adiante neste tópico.  
  
 No SDK do Windows 7, para instruções assíncronas ou operações de conexão, um aplicativo determinou que a operação assíncrona foi concluída usando o método de sondagem. A partir do SDK do Windows 8, você pode determinar que uma operação assíncrona seja concluída usando o método de notificação. Para obter mais informações, consulte [execução assíncrona (método de notificação)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md).  
  
 Por padrão, os drivers executam funções ODBC de forma síncrona; ou seja, o aplicativo chama uma função e o driver não retorna o controle para o aplicativo até que a execução da função seja concluída. No entanto, algumas funções podem ser executadas de forma assíncrona; ou seja, o aplicativo chama a função, e o driver, após o processamento mínimo, retorna o controle para o aplicativo. O aplicativo pode então chamar outras funções enquanto a primeira função ainda está em execução.  
  
 A execução assíncrona tem suporte para a maioria das funções que são amplamente executadas na fonte de dados, como as funções para estabelecer conexões, preparar e executar instruções SQL, recuperar metadados, buscar dados e confirmar transações. Ele é mais útil quando a tarefa que está sendo executada na fonte de dados leva muito tempo, como um processo de logon ou uma consulta complexa em relação a um banco de dados grande.  
  
 Quando o aplicativo executa uma função com uma instrução ou conexão que está habilitada para processamento assíncrono, o driver executa uma quantidade mínima de processamento (como verificação de argumentos de erros), o processamento de mãos para a fonte de dados e retorna o controle para o aplicativo com o SQL_STILL_EXECUTING código de retorno. Em seguida, o aplicativo executa outras tarefas. Para determinar quando a função assíncrona foi concluída, o aplicativo sonda o driver em intervalos regulares chamando a função com os mesmos argumentos usados originalmente. Se a função ainda estiver em execução, ela retornará SQL_STILL_EXECUTING; Se ele tiver terminado de ser executado, ele retornará o código que ele teria retornado, como SQL_SUCCESS, SQL_ERROR ou SQL_NEED_DATA.  
  
 Se uma função é executada de forma síncrona ou assíncrona, é específica do driver. Por exemplo, suponha que os metadados do conjunto de resultados sejam armazenados em cache no driver. Nesse caso, leva muito pouco tempo para executar **SQLDescribeCol** e o driver deve simplesmente executar a função em vez de atrasar artificialmente a execução. Por outro lado, se o driver precisar recuperar os metadados da fonte de dados, ele deverá retornar o controle ao aplicativo enquanto estiver fazendo isso. Portanto, o aplicativo deve ser capaz de lidar com um código de retorno diferente de SQL_STILL_EXECUTING quando ele executa pela primeira vez uma função de forma assíncrona.  
  
## <a name="executing-statement-operations-asynchronously"></a>Executando operações de instrução de forma assíncrona  
 As funções de instrução a seguir operam em uma fonte de dados e podem ser executadas de forma assíncrona:  

:::row:::
    :::column:::
        [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)  
        [SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)  
        [SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)  
        [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)  
        [SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)  
        [SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)  
        [SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)  
        [SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)  
        [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)  
    :::column-end:::
    :::column:::
        [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)  
        [SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)  
        [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)  
        [SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)  
        [SQLMoreResults](../../../odbc/reference/syntax/sqlmoreresults-function.md)  
        [SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)  
        [SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)  
        [SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)  
        [SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)  
    :::column-end:::
    :::column:::
        [SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)  
        [SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)  
        [SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)  
        [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)  
        [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)  
        [SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)  
        [SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)  
        [SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)  
        [SQLTables](../../../odbc/reference/syntax/sqltables-function.md)  
    :::column-end:::
:::row-end:::

 A execução da instrução assíncrona é controlada em uma base por instrução ou por conexão, dependendo da fonte de dados. Ou seja, o aplicativo especifica que uma função específica deve ser executada de forma assíncrona, mas que qualquer função executada em uma determinada instrução seja executada de forma assíncrona. Para descobrir qual deles tem suporte, um aplicativo chama [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) com uma opção de SQL_ASYNC_MODE. SQL_AM_CONNECTION será retornado se a execução assíncrona no nível de conexão (para um identificador de instrução) for suportada; SQL_AM_STATEMENT se houver suporte para a execução assíncrona em nível de instrução.  
  
 Para especificar que as funções executadas com uma determinada instrução sejam executadas de forma assíncrona, o aplicativo chama **SQLSetStmtAttr** com o atributo SQL_ATTR_ASYNC_ENABLE e o define como SQL_ASYNC_ENABLE_ON. Se houver suporte para o processamento assíncrono em nível de conexão, o atributo de instrução SQL_ATTR_ASYNC_ENABLE será somente leitura e seu valor será o mesmo que o atributo de conexão da conexão na qual a instrução foi alocada. Ele é específico do driver, quer o valor do atributo Statement seja definido no momento da alocação da instrução ou posterior. A tentativa de defini-lo retornará SQL_ERROR e SQLSTATE HYC00 (recurso opcional não implementado).  
  
 Para especificar que as funções executadas com uma conexão específica sejam executadas de forma assíncrona, o aplicativo chama **SQLSetConnectAttr** com o atributo SQL_ATTR_ASYNC_ENABLE e o define como SQL_ASYNC_ENABLE_ON. Todos os identificadores de instrução futuros alocados na conexão serão habilitados para execução assíncrona; Ele é definido por driver se os identificadores de instrução existentes serão habilitados por essa ação. Se SQL_ATTR_ASYNC_ENABLE for definido como SQL_ASYNC_ENABLE_OFF, todas as instruções na conexão estarão no modo síncrono. Um erro será retornado se a execução assíncrona estiver habilitada enquanto houver uma instrução ativa na conexão.  
  
 Para determinar o número máximo de instruções simultâneas ativas no modo assíncrono ao qual o driver pode dar suporte em uma determinada conexão, o aplicativo chama **SQLGetInfo** com a opção SQL_MAX_ASYNC_CONCURRENT_STATEMENTS.  
  
 O código a seguir demonstra como o modelo de sondagem funciona:  
  
```  
SQLHSTMT  hstmt1;  
SQLRETURN rc;  
  
// Specify that the statement is to be executed asynchronously.  
SQLSetStmtAttr(hstmt1, SQL_ATTR_ASYNC_ENABLE, SQL_ASYNC_ENABLE_ON, 0);  
  
// Execute a SELECT statement asynchronously.  
while ((rc=SQLExecDirect(hstmt1,"SELECT * FROM Orders",SQL_NTS))==SQL_STILL_EXECUTING) {  
   // While the statement is still executing, do something else.  
   // Do not use hstmt1, because it is being used asynchronously.  
}  
  
// When the statement has finished executing, retrieve the results.  
```  
  
 Embora uma função esteja sendo executada de forma assíncrona, o aplicativo pode chamar funções em quaisquer outras instruções. O aplicativo também pode chamar funções em qualquer conexão, exceto aquela associada à instrução assíncrona. Mas o aplicativo só pode chamar a função original e as funções a seguir (com o identificador de instrução ou sua conexão associada, identificador de ambiente), depois que uma operação de instrução retorna SQL_STILL_EXECUTING:  
  
-   [SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)  
  
-   [SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) (no identificador de instrução)  
  
-   [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
-   [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
-   [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
-   [SQLGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)  
  
-   [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
-   [SQLDataSources](../../../odbc/reference/syntax/sqldatasources-function.md)  
  
-   [SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)  
  
-   [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)  
  
-   [SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
-   [SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md)  
  
 Se o aplicativo chamar qualquer outra função com a instrução assíncrona ou com a conexão associada a essa instrução, a função retornará SQLSTATE HY010 (erro de sequência de função), por exemplo.  
  
```  
SQLHDBC       hdbc1, hdbc2;  
SQLHSTMT      hstmt1, hstmt2, hstmt3;  
SQLCHAR *     SQLStatement = "SELECT * FROM Orders";  
SQLUINTEGER   InfoValue;  
SQLRETURN     rc;  
  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt2);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc2, &hstmt3);  
  
// Specify that hstmt1 is to be executed asynchronously.  
SQLSetStmtAttr(hstmt1, SQL_ATTR_ASYNC_ENABLE, SQL_ASYNC_ENABLE_ON, 0);  
  
// Execute hstmt1 asynchronously.  
while ((rc = SQLExecDirect(hstmt1, SQLStatement, SQL_NTS)) == SQL_STILL_EXECUTING) {  
   // The following calls return HY010 because the previous call to  
   // SQLExecDirect is still executing asynchronously on hstmt1. The  
   // first call uses hstmt1 and the second call uses hdbc1, on which  
   // hstmt1 is allocated.  
   SQLExecDirect(hstmt1, SQLStatement, SQL_NTS);   // Error!  
   SQLGetInfo(hdbc1, SQL_UNION, (SQLPOINTER) &InfoValue, 0, NULL);   // Error!  
  
   // The following calls do not return errors. They use a statement  
   // handle other than hstmt1 or a connection handle other than hdbc1.  
   SQLExecDirect(hstmt2, SQLStatement, SQL_NTS);   // OK  
   SQLTables(hstmt3, NULL, 0, NULL, 0, NULL, 0, NULL, 0);   // OK  
   SQLGetInfo(hdbc2, SQL_UNION, (SQLPOINTER) &InfoValue, 0, NULL);   // OK  
}  
```  
  
 Quando um aplicativo chama uma função para determinar se ele ainda está sendo executado de forma assíncrona, ele deve usar o identificador de instrução original. Isso ocorre porque a execução assíncrona é controlada por instrução. O aplicativo também deve fornecer valores válidos para os outros argumentos: os argumentos originais farão-para obter uma verificação de erro anterior no Gerenciador de driver. No entanto, depois que o driver verifica o identificador de instrução e determina que a instrução está sendo executada de forma assíncrona, ela ignora todos os outros argumentos.  
  
 Embora uma função esteja sendo executada de forma assíncrona, ou seja, após ela ter retornado SQL_STILL_EXECUTING e antes de retornar um código diferente, o aplicativo pode cancelá-lo chamando **SQLCancel** ou **SQLCancelHandle** com o mesmo identificador de instrução. Isso não é garantido para cancelar a execução da função. Por exemplo, a função pode já ter sido concluída. Além disso, o código retornado por **SQLCancel** ou **SQLCancelHandle** apenas indica se a tentativa de cancelar a função foi bem-sucedida, não se ela realmente cancelou a função. Para determinar se a função foi cancelada, o aplicativo chama a função novamente. Se a função foi cancelada, ela retorna SQL_ERROR e SQLSTATE HY008 (operação cancelada). Se a função não tiver sido cancelada, ela retornará outro código, como SQL_SUCCESS, SQL_STILL_EXECUTING ou SQL_ERROR com um SQLSTATE diferente.  
  
 Para desabilitar a execução assíncrona de uma instrução específica quando o driver dá suporte ao processamento assíncrono em nível de instrução, o aplicativo chama **SQLSetStmtAttr** com o atributo SQL_ATTR_ASYNC_ENABLE e o define como SQL_ASYNC_ENABLE_OFF. Se o driver oferecer suporte ao processamento assíncrono em nível de conexão, o aplicativo chamará **SQLSetConnectAttr** para definir SQL_ATTR_ASYNC_ENABLE como SQL_ASYNC_ENABLE_OFF, o que desabilita a execução assíncrona de todas as instruções na conexão.  
  
 O aplicativo deve processar registros de diagnóstico no loop repetido da função original. Se **SQLGetDiagField** ou **SQLGetDiagRec** for chamado quando uma função assíncrona estiver em execução, ele retornará a lista atual de registros de diagnóstico. Cada vez que a chamada de função original é repetida, ela limpa os registros de diagnóstico anteriores.  
  
## <a name="executing-connection-operations-asynchronously"></a>Executando operações de conexão de forma assíncrona  
 Antes do ODBC 3,8, a execução assíncrona foi permitida para operações relacionadas à instrução, como preparar, executar e buscar, bem como para operações de metadados de catálogo. A partir do ODBC 3,8, a execução assíncrona também é possível para operações relacionadas à conexão, como conectar, desconectar, confirmar e reverter.  
  
 Para obter mais informações sobre o ODBC 3,8, consulte [What ' s New in odbc 3,8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).  
  
 A execução de operações de conexão assincronamente é útil nos seguintes cenários:  
  
-   Quando um pequeno número de threads gerencia um grande número de dispositivos com taxas de dados muito altas. Para maximizar a capacidade de resposta e a escalabilidade, é desejável que todas as operações sejam assíncronas.  
  
-   Quando você quiser sobrepor as operações de banco de dados em várias conexões para reduzir os tempos de transferência decorridos.  
  
-   Chamadas ODBC assíncronas eficientes e a capacidade de cancelar operações de conexão permitem que um aplicativo permita que o usuário cancele qualquer operação lenta sem precisar aguardar os tempos limite.  
  
 As funções a seguir, que operam em identificadores de conexão, agora podem ser executadas de forma assíncrona:  

:::row:::
    :::column:::
        [SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)  
        [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)  
    :::column-end:::
    :::column:::
        [SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)  
        [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)  
    :::column-end:::
    :::column:::
        [SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)  
        [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)  
    :::column-end:::
:::row-end:::

 Para determinar se um driver dá suporte a operações assíncronas nessas funções, um aplicativo chama **SQLGetInfo** com SQL_ASYNC_DBC_FUNCTIONS. SQL_ASYNC_DBC_CAPABLE será retornado se houver suporte para operações assíncronas. SQL_ASYNC_DBC_NOT_CAPABLE será retornado se não houver suporte para operações assíncronas.  
  
 Para especificar que as funções executadas com uma conexão específica sejam executadas de forma assíncrona, o aplicativo chama **SQLSetConnectAttr** e define o atributo SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE como SQL_ASYNC_DBC_ENABLE_ON. Definir um atributo de conexão antes de estabelecer uma conexão sempre é executado de forma síncrona. Além disso, a operação de configuração do atributo de conexão SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE com **SQLSetConnectAttr** sempre é executada de forma síncrona.  
  
 Um aplicativo pode habilitar a operação assíncrona antes de fazer uma conexão. Como o Gerenciador de driver não pode determinar qual driver usar antes de fazer uma conexão, o Gerenciador de driver sempre retornará êxito em **SQLSetConnectAttr**. No entanto, ele poderá falhar ao se conectar se o driver ODBC não oferecer suporte a operações assíncronas.  
  
 Em geral, pode haver no máximo uma função de execução assíncrona associada a um identificador de conexão ou identificador de instrução específico. No entanto, um identificador de conexão pode ter mais de um identificador de instrução associado. Se não houver nenhuma operação assíncrona em execução no identificador de conexão, um identificador de instrução associado poderá executar uma operação assíncrona. Da mesma forma, você pode ter uma operação assíncrona em um identificador de conexão se não houver operações assíncronas em andamento em qualquer identificador de instrução associado. Uma tentativa de executar uma operação assíncrona usando um identificador que está executando uma operação assíncrona, no momento, retornará HY010, "erro de sequência de função".  
  
 Se uma operação de conexão retornar SQL_STILL_EXECUTING, um aplicativo só poderá chamar a função original e as seguintes funções para esse identificador de conexão:  
  
-   **SQLCancelHandle** (no identificador de conexão)  
  
-   **SQLGetDiagField**  
  
-   **SQLGetDiagRec**  
  
-   **SQLAllocHandle** (alocando env/DBC)  
  
-   **SQLAllocHandleStd** (alocando env/DBC)  
  
-   **SQLGetEnvAttr**  
  
-   **SQLGetConnectAttr**  
  
-   **SQLDataSources**  
  
-   **SQLDrivers**  
  
-   **SQLGetInfo**  
  
-   **SQLGetFunctions**  
  
 O aplicativo deve processar registros de diagnóstico no loop repetido da função original. Se SQLGetDiagField ou SQLGetDiagRec for chamado quando uma função assíncrona estiver em execução, ele retornará a lista atual de registros de diagnóstico. Cada vez que a chamada de função original é repetida, ela limpa os registros de diagnóstico anteriores.  
  
 Se uma conexão estiver sendo aberta ou fechada de forma assíncrona, a operação será concluída quando o aplicativo receber SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO na chamada de função original.  
  
 Uma nova função foi adicionada ao ODBC 3,8, **SQLCancelHandle**. Essa função cancela as seis funções de conexão (**SQLBrowseConnect**, **SQLConnect**, **SQLDisconnect**, **SQLDriverConnect**, **SQLEndTran**e **SQLSetConnectAttr**). Um aplicativo deve chamar **SQLGetFunctions** para determinar se o driver dá suporte a **SQLCancelHandle**. Assim como com **SQLCancel**, se **SQLCancelHandle** retornar Success, isso não significa que a operação foi cancelada. Um aplicativo deve chamar a função original novamente para determinar se a operação foi cancelada. **SQLCancelHandle** permite cancelar operações assíncronas em identificadores de conexão ou identificadores de instrução. O uso de **SQLCancelHandle** para cancelar uma operação em um identificador de instrução é o mesmo que chamar **SQLCancel**.  
  
 Não é necessário dar suporte a operações de conexão assíncronas e **SQLCancelHandle** ao mesmo tempo. Um driver pode dar suporte A operações de conexão assíncronas, mas não **SQLCancelHandle**, nem vice-versa.  
  
 As operações de conexão assíncrona e **SQLCancelHandle** também podem ser usadas por aplicativos ODBC 3. x e ODBC 2. x com um driver ODBC 3,8 e o Gerenciador de driver ODBC 3,8. Para obter informações sobre como habilitar um aplicativo mais antigo para usar novos recursos na versão mais recente do ODBC, consulte [matriz de compatibilidade](../../../odbc/reference/develop-app/compatibility-matrix.md).  
  
### <a name="connection-pooling"></a>Pool de conexões  
 Sempre que o pool de conexões é habilitado, as operações assíncronas são apenas mínimas suportadas para estabelecer uma conexão (com **SQLConnect** e **SQLDriverConnect**) e fechar uma conexão com **SQLDisconnect**. Mas um aplicativo ainda deve ser capaz de lidar com o valor de retorno de SQL_STILL_EXECUTING de **SQLConnect**, **SQLDriverConnect**e **SQLDisconnect**.  
  
 Quando o pool de conexões está habilitado, **SQLEndTran** e **SQLSetConnectAttr** têm suporte para operações assíncronas.  
  
## <a name="example"></a>Exemplo  
  
### <a name="description"></a>Descrição  
 O exemplo a seguir mostra como usar **SQLSetConnectAttr** para habilitar a execução assíncrona para funções relacionadas à conexão.  
  
### <a name="code"></a>Código  
  
```  
BOOL AsyncConnect (SQLHANDLE hdbc)   
{  
   SQLRETURN r;  
   SQLHANDLE hdbc;  
  
   // Enable asynchronous execution of connection functions.  
   // This must be executed synchronously, that is r != SQL_STILL_EXECUTING  
   r = SQLSetConnectAttr(  
         hdbc,   
         SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE,  
         reinterpret_cast<SQLPOINTER> (SQL_ASYNC_DBC_ENABLE_ON),  
         0);  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO)   
   {  
      return FALSE;  
   }  
  
   TCHAR szConnStrIn[256] = _T("DSN=AsyncDemo");  
  
   r = SQLDriverConnect(hdbc, NULL, (SQLTCHAR *) szConnStrIn, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
  
   if (r == SQL_ERROR)   
   {  
      // Use SQLGetDiagRec to process the error.  
      // If SQLState is HY114, the driver does not support asynchronous execution.  
      return FALSE;  
   }  
  
   while (r == SQL_STILL_EXECUTING)   
   {  
      // Do something else.  
  
      // Check for completion, with the same set of arguments.  
      r = SQLDriverConnect(hdbc, NULL, (SQLTCHAR *) szConnStrIn, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
   }  
  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO)   
   {  
      return FALSE;  
   }  
  
   return TRUE;  
}  
  
```  
  
## <a name="example"></a>Exemplo  
  
### <a name="description"></a>Descrição  
 Este exemplo mostra operações de confirmação assíncronas. As operações de reversão também podem ser feitas dessa maneira.  
  
### <a name="code"></a>Código  
  
```  
BOOL AsyncCommit ()   
{  
   SQLRETURN r;   
  
   // Assume that SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE is SQL_ASYNC_DBC_ENABLE_ON.  
  
   r = SQLEndTran(SQL_HANDLE_DBC, hdbc, SQL_COMMIT);  
   while (r == SQL_STILL_EXECUTING)   
   {  
      // Do something else.  
  
      // Check for completion with the same set of arguments.  
      r = SQLEndTran(SQL_HANDLE_DBC, hdbc, SQL_COMMIT);  
   }  
  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO)   
   {  
      return FALSE;  
   }  
   return TRUE;  
}  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Executando instruções ODBC](../../../odbc/reference/develop-app/executing-statements-odbc.md)
