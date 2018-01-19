---
title: "+ (Mais unário) (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server (starting with 2008)
f1_keywords:
- + (positive)
- +
- positive
dev_langs: TSQL
helpviewer_keywords:
- + (positive operator)
- positive operator (+)
- positive values [SQL Server]
ms.assetid: 0f31c5cc-3078-4f6a-9870-7eb1a98053fb
caps.latest.revision: "33"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5759d9764789bff24f6512058b95d0e6f83db91f
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="unary-operators---positive"></a>Operadores unários - positivo
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna o valor de uma expressão numérica (um operador unário). Os operadores unários desempenham uma operação em apenas uma expressão de qualquer um dos tipos de dados da categoria de tipo de dados numéricos.   
  
|Operador|Significado|  
|--------------|-------------|  
|[+ (Positivo)](../../t-sql/language-elements/unary-operators-positive.md)|Valor numérico é positivo.|  
|[- (Negativo)](../../t-sql/language-elements/unary-operators-negative.md)|Valor numérico é negativo.|  
|[~ (NÃO bit a bit)](../../t-sql/language-elements/bitwise-not-transact-sql.md)|Retorna os complementos do número.|  
  
 Os operadores + (Positivo) e – (Negativo) podem ser usados em qualquer expressão de qualquer um dos tipos de dados da categoria de tipo de dados numérico. O operador ~ (NOT bit a bit) pode ser usado somente nas expressões de qualquer um dos tipos de dados da categoria de tipo de dados inteiros.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
+ numeric_expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 É qualquer [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de qualquer um dos dados de tipos na categoria de tipo de dados numéricos, exceto o **datetime** e **smalldatetime** tipos de dados.  
  
## <a name="result-types"></a>Tipos de resultado  
 Retorna o tipo de dados de *numeric_expression*.  
  
## <a name="remarks"></a>Remarks  
 Embora uma adição unária possa aparecer antes de qualquer expressão numérica, nenhuma operação é executada no valor retornado da expressão. Especificamente, não retornará o valor positivo de uma expressão negativa. Para retornar o valor positivo de uma expressão negativa, use o [ABS](../../t-sql/functions/abs-transact-sql.md) função.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-setting-a-variable-to-a-positive-value"></a>A. Definindo uma variável como um valor positivo  
 O exemplo a seguir define uma variável como um valor positivo.  
  
```  
DECLARE @MyNumber decimal(10,2);  
SET @MyNumber = +123.45;  
SELECT @MyNumber;  
GO  
```  
  
 Este é o conjunto de resultados:  
  
```  
-----------   
123.45            
  
(1 row(s) affected)  
```  
  
### <a name="b-using-the-unary-plus-operator-with-a-negative-value"></a>B. Usando o operador de adição unária com um valor negativo  
 O exemplo a seguir mostra o uso da adição unária com uma expressão negativa e da função ABS() na mesma expressão negativa. A adição unária não afeta a expressão, mas a função ABS retorna o valor positivo da expressão.  
  
```  
USE tempdb;  
GO  
DECLARE @Num1 int;  
SET @Num1 = -5;  
SELECT +@Num1, ABS(@Num1);  
GO  
```  
  
 Este é o conjunto de resultados:  
  
```  
----------- -----------  
-5          5  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Expressions &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Operators &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [ABS &#40;Transact-SQL&#41;](../../t-sql/functions/abs-transact-sql.md)  
  
  
