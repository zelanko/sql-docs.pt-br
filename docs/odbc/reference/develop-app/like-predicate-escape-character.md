---
title: COMO o caractere de Escape de predicado | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 20310c60759aea17d61b9252fd73d226567a7a54
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68027232"
---
# <a name="like-predicate-escape-character"></a>Caractere de escape de predicado LIKE
Em um **como** predicado, o sinal de porcentagem (%) corresponde a zero ou mais do qualquer caractere de sublinhado (_) corresponde a qualquer caractere. Para corresponder a um sinal de porcentagem real ou sublinhado em uma **como** predicado, um caractere de escape deve vir antes do sinal de porcentagem ou um sublinhado. A sequência de escape que define o **como** caractere de escape de predicado é:  
  
 **{escape '** *escape-character* **'}**  
  
 em que *caractere de escape* é qualquer caractere que tem suportada pela fonte de dados.  
  
 Para obter mais informações sobre o tipo de sequência de escape, consulte [sequência de Escape, como](../../../odbc/reference/appendixes/like-escape-sequence.md) no Apêndice c: Gramática SQL.  
  
 Por exemplo, as seguintes instruções SQL criam o mesmo conjunto de resultados de cliente com nomes que começam com os caracteres "% AAA". A primeira instrução usa a sintaxe de sequência de escape. A segunda instrução usa a sintaxe de nativa para o Microsoft® Access e não é interoperável. Observe que a porcentagem do segundo caractere em cada **como** predicado é um caractere curinga que corresponde a zero ou mais de qualquer caractere.  
  
```  
SELECT Name FROM Customers WHERE Name LIKE '\%AAA%' {escape '\'}  
  
SELECT Name FROM Customers WHERE Name LIKE '[%]AAA%'  
```  
  
 Para determinar se o **, como** caractere de escape de predicado é suportado por uma fonte de dados, um aplicativo chama **SQLGetInfo** com a opção SQL_LIKE_ESCAPE_CLAUSE.
