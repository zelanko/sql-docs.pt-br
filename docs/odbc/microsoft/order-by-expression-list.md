---
description: Lista de expressão ORDER BY
title: CLASSIFICAR por expressão-List | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ORDER BY clause [ODBC]
- SQL grammar [ODBC], order by clause
ms.assetid: 5ef88186-a99f-4e2c-a3f3-98a42d4f03a5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fd084a1012d445c89cacba168f21267238bc250f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340612"
---
# <a name="order-by-expression-list"></a>Lista de expressão ORDER BY
As expressões podem ser usadas na cláusula ORDER BY. Por exemplo, nas seguintes cláusulas, a tabela é ordenada por três expressões-chave: a + b, c + d e e.  
  
```  
SELECT * FROM emp  
ORDER BY a+b,c+d,e  
```  
  
 Nenhuma ordem é permitida em funções de conjunto ou em uma expressão que contém uma função de conjunto.
