---
title: Construtor de valor de tabela (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- inserting multiple rows
- row value expression
- row constructor [SQL Server]
- table value constructor [SQL Server]
ms.assetid: e57cd31d-140e-422f-8178-2761c27b9deb
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: b12ad1dcc054f7c59f52b3aee23d5d6368f1459b
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67948254"
---
# <a name="table-value-constructor-transact-sql"></a>Construtor de valor de tabela (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Especifica um conjunto de expressões de valores de linha a ser construído em uma tabela. O construtor de valor de tabela [!INCLUDE[tsql](../../includes/tsql-md.md)] permite especificar várias linhas de dados em uma única instrução DML. O construtor de valor de tabela pode ser especificado como a cláusula VALUES de uma instrução INSERT ... VALUES ou como uma tabela derivada na cláusula USING da instrução MERGE ou na cláusula FROM.
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
VALUES ( <row value expression list> ) [ ,...n ]   
  
<row value expression list> ::=  
    {<row value expression> } [ ,...n ]  
  
<row value expression> ::=  
    { DEFAULT | NULL | expression }  
```  
  
## <a name="arguments"></a>Argumentos  
 VALUES  
 Introduz as listas de expressões de valores de linha. Cada lista deve ser colocada entre parênteses e separada por uma vírgula.  
  
 O número de valores especificados em cada lista deve ser o mesmo e os valores devem estar na mesma ordem das colunas na tabela. É necessário especificar um valor para cada coluna na tabela ou a lista de colunas deve especificar explicitamente as colunas para cada valor de entrada.  
  
 DEFAULT  
 Força o [!INCLUDE[ssDE](../../includes/ssde-md.md)] a inserir o valor padrão definido para uma coluna. Se não existir um padrão para a coluna e a coluna aceitar valores nulos, NULL será inserido. DEFAULT não é válido para uma coluna de identidade. Quando especificado em um construtor de valor de tabela, DEFAULT só é permitido em uma instrução INSERT.  
  
 *expressão*  
 É uma constante, uma variável ou uma expressão. A expressão não pode conter uma instrução EXECUTE.  
  
## <a name="limitations-and-restrictions"></a>Limitações e Restrições  
 Quando usado como uma tabela derivada, não há nenhum limite no número de linhas.  
 
 Quando usado como a cláusula VALUES de uma instrução INSERT ... VALUES, há um limite de 1.000 linhas. O erro 10738 será retornado se o número de linhas exceder o máximo. Para inserir mais de 1000 linhas, use um dos métodos a seguir:  
  
- Crie várias instruções INSERT  
  
- Use uma tabela derivada  
  
- Importe os dados em massa usando o [utilitário **bcp**](../../tools/bcp-utility.md), a [classe SqlBulkCopy](/dotnet/api/system.data.sqlclient.sqlbulkcopy) do .NET, a instrução [OPENROWSET (BULK ...)](../../t-sql/functions/openrowset-transact-sql.md) ou [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)  
  
 Somente são permitidos valores escalares exclusivos como uma expressão de valor de linha. Uma subconsulta que envolve várias colunas não é permitida como uma expressão de valor de linha. Por exemplo, o código a seguir resulta em um erro de sintaxe porque a terceira lista de expressões de valores de linha contém uma subconsulta com várias colunas.  
  
```sql
USE AdventureWorks2012;  
GO  
CREATE TABLE dbo.MyProducts (Name varchar(50), ListPrice money);  
GO  
-- This statement fails because the third values list contains multiple columns in the subquery.  
INSERT INTO dbo.MyProducts (Name, ListPrice)  
VALUES ('Helmet', 25.50),  
       ('Wheel', 30.00),  
       (SELECT Name, ListPrice FROM Production.Product WHERE ProductID = 720);  
GO  
```  
  
 Entretanto, a instrução pode ser reescrita especificando cada coluna separadamente na subconsulta. O exemplo a seguir insere com êxito três linhas na tabela `MyProducts`.  
  
```sql
INSERT INTO dbo.MyProducts (Name, ListPrice)  
VALUES ('Helmet', 25.50),  
       ('Wheel', 30.00),  
       ((SELECT Name FROM Production.Product WHERE ProductID = 720),  
        (SELECT ListPrice FROM Production.Product WHERE ProductID = 720));  
GO  
```  
  
## <a name="data-types"></a>Tipos de dados  
 Os valores especificados em uma instrução INSERT de várias linhas seguem as propriedades de conversão de tipos de dados da sintaxe UNION ALL. Isso resulta na conversão implícita de tipos não correspondentes no tipo de [precedência](../../t-sql/data-types/data-type-precedence-transact-sql.md) mais alta. Se a conversão não for uma conversão implícita com suporte, um erro será retornado. Por exemplo, a instrução a seguir insere um valor inteiro e um valor de caractere em uma coluna do tipo **char**.  
  
```sql
CREATE TABLE dbo.t (a int, b char);  
GO  
INSERT INTO dbo.t VALUES (1,'a'), (2, 1);  
GO  
```  
  
 Quando a instrução INSERT for executada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tentará converter 'a' em um inteiro porque a precedência de tipo de dados indica que um inteiro é de um tipo mais alto do que um caractere. A conversão falhará e um erro será retornado. Para evitar o erro, converta explicitamente os valores conforme apropriado. Por exemplo, a instrução anterior pode ser escrita da seguinte maneira.  
  
```sql
INSERT INTO dbo.t VALUES (1,'a'), (2, CONVERT(CHAR,1));  
```  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-inserting-multiple-rows-of-data"></a>a. Inserindo várias linhas de dados  
 O exemplo a seguir cria a tabela `dbo.Departments` e usa o construtor de valor de tabela para inserir cinco linhas na tabela. Como os valores de todas as colunas são fornecidos e listados na mesma ordem que as colunas da tabela, os nomes das colunas não precisam ser especificados na lista de colunas.  
  
```sql
USE AdventureWorks2012;  
GO  
INSERT INTO Production.UnitMeasure  
VALUES (N'FT2', N'Square Feet ', '20080923'), (N'Y', N'Yards', '20080923'),
       (N'Y3', N'Cubic Yards', '20080923');  
GO  
```  
  
### <a name="b-inserting-multiple-rows-with-default-and-null-values"></a>B. Inserindo várias linhas com valores DEFAULT e NULL  
 O exemplo a seguir demonstra como especificar DEFAULT e NULL ao usar o construtor de valor de tabela para inserir linhas em uma tabela.  
  
```sql
USE AdventureWorks2012;  
GO  
CREATE TABLE Sales.MySalesReason(  
SalesReasonID int IDENTITY(1,1) NOT NULL,  
Name dbo.Name NULL ,  
ReasonType dbo.Name NOT NULL DEFAULT 'Not Applicable' );  
GO  
INSERT INTO Sales.MySalesReason   
VALUES ('Recommendation','Other'), ('Advertisement', DEFAULT), (NULL, 'Promotion');  
  
SELECT * FROM Sales.MySalesReason;  
```  
  
### <a name="c-specifying-multiple-values-as-a-derived-table-in-a-from-clause"></a>C. Especificando vários valores como uma tabela derivada em uma cláusula FROM  
 Os exemplos a seguir usam o construtor de valor de tabela para especificar vários valores na cláusula FROM de uma instrução SELECT.  
  
```sql
SELECT a, b FROM (VALUES (1, 2), (3, 4), (5, 6), (7, 8), (9, 10) ) AS MyTable(a, b);  
GO  
-- Used in an inner join to specify values to return.  
SELECT ProductID, a.Name, Color  
FROM Production.Product AS a  
INNER JOIN (VALUES ('Blade'), ('Crown Race'), ('AWC Logo Cap')) AS b(Name)   
ON a.Name = b.Name;  
```  
  
### <a name="d-specifying-multiple-values-as-a-derived-source-table-in-a-merge-statement"></a>D. Especificando vários valores como uma tabela de origem derivada em uma instrução MERGE  
 O exemplo a seguir usa MERGE para modificar a tabela `SalesReason` atualizando ou inserindo linhas. Quando o valor de `NewName` na tabela de origem corresponde a um valor na coluna `Name` da tabela de destino (`SalesReason`), a coluna `ReasonType` é atualizada na tabela de destino. Quando o valor de `NewName` não corresponde, a linha de origem é inserida na tabela de destino. A tabela de origem é uma tabela derivada que usa o construtor de valor de tabela do [!INCLUDE[tsql](../../includes/tsql-md.md)] para especificar várias linhas para a tabela de origem.  
  
```sql
USE AdventureWorks2012;  
GO  
-- Create a temporary table variable to hold the output actions.  
DECLARE @SummaryOfChanges TABLE(Change VARCHAR(20));  
  
MERGE INTO Sales.SalesReason AS Target  
USING (VALUES ('Recommendation','Other'), ('Review', 'Marketing'), ('Internet', 'Promotion'))  
       AS Source (NewName, NewReasonType)  
ON Target.Name = Source.NewName  
WHEN MATCHED THEN  
UPDATE SET ReasonType = Source.NewReasonType  
WHEN NOT MATCHED BY TARGET THEN  
INSERT (Name, ReasonType) VALUES (NewName, NewReasonType)  
OUTPUT $action INTO @SummaryOfChanges;  
  
-- Query the results of the table variable.  
SELECT Change, COUNT(*) AS CountPerChange  
FROM @SummaryOfChanges  
GROUP BY Change;  
```  
  
### <a name="e-inserting-more-than-1000-rows"></a>E. Como inserir mais de 1.000 linhas
  O exemplo a seguir demonstra como usar o construtor de valor de tabela como uma tabela derivada. Isso permite a inserção de mais de 1.000 linhas de um único construtor de valor de tabela.
  
```sql
CREATE TABLE dbo.Test ([Value] int);  
  
INSERT INTO dbo.Test ([Value])  
  SELECT drvd.[NewVal]
  FROM   (VALUES (0), (1), (2), (3), ..., (5000)) drvd([NewVal]);
```  


## <a name="see-also"></a>Consulte Também  
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [MERGE &#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)  
  
  
