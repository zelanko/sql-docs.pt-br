---
title: Erros e lotes | Microsoft Docs
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
- batches [ODBC], errors
- sql_success_with_info [ODBC]
- sql_success [ODBC]
- SQL statements [ODBC], batches
- sql_error [ODBC]
ms.assetid: 6debd41d-9f4c-4f4c-a44b-2993da5306f0
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4f00a70ec411824da13d37666c7b22f92248a236
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="errors-and-batches"></a>Erros e lotes
Quando ocorre um erro ao executar um lote de instruções SQL, um dos seguintes quatro resultados são possíveis. (Cada resultado possível é específico da fonte de dados e ainda pode depender as instruções incluídas no lote.)  
  
-   Nenhuma instrução no lote é executadas.  
  
-   Nenhuma instrução no lote é executadas e a transação será revertida.  
  
-   Todas as instruções antes da instrução de erro são executadas.  
  
-   Todas as instruções, exceto a instrução de erro são executadas.  
  
 Nos dois primeiros casos, **SQLExecute** e **SQLExecDirect** retornará SQL_ERROR. Nos dois últimos casos, eles podem retornar SQL_SUCCESS_WITH_INFO ou SQL_SUCCESS, dependendo da implementação. Em todos os casos, mais informações sobre o erro pode ser recuperado com **SQLGetDiagField**, **SQLGetDiagRec**, ou **SQLError**. No entanto, a natureza e a profundidade de informações é específico da fonte de dados. Além disso, essa informação é improvável identificar exatamente a instrução em erro.
