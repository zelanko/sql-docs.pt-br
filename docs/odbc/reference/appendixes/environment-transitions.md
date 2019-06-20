---
title: Transições de ambiente | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- environment transitions [ODBC]
- transitioning states [ODBC], environment
- state transitions [ODBC], environment
ms.assetid: 9d11b1ab-f4c8-48ca-9812-8c04303f939d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3ed2bbf40ac333db34d3920b2ed2ec688c344bfe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63189001"
---
# <a name="environment-transitions"></a>Transições de ambiente
Ambientes de ODBC tem três estados.  
  
|Estado|Descrição|  
|-----------|-----------------|  
|E0|Ambiente não alocado|  
|E1|Ambiente alocado, não alocado a conexão|  
|E2|Alocado ambiente, alocada a conexão|  
  
 As tabelas a seguir mostram como cada função ODBC afeta o estado do ambiente.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|E0<br /><br /> Não alocado|E1<br /><br /> alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|E1[1]|--[4]|--[4]|  
|(IH)[2]|E2[5]<br />(HY010)[6]|--[4]|  
|(IH)[3]|(IH)|--[4]|  
  
 [1] essa linha mostra as transições quando *HandleType* foi SQL_HANDLE_ENV.  
  
 [2] essa linha mostra as transições quando *HandleType* foi SQL_HANDLE_DBC.  
  
 [3] essa linha mostra as transições quando *HandleType* era SQL_HANDLE_STMT ou SQL_HANDLE_DESC.  
  
 [4] chamar **SQLAllocHandle** com *OutputHandlePtr* apontando para um identificador válido substituirá esse identificador. Isso pode ser um erro de programação de aplicativo.  
  
 [5] o atributo de ambiente SQL_ATTR_ODBC_VERSION tivesse sido definido no ambiente.  
  
 [6] o atributo de ambiente SQL_ATTR_ODBC_VERSION não tinha foi definido no ambiente.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources e SQLDrivers  
  
|E0<br /><br /> Não alocado|E1<br /><br /> alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010)[2]|--[1]<br />(HY010)[2]|  
  
 [1] o atributo de ambiente SQL_ATTR_ODBC_VERSION tivesse sido definido no ambiente.  
  
 [2] o atributo de ambiente SQL_ATTR_ODBC_VERSION não tinha foi definido no ambiente.  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|E0<br /><br /> Não alocado|E1<br /><br /> alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|(IH)[1]|--[3]<br />(HY010)[4]|--[3]<br />(HY010)[4]|  
|(IH)[2]|(IH)|--|  
  
 [1] essa linha mostra as transições quando *HandleType* foi SQL_HANDLE_ENV.  
  
 [2] essa linha mostra as transições quando *HandleType* foi SQL_HANDLE_DBC.  
  
 [3] o atributo de ambiente SQL_ATTR_ODBC_VERSION tivesse sido definido no ambiente.  
  
 [4], o atributo de ambiente SQL_ATTR_ODBC_VERSION não tinha foi definido no ambiente.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|E0<br /><br /> Não alocado|E1<br /><br /> alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|(IH)[1]|E0|(HY010)|  
|(IH)[2]|(IH)|--[4]<br />E1[5]|  
|(IH)[3]|(IH)|--|  
  
 [1] essa linha mostra as transições quando *HandleType* foi SQL_HANDLE_ENV.  
  
 [2] essa linha mostra as transições quando *HandleType* foi SQL_HANDLE_DBC.  
  
 [3] essa linha mostra as transições quando *HandleType* era SQL_HANDLE_STMT ou SQL_HANDLE_DESC.  
  
 [4] havia outros identificadores de conexão alocado.  
  
 [5] o identificador de conexão especificado em *manipular* era o identificador de conexão alocado única.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField e SQLGetDiagRec  
  
|E0<br /><br /> Não alocado|E1<br /><br /> alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|(IH)[1]|--|--|  
|(IH)[2]|(IH)|--|  
  
 [1] essa linha mostra as transições quando *HandleType* foi SQL_HANDLE_ENV.  
  
 [2] essa linha mostra as transições quando *HandleType* era SQL_HANDLE_DBC, SQL_HANDLE_STMT ou SQL_HANDLE_DESC.  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|E0<br /><br /> Não alocado|E1<br /><br /> alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010)[2]|--|  
  
 [1] o atributo de ambiente SQL_ATTR_ODBC_VERSION tivesse sido definido no ambiente.  
  
 [2] o atributo de ambiente SQL_ATTR_ODBC_VERSION não tinha foi definido no ambiente.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|E0<br /><br /> Não alocado|E1<br /><br /> alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010)[2]|(HY011)|  
  
 [1] o atributo de ambiente SQL_ATTR_ODBC_VERSION tivesse sido definido no ambiente.  
  
 [2]] o *atributo* argumento não era SQL_ATTR_ODBC_VERSION e o atributo de ambiente de SQL_ATTR_ODBC_VERSION não tinha sido definido no ambiente.  
  
## <a name="all-other-odbc-functions"></a>Todas as outras funções ODBC  
  
|E0<br /><br /> Não alocado|E1<br /><br /> alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|(IH)|(IH)|--|
