---
title: Operadores (Transact-SQL) composta | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server (starting with 2008)
dev_langs:
- TSQL
helpviewer_keywords:
- compound operators
- compound operators, described
ms.assetid: 5072fe91-02d3-42a7-831f-756eff714a17
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2e5fde8cd4265359722f33400d834b0a301718ef
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="compound-operators-transact-sql"></a>Operadores compostos (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Os operadores compostos executam alguma operação e definem um valor original para o resultado da operação. Por exemplo, se uma variável @x é igual a 35, então @x + = 2 assumirá o valor original de @x, adicionar 2 e conjuntos de @x para esse novo valor (37).  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] fornece os operadores compostos a seguir:  
  
|Operador|Link para mais informações|Ação|  
|--------------|------------------------------|------------|  
|+=|[+ = &#40; Adicionar EQUALS &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/add-equals-transact-sql.md)|Adiciona alguma quantidade ao valor original e define o valor original como resultado.|  
|-=|[-= &#40; Subtrair EQUALS &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/subtract-equals-transact-sql.md)|Subtrai alguma quantidade do valor original e define o valor original como resultado.|  
|*=|[&#42; = &#40; Multiplicar EQUALS &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/multiply-equals-transact-sql.md)|Multiplica por uma quantidade e define o valor original para o resultado.|  
|/=|[&#40; dividir EQUALS &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/divide-equals-transact-sql.md)|Divide por uma quantidade e define o valor original para o resultado.|  
|%=|[Módulo EQUALS &#40; Transact-SQL &#41;](../../t-sql/language-elements/modulo-equals-transact-sql.md)|Divide por uma quantidade e define o valor original para o módulo.|  
|&=|[& = &#40; AND bit a bit EQUALS &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/bitwise-and-equals-transact-sql.md)|Executa um AND bit a bit e define o valor original como o resultado.|  
|^=|[^ = &#40; Bit a bit exclusivo ou igual a &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/bitwise-exclusive-or-equals-transact-sql.md)|Executa um OR bit a bit exclusivo e define o valor original como o resultado.|  
|&#124;=|[&#124; = &#40; OR bit a bit é igual a &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/bitwise-or-equals-transact-sql.md)|Executa um OR bit a bit e define o valor original como o resultado.|  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
expression operator expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 É qualquer [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de qualquer um dos dados de tipos da categoria numérica.  
  
## <a name="result-types"></a>Tipos de resultado  
 Retorna o tipo de dados do argumento com a precedência mais alta. Para obter mais informações, veja [Precedência de tipo de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações, consulte os tópicos relacionados com cada operador.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir demonstram operações compostas.  
  
```  
DECLARE @x1 int = 27;  
SET @x1 += 2 ;  
SELECT @x1 AS Added_2;  
  
DECLARE @x2 int = 27;  
SET @x2 -= 2 ;  
SELECT @x2 AS Subtracted_2;  
  
DECLARE @x3 int = 27;  
SET @x3 *= 2 ;  
SELECT @x3 AS Multiplied_by_2;  
  
DECLARE @x4 int = 27;  
SET @x4 /= 2 ;  
SELECT @x4 AS Divided_by_2;  
  
DECLARE @x5 int = 27;  
SET @x5 %= 2 ;  
SELECT @x5 AS Modulo_of_27_divided_by_2;  
  
DECLARE @x6 int = 9;  
SET @x6 &= 13 ;  
SELECT @x6 AS Bitwise_AND;  
  
DECLARE @x7 int = 27;  
SET @x7 ^= 2 ;  
SELECT @x7 AS Bitwise_Exclusive_OR;  
  
DECLARE @x8 int = 27;  
SET @x8 |= 2 ;  
SELECT @x8 AS Bitwise_OR;  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Operadores bit a bit &#40; Transact-SQL &#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)  
  
  

