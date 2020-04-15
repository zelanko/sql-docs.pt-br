---
title: Como personagem de fuga de predicado | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- LIKE predicate [ODBC]
- escape sequences [ODBC], LIKE predicate
ms.assetid: 185d6109-48cf-4981-bc40-ec2a4a90cafc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2e4f04b12911145eede3354532736cb92f1ae413
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306147"
---
# <a name="like-predicate-escape-character"></a>Caractere de escape de predicado LIKE
Em um predicado **LIKE,** o sinal percentual (%) corresponde a zero ou mais de qualquer caractere e o sublinhado (_) corresponde a qualquer personagem. Para corresponder a um sinal percentual real ou sublinhar em um predicado **LIKE,** um caractere de fuga deve vir antes do sinal percentual ou sublinhado. A seqüência de fuga que define o personagem de fuga do predicado **LIKE** é:  
  
 **{escape '** *escape-character* **'}**  
  
 onde *escape-character* é qualquer personagem suportado pela fonte de dados.  
  
 Para obter mais informações sobre a seqüência de fuga LIKE, consulte [COMO seqüência de fuga](../../../odbc/reference/appendixes/like-escape-sequence.md) no apêndice C: Gramática SQL.  
  
 Por exemplo, as seguintes instruções SQL criam o mesmo conjunto de resultados de nomes de clientes que começam com os caracteres "%AAA". A primeira declaração usa a sintaxe de seqüência de fuga. A segunda declaração usa a sintaxe nativa para o Microsoft® Access e não é interoperável. Observe que o segundo por cento do personagem em cada predicado **LIKE** é um personagem curinga que corresponde a zero ou mais de qualquer personagem.  
  
```  
SELECT Name FROM Customers WHERE Name LIKE '\%AAA%' {escape '\'}  
  
SELECT Name FROM Customers WHERE Name LIKE '[%]AAA%'  
```  
  
 Para determinar se o caractere de fuga do predicado **LIKE** é suportado por uma fonte de dados, um aplicativo chama **sqlGetInfo** com a opção SQL_LIKE_ESCAPE_CLAUSE.
