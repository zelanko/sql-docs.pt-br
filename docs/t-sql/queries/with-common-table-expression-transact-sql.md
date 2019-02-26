---
title: WITH common_table_expression (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WITH common_table_expression
- WITH_TSQL
- WITH
- common table expression
dev_langs:
- TSQL
helpviewer_keywords:
- WITH common_table_expression clause
- CTEs
- hierarchical queries [SQL Server], WITH common_table_expression
- recursive CTEs [SQL Server]
- recursive queries [SQL Server]
- common table expressions
- MAXRECURSION hint
- clauses [SQL Server], WITH common_table_expression
ms.assetid: 27cfb819-3e8d-4274-8bbe-cbbe4d9c2e23
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: abccf047d58d03867f08ea9a0068c5acdbe49ea8
ms.sourcegitcommit: a13256f484eee2f52c812646cc989eb0ce6cf6aa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/25/2019
ms.locfileid: "56802560"
---
# <a name="with-commontableexpression-transact-sql"></a>WITH common_table_expression (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Especifica um conjunto de resultados nomeado temporário, conhecido como uma CTE (expressão de tabela comum). Ela é derivada de uma consulta simples e definida no escopo de execução de uma única instrução SELECT, INSERT, UPDATE, DELETE ou MERGE. Esta cláusula também pode ser usada em uma instrução CREATE VIEW como parte da instrução SELECT que a define. Uma expressão de tabela comum pode incluir referências a si mesma. É o que chamamos de expressão de tabela comum recursiva.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
[ WITH <common_table_expression> [ ,...n ] ]  
  
<common_table_expression>::=  
    expression_name [ ( column_name [ ,...n ] ) ]  
    AS  
    ( CTE_query_definition )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression_name*  
É um identificador válido para a expressão de tabela comum. *expression_name* deve ser diferente do nome de qualquer outra expressão de tabela comum definida na mesma cláusula WITH \<common_table_expression>, mas *expression_name* pode ser o mesmo que o nome de uma tabela base ou exibição. Qualquer referência a *expression_name* na consulta usa a expressão de tabela comum, e não o objeto base.
  
 *column_name*  
 Especifica um nome de coluna na expressão de tabela comum. Não são permitidos nomes duplicados em uma única definição de CTE. O número de nomes de coluna especificado deve corresponder ao número de colunas no conjunto de resultados da *CTE_query_definition*. A lista de nomes de colunas será opcional somente se forem fornecidos nomes distintos para todas as colunas resultantes na definição da consulta.  
  
 *CTE_query_definition*  
 Especifica uma instrução SELECT cujo conjunto de resultados popula a expressão de tabela comum. A instrução SELECT de *CTE_query_definition* deve atender aos mesmos requisitos da criação de uma exibição, com a exceção de que uma CTE não pode definir outra CTE. Para obter mais informações, consulte a seção Comentários e [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md).  
  
 Se mais de uma *CTE_query_definition* for definida, as definições de consulta poderão ser unidas por um destes dois conjuntos de operadores: UNION ALL, UNION, EXCEPT ou INTERSECT.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="guidelines-for-creating-and-using-common-table-expressions"></a>Diretrizes para criar e usar expressões de tabela comuns  
 As diretrizes a seguir se aplicam a expressões de tabela comuns não recursivas. Para verificar as diretrizes relacionadas a expressões de tabela comuns recursivas, consulte "Diretrizes para definir e usar expressões de tabela comuns recursivas" a seguir.  
  
-   Uma CTE deve ser seguida por uma única instrução SELECT, INSERT, UPDATE ou DELETE que faça referência a algumas ou todas as colunas da CTE. Uma CTE também pode ser especificada em uma instrução CREATE VIEW como parte da instrução SELECT que define a exibição.  
  
-   É possível ter várias definições de consulta CTE em uma CTE não recursiva. As definições devem ser combinadas por um destes operadores de conjunto: UNION ALL, UNION, INTERSECT ou EXCEPT.  
  
-   Uma CTE pode fazer referência a si mesma e a CTEs definidas anteriormente na mesma cláusula WITH. Não é permitido referência antecipada.  
  
-   Não é permitida a especificação de mais de uma cláusula WITH em uma CTE. Por exemplo, se uma *CTE_query_definition* contiver uma subconsulta, essa subconsulta não poderá conter uma cláusula WITH aninhada que define outra CTE.  
  
-   As seguintes cláusulas não podem ser usadas na *CTE_query_definition*:  
  
    -   ORDER BY (exceto quando uma cláusula TOP for especificada)  
  
    -   INTO  
  
    -   Cláusula OPTION com dicas de consulta  
  
    -   FOR BROWSE  
  
-   Quando uma CTE for usada em uma instrução que faça parte de um lote, a instrução anterior a ela deverá ser seguida por um ponto-e-vírgula.  
  
-   Uma consulta que faça referência a uma CTE pode ser usada para definir um cursor.  
  
-   As tabelas em servidores remotos podem ser referenciadas na CTE.  
  
-   Ao executar uma CTE, quaisquer dicas que façam referência a uma CTE podem entrar em conflito com outras dicas que forem descobertas quando a CTE acessar suas tabelas subjacentes, da mesma maneira como as dicas que fazem referência a exibições em consultas. Quando isso ocorre, a consulta retorna um erro.  
  
## <a name="guidelines-for-defining-and-using-recursive-common-table-expressions"></a>Diretrizes para definir e usar expressões de tabela comuns recursivas  
 As seguintes diretrizes aplicam-se à definição de uma expressão de tabela comum recursiva:  
  
-   A definição da CTE recursiva deve conter pelo menos duas definições de consulta de CTE, um membro de ancoragem e um membro recursivo. É possível definir vários membros de ancoragem e membros recursivos; entretanto, todas as definições de consulta de membro de ancoragem devem ser colocadas antes da primeira definição de membro recursivo. Todas as definições de consulta de CTE são membros de ancoragem, a menos que façam referência à própria CTE.  
  
-   Membros de ancoragem devem ser combinados por um destes operadores de conjunto: UNION ALL, UNION, INTERSECT ou EXCEPT. UNION ALL é o único operador de conjunto permitido entre o último membro de ancoragem e o primeiro membro recursivo e ao combinar vários membros recursivos.  
  
-   O número de colunas nos membros de ancoragem e recursivos deve ser o mesmo.  
  
-   O tipo de dados de uma coluna no membro recursivo deve ser o mesmo que o tipo de dados da coluna correspondente no membro de ancoragem.  
  
-   A cláusula FROM de um membro recursivo deve referenciar apenas uma vez o *expression_name* da CTE.  
  
-   Os seguintes itens não são permitidos na *CTE_query_definition* de um membro recursivo:  
  
    -   SELECT DISTINCT  
  
    -   GROUP BY  
  
    -   PIVOT (Quando o nível de compatibilidade de banco de dados é 110 ou superior. Consulte [Alterações recentes em recursos do Mecanismo de Banco de Dados no SQL Server 2016](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md).)  
  
    -   HAVING  
  
    -   Agregação escalar  
  
    -   INÍCIO  
  
    -   LEFT, RIGHT, OUTER JOIN (INNER JOIN é permitido)  
  
    -   Subconsultas  
  
    -   Uma dica aplicada a uma referência recursiva para uma CTE dentro de uma *CTE_query_definition*.  
  
 As seguintes diretrizes aplicam-se ao uso de uma expressão de tabela comum recursiva:  
  
-   Todas as colunas retornadas pela CTE recursiva aceitam valores nulos, independentemente da possibilidade de nulidade das colunas retornadas pelas instruções SELECT participantes.  
  
-   Uma CTE recursiva incorretamente composta pode causar um loop infinito. Por exemplo, se a definição de consulta do membro recursivo retornar os mesmos valores para as colunas pai e filho, um loop infinito será criado. Para prevenir um loop infinito, é possível limitar o número de níveis de recursão permitidos para uma instrução específica, usando a dica MAXRECURSION e um valor entre 0 e 32.767 na cláusula OPTION da instrução INSERT, UPDATE, DELETE ou SELECT. Isso permite controlar a execução da instrução até que você resolva o problema de código que está criando o loop. O padrão para todo o servidor é 100. Quando 0 é especificado, nenhum limite é aplicado. Apenas um valor MAXRECURSION pode ser especificado por instrução. Para obter mais informações, veja [Dicas de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
-   Uma exibição que contém uma expressão de tabela comum recursiva não pode ser usada para atualizar dados.  
  
-   É possível definir cursores em consultas usando CTEs. A CTE é o argumento *select_statement* que define o conjunto de resultados do cursor. Apenas cursores de somente avanço rápido e estáticos (instantâneos) são permitidos para CTEs recursivas. Se outro tipo de cursor for especificado em uma CTE recursiva, o tipo de cursor será convertido em estático.  
  
-   As tabelas em servidores remotos podem ser referenciadas na CTE. Se o servidor remoto for referenciado no membro recursivo da CTE, um spool será criado para cada tabela remota, de maneira que as tabelas possam ser acessadas localmente repetidamente. Se essa for uma consulta CTE, Index Spool/Lazy Spools será exibido no plano de consulta e terá o predicado adicional WITH STACK. Essa é uma maneira de confirmar a recursão correta.  
  
-   Funções analíticas e de agregação na parte recursiva da CTE são aplicadas para definir o nível de recursão atual e não para a definição da CTE. Funções como ROW_NUMBER funcionam apenas no subconjunto de dados passado para elas pelo nível de recursão atual e não no conjunto inteiro de dados passados para a parte recursiva da CTE. Para obter mais informações, veja o exemplo K. Usando funções analíticas em uma CTE recursiva a seguir.  
  
## <a name="features-and-limitations-of-common-table-expressions-in-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Recursos e limitações de Expressões de Tabela Comum no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 A implementação atual das CTEs no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] apresenta os seguintes recursos e limitações:  
  
-   Uma CTE pode ser especificada em uma instrução **SELECT**.  
  
-   Uma CTE pode ser especificada em uma instrução **CREATE VIEW**.  
  
-   Uma CTE pode ser especificada em uma instrução CTAS (**CREATE TABLE AS SELECT**).  
  
-   Uma CTE pode ser especificada em uma instrução CRTAS (**CREATE REMOTE TABLE AS SELECT**).  
  
-   Uma CTE pode ser especificada em uma instrução CETAS (**CREATE EXTERNAL TABLE AS SELECT**).  
  
-   Uma tabela remota pode ser referenciada em uma CTE.  
  
-   Uma tabela externa pode ser referenciada em uma CTE.  
  
-   Várias definições de consulta CTE podem ser definidas em uma CTE.  
  
-   Uma CTE deve ser seguida de uma única instrução **SELECT**. Não há suporte para as instruções **INSERT**, **UPDATE**, **DELETE** e **MERGE**.  
  
-   Não há suporte para uma expressão de tabela comum que inclui referências a si mesma (uma expressão de tabela comum recursiva).  
  
-   Não é permitida a especificação de mais de uma cláusula **WITH** em uma CTE. Por exemplo, se uma CTE_query_definition contiver uma subconsulta, essa subconsulta não poderá conter uma cláusula **WITH** aninhada que define outra CTE.  
  
-   Uma cláusula **ORDER BY** não pode ser usada na CTE_query_definition, exceto quando uma cláusula **TOP** é especificada.  
  
-   Quando uma CTE for usada em uma instrução que faça parte de um lote, a instrução anterior a ela deverá ser seguida por um ponto-e-vírgula.  
  
-   Quando usadas em instruções preparadas por **sp_prepare**, CTEs se comportarão da mesma maneira que outras instruções **SELECT** no PDW. No entanto, se as CTEs são usadas como parte da instrução CETAS preparada por **sp_prepare**, o comportamento pode ser adiado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e outras instruções do PDW, devido à maneira como a associação é implementada para **sp_prepare**. Se **SELECT** que referencia a CTE estiver usando uma coluna incorreta que não existe na CTE, o **sp_prepare** será passado sem detectar o erro, mas o erro será gerado durante **sp_execute**.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-simple-common-table-expression"></a>A. Criando uma expressão de tabela comum simples  
 O exemplo a seguir mostra o número total de pedidos de vendas por ano para cada representante de vendas na [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)].  
  
```  
  
-- Define the CTE expression name and column list.  
WITH Sales_CTE (SalesPersonID, SalesOrderID, SalesYear)  
AS  
-- Define the CTE query.  
(  
    SELECT SalesPersonID, SalesOrderID, YEAR(OrderDate) AS SalesYear  
    FROM Sales.SalesOrderHeader  
    WHERE SalesPersonID IS NOT NULL  
)  
-- Define the outer query referencing the CTE name.  
SELECT SalesPersonID, COUNT(SalesOrderID) AS TotalSales, SalesYear  
FROM Sales_CTE  
GROUP BY SalesYear, SalesPersonID  
ORDER BY SalesPersonID, SalesYear;  
GO  
  
```  
  
### <a name="b-using-a-common-table-expression-to-limit-counts-and-report-averages"></a>b. Usando uma expressão de tabela comum para limitar contagens e médias de relatório  
 O exemplo a seguir mostra o número médio de pedidos de vendas de todos os anos dos representantes de vendas.  
  
```  
WITH Sales_CTE (SalesPersonID, NumberOfOrders)  
AS  
(  
    SELECT SalesPersonID, COUNT(*)  
    FROM Sales.SalesOrderHeader  
    WHERE SalesPersonID IS NOT NULL  
    GROUP BY SalesPersonID  
)  
SELECT AVG(NumberOfOrders) AS "Average Sales Per Person"  
FROM Sales_CTE;  
GO  
```  
  
### <a name="c-using-multiple-cte-definitions-in-a-single-query"></a>C. Usando várias definições CTE em uma única consulta  
 O exemplo a seguir mostra como definir mais de uma CTE em uma única consulta. Observe que uma vírgula é usada para separar as definições de consulta CTE. A função FORMAT, usada para exibir as quantidades monetárias em um formato de moeda, está disponível no SQL Server 2012 e posterior.  
  
```  
  
WITH Sales_CTE (SalesPersonID, TotalSales, SalesYear)  
AS  
-- Define the first CTE query.  
(  
    SELECT SalesPersonID, SUM(TotalDue) AS TotalSales, YEAR(OrderDate) AS SalesYear  
    FROM Sales.SalesOrderHeader  
    WHERE SalesPersonID IS NOT NULL  
       GROUP BY SalesPersonID, YEAR(OrderDate)  
  
)  
,   -- Use a comma to separate multiple CTE definitions.  
  
-- Define the second CTE query, which returns sales quota data by year for each sales person.  
Sales_Quota_CTE (BusinessEntityID, SalesQuota, SalesQuotaYear)  
AS  
(  
       SELECT BusinessEntityID, SUM(SalesQuota)AS SalesQuota, YEAR(QuotaDate) AS SalesQuotaYear  
       FROM Sales.SalesPersonQuotaHistory  
       GROUP BY BusinessEntityID, YEAR(QuotaDate)  
)  
  
-- Define the outer query by referencing columns from both CTEs.  
SELECT SalesPersonID  
  , SalesYear  
  , FORMAT(TotalSales,'C','en-us') AS TotalSales  
  , SalesQuotaYear  
  , FORMAT (SalesQuota,'C','en-us') AS SalesQuota  
  , FORMAT (TotalSales -SalesQuota, 'C','en-us') AS Amt_Above_or_Below_Quota  
FROM Sales_CTE  
JOIN Sales_Quota_CTE ON Sales_Quota_CTE.BusinessEntityID = Sales_CTE.SalesPersonID  
                    AND Sales_CTE.SalesYear = Sales_Quota_CTE.SalesQuotaYear  
ORDER BY SalesPersonID, SalesYear;  
GO  
  
```  
  
 Este é um conjunto de resultados parcial.  
  
```  
  
SalesPersonID SalesYear   TotalSales    SalesQuotaYear SalesQuota  Amt_Above_or_Below_Quota  
------------- ---------   -----------   -------------- ---------- ----------------------------------   
  
274           2005        $32,567.92    2005           $35,000.00  ($2,432.08)  
274           2006        $406,620.07   2006           $455,000.00 ($48,379.93)  
274           2007        $515,622.91   2007           $544,000.00 ($28,377.09)  
274           2008        $281,123.55   2008           $271,000.00  $10,123.55  
  
```  
  
### <a name="d-using-a-recursive-common-table-expression-to-display-multiple-levels-of-recursion"></a>D. Usando uma expressão de tabela comum recursiva para exibir vários níveis de recursão  
 O exemplo a seguir mostra a lista hierárquica de gerentes e os funcionários subordinados a eles. O exemplo começa criando e populando a tabela `dbo.MyEmployees`.  
  
```  
-- Create an Employee table.  
CREATE TABLE dbo.MyEmployees  
(  
EmployeeID smallint NOT NULL,  
FirstName nvarchar(30)  NOT NULL,  
LastName  nvarchar(40) NOT NULL,  
Title nvarchar(50) NOT NULL,  
DeptID smallint NOT NULL,  
ManagerID int NULL,  
 CONSTRAINT PK_EmployeeID PRIMARY KEY CLUSTERED (EmployeeID ASC)   
);  
-- Populate the table with values.  
INSERT INTO dbo.MyEmployees VALUES   
 (1, N'Ken', N'Sánchez', N'Chief Executive Officer',16,NULL)  
,(273, N'Brian', N'Welcker', N'Vice President of Sales',3,1)  
,(274, N'Stephen', N'Jiang', N'North American Sales Manager',3,273)  
,(275, N'Michael', N'Blythe', N'Sales Representative',3,274)  
,(276, N'Linda', N'Mitchell', N'Sales Representative',3,274)  
,(285, N'Syed', N'Abbas', N'Pacific Sales Manager',3,273)  
,(286, N'Lynn', N'Tsoflias', N'Sales Representative',3,285)  
,(16,  N'David',N'Bradley', N'Marketing Manager', 4, 273)  
,(23,  N'Mary', N'Gibson', N'Marketing Specialist', 4, 16);  
```  
  
```  
USE AdventureWorks2012;  
GO  
WITH DirectReports(ManagerID, EmployeeID, Title, EmployeeLevel) AS   
(  
    SELECT ManagerID, EmployeeID, Title, 0 AS EmployeeLevel  
    FROM dbo.MyEmployees   
    WHERE ManagerID IS NULL  
    UNION ALL  
    SELECT e.ManagerID, e.EmployeeID, e.Title, EmployeeLevel + 1  
    FROM dbo.MyEmployees AS e  
        INNER JOIN DirectReports AS d  
        ON e.ManagerID = d.EmployeeID   
)  
SELECT ManagerID, EmployeeID, Title, EmployeeLevel   
FROM DirectReports  
ORDER BY ManagerID;  
GO  
```  
  
### <a name="e-using-a-recursive-common-table-expression-to-display-two-levels-of-recursion"></a>E. Usando uma expressão de tabela comum recursiva para exibir dois níveis de recursão  
 O exemplo a seguir mostra os gerentes e os funcionários subordinados a eles. O número de níveis retornado está limitado a dois.  
  
```  
USE AdventureWorks2012;  
GO  
WITH DirectReports(ManagerID, EmployeeID, Title, EmployeeLevel) AS   
(  
    SELECT ManagerID, EmployeeID, Title, 0 AS EmployeeLevel  
    FROM dbo.MyEmployees   
    WHERE ManagerID IS NULL  
    UNION ALL  
    SELECT e.ManagerID, e.EmployeeID, e.Title, EmployeeLevel + 1  
    FROM dbo.MyEmployees AS e  
        INNER JOIN DirectReports AS d  
        ON e.ManagerID = d.EmployeeID   
)  
SELECT ManagerID, EmployeeID, Title, EmployeeLevel   
FROM DirectReports  
WHERE EmployeeLevel <= 2 ;  
GO  
  
```  
  
### <a name="f-using-a-recursive-common-table-expression-to-display-a-hierarchical-list"></a>F. Usando uma expressão de tabela comum recursiva para exibir uma lista hierárquica  
 O exemplo a seguir é construído com base no exemplo D com a adição dos nomes do gerente e dos funcionários, e seus cargos respectivos. A hierarquia de gerentes e funcionários é evidenciada pelo recuo de cada nível.  
  
```  
USE AdventureWorks2012;  
GO  
WITH DirectReports(Name, Title, EmployeeID, EmployeeLevel, Sort)  
AS (SELECT CONVERT(varchar(255), e.FirstName + ' ' + e.LastName),  
        e.Title,  
        e.EmployeeID,  
        1,  
        CONVERT(varchar(255), e.FirstName + ' ' + e.LastName)  
    FROM dbo.MyEmployees AS e  
    WHERE e.ManagerID IS NULL  
    UNION ALL  
    SELECT CONVERT(varchar(255), REPLICATE ('|    ' , EmployeeLevel) +  
        e.FirstName + ' ' + e.LastName),  
        e.Title,  
        e.EmployeeID,  
        EmployeeLevel + 1,  
        CONVERT (varchar(255), RTRIM(Sort) + '|    ' + FirstName + ' ' +   
                 LastName)  
    FROM dbo.MyEmployees AS e  
    JOIN DirectReports AS d ON e.ManagerID = d.EmployeeID  
    )  
SELECT EmployeeID, Name, Title, EmployeeLevel  
FROM DirectReports   
ORDER BY Sort;  
GO  
```  
  
### <a name="g-using-maxrecursion-to-cancel-a-statement"></a>G. Usando MAXRECURSION para cancelar uma instrução  
 `MAXRECURSION` pode ser usado para impedir que uma CTE recursiva malformada entre em um loop infinito. O exemplo a seguir cria um loop infinito intencionalmente e usa a dica `MAXRECURSION` para limitar o número de níveis de recursão a dois.  
  
```  
USE AdventureWorks2012;  
GO  
--Creates an infinite loop  
WITH cte (EmployeeID, ManagerID, Title) as  
(  
    SELECT EmployeeID, ManagerID, Title  
    FROM dbo.MyEmployees  
    WHERE ManagerID IS NOT NULL  
  UNION ALL  
    SELECT cte.EmployeeID, cte.ManagerID, cte.Title  
    FROM cte   
    JOIN  dbo.MyEmployees AS e   
        ON cte.ManagerID = e.EmployeeID  
)  
--Uses MAXRECURSION to limit the recursive levels to 2  
SELECT EmployeeID, ManagerID, Title  
FROM cte  
OPTION (MAXRECURSION 2);  
GO  
```  
  
 Depois que o erro de codificação for corrigido, MAXRECURSION não será mais necessário. O exemplo a seguir mostra o código corrigido.  
  
```  
USE AdventureWorks2012;  
GO  
WITH cte (EmployeeID, ManagerID, Title)  
AS  
(  
    SELECT EmployeeID, ManagerID, Title  
    FROM dbo.MyEmployees  
    WHERE ManagerID IS NOT NULL  
  UNION ALL  
    SELECT  e.EmployeeID, e.ManagerID, e.Title  
    FROM dbo.MyEmployees AS e  
    JOIN cte ON e.ManagerID = cte.EmployeeID  
)  
SELECT EmployeeID, ManagerID, Title  
FROM cte;  
GO  
```  
  
### <a name="h-using-a-common-table-expression-to-selectively-step-through-a-recursive-relationship-in-a-select-statement"></a>H. Usando uma expressão de tabela comum para percorrer seletivamente uma relação recursiva em uma instrução SELECT  
 O exemplo a seguir mostra a hierarquia de assemblies e componentes do produto necessários para montar a bicicleta para `ProductAssemblyID = 800`.  
  
```  
USE AdventureWorks2012;  
GO  
WITH Parts(AssemblyID, ComponentID, PerAssemblyQty, EndDate, ComponentLevel) AS  
(  
    SELECT b.ProductAssemblyID, b.ComponentID, b.PerAssemblyQty,  
        b.EndDate, 0 AS ComponentLevel  
    FROM Production.BillOfMaterials AS b  
    WHERE b.ProductAssemblyID = 800  
          AND b.EndDate IS NULL  
    UNION ALL  
    SELECT bom.ProductAssemblyID, bom.ComponentID, p.PerAssemblyQty,  
        bom.EndDate, ComponentLevel + 1  
    FROM Production.BillOfMaterials AS bom   
        INNER JOIN Parts AS p  
        ON bom.ProductAssemblyID = p.ComponentID  
        AND bom.EndDate IS NULL  
)  
SELECT AssemblyID, ComponentID, Name, PerAssemblyQty, EndDate,  
        ComponentLevel   
FROM Parts AS p  
    INNER JOIN Production.Product AS pr  
    ON p.ComponentID = pr.ProductID  
ORDER BY ComponentLevel, AssemblyID, ComponentID;  
GO  
```  
  
### <a name="i-using-a-recursive-cte-in-an-update-statement"></a>I. Usando uma CTE recursiva em uma instrução UPDATE  
 O exemplo a seguir atualiza o valor de `PerAssemblyQty` de todas as peças usadas para construir o produto 'Road-550-W Yellow, 44' `(ProductAssemblyID``800`). A expressão de tabela comum retorna uma lista hierárquica das peças usadas para construir o `ProductAssemblyID 800` e os componentes usados para criar essas peças, etc. Somente as linhas retornadas pela expressão de tabela comum são modificadas.  
  
```  
USE AdventureWorks2012;  
GO  
WITH Parts(AssemblyID, ComponentID, PerAssemblyQty, EndDate, ComponentLevel) AS  
(  
    SELECT b.ProductAssemblyID, b.ComponentID, b.PerAssemblyQty,  
        b.EndDate, 0 AS ComponentLevel  
    FROM Production.BillOfMaterials AS b  
    WHERE b.ProductAssemblyID = 800  
          AND b.EndDate IS NULL  
    UNION ALL  
    SELECT bom.ProductAssemblyID, bom.ComponentID, p.PerAssemblyQty,  
        bom.EndDate, ComponentLevel + 1  
    FROM Production.BillOfMaterials AS bom   
        INNER JOIN Parts AS p  
        ON bom.ProductAssemblyID = p.ComponentID  
        AND bom.EndDate IS NULL  
)  
UPDATE Production.BillOfMaterials  
SET PerAssemblyQty = c.PerAssemblyQty * 2  
FROM Production.BillOfMaterials AS c  
JOIN Parts AS d ON c.ProductAssemblyID = d.AssemblyID  
WHERE d.ComponentLevel = 0;  
```  
  
### <a name="j-using-multiple-anchor-and-recursive-members"></a>J. Usando vários membros de ancoragem e recursivos  
 O exemplo a seguir usa vários membros de ancoragem e recursivos para retornar todos os ancestrais de uma pessoa especificada. Uma tabela é criada e valores inseridos para estabelecer a genealogia familiar retornada pela CTE recursiva.  
  
```  
-- Genealogy table  
IF OBJECT_ID('dbo.Person','U') IS NOT NULL DROP TABLE dbo.Person;  
GO  
CREATE TABLE dbo.Person(ID int, Name varchar(30), Mother int, Father int);  
GO  
INSERT dbo.Person   
VALUES(1, 'Sue', NULL, NULL)  
      ,(2, 'Ed', NULL, NULL)  
      ,(3, 'Emma', 1, 2)  
      ,(4, 'Jack', 1, 2)  
      ,(5, 'Jane', NULL, NULL)  
      ,(6, 'Bonnie', 5, 4)  
      ,(7, 'Bill', 5, 4);  
GO  
-- Create the recursive CTE to find all of Bonnie's ancestors.  
WITH Generation (ID) AS  
(  
-- First anchor member returns Bonnie's mother.  
    SELECT Mother   
    FROM dbo.Person  
    WHERE Name = 'Bonnie'  
UNION  
-- Second anchor member returns Bonnie's father.  
    SELECT Father   
    FROM dbo.Person  
    WHERE Name = 'Bonnie'  
UNION ALL  
-- First recursive member returns male ancestors of the previous generation.  
    SELECT Person.Father  
    FROM Generation, Person  
    WHERE Generation.ID=Person.ID  
UNION ALL  
-- Second recursive member returns female ancestors of the previous generation.  
    SELECT Person.Mother  
    FROM Generation, dbo.Person  
    WHERE Generation.ID=Person.ID  
)  
SELECT Person.ID, Person.Name, Person.Mother, Person.Father  
FROM Generation, dbo.Person  
WHERE Generation.ID = Person.ID;  
GO  
```  
  
###  <a name="bkmkUsingAnalyticalFunctionsInARecursiveCTE"></a> K. Usando funções analíticas em uma CTE recursiva  
 O exemplo a seguir mostra uma armadilha que pode ocorrer ao usar uma função analítica ou de agregação na parte recursiva de uma CTE.  
  
```  
DECLARE @t1 TABLE (itmID int, itmIDComp int);  
INSERT @t1 VALUES (1,10), (2,10);   
  
DECLARE @t2 TABLE (itmID int, itmIDComp int);   
INSERT @t2 VALUES (3,10), (4,10);   
  
WITH vw AS  
 (  
    SELECT itmIDComp, itmID  
    FROM @t1  
  
    UNION ALL  
  
    SELECT itmIDComp, itmID  
    FROM @t2  
)   
,r AS  
 (  
    SELECT t.itmID AS itmIDComp  
           , NULL AS itmID  
           ,CAST(0 AS bigint) AS N  
           ,1 AS Lvl  
    FROM (SELECT 1 UNION ALL SELECT 2 UNION ALL SELECT 3 UNION ALL SELECT 4) AS t (itmID)   
  
UNION ALL  
  
SELECT t.itmIDComp  
    , t.itmID  
    , ROW_NUMBER() OVER(PARTITION BY t.itmIDComp ORDER BY t.itmIDComp, t.itmID) AS N  
    , Lvl + 1  
FROM r   
    JOIN vw AS t ON t.itmID = r.itmIDComp  
)   
  
SELECT Lvl, N FROM r;  
```  
  
 Os resultados a seguir são os esperados da consulta.  
  
```  
Lvl  N  
1    0  
1    0  
1    0  
1    0  
2    4  
2    3  
2    2  
2    1  
```  
  
 Os resultados a seguir são os resultados reais da consulta.  
  
```  
Lvl  N  
1    0  
1    0  
1    0  
1    0  
2    1  
2    1  
2    1  
2    1  
```  
  
 `N` retorna 1 para cada passagem da parte recursiva da CTE porque apenas o subconjunto de dados daquele nível de recursão é transmitido para `ROWNUMBER`. Para cada uma das iterações da parte recursiva da consulta, apenas uma linha é transmitida para `ROWNUMBER`.  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="l-using-a-common-table-expression-within-a-ctas-statement"></a>L. Usando uma expressão de tabela comum dentro de uma instrução CTAS  
 O exemplo a seguir cria uma nova tabela que contém o número total de ordens de venda por ano para cada representante de vendas no [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)].  
  
```  
-- Uses AdventureWorks  
  
CREATE TABLE SalesOrdersPerYear  
WITH  
(  
    DISTRIBUTION = HASH(SalesPersonID)  
)  
AS  
    -- Define the CTE expression name and column list.  
    WITH Sales_CTE (SalesPersonID, SalesOrderID, SalesYear)  
    AS  
    -- Define the CTE query.  
    (  
        SELECT SalesPersonID, SalesOrderID, YEAR(OrderDate) AS SalesYear  
        FROM Sales.SalesOrderHeader  
        WHERE SalesPersonID IS NOT NULL  
    )  
    -- Define the outer query referencing the CTE name.  
    SELECT SalesPersonID, COUNT(SalesOrderID) AS TotalSales, SalesYear  
    FROM Sales_CTE  
    GROUP BY SalesYear, SalesPersonID  
    ORDER BY SalesPersonID, SalesYear;  
GO  
```  
  
### <a name="m-using-a-common-table-expression-within-a-cetas-statement"></a>M. Usando uma expressão de tabela comum dentro de uma instrução CETAS  
 O exemplo a seguir cria uma nova tabela externa que contém o número total de ordens de venda por ano para cada representante de vendas no [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)].  
  
```  
-- Uses AdventureWorks  
  
CREATE EXTERNAL TABLE SalesOrdersPerYear  
WITH  
(  
    LOCATION = 'hdfs://xxx.xxx.xxx.xxx:5000/files/Customer',  
    FORMAT_OPTIONS ( FIELD_TERMINATOR = '|' )   
)  
AS  
    -- Define the CTE expression name and column list.  
    WITH Sales_CTE (SalesPersonID, SalesOrderID, SalesYear)  
    AS  
    -- Define the CTE query.  
    (  
        SELECT SalesPersonID, SalesOrderID, YEAR(OrderDate) AS SalesYear  
        FROM Sales.SalesOrderHeader  
        WHERE SalesPersonID IS NOT NULL  
    )  
    -- Define the outer query referencing the CTE name.  
    SELECT SalesPersonID, COUNT(SalesOrderID) AS TotalSales, SalesYear  
    FROM Sales_CTE  
    GROUP BY SalesYear, SalesPersonID  
    ORDER BY SalesPersonID, SalesYear;  
GO  
```  
  
### <a name="n-using-multiple-comma-separated-ctes-in-a-statement"></a>N. Usando várias CTEs separadas por vírgula em uma instrução  
 O exemplo a seguir demonstra como incluir duas CTEs em uma única instrução. As CTEs não podem ser aninhadas (sem recursão).  
  
```  
WITH   
 CountDate (TotalCount, TableName) AS  
    (  
     SELECT COUNT(datekey), 'DimDate' FROM DimDate  
    ) ,  
 CountCustomer (TotalAvg, TableName) AS  
    (  
     SELECT COUNT(CustomerKey), 'DimCustomer' FROM DimCustomer  
    )  
SELECT TableName, TotalCount FROM CountDate  
UNION ALL  
SELECT TableName, TotalAvg FROM CountCustomer;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [EXCEPT e INTERSECT &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-operators-except-and-intersect-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  
  
  
