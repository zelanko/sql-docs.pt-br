---
title: COT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COT_TSQL
- COT
dev_langs:
- TSQL
helpviewer_keywords:
- COT function
- cotangent
ms.assetid: c87a9dac-e398-4125-80c3-7df3c2ce6b63
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 080b20e15242342e9662b5b4c459a9e8160822ab
ms.contentlocale: pt-br
ms.lasthandoff: 10/17/2017

---
# <a name="cot-transact-sql"></a>COT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Uma função matemática que retorna a cotangente trigonométrica do ângulo especificado, em radianos, especificado na **float** expressão.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
COT ( float_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
*float_expression*  
É um [expressão](../../t-sql/language-elements/expressions-transact-sql.md)do tipo **float** ou de um tipo que pode ser convertido implicitamente em **float**.
  
## <a name="return-types"></a>Tipos de retorno
**float**
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir retorna a COT do ângulo especificado.
  
```sql
DECLARE @angle float;  
SET @angle = 124.1332;  
SELECT 'The COT of the angle is: ' + CONVERT(varchar,COT(@angle));  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
The COT of the angle is: -0.040312                
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte também
[Funções matemáticas &#40; Transact-SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)
  
  


