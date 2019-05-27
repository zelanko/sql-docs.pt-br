---
title: += (Concatenação de cadeia de caracteres e atribuição) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/07/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- concatenate strings
- string concatenation
- += (concatenate operator)
ms.assetid: 4aaeaab7-9b2b-48e0-8487-04ed672ebcb1
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 18cbb602155c6f3ca8230d6ad4b149979f3b51bc
ms.sourcegitcommit: 5ed48c7dc6bed153079bc2b23a1e0506841310d1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65981551"
---
# <a name="-string-concatenation-assignment-transact-sql"></a>+= (Atribuição de concatenação de cadeia de caracteres) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Concatena duas cadeias de caracteres e define a cadeia de caracteres como o resultado da operação. Por exemplo, se uma variável @x for igual a 'Adventure', @x + = 'Works' usará o valor original de @x, adicionará 'Works' à cadeia de caracteres, e definirá @x com o novo valor 'AdventureWorks'.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
expression += expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 É qualquer [expression](../../t-sql/language-elements/expressions-transact-sql.md) válida de um dos tipos de dados de caractere.  
  
## <a name="result-types"></a>Tipos de resultado  
 Retorna o tipo de dados definido para a variável.  
  
## <a name="remarks"></a>Remarks  
 SET @v1 += 'expression' é equivalente a SET @v1 = @v1 + ('expression'). Além disso, SET @v1 = @v2 + @v3 + @v4 é equivalente a SET @v1 = (@v2 + @v3) + @v4.  
  
 O operador + = não pode ser usado sem uma variável. Por exemplo, o código a seguir provoca um erro:  
  
```  
SELECT 'Adventure' += 'Works'  
```  
  
## <a name="examples"></a>Exemplos  
### <a name="a-concatenation-using--operator"></a>A. Concatenação com o operador +=
 O exemplo a seguir concatena o uso do operador `+=`.  
  
```  
DECLARE @v1 varchar(40);  
SET @v1 = 'This is the original.';  
SET @v1 += ' More text.';  
PRINT @v1;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `This is the original. More text.`  
  
### <a name="b-order-of-evaluation-while-concatenating-using--operator"></a>B. Ordem de avaliação ao concatenar com o operador +=
O exemplo a seguir concatena várias cadeias de caracteres para formar uma cadeia de caracteres longa e, em seguida, tenta calcular o tamanho da cadeia de caracteres final. Este exemplo demonstra as regras de truncamento e a ordem de avaliação, durante o uso do operador de concatenação. 

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
   
## <a name="see-also"></a>Consulte Também  
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [+= &#40;Atribuição de adição&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/add-equals-transact-sql.md)   
 [+ &#40;Concatenação de cadeias de caracteres&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/string-concatenation-transact-sql.md)  
  
  
