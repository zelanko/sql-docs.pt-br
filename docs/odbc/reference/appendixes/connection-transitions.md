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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284766"
---
# <a name="connection-transitions"></a>Transições de conexão
As conexões ODBC têm os seguintes estados.  
  
|Estado|Descrição|  
|-----------|-----------------|  
|C0|Ambiente não alocado, conexão não alocada|  
|C1|Ambiente alocado, conexão não alocada|  
|C2|Ambiente alocado, conexão alocada|  
|C3|Função de conexão precisa de dados|  
|C4|Conexão conectada|  
|C5|Conexão conectada, declaração alocada|  
|C6|Conexão conectada, transação em andamento. É possível que uma conexão esteja no estado C6 sem declarações alocadas na conexão. Por exemplo, suponha que a conexão esteja no modo de confirmação manual e esteja no estado C4. Se uma instrução for alocada, executada (iniciando uma transação) e depois liberada, a transação permanece ativa, mas não há declarações sobre a conexão.|  
  
 As tabelas a seguir mostram como cada função ODBC afeta o estado de conexão.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|C0<br /><br /> Sem Env.|C1 Não Alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados de necessidade|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|--------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|C1[1]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|(IH) [2]|C2|--[5]|--[5]|--[5]|--[5]|--[5]|  
|(IH) [3]|(IH)|(08003)|(08003)|C5|--[5]|--[5]|  
|(IH) [4]|(IH)|(08003)|(08003)|--[5]|--[5]|--[5]|  
  
 [1] Esta linha mostra transições quando *handleType* foi SQL_HANDLE_ENV.  
  
 [2] Esta linha mostra transições quando *handleType* foi SQL_HANDLE_DBC.  
  
 [3] Esta linha mostra transições quando *handleType* foi SQL_HANDLE_STMT.  
  
 [4] Esta linha mostra transições quando *handleType* foi SQL_HANDLE_DESC.  
  
 [5] Chamar **SQLAllocHandle** com *OutputHandlePtr* apontando para uma superação de cabo válida que lida sem levar em conta o conteúdo anterior dessa alça, e pode causar problemas para os drivers ODBC. É incorreto a programação do aplicativo ODBC para chamar **SQLAllocHandle** duas vezes com a mesma variável de aplicativo definida para * \*OutputHandlePtr* sem chamar **SQLFreeHandle** para liberar a alça antes de realocá-la. A substituição de alças ODBC de tal maneira pode levar a comportamentos inconsistentes ou erros por parte dos drivers ODBC.  
  
## <a name="sqlbrowseconnect"></a>SQLBrowseConnect  
  
|C0<br /><br /> Sem Env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados de necessidade|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|C3 [d] C4 [s]|-- [d] C2 [e] C4 [s]|(08002)|(08002)|(08002)|  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|C0<br /><br /> Sem Env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados de necessidade|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--|-[1] C5[2]|  
  
 [1] A conexão estava no modo de confirmação manual.  
  
 [2] A conexão estava no modo de confirmação automática.  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumnPrivileges, SQLColumns, SQLForeignKeys, SQLGetTypeInfo, SQLPrimaryKeys, SQLProcedureColumns, SQLProcedures, SQLSpecialColumns, SQLStatistics, SQLTables e SQLTables  
  
|C0<br /><br /> Sem Env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados de necessidade|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|-[1] C6[2]|--|  
  
 [1] A conexão estava no modo de confirmação automática, ou a fonte de dados não começou uma transação.  
  
 [2] A conexão estava no modo de confirmação manual, e a fonte de dados começou uma transação.  
  
## <a name="sqlconnect"></a>SQLConnect  
  
|C0<br /><br /> Sem Env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados de necessidade|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|C4|(08002)|(08002)|(08002)|(08002)|  
  
## <a name="sqlcopydesc-sqlgetdescfield-sqlgetdescrec-sqlsetdescfield-and-sqlsetdescrec"></a>SQLCopyDesc, SQLGetDescField, SQLGetDescRec, SQLSetDescField e SQLSetDescRec  
  
|C0<br /><br /> Sem Env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados de necessidade|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|--[1]|--|--|  
  
 [1] Neste estado, os únicos descritores disponíveis para o aplicativo são descritores explicitamente alocados.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources e SQLDrivers  
  
|C0<br /><br /> Sem Env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados de necessidade|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|--|--|--|--|--|--|  
  
## <a name="sqldisconnect"></a>Sqldisconnect  
  
|C0<br /><br /> Sem Env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados de necessidade|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(08003)|C2|C2|C2|25000|  
  
## <a name="sqldriverconnect"></a>SQLDriverConnect  
  
|C0<br /><br /> Sem Env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados de necessidade|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|C4 s - n[f]|(08002)|(08002)|(08002)|(08002)|  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|C0<br /><br /> Sem Env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados de necessidade|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH) [1]|--[3]|--[3]|--[3]|--|--|-[4] ou [[5], [6], e [8]) C4[5] e [7] C5[5], [6], e [9]|  
|(IH) [2]|(IH)|(08003)|(08003)|--|--|C5|  
  
 [1] Esta linha mostra transições quando *handleType* foi SQL_HANDLE_ENV.  
  
 [2] Esta linha mostra transições quando *handleType* foi SQL_HANDLE_DBC.  
  
 [3] Como a conexão não está em um estado conectado, ela não é afetada pela transação.  
  
 [4] O compromisso ou reversão falhou na conexão. A função retorna SQL_ERROR neste caso.  
  
 [5] O commit ou a reversão tiveram sucesso na conexão. A função retorna SQL_ERROR se o compromisso ou a reversão falharem em outra conexão, ou a função retornar SQL_SUCCESS se a confirmação ou reversão tiver êxito em todas as conexões.  
  
 [6] Havia pelo menos uma declaração alocada na conexão.  
  
 [7] Não houve declarações alocadas na conexão.  
  
 [8] A conexão tinha pelo menos uma declaração para a qual havia um cursor aberto, e a fonte de dados preserva os cursores quando as transações são cometidas ou revertidas, o que se aplica (dependendo se *o CompletionType* foi SQL_COMMIT ou SQL_ROLLBACK). Para obter mais informações, consulte os atributos SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR no [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
 [9] Se a conexão tivesse quaisquer declarações para as quais havia cursores abertos, os cursores não foram preservados quando a transação foi cometida ou revertida.  
  
## <a name="sqlexecdirect-and-sqlexecute"></a>SQLExecDirect e SQLExecute  
  
|C0<br /><br /> Sem Env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados de necessidade|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|-[1] C6[2] C6[3]|--|  
  
 [1] A conexão estava no modo de confirmação automática, e a instrução executada não era uma *especificação* *do cursor* (como uma instrução SELECT); ou a conexão estava no modo de confirmação manual, e a declaração executada não começou uma transação.  
  
 [2] A conexão estava no modo de confirmação automática, e a instrução executada era uma *especificação* *do cursor* (como uma instrução SELECT).  
  
 [3] A conexão estava no modo de confirmação manual, e a fonte de dados começou uma transação.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|C0<br /><br /> Sem Env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados de necessidade|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH) [1]|C0|(HY010)|(HY010)|(HY010)|(HY010)|(HY010)|  
|(IH) [2]|(IH)|(C1)|(HY010)|(HY010)|(HY010)|(HY010)|  
|(IH) [3]|(IH)|(IH)|(IH)|(IH)|C4[5] --[6]|-[7] C4[5] e [8] C5[6] e [8]|  
|(IH) [4]|(IH)|(IH)|(IH)|--|--|--|  
  
 [1] Esta linha mostra transições quando *handleType* foi SQL_HANDLE_ENV.  
  
 [2] Esta linha mostra transições quando *handleType* foi SQL_HANDLE_DBC.  
  
 [3] Esta linha mostra transições quando *handleType* foi SQL_HANDLE_STMT.  
  
 [4] Esta linha mostra transições quando *handleType* foi SQL_HANDLE_DESC.  
  
 [5] Havia apenas uma declaração alocada na conexão.  
  
 [6] Havia várias declarações alocadas na conexão.  
  
 [7] A conexão estava no modo de confirmação manual.  
  
 [8] A conexão estava no modo de confirmação automática.  
  
## <a name="sqlfreestmt"></a>SQLFreeStmt  
  
|C0<br /><br /> Sem Env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados de necessidade|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH) [1]|(IH)|(IH)|(IH)|(IH)|--|C5[3] -[4]|  
|(IH) [2]|(IH)|(IH)|(IH)|(IH)|--|--|  
  
 [1] Esta linha mostra transações quando o argumento *Opção* é SQL_CLOSE.  
  
 [2] Esta linha mostra transações quando o argumento *Opção* é SQL_UNBIND ou SQL_RESET_PARAMS.  
  
 [3] A conexão estava no modo de confirmação automática, e nenhum cursor estava aberto em quaisquer declarações, exceto esta.  
  
 [4] A conexão estava no modo de confirmação manual, ou estava no modo de confirmação automática e um cursor estava aberto em pelo menos uma outra declaração.  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|C0<br /><br /> Sem Env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados de necessidade|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|Ih|--[1] 08003[2]|HY010|--|--|--|  
  
 [1] O argumento *atributo* foi SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE ou SQL_ATTR_TRACEFILE, ou um valor foi definido para o atributo de conexão.  
  
 [2] O argumento *Atributo* não foi SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE ou SQL_ATTR_TRACEFILE, e um valor não havia sido definido para o atributo de conexão.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField e SQLGetDiagRec  
  
|C0<br /><br /> Sem Env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados de necessidade|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH) [1]|--|--|--|--|--|--|  
|(IH) [2]|(IH)|--|--|--|--|--|  
|(IH) [3]|(IH)|(IH)|(IH)|(IH)|--|--|  
|(IH) [4]|(IH)|(IH)|(IH)|--|--|--|  
  
 [1] Esta linha mostra transições quando *handleType* foi SQL_HANDLE_ENV.  
  
 [2] Esta linha mostra transições quando *handleType* foi SQL_HANDLE_DBC.  
  
 [3] Esta linha mostra transições quando *handleType* foi SQL_HANDLE_STMT.  
  
 [4] Esta linha mostra transições quando *handleType* foi SQL_HANDLE_DESC.  
  
## <a name="sqlgetenvattr"></a>SQlGetEnvAttr  
  
|C0<br /><br /> Sem Env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados de necessidade|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|--|--|--|--|--|--|  
  
## <a name="sqlgetfunctions"></a>SQLGetFunctions  
  
|C0<br /><br /> Sem Env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados de necessidade|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|Ih|HY010|HY010|--|--|--|  
  
## <a name="sqlgetinfo"></a>SQLGetInfo  
  
|C0<br /><br /> Sem Env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados de necessidade|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|Ih|--[1] 08003[2]|08003|--|--|--|  
  
 [1] O argumento *infotype* foi SQL_ODBC_VER.  
  
 [2] O argumento *infotype* não foi SQL_ODBC_VER.  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|C0<br /><br /> Sem Env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados de necessidade|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|-[1] C6[2]|-[3] C5[1]|  
  
 [1] A conexão estava no modo de confirmação automática, e a chamada para **SQLMoreResults** não inicializou o processamento de um conjunto de resultados de uma especificação do cursor.  
  
 [2] A conexão estava no modo de confirmação automática, e a chamada para **SQLMoreResults** inicializou o processamento de um conjunto de resultados de uma especificação do cursor.  
  
 [3] A conexão estava no modo de confirmação manual.  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|C0<br /><br /> Sem Env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados de necessidade|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(08003)|(08003)|--|--|--|  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|C0<br /><br /> Sem Env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados de necessidade|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|-[1] C6[2]|--|  
  
 [1] A conexão estava no modo de confirmação automática, ou a fonte de dados não começou uma transação.  
  
 [2] A conexão estava no modo de confirmação manual, e a fonte de dados começou uma transação.  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|C0<br /><br /> Sem Env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados de necessidade|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|Ih|--[1] 08003[2]|HY010|-[3] 08002[4] HY011[5]|-[3] 08002[4] HY011[5]|-[3] e [6] C5[8] 08002[4] HY011[5] ou [7]|  
  
 [1] O argumento *do Atributo* não foi SQL_ATTR_TRANSLATE_LIB ou SQL_ATTR_TRANSLATE_OPTION.  
  
 [2] O argumento *do Atributo* foi SQL_ATTR_TRANSLATE_LIB ou SQL_ATTR_TRANSLATE_OPTION.  
  
 [3] O argumento *do Atributo* não foi SQL_ATTR_ODBC_CURSORS ou SQL_ATTR_PACKET_SIZE.  
  
 [4] O argumento *do Atributo* foi SQL_ATTR_ODBC_CURSORS.  
  
 [5] O argumento *do Atributo* foi SQL_ATTR_PACKET_SIZE.  
  
 [6] O argumento *Atributo* não foi SQL_ATTR_AUTOCOMMIT, ou o argumento *Atributo* foi SQL_ATTR_AUTOCOMMIT e a definição desse atributo não comprometeu a transação.  
  
 [7] O argumento *do Atributo* foi SQL_ATTR_TXN_ISOLATION.  
  
 [8] O argumento *Atributo* foi SQL_ATTR_AUTOCOMMIT, e a definição desse atributo comprometeu a transação.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|C0<br /><br /> Sem Env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados de necessidade|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|--|--|(HY010)|--|--|--|  
  
## <a name="all-other-odbc-functions"></a>Todas as outras funções ODBC  
  
|C0<br /><br /> Sem Env.|C1<br /><br /> Não alocado|C2<br /><br /> Alocado|C3<br /><br /> Dados de necessidade|C4<br /><br /> Conectado|C5<br /><br /> de|C6<br /><br /> Transação|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--|--|
