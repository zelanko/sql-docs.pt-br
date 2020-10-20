---
description: Operadores compostos (Transact-SQL)
title: Operadores compostos (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- compound operators
- compound operators, described
ms.assetid: 5072fe91-02d3-42a7-831f-756eff714a17
author: rothja
ms.author: jroth
ms.openlocfilehash: f2daa8d7b168266ac56d1047eca2aa9408ebfe25
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196660"
---
# <a name="compound-operators-transact-sql"></a>Operadores compostos (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Os operadores compostos executam alguma operação e definem um valor original para o resultado da operação. Por exemplo, se uma variável @x é igual a 35, @x += 2 assume o valor original de @x, adiciona 2 e define @x com esse novo valor (37).  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] fornece os operadores compostos a seguir:  
  
|Operador|Link para mais informações|Ação|  
|--------------|------------------------------|------------|  
|+=|[+= &#40;Atribuição de adição&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/add-equals-transact-sql.md)|Adiciona alguma quantidade ao valor original e define o valor original como resultado.|  
|-=|[-= &#40;Subtract Assignment&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/subtract-equals-transact-sql.md)|Subtrai alguma quantidade do valor original e define o valor original como resultado.|  
|*=|[&#42;= &#40;Atribuição de multiplicação&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/multiply-equals-transact-sql.md)|Multiplica por uma quantidade e define o valor original para o resultado.|  
|/=|[&#40;Divide Assignment&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/divide-equals-transact-sql.md)|Divide por uma quantidade e define o valor original para o resultado.|  
|%=|[Atribuição de módulo &#40;Transact-SQL&#41;](../../t-sql/language-elements/modulo-equals-transact-sql.md)|Divide por uma quantidade e define o valor original para o módulo.|  
|&=|[&= &#40;Atribuição de AND bit a bit&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-and-equals-transact-sql.md)|Executa um AND bit a bit e define o valor original como o resultado.|  
|^=|[^= &#40;Atribuição de OR exclusivo bit a bit&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-exclusive-or-equals-transact-sql.md)|Executa um OR bit a bit exclusivo e define o valor original como o resultado.|  
|&#124;=|[&#124;= &#40;Atribuição de OR bit a bit&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-or-equals-transact-sql.md)|Executa um OR bit a bit e define o valor original como o resultado.|  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
expression operator expression  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *expressão*  
 É qualquer [expression](../../t-sql/language-elements/expressions-transact-sql.md) válida de um dos tipos de dados da categoria numérica.  
  
## <a name="result-types"></a>Tipos de resultado  
 Retorna o tipo de dados do argumento com a precedência mais alta. Para obter mais informações, veja [Precedência de tipo de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações, consulte os tópicos relacionados com cada operador.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir demonstram operações compostas.  
  
```sql  
DECLARE @x1 INT = 27;  
SET @x1 += 2 ;  
SELECT @x1 AS Added_2;  
  
DECLARE @x2 INT = 27;  
SET @x2 -= 2 ;  
SELECT @x2 AS Subtracted_2;  
  
DECLARE @x3 INT = 27;  
SET @x3 *= 2 ;  
SELECT @x3 AS Multiplied_by_2;  
  
DECLARE @x4 INT = 27;  
SET @x4 /= 2 ;  
SELECT @x4 AS Divided_by_2;  
  
DECLARE @x5 INT = 27;  
SET @x5 %= 2 ;  
SELECT @x5 AS Modulo_of_27_divided_by_2;  
  
DECLARE @x6 INT = 9;  
SET @x6 &= 13 ;  
SELECT @x6 AS Bitwise_AND;  
  
DECLARE @x7 INT = 27;  
SET @x7 ^= 2 ;  
SELECT @x7 AS Bitwise_Exclusive_OR;  
  
DECLARE @x8 INT = 27;  
SET @x8 |= 2 ;  
SELECT @x8 AS Bitwise_OR;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Operadores bit a bit &#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)  
  
  
