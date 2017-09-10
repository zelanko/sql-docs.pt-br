---
title: "Operador de atribuição (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- operators [Transact-SQL], assignment
- assignment operators [Transact-SQL]
- headings [SQL Server columns]
- relationships [SQL Server], assignment operators
- column headings [SQL Server]
ms.assetid: c3040db6-21d6-40ac-a783-82c98ec006cc
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d10872712d1b7114655b5d95ab9b871709c55b14
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="assignment-operator-transact-sql"></a>Operador de atribuição(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  O sinal de igual (=) é o único operador de atribuição [!INCLUDE[tsql](../../includes/tsql-md.md)]. No exemplo a seguir, a variável `@MyCounter` é criada, e o operador de atribuição define `@MyCounter` com um valor retornado por uma expressão.  
  
```  
DECLARE @MyCounter INT;  
SET @MyCounter = 1;  
```  
  
 O operador de atribuição também pode ser usado para estabelecer a relação entre um título de coluna e a expressão que define os valores para a coluna. O exemplo a seguir exibe os títulos de coluna `FirstColumnHeading` e `SecondColumnHeading`. A cadeia de caracteres `xyz` é exibida no título de coluna `FirstColumnHeading` para todas as linhas. Depois, cada ID de produto da tabela `Product` é listada no título de coluna `SecondColumnHeading`.  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstColumnHeading = 'xyz',  
       SecondColumnHeading = ProductID  
FROM Production.Product;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
  
