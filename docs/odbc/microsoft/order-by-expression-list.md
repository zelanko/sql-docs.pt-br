---
title: ORDER BY-lista de expressões | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4c6be518211edb07251ff9234b095f3d3dde248b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63024267"
---
# <a name="order-by-expression-list"></a>Lista de expressão ORDER BY
Expressões podem ser usadas na cláusula ORDER BY. Por exemplo, nas seguintes cláusulas a tabela é solicitada pelos três expressões chave: a + b, c + d e.  
  
```  
SELECT * FROM emp  
ORDER BY a+b,c+d,e  
```  
  
 Nenhuma ordenação é permitida em funções de conjunto ou uma expressão que contém uma função de conjunto.
