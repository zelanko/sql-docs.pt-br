---
title: ASIN (Transact-SQL) | Microsoft Docs
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
- ASIN_TSQL
- ASIN
dev_langs:
- TSQL
helpviewer_keywords:
- ASIN function
- sine
- arcsine
ms.assetid: 6256dd7d-83d5-486e-a933-1d59afc7e417
caps.latest.revision: 35
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1ddfa04e926b4fd0e99455ea91774c31d34b0601
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="asin-transact-sql"></a>ASIN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Retorna o ângulo em radianos, cujo seno é especificado **float** expressão. Isso também é chamado de arco seno.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
ASIN ( float_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
*float_expression*  
É um [expressão](../../t-sql/language-elements/expressions-transact-sql.md) do tipo **float** ou de um tipo que pode ser convertido implicitamente em float, com um valor de -1 a 1. Valores fora deste intervalo retornam NULL e relatam um erro de domínio.
  
## <a name="return-types"></a>Tipos de retorno
**float**
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir usa uma **float** expressão e retorna o ASIN do ângulo especificado.
  
```sql
/* The first value will be -1.01. This fails because the value is   
outside the range.*/  
DECLARE @angle float  
SET @angle = -1.01  
SELECT 'The ASIN of the angle is: ' + CONVERT(varchar, ASIN(@angle))  
GO  
  
-- The next value is -1.00.  
DECLARE @angle float  
SET @angle = -1.00  
SELECT 'The ASIN of the angle is: ' + CONVERT(varchar, ASIN(@angle))  
GO  
  
-- The next value is 0.1472738.  
DECLARE @angle float  
SET @angle = 0.1472738  
SELECT 'The ASIN of the angle is: ' + CONVERT(varchar, ASIN(@angle))  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
-------------------------  
.Net SqlClient Data Provider: Msg 3622, Level 16, State 1, Line 3  
A domain error occurred.  
  
---------------------------------   
The ASIN of the angle is: -1.5708                          
  
(1 row(s) affected)  
  
----------------------------------   
The ASIN of the angle is: 0.147811                         
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
O exemplo a seguir retorna o arco seno de 1,00.
  
```sql
SELECT ASIN(1.00) AS asinCalc;  
```  
  
O exemplo a seguir retorna um erro, pois ele solicita o arco seno de um valor fora do intervalo permitido.
  
```sql
SELECT ASIN(1.1472738) AS asinCalc;  
```  
  
## <a name="see-also"></a>Consulte também
[Teto & #40; Transact-SQL & #41;](../../t-sql/functions/ceiling-transact-sql.md)  
[Funções matemáticas & #40; Transact-SQL & #41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
[Definir ARITHIGNORE & #40; Transact-SQL & #41;](../../t-sql/statements/set-arithignore-transact-sql.md)  
[SET ARITHABORT & #40; Transact-SQL & #41;](../../t-sql/statements/set-arithabort-transact-sql.md)
  
  


