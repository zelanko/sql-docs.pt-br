---
title: Criar funções definidas pelo usuário (Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SCHEMABINDING clause
- schema-bound functions [SQL Server]
- user-defined functions [SQL Server], creating
- CREATE FUNCTION statement
- valid statements [SQL Server]
ms.assetid: f0d5dd10-73fd-4e05-9177-07f56552bdf7
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1fec7107d5ba00c27e6f81eabfd2bfb199096224
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37418905"
---
# <a name="create-user-defined-functions-database-engine"></a>Criar funções definidas pelo usuário (Mecanismo de Banco de Dados)
  Este tópico descreve como criar uma função definida pelo usuário no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para criar uma função definida pelo usuário:**  
  
     [Crie uma função escalar](#Scalar)  
  
     [Criar uma função com valor de tabela](#TVF)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Funções definidas pelo usuário não podem ser usadas para executar ações que modificam o estado do banco de dados.  
  
-   As funções definidas pelo usuário não podem conter uma cláusula OUTPUT INTO que tenha uma tabela como seu destino.  
  
-   As funções definidas pelo usuário não podem retornar vários conjuntos de resultados. Use um procedimento armazenado se precisar retornar vários conjuntos de resultados.  
  
-   O tratamento de erros é restringido em uma função definida pelo usuário. Um UDF não dá suporte a TRY…CATCH, @ERROR ou RAISERROR.  
  
-   As funções definidas pelo usuário não podem chamar um procedimento armazenado, mas podem chamar um procedimento armazenado estendido.  
  
-   As funções definidas pelo usuário não podem fazer uso de SQL dinâmico ou tabelas temporárias. Variáveis de tabela são permitidas.  
  
-   A instruções SET não são permitidas em uma função definida pelo usuário.  
  
-   A cláusula FOR XML não é permitida.  
  
-   Funções definidas pelo usuário podem ser aninhadas, isto é, uma função definida pelo usuário pode chamar outra. O nível de aninhamento é incrementado quando a execução da função é iniciada, e reduzido quando a execução da função chamada é concluída. Até 32 níveis de funções definidas pelo usuário podem ser aninhados. Se o máximo de níveis de aninhamento for excedido haverá falha em toda a cadeia de funções da chamada de aninhamento. Qualquer referência a um código gerenciado de uma função definida pelo usuário do Transact-SQL é contada como um nível em relação ao limite de 32 níveis de aninhamento. Os métodos invocados a partir do código gerenciado não são contados em relação a esse limite.  
  
-   As seguintes instruções do Service Broker não podem ser incluídas na definição de uma função Transact-SQL definida pelo usuário:  
  
    -   BEGIN DIALOG CONVERSATION  
  
    -   END CONVERSATION  
  
    -   GET CONVERSATION GROUP  
  
    -   MOVE CONVERSATION  
  
    -   RECEIVE  
  
    -   SEND  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão CREATE FUNCTION no banco de dados e a permissão ALTER no esquema no qual a função está sendo criada. Se a função especificar um tipo definido pelo usuário, a permissão EXECUTE será exigida no tipo.  
  
##  <a name="Scalar"></a> Funções escalares  
 O exemplo a seguir cria uma função escalar de várias instruções no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] . A função pega um valor de entrada, um `ProductID`, e retorna um único valor de dados, a quantidade agregada do produto especificado no estoque.  
  
```  
IF OBJECT_ID (N'dbo.ufnGetInventoryStock', N'FN') IS NOT NULL  
    DROP FUNCTION ufnGetInventoryStock;  
GO  
CREATE FUNCTION dbo.ufnGetInventoryStock(@ProductID int)  
RETURNS int   
AS   
-- Returns the stock level for the product.  
BEGIN  
    DECLARE @ret int;  
    SELECT @ret = SUM(p.Quantity)   
    FROM Production.ProductInventory p   
    WHERE p.ProductID = @ProductID   
        AND p.LocationID = '6';  
     IF (@ret IS NULL)   
        SET @ret = 0;  
    RETURN @ret;  
END;  
GO  
  
```  
  
 O exemplo a seguir usa a função `ufnGetInventoryStock` , para retornar a quantidade atual do estoque dos produtos que têm um `ProductModelID` entre 75 e 80.  
  
```  
SELECT ProductModelID, Name, dbo.ufnGetInventoryStock(ProductID)AS CurrentSupply  
FROM Production.Product  
WHERE ProductModelID BETWEEN 75 and 80;  
  
```  
  
##  <a name="TVF"></a> Funções com valor de tabela  
 O exemplo a seguir cria uma função com valor de tabela embutida no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] . A função pega um parâmetro de entrada, um ID cliente (loja), e retorna as colunas `ProductID`, `Name`e a agregação das vendas do ano, até a data atual, como `YTD Total` para cada produto vendido para a loja.  
  
```  
IF OBJECT_ID (N'Sales.ufn_SalesByStore', N'IF') IS NOT NULL  
    DROP FUNCTION Sales.ufn_SalesByStore;  
GO  
CREATE FUNCTION Sales.ufn_SalesByStore (@storeid int)  
RETURNS TABLE  
AS  
RETURN   
(  
    SELECT P.ProductID, P.Name, SUM(SD.LineTotal) AS 'Total'  
    FROM Production.Product AS P   
    JOIN Sales.SalesOrderDetail AS SD ON SD.ProductID = P.ProductID  
    JOIN Sales.SalesOrderHeader AS SH ON SH.SalesOrderID = SD.SalesOrderID  
    JOIN Sales.Customer AS C ON SH.CustomerID = C.CustomerID  
    WHERE C.StoreID = @storeid  
    GROUP BY P.ProductID, P.Name  
);  
  
```  
  
 O exemplo a seguir invoca a função e especifica a ID do cliente 602.  
  
```  
SELECT * FROM Sales.ufn_SalesByStore (602);  
  
```  
  
 O exemplo a seguir cria uma função com valor de tabela no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] . A função usa um único parâmetro de entrada, um `EmployeeID` , e retorna uma lista de todos os funcionários que reportam direta ou indiretamente ao funcionário especificado. A função que especifica a ID do funcionário 109 é invocada em seguida.  
  
```  
IF OBJECT_ID (N'dbo.ufn_FindReports', N'TF') IS NOT NULL  
    DROP FUNCTION dbo.ufn_FindReports;  
GO  
CREATE FUNCTION dbo.ufn_FindReports (@InEmpID INTEGER)  
RETURNS @retFindReports TABLE   
(  
    EmployeeID int primary key NOT NULL,  
    FirstName nvarchar(255) NOT NULL,  
    LastName nvarchar(255) NOT NULL,  
    JobTitle nvarchar(50) NOT NULL,  
    RecursionLevel int NOT NULL  
)  
--Returns a result set that lists all the employees who report to the   
--specific employee directly or indirectly.*/  
AS  
BEGIN  
WITH EMP_cte(EmployeeID, OrganizationNode, FirstName, LastName, JobTitle, RecursionLevel) -- CTE name and columns  
    AS (  
        SELECT e.BusinessEntityID, e.OrganizationNode, p.FirstName, p.LastName, e.JobTitle, 0 -- Get the initial list of Employees for Manager n  
        FROM HumanResources.Employee e   
INNER JOIN Person.Person p   
ON p.BusinessEntityID = e.BusinessEntityID  
        WHERE e.BusinessEntityID = @InEmpID  
        UNION ALL  
        SELECT e.BusinessEntityID, e.OrganizationNode, p.FirstName, p.LastName, e.JobTitle, RecursionLevel + 1 -- Join recursive member to anchor  
        FROM HumanResources.Employee e   
            INNER JOIN EMP_cte  
            ON e.OrganizationNode.GetAncestor(1) = EMP_cte.OrganizationNode  
INNER JOIN Person.Person p   
ON p.BusinessEntityID = e.BusinessEntityID  
        )  
-- copy the required columns to the result of the function   
   INSERT @retFindReports  
   SELECT EmployeeID, FirstName, LastName, JobTitle, RecursionLevel  
   FROM EMP_cte   
   RETURN  
END;  
GO  
-- Example invocation  
SELECT EmployeeID, FirstName, LastName, JobTitle, RecursionLevel  
FROM dbo.ufn_FindReports(1);  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções definidas pelo usuário](user-defined-functions.md)   
 [CREATE FUNCTION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-function-transact-sql)  
  
  
