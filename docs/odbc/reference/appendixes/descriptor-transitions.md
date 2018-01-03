---
title: "Transições de descritor | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- state transitions [ODBC], descriptor
- transitioning states [ODBC], descriptor
- descriptor transitions [ODBC]
ms.assetid: 0cf24fe6-5e3c-45fa-81b8-4f52ddf8501d
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2c762c4276fe236418be07dfe1fe93482d4d9a10
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="descriptor-transitions"></a>Transições de descritor
Descritores ODBC tem os seguintes três estados.  
  
|Estado|Description|  
|-----------|-----------------|  
|D0|Descritor de não alocado|  
|D1i|Descritor alocado implicitamente|  
|D1e|Descritor alocado explicitamente|  
  
 As tabelas a seguir mostram como cada função ODBC afeta o estado do descritor.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|D0<br /><br /> Não alocado|D1i<br /><br /> Implícito|D1e<br /><br /> Explícito|  
|------------------------|----------------------|----------------------|  
|D1i [1]|--|--|  
|D1e [2]|--|--|  
  
 [1] essa linha mostra transições quando *HandleType* foi SQL_HANDLE_STMT.  
  
 [2] essa linha mostra transições quando *HandleType* foi SQL_HANDLE_DESC.  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|D0<br /><br /> Não alocado|D1i<br /><br /> Implícito|D1e<br /><br /> Explícito|  
|------------------------|----------------------|----------------------|  
|(IH)|--|--|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|D0<br /><br /> Não alocado|D1i<br /><br /> Implícito|D1e<br /><br /> Explícito|  
|------------------------|----------------------|----------------------|  
|--[1]|D0|--|  
|(IH) [2]|(HY017)|D0|  
  
 [1] essa linha mostra transições quando *HandleType* foi SQL_HANDLE_STMT.  
  
 [2] essa linha mostra transições quando *HandleType* foi SQL_HANDLE_DESC.  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDescField e SQLGetDescRec  
  
|D0<br /><br /> Não alocado|D1i<br /><br /> Implícito|D1e<br /><br /> Explícito|  
|------------------------|----------------------|----------------------|  
|(IH)|--|--|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDescField e SQLSetDescRec  
  
|D0<br /><br /> Não alocado|D1i<br /><br /> Implícito|D1e<br /><br /> Explícito|  
|------------------------|----------------------|----------------------|  
|(IH) [1]|--|--|  
  
 [1] essa linha mostra transições quando *DescriptorHandle* era o identificador de APD, descartar ou IPD, ou (para **SQLSetDescField**) quando *DescriptorHandle* era o identificador de um ird e *FieldIdentifier* foi SQL_DESC_ARRAY_STATUS_PTR ou SQL_DESC_ROWS_PROCESSED_PTR.  
  
## <a name="all-other-odbc-functions"></a>Todas as outras funções ODBC  
  
|D0<br /><br /> Não alocado|D1i<br /><br /> Implícito|D1e<br /><br /> Explícito|  
|------------------------|----------------------|----------------------|  
|--|--|--|
