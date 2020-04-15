---
title: Transições de declaração | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302847"
---
# <a name="statement-transitions"></a>Transições de instrução
As declarações da ODBC têm os seguintes estados.  
  
|Estado|Descrição|  
|-----------|-----------------|  
|S0|Declaração não alocada. (O estado de conexão deve ser C4, C5 ou C6. Para obter mais informações, consulte [Transições de conexão](../../../odbc/reference/appendixes/connection-transitions.md).)|  
|S1|Declaração alocada.|  
|S2|Declaração preparada. Nenhum conjunto de resultados será criado.|  
|S3|Declaração preparada. Um conjunto de resultados (possivelmente vazio) será criado.|  
|S4|A declaração foi executada e nenhum conjunto de resultados foi criado.|  
|S5|A declaração foi executada e um conjunto de resultados (possivelmente vazio) foi criado. O cursor está aberto e posicionado antes da primeira linha do conjunto de resultados.|  
|S6|Cursor posicionado com **SQLFetch** ou **SQLFetchScroll**.|  
|S7|Cursor posicionado com **SQLExtendedFetch**.|  
|S8|A função precisa de dados. **SQLParamData** não foi chamado.|  
|S9|A função precisa de dados. **SQLPutData** não foi chamado.|  
|S10|A função precisa de dados. **SQLPutData** foi chamado.|  
|S11|Ainda executando. Uma declaração é deixada neste estado após uma função que é executada de forma assíncrona SQL_STILL_EXECUTING. Uma declaração está temporariamente neste estado enquanto qualquer função que aceite uma alça de declaração está sendo executada. A residência temporária no estado S11 não é mostrada em nenhuma tabela estadual, exceto na tabela estadual para **SQLCancel**. Enquanto uma declaração estiver temporariamente no estado S11, a função pode ser cancelada ligando para **sqlcancel** de outro segmento.|  
|S12|Execução assíncrona cancelada. No S12, um aplicativo deve chamar a função cancelada até que devolva um valor diferente SQL_STILL_EXECUTING. A função só foi cancelada com sucesso se a função retornar SQL_ERROR e SQLSTATE HY008 (Operação cancelada). Se ele devolver qualquer outro valor, como SQL_SUCCESS, a operação de cancelamento falhará e a função executada normalmente.|  
  
 Os Estados S2 e S3 são conhecidos como estados preparados, estados S5 a S7 como estados cursores, estados S8 a S10 como os estados de dados necessários, e estados S11 e S12 como estados assíncronos. Em cada um desses grupos, as transições são mostradas separadamente apenas quando são diferentes para cada estado do grupo; na maioria dos casos, as transições para cada estado em cada um grupo são as mesmas.  
  
 As tabelas a seguir mostram como cada função ODBC afeta o estado de declaração.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1], [5], [6]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[2], [5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|S1[3]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[4], [5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
  
 [1] Esta linha mostra transições quando *handleType* foi SQL_HANDLE_ENV.  
  
 [2] Esta linha mostra transições quando *handleType* foi SQL_HANDLE_DBC.  
  
 [3] Esta linha mostra transições quando *handleType* foi SQL_HANDLE_STMT.  
  
 [4] Esta linha mostra transições quando *handleType* foi SQL_HANDLE_DESC.  
  
 [5] Chamar **SQLAllocHandle** com *OutputHandlePtr* apontando para uma superação de cabo válida que lida sem levar em conta o conteúdo anterior para essa alça e pode causar problemas para os drivers ODBC. É incorreto a programação do aplicativo ODBC para chamar **SQLAllocHandle** duas vezes com a mesma variável de aplicativo definida para * \*OutputHandlePtr* sem chamar **SQLFreeHandle** para liberar a alça antes de realocá-la. A substituição de alças ODBC de tal maneira pode levar a comportamentos inconsistentes ou erros por parte dos drivers ODBC.  
  
## <a name="sqlbindcol"></a>SQLBindCol  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbindparameter"></a>SQLBindParameter  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbrowseconnect-sqlconnect-and-sqldriverconnect"></a>SQLBrowseConnect, SQLConnect e SQLDriverConnect  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|08002|08002|08002|08002|08002|08002|08002|  
  
## <a name="sqlbulkoperations"></a>SQLBulkOperations  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|HY010|24.000|Veja a próxima tabela|HY010|NS [c] HY010 o|  
  
## <a name="sqlbulkoperations-cursor-states"></a>SQLBulkOperations (Estados cursor)  
  
|S5<br /><br /> Aberto|S6<br /><br /> SQLFetch ou SQLFetchScroll|S7<br /><br /> Sqlextendedfetch|  
|-------------------|---------------------------------------|-----------------------------|  
|-- [s] S8 [d] S11 [x]|-- [s] S8 [d] S11 [x]|HY010|  
  
## <a name="sqlcancel"></a>SQLCancel  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--|--|--|S1[1] S2 [nr] e [2] S3 [r] e [2] S5[3] e [5] S6([3] ou [4]) e [6] S7[4] e [7]|Veja a próxima tabela|  
  
 [1] **SQLExecDirect** retornou SQL_NEED_DATA.  
  
 [2] **SQLExecute** retornou SQL_NEED_DATA.  
  
 [3] **SQLBulkOperations** retornou SQL_NEED_DATA.  
  
 [4] **SQLSetPos** retornou SQL_NEED_DATA.  
  
 [5] **SQLFetch,** **SQLFetchScroll**ou **SQLExtendedFetch** não foram chamados.  
  
 [6] **SQLFetch** ou **SQLFetchScroll** foram chamados.  
  
 [7] **SQLExtendedFetch** tinha sido chamado.  
  
## <a name="sqlcancel-asynchronous-states"></a>SQLCancel (Estados Assíncronos)  
  
|S11<br /><br /> Ainda executando|S12<br /><br /> Assynch cancelado|  
|-----------------------------|-----------------------------|  
|NS[1] S12[2]|S12|  
  
 [1] A declaração foi temporariamente no estado S11 enquanto uma função estava sendo executada. **SQLCancel** foi chamado de um segmento diferente.  
  
 [2] A declaração estava no estado S11 porque uma função chamada de SQL_STILL_EXECUTING assíncronamente retornou.  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|24.000|24.000|24.000|S1 [np] S3 [p]|HY010|HY010|  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|Veja a próxima tabela|24.000|-- [s] S11 [x]|HY010|NS [c] HY010 o|  
  
## <a name="sqlcolattribute-prepared-states"></a>SQLColAttribute (Estados preparados)  
  
|S2<br /><br /> Sem resultados|S3<br /><br /> Resultados|  
|-----------------------|--------------------|  
|--[1] 07005[2]|-- [s] S11 x|  
  
 [1] *FieldIdentifier* foi SQL_DESC_COUNT.  
  
 [2] *FieldIdentifier* não foi SQL_DESC_COUNT.  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumnPrivileges, SQLColumns, SQLForeignKeys, SQLGetTypeInfo, SQLPrimaryKeys, SQLProcedureColumns, SQLProcedures, SQLSpecialColumns, SQLStatistics, SQLTables e SQLTables  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S5 [s] S11 [x]|S1 [e] S5 [s] S11 [x]|S1 [e] e [1] S5 [s] e [1] S11 [x] e [1] 24000[2]|Veja a próxima tabela|HY010|NS [c] HY010 o|  
  
 [1] O resultado atual é o último ou único resultado, ou não há resultados atuais. Para obter mais informações sobre vários resultados, consulte [Múltiplos Resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 [2] O resultado atual não é o último resultado.  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables-cursor-states"></a>SQLColumnPrivileges, SQLColumns, SQLForeignKeys, SQLGetTypeInfo, SQLPrimaryKeys, SQLProcedureColumns, SQLProcedures, SQLSpecialColumns, SQLStatistics, SQLTables e SQLTables (Estados cursor)  
  
|S5<br /><br /> Aberto|S6<br /><br /> SQLFetch ou SQLFetchScroll|S7<br /><br /> Sqlextendedfetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24.000|24000[1]|24.000|  
  
 [1] Este erro é devolvido pelo Gerenciador de driver se **SQLFetch** ou **SQLFetchScroll** não tiver retornado SQL_NO_DATA e for devolvido pelo driver se **SQLFetch** ou **SQLFetchScroll** retornaram SQL_NO_DATA.  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH[1]|--|--|--|--|HY010|NS [c] e [3] HY010 [o] ou [4]|  
|IH[2]|HY010|Veja a próxima tabela|24.000|-- [s] S11 x|HY010|NS [c] e [3] HY010 [o] ou [4]|  
  
 [1] Esta linha mostra transições quando o argumento *SourceDescHandle* era um ARD, APD ou IPD.  
  
 [2] Esta linha mostra transições quando o argumento *SourceDescHandle* era um IRD.  
  
 [3] Os *argumentos SourceDescHandle* e *TargetDescHandle* eram os mesmos da função **SQLCopyDesc** que está sendo executado de forma assíncrona.  
  
 [4] O argumento *SourceDescHandle* ou o argumento *TargetDescHandle* (ou ambos) eram diferentes da função **SQLCopyDesc** que está sendo executado de forma assíncrona.  
  
## <a name="sqlcopydesc-prepared-states"></a>SQLCopyDesc (Estados preparados)  
  
|S2<br /><br /> Sem resultados|S3<br /><br /> Resultados|  
|-----------------------|--------------------|  
|24000[1]|-- [s] S11 [x]|  
  
 [1] Esta linha mostra transições quando o argumento *SourceDescHandle* era um IRD.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources e SQLDrivers  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqldescribecol"></a>SQLDescribeCol  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|Veja a próxima tabela|24.000|-- [s] S11 [x]|HY010|NS [c] HY010 o|  
  
## <a name="sqldescribecol-prepared-states"></a>SQLDescribeCol (Estados preparados)  
  
|S2<br /><br /> Sem resultados|S3<br /><br /> Resultados|  
|-----------------------|--------------------|  
|07005|-- [s] S11 [x]|  
  
## <a name="sqldescribeparam"></a>SQLDescribeParam  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|-- [s] S11 [x]|HY010|HY010|HY010|NS [c] HY010 [o]|  
  
## <a name="sqldisconnect"></a>Sqldisconnect  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|S0[1]|S0[1]|S0[1]|S0[1]|(HY010)|(HY010)|  
  
 [1] Chamar **o SQLDisconnect** libera todas as declarações associadas à conexão. Além disso, isso retorna o estado de conexão para C2; o estado de conexão deve ser C4 antes que o estado de declaração seja S0.  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|-[2] ou [3] S1[1]|-[3] S1 [np] e ([1] ou [2]) S1 [p] e [1] S2 [p] e [2]|-[3] S1 [np] e ([1] ou [2]) S1 [p] e [1] S3 [p] e [2]|(HY010)|(HY010)|  
  
 [1] O argumento *CompletionType* é SQL_COMMIT e **o SQLGetInfo** retorna SQL_CB_DELETE para o tipo de informação SQL_CURSOR_COMMIT_BEHAVIOR, ou o argumento *CompletionType* é SQL_ROLLBACK e **o SQLGetInfo** retorna SQL_CB_DELETE para o tipo de informação SQL_CURSOR_ROLLBACK_BEHAVIOR.  
  
 [2] O argumento *CompletionType* é SQL_COMMIT e **o SQLGetInfo** retorna SQL_CB_CLOSE para o tipo de informação SQL_CURSOR_COMMIT_BEHAVIOR, ou o argumento *CompletionType* é SQL_ROLLBACK e **o SQLGetInfo** retorna SQL_CB_CLOSE para o tipo de informação SQL_CURSOR_ROLLBACK_BEHAVIOR.  
  
 [3] O argumento *CompletionType* é SQL_COMMIT e **o SQLGetInfo** retorna SQL_CB_PRESERVE para o SQL_CURSOR_COMMIT_BEHAVIOR tipo de informação, ou o argumento *CompletionType* é SQL_ROLLBACK e **o SQLGetInfo** retorna SQL_CB_PRESERVE para o tipo de informação SQL_CURSOR_ROLLBACK_BEHAVIOR.  
  
## <a name="sqlexecdirect"></a>SQLExecDirect  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S4 [s] e [nr] S5 [s] e [r] S8 [d] S11 [x]|-- [e] e [1] S1 [e] e [2] S4 [s] e [nr] S5 [s] e [r] S8 [d] S11 [x]|-- [e], [1], e [3] S1 [e], [2], e [3] S4 [s], [nr], e [3] S5 [s], [r], e [3] S8 [d] e [3] S11 [x] e [3] 24000 [4]|Veja a próxima tabela|HY010|NS [c] HY010 [o]|  
  
 [1] O erro foi devolvido pelo Gerente de Motorista.  
  
 [2] O erro não foi devolvido pelo Driver Manager.  
  
 [3] O resultado atual é o último ou único resultado, ou não há resultados atuais. Para obter mais informações sobre vários resultados, consulte [Múltiplos Resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 [4] O resultado atual não é o último resultado.  
  
## <a name="sqlexecdirect-cursor-states"></a>SQLExecDirect (Estados cursor)  
  
|S5<br /><br /> Aberto|S6<br /><br /> SQLFetch ou SQLFetchScroll|S7<br /><br /> Sqlextendedfetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24.000|24000 [1]|24.000|  
  
 [1] Este erro é devolvido pelo Gerenciador de driver se **SQLFetch** ou **SQLFetchScroll** não tiver retornado SQL_NO_DATA e for devolvido pelo driver se **SQLFetch** ou **SQLFetchScroll** retornarem SQL_NO_DATA.  
  
## <a name="sqlexecute"></a>SQLExecute  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|(HY010)|Veja a próxima tabela|S2 [e], p, e [1] S4 [s], [p], [nr], e [1] S5 [s], [p], [r], e [1] S8 [d], [p], e [1] S11 [x], [p], e [1] 24000 [p] e [2] HY010 [np]|Ver tabela estados do cursor|HY010|NS [c] HY010 [o]|  
  
 [1] O resultado atual é o último ou único resultado, ou não há resultados atuais. Para obter mais informações sobre vários resultados, consulte [Múltiplos Resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 [2] O resultado atual não é o último resultado.  
  
## <a name="sqlexecute-prepared-states"></a>SQLExecute (Estados preparados)  
  
|S2<br /><br /> Sem resultados|S3<br /><br /> Resultados|  
|-----------------------|--------------------|  
|S4 [s] S8 [d] S11 [x]|S5 [s] S8 [d] S11 [x]|  
  
## <a name="sqlexecute-cursor-states"></a>SQLExecute (Estados cursor)  
  
|S5<br /><br /> Aberto|S6<br /><br /> SQLFetch ou SQLFetchScroll|S7<br /><br /> Sqlextendedfetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000 [p] HY010 [np]|24000 [p], [1] HY010 [np]|24000 [p] HY010 [np]|  
  
 [1] Este erro é devolvido pelo Gerenciador de driver se **SQLFetch** ou **SQLFetchScroll** não tiver retornado SQL_NO_DATA e for devolvido pelo driver se **SQLFetch** ou **SQLFetchScroll** retornarem SQL_NO_DATA.  
  
## <a name="sqlextendedfetch"></a>Sqlextendedfetch  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|S1010|S1010|24.000|Veja a próxima tabela|S1010|NS [c] S1010 [o]|  
  
## <a name="sqlextendedfetch-cursor-states"></a>SQLExtendedFetch (Estados cursor)  
  
|S5<br /><br /> Aberto|S6<br /><br /> SQLFetch ou SQLFetchScroll|S7<br /><br /> Sqlextendedfetch|  
|-------------------|---------------------------------------|-----------------------------|  
|S7 [s] ou [nf] S11 [x]|S1010|-- [s] ou [nf] S11 [x]|  
  
## <a name="sqlfetch-and-sqlfetchscroll"></a>SQLFetch e SQLFetchScroll  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|HY010|24.000|Veja a próxima tabela|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlfetch-and-sqlfetchscroll-cursor-states"></a>SQLFetch e SQLFetchScroll (estados cursor)  
  
|S5<br /><br /> Aberto|S6<br /><br /> SQLFetch ou SQLFetchScroll|S7<br /><br /> Sqlextendedfetch|  
|-------------------|---------------------------------------|-----------------------------|  
|S6 [s] ou [nf] S11 [x]|-- [s] ou [nf] S11 [x]|HY010|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|-- [1]|HY010|HY010|HY010|HY010|HY010|HY010|  
|IH [2]|S0|S0|S0|S0|HY010|HY010|  
|-- [3]|--|--|--|--|--|--|  
  
 [1] Esta linha mostra transições quando *handleType* foi SQL_HANDLE_ENV ou SQL_HANDLE_DBC.  
  
 [2] Esta linha mostra transições quando *handleType* foi SQL_HANDLE_STMT.  
  
 [3] Esta linha mostra transições quando *handleType* foi SQL_HANDLE_DESC e o descritor foi explicitamente alocado.  
  
## <a name="sqlfreestmt"></a>SQLFreeStmt  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH [1]|--|--|S1 [np] S2 [p]|S1 [np] S3 [p]|HY010|HY010|  
|IH [2]|--|--|--|--|HY010|HY010|  
  
 [1] Esta linha mostra transições quando *Option* foi SQL_CLOSE.  
  
 [2] Esta linha mostra transições quando *Option* foi SQL_UNBIND ou SQL_RESET_PARAMS. Se o argumento *Opção* foi SQL_DROP e o driver subjacente for um driver ODBC 3 *.x,* o Driver Manager o mapeia para uma chamada para **SQLFreeHandle** com *HandleType* definido como SQL_HANDLE_STMT. Para obter mais informações, consulte a tabela de transição para [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md).  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetcursorname"></a>SQLGetCursorName  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--|--|--|HY010|HY010|  
  
## <a name="sqlgetdata"></a>SQLGetData  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|HY010|24.000|Veja a próxima tabela|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlgetdata-cursor-states"></a>SQLGetData (Estados cursor)  
  
|S5<br /><br /> Aberto|S6<br /><br /> SQLFetch ou SQLFetchScroll|S7<br /><br /> Sqlextendedfetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24.000|-- [s] ou [nf] S11 [x] 24000 [b] HY109 [i]|-- [s] ou [nf] S11 [x] 24000 [b] HY109 [i]|  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDescField e SQLGetDescRec  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|-- [1] ou [2] HY010 [3]|Veja a próxima tabela|-- [1] ou [2] 24000 [3]|-- [1], [2], ou [3] S11 [3] e [x]|HY010|NS [c] ou [4] HY010 [o] e [5]|  
  
 [1] O argumento *DscriptorHandle* era um APD ou ARD.  
  
 [2] O argumento *DscriptorHandle* era um IPD.  
  
 [3] O argumento *DscriptorHandle* era um IRD.  
  
 [4] O argumento *DscriptorHandle* foi o mesmo que o argumento *DscriptorHandle* na função **SQLGetDescField** ou **SQLGetDescRec** que está sendo executado de forma assíncrona.  
  
 [5] O argumento *DscriptorHandle* era diferente do argumento *DscriptorHandle* na função **SQLGetDescField** ou **SQLGetDescRec** que está sendo executado de forma assíncrona.  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec-prepared-states"></a>SQLGetDescField e SQLGetDescRec (Estados preparados)  
  
|S2<br /><br /> Sem resultados|S3<br /><br /> Resultados|  
|-----------------------|--------------------|  
|-[1], [2], ou [3] S11[2] e [x]|-[1], [2], ou [3] S11 [x]|  
  
 [1] O argumento *DscriptorHandle* era um APD ou ARD.  
  
 [2] O argumento *DscriptorHandle* era um IPD.  
  
 [3] O argumento *DscriptorHandle* era um IRD. Observe que essas funções sempre retornam SQL_NO_DATA no estado S2 quando *DscriptorHandle* era um IRD.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField e SQLGetDiagRec  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--|--|--|  
|IH[2]|--[3]|--[3]|--|--|--[3]|--[3]|  
  
 [1] Esta linha mostra transições quando *handleType* foi SQL_HANDLE_ENV, SQL_HANDLE_DBC ou SQL_HANDLE_DESC.  
  
 [2] Esta linha mostra transições quando *handleType* foi SQL_HANDLE_STMT.  
  
 [3] **SQLGetDiagField** sempre retorna um erro neste estado quando *o DiagIdentifier* é SQL_DIAG_ROW_COUNT.  
  
## <a name="sqlgetenvattr"></a>SQlGetEnvAttr  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetfunctions"></a>SQLGetFunctions  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetinfo"></a>SQLGetInfo  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--[1] 24000[2]|--[1] 24000[2]|--[1] 24000[2]|Veja a próxima tabela|HY010|HY010|  
  
 [1] O atributo da declaração não foi SQL_ATTR_ROW_NUMBER.  
  
 [2] O atributo da declaração foi SQL_ATTR_ROW_NUMBER.  
  
## <a name="sqlgetstmtattr-cursor-states"></a>SQLGetStmtAttr (Estados cursor)  
  
|S5<br /><br /> Aberto|S6<br /><br /> SQLFetch ou SQLFetchScroll|S7<br /><br /> Sqlextendedfetch|  
|-------------------|---------------------------------------|-----------------------------|  
|--[1] 24000[2]|-[1] ou ([v] e [2]) 24000 [b] e [2] HY109 [i] e [2]|-- [i] ou [v] e [2]) 24000 [b] e [2] HY109[1] e [2]|  
  
 [1] O argumento *do Atributo* não foi SQL_ATTR_ROW_NUMBER.  
  
 [2] O argumento *do Atributo* foi SQL_ATTR_ROW_NUMBER.  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|--[1]|--[1]|-- [s] e [2] S1 [nf], [np], e [4] S2 [nf], [p], e [4] S5 [s] e [3] S11 [x]|S1 [nf], [np], e [4] S3 [nf], [p] e [4] S4 [s] e [2] S5 [s] e [3] S11 [x]|HY010|NS [c] HY010 [o]|  
  
 [1] A função sempre retorna SQL_NO_DATA neste estado.  
  
 [2] O próximo resultado é uma contagem de linhas.  
  
 [3] O próximo resultado é um conjunto de resultados.  
  
 [4] O resultado atual é o último resultado.  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlnumparams"></a>SQLNumParams  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|-- [s] S11 [x]|-- [s] S11 [x]|-- [s] S11 [x]|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlnumresultcols"></a>SQLNumResultCols  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|-- [s] S11 [x]|-- [s] S11 [x]|-- [s] S11 [x]|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlparamdata"></a>SQLParamData  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|HY010|HY010|HY010|Veja a próxima tabela|NS [c] HY010 [o]|  
  
## <a name="sqlparamdata-need-data-states"></a>SQLParamData (Estados de dados de necessidade)  
  
|S8<br /><br /> Dados de necessidade|S9<br /><br /> Deve colocar|S10<br /><br /> pode colocar|  
|----------------------|---------------------|---------------------|  
|S1 [e] e [1] S2 [e], [nr], e [2] S3 [e], [r], e [2] S5 [e] e [4] S6 [e] e [5] S7 [e] e [3] S9 [d] S11 [x]|HY010|S1 [e] e [1] S2 [e], [nr], e [2] S3 [e], [r], e [2] S4 [s], [nr], e ([1] ou [2]) S5 [s], [r], e ([1] ou [2]) S5 ([s] ou [e]) e [4] S6 ([s] ou [e]) e [5] S7 ([s] ou [e]) e [3] S9 [d] S11 [x]|  
  
 [1] **SQLExecDirect** retornou SQL_NEED_DATA.  
  
 [2] **SQLExecute** retornou SQL_NEED_DATA.  
  
 [3] **SQLSetPos** tinha sido chamado do estado S7 e retornado SQL_NEED_DATA.  
  
 [4] **SQLBulkOperations** tinha sido chamado do estado S5 e devolvido SQL_NEED_DATA.  
  
 [5] **SQLSetPos** ou **SQLBulkOperations** foram chamados do estado S6 e retornaram SQL_NEED_DATA.  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S2 [s] e [nr] S3 [s] e [r] S11 [x]|-- [s] ou ([e] e [1]) S1 [e] e [2] S11 [x]|S1 [e] e [3] S2 [s], [nr], e [3] S3 [s], [r], e [3] S11 [x] e [3] 24000[4]|Veja a próxima tabela|HY010|NS [c] HY010 [o]|  
  
 [1] A preparação falha por uma razão diferente de validar a declaração (o SQLSTATE era HY009 [valor de argumento inválido] ou HY090 [comprimento inválido da seqüência ou buffer]).  
  
 [2] A preparação falha ao validar a declaração (o SQLSTATE não era HY009 [valor de argumento inválido] ou HY090 [comprimento de string ou buffer inválido]).  
  
 [3] O resultado atual é o último ou único resultado, ou não há resultados atuais. Para obter mais informações sobre vários resultados, consulte [Múltiplos Resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 [4] O resultado atual não é o último resultado.  
  
## <a name="sqlprepare-cursor-states"></a>SQLPrepare (Estados cursor)  
  
|S5<br /><br /> Aberto|S6<br /><br /> SQLFetch ou SQLFetchScroll|S7<br /><br /> Sqlextendedfetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24.000|24.000|24.000|  
  
## <a name="sqlputdata"></a>SQLPutData  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|HY010|HY010|HY010|Veja a próxima tabela|NS [c] HY010 [o]|  
  
## <a name="sqlputdata-need-data-states"></a>SQLPutData (Estados de dados de necessidade)  
  
|S8<br /><br /> Dados de necessidade|S9<br /><br /> Deve colocar|S10<br /><br /> pode colocar|  
|----------------------|---------------------|---------------------|  
|HY010|S1 [e] e [1] S2 [e], [nr], e [2] S3 [e], [r], e [2] S5 [e] e [4] S6 [e] e [5] S7 [e] e [3] S10 [s] S11 [x]|-- [s] S1 [e] e [1] S2 [e], [nr], e [2] S3 [e], [r], e [2] S5 [e] e [4] S6 [e] e [5] S7 [e] e [3] S11 [x] HY011[6]|  
  
 [1] **SQLExecDirect** retornou SQL_NEED_DATA.  
  
 [2] **SQLExecute** retornou SQL_NEED_DATA.  
  
 [3] **SQLSetPos** tinha sido chamado do estado S7 e retornado SQL_NEED_DATA.  
  
 [4] **SQLBulkOperations** tinha sido chamado do estado S5 e devolvido SQL_NEED_DATA.  
  
 [5] **SQLSetPos** ou **SQLBulkOperations** foram chamados do estado S6 e retornaram SQL_NEED_DATA.  
  
 [6] Uma ou mais chamadas para **SQLPutData** para um único parâmetro retornaram SQL_SUCCESS e, em seguida, uma chamada para **SQLPutData** foi feita para o mesmo parâmetro com *StrLen_or_Ind* definido para SQL_NULL_DATA.  
  
## <a name="sqlrowcount"></a>SQLRowCount  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|(HY010)|(HY010)|--|--|(HY010)|(HY010)|  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--[2] 24000[3]|HY010|HY010|  
  
 [1] Esta linha mostra transições quando *Atributo* era um atributo de conexão. Para transições quando *Atributo* era um atributo de declaração, consulte a tabela de transição de declaração para **SQLSetStmtAttr**.  
  
 [2] O argumento *do Atributo* não foi SQL_ATTR_CURRENT_CATALOG.  
  
 [3] O argumento *do Atributo* foi SQL_ATTR_CURRENT_CATALOG.  
  
## <a name="sqlsetcursorname"></a>Sqlsetcursorname  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--|24.000|24.000|HY010|HY010|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDescField e SQLSetDescRec  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH[1]|--|--|--|--|HY010|HY010|  
  
 [1] Esta linha mostra transições onde o argumento *DscriptorHandle* é um ARD, APD, IPD ou (para **SQLSetDescField**) um IRD quando o argumento *FieldIdentifier* é SQL_DESC_ARRAY_STATUS_PTR ou SQL_DESC_ROWS_PROCESSED_PTR. É um erro chamar **SQLSetDescField** para um IRD quando *fieldIdentifier* é qualquer outro valor.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|HY011|HY011|HY011|HY011|Y011|HY01|HY011|  
  
## <a name="sqlsetpos"></a>SQLSetPos  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|HY010|24.000|Veja a próxima tabela|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlsetpos-cursor-states"></a>SQLSetPos (Estados cursor)  
  
|S5<br /><br /> Aberto|S6<br /><br /> SQLFetch ou SQLFetchScroll|S7<br /><br /> Sqlextendedfetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24.000|-- [s] S8 [d] S11 [x] 24000 [b] HY109 [i]|-- [s] S8 [d] S11 [x] 24000 [b] HY109 [i]|  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2-S3<br /><br /> Prepared|S4<br /><br /> Executado|S5-S7<br /><br /> Cursor|S8-S10<br /><br /> Dados de necessidade|S11-S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|-[1] HY011[2]|--[1] 24000[2]|--[1] 24000[2]|HY010 [np] ou [1] HY011 [p] e [2]|HY010 [np] ou [1] HY011 [p] e [2]|  
  
 [1] O argumento *do Atributo* não foi SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR, SQL_ATTR_USE_BOOKMARKS, SQL_ATTR_CURSOR_SCROLLABLE ou SQL_ATTR_CURSOR_SENSITIVITY.  
  
 [2] O argumento *do Atributo* foi SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR, SQL_ATTR_USE_BOOKMARKS, SQL_ATTR_CURSOR_SCROLLABLE ou SQL_ATTR_CURSOR_SENSITIVITY.
