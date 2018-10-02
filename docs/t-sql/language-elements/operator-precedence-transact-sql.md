---
title: Precedência do operador (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- operators [Transact-SQL], precedence
- operator precedence [Transact-SQL]
- order of operator execution [Transact-SQL]
- precedence [SQL Server], operators
ms.assetid: f04d2439-6fff-4e4c-801f-cc62faef510a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b4eb0d7865b71ba29ec00895e64574c0a188b3bc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47795594"
---
# <a name="operator-precedence-transact-sql"></a>Precedência dos operadores (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Quando uma expressão complexa tiver vários operadores, A precedência de operador determina a sequência na qual as operações são executadas. A ordem de execução pode afetar o valor resultante significativamente.  
  
 Os níveis de precedência dos operadores são mostrados na tabela a seguir. Um operador em níveis superiores é avaliado antes de um operador em um nível inferior.  
  
|Nível|Operadores|  
|-----------|---------------|  
|1|~ (Não de bit a bit)|  
|2|* (Multiplicação), / (Divisão), % (Módulo)|  
|3|+ (Positivo), – (Negativo), + (Adição), + (Concatenação), – (Subtração), & (AND bit a bit), ^ (OR exclusivo bit a bit) e &#124; (OR bit a bit)|  
|4|=, >, \<, >=, <=, <>, !=, !>, !< (Operadores de comparação)|  
|5|NOT|  
|6|AND|  
|7|ALL, ANY, BETWEEN, IN, LIKE, OR, SOME|  
|8|= (Atribuição)|  
  
 Quando dois operadores em uma expressão tiverem o mesmo nível de precedência de operador, eles serão avaliados da esquerda para a direita em sua posição na expressão. Por exemplo, na expressão usada na seguinte instrução `SET`, o operador de subtração é avaliado antes do operador de adição.  
  
```sql  
DECLARE @MyNumber int;  
SET @MyNumber = 4 - 2 + 27;  
-- Evaluates to 2 + 27 which yields an expression result of 29.  
SELECT @MyNumber;  
```  
  
 Use parênteses para substituir a precedência definida dos operadores em uma expressão. Tudo que estiver entre parênteses é avaliado primeiro para gerar um único valor antes daquele que poderá ser usado por qualquer operador fora dos parênteses.  
  
 Por exemplo, na expressão usada na seguinte instrução `SET`, o operador de multiplicação tem uma precedência maior que o operador de adição. Portanto, ele é avaliado primeiro; o resultado da expressão é `13`.  
  
```sql  
DECLARE @MyNumber int;  
SET @MyNumber = 2 * 4 + 5;  
-- Evaluates to 8 + 5 which yields an expression result of 13.  
SELECT @MyNumber;  
```  
  
 Na expressão usada na seguinte instrução `SET`, os parênteses fazem com que a adição seja executada primeiro. O resultado da expressão é `18`.  
  
```sql  
DECLARE @MyNumber int;  
SET @MyNumber = 2 * (4 + 5);  
-- Evaluates to 2 * 9 which yields an expression result of 18.  
SELECT @MyNumber;  
```  
  
 Se uma expressão tiver parênteses aninhados, a expressão mais aninhada será avaliada primeiro. O exemplo a seguir contém parênteses aninhados, com a expressão `5 - 3` no conjunto de parênteses mais aninhado. Essa expressão gera um valor de `2`. Em seguida, o operador de adição (`+`) adiciona esse resultado a `4`. Isso gera um valor de `6`. Finalmente, os `6` são multiplicados por `2` para gerar um resultado de expressão de `12`.  
  
```sql  
DECLARE @MyNumber int;  
SET @MyNumber = 2 * (4 + (5 - 3) );  
-- Evaluates to 2 * (4 + 2) which then evaluates to 2 * 6, and   
-- yields an expression result of 12.  
SELECT @MyNumber;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Operadores lógicos &#40;Transact-SQL&#41;](../../t-sql/language-elements/logical-operators-transact-sql.md)   
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Funções internas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
  
  
