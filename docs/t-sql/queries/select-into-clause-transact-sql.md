---
title: "NA cláusula (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 05/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- INTO_TSQL
- INSERT_INTO_TSQL
- INSERT INTO
- INTO
- INTO clause
- INTO_clause_TSQL
dev_langs: TSQL
helpviewer_keywords:
- copying data [SQL Server], into a new table
- INTO clause
- moving data, to a new table
- table creation [SQL Server], INTO clause
- SELECT INTO statement
- inserting rows
- clauses [SQL Server], INTO
- row additions [SQL Server], INTO clause
ms.assetid: b48d69e8-5a00-48bf-b2f3-19278a72dd88
caps.latest.revision: "63"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 5501732e0551a1142ea5bf1a8bc48122aaff6a25
ms.sourcegitcommit: 5763d63a3c455ec8743b75c057a2254a96a1d4fe
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2018
---
# <a name="select---into-clause-transact-sql"></a>-Cláusula SELECT INTO (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  SELECT…INTO cria uma tabela nova no grupo de arquivos padrão e insere nela as linhas resultantes da consulta. Para exibir a sintaxe completa de SELECT, consulte [SELECT &#40; Transact-SQL &#41; ](../../t-sql/queries/select-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
[ INTO new_table ]
[ ON filegroup]
```  
  
## <a name="arguments"></a>Argumentos  
 *new_table*  
 Especifica o nome de uma nova tabela a ser criada com base nas colunas da lista de seleção e nas linhas escolhidas na origem dos dados.  
 
  *grupo de arquivos*
 
 Especifica o nome do grupo de arquivos no qual a nova tabela será criada. O grupo de arquivos especificado deve existir no banco de dados mais a SQL Server engine gera um erro. Essa opção tem suporte apenas a partir [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)].
 
 O formato de *new_table* é determinado pela avaliação das expressões na lista de seleção. As colunas na *new_table* são criadas na ordem especificada pela lista de seleção. Cada coluna em *new_table* tem o mesmo nome, tipo de dados, nulidade e valor da expressão correspondente na lista de seleção. A propriedade IDENTITY de uma coluna é transferida, exceto nas condições definidas em "Trabalhando com colunas de identidade", na seção Comentários.  
  
 Para criar a tabela em outro banco de dados na mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], especifique *new_table* como um nome totalmente qualificado no formato *table_name*.  
  
 Não é possível criar *new_table* em um servidor remoto; no entanto, você pode preencher *new_table* de uma fonte de dados remota. Para criar *new_table* de uma tabela de origem remota, especifique a tabela de origem usando um nome de quatro partes no formulário *linked_server*. *catálogo*. *esquema*. *objeto* na cláusula FROM da instrução SELECT. Como alternativa, você pode usar o [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md) função ou o [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md) função na cláusula FROM para especificar a fonte de dados remoto.  
  
## <a name="data-types"></a>Tipos de dados  
 O atributo FILESTREAM não é transferido para a nova tabela. FILESTREAM BLOBs são copiados e armazenados na nova tabela como **varbinary (max)** BLOBs. Sem o atributo FILESTREAM, o **varbinary (max)** tipo de dados tem uma limitação de 2 GB. Se um FILESTREAM BLOB exceder esse valor, ocorrerá o erro 7119, e a instrução será interrompida.  
  
 Quando uma coluna de identidade existente é seleciona para uma nova tabela, a nova coluna herda a propriedade IDENTITY, a menos que uma das seguintes condições seja verdadeira:  
  
-   A instrução SELECT contém uma junção.  
  
-   Várias instruções SELECT são unidas usando UNION.  
  
-   A coluna de identidade é listada mais de uma vez na lista de seleção.  
  
-   A coluna de identidade faz parte de uma expressão.  
  
-   A coluna de identidade provém de uma fonte de dados remota.  
  
Se alguma dessas condições for verdadeira, a coluna será criada como NOT NULL em vez de herdar a propriedade IDENTITY. Se uma coluna de identidade for obrigatória na nova tabela, mas não estiver disponível, ou se você desejar um valor de semente ou de incremento diferente da coluna de identidade de origem, defina a coluna na lista de seleção que usa a função IDENTITY. Consulte "Criando uma coluna de identidade usando a função IDENTITY" na seção Exemplos abaixo.  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 Não é possível especificar uma variável de tabela ou um parâmetro com valor de tabela como a nova tabela.  
  
 Você não pode usar SELECT...INTO para criar uma tabela particionada, mesmo quando a tabela de origem está particionada. SELECT...INTO não usa o esquema de partição da tabela de origem; em vez disso, a nova tabela é criada no grupo de arquivos padrão. Para inserir linhas em uma tabela particionada, crie primeiro a tabela particionada e depois use a instrução INSERT INTO...SELECT FROM.  
  
 Índices, restrições e gatilhos definidos na tabela de origem não são transferidos para a nova tabela, nem podem ser especificados na instrução SELECT... INTO. Se esses objetos forem obrigatórios, você poderá criá-los depois de executar a instrução SELECT...INTO.  
  
 A especificação de uma cláusula ORDER BY não garante que as linhas sejam inseridas na ordem especificada.  
  
 Quando uma coluna esparsa é incluída na lista de seleção, a propriedade da coluna esparsa não é transferida para a coluna na nova tabela. Se essa propriedade for necessária na nova tabela, altere a definição de coluna depois de executar a instrução SELECT... INTO para incluir essa propriedade.  
  
 Quando uma coluna computada é incluída na lista de seleção, a coluna correspondente na nova tabela não é uma coluna computada. Os valores na nova coluna são os computados no momento em que SELECT...INTO foi executada.  
  
## <a name="logging-behavior"></a>Comportamento de log  
 A quantidade de logs de SELECT...INTO depende do modelo de recuperação em vigor para o banco de dados. Nos modelos de recuperação simples ou bulk-logged, as operações em massa são registradas minimamente. Com log mínimo, usando o SELECT... NA instrução pode ser mais eficiente do que criar uma tabela e, em seguida, preencher a tabela com uma instrução INSERT. Para obter mais informações, veja [O log de transações &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md).  
  
## <a name="permissions"></a>Permissões  
 Exige permissão CREATE DATABASE no banco de dados de destino.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-table-by-specifying-columns-from-multiple-sources"></a>A. Criando uma tabela especificando colunas de várias origens  
 O exemplo a seguir cria a tabela `dbo.EmployeeAddresses` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] selecionando sete colunas de várias tabelas relacionadas a funcionários e endereços.  
  
```sql  
SELECT c.FirstName, c.LastName, e.JobTitle, a.AddressLine1, a.City,   
    sp.Name AS [State/Province], a.PostalCode  
INTO dbo.EmployeeAddresses  
FROM Person.Person AS c  
    JOIN HumanResources.Employee AS e   
    ON e.BusinessEntityID = c.BusinessEntityID  
    JOIN Person.BusinessEntityAddress AS bea  
    ON e.BusinessEntityID = bea.BusinessEntityID  
    JOIN Person.Address AS a  
    ON bea.AddressID = a.AddressID  
    JOIN Person.StateProvince as sp   
    ON sp.StateProvinceID = a.StateProvinceID;  
GO  
```  
  
### <a name="b-inserting-rows-using-minimal-logging"></a>B. Inserindo linhas usando log mínimo  
 O exemplo a seguir cria a tabela `dbo.NewProducts` e insere linhas da tabela `Production.Product`. O exemplo pressupõe que o modelo de recuperação do banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] esteja definido como FULL. Para assegurar um log mínimo, o modelo de recuperação do banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] é definido como BULK_LOGGED antes da inserção das linhas e redefinido como FULL após a instrução SELECT...INTO. Esse processo garante que a instrução SELECT... INTO use um espaço mínimo no log de transações e seja executada de forma eficiente.  
  
```sql  
ALTER DATABASE AdventureWorks2012 SET RECOVERY BULK_LOGGED;  
GO  
  
SELECT * INTO dbo.NewProducts  
FROM Production.Product  
WHERE ListPrice > $25   
AND ListPrice < $100;  
GO  
ALTER DATABASE AdventureWorks2012 SET RECOVERY FULL;  
GO  
```  
  
### <a name="c-creating-an-identity-column-using-the-identity-function"></a>C. Criando uma coluna de identidade usando a função IDENTITY  
 O exemplo a seguir usa a função IDENTITY para criar uma coluna de identidade na nova tabela `Person.USAddress` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Isso é necessário porque a instrução SELECT que define a tabela contém uma junção; por isso, a propriedade IDENTITY não é transferida para a nova tabela. Observe que os valores de semente e incremento especificados na função IDENTITY são diferentes dos valores da coluna `AddressID` na tabela de origem `Person.Address`.  
  
```sql  
-- Determine the IDENTITY status of the source column AddressID.  
SELECT OBJECT_NAME(object_id) AS TableName, name AS column_name, 
  is_identity, seed_value, increment_value  
FROM sys.identity_columns  
WHERE name = 'AddressID';  
  
-- Create a new table with columns from the existing table Person.Address. 
-- A new IDENTITY column is created by using the IDENTITY function.  
SELECT IDENTITY (int, 100, 5) AS AddressID,   
       a.AddressLine1, a.City, b.Name AS State, a.PostalCode  
INTO Person.USAddress   
FROM Person.Address AS a  
INNER JOIN Person.StateProvince AS b 
  ON a.StateProvinceID = b.StateProvinceID  
WHERE b.CountryRegionCode = N'US';   
  
-- Verify the IDENTITY status of the AddressID columns in both tables.  
SELECT OBJECT_NAME(object_id) AS TableName, name AS column_name, 
  is_identity, seed_value, increment_value  
FROM sys.identity_columns  
WHERE name = 'AddressID';  
```  
  
### <a name="d-creating-a-table-by-specifying-columns-from-a-remote-data-source"></a>D. Criando uma tabela especificando colunas de uma fonte de dados remotos  
 O seguinte exemplo demonstra três métodos para criar uma nova tabela no servidor local de uma fonte de dados remota. O exemplo começa criando um link para a fonte de dados remota. O nome do servidor vinculado, `MyLinkServer,` especificada na cláusula FROM da primeira SELECT... NA instrução e na função OPENQUERY da segunda SELECT... NA instrução. A terceira instrução SELECT... INTO usa a função OPENDATASOURCE, que especifica a fonte de dados remota diretamente, em vez de usar o nome de servidor vinculado.  
  
 **Aplica-se a:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```sql
USE master;  
GO  
-- Create a link to the remote data source.   
-- Specify a valid server name for @datasrc as 'server_name' 
-- or 'server_name\instance_name'.  
EXEC sp_addlinkedserver @server = N'MyLinkServer',  
    @srvproduct = N' ',  
    @provider = N'SQLNCLI',   
    @datasrc = N'server_name',  
    @catalog = N'AdventureWorks2012';  
GO  

USE AdventureWorks2012;  
GO  
-- Specify the remote data source in the FROM clause using a four-part name   
-- in the form linked_server.catalog.schema.object.  
SELECT DepartmentID, Name, GroupName, ModifiedDate  
INTO dbo.Departments  
FROM MyLinkServer.AdventureWorks2012.HumanResources.Department  
GO  
-- Use the OPENQUERY function to access the remote data source.  
SELECT DepartmentID, Name, GroupName, ModifiedDate  
INTO dbo.DepartmentsUsingOpenQuery  
FROM OPENQUERY(MyLinkServer, 'SELECT *  
               FROM AdventureWorks2012.HumanResources.Department');   
GO  
-- Use the OPENDATASOURCE function to specify the remote data source.  
-- Specify a valid server name for Data Source using the format 
-- server_name or server_name\instance_name.  
SELECT DepartmentID, Name, GroupName, ModifiedDate  
INTO dbo.DepartmentsUsingOpenDataSource  
FROM OPENDATASOURCE('SQLNCLI',  
    'Data Source=server_name;Integrated Security=SSPI')  
    .AdventureWorks2012.HumanResources.Department;  
GO  
```  
  
### <a name="e-import-from-an-external-table-created-with--polybase"></a>E. Importar de uma tabela externa criada com o PolyBase  
 Importe dados do Hadoop ou armazenamento do Azure para SQL Server, para armazenamento persistente. Use `SELECT INTO` para importar dados referenciados por uma tabela externa para armazenamento persistente no SQL Server. Crie uma tabela relacional rapidamente e, em seguida, crie um índice de repositório de coluna sobre a tabela em uma segunda etapa.  
  
 **Aplica-se ao:** [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```sql
-- Import data for car drivers into SQL Server to do more in-depth analysis.  
SELECT DISTINCT   
        Insured_Customers.FirstName, Insured_Customers.LastName,   
        Insured_Customers.YearlyIncome, Insured_Customers.MaritalStatus  
INTO Fast_Customers from Insured_Customers INNER JOIN   
(  
        SELECT * FROM CarSensor_Data where Speed > 35   
) AS SensorD  
ON Insured_Customers.CustomerKey = SensorD.CustomerKey  
ORDER BY YearlyIncome  
  
```  
### <a name="f-creating-a-new-table-as-a-copy-of-another-table-and-loading-it-a-specified-filegroup"></a>F. Criando uma nova tabela como uma cópia de outra tabela e carregá-lo um grupo de arquivos especificado
O exemplo a seguir demonstra a criação de uma nova tabela como uma cópia de outra tabela e carregá-lo em um grupo de arquivos especificado diferente do grupo de arquivos padrão do usuário.

 **Aplica-se a:**[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]

```sql
ALTER DATABASE [AdventureWorksDW2016] ADD FILEGROUP FG2;
ALTER DATABASE [AdventureWorksDW2016]
ADD FILE
(
NAME='FG2_Data',
FILENAME = '/var/opt/mssql/data/AdventureWorksDW2016_Data1.mdf'
)
TO FILEGROUP FG2;
GO
SELECT *  INTO [dbo].[FactResellerSalesXL] ON FG2 from [dbo].[FactResellerSales]
```
  
## <a name="see-also"></a>Consulte também  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [Exemplos SELECT &#40; Transact-SQL &#41;](../../t-sql/queries/select-examples-transact-sql.md)   
 [INSERIR &#40;O Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [IDENTIDADE &#40; Função &#41; &#40; Transact-SQL &#41;](../../t-sql/functions/identity-function-transact-sql.md)  
  
  
