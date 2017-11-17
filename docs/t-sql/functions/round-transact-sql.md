---
title: ROUND (Transact-SQL) | Microsoft Docs
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
- ROUND_TSQL
- ROUND
dev_langs:
- TSQL
helpviewer_keywords:
- rounding expressions
- ROUND function [Transact-SQL]
ms.assetid: 23921ed6-dd6a-4c9e-8c32-91c0d44fe4b7
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: cba8b5a9b62a21fc810ff9bb5fcd3d0c6429f9f5
ms.contentlocale: pt-br
ms.lasthandoff: 10/17/2017

---
# <a name="round-transact-sql"></a>ROUND (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna um valor numérico, arredondado, para o comprimento ou precisão especificados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
ROUND ( numeric_expression , length [ ,function ] )  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ROUND (numeric_expression , length )  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 É um [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de exato dados numéricos aproximados ou categoria de tipo, exceto para o **bit** tipo de dados.  
  
 *length*  
 É a precisão para o qual *numeric_expression* deve ser arredondada. *comprimento* deve ser uma expressão de tipo **tinyint**, **smallint**, ou **int**. Quando *comprimento* é um número positivo, *numeric_expression* é arredondado para o número de posições decimais especificado por *comprimento*. Quando *comprimento* é um número negativo, *numeric_expression* será arredondado à esquerda da vírgula decimal, conforme especificado por *comprimento*.  
  
 *função*  
 É o tipo de operação a ser executada. *função* devem ser **tinyint**, **smallint**, ou **int**. Quando *função* for omitido ou tem um valor de 0 (padrão), *numeric_expression* é arredondado. Quando um valor diferente de 0 for especificado, *numeric_expression* será truncado.  
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna os tipos de dados a seguir.  
  
|Resultado da expressão|Tipo de retorno|  
|-----------------------|-----------------|  
|**tinyint**|**int**|  
|**smallint**|**int**|  
|**int**|**int**|  
|**bigint**|**bigint**|  
|**decimal** e **numérico** categoria (p, s)|**decimal (p, s)**|  
|**Money** e **smallmoney** categoria|**money**|  
|**float** e **real** categoria|**float**|  
  
## <a name="remarks"></a>Comentários  
 ROUND sempre retorna um valor. Se *comprimento* é negativo e maior que o número de dígitos antes do ponto decimal, ROUND retorna 0.  
  
|Exemplo|Resultado|  
|-------------|------------|  
|ROUND (748.58, -4)|0|  
  
 ROUND retornará um arredondado *numeric_expression*, independentemente do tipo de dados, quando *comprimento* for um número negativo.  
  
|Exemplos|Resultado|  
|--------------|------------|  
|ROUND (748.58, -1)|750.00|  
|ROUND (748.58, -2)|700.00|  
|ROUND(748.58, -3)|Os resultados em um estouro aritmético porque o valor padrão de 748.58 é o decimal(5,2), que não pode retornar 1000.00.|  
|Para arredondar até 4 dígitos, altere o tipo de dados da entrada. Por exemplo:<br /><br /> `SELECT ROUND(CAST (748.58 AS decimal (6,2)),-3);`|1000.00|  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-round-and-estimates"></a>A. Usando ROUND e estimativas  
 O exemplo a seguir apresenta duas expressões que, usando `ROUND`, demonstram que o último dígito sempre é uma estimativa.  
  
```  
SELECT ROUND(123.9994, 3), ROUND(123.9995, 3);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------- -----------  
123.9990    124.0000      
```  
  
### <a name="b-using-round-and-rounding-approximations"></a>B. Usando ROUND e arredondando aproximações  
 O exemplo a seguir mostra arredondamentos e aproximações.  
  
```  
SELECT ROUND(123.4545, 2), ROUND(123.45, -2);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

 ```
--------  ----------
123.45    100.00
```
  
### <a name="c-using-round-to-truncate"></a>C. Usando ROUND para truncar  
 O exemplo a seguir usa duas instruções `SELECT` para demonstrar a diferença entre arredondamento e truncagem. A primeira instrução arredonda o resultado. A segunda instrução trunca o resultado.  
  
```  
SELECT ROUND(150.75, 0);  
GO  
SELECT ROUND(150.75, 0, 1);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--------  
151.00  
  
(1 row(s) affected)  
  
--------  
150.00  
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-round-and-estimates"></a>D. Usando ROUND e estimativas  
 O exemplo a seguir apresenta duas expressões que, usando `ROUND`, demonstram que o último dígito sempre é uma estimativa.  
  
```  
SELECT ROUND(123.994999, 3), ROUND(123.995444, 3);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

 ```
--------  ---------
123.995000    123.995444
```
  
## <a name="see-also"></a>Consulte também  
 [Teto &#40; Transact-SQL &#41;](../../t-sql/functions/ceiling-transact-sql.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Expressões &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [FLOOR &#40; Transact-SQL &#41;](../../t-sql/functions/floor-transact-sql.md)   
 [Funções matemáticas &#40; Transact-SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
  
  


