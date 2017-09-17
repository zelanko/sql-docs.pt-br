---
title: "COMO a sequência de Escape | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC escape sequences [ODBC], LIKE
- LIKE escape sequence [ODBC]
- escape sequences [ODBC], LIKE
ms.assetid: 798d75ea-be9d-4bef-b297-318bc327f1ca
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 678f2f8f720823ef5658ba7ee1e1391bbebc1c50
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="like-escape-sequence"></a>COMO a sequência de Escape
ODBC usa sequências de escape para a cláusula LIKE. A sintaxe dessa sequência de escape é da seguinte maneira:  
  
```  
{'escape-character'}  
```  
  
## <a name="remarks"></a>Comentários  
 Na notação BNF, a sintaxe é:  
  
 *Escape de ODBC-like* :: =  
  
 *Iniciador de esc ODBC* escape '*caractere de escape*' *terminador de esc ODBC*  
  
 *caractere de escape* :: = *caractere*  
  
 *Iniciador de esc ODBC* :: = {  
  
 *Terminador de esc ODBC* :: =}  
  
 Para determinar se o driver suporta o escape LIKE sequência, um aplicativo pode chamar **SQLGetInfo** com o tipo de informação SQL_LIKE_ESCAPE_CLAUSE.
