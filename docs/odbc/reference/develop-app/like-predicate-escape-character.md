---
description: Caractere de escape de predicado LIKE
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5304068e21dd6faf0e737a94add0cce177c4dabc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476548"
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
