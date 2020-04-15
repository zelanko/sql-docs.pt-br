---
title: Execução Assíncrona (Método de Votação) | Microsoft Docs
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
ms.openlocfilehash: ca7b3d5fa16be44bf4c2ef8f8df8953ae081235d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293396"
---
# <a name="asynchronous-execution-polling-method"></a>Execução assíncrona (Método de Sondagem)
Antes do ODBC 3.8 e do Windows 7 SDK, as operações assíncronas eram permitidas apenas em funções de declaração. Para obter mais informações, consulte as **operações de demonstração de execução assíncronamente,** mais tarde neste tópico.  
  
 O ODBC 3.8 no Windows 7 SDK introduziu execução assíncrona em operações relacionadas à conexão. Para obter mais informações, consulte a seção **Executando operações de conexão assíncronamente,** mais tarde neste tópico.  
  
 No SDK do Windows 7, para operações de declaração assíncrona ou conexão, um aplicativo determinou que a operação assíncrona estava completa usando o método de votação. A partir do SDK do Windows 8, você pode determinar que uma operação assíncrona está completa usando o método de notificação. Para obter mais informações, consulte [Execução Assíncrona (Método de Notificação)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md).  
  
 Por padrão, os drivers executam funções ODBC sincronizadamente; ou seja, o aplicativo chama uma função e o motorista não retorna o controle para o aplicativo até que tenha terminado a execução da função. No entanto, algumas funções podem ser executadas de forma assíncrona; ou seja, o aplicativo chama a função, e o motorista, após o processamento mínimo, retorna o controle para o aplicativo. O aplicativo pode então chamar outras funções enquanto a primeira função ainda está sendo executada.  
  
 A execução assíncrona é suportada para a maioria das funções que são executadas em grande parte na fonte de dados, como as funções para estabelecer conexões, preparar e executar declarações SQL, recuperar metadados, buscar dados e cometer transações. É mais útil quando a tarefa que está sendo executada na fonte de dados leva muito tempo, como um processo de login ou uma consulta complexa contra um grande banco de dados.  
  
 Quando o aplicativo executa uma função com uma declaração ou conexão habilitada para processamento assíncrono, o driver executa uma quantidade mínima de processamento (como verificar argumentos de erros), processamento de mãos para a fonte de dados e retorna o controle ao aplicativo com o código de retorno SQL_STILL_EXECUTING. Em seguida, o aplicativo executa outras tarefas. Para determinar quando a função assíncrona foi concluída, o aplicativo pesquisa o driver em intervalos regulares, chamando a função com os mesmos argumentos que foi usada originalmente. Se a função ainda estiver sendo executada, ela retorna SQL_STILL_EXECUTING; se tiver terminado a execução, ele retorna o código que teria retornado se tivesse sido executado de forma sincronizada, como SQL_SUCCESS, SQL_ERROR ou SQL_NEED_DATA.  
  
 Se uma função é executada de forma sincronizada ou assíncrona é específica do driver. Por exemplo, suponha que os metadados do conjunto de resultados sejam armazenados em cache no driver. Neste caso, leva muito pouco tempo para executar **sqldescribecol** e o driver deve simplesmente executar a função em vez de atrasar artificialmente a execução. Por outro lado, se o driver precisar recuperar os metadados da fonte de dados, ele deve retornar o controle ao aplicativo enquanto está fazendo isso. Portanto, o aplicativo deve ser capaz de lidar com um código de retorno diferente SQL_STILL_EXECUTING quando executa uma função de forma assíncrona.  
  
## <a name="executing-statement-operations-asynchronously"></a>Executando operações de declaração assíncronamente  
 As funções de declaração a seguir operam em uma fonte de dados e podem ser executadas de forma assíncrona:  
  
||||  
|-|-|-|  
|[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|[SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|[SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|[SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|[SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|[SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|[SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)|[SQLMoreResults](../../../odbc/reference/syntax/sqlmoreresults-function.md)|[SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|[SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|[SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|[SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|[SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|[SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)|  
|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|[SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|  
|[SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|[SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|[SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|  
  
 A execução da declaração assíncrona é controlada por declaração ou por conexão, dependendo da fonte de dados. Ou seja, o aplicativo especifica não que uma determinada função deve ser executada de forma assíncrona, mas que qualquer função executada em uma determinada declaração deve ser executada de forma assíncrona. Para descobrir qual deles é suportado, um aplicativo chama [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) com uma opção de SQL_ASYNC_MODE. SQL_AM_CONNECTION é devolvida se a execução assíncrona em nível de conexão (para uma alça de declaração) for suportada; SQL_AM_STATEMENT se a execução assíncrona em nível de declaração for suportada.  
  
 Para especificar que as funções executadas com uma determinada declaração devem ser executadas de forma assíncrona, o aplicativo chama **SQLSetStmtAttr** com o atributo SQL_ATTR_ASYNC_ENABLE e define-o para SQL_ASYNC_ENABLE_ON. Se o processamento assíncrono em nível de conexão for suportado, o atributo de declaração SQL_ATTR_ASYNC_ENABLE é somente leitura e seu valor é o mesmo que o atributo de conexão da conexão na qual a declaração foi alocada. É específico do driver se o valor do atributo da instrução é definido no tempo de alocação da declaração ou posterior. A tentativa de defini-lo retornará SQL_ERROR e SQLSTATE HYC00 (recurso opcional não implementado).  
  
 Para especificar que as funções executadas com uma determinada conexão devem ser executadas de forma assíncrona, o aplicativo chama **SQLSetConnectAttr** com o atributo SQL_ATTR_ASYNC_ENABLE e define-o como SQL_ASYNC_ENABLE_ON. Todas as alças de declaração futuras alocadas na conexão serão habilitadas para execução assíncrona; é definido pelo driver se as alças de declaração existentes serão habilitadas por esta ação. Se SQL_ATTR_ASYNC_ENABLE estiver definido como SQL_ASYNC_ENABLE_OFF, todas as instruções na conexão estarão no modo síncrono. Um erro é retornado se a execução assíncrona estiver ativa enquanto houver uma declaração ativa na conexão.  
  
 Para determinar o número máximo de instruções simultâneas ativas no modo assíncrono que o driver pode suportar em uma determinada conexão, o aplicativo chama **SQLGetInfo** com a opção SQL_MAX_ASYNC_CONCURRENT_STATEMENTS.  
  
 O código a seguir demonstra como funciona o modelo de votação:  
  
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
  
 Enquanto uma função está sendo executada de forma assíncrona, o aplicativo pode chamar funções em quaisquer outras instruções. O aplicativo também pode chamar funções em qualquer conexão, exceto a associada à declaração assíncrona. Mas o aplicativo só pode chamar a função original e as seguintes funções (com a alça da declaração ou sua conexão associada, alça do ambiente), após o retorno de uma operação de declaração SQL_STILL_EXECUTING:  
  
-   [SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)  
  
-   [SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) (na alça da declaração)  
  
-   [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
-   [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
-   [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
-   [SQlGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)  
  
-   [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
-   [SQLDataSources](../../../odbc/reference/syntax/sqldatasources-function.md)  
  
-   [SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)  
  
-   [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)  
  
-   [SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
-   [SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md)  
  
 Se o aplicativo chamar qualquer outra função com a declaração assíncrona ou com a conexão associada a essa declaração, a função retorna SQLSTATE HY010 (erro de seqüência de função), por exemplo.  
  
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
  
 Quando um aplicativo chama uma função para determinar se ele ainda está executando de forma assíncrona, ele deve usar a alça de declaração original. Isso porque a execução assíncrona é rastreada por declaração. O aplicativo também deve fornecer valores válidos para os outros argumentos - os argumentos originais farão - para passar a verificação de erros no Driver Manager. No entanto, depois que o motorista verifica o cabo da declaração e determina que a declaração está sendo executada de forma assíncrona, ele ignora todos os outros argumentos.  
  
 Enquanto uma função está sendo executada de forma assíncrona - ou seja, depois de ter retornado SQL_STILL_EXECUTING e antes de retornar um código diferente - o aplicativo pode cancelá-la chamando **SQLCancel** ou **SQLCancelHandle** com a mesma alça de declaração. Isso não é garantido para cancelar a execução da função. Por exemplo, a função pode já ter terminado. Além disso, o código retornado por **SQLCancel** ou **SQLCancelHandle** apenas indica se a tentativa de cancelar a função foi bem sucedida, não se ela realmente cancelou a função. Para determinar se a função foi cancelada, o aplicativo chama a função novamente. Se a função foi cancelada, ela retorna SQL_ERROR e SQLSTATE HY008 (Operação cancelada). Se a função não foi cancelada, ela retorna outro código, como SQL_SUCCESS, SQL_STILL_EXECUTING ou SQL_ERROR com um SQLSTATE diferente.  
  
 Para desativar a execução assíncrona de uma declaração específica quando o driver suporta processamento assíncrono em nível de declaração, o aplicativo chama **SQLSetStmtAttr** com o atributo SQL_ATTR_ASYNC_ENABLE e define-o como SQL_ASYNC_ENABLE_OFF. Se o driver suportar o processamento assíncrono em nível de conexão, o aplicativo chamará **o SQLSetConnectAttr** para definir SQL_ATTR_ASYNC_ENABLE para SQL_ASYNC_ENABLE_OFF, o que desativa a execução assíncrona de todas as instruções na conexão.  
  
 O aplicativo deve processar registros diagnósticos no loop de repetição da função original. Se **SQLGetDiagField** ou **SQLGetDiagRec** forem chamados quando uma função assíncrona estiver sendo executada, ela retornará a lista atual de registros de diagnóstico. Cada vez que a chamada de função original é repetida, ela limpa registros de diagnóstico anteriores.  
  
## <a name="executing-connection-operations-asynchronously"></a>Executando operações de conexão assíncronamente  
 Antes do ODBC 3.8, a execução assíncrona era permitida para operações relacionadas à declaração, como preparar, executar e buscar, bem como para operações de metadados de catálogo. A partir do ODBC 3.8, a execução assíncrona também é possível para operações relacionadas à conexão, como conectar, desconectar, cometer e reverter.  
  
 Para obter mais informações sobre o ODBC 3.8, consulte [o que há de novo no ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).  
  
 Executar operações de conexão de forma assíncrona é útil nos seguintes cenários:  
  
-   Quando um pequeno número de threads gerencia um grande número de dispositivos com taxas de dados muito altas. Para maximizar a capacidade de resposta e escalabilidade é desejável que todas as operações sejam assíncronas.  
  
-   Quando você quiser sobrepor as operações de banco de dados sobre várias conexões para reduzir os tempos de transferência decorridos.  
  
-   Chamadas oDBC assíncronas eficientes e a capacidade de cancelar operações de conexão permitem que um aplicativo permita que o usuário cancele qualquer operação lenta sem ter que esperar por intervalos.  
  
 As seguintes funções, que operam em alças de conexão, agora podem ser executadas de forma assíncrona:  
  
||||  
|-|-|-|  
|[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|[Sqldisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
 Para determinar se um driver suporta operações assíncronas nessas funções, um aplicativo chama **SQLGetInfo** com SQL_ASYNC_DBC_FUNCTIONS. SQL_ASYNC_DBC_CAPABLE é devolvido se as operações assíncronas forem suportadas. SQL_ASYNC_DBC_NOT_CAPABLE é devolvido se as operações assíncronas não forem suportadas.  
  
 Para especificar que as funções executadas com uma determinada conexão devem ser executadas de forma assíncrona, o aplicativo chama **SQLSetConnectAttr** e define o atributo SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE para SQL_ASYNC_DBC_ENABLE_ON. Definir um atributo de conexão antes de estabelecer uma conexão sempre executa sincronicamente. Além disso, a configuração de operação do atributo de conexão SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE com **SQLSetConnectAttr** sempre é executada de forma sincronizada.  
  
 Um aplicativo pode habilitar uma operação assíncrona antes de fazer uma conexão. Como o Driver Manager não pode determinar qual driver usar antes de fazer uma conexão, o Driver Manager sempre retornará o sucesso no **SQLSetConnectAttr**. No entanto, ele pode não se conectar se o driver ODBC não suportar operações assíncronas.  
  
 Em geral, pode haver no máximo uma função de execução assíncrona associada a uma determinada alça de conexão ou alça de declaração. No entanto, uma alça de conexão pode ter mais de uma alça de declaração associada. Se não houver uma operação assíncrona sendo executada no cabo de conexão, uma alça de declaração associada pode executar uma operação assíncrona. Da mesma forma, você pode ter uma operação assíncrona em uma alça de conexão se não houver operações assíncronas em andamento em qualquer alça de declaração associada. Uma tentativa de executar uma operação assíncrona usando uma alça que está executando uma operação assíncrona retornará HY010, "Erro de seqüência de função".  
  
 Se uma operação de conexão retornar SQL_STILL_EXECUTING, um aplicativo só poderá chamar a função original e as seguintes funções para o cabo de conexão:  
  
-   **SQLCancelHandle** (na alça de conexão)  
  
-   **SQLGetDiagField**  
  
-   **SQLGetDiagRec**  
  
-   **SQLAllocHandle** (alocando ENV/DBC)  
  
-   **SQLAllocHandleStd** (alocando ENV/DBC)  
  
-   **SQlGetEnvAttr**  
  
-   **SQLGetConnectAttr**  
  
-   **SQLDataSources**  
  
-   **SQLDrivers**  
  
-   **SQLGetInfo**  
  
-   **SQLGetFunctions**  
  
 O aplicativo deve processar registros diagnósticos no loop de repetição da função original. Se SQLGetDiagField ou SQLGetDiagRec forem chamados quando uma função assíncrona estiver sendo executada, ela retornará a lista atual de registros de diagnóstico. Cada vez que a chamada de função original é repetida, ela limpa registros de diagnóstico anteriores.  
  
 Se uma conexão estiver sendo aberta ou fechada de forma assíncrona, a operação será concluída quando o aplicativo receber SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO na chamada de função original.  
  
 Uma nova função foi adicionada ao ODBC 3.8, **SQLCancelHandle**. Esta função cancela as seis funções de conexão (**SQLBrowseConnect,** **SQLConnect,** **SQLDisconnect,** **SQLDriverConnect,** **SQLEndTran**e **SQLSetConnectAttr**). Um aplicativo deve ligar para **SQLGetFunctions** para determinar se o driver suporta **SQLCancelHandle**. Assim como no **SQLCancel**, se **o SQLCancelHandle** retornar o sucesso, isso não significa que a operação foi cancelada. Um aplicativo deve chamar a função original novamente para determinar se a operação foi cancelada. **O SQLCancelHandle** permite cancelar operações assíncronas em alças de conexão ou alças de declaração. Usar **o SQLCancelHandle** para cancelar uma operação em uma alça de declaração é o mesmo que chamar **sQLCancel**.  
  
 Não é necessário suportar tanto as operações **de conexão SQLCancelHandle** quanto assíncronas ao mesmo tempo. Um driver pode suportar operações de conexão assíncronas, mas não **SQLCancelHandle,** ou vice-versa.  
  
 As operações de conexão assíncrona e **o SQLCancelHandle** também podem ser usados pelos aplicativos ODBC 3.x e ODBC 2.x com driver ODBC 3.8 e ODBC 3.8 Driver Manager. Para obter informações sobre como habilitar um aplicativo mais antigo para usar novos recursos na versão ODBC posterior, consulte [Matrix de compatibilidade](../../../odbc/reference/develop-app/compatibility-matrix.md).  
  
### <a name="connection-pooling"></a>Pool de conexões  
 Sempre que o pool de conexões estiver ativado, as operações assíncronas são minimamente suportadas para estabelecer uma conexão (com **SQLConnect** e **SQLDriverConnect)** e fechar uma conexão com **o SQLDisconnect**. Mas um aplicativo ainda deve ser capaz de lidar com o valor de retorno SQL_STILL_EXECUTING do **SQLConnect,** **SQLDriverConnect**e **SQLDisconnect**.  
  
 Quando o pool de conexões é ativado, **o SQLEndTran** e **o SQLSetConnectAttr** são suportados para operações assíncronas.  
  
## <a name="example"></a>Exemplo  
  
### <a name="description"></a>Descrição  
 O exemplo a seguir mostra como usar **o SQLSetConnectAttr** para permitir a execução assíncrona para funções relacionadas à conexão.  
  
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
 Este exemplo mostra operações de confirmação assíncronas. As operações de reversão também podem ser feitas dessa forma.  
  
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
 [Executando declarações ODBC](../../../odbc/reference/develop-app/executing-statements-odbc.md)
