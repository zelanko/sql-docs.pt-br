---
title: SOME | ANY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SOME
- SOME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- scalar values
- comparing scalar with single-column set
- ANY operator
- SOME | ANY keyword
- single-column set of values [SQL Server]
ms.assetid: 1f717ad6-f67b-4980-9397-577ecb0e5789
author: rothja
ms.author: jroth
ms.openlocfilehash: 561f6a893803aba1e545356b05de9a5e86088476
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85706149"
---
# <a name="some--any-transact-sql"></a>SOME | ANY (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Compara um valor escalar com um conjunto de valores de uma única coluna. SOME e ANY são equivalentes.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
  
scalar_expression { = | < > | ! = | > | > = | ! > | < | < = | ! < }   
     { SOME | ANY } ( subquery )   
```  
  
## <a name="arguments"></a>Argumentos  
 *scalar_expression*  
 É qualquer [expressão](../../t-sql/language-elements/expressions-transact-sql.md) válida.  
  
 { = | <> | != | > | >= | !> | < | <= | !< }  
 É qualquer operador de comparação válido.  
  
 SOME | ANY  
 Especifica que uma comparação deve ser feita.  
  
 *subquery*  
 É uma subconsulta que tem um conjunto de resultados de uma coluna. O tipo de dados da coluna retornada deve ser o mesmo da *scalar_expression*.  
  
## <a name="result-types"></a>Tipos de resultado  
 **Booliano**  
  
## <a name="result-value"></a>Valor do resultado  
 SOME ou ANY retornará **TRUE** quando a comparação especificada for TRUE para todos os pares (_scalar_expression_ **,** _x_) e quando *x* for um valor no conjunto de uma única coluna, caso contrário retornará **FALSE**.  
  
## <a name="remarks"></a>Comentários  
 SOME exige que a *scalar_expression* seja comparada positivamente com, pelo menos, um valor retornado pela subconsulta. Para obter instruções que exigem que *scalar_expression* seja comparada positivamente com todo valor retornado pela subconsulta, consulte [ALL &#40;Transact-SQL&#41;](../../t-sql/language-elements/all-transact-sql.md). Por exemplo, se a subconsulta retornar os valores 2 e 3, *scalar_expression* = SOME (subconsulta) será avaliada como TRUE para um *scalar_express* igual a 2. Se a consulta aninhada retornar os valores 2 e 3, *scalar_expression* = ALL (consulta aninhada) será avaliada como FALSE, porque alguns dos valores da consulta aninhada (o valor 3) não atenderão aos critérios da expressão.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-running-a-simple-example"></a>a. Executando um exemplo simples  
 As instruções a seguir criam uma tabela simples e adicionam os valores `1`, `2`, `3` e `4` à coluna `ID`.  
  
```  
CREATE TABLE T1  
(ID int) ;  
GO  
INSERT T1 VALUES (1) ;  
INSERT T1 VALUES (2) ;  
INSERT T1 VALUES (3) ;  
INSERT T1 VALUES (4) ;  
```  
  
 A consulta a seguir retorna `TRUE` porque `3` é menor do que alguns dos valores da tabela.  
  
```  
IF 3 < SOME (SELECT ID FROM T1)  
PRINT 'TRUE'   
ELSE  
PRINT 'FALSE' ;  
```  
  
 A consulta a seguir retorna `FALSE` porque `3` não é menor do que todos os valores da tabela.  
  
```  
IF 3 < ALL (SELECT ID FROM T1)  
PRINT 'TRUE'   
ELSE  
PRINT 'FALSE' ;  
```  
  
### <a name="b-running-a-practical-example"></a>B. Executando um exemplo prático  
 O exemplo a seguir cria um procedimento armazenado que determina se todos os componentes de um `SalesOrderID` especificado no banco de dados `AdventureWorks2012` podem ser fabricados no número de dias especificado. O exemplo usa uma subconsulta para criar uma lista do número do valor de `DaysToManufacture` para todos os componentes do `SalesOrderID` específico e, em seguida, testa se algum dos valores retornados pela subconsulta é maior que o número de dias especificado. Se todo valor de `DaysToManufacture` retornado for menor que o número fornecido, a condição será TRUE e a primeira mensagem será impressa.  
  
```  
-- Uses AdventureWorks  
  
CREATE PROCEDURE ManyDaysToComplete @OrderID int, @NumberOfDays int  
AS  
IF   
@NumberOfDays < SOME  
   (  
    SELECT DaysToManufacture  
    FROM Sales.SalesOrderDetail  
    JOIN Production.Product   
    ON Sales.SalesOrderDetail.ProductID = Production.Product.ProductID   
    WHERE SalesOrderID = @OrderID  
   )  
PRINT 'At least one item for this order can't be manufactured in specified number of days.'  
ELSE   
PRINT 'All items for this order can be manufactured in the specified number of days or less.' ;  
  
```  
  
 Para testar o procedimento, execute-o usando o `SalesOrderID``49080`, que tem um componente que exige `2` dias e dois componentes que exigem 0 dia. A primeira instrução atende aos critérios. A segunda consulta não.  
  
```  
EXECUTE ManyDaysToComplete 49080, 2 ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `All items for this order can be manufactured in the specified number of days or less.`  
  
```  
EXECUTE ManyDaysToComplete 49080, 1 ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `At least one item for this order can't be manufactured in specified number of days.`  
  
## <a name="see-also"></a>Consulte Também  
 [ALL &#40;Transact-SQL&#41;](../../t-sql/language-elements/all-transact-sql.md)   
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [Funções internas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [IN &#40;Transact-SQL&#41;](../../t-sql/language-elements/in-transact-sql.md)  
  
