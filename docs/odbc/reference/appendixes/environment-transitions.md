---
title: "Transições de ambiente | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- environment transitions [ODBC]
- transitioning states [ODBC], environment
- state transitions [ODBC], environment
ms.assetid: 9d11b1ab-f4c8-48ca-9812-8c04303f939d
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 13d7b923f6fad42df791aa757d6c0349f58ad7d0
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="environment-transitions"></a>Transições de ambiente
Ambientes de ODBC tem os seguintes três estados.  
  
|Estado|Description|  
|-----------|-----------------|  
|E0|Ambiente não alocado|  
|E1|Ambiente alocado, não alocado de conexão|  
|E2|Alocada ambiente, alocada a conexão|  
  
 As tabelas a seguir mostram como cada função ODBC afeta o estado do ambiente.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|E0<br /><br /> Não alocado|E1<br /><br /> Alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|E1 [1]|--[4]|--[4]|  
|(IH) [2]|E2 [5]<br />(HY010) [6]|--[4]|  
|(IH) [3]|(IH)|--[4]|  
  
 [1] essa linha mostra transições quando *HandleType* foi SQL_HANDLE_ENV.  
  
 [2] essa linha mostra transições quando *HandleType* foi SQL_HANDLE_DBC.  
  
 [3] essa linha mostra transições quando *HandleType* foi SQL_HANDLE_STMT ou SQL_HANDLE_DESC.  
  
 [4] chamada **SQLAllocHandle** com *OutputHandlePtr* apontando para um identificador válido substituirá esse identificador. Isso pode ser um erro de programação de aplicativo.  
  
 [5] o atributo de ambiente SQL_ATTR_ODBC_VERSION tinha sido definido no ambiente.  
  
 [6] o atributo de ambiente de SQL_ATTR_ODBC_VERSION não tinha sido definido no ambiente.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources e SQLDrivers  
  
|E0<br /><br /> Não alocado|E1<br /><br /> Alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010) [2]|--[1]<br />(HY010) [2]|  
  
 [1] o atributo de ambiente SQL_ATTR_ODBC_VERSION tivesse sido definido no ambiente.  
  
 [2], o atributo de ambiente SQL_ATTR_ODBC_VERSION não tinha foi definido no ambiente.  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|E0<br /><br /> Não alocado|E1<br /><br /> Alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|(IH) [1]|--[3]<br />(HY010) [4]|--[3]<br />(HY010) [4]|  
|(IH) [2]|(IH)|--|  
  
 [1] essa linha mostra transições quando *HandleType* foi SQL_HANDLE_ENV.  
  
 [2] essa linha mostra transições quando *HandleType* foi SQL_HANDLE_DBC.  
  
 [3] o atributo de ambiente SQL_ATTR_ODBC_VERSION tivesse sido definido no ambiente.  
  
 [4], o atributo de ambiente SQL_ATTR_ODBC_VERSION não tinha foi definido no ambiente.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|E0<br /><br /> Não alocado|E1<br /><br /> Alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|(IH) [1]|E0|(HY010)|  
|(IH) [2]|(IH)|--[4]<br />E1 [5]|  
|(IH) [3]|(IH)|--|  
  
 [1] essa linha mostra transições quando *HandleType* foi SQL_HANDLE_ENV.  
  
 [2] essa linha mostra transições quando *HandleType* foi SQL_HANDLE_DBC.  
  
 [3] essa linha mostra transições quando *HandleType* foi SQL_HANDLE_STMT ou SQL_HANDLE_DESC.  
  
 [4] havia outros identificadores de conexão alocado.  
  
 [5] o identificador de conexão especificado em *tratar* era o identificador de conexão alocado somente.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField e SQLGetDiagRec  
  
|E0<br /><br /> Não alocado|E1<br /><br /> Alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|(IH) [1]|--|--|  
|(IH) [2]|(IH)|--|  
  
 [1] essa linha mostra transições quando *HandleType* foi SQL_HANDLE_ENV.  
  
 [2] essa linha mostra transições quando *HandleType* foi SQL_HANDLE_DBC, SQL_HANDLE_STMT ou SQL_HANDLE_DESC.  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|E0<br /><br /> Não alocado|E1<br /><br /> Alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010) [2]|--|  
  
 [1] o atributo de ambiente SQL_ATTR_ODBC_VERSION tivesse sido definido no ambiente.  
  
 [2], o atributo de ambiente SQL_ATTR_ODBC_VERSION não tinha foi definido no ambiente.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|E0<br /><br /> Não alocado|E1<br /><br /> Alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010) [2]|(HY011)|  
  
 [1] o atributo de ambiente SQL_ATTR_ODBC_VERSION tivesse sido definido no ambiente.  
  
 [2] de *atributo* argumento não era SQL_ATTR_ODBC_VERSION e o atributo de ambiente SQL_ATTR_ODBC_VERSION não tinha foi definido no ambiente.  
  
## <a name="all-other-odbc-functions"></a>Todas as outras funções ODBC  
  
|E0<br /><br /> Não alocado|E1<br /><br /> Alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|(IH)|(IH)|--|
