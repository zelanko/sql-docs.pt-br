---
title: ENTRADA (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SIGN_TSQL
- SIGN
dev_langs:
- TSQL
helpviewer_keywords:
- '- (negative)'
- + (positive sign)
- zero (0)
- SIGN function
- positive values [SQL Server]
- 0 (zero)
- negative values
ms.assetid: c3a98b52-6fbe-4127-a5c9-8a4922e83e28
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5ec7a98db7e5fa31bebed31ba02758ebc4ec02a1
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="sign-transact-sql"></a>SIGN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna o sinal positivo (+1), zero (0) ou sinal negativo (-1) da expressão especificada.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SIGN ( numeric_expression )  
```  
  

## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 É um [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de exato dados numéricos aproximados ou categoria de tipo, exceto para o **bit** tipo de dados.  
  
## <a name="return-types"></a>Tipos de retorno  
  
|Expressão especificada|Tipo de retorno|  
|--------------------------|-----------------|  
|**bigint**|**bigint**|  
|**smallint/int/tinyint**|**int**|  
|**Money/smallmoney**|**money**|  
|**numérico/decimal**|**numérico/decimal**|  
|**Outros tipos**|**float**|  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna os valores SIGN de números de -1 a 1.  
  
```  
DECLARE @value real  
SET @value = -1  
WHILE @value < 2  
   BEGIN  
      SELECT SIGN(@value)  
      SET NOCOUNT ON  
      SELECT @value = @value + 1  
      SET NOCOUNT OFF  
   END  
SET NOCOUNT OFF  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
(1 row(s) affected)  
  
------------------------   
-1.0                       
  
(1 row(s) affected)  
  
------------------------   
0.0                        
  
(1 row(s) affected)  
  
------------------------   
1.0                        
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir retorna os valores de entrada de três números.  
  
```  
SELECT SIGN(-125), SIGN(0), SIGN(564);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
-----  -----  -----  
-1     0      1
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções matemáticas &#40; Transact-SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
  
  


