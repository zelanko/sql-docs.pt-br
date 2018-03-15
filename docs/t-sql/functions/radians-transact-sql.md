---
title: RADIANS (Transact-SQL) | Microsoft Docs
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
- RADIANS
- RADIANS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- RADIANS function
ms.assetid: e9f69951-ecda-45d9-8909-dcb716b1b1c0
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c36e42ad7cb28ae752809015fc90541d7530a807
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="radians-transact-sql"></a>RADIANS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna radianos quando uma expressão numérica, em graus, é inserida.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
RADIANS ( numeric_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 É uma [expression](../../t-sql/language-elements/expressions-transact-sql.md) da categoria de tipo de dados numéricos exatos ou aproximados, com exceção do tipo de dados **bit**.  
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna o mesmo tipo que *numeric_expression*.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-radians-to-show-00"></a>A. Usando RADIANS para mostrar 0,0  
 O exemplo a seguir retorna um resultado de `0.0` porque a expressão numérica a ser convertida em radianos é muito pequena para a função `RADIANS`.  
  
```  
SELECT RADIANS(1e-307)  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-------------------   
0.0                        
(1 row(s) affected)  
```  
  
### <a name="b-using-radians-to-return-the-equivalent-angle-of-a-float-expression"></a>B. Usando RADIANS para retornar o ângulo equivalente de uma expressão flutuante.  
 O exemplo a seguir usa uma expressão `float` e retorna os `RADIANS` do ângulo especificado.  
  
```  
-- First value is -45.01.  
DECLARE @angle float  
SET @angle = -45.01  
SELECT 'The RADIANS of the angle is: ' +  
   CONVERT(varchar, RADIANS(@angle))  
GO  
-- Next value is -181.01.  
DECLARE @angle float  
SET @angle = -181.01  
SELECT 'The RADIANS of the angle is: ' +  
   CONVERT(varchar, RADIANS(@angle))  
GO  
-- Next value is 0.00.  
DECLARE @angle float  
SET @angle = 0.00  
SELECT 'The RADIANS of the angle is: ' +  
   CONVERT(varchar, RADIANS(@angle))  
GO  
-- Next value is 0.1472738.  
DECLARE @angle float  
SET @angle = 0.1472738  
SELECT 'The RADIANS of the angle is: ' +  
    CONVERT(varchar, RADIANS(@angle))  
GO  
-- Last value is 197.1099392.  
DECLARE @angle float  
SET @angle = 197.1099392  
SELECT 'The RADIANS of the angle is: ' +  
   CONVERT(varchar, RADIANS(@angle))  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
---------------------------------------   
The RADIANS of the angle is: -0.785573                        
(1 row(s) affected)  
---------------------------------------   
The RADIANS of the angle is: -3.15922                         
(1 row(s) affected)  
---------------------------------------   
The RADIANS of the angle is: 0                                
(1 row(s) affected)  
---------------------------------------   
The RADIANS of the angle is: 0.00257041                       
 (1 row(s) affected)  
---------------------------------------   
The RADIANS of the angle is: 3.44022                          
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [decimal e numeric &#40;Transact-SQL&#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)   
 [float e real &#40;Transact-SQL&#41;](../../t-sql/data-types/float-and-real-transact-sql.md)   
 [int, bigint, smallint e tinyint &#40;Transact-SQL&#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)   
 [Funções matemáticas &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)   
 [money e smallmoney &#40;Transact-SQL&#41;](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)  
  
  

