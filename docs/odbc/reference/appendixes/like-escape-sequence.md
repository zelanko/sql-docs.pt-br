---
title: COMO a sequência de Escape | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- ODBC escape sequences [ODBC], LIKE
- LIKE escape sequence [ODBC]
- escape sequences [ODBC], LIKE
ms.assetid: 798d75ea-be9d-4bef-b297-318bc327f1ca
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 09602a92bce41b05fe6643ab12013b3e4637a273
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="like-escape-sequence"></a>COMO a sequência de Escape
ODBC usa sequências de escape para a cláusula LIKE. A sintaxe dessa sequência de escape é da seguinte maneira:  
  
```  
{'escape-character'}  
```  
  
## <a name="remarks"></a>Remarks  
 Na notação BNF, a sintaxe é:  
  
 *Escape de ODBC-like* :: =  
  
 *Iniciador de esc ODBC* escape '*caractere de escape*' *terminador de esc ODBC*  
  
 *caractere de escape* :: = *caractere*  
  
 *Iniciador de esc ODBC* :: = {  
  
 *Terminador de esc ODBC* :: =}  
  
 Para determinar se o driver suporta o escape LIKE sequência, um aplicativo pode chamar **SQLGetInfo** com o tipo de informação SQL_LIKE_ESCAPE_CLAUSE.
