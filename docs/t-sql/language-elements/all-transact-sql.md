---
title: Todas as (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server (starting with 2008)
f1_keywords:
- ALL_TSQL
- ALL
dev_langs:
- TSQL
helpviewer_keywords:
- single-column set of values [SQL Server]
- ALL (Transact-SQL)
ms.assetid: 4b0c002e-1ffd-4425-a980-11fdc1f24af7
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1fd1b250a30b83a3b014384aafee6c40ff4f1a5a
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="all-transact-sql"></a>ALL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Compara um valor escalar com um conjunto de valores de uma única coluna.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
scalar_expression { = | <> | != | > | >= | !> | < | <= | !< } ALL ( subquery )  
```  
  
## <a name="arguments"></a>Argumentos  
 *scalar_expression*  
 É qualquer [expressão](../../t-sql/language-elements/expressions-transact-sql.md).  
  
 { = | <> | != | > | >= | !> | < | <= | !< }  
 É um operador de comparação.  
  
 *subconsulta*  
 É uma subconsulta que retorna um conjunto de resultados com uma coluna. O tipo de dados da coluna retornada deve ser o mesmo tipo de dados como o tipo de dados de *scalar_expression*.  
  
 É uma instrução SELECT restrita, na qual a cláusula ORDER BY e a palavra-chave INTO não são permitidas.  
  
## <a name="result-types"></a>Tipos de resultado  
 **Booliano**  
  
## <a name="result-value"></a>Valor do resultado  
 Retorna verdadeiro quando a comparação especificada é verdadeiro para todos os pares (*scalar_expression***,***x)*, quando *x* é um valor na conjunto de coluna única. Caso contrário, retornará FALSE.  
  
## <a name="remarks"></a>Comentários  
 ALL requer o *scalar_expression* seja comparada positivamente com todo valor retornado pela subconsulta. Por exemplo, se a subconsulta retornar os valores 2 e 3, *scalar_expression* < = ALL (a subconsulta) será avaliada como TRUE para um *scalar_expression* de 2. Se a subconsulta retornar os valores 2 e 3, *scalar_expression* = ALL (a subconsulta) seria avaliada como FALSE, porque alguns dos valores da subconsulta (o valor de 3) não atende aos critérios da expressão.  
  
 Para instruções que requerem o *scalar_expression* seja comparada positivamente a somente um valor que é retornado pela subconsulta, consulte [alguns &#124; QUALQUER &#40; Transact-SQL &#41; ](../../t-sql/language-elements/some-any-transact-sql.md).  
  
 Este tópico se refere a ALL quando for usado com uma subconsulta. ALL também pode ser usado com [união](../../t-sql/language-elements/set-operators-union-transact-sql.md) e [selecione](../../t-sql/queries/select-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria um procedimento armazenado que determina se todos os componentes de determinado `SalesOrderID` no [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] banco de dados pode ser fabricado no número especificado de dias. O exemplo usa uma subconsulta para criar uma lista do número de valores de `DaysToManufacture` para todos os componentes do `SalesOrderID` específico e depois confirma se todos os `DaysToManufacture` estão dentro do número de dias especificado.  
  
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
PRINT 'Some items for this order cannot be manufactured in specified number of days or less.' ;  
  
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
  
 `Some items for this order cannot be manufactured in specified number of days or less.`  
  
## <a name="see-also"></a>Consulte também  
 [Caso &#40; Transact-SQL &#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [Expressões &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Funções internas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [COMO &#40; Transact-SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [Operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [ONDE &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)   
 [IN &#40; Transact-SQL &#41;](../../t-sql/language-elements/in-transact-sql.md)  
  
  

