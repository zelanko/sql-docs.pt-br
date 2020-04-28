---
title: Transições de conexão | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 225f8517a78f8e9d4d765163649da174d72e490c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81284766"
---
# <a name="connection-transitions"></a>Transições de conexão
As conexões ODBC têm os seguintes Estados.  
  
|Estado|Descrição|  
|-----------|-----------------|  
|C0|Ambiente não alocado, conexão não alocada|  
|C1|Ambiente alocado, conexão não alocada|  
|C2|Ambiente alocado, conexão alocada|  
|C3|A função de conexão precisa de dados|  
|C4|Conexão conectada|  
|C5|Conexão conectada, instrução alocada|  
|C6|Conexão conectada, transação em andamento. É possível que uma conexão esteja no estado C6 sem instruções alocadas na conexão. Por exemplo, suponha que a conexão esteja no modo de confirmação manual e esteja no estado C4. Se uma instrução for alocada, executada (iniciando uma transação) e, em seguida, liberada, a transação permanecerá ativa, mas não haverá instruções na conexão.|  
  
 As tabelas a seguir mostram como cada função ODBC afeta o estado da conexão.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|C0<br /><br /> Sem env.|C1 não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados necessários|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|--------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|C1 [1]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|Ih 2|C2|--[5]|--[5]|--[5]|--[5]|--[5]|  
|Ih Beta|Ih|(08003)|(08003)|C5|--[5]|--[5]|  
|Ih quatro|Ih|(08003)|(08003)|--[5]|--[5]|--[5]|  
  
 [1] esta linha mostra as transições quando *HandleType* foi SQL_HANDLE_ENV.  
  
 [2] esta linha mostra transições quando o *HandleType* foi SQL_HANDLE_DBC.  
  
 [3] esta linha mostra as transições quando *HandleType* foi SQL_HANDLE_STMT.  
  
 [4] essa linha mostra as transições quando *HandleType* foi SQL_HANDLE_DESC.  
  
 [5] chamar **SQLAllocHandle** com *OutputHandlePtr* apontando para um identificador válido substitui esse identificador sem considerar o conteúdo anterior ofthat identificador e pode causar problemas para drivers ODBC. É uma programação de aplicativo ODBC incorreta para chamar **SQLAllocHandle** duas vezes com a mesma variável de aplicativo definida para * \*OutputHandlePtr* sem chamar **SQLFreeHandle** para liberar o identificador antes de realocá-lo. A substituição de identificadores ODBC de forma pode levar a comportamentos inconsistentes ou erros na parte de drivers ODBC.  
  
## <a name="sqlbrowseconnect"></a>SQLBrowseConnect  
  
|C0<br /><br /> Sem env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados necessários|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|Ih|C3 [d] C4 [s]|--[d] C2 [e] C4 [s]|(08002)|(08002)|(08002)|  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|C0<br /><br /> Sem env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados necessários|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|Ih|Ih|Ih|Ih|--|--[1] C5 [2]|  
  
 [1] a conexão estava no modo de confirmação manual.  
  
 [2] a conexão estava no modo de confirmação automática.  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumnPrivileges, SQLColumns, SQLForeignKeys, SQLGetTypeInfo, SQLPrimaryKeys, SQLProcedureColumns, SQLProcedures, SQLSpecialColumns, SQLStatistics, SQLTablePrivileges e SQLTables  
  
|C0<br /><br /> Sem env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados necessários|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|Ih|Ih|Ih|Ih|--[1] C6 [2]|--|  
  
 [1] a conexão estava no modo de confirmação automática ou a fonte de dados não inicializou uma transação.  
  
 [2] a conexão estava no modo de confirmação manual e a fonte de dados iniciou uma transação.  
  
## <a name="sqlconnect"></a>SQLConnect  
  
|C0<br /><br /> Sem env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados necessários|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|Ih|C4|(08002)|(08002)|(08002)|(08002)|  
  
## <a name="sqlcopydesc-sqlgetdescfield-sqlgetdescrec-sqlsetdescfield-and-sqlsetdescrec"></a>SQLCopyDesc, SQLGetDescField, SQLGetDescRec, SQLSetDescField e SQLSetDescRec  
  
|C0<br /><br /> Sem env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados necessários|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|Ih|Ih|Ih|--[1]|--|--|  
  
 [1] nesse estado, os únicos descritores disponíveis para o aplicativo são descritores explicitamente alocados.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources e sqldriveers  
  
|C0<br /><br /> Sem env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados necessários|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|--|--|--|--|--|--|  
  
## <a name="sqldisconnect"></a>SQLDisconnect  
  
|C0<br /><br /> Sem env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados necessários|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|Ih|(08003)|C2|C2|C2|25000|  
  
## <a name="sqldriverconnect"></a>SQLDriverConnect  
  
|C0<br /><br /> Sem env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados necessários|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|Ih|C4 s--n [f]|(08002)|(08002)|(08002)|(08002)|  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|C0<br /><br /> Sem env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados necessários|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih uma|--[3]|--[3]|--[3]|--|--|--[4] ou ([5], [6] e [8]) C4 [5] e [7] C5 [5], [6] e [9]|  
|Ih 2|Ih|(08003)|(08003)|--|--|C5|  
  
 [1] esta linha mostra as transições quando *HandleType* foi SQL_HANDLE_ENV.  
  
 [2] esta linha mostra transições quando o *HandleType* foi SQL_HANDLE_DBC.  
  
 [3] como a conexão não está em um estado conectado, ela não é afetada pela transação.  
  
 [4] falha na confirmação ou reversão na conexão. A função retorna SQL_ERROR nesse caso.  
  
 [5] a confirmação ou a reversão foi bem-sucedida na conexão. A função retornará SQL_ERROR se a confirmação ou reversão falhar em outra conexão ou se a função retornar SQL_SUCCESS se a confirmação ou a reversão tiver sido bem-sucedida em todas as conexões.  
  
 [6] havia pelo menos uma instrução alocada na conexão.  
  
 [7] não havia instruções alocadas na conexão.  
  
 [8] a conexão tinha pelo menos uma instrução para a qual havia um cursor aberto, e a fonte de dados preserva cursores quando as transações são confirmadas ou revertidas, o que for aplicável (dependendo se *complettype* foi SQL_COMMIT ou SQL_ROLLBACK). Para obter mais informações, consulte os atributos SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR em [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
 [9] se a conexão tiver alguma instrução para a qual havia cursores abertos, os cursores não foram preservados quando a transação foi confirmada ou revertida.  
  
## <a name="sqlexecdirect-and-sqlexecute"></a>SQLExecDirect e SQLExecute  
  
|C0<br /><br /> Sem env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados necessários|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|Ih|Ih|Ih|Ih|--[1] C6 [2] C6 [3]|--|  
  
 [1] a conexão estava no modo de confirmação automática e a instrução executada não era uma *especificação* de *cursor* (como uma instrução SELECT); ou a conexão estava no modo de confirmação manual e a instrução executada não começou uma transação.  
  
 [2] a conexão estava no modo de confirmação automática e a instrução executada foi uma *especificação* de *cursor* (como uma instrução SELECT).  
  
 [3] a conexão estava no modo de confirmação manual e a fonte de dados iniciou uma transação.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|C0<br /><br /> Sem env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados necessários|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih uma|C0|(HY010)|(HY010)|(HY010)|(HY010)|(HY010)|  
|Ih 2|Ih|C1|(HY010)|(HY010)|(HY010)|(HY010)|  
|Ih Beta|Ih|Ih|Ih|Ih|C4 [5]--[6]|--[7] C4 [5] e [8] C5 [6] e [8]|  
|Ih quatro|Ih|Ih|Ih|--|--|--|  
  
 [1] esta linha mostra as transições quando *HandleType* foi SQL_HANDLE_ENV.  
  
 [2] esta linha mostra transições quando o *HandleType* foi SQL_HANDLE_DBC.  
  
 [3] esta linha mostra as transições quando *HandleType* foi SQL_HANDLE_STMT.  
  
 [4] essa linha mostra as transições quando *HandleType* foi SQL_HANDLE_DESC.  
  
 [5] havia apenas uma instrução alocada na conexão.  
  
 [6] havia várias instruções alocadas na conexão.  
  
 [7] a conexão estava no modo de confirmação manual.  
  
 [8] a conexão estava no modo de confirmação automática.  
  
## <a name="sqlfreestmt"></a>SQLFreeStmt  
  
|C0<br /><br /> Sem env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados necessários|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih uma|Ih|Ih|Ih|Ih|--|C5 [3]--[4]|  
|Ih 2|Ih|Ih|Ih|Ih|--|--|  
  
 [1] esta linha mostra transações quando o argumento de *opção* é SQL_CLOSE.  
  
 [2] esta linha mostra transações quando o argumento de *opção* é SQL_UNBIND ou SQL_RESET_PARAMS.  
  
 [3] a conexão estava no modo de confirmação automática e nenhum curso foi aberto em nenhuma instrução, exceto esta.  
  
 [4] a conexão estava no modo de confirmação manual ou estava no modo de confirmação automática e um cursor estava aberto em pelo menos uma outra instrução.  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|C0<br /><br /> Sem env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados necessários|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|--[1] 08003 [2]|HY010|--|--|--|  
  
 [1] o argumento de *atributo* foi SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE ou SQL_ATTR_TRACEFILE ou um valor foi definido para o atributo de conexão.  
  
 [2] o argumento de *atributo* não foi SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE ou SQL_ATTR_TRACEFILE, e um valor não tinha sido definido para o atributo de conexão.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField e SQLGetDiagRec  
  
|C0<br /><br /> Sem env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados necessários|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih uma|--|--|--|--|--|--|  
|Ih 2|Ih|--|--|--|--|--|  
|Ih Beta|Ih|Ih|Ih|Ih|--|--|  
|Ih quatro|Ih|Ih|Ih|--|--|--|  
  
 [1] esta linha mostra as transições quando *HandleType* foi SQL_HANDLE_ENV.  
  
 [2] esta linha mostra transições quando o *HandleType* foi SQL_HANDLE_DBC.  
  
 [3] esta linha mostra as transições quando *HandleType* foi SQL_HANDLE_STMT.  
  
 [4] essa linha mostra as transições quando *HandleType* foi SQL_HANDLE_DESC.  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|C0<br /><br /> Sem env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados necessários|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|--|--|--|--|--|--|  
  
## <a name="sqlgetfunctions"></a>SQLGetFunctions  
  
|C0<br /><br /> Sem env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados necessários|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|HY010|HY010|--|--|--|  
  
## <a name="sqlgetinfo"></a>SQLGetInfo  
  
|C0<br /><br /> Sem env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados necessários|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|--[1] 08003 [2]|08003|--|--|--|  
  
 [1] o argumento *InfoType* foi SQL_ODBC_VER.  
  
 [2] o argumento *InfoType* não foi SQL_ODBC_VER.  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|C0<br /><br /> Sem env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados necessários|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|Ih|Ih|Ih|Ih|--[1] C6 [2]|--[3] C5 [1]|  
  
 [1] a conexão estava no modo de confirmação automática e a chamada para **SQLMoreResults** não inicializou o processamento de um conjunto de resultados de uma especificação de cursor.  
  
 [2] a conexão estava no modo de confirmação automática e a chamada para **SQLMoreResults** inicializou o processamento de um conjunto de resultados de uma especificação de cursor.  
  
 [3] a conexão estava no modo de confirmação manual.  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|C0<br /><br /> Sem env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados necessários|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|Ih|(08003)|(08003)|--|--|--|  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|C0<br /><br /> Sem env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados necessários|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|Ih|Ih|Ih|Ih|--[1] C6 [2]|--|  
  
 [1] a conexão estava no modo de confirmação automática ou a fonte de dados não inicializou uma transação.  
  
 [2] a conexão estava no modo de confirmação manual e a fonte de dados iniciou uma transação.  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|C0<br /><br /> Sem env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados necessários|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|--[1] 08003 [2]|HY010|--[3] 08002 [4] HY011 [5]|--[3] 08002 [4] HY011 [5]|--[3] e [6] C5 [8] 08002 [4] HY011 [5] ou [7]|  
  
 [1] o argumento de *atributo* não foi SQL_ATTR_TRANSLATE_LIB ou SQL_ATTR_TRANSLATE_OPTION.  
  
 [2] o argumento de *atributo* foi SQL_ATTR_TRANSLATE_LIB ou SQL_ATTR_TRANSLATE_OPTION.  
  
 [3] o argumento de *atributo* não foi SQL_ATTR_ODBC_CURSORS ou SQL_ATTR_PACKET_SIZE.  
  
 [4] o argumento de *atributo* foi SQL_ATTR_ODBC_CURSORS.  
  
 [5] o argumento de *atributo* foi SQL_ATTR_PACKET_SIZE.  
  
 [6] o argumento de *atributo* não foi SQL_ATTR_AUTOCOMMIT ou o argumento de *atributo* foi SQL_ATTR_AUTOCOMMIT e a definição desse atributo não confirmou a transação.  
  
 [7] o argumento de *atributo* foi SQL_ATTR_TXN_ISOLATION.  
  
 [8] o argumento de *atributo* foi SQL_ATTR_AUTOCOMMIT e a configuração deste atributo confirmou a transação.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|C0<br /><br /> Sem env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados necessários|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|--|--|(HY010)|--|--|--|  
  
## <a name="all-other-odbc-functions"></a>Todas as outras funções ODBC  
  
|C0<br /><br /> Sem env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados necessários|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|Ih|Ih|Ih|Ih|--|--|
