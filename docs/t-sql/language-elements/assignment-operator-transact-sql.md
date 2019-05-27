---
title: = (Operador de atribuição) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 144185dfc0ce2a4318b29b2526bdba51ceb046ab
ms.sourcegitcommit: 5ed48c7dc6bed153079bc2b23a1e0506841310d1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65980592"
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
  
## <a name="see-also"></a>Consulte Também  
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Operadores compostos &#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
  
