---
title: Transições de instrução | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transitioning states [ODBC], statement
- state transitions [ODBC], statement
- statement transitions [ODBC]
ms.assetid: 3d70e0e3-fe83-4b4d-beac-42c82495a05b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 55f82e275bfd5bff12544b35a1370cdb31495320
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302847"
---
# <a name="statement-transitions"></a>Transições de instrução
As instruções ODBC têm os seguintes Estados.  
  
|Estado|Descrição|  
|-----------|-----------------|  
|S0|Instrução não alocada. (O estado da conexão deve ser C4, C5 ou C6. Para obter mais informações, consulte [transições de conexão](../../../odbc/reference/appendixes/connection-transitions.md).)|  
|S1|Instrução alocada.|  
|S2|Instrução preparada. Nenhum conjunto de resultados será criado.|  
|S3|Instrução preparada. Um conjunto de resultados (possivelmente vazio) será criado.|  
|S4|A instrução foi executada e nenhum conjunto de resultados foi criado.|  
|S5|A instrução foi executada e um conjunto de resultados (possivelmente vazio) foi criado. O cursor está aberto e posicionado antes da primeira linha do conjunto de resultados.|  
|S6|Cursor posicionado com **SQLFetch** ou **SQLFetchScroll**.|  
|S7|Cursor posicionado com **SQLExtendedFetch**.|  
|S8|A função precisa de dados. **SQLParamData** não foi chamado.|  
|S9|A função precisa de dados. **SQLPutData** não foi chamado.|  
|S10|A função precisa de dados. **SQLPutData** foi chamado.|  
|S11|Ainda em execução. Uma instrução é deixada nesse estado depois que uma função executada de forma assíncrona retorna SQL_STILL_EXECUTING. Uma instrução está temporariamente nesse estado enquanto qualquer função que aceita um identificador de instrução está em execução. A residência temporária no estado S11 não é mostrada em nenhuma tabela de estado, exceto a Table de estado para **SQLCancel**. Embora uma instrução esteja temporariamente no estado S11, a função pode ser cancelada chamando **SQLCancel** de outro thread.|  
|S12|Execução assíncrona cancelada. No S12, um aplicativo deve chamar a função cancelada até que ela retorne um valor diferente de SQL_STILL_EXECUTING. A função foi cancelada com êxito somente se a função retornar SQL_ERROR e SQLSTATE HY008 (operação cancelada). Se ele retornar qualquer outro valor, como SQL_SUCCESS, a operação de cancelamento falhou e a função foi executada normalmente.|  
  
 Os Estados S2 e S3 são conhecidos como Estados preparados, Estados S5 a S7 como Estados do cursor, Estados S8 por meio de S10 como os Estados de dados necessários e os Estados S11 e S12 como os Estados assíncronos. Em cada um desses grupos, as transições são mostradas separadamente somente quando são diferentes para cada Estado no grupo; na maioria dos casos, as transições para cada Estado em cada grupo são as mesmas.  
  
 As tabelas a seguir mostram como cada função ODBC afeta o estado da instrução.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1], [5], [6]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[2], [5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|S1 [3]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[4], [5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
  
 [1] esta linha mostra as transições quando *HandleType* foi SQL_HANDLE_ENV.  
  
 [2] esta linha mostra transições quando o *HandleType* foi SQL_HANDLE_DBC.  
  
 [3] esta linha mostra as transições quando *HandleType* foi SQL_HANDLE_STMT.  
  
 [4] essa linha mostra as transições quando *HandleType* foi SQL_HANDLE_DESC.  
  
 [5] chamar **SQLAllocHandle** com *OutputHandlePtr* apontando para um identificador válido substitui esse identificador sem considerar o conteúdo anterior a esse identificador e pode causar problemas para drivers ODBC. É uma programação de aplicativo ODBC incorreta para chamar **SQLAllocHandle** duas vezes com a mesma variável de aplicativo definida para * \*OutputHandlePtr* sem chamar **SQLFreeHandle** para liberar o identificador antes de realocá-lo. A substituição de identificadores ODBC de forma pode levar a comportamentos inconsistentes ou erros na parte de drivers ODBC.  
  
## <a name="sqlbindcol"></a>SQLBindCol  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbindparameter"></a>SQLBindParameter  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbrowseconnect-sqlconnect-and-sqldriverconnect"></a>SQLBrowseConnect, SQLConnect e SQLDriverConnect  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|08002|08002|08002|08002|08002|08002|08002|  
  
## <a name="sqlbulkoperations"></a>SQLBulkOperations  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|24.000|Consulte a próxima tabela|HY010|NS [c] HY010 o|  
  
## <a name="sqlbulkoperations-cursor-states"></a>SQLBulkOperations (Estados do cursor)  
  
|S5<br /><br /> Aberto|S6<br /><br /> SQLFetch ou SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|--[s] S8 [d] S11 [x]|--[s] S8 [d] S11 [x]|HY010|  
  
## <a name="sqlcancel"></a>SQLCancel  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|--|--|S1 [1] S2 [NR] e [2] S3 [r] e [2] S5 [3] e [5] S6 ([3] ou [4]) e [6] S7 [4] e [7]|Consulte a próxima tabela|  
  
 [1] **SQLExecDirect** retornou SQL_NEED_DATA.  
  
 [2] **SQLExecute** retornou SQL_NEED_DATA.  
  
 [3] **SQLBulkOperations** retornou SQL_NEED_DATA.  
  
 [4] **SQLSetPos** retornou SQL_NEED_DATA.  
  
 [5] **SQLFetch**, **SQLFetchScroll**ou **SQLExtendedFetch** não foi chamado.  
  
 [6] **SQLFetch** ou **SQLFetchScroll** foi chamado.  
  
 [7] **SQLExtendedFetch** foi chamado.  
  
## <a name="sqlcancel-asynchronous-states"></a>SQLCancel (Estados assíncronos)  
  
|S11<br /><br /> Ainda em execução|S12<br /><br /> Asynch cancelado|  
|-----------------------------|-----------------------------|  
|NS [1] S12 [2]|S12|  
  
 [1] a instrução estava temporariamente no estado S11 enquanto uma função estava em execução. **SQLCancel** foi chamado de um thread diferente.  
  
 [2] a instrução estava no estado S11 porque uma função chamada SQL_STILL_EXECUTING retornada de forma assíncrona.  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|24.000|24.000|24.000|S1 [NP] S3 [p]|HY010|HY010|  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|Consulte a próxima tabela|24.000|--[s] S11 [x]|HY010|NS [c] HY010 o|  
  
## <a name="sqlcolattribute-prepared-states"></a>SQLColAttribute (Estados preparados)  
  
|S2<br /><br /> Nenhum resultado|S3<br /><br /> Resultados|  
|-----------------------|--------------------|  
|--[1] 07005 [2]|--[s] S11 x|  
  
 [1] *FieldIdentifier* foi SQL_DESC_COUNT.  
  
 [2] *FieldIdentifier* não foi SQL_DESC_COUNT.  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumnPrivileges, SQLColumns, SQLForeignKeys, SQLGetTypeInfo, SQLPrimaryKeys, SQLProcedureColumns, SQLProcedures, SQLSpecialColumns, SQLStatistics, SQLTablePrivileges e SQLTables  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|S5 [s] S11 [x]|S1 [e] S5 [s] S11 [x]|S1 [e] e [1] S5 [s] e [1] S11 [x] e [1] 24000 [2]|Consulte a próxima tabela|HY010|NS [c] HY010 o|  
  
 [1] o resultado atual é o último ou único resultado, ou não há resultados atuais. Para obter mais informações sobre vários resultados, consulte [vários resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 [2] o resultado atual não é o último resultado.  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables-cursor-states"></a>SQLColumnPrivileges, SQLColumns, SQLForeignKeys, SQLGetTypeInfo, sqlprimarykeyes, SQLProcedureColumns, SQLProcedures, SQLSpecialColumns, SQLStatistics, SQLTablePrivileges e SQLTables (Estados de cursor)  
  
|S5<br /><br /> Aberto|S6<br /><br /> SQLFetch ou SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24.000|24000 [1]|24.000|  
  
 [1] esse erro será retornado pelo Gerenciador de driver se **SQLFetch** ou **SQLFetchScroll** não tiver retornado SQL_NO_DATA e será retornado pelo driver se **SQLFetch** ou **SQLFetchScroll** tiver retornado SQL_NO_DATA.  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH [1]|--|--|--|--|HY010|NS [c] e [3] HY010 [o] ou [4]|  
|IH [2]|HY010|Consulte a próxima tabela|24.000|--[s] S11 x|HY010|NS [c] e [3] HY010 [o] ou [4]|  
  
 [1] esta linha mostra transições quando o argumento *SourceDescHandle* era um ARD, APD ou IPD.  
  
 [2] esta linha mostra transições quando o argumento *SourceDescHandle* era um IRD.  
  
 [3] os argumentos *SourceDescHandle* e *TargetDescHandle* eram iguais aos da função **SQLCopyDesc** que está sendo executada de forma assíncrona.  
  
 [4] o argumento *SourceDescHandle* ou o argumento *TargetDescHandle* (ou ambos) foram diferentes do que na função **SQLCopyDesc** que está sendo executada de forma assíncrona.  
  
## <a name="sqlcopydesc-prepared-states"></a>SQLCopyDesc (Estados preparados)  
  
|S2<br /><br /> Nenhum resultado|S3<br /><br /> Resultados|  
|-----------------------|--------------------|  
|24000 [1]|--[s] S11 [x]|  
  
 uma Esta linha mostra as transições quando o argumento *SourceDescHandle* era um IRD.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources e sqldriveers  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqldescribecol"></a>SQLDescribeCol  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|Consulte a próxima tabela|24.000|--[s] S11 [x]|HY010|NS [c] HY010 o|  
  
## <a name="sqldescribecol-prepared-states"></a>SQLDescribeCol (Estados preparados)  
  
|S2<br /><br /> Nenhum resultado|S3<br /><br /> Resultados|  
|-----------------------|--------------------|  
|07005|--[s] S11 [x]|  
  
## <a name="sqldescribeparam"></a>SQLDescribeParam  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|--[s] S11 [x]|HY010|HY010|HY010|NS [c] HY010 [o]|  
  
## <a name="sqldisconnect"></a>SQLDisconnect  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|S0 [1]|S0 [1]|S0 [1]|S0 [1]|(HY010)|(HY010)|  
  
 [1] chamar **SQLDisconnect** libera Todas as instruções associadas à conexão. Além disso, isso retorna o estado da conexão para C2; o estado da conexão deve ser C4 antes que o estado da instrução seja S0.  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--[2] ou [3] S1 [1]|--[3] S1 [NP] e ([1] ou [2]) S1 [p] e [1] S2 [p] e [2]|--[3] S1 [NP] e ([1] ou [2]) S1 [p] e [1] S3 [p] e [2]|(HY010)|(HY010)|  
  
 [1] o argumento *complettype* é SQL_COMMIT e **SQLGetInfo** retorna SQL_CB_DELETE para o tipo de informação SQL_CURSOR_COMMIT_BEHAVIOR ou o argumento *complettype* é SQL_ROLLBACK e **SQLGetInfo** retorna SQL_CB_DELETE para o tipo de informações SQL_CURSOR_ROLLBACK_BEHAVIOR.  
  
 [2] o argumento *complettype* é SQL_COMMIT e **SQLGetInfo** retorna SQL_CB_CLOSE para o tipo de informação SQL_CURSOR_COMMIT_BEHAVIOR ou o argumento *complettype* é SQL_ROLLBACK e **SQLGetInfo** retorna SQL_CB_CLOSE para o tipo de informações SQL_CURSOR_ROLLBACK_BEHAVIOR.  
  
 [3] o argumento *complettype* é SQL_COMMIT e **SQLGetInfo** retorna SQL_CB_PRESERVE para o tipo de informação SQL_CURSOR_COMMIT_BEHAVIOR ou o argumento *complettype* é SQL_ROLLBACK e **SQLGetInfo** retorna SQL_CB_PRESERVE para o tipo de informações SQL_CURSOR_ROLLBACK_BEHAVIOR.  
  
## <a name="sqlexecdirect"></a>SQLExecDirect  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|S4 [s] e [NR] S5 [s] e [r] S8 [d] S11 [x]|--[e] e [1] S1 [e] e [2] S4 [s] e [NR] S5 [s] e [r] S8 [d] S11 [x]|--[e], [1] e [3] S1 [e], [2] e [3] S4 [s], [NR] e [3] S5 [s], [r] e [3] S8 [d] e [3] S11 [x] e [3] 24000 [4]|Consulte a próxima tabela|HY010|NS [c] HY010 [o]|  
  
 [1] o erro foi retornado pelo Gerenciador de driver.  
  
 [2] o erro não foi retornado pelo Gerenciador de driver.  
  
 [3] o resultado atual é o último ou único resultado, ou não há resultados atuais. Para obter mais informações sobre vários resultados, consulte [vários resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 [4] o resultado atual não é o último resultado.  
  
## <a name="sqlexecdirect-cursor-states"></a>SQLExecDirect (Estados do cursor)  
  
|S5<br /><br /> Aberto|S6<br /><br /> SQLFetch ou SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24.000|24000 [1]|24.000|  
  
 [1] esse erro será retornado pelo Gerenciador de driver se **SQLFetch** ou **SQLFetchScroll** não tiver retornado SQL_NO_DATA e será retornado pelo driver se **SQLFetch** ou **SQLFetchScroll** tiver retornado SQL_NO_DATA.  
  
## <a name="sqlexecute"></a>SQLExecute  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|(HY010)|Consulte a próxima tabela|S2 [e], p, e [1] S4 [s], [p], [NR] e [1] S5 [s], [p], [r] e [1] S8 [d], [p] e [1] S11 [x], [p] e [1] 24000 [p] e [2] HY010 [NP]|Consulte a tabela de Estados do cursor|HY010|NS [c] HY010 [o]|  
  
 [1] o resultado atual é o último ou único resultado, ou não há resultados atuais. Para obter mais informações sobre vários resultados, consulte [vários resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 [2] o resultado atual não é o último resultado.  
  
## <a name="sqlexecute-prepared-states"></a>SQLExecute (Estados preparados)  
  
|S2<br /><br /> Nenhum resultado|S3<br /><br /> Resultados|  
|-----------------------|--------------------|  
|S4 [s] S8 [d] S11 [x]|S5 [s] S8 [d] S11 [x]|  
  
## <a name="sqlexecute-cursor-states"></a>SQLExecute (Estados do cursor)  
  
|S5<br /><br /> Aberto|S6<br /><br /> SQLFetch ou SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000 [p] HY010 [NP]|24000 [p], [1] HY010 [NP]|24000 [p] HY010 [NP]|  
  
 [1] esse erro será retornado pelo Gerenciador de driver se **SQLFetch** ou **SQLFetchScroll** não tiver retornado SQL_NO_DATA e será retornado pelo driver se **SQLFetch** ou **SQLFetchScroll** tiver retornado SQL_NO_DATA.  
  
## <a name="sqlextendedfetch"></a>SQLExtendedFetch  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|S1010|S1010|24.000|Consulte a próxima tabela|S1010|NS [c] S1010 [o]|  
  
## <a name="sqlextendedfetch-cursor-states"></a>SQLExtendedFetch (Estados do cursor)  
  
|S5<br /><br /> Aberto|S6<br /><br /> SQLFetch ou SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|S7 [s] ou [NF] S11 [x]|S1010|--[s] ou [NF] S11 [x]|  
  
## <a name="sqlfetch-and-sqlfetchscroll"></a>SQLFetch e SQLFetchScroll  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|24.000|Consulte a próxima tabela|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlfetch-and-sqlfetchscroll-cursor-states"></a>SQLFetch e SQLFetchScroll (Estados do cursor)  
  
|S5<br /><br /> Aberto|S6<br /><br /> SQLFetch ou SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|S6 [s] ou [NF] S11 [x]|--[s] ou [NF] S11 [x]|HY010|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|HY010|HY010|HY010|HY010|HY010|HY010|  
|IH [2]|S0|S0|S0|S0|HY010|HY010|  
|--[3]|--|--|--|--|--|--|  
  
 [1] esta linha mostra transições quando o *HandleType* era SQL_HANDLE_ENV ou SQL_HANDLE_DBC.  
  
 [2] esta linha mostra transições quando o *HandleType* foi SQL_HANDLE_STMT.  
  
 [3] esta linha mostra as transições quando *HandleType* foi SQL_HANDLE_DESC e o descritor foi explicitamente alocado.  
  
## <a name="sqlfreestmt"></a>SQLFreeStmt  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH [1]|--|--|S1 [NP] S2 [p]|S1 [NP] S3 [p]|HY010|HY010|  
|IH [2]|--|--|--|--|HY010|HY010|  
  
 [1] esta linha mostra transições quando a *opção* foi SQL_CLOSE.  
  
 [2] esta linha mostra transições quando a *opção* foi SQL_UNBIND ou SQL_RESET_PARAMS. Se o argumento de *opção* tiver sido SQL_DROP e o driver subjacente for um driver ODBC 3 *. x* , o Gerenciador de driver o mapeará para uma chamada para **SQLFreeHandle** com *identificadortype* definido como SQL_HANDLE_STMT. Para obter mais informações, consulte a tabela de transição para [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md).  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetcursorname"></a>SQLGetCursorName  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|--|--|HY010|HY010|  
  
## <a name="sqlgetdata"></a>SQLGetData  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|24.000|Consulte a próxima tabela|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlgetdata-cursor-states"></a>SQLGetData (Estados do cursor)  
  
|S5<br /><br /> Aberto|S6<br /><br /> SQLFetch ou SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24.000|--[s] ou [NF] S11 [x] 24000 [b] HY109 [i]|--[s] ou [NF] S11 [x] 24000 [b] HY109 [i]|  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDescField e SQLGetDescRec  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--[1] ou [2] HY010 [3]|Consulte a próxima tabela|--[1] ou [2] 24000 [3]|--[1], [2] ou [3] S11 [3] e [x]|HY010|NS [c] ou [4] HY010 [o] e [5]|  
  
 [1] o argumento *DescriptorHandle* era um APD ou ARD.  
  
 [2] o argumento *DescriptorHandle* era um IPD.  
  
 [3] o argumento *DescriptorHandle* era um IRD.  
  
 [4] o argumento *DescriptorHandle* era o mesmo que o argumento *DescriptorHandle* na função **SQLGetDescField** ou **SQLGetDescRec** que está sendo executada de forma assíncrona.  
  
 [5] o argumento *DescriptorHandle* era diferente do argumento *DescriptorHandle* na função **SQLGetDescField** ou **SQLGetDescRec** que está sendo executada de forma assíncrona.  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec-prepared-states"></a>SQLGetDescField e SQLGetDescRec (Estados preparados)  
  
|S2<br /><br /> Nenhum resultado|S3<br /><br /> Resultados|  
|-----------------------|--------------------|  
|--[1], [2] ou [3] S11 [2] e [x]|--[1], [2] ou [3] S11 [x]|  
  
 [1] o argumento *DescriptorHandle* era um APD ou ARD.  
  
 [2] o argumento *DescriptorHandle* era um IPD.  
  
 [3] o argumento *DescriptorHandle* era um IRD. Observe que essas funções sempre retornam SQL_NO_DATA no estado S2 quando *DescriptorHandle* era um IRD.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField e SQLGetDiagRec  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--|--|--|  
|IH [2]|--[3]|--[3]|--|--|--[3]|--[3]|  
  
 [1] esta linha mostra transições quando o *HandleType* era SQL_HANDLE_ENV, SQL_HANDLE_DBC ou SQL_HANDLE_DESC.  
  
 [2] esta linha mostra transições quando o *HandleType* foi SQL_HANDLE_STMT.  
  
 [3] **SQLGetDiagField** sempre retorna um erro nesse estado quando *DiagIdentifier* é SQL_DIAG_ROW_COUNT.  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetfunctions"></a>SQLGetFunctions  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetinfo"></a>SQLGetInfo  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--[1] 24000 [2]|--[1] 24000 [2]|--[1] 24000 [2]|Consulte a próxima tabela|HY010|HY010|  
  
 [1] o atributo de instrução não foi SQL_ATTR_ROW_NUMBER.  
  
 [2] o atributo de instrução foi SQL_ATTR_ROW_NUMBER.  
  
## <a name="sqlgetstmtattr-cursor-states"></a>SQLGetStmtAttr (Estados do cursor)  
  
|S5<br /><br /> Aberto|S6<br /><br /> SQLFetch ou SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|--[1] 24000 [2]|--[1] ou ([v] e [2]) 24000 [b] e [2] HY109 [i] e [2]|--[i] ou ([v] e [2]) 24000 [b] e [2] HY109 [1] e [2]|  
  
 [1] o argumento de *atributo* não foi SQL_ATTR_ROW_NUMBER.  
  
 [2] o argumento de *atributo* foi SQL_ATTR_ROW_NUMBER.  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--[1]|--[1]|--[s] e [2] S1 [NF], [NP] e [4] S2 [NF], [p] e [4] S5 [s] e [3] S11 [x]|S1 [NF], [NP] e [4] S3 [NF], [p] e [4] S4 [s] e [2] S5 [s] e [3] S11 [x]|HY010|NS [c] HY010 [o]|  
  
 [1] a função sempre retorna SQL_NO_DATA nesse estado.  
  
 [2] o próximo resultado é uma contagem de linhas.  
  
 [3] o próximo resultado é um conjunto de resultados.  
  
 [4] o resultado atual é o último resultado.  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlnumparams"></a>SQLNumParams  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|--[s] S11 [x]|--[s] S11 [x]|--[s] S11 [x]|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlnumresultcols"></a>SQLNumResultCols  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|--[s] S11 [x]|--[s] S11 [x]|--[s] S11 [x]|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlparamdata"></a>SQLParamData  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|HY010|HY010|Consulte a próxima tabela|NS [c] HY010 [o]|  
  
## <a name="sqlparamdata-need-data-states"></a>SQLParamData (necessidade de Estados de dados)  
  
|S8<br /><br /> Dados necessários|S9<br /><br /> Deve colocar|S10<br /><br /> Pode colocar|  
|----------------------|---------------------|---------------------|  
|S1 [e] e [1] S2 [e], [NR] e [2] S3 [e], [r] e [2] S5 [e] e [4] S6 [e] e [5] S7 [e] e [3] S9 [d] S11 [x]|HY010|S1 [e] e [1] S2 [e], [NR] e [2] S3 [e], [r] e [2] S4 [s], [NR] e ([1] ou [2]) S5 [s], [r] e ([1] ou [2]) S5 ([s] ou [e]) e [4] S6 ([s] ou [e]) e [5] S7 ([s] ou [e]) e [3] S9 [d] S11 [x]|  
  
 [1] **SQLExecDirect** retornou SQL_NEED_DATA.  
  
 [2] **SQLExecute** retornou SQL_NEED_DATA.  
  
 [3] **SQLSetPos** tinha sido chamado do estado S7 e retornou SQL_NEED_DATA.  
  
 [4] **SQLBulkOperations** foi chamado do estado S5 e retornou SQL_NEED_DATA.  
  
 [5] **SQLSetPos** ou **SQLBulkOperations** foi chamado do estado S6 e retornou SQL_NEED_DATA.  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|S2 [s] e [NR] S3 [s] e [r] S11 [x]|--[s] ou ([e] e [1]) S1 [e] e [2] S11 [x]|S1 [e] e [3] S2 [s], [NR] e [3] S3 [s], [r] e [3] S11 [x] e [3] 24000 [4]|Consulte a próxima tabela|HY010|NS [c] HY010 [o]|  
  
 [1] a preparação falha por um motivo que não é validar a instrução (o SQLSTATE era HY009 [valor de argumento inválido] ou HY090 [cadeia de caracteres ou comprimento de buffer inválido]).  
  
 [2] a preparação falha ao validar a instrução (o SQLSTATE não era HY009 [valor de argumento inválido] ou HY090 [cadeia de caracteres ou comprimento de buffer inválido]).  
  
 [3] o resultado atual é o último ou único resultado, ou não há resultados atuais. Para obter mais informações sobre vários resultados, consulte [vários resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 [4] o resultado atual não é o último resultado.  
  
## <a name="sqlprepare-cursor-states"></a>SQLPrepare (Estados do cursor)  
  
|S5<br /><br /> Aberto|S6<br /><br /> SQLFetch ou SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24.000|24.000|24.000|  
  
## <a name="sqlputdata"></a>SQLPutData  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|HY010|HY010|Consulte a próxima tabela|NS [c] HY010 [o]|  
  
## <a name="sqlputdata-need-data-states"></a>SQLPutData (necessidade de Estados de dados)  
  
|S8<br /><br /> Dados necessários|S9<br /><br /> Deve colocar|S10<br /><br /> Pode colocar|  
|----------------------|---------------------|---------------------|  
|HY010|S1 [e] e [1] S2 [e], [NR] e [2] S3 [e], [r] e [2] S5 [e] e [4] S6 [e] e [5] S7 [e] e [3] S10 [s] S11 [x]|--[s] S1 [e] e [1] S2 [e], [NR] e [2] S3 [e], [r] e [2] S5 [e] e [4] S6 [e] e [5] S7 [e] e [3] S11 [x] HY011 [6]|  
  
 [1] **SQLExecDirect** retornou SQL_NEED_DATA.  
  
 [2] **SQLExecute** retornou SQL_NEED_DATA.  
  
 [3] **SQLSetPos** tinha sido chamado do estado S7 e retornou SQL_NEED_DATA.  
  
 [4] **SQLBulkOperations** foi chamado do estado S5 e retornou SQL_NEED_DATA.  
  
 [5] **SQLSetPos** ou **SQLBulkOperations** foi chamado do estado S6 e retornou SQL_NEED_DATA.  
  
 [6] uma ou mais chamadas para **SQLPutData** para um único parâmetro retornaram SQL_SUCCESS e, em seguida, uma chamada para **SQLPutData** foi feita para o mesmo parâmetro com *StrLen_or_Ind* definido como SQL_NULL_DATA.  
  
## <a name="sqlrowcount"></a>SQLRowCount  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|(HY010)|(HY010)|--|--|(HY010)|(HY010)|  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--[2] 24000 [3]|HY010|HY010|  
  
 [1] esta linha mostra transições quando o *atributo* era um atributo de conexão. Para transições quando o *atributo* era um atributo de instrução, consulte a tabela de transição de instrução para **SQLSetStmtAttr**.  
  
 [2] o argumento de *atributo* não foi SQL_ATTR_CURRENT_CATALOG.  
  
 [3] o argumento de *atributo* foi SQL_ATTR_CURRENT_CATALOG.  
  
## <a name="sqlsetcursorname"></a>SQLSetCursorName  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|24.000|24.000|HY010|HY010|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDescField e SQLSetDescRec  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH [1]|--|--|--|--|HY010|HY010|  
  
 [1] esta linha mostra transições em que o argumento *DescriptorHandle* é um ARD, APD, IPD ou (para **SQLSETDESCFIELD**) um IRD quando o argumento *FieldIdentifier* é SQL_DESC_ARRAY_STATUS_PTR ou SQL_DESC_ROWS_PROCESSED_PTR. É um erro chamar **SQLSetDescField** para um IRD quando *FieldIdentifier* é qualquer outro valor.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|HY011|HY011|HY011|HY011|Y011|HY01|HY011|  
  
## <a name="sqlsetpos"></a>SQLSetPos  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|24.000|Consulte a próxima tabela|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlsetpos-cursor-states"></a>SQLSetPos (Estados do cursor)  
  
|S5<br /><br /> Aberto|S6<br /><br /> SQLFetch ou SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24.000|--[s] S8 [d] S11 [x] 24000 [b] HY109 [i]|--[s] S8 [d] S11 [x] 24000 [b] HY109 [i]|  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executo|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados necessários|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--[1] HY011 [2]|--[1] 24000 [2]|--[1] 24000 [2]|HY010 [NP] ou [1] HY011 [p] e [2]|HY010 [NP] ou [1] HY011 [p] e [2]|  
  
 [1] o argumento de *atributo* não foi SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR, SQL_ATTR_USE_BOOKMARKS, SQL_ATTR_CURSOR_SCROLLABLE ou SQL_ATTR_CURSOR_SENSITIVITY.  
  
 [2] o argumento de *atributo* foi SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR, SQL_ATTR_USE_BOOKMARKS, SQL_ATTR_CURSOR_SCROLLABLE ou SQL_ATTR_CURSOR_SENSITIVITY.
