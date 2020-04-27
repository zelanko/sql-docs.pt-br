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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ebfb5475d24d5fc70c4cb46a666b2573066565a1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81283296"
---
# <a name="environment-transitions"></a>Transições de ambiente
Os ambientes ODBC têm os três Estados a seguir.  
  
|Estado|Descrição|  
|-----------|-----------------|  
|E0|Ambiente não alocado|  
|E1|Ambiente alocado, conexão não alocada|  
|E2|Ambiente alocado, conexão alocada|  
  
 As tabelas a seguir mostram como cada função ODBC afeta o estado do ambiente.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|E0<br /><br /> Não alocado|E1<br /><br /> Alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|E1 [1]|--[4]|--[4]|  
|Ih 2|E2 [5]<br />(HY010) 152|--[4]|  
|Ih Beta|Ih|--[4]|  
  
 [1] esta linha mostra as transições quando *HandleType* foi SQL_HANDLE_ENV.  
  
 [2] esta linha mostra transições quando o *HandleType* foi SQL_HANDLE_DBC.  
  
 [3] essa linha mostra as transições quando *HandleType* foi SQL_HANDLE_STMT ou SQL_HANDLE_DESC.  
  
 [4] chamar **SQLAllocHandle** com *OutputHandlePtr* apontando para um identificador válido substitui esse identificador. Isso pode ser um erro de programação de aplicativo.  
  
 [5] o atributo de ambiente SQL_ATTR_ODBC_VERSION foi definido no ambiente.  
  
 [6] o atributo de ambiente SQL_ATTR_ODBC_VERSION não foi definido no ambiente.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources e sqldriveers  
  
|E0<br /><br /> Não alocado|E1<br /><br /> Alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|Ih|--[1]<br />(HY010) 2|--[1]<br />(HY010) 2|  
  
 [1] o atributo de ambiente SQL_ATTR_ODBC_VERSION foi definido no ambiente.  
  
 [2] o atributo de ambiente SQL_ATTR_ODBC_VERSION não foi definido no ambiente.  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|E0<br /><br /> Não alocado|E1<br /><br /> Alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|Ih uma|--[3]<br />(HY010) quatro|--[3]<br />(HY010) quatro|  
|Ih 2|Ih|--|  
  
 [1] esta linha mostra as transições quando *HandleType* foi SQL_HANDLE_ENV.  
  
 [2] esta linha mostra transições quando o *HandleType* foi SQL_HANDLE_DBC.  
  
 [3] o atributo de ambiente SQL_ATTR_ODBC_VERSION foi definido no ambiente.  
  
 [4] o atributo de ambiente SQL_ATTR_ODBC_VERSION não foi definido no ambiente.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|E0<br /><br /> Não alocado|E1<br /><br /> Alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|Ih uma|E0|(HY010)|  
|Ih 2|Ih|--[4]<br />E1 [5]|  
|Ih Beta|Ih|--|  
  
 [1] esta linha mostra as transições quando *HandleType* foi SQL_HANDLE_ENV.  
  
 [2] esta linha mostra transições quando o *HandleType* foi SQL_HANDLE_DBC.  
  
 [3] essa linha mostra as transições quando *HandleType* foi SQL_HANDLE_STMT ou SQL_HANDLE_DESC.  
  
 [4] havia outros identificadores de conexão alocados.  
  
 [5] o identificador de conexão especificado no *identificador* foi o único identificador de conexão alocado.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField e SQLGetDiagRec  
  
|E0<br /><br /> Não alocado|E1<br /><br /> Alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|Ih uma|--|--|  
|Ih 2|Ih|--|  
  
 [1] esta linha mostra as transições quando *HandleType* foi SQL_HANDLE_ENV.  
  
 [2] esta linha mostra transições quando o *HandleType* era SQL_HANDLE_DBC, SQL_HANDLE_STMT ou SQL_HANDLE_DESC.  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|E0<br /><br /> Não alocado|E1<br /><br /> Alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|Ih|--[1]<br />(HY010) 2|--|  
  
 [1] o atributo de ambiente SQL_ATTR_ODBC_VERSION foi definido no ambiente.  
  
 [2] o atributo de ambiente SQL_ATTR_ODBC_VERSION não foi definido no ambiente.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|E0<br /><br /> Não alocado|E1<br /><br /> Alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|Ih|--[1]<br />(HY010) 2|(HY011)|  
  
 [1] o atributo de ambiente SQL_ATTR_ODBC_VERSION foi definido no ambiente.  
  
 [2] o argumento de *atributo* não foi SQL_ATTR_ODBC_VERSION e o atributo de ambiente SQL_ATTR_ODBC_VERSION não foi definido no ambiente.  
  
## <a name="all-other-odbc-functions"></a>Todas as outras funções ODBC  
  
|E0<br /><br /> Não alocado|E1<br /><br /> Alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|Ih|Ih|--|
