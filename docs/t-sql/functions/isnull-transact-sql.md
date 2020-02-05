---
title: ISNULL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b49310a633c822f8c57f66cc36951dfebe2c0707
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "73843642"
---
# <a name="isnull-transact-sql"></a>ISNULL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Substitui NULL pelo valor de substituição especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
ISNULL ( check_expression , replacement_value )  
```  
  
## <a name="arguments"></a>Argumentos  
 *check_expression*  
 É a [expressão](../../t-sql/language-elements/expressions-transact-sql.md) a ser verificada para NULL. *check_expression* pode ser de qualquer tipo.  
  
 *replacement_value*  
 É a expressão a ser retornada se *check_expression* for NULL. *replacement_value* deve ser de um tipo que seja implicitamente convertido no tipo *check_expression*.  
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna o mesmo tipo que *check_expression*. Se um NULL literal for fornecido como *check_expression*, retornará o tipo de dados de *replacement_value*. Se um NULL literal for fornecido como *check_expression* e nenhum *replacement_value* for fornecido, retornará um **int**.  
  
## <a name="remarks"></a>Comentários  
 O valor de *check_expression* será retornado se não for NULL, caso contrário, *replacement_value* será retornado depois de ser convertido implicitamente no tipo de *check_expression*, se os tipos forem diferentes. *replacement_value* poderá ser truncado se *replacement_value* for maior do que *check_expression*.  
  
> [!NOTE]  
>  Use [COALESCE &#40;Transact-SQL&#41; ](../../t-sql/language-elements/coalesce-transact-sql.md) para retornar o primeiro valor não nulo.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-isnull-with-avg"></a>a. Usando ISNULL com AVG  
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
  
|  DESCRIÇÃO       |  DiscountPct    |   MinQty    |   Quantidade Máx.       |
|  ---------------   |  -------------  |   --------  |   ---------------    |
|  No Discount       |  0,00           |   0         |   0                  |
|  Volume Discount   |  0,02           |   11        |   14                 |
|  Volume Discount   |  0,05           |   15        |   4                  |
|  Volume Discount   |  0.10           |   25        |   0                  |
|  Volume Discount   |  0.15           |   41        |   0                  |
|  Volume Discount   |  0,20           |   61        |   0                  |
|  Mountain-100 Cl   |  0,35           |   0         |   0                  |
|  Sport Helmet Di   |  0.10           |   0         |   0                  |
|  Road-650 Overst   |  0,30           |   0         |   0                  |
|  Mountain Tire S   |  0.50           |   0         |   0                  |
|  Sport Helmet Di   |  0.15           |   0         |   0                  |
|  LL Road Frame S   |  0,35           |   0         |   0                  |
|  Touring-3000 Pr   |  0.15           |   0         |   0                  |
|  Touring-1000 Pr   |  0,20           |   0         |   0                  |
|  Half-Price Peda   |  0.50           |   0         |   0                  |
|  Mountain-500 Si   |  0,40           |   0         |   0                  |

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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-isnull-with-avg"></a>D. Usando ISNULL com AVG  
 O exemplo a seguir localiza a média do peso de todos os produtos em uma tabela de amostra. Substitui o valor `50` para todas as entradas NULL na coluna `Weight` da tabela `Product`.  
  
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
|  Uma Associação de Bicicletas       |     0,0000         |
|  Uma Loja de Bicicletas                |     0,0000         |
|  Uma Loja de Bike                |     0,0000         |
|  Uma Ótima Empresa de Bicicleta     |     0,0000         |
|  Uma Loja de Bicicletas Típica         |   200,0000         |
|  Vendas e Serviço Aceitáveis  |     0,0000         |
  
### <a name="f-using-is-null-to-test-for-null-in-a-where-clause"></a>F. Usando IS NULL para testar NULL em uma cláusula WHERE  
 O exemplo a seguir localiza todos os produtos que têm `NULL` na coluna `Weight`. Observe o espaço entre `IS` e `NULL`.  
  
```  
-- Uses AdventureWorks  
  
SELECT EnglishProductName, Weight  
FROM dbo.DimProduct  
WHERE Weight IS NULL;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [IS NULL &#40;Transact-SQL&#41;](../../t-sql/queries/is-null-transact-sql.md)   
 [Funções de sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [COALESCE &#40;Transact-SQL&#41;](../../t-sql/language-elements/coalesce-transact-sql.md)  
  
  

