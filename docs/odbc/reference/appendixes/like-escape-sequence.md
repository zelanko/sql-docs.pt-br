---
title: Sequência de Escape LIKE | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 65447904f32b7e0457ed807f18e942b334ddc236
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47626614"
---
# <a name="like-escape-sequence"></a>Sequência de escape LIKE
ODBC usa sequências de escape para a cláusula LIKE. A sintaxe dessa sequência de escape é da seguinte maneira:  
  
```  
{'escape-character'}  
```  
  
## <a name="remarks"></a>Comentários  
 Na notação BNF, a sintaxe é:  
  
 *Escape de ODBC-like* :: =  
  
 *Iniciador do ODBC-esc* escape '*caractere de escape*' *terminador de esc ODBC*  
  
 *caractere de escape* :: = *caractere*  
  
 *Iniciador do ODBC-esc* :: = {  
  
 *Terminador de esc ODBC* :: =}  
  
 Para determinar se o driver dá suporte o LIKE escape sequência, um aplicativo pode chamar **SQLGetInfo** com o tipo de informação SQL_LIKE_ESCAPE_CLAUSE.
