---
title: COMO o caractere de Escape predicado | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- LIKE predicate [ODBC]
- escape sequences [ODBC], LIKE predicate
ms.assetid: 185d6109-48cf-4981-bc40-ec2a4a90cafc
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 38fa73fb069f7b7a037a61af711474b277cfa0d7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32911861"
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
