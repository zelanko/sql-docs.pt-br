---
title: SOME | ANY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server (starting with 2008)
f1_keywords:
- SOME
- SOME_TSQL
dev_langs: TSQL
helpviewer_keywords:
- scalar values
- comparing scalar with single-column set
- ANY operator
- SOME | ANY keyword
- single-column set of values [SQL Server]
ms.assetid: 1f717ad6-f67b-4980-9397-577ecb0e5789
caps.latest.revision: "41"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 0f99a9d507b74dfd12bbdaf273683f857ceec881
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="some--any-transact-sql"></a>SOME | ANY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Compara um valor escalar com um conjunto de valores de uma única coluna. SOME e ANY são equivalentes.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
scalar_expression { = | < > | ! = | > | > = | ! > | < | < = | ! < }   
     { SOME | ANY } ( subquery )   
```  
  
## <a name="arguments"></a>Argumentos  
 *scalar_expression*  
 É qualquer [expressão](../../t-sql/language-elements/expressions-transact-sql.md).  
  
 { = | <> | != | > | >= | !> | < | <= | !< }  
 É qualquer operador de comparação válido.  
  
 SOME | ANY  
 Especifica que uma comparação deve ser feita.  
  
 *subquery*  
 É uma subconsulta que tem um conjunto de resultados de uma coluna. O tipo de dados da coluna retornada deve ser o mesmo tipo de dados *scalar_expression*.  
  
## <a name="result-types"></a>Tipos de resultado  
 **Booliano**  
  
## <a name="result-value"></a>Valor do resultado  
 SOME ou ANY retornará **TRUE** quando a comparação especificada for TRUE para qualquer par (*scalar_expression***,***x*) onde *x* é um valor na conjunto de coluna única. Caso contrário, retornará **FALSE**.  
  
## <a name="remarks"></a>Remarks  
 SOME exige o *scalar_expression* seja comparada positivamente com pelo menos um valor retornado pela subconsulta. Para instruções que requerem o *scalar_expression* seja comparada positivamente a cada valor que é retornado pela subconsulta, consulte [todos os &#40; Transact-SQL &#41; ](../../t-sql/language-elements/all-transact-sql.md). Por exemplo, se a subconsulta retornar os valores 2 e 3, *scalar_expression* = algumas (a subconsulta) será avaliada como TRUE para um *scalar_express* de 2. Se a subconsulta retornar os valores 2 e 3, *scalar_expression* = ALL (a subconsulta) seria avaliada como FALSE, porque alguns dos valores da subconsulta (o valor de 3) não atende aos critérios da expressão.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-running-a-simple-example"></a>A. Executando um exemplo simples  
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
 O exemplo a seguir cria um procedimento armazenado que determina se todos os componentes de determinado `SalesOrderID` no `AdventureWorks2012` banco de dados pode ser fabricado no número especificado de dias. O exemplo usa uma subconsulta para criar uma lista do número do valor de `DaysToManufacture` para todos os componentes do `SalesOrderID` específico e, em seguida, testa se algum dos valores retornados pela subconsulta é maior que o número de dias especificado. Se todo valor de `DaysToManufacture` retornado for menor que o número fornecido, a condição será TRUE e a primeira mensagem será impressa.  
  
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
PRINT 'At least one item for this order cannot be manufactured in specified number of days.'  
ELSE   
PRINT 'All items for this order can be manufactured in the specified number of days or less.' ;  
  
```  
  
 Para testar o procedimento, execute o procedimento usando o `SalesOrderID``49080`, que tem um componente que requer `2` dias e dois componentes que requerem 0 dia. A primeira instrução atende aos critérios. A segunda consulta não.  
  
```  
EXECUTE ManyDaysToComplete 49080, 2 ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `All items for this order can be manufactured in the specified number of days or less.`  
  
```  
EXECUTE ManyDaysToComplete 49080, 1 ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `At least one item for this order cannot be manufactured in specified number of days.`  
  
## <a name="see-also"></a>Consulte também  
 [ALL &#40;Transact-SQL&#41;](../../t-sql/language-elements/all-transact-sql.md)   
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [Funções internas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operators &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [IN &#40;Transact-SQL&#41;](../../t-sql/language-elements/in-transact-sql.md)  
  
  
