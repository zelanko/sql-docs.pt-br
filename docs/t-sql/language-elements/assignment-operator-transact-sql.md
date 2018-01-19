---
title: "= (Operador de atribuição) (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- operators [Transact-SQL], assignment
- assignment operators [Transact-SQL]
- headings [SQL Server columns]
- relationships [SQL Server], assignment operators
- column headings [SQL Server]
ms.assetid: c3040db6-21d6-40ac-a783-82c98ec006cc
caps.latest.revision: "29"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 1a4a3e1634579ecb985a6c99fc4973d7f8717c94
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="-assignment-operator-transact-sql"></a>= (Operador de atribuição) (Transact-SQL)
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
 [Operators &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Composta operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
  
