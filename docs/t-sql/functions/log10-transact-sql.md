---
title: LOG10 (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LOG10
- LOG10_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- float expressions
- LOG10 function
- base-10 logarithms
- logarithm of expression
ms.assetid: 1eb7fb34-1937-4a39-a936-f5c0c7c7e06f
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d8cc5b0ef6af319e55744a3ca373f0e6b11e230b
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="log10-transact-sql"></a>LOG10 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna o logaritmo de base 10 de especificado **float** expressão.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
LOG10 ( float_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *float_expression*  
 É um [expressão](../../t-sql/language-elements/expressions-transact-sql.md) do tipo **float** ou de um tipo que pode ser convertido implicitamente em **float**.  
  
## <a name="return-types"></a>Tipos de retorno  
 **float**  
  
## <a name="remarks"></a>Comentários  
 As funções LOG10 e POWER estão inversamente relacionadas uma à outra. Por exemplo, 10 ^ LOG10 (*n*) =  *n* .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-calculating-the-base-10-logarithm-for-a-variable"></a>A. Calculando um logaritmo na base 10 para uma variável.  
 O exemplo a seguir calcula o `LOG10` da variável especificada.  
  
```  
DECLARE @var float;  
SET @var = 145.175643;  
SELECT 'The LOG10 of the variable is: ' + CONVERT(varchar,LOG10(@var));  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
The LOG10 of the variable is: 2.16189      
  
(1 row(s) affected)  
```  
  
### <a name="b-calculating-the-result-of-raising-a-base-10-logarithm-to-a-specified-power"></a>B. Calculando o resultado da elevação de um logaritmo na base 10 a uma potência especificada.  
 O exemplo a seguir retorna o resultado da elevação de um logaritmo na base 10 a uma potência especificada.  
  
```  
SELECT POWER (10, LOG10(5));   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-----------  
5  
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-calculating-the-base-10-logarithm-for-a-value"></a>C: calculando o logaritmo de base 10 para um valor.  
 O exemplo a seguir calcula o `LOG10` do valor especificado.  
  
```  
SELECT LOG10(145.175642);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
-------------------  
2.16
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções matemáticas &#40; Transact-SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)   
 [ENERGIA &#40; Transact-SQL &#41;](../../t-sql/functions/power-transact-sql.md)   
 [LOG &#40; Transact-SQL &#41;](../../t-sql/functions/log-transact-sql.md)  
  
  


