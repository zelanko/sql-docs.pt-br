---
title: ISNULL (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
- ISNULL
- ISNULL_TSQL
- IFNULL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- replacing null values
- null values [SQL Server], ISNULL
- null values [SQL Server], replacement values
- ISNULL function
ms.assetid: 6f3e5802-864b-4e77-9862-657bb5430b68
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8d364548d3303de493343365bd16677ffdfd5641
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="isnull-transact-sql"></a>ISNULL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Substitui NULL pelo valor de substituição especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
ISNULL ( check_expression , replacement_value )  
```  
  
## <a name="arguments"></a>Argumentos  
 *check_expression*  
 É o [expressão](../../t-sql/language-elements/expressions-transact-sql.md) a ser verificada para NULL. *check_expression* pode ser de qualquer tipo.  
  
 *replacement_value*  
 A expressão a ser retornada se *check_expression* é NULL. *replacement_value* deve ser de um tipo que é implicitamente conversível para o tipo de *check_expresssion*.  
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna o mesmo tipo *check_expression*. Se um NULL literal for fornecido como *check_expression*, retorna o tipo de dados de *replacement_value*. Se um NULL literal for fornecido como *check_expression* e não *replacement_value* for fornecido, retornará uma **int**.  
  
## <a name="remarks"></a>Comentários  
 O valor de *check_expression* será retornado se não for NULL; caso contrário, *replacement_value* é retornado depois que ele é convertido implicitamente no tipo de *check_expression*, se os tipos são diferentes. *replacement_value* pode ser truncada se *replacement_value* é maior do que *check_expression*.  
  
> [!NOTE]  
>  Use [ADESÃO &#40; Transact-SQL &#41; ](../../t-sql/language-elements/coalesce-transact-sql.md) para retornar o primeiro valor não nulo.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-isnull-with-avg"></a>A. Usando ISNULL com AVG  
 O exemplo a seguir localiza a média do peso de todos os produtos. Substitui o valor `50` para todas as entradas NULL na coluna `Weight` da tabela `Product`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT AVG(ISNULL(Weight, 50))  
FROM Production.Product;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 -------------------------- 
59.79  
  
 (1 row(s) affected)
 ```  
  
### <a name="b-using-isnull"></a>B. Usando ISNULL  
 O exemplo a seguir seleciona a descrição, o percentual de desconto, a quantidade mínima e a quantidade máxima para todas as ofertas especiais em `AdventureWorks2012`. Se a quantidade máxima de uma oferta especial específica for NULL, a `MaxQty` mostrada no conjunto de resultados será `0.00`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Description, DiscountPct, MinQty, ISNULL(MaxQty, 0.00) AS 'Max Quantity'  
FROM Sales.SpecialOffer;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|  Description       |  DiscountPct    |   MinQty    |   Quantidade máxima       |
|  ---------------   |  -------------  |   --------  |   ---------------    |
|  No Discount       |  0.00           |   0         |   0                  |
|  Volume Discount   |  0.02           |   11        |   14                 |
|  Volume Discount   |  0.05           |   15        |   4                  |
|  Volume Discount   |  0.10           |   25        |   0                  |
|  Volume Discount   |  0.15           |   41        |   0                  |
|  Volume Discount   |  0.20           |   61        |   0                  |
|  Mountain-100 Cl   |  0.35           |   0         |   0                  |
|  Injeção de dependência de Capacete Sport   |  0.10           |   0         |   0                  |
|  Road-650 Overst   |  0.30           |   0         |   0                  |
|  Pneu para Mountain Bike S   |  0.50           |   0         |   0                  |
|  Injeção de dependência de Capacete Sport   |  0.15           |   0         |   0                  |
|  Quadro de estrada LL S   |  0.35           |   0         |   0                  |
|  Pr Touring-3000   |  0.15           |   0         |   0                  |
|  Pr Touring-1000   |  0.20           |   0         |   0                  |
|  Metade do preço Peda   |  0.50           |   0         |   0                  |
|  Si Mountain-500   |  0.40           |   0         |   0                  |

 `(16 row(s) affected)`  
  
### <a name="c-testing-for-null-in-a-where-clause"></a>C. Testando NULL em uma cláusula WHERE  
 Não use ISNULL para localizar valores NULL. Em vez disso, use IS NULL. O exemplo a seguir localiza todos os produtos que têm `NULL` na coluna de peso. Observe o espaço entre `IS` e `NULL`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Name, Weight  
FROM Production.Product  
WHERE Weight IS NULL;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-isnull-with-avg"></a>D. Usando ISNULL com AVG  
 O exemplo a seguir encontra a média do peso de todos os produtos em uma tabela de exemplo. Substitui o valor `50` para todas as entradas NULL na coluna `Weight` da tabela `Product`.  
  
```  
-- Uses AdventureWorks  
  
SELECT AVG(ISNULL(Weight, 50))  
FROM dbo.DimProduct;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--------------------------   
52.88   
```  
  
### <a name="e-using-isnull"></a>E. Usando ISNULL  
 O exemplo a seguir usa ISNULL para testar valores NULL na coluna `MinPaymentAmount` e exibir o valor `0.00` para essas linhas.  
  
```  
-- Uses AdventureWorks  
  
SELECT ResellerName,   
       ISNULL(MinPaymentAmount,0) AS MinimumPayment  
FROM dbo.DimReseller  
ORDER BY ResellerName;  
  
```  
  
 Este é um conjunto de resultados parcial.  
  
|  ResellerName                |  MinimumPayment    |
|  -------------------------   |  --------------    |
|  Uma associação de bicicleta       |     0.0000         |
|  Um repositório de bicicleta                |     0.0000         |
|  Uma fábrica de ciclo                |     0.0000         |
|  Uma empresa de bicicleta ótimo     |     0.0000         |
|  Uma loja de bicicleta típico         |   200.0000         |
|  Aceitável de vendas e de serviço  |     0.0000         |
  
### <a name="f-using-is-null-to-test-for-null-in-a-where-clause"></a>F. Usando IS NULL para testar o NULL em uma cláusula WHERE  
 O exemplo a seguir localiza todos os produtos que têm `NULL` no `Weight` coluna. Observe o espaço entre `IS` e `NULL`.  
  
```  
-- Uses AdventureWorks  
  
SELECT EnglishProductName, Weight  
FROM dbo.DimProduct  
WHERE Weight IS NULL;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Expressões &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [É NULL &#40; Transact-SQL &#41;](../../t-sql/queries/is-null-transact-sql.md)   
 [Funções de sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [ONDE &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)   
 [União &#40; Transact-SQL &#41;](../../t-sql/language-elements/coalesce-transact-sql.md)  
  
  


