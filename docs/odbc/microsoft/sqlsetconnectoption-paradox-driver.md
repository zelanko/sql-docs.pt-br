---
title: SQLSetConnectOption (Driver Paradox) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLSetConnectOption
ms.assetid: 050ee2be-594e-4dbd-af67-8b6aae756cd1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9166aea00327d032f8081e24ead35706358c85fc
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetconnectoption-paradox-driver"></a>SQLSetConnectOption (Driver Paradox)
> [!NOTE]  
>  Este tópico fornece informações específicas de Driver Paradox. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|fOption|Comentário|  
|-------------|-------------|  
|SQL_ACCESS_MODE|O fOption SQL_ACCESS_MODE pode ser definido como SQL_MODE_READ_ONLY ou SQL_MODE_READ_WRITE. No entanto, o driver não impede que atualizações se SQL_ACCESS_MODE for definido como SQL_MODE_READ_ONLY.|  
|SQL_AUTOCOMMIT|O driver do Paradox suporta apenas SQL_AUTOCOMMIT sendo definido como (o estado padrão), porque eles não dão suporte a transações.|  
|SQL_CURRENT_QUALIFIER|Tem suporte.|  
|SQL_LOGIN_TIMEOUT|Sem suporte.|  
|SQL_OPT_TRACE|Tem suporte.|  
|SQL_OPT_TRACEFILE|Tem suporte.|  
|SQL_PACKET_SIZE|Sem suporte.|  
|SQL_QUIET_MODE|Sem suporte.|  
|SQL_TRANSLATE_DLL|Sem suporte.|  
|SQL_TRANSLATION_OPTION|Sem suporte.|  
|SQL_TXN_ISOLATION|Sem suporte.|

