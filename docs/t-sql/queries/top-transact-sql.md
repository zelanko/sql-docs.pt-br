---
description: TOP (Transact-SQL)
title: TOP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TOP_TSQL
- TOP
dev_langs:
- TSQL
helpviewer_keywords:
- TOP clause
- first set of query result rows [SQL Server]
- TOP clause, about TOP clause
- queries [SQL Server], results
ms.assetid: da983c0a-06c5-4cf8-a6a4-7f9d66f34f2c
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 295e21500b51bed644807c2cbbab03515fb7e7d9
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97483998"
---
# <a name="top-transact-sql"></a>TOP (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Limita as linhas retornadas em um conjunto de resultados de consulta a um número ou percentual de linhas no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Quando você usa TOP com a cláusula ORDER BY, o conjunto de resultados é limitado ao primeiro número *N* de linhas ordenadas. Caso contrário, TOP retorna o primeiro número *N* de linhas em uma ordem indefinida. Use esta cláusula para especificar o número de linhas retornadas de uma instrução SELECT. Ou então, use TOP para especificar as linhas afetadas por uma instrução INSERT, UPDATE, MERGE ou DELETE.  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
 
 A seguir, é possível ver a sintaxe do SQL Server e do Banco de Dados SQL do Azure:

```syntaxsql  
[   
    TOP (expression) [PERCENT]  
    [ WITH TIES ]  
]  
```  

A seguir, é possível ver a sintaxe do [!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)] e do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]:

```syntaxsql  
[   
    TOP ( expression )   
    [ WITH TIES ]  
]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
*expressão*  
A expressão numérica que especifica o número de linhas a serem retornadas. *expression* será convertido implicitamente em um **float** se você especificar PERCENT. Caso contrário, *expression* é convertido em **bigint**.  
  
PERCENT  
Indica que a consulta retorna apenas a primeira porcentagem de linhas da *expression* do conjunto de resultados. Os valores fracionários são arredondados até o próximo valor inteiro.  
  
WITH TIES  
Retorna duas ou mais linhas associadas ao último lugar do conjunto de resultados limitado. Você deve usar esse argumento com a cláusula **ORDER BY**. **WITH TIES** pode fazer com que mais linhas sejam retornadas do que o valor especificado em *expression*. Por exemplo, se *expression* for definido como 5, mas duas linhas adicionais corresponderem aos valores das colunas **ORDER BY** na linha 5, o conjunto de resultados conterá sete linhas.  
  
Você poderá especificar a cláusula TOP com o argumento WITH TIES somente em instruções SELECT e somente se você também tiver especificado a cláusula ORDER BY. A ordem retornada de registros vinculados é arbitrária. ORDER BY não afeta essa regra.  
  
## <a name="best-practices"></a>Práticas Recomendadas  
Em uma instrução SELECT, sempre use uma cláusula ORDER BY com a cláusula TOP. Porque essa é a única forma de indicar de maneira previsível as linhas que são afetadas por TOP.  
  
Use OFFSET e FETCH na cláusula ORDER BY em vez da cláusula TOP implementar uma solução de paginação de consulta. Uma solução de página (ou seja, enviar partes ou "páginas" de dados ao cliente) é mais fácil de implementar com as cláusulas OFFSET e FETCH. Para obter mais informações, consulte [Cláusula ORDER BY &#40;Transact-SQL&#41;](../../t-sql/queries/select-order-by-clause-transact-sql.md).  
  
Use TOP (ou OFFSET e FETCH) em vez de SET ROWCOUNT para limitar o número de linhas retornadas. Esses métodos são preferenciais em relação ao uso de SET ROWCOUNT pelos seguintes motivos:  
  
-   Como parte de uma instrução SELECT, o otimizador de consultas pode considerar o valor da *expression* nas cláusulas TOP ou FETCH durante a otimização de consultas. Como SET ROWCOUNT é usada fora de uma instrução que executa uma consulta, seu valor não pode ser considerado em um plano de consulta.  
  
## <a name="compatibility-support"></a>Suporte de compatibilidade  
Para compatibilidade com versões anteriores, os parênteses são opcionais em instruções SELECT. É recomendável que você sempre use parênteses para TOP em instruções SELECT. Isso proporciona consistência com seu uso obrigatório em instruções INSERT, UPDATE, MERGE e DELETE. 
  
## <a name="interoperability"></a>Interoperabilidade  
A expressão TOP não afeta instruções que possam ser executadas devido a um gatilho. As tabelas **inserted** e **deleted** nos gatilhos retornam somente as linhas que realmente forem afetadas pelas instruções INSERT, UPDATE, MERGE ou DELETE. Por exemplo, se um INSERT TRIGGER for acionado como resultado de uma instrução INSERT que usou uma cláusula TOP.  
  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite a atualização de linhas através de exibições. Como a cláusula TOP pode ser incluída na definição de exibição, algumas linhas poderão desaparecer da exibição se as linhas deixarem de atender aos requisitos da expressão TOP devido a uma atualização.  
  
Quando especificado na instrução MERGE, a cláusula TOP é aplicável *depois de* a tabela de origem inteira e a tabela de destino inteira serem unidas. E as linhas unidas que não se qualificam para uma ação de inserção, atualização ou exclusão são removidas. A cláusula TOP ainda reduz o número de linhas unidas para o valor especificado e as ações de inserção, atualização ou exclusão são aplicadas às linhas unidas restantes de uma forma não ordenada. Ou seja, não há ordem na qual as linhas são distribuídas entre as ações definidas nas cláusulas WHEN. Por exemplo, se a especificação de TOP (10) afeta 10 linhas, dessas linhas, sete podem ser atualizadas e três inseridas. Ou, uma pode ser excluída, cinco atualizadas e quatro inseridas e assim por diante. Como a instrução MERGE executa uma verificação completa das tabelas de origem e de destino, o desempenho de E/S pode ser afetado ao usar a cláusula TOP para modificar uma tabela grande criando vários lotes. Nesse cenário, é importante garantir que todos os lotes sucessivos se destinem a novas linhas.  
  
Tenha cautela ao especificar a cláusula TOP em uma consulta que contenha um operador UNION, UNION ALL, EXCEPT ou INTERSECT. É possível gravar uma consulta que retorne resultados inesperados, pois a ordem na qual as cláusulas TOP e ORDER BY são logicamente processadas nem sempre é intuitiva quando esses operadores são usados em uma operação de seleção. Por exemplo, a partir da tabela e dos dados a seguir, suponha que você queira retornar o carro vermelho e o carro azul mais baratos. Isto é, o automóvel vermelho e a van azul.  
  
```sql  
CREATE TABLE dbo.Cars(Model VARCHAR(15), Price MONEY, Color VARCHAR(10));  
INSERT dbo.Cars VALUES  
    ('sedan', 10000, 'red'), ('convertible', 15000, 'blue'),   
    ('coupe', 20000, 'red'), ('van', 8000, 'blue');  
```  
  
Para obter esses resultados, você poderia gravar a consulta a seguir.  
  
```sql  
SELECT TOP(1) Model, Color, Price  
FROM dbo.Cars  
WHERE Color = 'red'  
UNION ALL  
SELECT TOP(1) Model, Color, Price  
FROM dbo.Cars  
WHERE Color = 'blue'  
ORDER BY Price ASC;  
GO    
```  
  
O conjunto de resultados é o seguinte.  
  
 ```
 Model         Color      Price  
 ------------- ---------- -------  
 sedan         red        10000.00  
 convertible   blue       15000.00
 ```  
  
Os resultados inesperados são retornados porque a cláusula TOP é executada logicamente antes da cláusula ORDER BY, que classifica os resultados do operador (UNION ALL, neste caso). Assim, a consulta anterior retorna qualquer carro vermelho e qualquer carro azul e, em seguida, ordena o resultado dessa união pelo preço. O exemplo a seguir mostra o método correto de gravar essa consulta para obter o resultado desejado.  
  
```sql  
SELECT Model, Color, Price  
FROM (SELECT TOP(1) Model, Color, Price  
      FROM dbo.Cars  
      WHERE Color = 'red'  
      ORDER BY Price ASC) AS a  
UNION ALL  
SELECT Model, Color, Price  
FROM (SELECT TOP(1) Model, Color, Price  
      FROM dbo.Cars  
      WHERE Color = 'blue'  
      ORDER BY Price ASC) AS b;  
GO    
```  
  
Usando TOP e ORDER BY em uma operação de subseleção, você assegura que os resultados da cláusula ORDER BY sejam aplicados à cláusula TOP e não à classificação do resultado da operação UNION.  
  
 Este é o conjunto de resultados.  
  
 ```
 Model         Color      Price  
 ------------- ---------- -------  
 sedan         red        10000.00  
 van           blue        8000.00
 ```  
  
## <a name="limitations-and-restrictions"></a>Limitações e Restrições  
Quando você usa TOP com INSERT, UPDATE, MERGE ou DELETE, as linhas referenciadas não são organizadas em qualquer ordem. E não é possível especificar a cláusula ORDER BY nessas instruções. Se você precisar usar TOP para inserir, excluir ou modificar linhas em uma ordem cronológica significativa, use TOP junto com uma cláusula ORDER BY especificada em uma instrução de subseleção. Consulte a seção Exemplos a seguir neste artigo.  
  
TOP não pode ser usado em instruções UPDATE e DELETE em exibições particionadas.  
  
Não é possível combinar TOP com OFFSET e FETCH na mesma expressão de consulta (no mesmo escopo de consulta). Para obter mais informações, consulte [Cláusula ORDER BY &#40;Transact-SQL&#41;](../../t-sql/queries/select-order-by-clause-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
  
|Categoria|Elementos de sintaxe em destaque|  
|--------------|------------------------------|  
|[Sintaxe básica](#BasicSyntax)|TOP • PERCENT|  
|[Incluindo valores de empate](#tie)|WITH TIES|  
|[Limitando as linhas afetadas por DELETE, INSERT ou UPDATE](#DML)|DELETE • INSERT • UPDATE|  
  
###  <a name="basic-syntax"></a><a name="BasicSyntax"></a> Sintaxe básica  
Os exemplos nesta seção demonstram a funcionalidade básica da cláusula ORDER BY usando a sintaxe mínima necessária.  
  
#### <a name="a-using-top-with-a-constant-value"></a>a. Usando TOP com um valor constante  
Os exemplos a seguir usam um valor constante para especificar o número de funcionários que são retornados no conjunto de resultados da consulta. No primeiro exemplo, as primeiras 10 linhas indefinidas são retornadas porque uma cláusula ORDER BY não é usada. No segundo exemplo, uma cláusula ORDER BY é usada para retornar os 10 funcionários contratados mais recentemente.  
  
```sql  
USE AdventureWorks2012;  
GO  
-- Select the first 10 random employees.  
SELECT TOP(10)JobTitle, HireDate  
FROM HumanResources.Employee;  
GO  
-- Select the first 10 employees hired most recently.  
SELECT TOP(10)JobTitle, HireDate  
FROM HumanResources.Employee  
ORDER BY HireDate DESC;  
GO  
```  
  
#### <a name="b-using-top-with-a-variable"></a>B. Usando TOP com uma variável  
O exemplo a seguir usa uma variável para especificar o número de funcionários que são retornados no conjunto de resultados da consulta.  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @p AS INT = 10;  
SELECT TOP(@p)JobTitle, HireDate, VacationHours  
FROM HumanResources.Employee  
ORDER BY VacationHours DESC;  
GO  
```  
  
#### <a name="c-specifying-a-percentage"></a>C. Especificando uma porcentagem  
O exemplo a seguir usa PERCENT para especificar o número de funcionários que são retornados no conjunto de resultados da consulta. Há 290 funcionários na tabela `HumanResources.Employee`. Como cinco por cento de 290 é um valor fracionário, o valor é arredondado para o próximo número inteiro.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT TOP(5)PERCENT JobTitle, HireDate  
FROM HumanResources.Employee  
ORDER BY HireDate DESC;  
GO    
```  
  
###  <a name="including-tie-values"></a><a name="tie"></a> Incluindo valores de empate  
  
#### <a name="a-using-with-ties-to-include-rows-that-match-the-values-in-the-last-row"></a>a. Usando WITH TIES para incluir linhas que correspondam aos valores da última linha  
O exemplo a seguir obtém os primeiros `10` por cento de todos os funcionários com o salário mais alto e os retorna em ordem descendente, de acordo com seu salário. Especificar `WITH TIES` assegura que todos os funcionários que recebem salários iguais ao salário mais baixo retornado (a última linha) também serão incluídos no conjunto de resultados, mesmo que isso exceda `10` por cento dos funcionários.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT TOP(10) PERCENT WITH TIES  
pp.FirstName, pp.LastName, e.JobTitle, e.Gender, r.Rate  
FROM Person.Person AS pp   
    INNER JOIN HumanResources.Employee AS e  
        ON pp.BusinessEntityID = e.BusinessEntityID  
    INNER JOIN HumanResources.EmployeePayHistory AS r  
        ON r.BusinessEntityID = e.BusinessEntityID  
ORDER BY Rate DESC;  
GO    
```  
  
###  <a name="limiting-the-rows-affected-by-delete-insert-or-update"></a><a name="DML"></a> Limitando as linhas afetadas por DELETE, INSERT ou UPDATE  
  
#### <a name="a-using-top-to-limit-the-number-of-rows-deleted"></a>a. Usando TOP para limitar o número de linhas excluídas  
Quando uma cláusula TOP (*n*) é usada com DELETE, a operação de exclusão é executada em uma seleção indefinida de um número *n* de linhas. Ou seja, a instrução DELETE escolhe qualquer número (*n*) de linhas que atendem aos critérios definidos na cláusula WHERE. O exemplo a seguir exclui `20` linhas da tabela `PurchaseOrderDetail` que têm datas de conclusão anteriores a 1º de julho de 2002.  
  
```sql  
USE AdventureWorks2012;  
GO  
DELETE TOP (20)   
FROM Purchasing.PurchaseOrderDetail  
WHERE DueDate < '20020701';  
GO  
```  
  
Se quiser usar TOP para excluir linhas em uma ordem cronológica significativa, será preciso usar TOP com ORDER BY em uma instrução de subseleção. A consulta a seguir exclui as 10 linhas da tabela `PurchaseOrderDetail` que têm as primeiras datas de vencimento. Para garantir que apenas 10 linhas sejam excluídas, a coluna especificada na instrução de subseleção (`PurchaseOrderID`) é a chave primária da tabela. O uso de uma coluna não chave na instrução de subseleção pode resultar na exclusão de mais de 10 linhas se a coluna especificada contiver valores duplicados.  
  
```sql  
USE AdventureWorks2012;  
GO  
DELETE FROM Purchasing.PurchaseOrderDetail  
WHERE PurchaseOrderDetailID IN  
   (SELECT TOP 10 PurchaseOrderDetailID   
    FROM Purchasing.PurchaseOrderDetail   
    ORDER BY DueDate ASC);  
GO  
```  
  
#### <a name="b-using-top-to-limit-the-number-of-rows-inserted"></a>B. Usando TOP para limitar o número de linhas inseridas  
O exemplo a seguir cria a tabela `EmployeeSales` e insere nela o nome e os dados de vendas desde o início do ano dos cinco funcionários principais da tabela `HumanResources.Employee`. A instrução INSERT escolhe cinco linhas retornadas pela instrução `SELECT` que atendam aos critérios definidos na cláusula WHERE. A cláusula OUTPUT exibe as linhas inseridas na tabela `EmployeeSales`. Observe que a cláusula ORDER BY na instrução SELECT não é usada para determinar os cinco funcionários principais.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
IF OBJECT_ID ('dbo.EmployeeSales', 'U') IS NOT NULL  
    DROP TABLE dbo.EmployeeSales;  
GO  
CREATE TABLE dbo.EmployeeSales  
( EmployeeID   NVARCHAR(11) NOT NULL,  
  LastName     NVARCHAR(20) NOT NULL,  
  FirstName    NVARCHAR(20) NOT NULL,  
  YearlySales  MONEY NOT NULL  
 );  
GO  
INSERT TOP(5)INTO dbo.EmployeeSales  
    OUTPUT inserted.EmployeeID, inserted.FirstName, inserted.LastName, inserted.YearlySales  
    SELECT sp.BusinessEntityID, c.LastName, c.FirstName, sp.SalesYTD   
    FROM Sales.SalesPerson AS sp  
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.SalesYTD > 250000.00  
    ORDER BY sp.SalesYTD DESC;  
GO    
```  
  
Se quiser usar TOP para inserir linhas em uma ordem cronológica significativa, será preciso usar TOP com ORDER BY em uma instrução de subseleção. O exemplo a seguir mostra como fazer isso. A cláusula OUTPUT exibe as linhas inseridas na tabela `EmployeeSales`. Observe que os cinco funcionários principais agora são inseridos com base nos resultados da cláusula ORDER BY, em vez de linhas indefinidas.  
  
```sql  
INSERT INTO dbo.EmployeeSales  
    OUTPUT inserted.EmployeeID, inserted.FirstName, inserted.LastName, inserted.YearlySales  
    SELECT TOP (5) sp.BusinessEntityID, c.LastName, c.FirstName, sp.SalesYTD   
    FROM Sales.SalesPerson AS sp  
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.SalesYTD > 250000.00  
    ORDER BY sp.SalesYTD DESC;  
GO    
```  
  
#### <a name="c-using-top-to-limit-the-number-of-rows-updated"></a>C. Usando TOP para limitar o número de linhas atualizadas  
O exemplo a seguir usa a cláusula TOP para atualizar linhas em uma tabela. Quando uma cláusula TOP (*n*) é usada com UPDATE, a operação de atualização é executada em um número indefinido de linhas. Ou seja, a instrução UPDATE escolhe qualquer número (*n*) de linhas que atendem aos critérios definidos na cláusula WHERE. O exemplo a seguir atribui 10 clientes de um vendedor para outro.  
  
```sql  
USE AdventureWorks2012;  
UPDATE TOP (10) Sales.Store  
SET SalesPersonID = 276  
WHERE SalesPersonID = 275;  
GO  
```  
  
Caso seja necessário usar a cláusula TOP para aplicar atualizações em uma ordem cronológica significativa, será preciso usar TOP junto com ORDER BY em uma instrução de subseleção. O exemplo a seguir atualiza as horas de férias dos 10 funcionários com as datas de contratação mais antigas.  
  
```sql  
UPDATE HumanResources.Employee  
SET VacationHours = VacationHours + 8  
FROM (SELECT TOP 10 BusinessEntityID FROM HumanResources.Employee  
     ORDER BY HireDate ASC) AS th  
WHERE HumanResources.Employee.BusinessEntityID = th.BusinessEntityID;  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
O exemplo a seguir retorna as primeiras 31 linhas que correspondem aos critérios de consulta. A cláusula **ORDER BY** garante que as 31 linhas retornadas sejam as primeiras 31 linhas com base em uma ordem alfabética da coluna `LastName`.  
  
Usando **TOP** sem especificar empates.  
  
```sql  
SELECT TOP (31) FirstName, LastName   
FROM DimEmployee ORDER BY LastName;  
```  
  
Resultado: 31 linhas são retornadas.  
  
Usando TOP, especificando WITH TIES.  
  
```sql  
SELECT TOP (31) WITH TIES FirstName, LastName   
FROM DimEmployee ORDER BY LastName;  
```  
  
Resultado: 33 linhas são retornadas, porque três funcionários chamados Brown empatam na linha 31.  
  
## <a name="see-also"></a>Consulte Também  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [ORDER BY Clause &#40;Transact-SQL&#41;](../../t-sql/queries/select-order-by-clause-transact-sql.md)   
 [SET ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/statements/set-rowcount-transact-sql.md)   
 [MERGE &#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)  
  
 
