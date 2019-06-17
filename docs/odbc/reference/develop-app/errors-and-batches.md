---
title: Erros e lotes | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- batches [ODBC], errors
- sql_success_with_info [ODBC]
- sql_success [ODBC]
- SQL statements [ODBC], batches
- sql_error [ODBC]
ms.assetid: 6debd41d-9f4c-4f4c-a44b-2993da5306f0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 97179574407dca56026f9d5216e4978069cffc1e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62942979"
---
# <a name="errors-and-batches"></a>Erros e lotes
Quando ocorre um erro ao executar um lote de instruções SQL, uma das quatro seguintes resultados são possíveis. (Cada resultado possível é específico da fonte de dados e até mesmo pode depender das instruções incluídas no lote.)  
  
-   Não há instruções no lote são executadas.  
  
-   Nenhuma instrução no lote é executadas e a transação será revertida.  
  
-   Todas as instruções antes da instrução de erro são executadas.  
  
-   Todas as instruções, exceto a instrução de erro são executadas.  
  
 Nos dois primeiros casos, **SQLExecute** e **SQLExecDirect** retornará SQL_ERROR. Os dois últimos casos, eles podem retornar SQL_SUCCESS_WITH_INFO ou SQL_SUCCESS, dependendo da implementação. Em todos os casos, ainda mais informações sobre o erro pode ser recuperado com **SQLGetDiagField**, **SQLGetDiagRec**, ou **SQLError**. No entanto, a natureza e a profundidade dessas informações é específico da fonte de dados. Além disso, essa informação é improvável identificar exatamente a instrução em erro.
