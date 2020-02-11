---
title: Caractere de escape de predicado LIKE | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68027232"
---
# <a name="like-predicate-escape-character"></a>Caractere de escape de predicado LIKE
Em um predicado **like** , o sinal de porcentagem (%) corresponde a zero ou mais de qualquer caractere e o sublinhado (_) corresponde a qualquer caractere. Para corresponder a um sinal de porcentagem real ou sublinhado em um predicado **like** , um caractere de escape deve vir antes do sinal de porcentagem ou sublinhado. A sequência de escape que define o caractere de escape de predicado **like** é:  
  
 **{escape '** *caractere de escape* **'}**  
  
 onde *escape-character* é qualquer caractere suportado pela fonte de dados.  
  
 Para obter mais informações sobre a sequência de escape LIKE, consulte [como sequência de escape](../../../odbc/reference/appendixes/like-escape-sequence.md) no Apêndice C: gramática SQL.  
  
 Por exemplo, as instruções SQL a seguir criam o mesmo conjunto de resultados de nomes de clientes que começam com os caracteres "% AAA". A primeira instrução usa a sintaxe de sequência de escape. A segunda instrução usa a sintaxe nativa para o Microsoft® Access e não é interoperável. Observe que o segundo caractere de porcentagem em cada predicado **like** é um caractere curinga que corresponde a zero ou mais de qualquer caractere.  
  
```  
SELECT Name FROM Customers WHERE Name LIKE '\%AAA%' {escape '\'}  
  
SELECT Name FROM Customers WHERE Name LIKE '[%]AAA%'  
```  
  
 Para determinar se o caractere de escape de predicado **like** tem suporte de uma fonte de dados, um aplicativo chama **SQLGetInfo** com a opção SQL_LIKE_ESCAPE_CLAUSE.
