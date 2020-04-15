---
title: Transições ambientais | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283296"
---
# <a name="environment-transitions"></a>Transições de ambiente
Os ambientes ODBC têm os seguintes três estados.  
  
|Estado|Descrição|  
|-----------|-----------------|  
|E0|Ambiente não alocado|  
|E1|Ambiente alocado, conexão não alocada|  
|E2|Ambiente alocado, conexão alocada|  
  
 As tabelas a seguir mostram como cada função ODBC afeta o estado ambiental.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|E0<br /><br /> Não alocado|E1<br /><br /> Alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|E1[1]|--[4]|--[4]|  
|(IH) [2]|E2[5]<br />(HY010) [6]|--[4]|  
|(IH) [3]|(IH)|--[4]|  
  
 [1] Esta linha mostra transições quando *handleType* foi SQL_HANDLE_ENV.  
  
 [2] Esta linha mostra transições quando *handleType* foi SQL_HANDLE_DBC.  
  
 [3] Esta linha mostra transições quando *handleType* foi SQL_HANDLE_STMT ou SQL_HANDLE_DESC.  
  
 [4] Chamar **SQLAllocHandle** com *OutputHandlePtr* apontando para uma alça válida sobregrava que o cabo. Isso pode ser um erro de programação de aplicativos.  
  
 [5] O SQL_ATTR_ODBC_VERSION atributo ambiental tinha sido definido sobre o meio ambiente.  
  
 [6] O SQL_ATTR_ODBC_VERSION atributo ambiental não tinha sido definido sobre o meio ambiente.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources e SQLDrivers  
  
|E0<br /><br /> Não alocado|E1<br /><br /> Alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010) [2]|--[1]<br />(HY010) [2]|  
  
 [1] O atributo SQL_ATTR_ODBC_VERSION ambiente tinha sido definido sobre o meio ambiente.  
  
 [2] O atributo SQL_ATTR_ODBC_VERSION ambiente não havia sido definido sobre o meio ambiente.  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|E0<br /><br /> Não alocado|E1<br /><br /> Alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|(IH) [1]|--[3]<br />(HY010) [4]|--[3]<br />(HY010) [4]|  
|(IH) [2]|(IH)|--|  
  
 [1] Esta linha mostra transições quando *handleType* foi SQL_HANDLE_ENV.  
  
 [2] Esta linha mostra transições quando *handleType* foi SQL_HANDLE_DBC.  
  
 [3] O SQL_ATTR_ODBC_VERSION atributo ambiental tinha sido definido sobre o meio ambiente.  
  
 [4] O SQL_ATTR_ODBC_VERSION atributo ambiental não tinha sido definido sobre o meio ambiente.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|E0<br /><br /> Não alocado|E1<br /><br /> Alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|(IH) [1]|E0|(HY010)|  
|(IH) [2]|(IH)|--[4]<br />E1[5]|  
|(IH) [3]|(IH)|--|  
  
 [1] Esta linha mostra transições quando *handleType* foi SQL_HANDLE_ENV.  
  
 [2] Esta linha mostra transições quando *handleType* foi SQL_HANDLE_DBC.  
  
 [3] Esta linha mostra transições quando *handleType* foi SQL_HANDLE_STMT ou SQL_HANDLE_DESC.  
  
 [4] Havia outras alças de conexão alocadas.  
  
 [5] O cabo de conexão especificado no *Handle* era o único cabo de conexão alocado.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField e SQLGetDiagRec  
  
|E0<br /><br /> Não alocado|E1<br /><br /> Alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|(IH) [1]|--|--|  
|(IH) [2]|(IH)|--|  
  
 [1] Esta linha mostra transições quando *handleType* foi SQL_HANDLE_ENV.  
  
 [2] Esta linha mostra transições quando *handleType* foi SQL_HANDLE_DBC, SQL_HANDLE_STMT ou SQL_HANDLE_DESC.  
  
## <a name="sqlgetenvattr"></a>SQlGetEnvAttr  
  
|E0<br /><br /> Não alocado|E1<br /><br /> Alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010) [2]|--|  
  
 [1] O atributo SQL_ATTR_ODBC_VERSION ambiente tinha sido definido sobre o meio ambiente.  
  
 [2] O atributo SQL_ATTR_ODBC_VERSION ambiente não havia sido definido sobre o meio ambiente.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|E0<br /><br /> Não alocado|E1<br /><br /> Alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010) [2]|(Hy011)|  
  
 [1] O atributo SQL_ATTR_ODBC_VERSION ambiente tinha sido definido sobre o meio ambiente.  
  
 [2] O argumento *do Atributo* não foi SQL_ATTR_ODBC_VERSION, e o SQL_ATTR_ODBC_VERSION atributo ambiental não havia sido definido sobre o meio ambiente.  
  
## <a name="all-other-odbc-functions"></a>Todas as outras funções ODBC  
  
|E0<br /><br /> Não alocado|E1<br /><br /> Alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|(IH)|(IH)|--|
