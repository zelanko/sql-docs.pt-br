---
title: Transições de Conexão | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transitioning states [ODBC], connection
- connection transitions [ODBC]
- state transitions [ODBC], connection
ms.assetid: 6b6e1a47-4a52-41c8-bb9e-7ddeae09913e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 00ebbe36f8668e83697ff3a0038fbeb38f23ffd2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019193"
---
# <a name="connection-transitions"></a>Transições de conexão
Conexões ODBC tem os seguintes estados.  
  
|Estado|Descrição|  
|-----------|-----------------|  
|C0|Ambiente não alocado, não alocado a conexão|  
|C1|Ambiente alocado, não alocado a conexão|  
|C2|Alocado ambiente, alocada a conexão|  
|C3|Função de Conexão precisa de dados|  
|C4|Conexão conectado|  
|C5|Conectado a conexão, alocada a instrução|  
|C6|Conexão conectada, a transação em andamento. É possível que uma conexão esteja no estado C6 sem declarações alocados na conexão. Por exemplo, suponha que a conexão está no modo de confirmação manual e está em estado C4. Se uma instrução é alocada, executada (Iniciar uma transação) e então liberada, a transação permanecerá ativa, mas não há nenhuma instrução sobre a conexão.|  
  
 As tabelas a seguir mostram como cada função ODBC afeta o estado de conexão.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|C0<br /><br /> Não há Env.|C1 não alocado|C2<br /><br /> alocado|C3<br /><br /> Precisa de dados|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transaction|  
|--------------------|--------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|C1[1]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|(IH)[2]|C2|--[5]|--[5]|--[5]|--[5]|--[5]|  
|(IH)[3]|(IH)|(08003)|(08003)|C5|--[5]|--[5]|  
|(IH)[4]|(IH)|(08003)|(08003)|--[5]|--[5]|--[5]|  
  
 [1] essa linha mostra as transições quando *HandleType* foi SQL_HANDLE_ENV.  
  
 [2] essa linha mostra as transições quando *HandleType* foi SQL_HANDLE_DBC.  
  
 [3] essa linha mostra as transições quando *HandleType* foi SQL_HANDLE_STMT.  
  
 [4] essa linha mostra as transições quando *HandleType* foi SQL_HANDLE_DESC.  
  
 [5] chamada **SQLAllocHandle** com *OutputHandlePtr* apontando para um identificador válido substituirá esse identificador sem levar em consideração para o identificador de ofthat conteúdo anterior e pode causar problemas para drivers ODBC. Ele é incorreta programação de aplicativo de ODBC para chamar **SQLAllocHandle** duas vezes com a mesma variável de aplicativo definida para  *\*OutputHandlePtr* sem chamar  **SQLFreeHandle** para liberar o identificador antes de realocar a ele. Substituindo ODBC alças dessa maneira podem levar a erros por parte de drivers ODBC ou um comportamento inconsistente.  
  
## <a name="sqlbrowseconnect"></a>SQLBrowseConnect  
  
|C0<br /><br /> Não há Env.|C1<br /><br /> Não alocado|C2<br /><br /> alocado|C3<br /><br /> Precisa de dados|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|C3 [d] C4 [s]|-- [d] C2 [e] C4 [s]|(08002)|(08002)|(08002)|  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|C0<br /><br /> Não há Env.|C1<br /><br /> Não alocado|C2<br /><br /> alocado|C3<br /><br /> Precisa de dados|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--|--[1] C5[2]|  
  
 [1] a conexão estava no modo de confirmação manual.  
  
 [2] a conexão estava no modo de confirmação automática.  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumnPrivileges, SQLColumns, SQLForeignKeys, SQLGetTypeInfo, SQLPrimaryKeys, SQLProcedureColumns, SQLProcedures, SQLSpecialColumns, SQLStatistics, SQLTablePrivileges e SQLTables  
  
|C0<br /><br /> Não há Env.|C1<br /><br /> Não alocado|C2<br /><br /> alocado|C3<br /><br /> Precisa de dados|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6[2]|--|  
  
 [1] a conexão estava no modo de confirmação automática, ou a fonte de dados não iniciaram uma transação.  
  
 [2] a conexão estava no modo de confirmação manual e a fonte de dados iniciou uma transação.  
  
## <a name="sqlconnect"></a>SQLConnect  
  
|C0<br /><br /> Não há Env.|C1<br /><br /> Não alocado|C2<br /><br /> alocado|C3<br /><br /> Precisa de dados|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|C4|(08002)|(08002)|(08002)|(08002)|  
  
## <a name="sqlcopydesc-sqlgetdescfield-sqlgetdescrec-sqlsetdescfield-and-sqlsetdescrec"></a>SQLCopyDesc, SQLGetDescField, SQLGetDescRec, SQLSetDescField, and SQLSetDescRec  
  
|C0<br /><br /> Não há Env.|C1<br /><br /> Não alocado|C2<br /><br /> alocado|C3<br /><br /> Precisa de dados|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|--[1]|--|--|  
  
 [1] no estado, os descritores de apenas disponíveis para o aplicativo são explicitamente alocados descritores.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources e SQLDrivers  
  
|C0<br /><br /> Não há Env.|C1<br /><br /> Não alocado|C2<br /><br /> alocado|C3<br /><br /> Precisa de dados|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|--|--|--|--|--|--|  
  
## <a name="sqldisconnect"></a>SQLDisconnect  
  
|C0<br /><br /> Não há Env.|C1<br /><br /> Não alocado|C2<br /><br /> alocado|C3<br /><br /> Precisa de dados|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(08003)|C2|C2|C2|25000|  
  
## <a name="sqldriverconnect"></a>SQLDriverConnect  
  
|C0<br /><br /> Não há Env.|C1<br /><br /> Não alocado|C2<br /><br /> alocado|C3<br /><br /> Precisa de dados|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|C4 s -- n[f]|(08002)|(08002)|(08002)|(08002)|  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|C0<br /><br /> Não há Env.|C1<br /><br /> Não alocado|C2<br /><br /> alocado|C3<br /><br /> Precisa de dados|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)[1]|--[3]|--[3]|--[3]|--|--|– [4] ou ([5], [6], [8]) C4 [5] e [7] C5 [5], [6], [9]|  
|(IH)[2]|(IH)|(08003)|(08003)|--|--|C5|  
  
 [1] essa linha mostra as transições quando *HandleType* foi SQL_HANDLE_ENV.  
  
 [2] essa linha mostra as transições quando *HandleType* foi SQL_HANDLE_DBC.  
  
 [3] porque a conexão não está em um estado conectado, ele não é afetado pela transação.  
  
 [4] a confirmação ou reversão falha sobre a conexão. Nesse caso, a função retornará SQL_ERROR.  
  
 [5] a confirmação ou reversão bem-sucedida na conexão. A função retornará SQL_ERROR se a confirmação ou reversão falha em outra conexão ou a função retorna SQL_SUCCESS se a confirmação ou reversão bem-sucedida em todas as conexões.  
  
 [6] ocorreu pelo menos uma instrução alocada em que a conexão.  
  
 [7] não havia nenhuma instrução alocada em que a conexão.  
  
 [8] a conexão tiver pelo menos era de uma instrução para o qual existe um cursor aberto, e a fonte de dados preserva cursores quando as transações são confirmadas ou revertidas, o que for aplicável (dependendo se *CompletionType* foi SQL _ Confirmar ou SQL_ROLLBACK). Para obter mais informações, consulte os atributos SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
 [9] se a conexão teve todas as instruções para o qual houve cursores abertos, os cursores não foram preservados quando a transação foi confirmada ou revertida.  
  
## <a name="sqlexecdirect-and-sqlexecute"></a>SQLExecDirect e SQLExecute  
  
|C0<br /><br /> Não há Env.|C1<br /><br /> Não alocado|C2<br /><br /> alocado|C3<br /><br /> Precisa de dados|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6[2] C6[3]|--|  
  
 [1] a conexão estava no modo de confirmação automática e a instrução executada não era um *cursor* *especificação* (por exemplo, uma instrução SELECT); ou a conexão estava no modo de confirmação manual e a instrução executado não iniciaram uma transação.  
  
 [2] a conexão estava no modo de confirmação automática e a instrução executada foi uma *cursor* *especificação* (como uma instrução SELECT).  
  
 [3] a conexão estava no modo de confirmação manual e a fonte de dados iniciou uma transação.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|C0<br /><br /> Não há Env.|C1<br /><br /> Não alocado|C2<br /><br /> alocado|C3<br /><br /> Precisa de dados|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)[1]|C0|(HY010)|(HY010)|(HY010)|(HY010)|(HY010)|  
|(IH)[2]|(IH)|(C1)|(HY010)|(HY010)|(HY010)|(HY010)|  
|(IH)[3]|(IH)|(IH)|(IH)|(IH)|C4[5] --[6]|– C4 [7] [5] e [8] C5 [6] e [8]|  
|(IH)[4]|(IH)|(IH)|(IH)|--|--|--|  
  
 [1] essa linha mostra as transições quando *HandleType* foi SQL_HANDLE_ENV.  
  
 [2] essa linha mostra as transições quando *HandleType* foi SQL_HANDLE_DBC.  
  
 [3] essa linha mostra as transições quando *HandleType* foi SQL_HANDLE_STMT.  
  
 [4] essa linha mostra as transições quando *HandleType* foi SQL_HANDLE_DESC.  
  
 [5] houve apenas uma instrução alocada em que a conexão.  
  
 [6] foram alocadas em que a conexão de várias instruções.  
  
 [7] a conexão estava no modo de confirmação manual.  
  
 [8] a conexão estava no modo de confirmação automática.  
  
## <a name="sqlfreestmt"></a>SQLFreeStmt  
  
|C0<br /><br /> Não há Env.|C1<br /><br /> Não alocado|C2<br /><br /> alocado|C3<br /><br /> Precisa de dados|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)[1]|(IH)|(IH)|(IH)|(IH)|--|C5[3] --[4]|  
|(IH)[2]|(IH)|(IH)|(IH)|(IH)|--|--|  
  
 [1] essa linha mostra as transações quando o *opção* argumento é SQL_CLOSE.  
  
 [2] essa linha mostra as transações quando o *opção* argumento é SQL_UNBIND ou SQL_RESET_PARAMS.  
  
 [3] a conexão estava no modo de confirmação automática, e nenhum cursor estava abertos em nenhuma instrução exceto este.  
  
 [4] a conexão estava no modo de confirmação manual, ou ele estava no modo de confirmação automática e um cursor foi aberto pelo menos uma outra instrução.  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|C0<br /><br /> Não há Env.|C1<br /><br /> Não alocado|C2<br /><br /> alocado|C3<br /><br /> Precisa de dados|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|--[1] 08003[2]|HY010|--|--|--|  
  
 [1] o *atributo* argumento era SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE ou SQL_ATTR_TRACEFILE ou um valor foi definido para o atributo de conexão.  
  
 [2] o *atributo* argumento não era SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE ou SQL_ATTR_TRACEFILE e um valor não tiver sido definido para a conexão atributo.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField e SQLGetDiagRec  
  
|C0<br /><br /> Não há Env.|C1<br /><br /> Não alocado|C2<br /><br /> alocado|C3<br /><br /> Precisa de dados|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)[1]|--|--|--|--|--|--|  
|(IH)[2]|(IH)|--|--|--|--|--|  
|(IH)[3]|(IH)|(IH)|(IH)|(IH)|--|--|  
|(IH)[4]|(IH)|(IH)|(IH)|--|--|--|  
  
 [1] essa linha mostra as transições quando *HandleType* foi SQL_HANDLE_ENV.  
  
 [2] essa linha mostra as transições quando *HandleType* foi SQL_HANDLE_DBC.  
  
 [3] essa linha mostra as transições quando *HandleType* foi SQL_HANDLE_STMT.  
  
 [4] essa linha mostra as transições quando *HandleType* foi SQL_HANDLE_DESC.  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|C0<br /><br /> Não há Env.|C1<br /><br /> Não alocado|C2<br /><br /> alocado|C3<br /><br /> Precisa de dados|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|--|--|--|--|--|--|  
  
## <a name="sqlgetfunctions"></a>SQLGetFunctions  
  
|C0<br /><br /> Não há Env.|C1<br /><br /> Não alocado|C2<br /><br /> alocado|C3<br /><br /> Precisa de dados|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|HY010|HY010|--|--|--|  
  
## <a name="sqlgetinfo"></a>SQLGetInfo  
  
|C0<br /><br /> Não há Env.|C1<br /><br /> Não alocado|C2<br /><br /> alocado|C3<br /><br /> Precisa de dados|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|--[1] 08003[2]|08003|--|--|--|  
  
 [1] o *tipo de informação* argumento era SQL_ODBC_VER.  
  
 [2] o *tipo de informação* argumento não era SQL_ODBC_VER.  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|C0<br /><br /> Não há Env.|C1<br /><br /> Não alocado|C2<br /><br /> alocado|C3<br /><br /> Precisa de dados|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6[2]|--[3] C5[1]|  
  
 [1] a conexão estava no modo de confirmação automática e a chamada para **SQLMoreResults** não inicializou o processamento de um conjunto de resultados de uma especificação de cursor.  
  
 [2] a conexão estava no modo de confirmação automática e a chamada para **SQLMoreResults** inicializou o processamento de um conjunto de resultados de uma especificação de cursor.  
  
 [3] a conexão estava no modo de confirmação manual.  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|C0<br /><br /> Não há Env.|C1<br /><br /> Não alocado|C2<br /><br /> alocado|C3<br /><br /> Precisa de dados|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(08003)|(08003)|--|--|--|  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|C0<br /><br /> Não há Env.|C1<br /><br /> Não alocado|C2<br /><br /> alocado|C3<br /><br /> Precisa de dados|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6[2]|--|  
  
 [1] a conexão estava no modo de confirmação automática, ou a fonte de dados não iniciaram uma transação.  
  
 [2] a conexão estava no modo de confirmação manual e a fonte de dados iniciou uma transação.  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|C0<br /><br /> Não há Env.|C1<br /><br /> Não alocado|C2<br /><br /> alocado|C3<br /><br /> Precisa de dados|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|--[1] 08003[2]|HY010|--[3] 08002[4] HY011[5]|--[3] 08002[4] HY011[5]|– [3] e [6] C5 [8] 08002 [4] HY011 [5] ou [7]|  
  
 [1] o *atributo* argumento não era SQL_ATTR_TRANSLATE_LIB ou SQL_ATTR_TRANSLATE_OPTION.  
  
 [2] o *atributo* argumento era SQL_ATTR_TRANSLATE_LIB ou SQL_ATTR_TRANSLATE_OPTION.  
  
 [3] quanto *atributo* argumento não era SQL_ATTR_ODBC_CURSORS ou SQL_ATTR_PACKET_SIZE.  
  
 [4] de *atributo* argumento era SQL_ATTR_ODBC_CURSORS.  
  
 [5] quanto *atributo* argumento era SQL_ATTR_PACKET_SIZE.  
  
 [6] quanto *atributo* argumento não era SQL_ATTR_AUTOCOMMIT, ou o *atributo* argumento era SQL_ATTR_AUTOCOMMIT e definir esse atributo não confirmar a transação.  
  
 [7] quanto *atributo* argumento era SQL_ATTR_TXN_ISOLATION.  
  
 [8] quanto *atributo* argumento era SQL_ATTR_AUTOCOMMIT e a configuração desse atributo confirmado a transação.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|C0<br /><br /> Não há Env.|C1<br /><br /> Não alocado|C2<br /><br /> alocado|C3<br /><br /> Precisa de dados|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|--|--|(HY010)|--|--|--|  
  
## <a name="all-other-odbc-functions"></a>Todas as outras funções ODBC  
  
|C0<br /><br /> Não há Env.|C1<br /><br /> Não alocado|C2<br /><br /> alocado|C3<br /><br /> Precisa de dados|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--|--|
