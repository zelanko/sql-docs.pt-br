---
title: "Funções matemáticas (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 07/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- calculations [SQL Server]
- mathematical functions [SQL Server]
- functions [SQL Server], mathematical
ms.assetid: 46495a2e-81d0-4677-9d72-9db083cd1023
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5ec4a6767acab606d6459b439683a88a0cae1caf
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="mathematical-functions-transact-sql"></a>Funções matemáticas (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  As funções escalares a seguir executam um cálculo, normalmente com base em valores de entrada fornecidos como argumentos e retornam um valor numérico:  
  
||||  
|-|-|-|  
|[ABS](../../t-sql/functions/abs-transact-sql.md)|[GRAUS](../../t-sql/functions/degrees-transact-sql.md)|[RAND](../../t-sql/functions/rand-transact-sql.md)|  
|[ACOS](../../t-sql/functions/acos-transact-sql.md)|[EXP](../../t-sql/functions/exp-transact-sql.md)|[ARREDONDAR](../../t-sql/functions/round-transact-sql.md)|  
|[ASIN](../../t-sql/functions/asin-transact-sql.md)|[FLOOR](../../t-sql/functions/floor-transact-sql.md)|[LOGON](../../t-sql/functions/sign-transact-sql.md)|  
|[ATAN](../../t-sql/functions/atan-transact-sql.md)|[LOG](../../t-sql/functions/log-transact-sql.md)|[SIN](../../t-sql/functions/sin-transact-sql.md)|  
|[ATN2](../../t-sql/functions/atn2-transact-sql.md)|[LOG10](../../t-sql/functions/log10-transact-sql.md)|[SQRT](../../t-sql/functions/sqrt-transact-sql.md)|  
|[CEILING](../../t-sql/functions/ceiling-transact-sql.md)|[PI](../../t-sql/functions/pi-transact-sql.md)|[QUADRADO](../../t-sql/functions/square-transact-sql.md)|  
|[COS](../../t-sql/functions/cos-transact-sql.md)|[ENERGIA](../../t-sql/functions/power-transact-sql.md)|[TAN](../../t-sql/functions/tan-transact-sql.md)|  
|[COT](../../t-sql/functions/cot-transact-sql.md)|[RADIANOS](../../t-sql/functions/radians-transact-sql.md)||  
  
> [!NOTE]  
>  Funções aritméticas, como ABS, CEILING, DEGREES, FLOOR, POWER, RADIANS e SIGN, retornam um valor com o mesmo tipo de dados que o valor de entrada. Funções trigonométricas e outras, incluindo EXP, LOG, LOG10, SQUARE e SQRT, convertem seus valores para **float** e retornar um **float** valor.  
  
 Todas as funções matemáticas, com exceção de RAND, são funções deterministas. Isso significa que elas retornam os mesmos resultados sempre que são chamadas com um conjunto específico de valores de entrada. RAND só é determinista quando um parâmetro de propagação é especificado. Para obter mais informações sobre determinismo de função, consulte [determinísticas e funções não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="see-also"></a>Consulte também  
  [Operadores aritméticos &#40; Transact-SQL &#41;](../../t-sql/language-elements/arithmetic-operators-transact-sql.md)  
  [Funções internas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
  
  

