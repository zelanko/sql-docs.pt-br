---
title: Criar funções definidas pelo usuário (Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 11/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- SCHEMABINDING clause
- schema-bound functions [SQL Server]
- user-defined functions [SQL Server], creating
- CREATE FUNCTION statement
- valid statements [SQL Server]
- UDF
- TVF
ms.assetid: f0d5dd10-73fd-4e05-9177-07f56552bdf7
author: rothja
ms.author: jroth
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6b2ff8188f2733fd0467ac39266bc9f0510de621
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52515477"
---
# <a name="create-user-defined-functions-database-engine"></a>Criar funções definidas pelo usuário (Mecanismo de Banco de Dados)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  Este tópico descreve como criar uma UDF (função definida pelo usuário) no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Funções definidas pelo usuário não podem ser usadas para executar ações que modificam o estado do banco de dados.  
  
-   As funções definidas pelo usuário não podem conter uma cláusula `OUTPUT INTO` que tenha uma tabela como seu destino.  
  
-   As funções definidas pelo usuário não podem retornar vários conjuntos de resultados. Use um procedimento armazenado se precisar retornar vários conjuntos de resultados.  
  
-   O tratamento de erros é restringido em uma função definida pelo usuário. Uma UDF não é compatível com `TRY...CATCH`, `@ERROR` ou `RAISERROR`.  
  
-   As funções definidas pelo usuário não podem chamar um procedimento armazenado, mas podem chamar um procedimento armazenado estendido.  
  
-   As funções definidas pelo usuário não podem fazer uso de SQL dinâmico ou tabelas temporárias. Variáveis de tabela são permitidas.  
  
-   As instruções `SET` não são permitidas em uma função definida pelo usuário.  
  
-   A cláusula `FOR XML` vazia não é permitida.  
  
-   Funções definidas pelo usuário podem ser aninhadas, isto é, uma função definida pelo usuário pode chamar outra. O nível de aninhamento é incrementado quando a execução da função é iniciada, e reduzido quando a execução da função chamada é concluída. Até 32 níveis de funções definidas pelo usuário podem ser aninhados. Se o máximo de níveis de aninhamento for excedido haverá falha em toda a cadeia de funções da chamada de aninhamento. Qualquer referência a um código gerenciado de uma função definida pelo usuário do Transact-SQL é contada como um nível em relação ao limite de 32 níveis de aninhamento. Os métodos invocados a partir do código gerenciado não são contados em relação a esse limite.  
  
-   As seguintes instruções do Service Broker **não podem ser incluídas** na definição de uma função definida pelo usuário [!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
    -   `BEGIN DIALOG CONVERSATION`  
  
    -   `END CONVERSATION`  
  
    -   `GET CONVERSATION GROUP`  
  
    -   `MOVE CONVERSATION`  
  
    -   `RECEIVE`  
  
    -   `SEND`  
  
###  <a name="Security"></a> Permissões 

Requer a permissão `CREATE FUNCTION` no banco de dados e a permissão `ALTER` no esquema no qual a função está sendo criada. Se a função especificar um tipo definido pelo usuário, a permissão `EXECUTE` será exigida no tipo.  
  
##  <a name="Scalar"></a> Funções escalares  
 O exemplo a seguir cria uma **função escalar (UDF escalar)** de várias instruções no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. A função pega um valor de entrada, um `ProductID`, e retorna um único valor de dados, a quantidade agregada do produto especificado no estoque.  
  
```sql  
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
```  
  
 O exemplo a seguir usa a função `ufnGetInventoryStock` , para retornar a quantidade atual do estoque dos produtos que têm um `ProductModelID` entre 75 e 80.  
  
```sql  
SELECT ProductModelID, Name, dbo.ufnGetInventoryStock(ProductID)AS CurrentSupply  
FROM Production.Product  
WHERE ProductModelID BETWEEN 75 and 80;  
```  

> [!NOTE]  
> Para obter mais informações e exemplos de funções escalares, confira [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md). 

##  <a name="TVF"></a> Funções com valor de tabela  
O exemplo a seguir cria uma **TVF (função com valor de tabela) embutida** no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. A função pega um parâmetro de entrada, um ID cliente (loja), e retorna as colunas `ProductID`, `Name`e a agregação das vendas do ano, até a data atual, como `YTD Total` para cada produto vendido para a loja.  
  
```sql  
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
  
```sql  
SELECT * FROM Sales.ufn_SalesByStore (602);  
```  
  
O exemplo a seguir cria uma **MSTVF (função com valor de tabela de várias instruções)** no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. A função usa um único parâmetro de entrada, um `EmployeeID` , e retorna uma lista de todos os funcionários que reportam direta ou indiretamente ao funcionário especificado. A função que especifica a ID do funcionário 109 é invocada em seguida.  
  
```sql  
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
```  
  
O exemplo a seguir invoca a função e especifica a ID do funcionário 1.  
  
```sql  
SELECT EmployeeID, FirstName, LastName, JobTitle, RecursionLevel  
FROM dbo.ufn_FindReports(1);  
```  

> [!NOTE]  
> Para obter mais informações e exemplos TVFs embutidas (funções com valor de tabela embutidas) e MSTVFs (funções com valor de tabela de várias instruções), confira [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md). 

## <a name="best-practices"></a>Práticas recomendadas  
Se uma UDF (função definida pelo usuário) não for criada com a cláusula `SCHEMABINDING`, as alterações feitas nos objetos subjacentes poderão afetar a definição da função e produzir resultados inesperados quando ela for chamada. É recomendável que você implemente um dos seguintes métodos para garantir que a função não se torne desatualizada devido a alterações em seus objetos subjacentes:  
  
-   Especifique a cláusula `WITH SCHEMABINDING` quando você estiver criando a UDF. Isso garante que os objetos referenciados na definição da função não possam ser modificados, a menos que a função também seja modificada.  
  
-   Execute o procedimento armazenado [sp_refreshsqlmodule](../../relational-databases/system-stored-procedures/sp-refreshsqlmodule-transact-sql.md) depois de modificar um objeto especificado na definição da UDF.  

Se estiver criando uma UDF que não acessa os dados, especifique a opção `SCHEMABINDING`. Isso impedirá que o otimizador de consulta gere operadores de spool desnecessários para planos de consulta que envolvem essas UDFs. Para obter mais informações sobre spools, confira [Referência de operadores lógicos e físicos de plano de execução](../../relational-databases/showplan-logical-and-physical-operators-reference.md). Para obter mais informações sobre como criar uma função associada a esquema, confira [Funções associadas a esquema](../../relational-databases/user-defined-functions/user-defined-functions.md#SchemaBound).

O ingresso em uma MSTVF em uma cláusula `FROM` é possível, mas pode resultar em baixo desempenho. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode usar todas as técnicas otimizadas em algumas instruções que podem ser incluídas em uma MSTVF, resultando em um plano de consulta de qualidade inferior. Para obter o melhor desempenho possível, sempre que possível use junções entre tabelas base em vez de funções.  

> [!IMPORTANT]
> As MSTVFs têm uma estimativa de cardinalidade fixa de 100 começando com [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e de 1 para versões anteriores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].    
> Começando com [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)], otimizar um plano de execução que usa as MSTVFs pode aproveitar a execução intercalada, que resulta no uso de cardinalidade real em vez da heurística acima.     
> Para obter mais informações, consulte [Interleaved execution for multi-statement table valued functions](../../relational-databases/performance/adaptive-query-processing.md#interleaved-execution-for-multi-statement-table-valued-functions) (Execução intercalada para funções com valor de tabela de várias instruções).

> [!NOTE]  
> ANSI_WARNINGS não é cumprido quando você passa parâmetros em um procedimento armazenado, em uma função definida pelo usuário ou quando declara ou define variáveis em uma instrução de lote. Por exemplo, se a variável for definida como **char(3)** e, em seguida, configurada com um valor maior que três caracteres, os dados serão truncados até o tamanho definido e a instrução `INSERT` ou `UPDATE` terá êxito.

## <a name="see-also"></a>Consulte Também  
 [Funções definidas pelo usuário](../../relational-databases/user-defined-functions/user-defined-functions.md)     
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)    
 [ALTER FUNCTION &#40;Transact-SQL&#41;](../../tools/sql-server-profiler/start-sql-server-profiler.md)    
 [DROP FUNCTION &#40;Transact-SQL&#41;](../../tools/sql-server-profiler/start-sql-server-profiler.md)     
 [DROP PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-partition-function-transact-sql.md)    
 Veja mais exemplos na [comunidade](https://www.bing.com/search?q=user%20defined%20function%20%22sql%20server%202016%22%20examples&qs=n&form=QBRE&pq=user%20defined%20function%20%22sql%20server%202016%22%20examples&sc=0-48&sp=-1&sk=&cvid=C3AD337125A840AD9EEFA3AAC36A3712)   
  
