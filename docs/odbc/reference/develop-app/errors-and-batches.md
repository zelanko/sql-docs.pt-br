---
description: Erros e lotes
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1e5cdf4d394ffa1c17173aedc4485b6979cf371e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461488"
---
# <a name="errors-and-batches"></a>Erros e lotes
Quando ocorre um erro durante a execução de um lote de instruções SQL, um dos quatro resultados a seguir é possível. (Cada resultado possível é específico da fonte de dados e pode até mesmo depender das instruções incluídas no lote.)  
  
-   Nenhuma instrução no lote é executada.  
  
-   Nenhuma instrução no lote é executada e a transação é revertida.  
  
-   Todas as instruções antes da execução da instrução de erro.  
  
-   Todas as instruções, exceto a instrução de erro, são executadas.  
  
 Nos dois primeiros casos, **SQLExecute** e **SQLExecDirect** retornam SQL_ERROR. Nos dois últimos casos, eles podem retornar SQL_SUCCESS_WITH_INFO ou SQL_SUCCESS, dependendo da implementação. Em todos os casos, outras informações de erro podem ser recuperadas com **SQLGetDiagField**, **SQLGetDiagRec**ou **SqlError**. No entanto, a natureza e a profundidade dessas informações são específicas da fonte de dados. Além disso, é improvável que essas informações identifiquem exatamente a instrução em caso de erro.
