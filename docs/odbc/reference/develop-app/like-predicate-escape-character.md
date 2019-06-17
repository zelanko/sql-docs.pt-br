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
manager: craigg
ms.openlocfilehash: 30547551cc1793622eaa981c07bbc002d07a094d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63312917"
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
