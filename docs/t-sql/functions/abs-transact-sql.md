---
title: ABS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
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
- ABS_TSQL
- ABS
dev_langs:
- TSQL
helpviewer_keywords:
- values [SQL Server], positive
- values [SQL Server], absolute
- ABS function
- absolute positive value
ms.assetid: e2ea7a6d-3e2f-472c-afbc-437d3b835c03
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 9f96d651f179120fab6fabfb78d08cca84404bd1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="abs-transact-sql"></a>ABS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Uma função matemática que retorna o valor absoluto (positivo) da expressão numérica especificada. (`ABS` alterações negativo de valores para valores positivos. `ABS`não tem nenhum efeito em zero ou valores positivos.)
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
ABS ( numeric_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
*numeric_expression*  
É uma expressão da categoria de tipo de dados numéricos exatos ou aproximados.
  
## <a name="return-types"></a>Tipos de retorno  
Retorna o mesmo tipo que *numeric_expression*.
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir mostra os resultados do uso da função `ABS` em três números diferentes.
  
```sql
SELECT ABS(-1.0), ABS(0.0), ABS(1.0);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
---- ---- ----  
1.0  .0   1.0  
```  
  
A função `ABS` pode produzir um erro de estouro quando o valor absoluto de um número é maior que o maior número que pode ser representado pelo tipo de dados especificado. Por exemplo, o tipo de dados `int` só pode conter valores que variam de `-2,147,483,648` a `2,147,483,647`. Computar o valor absoluto para o inteiro assinado `-2,147,483,648` causa um erro de estouro porque seu valor absoluto é maior do que o intervalo positive para o tipo de dados `int`.
  
```sql
DECLARE @i int;  
SET @i = -2147483648;  
SELECT ABS(@i);  
GO  
```  
  
Esta é a mensagem de erro:
  
“Mensagem 8115, Nível 16, Estado 2, Linha 3"
  
"Erro de estouro aritmético ao converter a expressão em dados tipo int".

  
## <a name="see-also"></a>Consulte também
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[Funções matemáticas &#40; Transact-SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
[Funções internas &#40;Transact-SQL&#41;](../../t-sql/functions/functions.md)
  
  

