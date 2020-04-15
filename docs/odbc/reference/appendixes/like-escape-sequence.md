---
title: Como seqüência de fuga | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 517c21f7b64fa7ceb662af9839a9fed1a1e6eff6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304917"
---
# <a name="like-escape-sequence"></a>Sequência de escape LIKE
ODBC usa seqüências de fuga para a cláusula LIKE. A sintaxe desta seqüência de fuga é a seguinte:  
  
```  
{'escape-character'}  
```  
  
## <a name="remarks"></a>Comentários  
 Na notação da BNF, a sintaxe é a seguinte:  
  
 *ODBC-like-escape* ::=  
  
 *ODBC-esc-iniciador* escape '*escape-character*' *ODBC-esc-terminator*  
  
 *escape-caractere* ::= *caractere*  
  
 *ODBC-esc-iniciador* ::= {  
  
 *ODBC-esc-terminator* ::= }  
  
 Para determinar se o driver suporta a seqüência de fuga LIKE, um aplicativo pode ligar para **o SQLGetInfo** com o SQL_LIKE_ESCAPE_CLAUSE tipo de informação.
