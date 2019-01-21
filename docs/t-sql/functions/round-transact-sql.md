---
title: ROUND (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 002b2036c1d0c78d67b3278cd3932338ba4f4c9d
ms.sourcegitcommit: 96032813f6bf1cba680b5e46d82ae1f0f2da3d11
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/15/2019
ms.locfileid: "54299626"
---
# <a name="round-transact-sql"></a>ROUND (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

> [!div class="nextstepaction"]
> [Compartilhe seus comentários sobre o Sumário do SQL Docs!](https://aka.ms/sqldocsurvey)

Retorna um valor numérico, arredondado, para o comprimento ou precisão especificados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ROUND ( numeric_expression , length [ ,function ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 É uma [expression](../../t-sql/language-elements/expressions-transact-sql.md) da categoria de tipo de dados numéricos exatos ou aproximados, com exceção do tipo de dados **bit**.  
  
 *length*  
 É a precisão para a qual *numeric_expression* deve ser arredondada. *length* deve ser uma expressão do tipo **tinyint**, **smallint** ou **int**. Quando *length* é um número positivo, *numeric_expression* é arredondado para o número de posições decimais especificado por *length*. Quando *length* é um número negativo, *numeric_expression* é arredondado à esquerda da vírgula decimal, conforme especificado por *length*.  
  
 *função*  
 É o tipo de operação a ser executada. *function* deve ser **tinyint**, **smallint** ou **int**. Quando *function* é omitido ou tem um valor igual a 0 (padrão), *numeric_expression* é arredondado. Quando um valor diferente de 0 é especificado, *numeric_expression* é truncado.  
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna os tipos de dados a seguir.  
  
|Resultado da expressão|Tipo de retorno|  
|-----------------------|-----------------|  
|**tinyint**|**int**|  
|**smallint**|**int**|  
|**int**|**int**|  
|**bigint**|**bigint**|  
|Categorias **decimal** e **numeric** (p, s)|**decimal(p, s)**|  
|Categorias **money** e **smallmoney**|**money**|  
|Categorias **float** e **real**|**float**|  
  
## <a name="remarks"></a>Remarks  
 ROUND sempre retorna um valor. Se *length* for negativo e maior que o número de dígitos antes do ponto decimal, ROUND retornará 0.  
  
|Exemplo|Resultado|  
|-------------|------------|  
|ROUND(748.58, -4)|0|  
  
 ROUND retornará uma *numeric_expression* arredondada, seja qual for o tipo de dados, quando *length* for um número negativo.  
  
|Exemplos|Resultado|  
|--------------|------------|  
|ROUND(748.58, -1)|750.00|  
|ROUND(748.58, -2)|700.00|  
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
  
### <a name="b-using-round-and-rounding-approximations"></a>b. Usando ROUND e arredondando aproximações  
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
  
## <a name="see-also"></a>Consulte Também  
 [CEILING &#40;Transact-SQL&#41;](../../t-sql/functions/ceiling-transact-sql.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [FLOOR &#40;Transact-SQL&#41;](../../t-sql/functions/floor-transact-sql.md)   
 [Funções matemáticas &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)
