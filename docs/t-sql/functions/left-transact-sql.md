---
title: LEFT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a83289d8b97992ad27f31db130926e46e4871588
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37791117"
---
# <a name="left-transact-sql"></a>LEFT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna a parte da esquerda de uma cadeia de caracteres com o número de caracteres especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
LEFT ( character_expression , integer_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 É uma [expression](../../t-sql/language-elements/expressions-transact-sql.md) de dados binários ou de caracteres. *character_expression* pode ser uma constante, variável ou coluna. *character_expression* pode ser de qualquer tipo de dados, exceto **text** ou **ntext**, que pode ser convertido implicitamente em **varchar** ou **nvarchar** . Caso contrário, use a função [CAST](../../t-sql/functions/cast-and-convert-transact-sql.md) para converter explicitamente *character_expression*.  
  
 *integer_expression*  
 É um inteiro positivo que especifica quantos caracteres da *character_expression* serão retornados. Se *integer_expression* for negativa, um erro será retornado. Se *integer_expression* for do tipo **bigint** e contiver um valor grande, *character_expression* deverá ser de um tipo de dados grandes, como **varchar(max)**.  
  
 O parâmetro *integer_expression* conta um caractere alternativo de UTF-16 como um caractere.  
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna **varchar** quando *character_expression* é um tipo de dados de caractere não Unicode.  
  
 Retorna **nvarchar** quando *character_expression* é um tipo de dados de caractere Unicode.  
  
## <a name="remarks"></a>Remarks  
 Durante o uso de agrupamentos SC, o parâmetro *integer_expression* conta um par alternativo UTF-16 como um caractere. Para obter mais informações, consulte [Suporte a agrupamentos e Unicode](../../relational-databases/collations/collation-and-unicode-support.md).  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [LTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)  
 [RIGHT &#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)  
 [RTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)  
 [STRING_SPLIT &#40;Transact-SQL&#41;](../../t-sql/functions/string-split-transact-sql.md)  
 [SUBSTRING &#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)  
 [TRIM &#40;Transact-SQL&#41;](../../t-sql/functions/trim-transact-sql.md)  
 [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funções de cadeia de caracteres &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  

