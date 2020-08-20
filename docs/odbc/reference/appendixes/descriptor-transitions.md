---
description: Transições de descritor
title: Transições de descritor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- state transitions [ODBC], descriptor
- transitioning states [ODBC], descriptor
- descriptor transitions [ODBC]
ms.assetid: 0cf24fe6-5e3c-45fa-81b8-4f52ddf8501d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 168df441e2e7e785f7dfc89894ec7aa9caf8207c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456592"
---
# <a name="descriptor-transitions"></a>Transições de descritor
Os descritores ODBC têm os três Estados a seguir.  
  
|Estado|Descrição|  
|-----------|-----------------|  
|D0|Descritor não alocado|  
|D1i|Descritor implicitamente alocado|  
|D1e|Descritor explicitamente alocado|  
  
 As tabelas a seguir mostram como cada função ODBC afeta o estado do descritor.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|D0<br /><br /> Não alocado|D1i<br /><br /> Implícita|D1e<br /><br /> Explícita|  
|------------------------|----------------------|----------------------|  
|D1i [1]|--|--|  
|D1E [2]|--|--|  
  
 [1] esta linha mostra as transições quando *HandleType* foi SQL_HANDLE_STMT.  
  
 [2] esta linha mostra transições quando o *HandleType* foi SQL_HANDLE_DESC.  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|D0<br /><br /> Não alocado|D1i<br /><br /> Implícita|D1e<br /><br /> Explícita|  
|------------------------|----------------------|----------------------|  
|Ih|--|--|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|D0<br /><br /> Não alocado|D1i<br /><br /> Implícita|D1e<br /><br /> Explícita|  
|------------------------|----------------------|----------------------|  
|--[1]|D0|--|  
|Ih 2|(HY017)|D0|  
  
 [1] esta linha mostra as transições quando *HandleType* foi SQL_HANDLE_STMT.  
  
 [2] esta linha mostra transições quando o *HandleType* foi SQL_HANDLE_DESC.  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDescField e SQLGetDescRec  
  
|D0<br /><br /> Não alocado|D1i<br /><br /> Implícita|D1e<br /><br /> Explícita|  
|------------------------|----------------------|----------------------|  
|Ih|--|--|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDescField e SQLSetDescRec  
  
|D0<br /><br /> Não alocado|D1i<br /><br /> Implícita|D1e<br /><br /> Explícita|  
|------------------------|----------------------|----------------------|  
|Ih uma|--|--|  
  
 [1] esta linha mostra transições quando *DescriptorHandle* era o identificador de um ARD, APD ou IPD ou (para **SQLSetDescField**) quando *DescriptorHandle* era o identificador de um IRD e *FieldIdentifier* era SQL_DESC_ARRAY_STATUS_PTR ou SQL_DESC_ROWS_PROCESSED_PTR.  
  
## <a name="all-other-odbc-functions"></a>Todas as outras funções ODBC  
  
|D0<br /><br /> Não alocado|D1i<br /><br /> Implícita|D1e<br /><br /> Explícita|  
|------------------------|----------------------|----------------------|  
|--|--|--|
