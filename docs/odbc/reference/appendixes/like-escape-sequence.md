---
title: Sequência de escape LIKE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC escape sequences [ODBC], LIKE
- LIKE escape sequence [ODBC]
- escape sequences [ODBC], LIKE
ms.assetid: 798d75ea-be9d-4bef-b297-318bc327f1ca
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 629ceaf666ae732d0838a216272c308dcb5b5658
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68041715"
---
# <a name="like-escape-sequence"></a>Sequência de escape LIKE
O ODBC usa sequências de escape para a cláusula LIKE. A sintaxe dessa sequência de escape é a seguinte:  
  
```  
{'escape-character'}  
```  
  
## <a name="remarks"></a>Comentários  
 Na notação BNF, a sintaxe é a seguinte:  
  
 *ODBC-like-escape* :: =  
  
 *ODBC-ESC-Initiator* escape "*escape-character*" *ODBC-ESC-terminador*  
  
 *escape-caractere* :: = *caractere*  
  
 *ODBC-ESC-Initiator* :: = {  
  
 *ODBC-ESC-terminador* :: =}  
  
 Para determinar se o driver dá suporte à sequência de escape LIKE, um aplicativo pode chamar **SQLGetInfo** com o tipo de informação SQL_LIKE_ESCAPE_CLAUSE.
