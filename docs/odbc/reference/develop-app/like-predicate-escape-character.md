---
title: COMO o caractere de Escape predicado | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- LIKE predicate [ODBC]
- escape sequences [ODBC], LIKE predicate
ms.assetid: 185d6109-48cf-4981-bc40-ec2a4a90cafc
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f807bd12056f3c6a8e7a38efee56f0a6b6727066
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="like-predicate-escape-character"></a>COMO o caractere de Escape de predicado
Em um **como** predicado, o sinal de porcentagem (%) correspondências zero ou mais de qualquer caractere e o caractere de sublinhado (_) corresponde a qualquer caractere. Para corresponder a um sinal de porcentagem real ou sublinhado em um **como** predicado, um caractere de escape deve vir antes do sinal de porcentagem ou um sublinhado. A sequência de escape que define o **como** caractere de escape de predicado é:  
  
 **{escape '** *caractere de escape* **'}**  
  
 onde *caractere de escape* é qualquer caractere com suporte pela fonte de dados.  
  
 Para obter mais informações sobre o tipo de sequência de escape, consulte [como sequência de Escape](../../../odbc/reference/appendixes/like-escape-sequence.md) na gramática do apêndice c: SQL.  
  
 Por exemplo, as seguintes instruções SQL criam o mesmo conjunto de resultados do cliente nomes que começam com os caracteres "AAA %". A primeira instrução usa a sintaxe de sequência de escape. A segunda instrução usa a sintaxe de nativo para o Microsoft® Access e não é interoperável. Observe que a porcentagem segundo caractere em cada **como** predicado é um caractere curinga que corresponde a zero ou mais caracteres.  
  
```  
SELECT Name FROM Customers WHERE Name LIKE '\%AAA%' {escape '\'}  
  
SELECT Name FROM Customers WHERE Name LIKE '[%]AAA%'  
```  
  
 Para determinar se o **como** caractere de escape de predicado é suportada por uma fonte de dados, um aplicativo chama **SQLGetInfo** com a opção SQL_LIKE_ESCAPE_CLAUSE.
