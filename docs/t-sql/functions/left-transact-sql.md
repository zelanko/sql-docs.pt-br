---
title: ESQUERDA (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LEFT
- LEFT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- character strings [SQL Server], LEFT
- characters [SQL Server], leftmost
- LEFT function
- leftmost character of expression
ms.assetid: 44a8c71b-63d8-458b-8b5d-99d570067c3c
caps.latest.revision: 48
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0b0ec58ed9e8bbaae6f4f4ae90834f415476b039
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="left-transact-sql"></a>LEFT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna a parte da esquerda de uma cadeia de caracteres com o número de caracteres especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
LEFT ( character_expression , integer_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 É um [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de caractere ou dados binários. *character_expression* pode ser uma constante, variável ou coluna. *character_expression* pode ser de qualquer tipo de dados, exceto **texto** ou **ntext**, que pode ser convertido implicitamente em **varchar** ou  **nvarchar**. Caso contrário, use o [CAST](../../t-sql/functions/cast-and-convert-transact-sql.md) função para converter explicitamente *character_expression*.  
  
 *integer_expression*  
 É um inteiro positivo que especifica o número de caracteres da *character_expression* será retornado. Se *integer_expression* é negativo, um erro será retornado. Se *integer_expression* é do tipo **bigint** e contém um valor grande, *character_expression* deve ser de um tipo de dados grandes, como **varchar (max)**.  
  
 O *integer_expression* parâmetro contagens de um caractere substituto de UTF-16 como um caractere.  
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna **varchar** quando *character_expression* é um tipo de dados de caractere não Unicode.  
  
 Retorna **nvarchar** quando *character_expression* é um tipo de dados de caractere Unicode.  
  
## <a name="remarks"></a>Comentários  
 Ao usar agrupamentos SC, o *integer_expression* parâmetro contagens de um par de substituto UTF-16 como um caractere. Para obter mais informações, consulte [Suporte a agrupamentos e Unicode](../../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-left-with-a-column"></a>A. Usando LEFT com uma coluna  
 O exemplo a seguir retorna os cinco caracteres mais à esquerda do nome de cada produto na tabela `Product` do banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
SELECT LEFT(Name, 5)   
FROM Production.Product  
ORDER BY ProductID;  
GO  
```  
  
### <a name="b-using-left-with-a-character-string"></a>B. Usando LEFT com uma cadeia de caracteres  
 O exemplo a seguir usa `LEFT` para retornar os dois caracteres mais à esquerda da cadeia de caracteres `abcdefg`.  
  
```  
SELECT LEFT('abcdefg',2);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--   
ab   
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-left-with-a-column"></a>C. Usando LEFT com uma coluna  
 O exemplo a seguir retorna os cinco caracteres mais à esquerda do nome de cada produto.  
  
```  
-- Uses AdventureWorks  
  
SELECT LEFT(EnglishProductName, 5)   
FROM dbo.DimProduct  
ORDER BY ProductKey;  
```  
  
### <a name="d-using-left-with-a-character-string"></a>D. Usando LEFT com uma cadeia de caracteres  
 O exemplo a seguir usa `LEFT` para retornar os dois caracteres mais à esquerda da cadeia de caracteres `abcdefg`.  
  
```  
-- Uses AdventureWorks  
  
SELECT LEFT('abcdefg',2) FROM dbo.DimProduct;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--   
ab  
```  
  
## <a name="see-also"></a>Consulte também  
 [CAST e CONVERT &#40; Transact-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funções de cadeia de caracteres &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  


