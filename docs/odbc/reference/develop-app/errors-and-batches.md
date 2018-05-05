---
title: Erros e lotes | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- batches [ODBC], errors
- sql_success_with_info [ODBC]
- sql_success [ODBC]
- SQL statements [ODBC], batches
- sql_error [ODBC]
ms.assetid: 6debd41d-9f4c-4f4c-a44b-2993da5306f0
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d00672166039421fb8518c52a58d19d73d02d477
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="errors-and-batches"></a>Erros e lotes
Quando ocorre um erro ao executar um lote de instruções SQL, um dos seguintes quatro resultados são possíveis. (Cada resultado possível é específico da fonte de dados e ainda pode depender as instruções incluídas no lote.)  
  
-   Nenhuma instrução no lote é executadas.  
  
-   Nenhuma instrução no lote é executadas e a transação será revertida.  
  
-   Todas as instruções antes da instrução de erro são executadas.  
  
-   Todas as instruções, exceto a instrução de erro são executadas.  
  
 Nos dois primeiros casos, **SQLExecute** e **SQLExecDirect** retornará SQL_ERROR. Nos dois últimos casos, eles podem retornar SQL_SUCCESS_WITH_INFO ou SQL_SUCCESS, dependendo da implementação. Em todos os casos, mais informações sobre o erro pode ser recuperado com **SQLGetDiagField**, **SQLGetDiagRec**, ou **SQLError**. No entanto, a natureza e a profundidade de informações é específico da fonte de dados. Além disso, essa informação é improvável identificar exatamente a instrução em erro.
