---
title: VAR (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- VAR
- VAR_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- statistical variances
- expressions [SQL Server], statistical variance
- VAR function [Transact-SQL]
ms.assetid: 71dfc339-16c8-42f9-8555-ad45400f7f9b
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c9b716b085e45fbdb9071fa0dbc368ad02993f59
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82828530"
---
# <a name="var-transact-sql"></a>VAR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna a variância estatística de todos os valores da expressão especificada. Pode ser seguido pela [cláusula OVER](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```    
-- Aggregate Function Syntax   
VAR ( [ ALL | DISTINCT ] expression )  
  
-- Analytic Function Syntax  
VAR ([ ALL ] expression) OVER ( [ partition_by_clause ] order_by_clause)  
```  
  
## <a name="arguments"></a>Argumentos  
 **ALL**  
 Aplica a função a todos os valores. ALL é o padrão.  
  
 DISTINTO  
 Especifica que cada valor exclusivo é considerado.  
  
 *expressão*  
 É uma [expression](../../t-sql/language-elements/expressions-transact-sql.md) da categoria de tipo de dados numéricos exatos ou aproximados, com exceção do tipo de dados **bit**. Funções de agregação e subconsultas não são permitidas.  
  
 OVER **(** [ _partition\_by\_clause_ ] _order\_by\_clause_ **)**  
 *partition_by_clause* divide o conjunto de resultados produzido pela cláusula FROM em partições às quais a função é aplicada. Se não for especificado, a função tratará todas as linhas do conjunto de resultados da consulta como um único grupo. _order\_by\_clause_ determina a ordem lógica na qual a operação é executada. _order\_by\_clause_ é necessário. Para obter mais informações, consulte [Cláusula OVER &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>Tipos de retorno  
 **float**  
  
## <a name="remarks"></a>Comentários  
 Se VAR for usado em todos os itens uma instrução SELECT, cada valor do conjunto de resultados será incluído no cálculo. VAR pode ser usado exclusivamente com colunas numéricas. Valores nulos são ignorados.  
  
 VAR é uma função determinística quando usada sem as cláusulas OVER e ORDER BY. É não determinística quando especificada com as cláusulas OVER e ORDER BY. Para obter mais informações, veja [Funções determinísticas e não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-var"></a>A: Usando VAR  
 O exemplo a seguir retorna a variância padrão de todos os valores de gratificação da tabela `SalesPerson` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
SELECT VAR(Bonus)  
FROM Sales.SalesPerson;  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-using-var"></a>B: Usando VAR  
 O exemplo a seguir retorna a variância estatística dos valores de cota de vendas na tabela `dbo.FactSalesQuota`. A primeira coluna contém a variação de todos os valores distintos e a segunda coluna contém a variação de todos os valores, incluindo valores duplicados.  
  
```  
-- Uses AdventureWorks  
  
SELECT VAR(DISTINCT SalesAmountQuota)AS Distinct_Values, VAR(SalesAmountQuota) AS All_Values  
FROM dbo.FactSalesQuota;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Distinct_Values   All_Values
----------------  ----------------
159180469909.18   158762853821.10
 ```  
  
### <a name="c-using-var-with-over"></a>C. Usando VAR com OVER  
 O exemplo a seguir retorna a variância estatística dos valores de cota de vendas para cada trimestre em um ano civil. Observe que ORDER BY na cláusula OVER ordena a variação estatística e ORDER BY da instrução SELECT ordena o conjunto de resultados.  
  
```  
-- Uses AdventureWorks  
  
SELECT CalendarYear AS Year, CalendarQuarter AS Quarter, SalesAmountQuota AS SalesQuota,  
       VAR(SalesAmountQuota) OVER (ORDER BY CalendarYear, CalendarQuarter) AS Variance  
FROM dbo.FactSalesQuota  
WHERE EmployeeKey = 272 AND CalendarYear = 2002  
ORDER BY CalendarQuarter;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Year  Quarter  SalesQuota              Variance
----  -------  ----------------------  -------------------
2002  1         91000.0000             null
2002  2        140000.0000             1200500000.00
2002  3         70000.0000             1290333333.33
2002  4        154000.0000             1580250000.00
 ```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções de agregação &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)   
 [Cláusula OVER &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)  
  
  

