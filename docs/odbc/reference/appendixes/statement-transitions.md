---
title: Instrução transições | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transitioning states [ODBC], statement
- state transitions [ODBC], statement
- statement transitions [ODBC]
ms.assetid: 3d70e0e3-fe83-4b4d-beac-42c82495a05b
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5f20ec0efb42e877695c44f4d62c4ffc1ae79806
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32914211"
---
# <a name="statement-transitions"></a>Transições de instrução
Instruções de ODBC tem os seguintes estados.  
  
|Estado|Description|  
|-----------|-----------------|  
|S0|Instrução não alocada. (O estado de conexão deve ser C4, C5 ou C6. Para obter mais informações, consulte [Conexão transições](../../../odbc/reference/appendixes/connection-transitions.md).)|  
|S1|Instrução alocada.|  
|S2|Instrução preparada. Nenhum conjunto de resultados será criado.|  
|S3|Instrução preparada. Um conjunto de resultados (possivelmente vazia) será criado.|  
|S4|Instrução executada e nenhum conjunto de resultados foi criada.|  
|S5|Instrução executada e um conjunto de resultados (possivelmente vazia) foi criado. O cursor é aberta e posicionada antes da primeira linha do conjunto de resultados.|  
|S6|Cursor posicionado com **SQLFetch** ou **SQLFetchScroll**.|  
|S7|Cursor posicionado com **SQLExtendedFetch**.|  
|S8|Função precisa de dados. **SQLParamData** não foi chamado.|  
|S9|Função precisa de dados. **SQLPutData** não foi chamado.|  
|S10|Função precisa de dados. **SQLPutData** foi chamado.|  
|S11|Ainda em execução. Uma instrução fica nesse estado depois que uma função que é executada de forma assíncrona retornará SQL_STILL_EXECUTING. Uma instrução é temporariamente nesse estado enquanto qualquer função que aceite que um identificador de instrução está em execução. Residência temporária em estado S11 não é mostrada em nenhuma tabela de estado, exceto a tabela de estado **SQLCancel**. Enquanto uma instrução temporariamente está em estado S11, a função pode ser cancelada chamando **SQLCancel** de outro thread.|  
|S12|Execução assíncrona cancelada. /S12, um aplicativo deve chamar a função cancelada até que ela retorna um valor diferente de SQL_STILL_EXECUTING. A função foi cancelada com êxito apenas se a função retornará SQL_ERROR e SQLSTATE HY008 (operação cancelada). Se ele retornar qualquer outro valor, como SQL_SUCCESS, falha na operação de cancelamento e a função executada normalmente.|  
  
 Estados S2 e S3 são conhecidos como os estados preparados, Estados S5 por meio de S7 como o cursor estados, Estados S8 por meio de S10 como os estados de dados necessário e estados S11 e /s12 como os estados assíncronos. Em cada um desses grupos, as transições são mostradas separadamente somente quando eles são diferentes para cada estado do grupo. Na maioria dos casos, as transições de cada estado em cada um grupo são os mesmos.  
  
 As tabelas a seguir mostram como cada função ODBC afeta o estado de instrução.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1], [5], [6]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[2], [5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|S1 [3]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[4], [5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
  
 [1] essa linha mostra transições quando *HandleType* foi SQL_HANDLE_ENV.  
  
 [2] essa linha mostra transições quando *HandleType* foi SQL_HANDLE_DBC.  
  
 [3] essa linha mostra transições quando *HandleType* foi SQL_HANDLE_STMT.  
  
 [4] essa linha mostra transições quando *HandleType* foi SQL_HANDLE_DESC.  
  
 [5] chamada **SQLAllocHandle** com *OutputHandlePtr* apontando para um identificador válido substituirá esse identificador sem levar em consideração para o conteúdo anterior ao manipula e pode causar problemas para drivers ODBC. É incorretova programação de aplicativo de ODBC para chamar **SQLAllocHandle** duas vezes com a mesma variável de aplicativo definida para  *\*OutputHandlePtr* sem chamar  **SQLFreeHandle** para liberar o identificador antes realocando-lo. Substituindo o ODBC identificadores dessa forma podem causar um comportamento inconsistente ou erros por parte de drivers ODBC.  
  
## <a name="sqlbindcol"></a>SQLBindCol  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbindparameter"></a>SQLBindParameter  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbrowseconnect-sqlconnect-and-sqldriverconnect"></a>SQLBrowseConnect SQLConnect e SQLDriverConnect  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|08002|08002|08002|08002|08002|08002|08002|  
  
## <a name="sqlbulkoperations"></a>SQLBulkOperations  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|24000|Consulte a tabela a seguir|HY010|O de HY010 NS [c]|  
  
## <a name="sqlbulkoperations-cursor-states"></a>SQLBulkOperations (Cursor estados)  
  
|S5<br /><br /> Aberto|S6<br /><br /> SQLFetch ou SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|– S8 [s] [d] S11 [x]|– S8 [s] [d] S11 [x]|HY010|  
  
## <a name="sqlcancel"></a>SQLCancel  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|--|--|S1 [1] S2 [nr] e [2] S3 [r] e S5 [2] [3] e [5] S6 ([3] ou [4]) e [6] S7 [4] e [7]|Consulte a tabela a seguir|  
  
 [1] **SQLExecDirect** retornou SQL_NEED_DATA.  
  
 [2] **SQLExecute** retornou SQL_NEED_DATA.  
  
 [3] **SQLBulkOperations** retornou SQL_NEED_DATA.  
  
 [4] **SQLSetPos** retornou SQL_NEED_DATA.  
  
 [5] **SQLFetch**, **SQLFetchScroll**, ou **SQLExtendedFetch** não tivesse sido chamada.  
  
 [6] **SQLFetch** ou **SQLFetchScroll** tivesse sido chamada.  
  
 [7] **SQLExtendedFetch** tivesse sido chamada.  
  
## <a name="sqlcancel-asynchronous-states"></a>SQLCancel (Estados assíncronos)  
  
|S11<br /><br /> Ainda em execução|S12<br /><br /> Assíncrona cancelada|  
|-----------------------------|-----------------------------|  
|/S12 NS [1] [2]|S12|  
  
 [1] a instrução foi temporariamente no estado S11 enquanto uma função estava em execução. **SQLCancel** foi chamado de um thread diferente.  
  
 [2] a instrução estava no estado S11 porque uma função chamada assíncrona retornou SQL_STILL_EXECUTING.  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|24000|24000|24000|S1 [np] S3 [p]|HY010|HY010|  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|Consulte a tabela a seguir|24000|-[s] S11 [x]|HY010|O de HY010 NS [c]|  
  
## <a name="sqlcolattribute-prepared-states"></a>SQLColAttribute (preparados estados)  
  
|S2<br /><br /> Nenhum resultado|S3<br /><br /> Resultados|  
|-----------------------|--------------------|  
|--[1] 07005[2]|-[s] S11 x|  
  
 [1] *FieldIdentifier* foi SQL_DESC_COUNT.  
  
 [2] *FieldIdentifier* não era SQL_DESC_COUNT.  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumnPrivileges, SQLColumns, SQLForeignKeys, SQLGetTypeInfo, SQLPrimaryKeys, SQLProcedureColumns, SQLProcedures, SQLSpecialColumns, SQLStatistics, SQLTablePrivileges e SQLTables  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S5 [s] S11 [x]|S1 [e] S5 [s] S11 [x]|S1 [e] e [1] S5 [s] e [1] S11 [x] e [1] 24000 [2]|Consulte a tabela a seguir|HY010|O de HY010 NS [c]|  
  
 [1] o resultado atual é o último ou apenas os resultados ou nenhum resultado atual. Para obter mais informações sobre vários resultados, consulte [vários resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 [2], o resultado atual não é o último resultado.  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables-cursor-states"></a>SQLColumnPrivileges, SQLColumns, SQLForeignKeys, SQLGetTypeInfo, SQLPrimaryKeys, SQLProcedureColumns, SQLProcedures, SQLSpecialColumns, SQLStatistics, SQLTablePrivileges e SQLTables (Cursor estados)  
  
|S5<br /><br /> Aberto|S6<br /><br /> SQLFetch ou SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000[1]|24000|  
  
 [1] esse erro é retornado pelo Gerenciador de Driver se **SQLFetch** ou **SQLFetchScroll** não retornou SQL_NO_DATA e é retornada pelo driver se **SQLFetch** ou **SQLFetchScroll** retornou SQL_NO_DATA.  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH [1]|--|--|--|--|HY010|NS [c] e [3] HY010 [s] ou [4]|  
|IH [2]|HY010|Consulte a tabela a seguir|24000|-[s] S11 x|HY010|NS [c] e [3] HY010 [s] ou [4]|  
  
 [1] essa linha mostra transições quando o *SourceDescHandle* argumento era um descartar, APD ou IPD.  
  
 [2] essa linha mostra transições quando o *SourceDescHandle* argumento era um IRD.  
  
 [3] de *SourceDescHandle* e *TargetDescHandle* argumentos eram os mesmos do **SQLCopyDesc** função que está executando de forma assíncrona.  
  
 [4] ou o *SourceDescHandle* argumento ou o *TargetDescHandle* argumento (ou ambos) eram diferentes em relação a **SQLCopyDesc** função que está em execução de forma assíncrona.  
  
## <a name="sqlcopydesc-prepared-states"></a>SQLCopyDesc (preparados estados)  
  
|S2<br /><br /> Nenhum resultado|S3<br /><br /> Resultados|  
|-----------------------|--------------------|  
|24000[1]|-[s] S11 [x]|  
  
 [1] Essa linha mostra transições quando o *SourceDescHandle* argumento era um IRD.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources e SQLDrivers  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqldescribecol"></a>SQLDescribeCol  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|Consulte a tabela a seguir|24000|-[s] S11 [x]|HY010|O de HY010 NS [c]|  
  
## <a name="sqldescribecol-prepared-states"></a>SQLDescribeCol (preparados estados)  
  
|S2<br /><br /> Nenhum resultado|S3<br /><br /> Resultados|  
|-----------------------|--------------------|  
|07005|-[s] S11 [x]|  
  
## <a name="sqldescribeparam"></a>SQLDescribeParam  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|-[s] S11 [x]|HY010|HY010|HY010|HY010 NS [c] [s]|  
  
## <a name="sqldisconnect"></a>SQLDisconnect  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|S0 [1]|S0 [1]|S0 [1]|S0 [1]|(HY010)|(HY010)|  
  
 [1] chamada **SQLDisconnect** libera todas as instruções associadas com a conexão. Além disso, isso retorna o estado de conexão para C2; o estado de conexão deve ser C4 antes do estado de instrução é S0.  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|-[2] ou [3] S1 [1]|– S1 [3] [np] e ([1] ou [2]) S1 [p] e [1] S2 [p] e [2]|– S1 [3] [np] e ([1] ou [2]) S1 [p] e [1] S3 [p] e [2]|(HY010)|(HY010)|  
  
 [1] de *CompletionType* argumento é SQL_COMMIT e **SQLGetInfo** retorna SQL_CB_DELETE para o tipo de informação de SQL_CURSOR_COMMIT_BEHAVIOR ou o *CompletionType*argumento é SQL_ROLLBACK e **SQLGetInfo** retorna SQL_CB_DELETE para o tipo de informação SQL_CURSOR_ROLLBACK_BEHAVIOR.  
  
 [2] de *CompletionType* argumento é SQL_COMMIT e **SQLGetInfo** retorna SQL_CB_CLOSE para o tipo de informação de SQL_CURSOR_COMMIT_BEHAVIOR ou o *CompletionType*argumento é SQL_ROLLBACK e **SQLGetInfo** retorna SQL_CB_CLOSE para o tipo de informação SQL_CURSOR_ROLLBACK_BEHAVIOR.  
  
 [3] de *CompletionType* argumento é SQL_COMMIT e **SQLGetInfo** retorna SQL_CB_PRESERVE para o tipo de informação de SQL_CURSOR_COMMIT_BEHAVIOR ou o *CompletionType*argumento é SQL_ROLLBACK e **SQLGetInfo** retorna SQL_CB_PRESERVE para o tipo de informação SQL_CURSOR_ROLLBACK_BEHAVIOR.  
  
## <a name="sqlexecdirect"></a>SQLExecDirect  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S4 [s] e [nr] S5 [s] e [r] S11 S8 [d] [x]|-[e] e [1] S1 [e] e [2] S4 [s] e [nr] S5 [s] e [r] S11 S8 [d] [x]|– [e], [1] e [3] S1 [e], [2] e [s], [3] S4 nr e [3] S5 [s], [r] e S8 [3] [d] e [3] S11 [x] e [3] 24000 [4]|Consulte a tabela a seguir|HY010|HY010 NS [c] [s]|  
  
 [1] o erro foi retornado pelo Gerenciador de Driver.  
  
 [2] o erro não foi retornado pelo Gerenciador de Driver.  
  
 [3], o resultado atual é o último ou apenas os resultados ou nenhum resultado atual. Para obter mais informações sobre vários resultados, consulte [vários resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 [4], o resultado atual não é o último resultado.  
  
## <a name="sqlexecdirect-cursor-states"></a>SQLExecDirect (Cursor estados)  
  
|S5<br /><br /> Aberto|S6<br /><br /> SQLFetch ou SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000 [1]|24000|  
  
 [1] esse erro é retornado pelo Gerenciador de Driver se **SQLFetch** ou **SQLFetchScroll** não retornou SQL_NO_DATA e é retornada pelo driver se **SQLFetch** ou  **SQLFetchScroll** retornou SQL_NO_DATA.  
  
## <a name="sqlexecute"></a>SQLExecute  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|(HY010)|Consulte a tabela a seguir|S2 [e], p e [1] S4 [s], [p] nr e [1] S5 [s], [p], [r] e [1] S8 [d] [p] e [1] S11 [x], [p] e [1] 24000 [p] e [2] HY010 [np]|Consulte a tabela de estados de cursor|HY010|HY010 NS [c] [s]|  
  
 [1] o resultado atual é o último ou apenas os resultados ou nenhum resultado atual. Para obter mais informações sobre vários resultados, consulte [vários resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 [2], o resultado atual não é o último resultado.  
  
## <a name="sqlexecute-prepared-states"></a>SQLExecute (preparados estados)  
  
|S2<br /><br /> Nenhum resultado|S3<br /><br /> Resultados|  
|-----------------------|--------------------|  
|S4 [s] S11 S8 [d] [x]|S5 [s] S11 S8 [d] [x]|  
  
## <a name="sqlexecute-cursor-states"></a>SQLExecute (Cursor estados)  
  
|S5<br /><br /> Aberto|S6<br /><br /> SQLFetch ou SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000 HY010 de [p] [np]|24000 [p], [1] HY010 [np]|24000 HY010 de [p] [np]|  
  
 [1] esse erro é retornado pelo Gerenciador de Driver se **SQLFetch** ou **SQLFetchScroll** não retornou SQL_NO_DATA e é retornada pelo driver se **SQLFetch** ou  **SQLFetchScroll** retornou SQL_NO_DATA.  
  
## <a name="sqlextendedfetch"></a>SQLExtendedFetch  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|S1010|S1010|24000|Consulte a tabela a seguir|S1010|S1010 NS [c] [s]|  
  
## <a name="sqlextendedfetch-cursor-states"></a>SQLExtendedFetch (Cursor estados)  
  
|S5<br /><br /> Aberto|S6<br /><br /> SQLFetch ou SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|S7 [s] ou [nf] S11 [x]|S1010|-[s] ou [nf] S11 [x]|  
  
## <a name="sqlfetch-and-sqlfetchscroll"></a>SQLFetch e SQLFetchScroll  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|24000|Consulte a tabela a seguir|HY010|HY010 NS [c] [s]|  
  
## <a name="sqlfetch-and-sqlfetchscroll-cursor-states"></a>SQLFetch e SQLFetchScroll (Estados de Cursor)  
  
|S5<br /><br /> Aberto|S6<br /><br /> SQLFetch ou SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|S6 [s] ou [nf] S11 [x]|-[s] ou [nf] S11 [x]|HY010|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|-- [1]|HY010|HY010|HY010|HY010|HY010|HY010|  
|IH [2]|S0|S0|S0|S0|HY010|HY010|  
|-- [3]|--|--|--|--|--|--|  
  
 [1] essa linha mostra transições quando *HandleType* foi SQL_HANDLE_ENV ou SQL_HANDLE_DBC.  
  
 [2] essa linha mostra transições quando *HandleType* foi SQL_HANDLE_STMT.  
  
 [3] essa linha mostra transições quando *HandleType* foi SQL_HANDLE_DESC e o descritor explicitamente foi alocado.  
  
## <a name="sqlfreestmt"></a>SQLFreeStmt  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH [1]|--|--|S1 [np] S2 [p]|S1 [np] S3 [p]|HY010|HY010|  
|IH [2]|--|--|--|--|HY010|HY010|  
  
 [1] essa linha mostra transições quando *opção* foi SQL_CLOSE.  
  
 [2] essa linha mostra transições quando *opção* foi SQL_UNBIND ou SQL_RESET_PARAMS. Se o *opção* argumento era SQL_DROP e o driver subjacente é um ODBC 3 *. x* driver, o Gerenciador de Driver mapeia isso para uma chamada para **SQLFreeHandle** com  *HandleType* definido como SQL_HANDLE_STMT. Para obter mais informações, consulte a tabela de transição para [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md).  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetcursorname"></a>SQLGetCursorName  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|--|--|HY010|HY010|  
  
## <a name="sqlgetdata"></a>SQLGetData  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|24000|Consulte a tabela a seguir|HY010|HY010 NS [c] [s]|  
  
## <a name="sqlgetdata-cursor-states"></a>SQLGetData (Cursor estados)  
  
|S5<br /><br /> Aberto|S6<br /><br /> SQLFetch ou SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|-[s] ou [nf] S11 [x] 24000 [b] HY109 [i]|-[s] ou [nf] S11 [x] 24000 [b] HY109 [i]|  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDescField e SQLGetDescRec  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|-[1] ou HY010 [2] [3]|Consulte a tabela a seguir|-[1] ou 24000 [2] [3]|-[1], [2] ou [3] S11 [3] e [x]|HY010|NS [c] ou [4] HY010 [o] e [5]|  
  
 [1] de *DescriptorHandle* argumento era um APD ou descartar.  
  
 [2] de *DescriptorHandle* argumento era um IPD.  
  
 [3] de *DescriptorHandle* argumento era um IRD.  
  
 [4] de *DescriptorHandle* argumento era igual a *DescriptorHandle* argumento o **SQLGetDescField** ou **SQLGetDescRec** função que está executando de forma assíncrona.  
  
 [5] o *DescriptorHandle* argumento for diferente do que o *DescriptorHandle* argumento o **SQLGetDescField** ou **SQLGetDescRec**função que está executando de forma assíncrona.  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec-prepared-states"></a>SQLGetDescField e SQLGetDescRec (preparados estados)  
  
|S2<br /><br /> Nenhum resultado|S3<br /><br /> Resultados|  
|-----------------------|--------------------|  
|-[1], [2] ou [3] S11 [2] e [x]|-[1], [2] ou [3] S11 [x]|  
  
 [1] de *DescriptorHandle* argumento era um APD ou descartar.  
  
 [2] de *DescriptorHandle* argumento era um IPD.  
  
 [3] de *DescriptorHandle* argumento era um IRD. Observe que essas funções sempre retornam SQL_NO_DATA no estado S2 quando *DescriptorHandle* foi um IRD.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField e SQLGetDiagRec  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--|--|--|  
|IH [2]|--[3]|--[3]|--|--|--[3]|--[3]|  
  
 [1] essa linha mostra transições quando *HandleType* foi SQL_HANDLE_ENV, SQL_HANDLE_DBC ou SQL_HANDLE_DESC.  
  
 [2] essa linha mostra transições quando *HandleType* foi SQL_HANDLE_STMT.  
  
 [3] **SQLGetDiagField** sempre retorna um erro neste estado quando *DiagIdentifier* é SQL_DIAG_ROW_COUNT.  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetfunctions"></a>SQLGetFunctions  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetinfo"></a>SQLGetInfo  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--[1] 24000[2]|--[1] 24000[2]|--[1] 24000[2]|Consulte a tabela a seguir|HY010|HY010|  
  
 [1] o atributo de instrução não era SQL_ATTR_ROW_NUMBER.  
  
 [2] o atributo de instrução foi SQL_ATTR_ROW_NUMBER.  
  
## <a name="sqlgetstmtattr-cursor-states"></a>SQLGetStmtAttr (Cursor estados)  
  
|S5<br /><br /> Aberto|S6<br /><br /> SQLFetch ou SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|--[1] 24000[2]|-[1] ou ([v] e [2]) 24000 [b] e [2] HY109 [i] e [2]|-[i] ou ([v] e [2]) 24000 [b] e [2] HY109 [1] e [2]|  
  
 [1] de *atributo* argumento não era SQL_ATTR_ROW_NUMBER.  
  
 [2] de *atributo* argumento foi SQL_ATTR_ROW_NUMBER.  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|--[1]|--[1]|– [s] e [2] S1 [nf], [np] e [4] S2 [nf], [p] e [4] S5 [s] e [3] S11 [x]|S1 [nf], [np] e [4] S3 [nf], [p] e [4] S4 [s] e [2] S5 [s] e [3] S11 [x]|HY010|HY010 NS [c] [s]|  
  
 [1] a função sempre retorna SQL_NO_DATA nesse estado.  
  
 [2], o próximo resultado é uma contagem de linhas.  
  
 [3], o próximo resultado é um conjunto de resultados.  
  
 [4], o resultado atual é o último resultado.  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlnumparams"></a>SQLNumParams  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|-[s] S11 [x]|-[s] S11 [x]|-[s] S11 [x]|HY010|HY010 NS [c] [s]|  
  
## <a name="sqlnumresultcols"></a>SQLNumResultCols  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|-[s] S11 [x]|-[s] S11 [x]|-[s] S11 [x]|HY010|HY010 NS [c] [s]|  
  
## <a name="sqlparamdata"></a>SQLParamData  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|HY010|HY010|Consulte a tabela a seguir|HY010 NS [c] [s]|  
  
## <a name="sqlparamdata-need-data-states"></a>SQLParamData (necessidade de estados de dados)  
  
|S8<br /><br /> Precisa de dados|S9<br /><br /> Coloque|S10<br /><br /> Pode colocar|  
|----------------------|---------------------|---------------------|  
|S1 [e] e [e], [1] S2 nr e S3 [2] [e] [r] e [2] S5 [e] e [4] S6 [e] e [5] S7 [e] e [x] de [3] S9 [d] S11|HY010|S1 [e] e [e], [1] S2 nr e S3 [2] [e], [r] e [2] S4 [s] nr, e ([1] ou [2]) S5 [s], [r] e ([1] ou [2]) S5 ([s] ou [e]) e [4] S6 ([s] ou [e]) e [5] S7 ([s] ou [e]) e S9 [3] [d] S11 [x]|  
  
 [1] **SQLExecDirect** retornou SQL_NEED_DATA.  
  
 [2] **SQLExecute** retornou SQL_NEED_DATA.  
  
 [3] **SQLSetPos** tinha sido chamado a partir do estado S7 e retornado SQL_NEED_DATA.  
  
 [4] **SQLBulkOperations** tinha sido chamado a partir do estado S5 e retornado SQL_NEED_DATA.  
  
 [5] **SQLSetPos** ou **SQLBulkOperations** tinha sido chamado a partir do estado S6 e retornado SQL_NEED_DATA.  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S2 [s] e [nr] S3 [s] e [r] S11 [x]|-[s] ou ([e] e [1]) S1 [e] e [2] S11 [x]|S1 [e] e [3] S2 [s], [nr] e [3] S3 [s], [r] e [3] S11 [x] e [3] 24000 [4]|Consulte a tabela a seguir|HY010|HY010 NS [c] [s]|  
  
 [1] a preparação falha por um motivo diferente de validar a instrução (o SQLSTATE foi HY009 [valor de argumento inválido] ou HY090 [comprimento inválido de cadeia de caracteres ou buffer]).  
  
 [2] a preparação da falha ao validar a instrução (o SQLSTATE não era HY009 [valor de argumento inválido] ou HY090 [comprimento inválido de cadeia de caracteres ou buffer]).  
  
 [3], o resultado atual é o último ou apenas os resultados ou nenhum resultado atual. Para obter mais informações sobre vários resultados, consulte [vários resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 [4], o resultado atual não é o último resultado.  
  
## <a name="sqlprepare-cursor-states"></a>SQLPrepare (Cursor estados)  
  
|S5<br /><br /> Aberto|S6<br /><br /> SQLFetch ou SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000|24000|  
  
## <a name="sqlputdata"></a>SQLPutData  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|HY010|HY010|Consulte a tabela a seguir|HY010 NS [c] [s]|  
  
## <a name="sqlputdata-need-data-states"></a>SQLPutData (necessidade de estados de dados)  
  
|S8<br /><br /> Precisa de dados|S9<br /><br /> Coloque|S10<br /><br /> Pode colocar|  
|----------------------|---------------------|---------------------|  
|HY010|S1 [e] e [e], [1] S2 nr e S3 [2] [e], [r] e [2] S5 [e] e [4] S6 [e] e [5] S7 [e] e [3] S10 [s] S11 [x]|-[e] [s] S1 e S2 [1] [e] nr e S3 [2] [e], [r] e [2] S5 [e] e [4] S6 [e] e [5] S7 [e] e [x] [3] S11 HY011 [6]|  
  
 [1] **SQLExecDirect** retornou SQL_NEED_DATA.  
  
 [2] **SQLExecute** retornou SQL_NEED_DATA.  
  
 [3] **SQLSetPos** tinha sido chamado a partir do estado S7 e retornado SQL_NEED_DATA.  
  
 [4] **SQLBulkOperations** tinha sido chamado a partir do estado S5 e retornado SQL_NEED_DATA.  
  
 [5] **SQLSetPos** ou **SQLBulkOperations** tinha sido chamado a partir do estado S6 e retornado SQL_NEED_DATA.  
  
 [6] uma ou mais chamadas para **SQLPutData** para um único parâmetro retornado SQL_SUCCESS e, em seguida, uma chamada para **SQLPutData** foi feita para o mesmo parâmetro com *StrLen_or_Ind* definido como SQL_NULL_DATA.  
  
## <a name="sqlrowcount"></a>SQLRowCount  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|(HY010)|(HY010)|--|--|(HY010)|(HY010)|  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--[2] 24000[3]|HY010|HY010|  
  
 [1] essa linha mostra transições quando *atributo* era um atributo de conexão. Para faz a transição quando *atributo* foi uma declaração de atributo, consulte a tabela de transição de instrução para **SQLSetStmtAttr**.  
  
 [2] de *atributo* argumento não era SQL_ATTR_CURRENT_CATALOG.  
  
 [3] de *atributo* argumento foi SQL_ATTR_CURRENT_CATALOG.  
  
## <a name="sqlsetcursorname"></a>SQLSetCursorName  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|24000|24000|HY010|HY010|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDescField e SQLSetDescRec  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH [1]|--|--|--|--|HY010|HY010|  
  
 [1] essa linha mostra transições onde o *DescriptorHandle* argumento é uma descartar, APD, IPD, ou (para **SQLSetDescField**) um IRD quando o *FieldIdentifier* argumento for SQL _ DESC_ARRAY_STATUS_PTR ou SQL_DESC_ROWS_PROCESSED_PTR. Erro ao chamar **SQLSetDescField** para um IRD quando *FieldIdentifier* for qualquer outro valor.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|HY011|HY011|HY011|HY011|Y011|HY01|HY011|  
  
## <a name="sqlsetpos"></a>SQLSetPos  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|24000|Consulte a tabela a seguir|HY010|HY010 NS [c] [s]|  
  
## <a name="sqlsetpos-cursor-states"></a>SQLSetPos (Cursor estados)  
  
|S5<br /><br /> Aberto|S6<br /><br /> SQLFetch ou SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|-[s] S8 [d] S11 [x] 24000 [b] HY109 [i]|-[s] S8 [d] S11 [x] 24000 [b] HY109 [i]|  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
  
|S0<br /><br /> Não alocado|S1<br /><br /> Alocado|S2 – S3<br /><br /> Prepared|S4<br /><br /> executado|S5 – S7<br /><br /> Cursor|S8 – S10<br /><br /> Precisa de dados|S11 – /S12<br /><br /> Assíncrono|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|– HY011 [1] [2]|--[1] 24000[2]|--[1] 24000[2]|HY010 [np] ou [1] HY011 [p] e [2]|HY010 [np] ou [1] HY011 [p] e [2]|  
  
 [1] de *atributo* argumento não era SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR, SQL_ATTR_USE_BOOKMARKS, SQL_ATTR_CURSOR_SCROLLABLE e SQL_ATTR_CURSOR_SENSITIVITY.  
  
 [2] de *atributo* argumento era SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR, SQL_ATTR_USE_BOOKMARKS, SQL_ATTR_CURSOR_SCROLLABLE e SQL_ATTR_CURSOR_SENSITIVITY.
