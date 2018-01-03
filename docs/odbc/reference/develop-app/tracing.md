---
title: Rastreamento | Microsoft Docs
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
- tracing options [ODBC], about tracing
- driver manager [ODBC], tracing
ms.assetid: 77ed4c6c-d976-4eb2-8526-a12697b0ef83
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 780cbed9bb417c32b6a7ed33f68e4671c612ca6e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="tracing"></a>Rastreamento
O Gerenciador de Driver ODBC tem um recurso de rastreamento que permite que a sequência de chamadas de função feitas por um aplicativo ODBC a ser registrada e transcrita em um arquivo de log. O rastreamento é executado por uma DLL de rastreamento que captura chamadas entre o aplicativo e o Gerenciador de Driver e entre o Gerenciador de Driver e o driver. Esse método de rastreamento substitui o rastreamento executado pelo ODBC 2*. x* Gerenciador de Driver e o rastreamento realizadas em ODBC 2*. x* por Spy ODBC.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [DLL de rastreamento](../../../odbc/reference/develop-app/trace-dll.md)  
  
-   [Arquivo de rastreamento](../../../odbc/reference/develop-app/trace-file.md)  
  
-   [Habilitando o rastreamento](../../../odbc/reference/develop-app/enabling-tracing.md)  
  
-   [Rastreamento dinâmico](../../../odbc/reference/develop-app/dynamic-tracing.md)
