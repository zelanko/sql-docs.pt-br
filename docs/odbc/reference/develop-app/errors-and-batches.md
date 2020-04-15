---
title: Erros e Lotes | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 36a402686a695a08748df24a7b40a228d7a2ca7f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300426"
---
# <a name="errors-and-batches"></a>Erros e lotes
Quando ocorre um erro durante a execução de um lote de instruções SQL, um dos quatro resultados a seguir é possível. (Cada resultado possível é específico da fonte de dados e pode até depender das declarações incluídas no lote.)  
  
-   Nenhuma declaração no lote é executada.  
  
-   Nenhuma declaração no lote é executada e a transação é revertida.  
  
-   Todas as declarações antes da instrução de erro são executadas.  
  
-   Todas as declarações, exceto a instrução de erro, são executadas.  
  
 Nos dois primeiros casos, **o retorno sqlexecute** e **sqlexecdirect** SQL_ERROR. Nos dois últimos casos, podem retornar SQL_SUCCESS_WITH_INFO ou SQL_SUCCESS, dependendo da implementação. Em todos os casos, mais informações de erro podem ser recuperadas com **SQLGetDiagField,** **SQLGetDiagRec**ou **SQLError**. No entanto, a natureza e a profundidade dessas informações são específicas da fonte de dados. Além disso, é improvável que essas informações identifiquem exatamente a declaração por engano.
