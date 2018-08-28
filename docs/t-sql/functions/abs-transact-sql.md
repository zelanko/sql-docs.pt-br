---
title: ABS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 44
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 988e0121acc0e76f406c01ccd56c9a4f6c0953a2
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43110142"
---
# <a name="abs-transact-sql"></a>ABS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Uma função matemática que retorna o valor absoluto (positivo) da expressão numérica especificada. (`ABS` altera valores negativos para valores positivos. `ABS` não tem nenhum efeito em zero ou em valores positivos.)
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
ABS ( numeric_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
*numeric_expression*  
Uma expressão da categoria de tipo de dados numéricos exatos ou aproximados.
  
## <a name="return-types"></a>Tipos de retorno  
Retorna o mesmo tipo que *numeric_expression*.
  
## <a name="examples"></a>Exemplos  
Este exemplo mostra os resultados do uso da função `ABS` em três números diferentes.
  
```sql
SELECT ABS(-1.0), ABS(0.0), ABS(1.0);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
---- ---- ----  
1.0  .0   1.0  
```  
  
A função `ABS` pode produzir um erro de estouro quando o valor absoluto de um número excede o maior número que o tipo de dados especificado pode representar. Por exemplo, o tipo de dados `int` tem um intervalo de valor entre `-2,147,483,648` e `2,147,483,647`. O cálculo do valor absoluto para o inteiro com sinal `-2,147,483,648` causará um erro de estouro porque seu valor absoluto excede o limite positivo do intervalo do tipo de dados `int`.
  
```sql
DECLARE @i int;  
SET @i = -2147483648;  
SELECT ABS(@i);  
GO  
```  
  
Retorna essa mensagem de erro:
  
“Mensagem 8115, Nível 16, Estado 2, Linha 3"
  
"Erro de estouro aritmético ao converter a expressão em dados tipo int".

  
## <a name="see-also"></a>Confira também
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[Funções matemáticas &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
[Funções internas &#40;Transact-SQL&#41;](../../t-sql/functions/functions.md)
  
  

