---
title: ALL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALL_TSQL
- ALL
dev_langs:
- TSQL
helpviewer_keywords:
- single-column set of values [SQL Server]
- ALL (Transact-SQL)
ms.assetid: 4b0c002e-1ffd-4425-a980-11fdc1f24af7
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6901a6eb93ad2374eaf6d613e9eada21dea3cc55
ms.sourcegitcommit: 5ed48c7dc6bed153079bc2b23a1e0506841310d1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65983230"
---
# <a name="all-transact-sql"></a>ALL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Compara um valor escalar com um conjunto de valores de uma única coluna.  
  
 ![Ícone de link do artigo](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do artigo") [Convenções de sintaxe do Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
scalar_expression { = | <> | != | > | >= | !> | < | <= | !< } ALL ( subquery )  
```  
  
## <a name="arguments"></a>Argumentos  
 *scalar_expression*  
 É qualquer [expressão](../../t-sql/language-elements/expressions-transact-sql.md) válida.  
  
 { = | <> | != | > | >= | !> | < | <= | !< }  
 É um operador de comparação.  
  
 *subquery*  
 É uma subconsulta que retorna um conjunto de resultados com uma coluna. O tipo de dados da coluna retornada precisa ser o mesmo tipo de dados que o da *scalar_expression*.  
  
 É uma instrução SELECT restrita, em que a cláusula ORDER BY e a palavra-chave INTO não são permitidas.  
  
## <a name="result-types"></a>Tipos de resultado  
 **Booliano**  
  
## <a name="result-value"></a>Valor do resultado  
 Retornará TRUE quando a comparação especificada for TRUE para todos os pares (_scalar_expression_ **,** _x)_ e quando *x* for um valor no conjunto de uma única coluna. Caso contrário, retornará FALSE.  
  
## <a name="remarks"></a>Remarks  
 ALL requer que a *scalar_expression* seja comparada positivamente com todos os valores retornados pela subconsulta. Por exemplo, se a subconsulta retornar os valores 2 e 3, *scalar_expression* <= ALL (a subconsulta) será avaliada como TRUE para uma *scalar_expression* igual a 2. Se a consulta aninhada retornar os valores 2 e 3, *scalar_expression* = ALL (consulta aninhada) será avaliada como FALSE, porque alguns dos valores da consulta aninhada (o valor 3) não atenderão aos critérios da expressão.  
  
 Para instruções que requerem que a *scalar_expression* seja comparada positivamente somente a um valor retornado pela subconsulta, confira [SOME &#124; ANY &#40;Transact-SQL&#41;](../../t-sql/language-elements/some-any-transact-sql.md).  
  
 Este artigo se refere a ALL quando usado com uma consulta aninhada. ALL também pode ser usado com [UNION](../../t-sql/language-elements/set-operators-union-transact-sql.md) e [SELECT](../../t-sql/queries/select-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria um procedimento armazenado que determina se todos os componentes de um `SalesOrderID` especificado no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] podem ser fabricados no número de dias especificado. O exemplo usa uma consulta aninhada para criar uma lista do número de valores de `DaysToManufacture` para todos os componentes do `SalesOrderID` específico e, em seguida, confirma se todos os `DaysToManufacture` estão dentro do número de dias especificado.  
  
```  
-- Uses AdventureWorks  
  
CREATE PROCEDURE DaysToBuild @OrderID int, @NumberOfDays int  
AS  
IF   
@NumberOfDays >= ALL  
   (  
    SELECT DaysToManufacture  
    FROM Sales.SalesOrderDetail  
    JOIN Production.Product   
    ON Sales.SalesOrderDetail.ProductID = Production.Product.ProductID   
    WHERE SalesOrderID = @OrderID  
   )  
PRINT 'All items for this order can be manufactured in specified number of days or less.'  
ELSE   
PRINT 'Some items for this order can''t be manufactured in specified number of days or less.' ;  
  
```  
  
 Para testar o procedimento, execute-o usando o `SalesOrderID 49080`, que tem um componente que requer `2` dias e dois componentes que requerem 0 dia. A primeira instrução a seguir corresponde aos critérios. A segunda consulta não.  
  
```  
EXECUTE DaysToBuild 49080, 2 ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `All items for this order can be manufactured in specified number of days or less.`  
  
```  
EXECUTE DaysToBuild 49080, 1 ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Some items for this order can't be manufactured in specified number of days or less.`  
  
## <a name="see-also"></a>Consulte Também  
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Funções internas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [IN &#40;Transact-SQL&#41;](../../t-sql/language-elements/in-transact-sql.md)  
  
