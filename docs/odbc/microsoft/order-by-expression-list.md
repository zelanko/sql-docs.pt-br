---
title: ORDER BY-lista de expressões | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ORDER BY clause [ODBC]
- SQL grammar [ODBC], order by clause
ms.assetid: 5ef88186-a99f-4e2c-a3f3-98a42d4f03a5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3f210642f14b945ee62bd4eba3d1a722d8b8e11c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="order-by-expression-list"></a>ORDER BY-lista de expressões
Expressões podem ser usadas na cláusula ORDER BY. Por exemplo, as seguintes cláusulas a tabela é ordenada por três expressões chave: a + b, c + d e e.  
  
```  
SELECT * FROM emp  
ORDER BY a+b,c+d,e  
```  
  
 Nenhuma ordem é permitida em funções de conjunto ou uma expressão que contém uma função de conjunto.
