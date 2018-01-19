---
title: "+ = (Concatenação de cadeia de caracteres e atribuição) (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 12/07/2016
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
- concatenate strings
- string concatenation
- += (concatenate operator)
ms.assetid: 4aaeaab7-9b2b-48e0-8487-04ed672ebcb1
caps.latest.revision: "15"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 70f37ef6816f5288c1d50240bf813a20ff33fae7
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="-string-concatenation-assignment-transact-sql"></a>+= (String Concatenation Assignment) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Concatena duas cadeias de caracteres e define a cadeia de caracteres como o resultado da operação. Por exemplo, se uma variável @x é igual a 'Adventure', em seguida, @x + = 'Works' assumirá o valor original de @x, adiciona 'Works' à cadeia de caracteres e define @x para esse novo valor 'AdventureWorks'.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
expression += expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 É qualquer [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de qualquer um dos tipos de dados de caracteres.  
  
## <a name="result-types"></a>Tipos de resultado  
 Retorna o tipo de dados definido para a variável.  
  
## <a name="remarks"></a>Remarks  
 DEFINIR @v1 + = 'expression' é equivalente ao conjunto @v1 = @v1 + ('expression'). Além disso, defina @v1 = @v2 + @v3 + @v4 é equivalente ao conjunto @v1 = (@v2 + @v3) + @v4.  
  
 O operador + = não pode ser usado sem uma variável. Por exemplo, o código a seguir provoca um erro:  
  
```  
SELECT 'Adventure' += 'Works'  
```  
  
## <a name="examples"></a>Exemplos  
### <a name="a-concatenation-using--operator"></a>A. Concatenação usando o operador + =
 O exemplo a seguir concatena o uso do operador `+=`.  
  
```  
DECLARE @v1 varchar(40);  
SET @v1 = 'This is the original.';  
SET @v1 += ' More text.';  
PRINT @v1;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `This is the original. More text.`  
  
### <a name="b-order-of-evaluation-while-concatenating-using--operator"></a>B. Ordem de avaliação ao concatenar usando o operador + =
O exemplo a seguir concatena várias cadeias de caracteres para formar uma cadeia de caracteres longa e, em seguida, tenta calcular o comprimento da cadeia de caracteres final. Este exemplo demonstra as regras de truncamento e a ordem de avaliação, ao usar o operador de concatenação. 

```
DECLARE @x varchar(4000) = replicate('x', 4000)
DECLARE @z varchar(8000) = replicate('z',8000)
DECLARE @y varchar(max);
 
SET @y = '';
SET @y += @x + @z;
SELECT LEN(@y) AS Y; -- 8000
 
SET @y = '';
SET @y = @y + @x + @z;
SELECT LEN(@y) AS Y; -- 12000
 
SET @y = '';
SET @y = @y +(@x + @z);
SELECT LEN(@y) AS Y; -- 8000
-- or
SET @y = '';
SET @y = @x + @z + @y;
SELECT LEN(@y) AS Y; -- 8000
GO
```
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Y       
 ------- 
 8000 
  
 (1 row(s) affected) 
  
    
 Y       
 ------- 
 12000 
  
 (1 row(s) affected) 

 Y       
 ------- 
 8000 
  
 (1 row(s) affected) 
  
 Y       
 ------- 
 8000 
  
 (1 row(s) affected)
  ```   
   
## <a name="see-also"></a>Consulte também  
 [Operators &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [+= &#40;Add Assignment&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/add-equals-transact-sql.md)   
 [+ &#40;String Concatenation&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/string-concatenation-transact-sql.md)  
  
  
