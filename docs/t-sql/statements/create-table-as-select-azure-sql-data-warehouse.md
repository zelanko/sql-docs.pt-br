---
title: CREATE TABLE AS SELECT (SQL Data Warehouse do Azure) | Microsoft Docs
ms.custom: 
ms.date: 10/07/2016
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d1e08f88-64ef-4001-8a66-372249df2533
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 429c2dc727d844c35943fa599e6fbcb911df04ac
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="create-table-as-select-azure-sql-data-warehouse"></a>CREATE TABLE AS SELECT (SQL Data Warehouse do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

CTAS (CREATE TABLE AS SELECT) é um dos recursos mais importantes do T-SQL disponíveis. É uma operação totalmente em paralelo que cria uma nova tabela com base na saída de uma instrução SELECT. CTAS é a maneira mais rápida e simples de criar uma cópia de uma tabela.   
 
 Por exemplo, use CTAS para:  
  
-   Recriar uma tabela com uma coluna de distribuição de hash diferente.
-   Recriar uma tabela como replicada.   
-   Criar um índice columnstore em apenas algumas das colunas da tabela.  
-   Consultar ou importar dados externos.  

> [!NOTE]  
> Como CTAS complementa os recursos de criação de uma tabela, este tópico tenta não repetir o tópico CREATE TABLE. Ele descreve as diferenças entre as instruções CTAS e CREATE TABLE. Para obter os detalhes sobre CREATE TABLE, veja a instrução [CREATE TABLE (SQL Data Warehouse do Azure)](https://msdn.microsoft.com/library/mt203953/). 
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
<a name="syntax-bk"></a>

## <a name="syntax"></a>Sintaxe   

```  
CREATE TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    [ ( column_name [ ,...n ] ) ]  
    WITH ( 
      <distribution_option> -- required
      [ , <table_option> [ ,...n ] ]    
    )  
    AS <select_statement>   
[;]  

<distribution_option> ::=
    { 
        DISTRIBUTION = HASH ( distribution_column_name ) 
      | DISTRIBUTION = ROUND_ROBIN 
      | DISTRIBUTION = REPLICATE
    }   

<table_option> ::= 
    {   
        CLUSTERED COLUMNSTORE INDEX --default for SQL Data Warehouse 
      | HEAP --default for Parallel Data Warehouse   
      | CLUSTERED INDEX ( { index_column_name [ ASC | DESC ] } [ ,...n ] ) --default is ASC 
    }  
    | PARTITION ( partition_column_name RANGE [ LEFT | RIGHT ] --default is LEFT  
        FOR VALUES ( [ boundary_value [,...n] ] ) ) 
  
<select_statement> ::=  
    [ WITH <common_table_expression> [ ,...n ] ]  
    SELECT select_criteria  

```  

<a name="arguments-bk"></a>
  
## <a name="arguments"></a>Argumentos  
Para obter detalhes, confira a [seção Argumentos](https://msdn.microsoft.com/library/mt203953/#Arguments) em CREATE TABLE.  

<a name="column-options-bk"></a>

### <a name="column-options"></a>Opções de coluna
`column_name` [ ,...`n` ]   
 Os nomes de coluna não permitem as [opções de coluna](https://msdn.microsoft.com/library/mt203953/#ColumnOptions) mencionadas em CREATE TABLE.  Nesse caso, você pode fornecer uma lista opcional de um ou mais nomes de coluna para a nova tabela. As colunas na nova tabela usarão os nomes que você especificar. Quando você especificar nomes de coluna, o número de colunas na lista de colunas deverá corresponder ao número de colunas nos resultados de select. Se você não especificar nenhum nome de coluna, a nova tabela de destino usará os nomes de coluna nos resultados da instrução select. 
  
 Não é possível especificar nenhuma outra opções de coluna, como tipos de dados, agrupamento ou nulidade. Cada um desses atributos é derivado dos resultados da instrução `SELECT`. No entanto, você pode usar a instrução SELECT para alterar os atributos. Para obter um exemplo, confira [Usar CTAS para alterar os atributos da coluna](#ctas-change-column-attributes-bk).   

<a name="table-distribution-options-bk"></a>

### <a name="table-distribution-options"></a>Opções de distribuição da tabela

`DISTRIBUTION` = `HASH` ( *distribution_column_name* ) | ROUND_ROBIN | REPLICATE      
A instrução CTAS requer uma opção de distribuição e não têm valores padrão. Isso é diferente de CREATE TABLE, que tem padrões. 

Para obter detalhes e entender como escolher a melhor coluna de distribuição, veja a seção [Opções de distribuição da tabela](https://msdn.microsoft.com/library/mt203953/#TableDistributionOptions) em CREATE TABLE. 

<a name="table-partition-options-bk"></a>

### <a name="table-partition-options"></a>Opções de partição da tabela
A instrução CTAS cria uma tabela não particionada por padrão, mesmo quando a tabela de origem está particionada. Para criar uma tabela particionada com a instrução CTAS, você precisa especificar a opção de partição. 

Para obter detalhes, veja a seção [Opções de partição da tabela](https://msdn.microsoft.com/library/mt203953/#TablePartitionOptions) em CREATE TABLE.

<a name="select-options-bk"></a>

### <a name="select-options"></a>Opções de select
A instrução select é a diferença fundamental entre CTAS e CREATE TABLE.  

 `WITH` *common_table_expression*  
 Especifica um conjunto de resultados nomeado temporário, conhecido como uma CTE (expressão de tabela comum). Para obter mais informações, confira [WITH common_table_expression &#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 `SELECT` *select_criteria*  
 Popula a nova tabela com os resultados de uma instrução SELECT. *select_criteria* é o corpo da instrução SELECT que determina quais dados serão copiados para a nova tabela. Para obter informações sobre as instruções SELECT, confira [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md).  
  
<a name="permissions-bk"></a>  
  
## <a name="permissions"></a>Permissões  
CTAS requer a permissão `SELECT` em todos os objetos referenciados em *select_criteria*.

Para obter permissões para criar uma tabela, confira [Permissões](https://msdn.microsoft.com/library/mt203953/#Permissions) em CREATE TABLE. 
  
<a name="general-remarks-bk"></a>
  
## <a name="general-remarks"></a>Comentários gerais
Para obter detalhes, confira [Comentários gerais](https://msdn.microsoft.com/library/mt203953/#GeneralRemarks) em CREATE TABLE.

<a name="limitations-bk"></a>

## <a name="limitations-and-restrictions"></a>Limitações e restrições  
O SQL Data Warehouse do Azure ainda não é compatível com as estatísticas de criação automática nem de atualização automática.  Para obter o melhor desempenho nas consultas, é importante criar estatísticas em todas as colunas de todas as tabelas depois de executar CTAS e depois que ocorrerem alterações significativas nos dados. Para obter mais informações, veja [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md).

[SET ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/statements/set-rowcount-transact-sql.md) não tem efeito em CTAS. Para obter um comportamento semelhante, use [TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md).  
 
Para obter detalhes, confira [Limitações e restrições](https://msdn.microsoft.com/library/mt203953/#LimitationsRestrictions) em CREATE TABLE.

<a name="locking-behavior-bk"></a>
  
## <a name="locking-behavior"></a>Comportamento de bloqueio  
 Para obter detalhes, confira [Comportamento de bloqueio](https://msdn.microsoft.com/library/mt203953/#LockingBehavior) em CREATE TABLE.
 
<a name="performance-bk"></a>
 
 ## <a name="performance"></a>Desempenho 

Para uma tabela distribuída por hash, você pode usar CTAS para escolher uma coluna de distribuição diferente para melhorar o desempenho das junções e agregações. Se escolher uma coluna de distribuição diferente não for seu objetivo, você terá o melhor desempenho em CTAS se especificar a mesma coluna de distribuição, pois isso evitará a redistribuição das linhas. 

Se você estiver usando CTAS para criar a tabela e o desempenho não for um fator, especifique `ROUND_ROBIN` para não precisar decidir por uma coluna de distribuição.

Para evitar a movimentação de dados nas próximas consultas, especifique `REPLICATE`, às custas do aumento do armazenamento, para carregar uma cópia completa da tabela em cada nó de computação.  


<a name="examples-copy-table-bk"></a>

## <a name="examples-for-copying-a-table"></a>Exemplos para copiar uma tabela

<a name="ctas-copy-table-bk"></a>

### <a name="a-use-ctas-to-copy-a-table"></a>A. Usar CTAS para copiar uma tabela 
Aplica-se a: SQL Data Warehouse do Azure e Parallel Data Warehouse

Talvez um dos tipos de uso mais comuns do `CTAS` é criar uma cópia de uma tabela para que você possa alterar a DDL. Por exemplo, se você criou a tabela originalmente como `ROUND_ROBIN` e agora deseja alterá-la para uma tabela distribuída em uma coluna, `CTAS` será a forma de alterar a coluna de distribuição. `CTAS` também pode ser usado para alterar os tipos de particionamento, de indexação ou de coluna.

Digamos que você criou esta tabela usando o tipo de distribuição padrão de `ROUND_ROBIN` distribuído porque nenhuma coluna de distribuição foi especificada no `CREATE TABLE`.

```sql
CREATE TABLE FactInternetSales
(
    ProductKey int NOT NULL,
    OrderDateKey int NOT NULL,
    DueDateKey int NOT NULL,
    ShipDateKey int NOT NULL,
    CustomerKey int NOT NULL,
    PromotionKey int NOT NULL,
    CurrencyKey int NOT NULL,
    SalesTerritoryKey int NOT NULL,
    SalesOrderNumber nvarchar(20) NOT NULL,
    SalesOrderLineNumber tinyint NOT NULL,
    RevisionNumber tinyint NOT NULL,
    OrderQuantity smallint NOT NULL,
    UnitPrice money NOT NULL,
    ExtendedAmount money NOT NULL,
    UnitPriceDiscountPct float NOT NULL,
    DiscountAmount float NOT NULL,
    ProductStandardCost money NOT NULL,
    TotalProductCost money NOT NULL,
    SalesAmount money NOT NULL,
    TaxAmt money NOT NULL,
    Freight money NOT NULL,
    CarrierTrackingNumber nvarchar(25),
    CustomerPONumber nvarchar(25)
);
```

Agora você deseja criar uma nova cópia dessa tabela com um índice columnstore clusterizado para poder usufruir do desempenho das tabelas columnstore clusterizadas. Você também deseja distribuir essa tabela em ProductKey pois prevê que haverá junções nessa coluna e deseja evitar a movimentação de dados durante a junções em ProductKey. Por fim, você também deseja adicionar o particionamento em OrderDateKey para que seja possível excluir rapidamente os dados antigos descartando as partições antigas. Aqui está a instrução CTAS que copiaria a tabela antiga em uma nova tabela.

```sql
CREATE TABLE FactInternetSales_new
WITH
(
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = HASH(ProductKey),
    PARTITION
    (
        OrderDateKey RANGE RIGHT FOR VALUES
        (
        20000101,20010101,20020101,20030101,20040101,20050101,20060101,20070101,20080101,20090101,
        20100101,20110101,20120101,20130101,20140101,20150101,20160101,20170101,20180101,20190101,
        20200101,20210101,20220101,20230101,20240101,20250101,20260101,20270101,20280101,20290101
        )
    )
)
AS SELECT * FROM FactInternetSales;
```

Por fim, você pode renomear as tabelas para fazer a troca pela nova tabela e, em seguida, remover a tabela antiga.

```sql
RENAME OBJECT FactInternetSales TO FactInternetSales_old;
RENAME OBJECT FactInternetSales_new TO FactInternetSales;

DROP TABLE FactInternetSales_old;
```

<a name="examples-column-bk"></a>

## <a name="examples-for-column-options"></a>Exemplos de opções de coluna

<a name="ctas-change-column-attributes-bk"></a>

### <a name="b-use-ctas-to-change-column-attributes"></a>B. Usar CTAS para alterar atributos de coluna 
Aplica-se a: SQL Data Warehouse do Azure e Parallel Data Warehouse

Este exemplo usa CTAS para alterar os tipos de dados, a nulidade e o agrupamento para várias colunas na tabela DimCustomer2.  
  
```  
-- Original table 
CREATE TABLE [dbo].[DimCustomer2] (  
    [CustomerKey] int NOT NULL,  
    [GeographyKey] int NULL,  
    [CustomerAlternateKey] nvarchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL  
)  
WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = HASH([CustomerKey]));  
  
-- CTAS example to change data types, nullability, and column collations  
CREATE TABLE test  
WITH (HEAP, DISTRIBUTION = ROUND_ROBIN)  
AS  
SELECT  
    CustomerKey AS CustomerKeyNoChange,  
    CustomerKey*1 AS CustomerKeyChangeNullable,  
    CAST(CustomerKey AS DECIMAL(10,2)) AS CustomerKeyChangeDataTypeNullable,  
    ISNULL(CAST(CustomerKey AS DECIMAL(10,2)),0) AS CustomerKeyChangeDataTypeNotNullable,  
    GeographyKey AS GeographyKeyNoChange,  
    ISNULL(GeographyKey,0) AS GeographyKeyChangeNotNullable,  
    CustomerAlternateKey AS CustomerAlternateKeyNoChange,  
    CASE WHEN CustomerAlternateKey = CustomerAlternateKey 
        THEN CustomerAlternateKey END AS CustomerAlternateKeyNullable,  
    CustomerAlternateKey COLLATE Latin1_General_CS_AS_KS_WS AS CustomerAlternateKeyChangeCollation  
FROM [dbo].[DimCustomer2]  
  
-- Resulting table 
CREATE TABLE [dbo].[test] (
    [CustomerKeyNoChange] int NOT NULL, 
    [CustomerKeyChangeNullable] int NULL, 
    [CustomerKeyChangeDataTypeNullable] decimal(10, 2) NULL, 
    [CustomerKeyChangeDataTypeNotNullable] decimal(10, 2) NOT NULL, 
    [GeographyKeyNoChange] int NULL, 
    [GeographyKeyChangeNotNullable] int NOT NULL, 
    [CustomerAlternateKeyNoChange] nvarchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL, 
    [CustomerAlternateKeyNullable] nvarchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NULL, 
    [CustomerAlternateKeyChangeCollation] nvarchar(15) COLLATE Latin1_General_CS_AS_KS_WS NOT NULL
)
WITH (DISTRIBUTION = ROUND_ROBIN);
```
 
Como etapa final, você pode usar [RENAME &#40;Transact-SQL&#41;](../../t-sql/statements/rename-transact-sql.md) para mudar os nomes das tabelas. Assim, DimCustomer2 torna-se a nova tabela.

```
RENAME OBJECT DimCustomer2 TO DimCustomer2_old;
RENAME OBJECT test TO DimCustomer2;

DROP TABLE DimCustomer2_old;
```

<a name="examples-table-distribution-bk"></a>

## <a name="examples-for-table-distribution"></a>Exemplos de distribuição da tabela

<a name="ctas-change-distribution-method-bk"></a>

### <a name="c-use-ctas-to-change-the-distribution-method-for-a-table"></a>C. Usar CTAS para alterar o método de distribuição de uma tabela
Aplica-se a: SQL Data Warehouse do Azure e Parallel Data Warehouse

Esse exemplo simples mostra como alterar o método de distribuição de uma tabela. Para mostrar o mecanismo de como fazer isso, ele altera uma tabela distribuída por hash para round robin e, em seguida, altera a tabela de round robin para distribuída por hash. A tabela final corresponde à tabela original. 

Na maioria dos casos, não será necessário converter uma tabela distribuída por hash em uma tabela de round robin. Com um frequência maior, pode ser necessário converter uma tabela de round robin em uma tabela distribuída por hash. Por exemplo, você pode carregar inicialmente uma nova tabela como round robin e, mais tarde, convertê-la em uma tabela distribuída por hash para melhorar o desempenho da junção.

Este exemplo usa o banco de dados de exemplo AdventureWorksDW. Para carregar a versão do SQL Data Warehouse, confira [Carregar dados de exemplo no SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-load-sample-databases/)
 
```
-- DimSalesTerritory is hash-distributed.
-- Copy it to a round-robin table.
CREATE TABLE [dbo].[myTable]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = ROUND_ROBIN  
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]; 

-- Switch table names

RENAME OBJECT [dbo].[DimSalesTerritory] to [DimSalesTerritory_old];
RENAME OBJECT [dbo].[myTable] TO [DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];

```  
Em seguida, converta-a novamente em uma tabela distribuída por hash.

```
-- You just made DimSalesTerritory a round-robin table.
-- Change it back to the original hash-distributed table. 
CREATE TABLE [dbo].[myTable]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = HASH(SalesTerritoryKey) 
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]; 

-- Switch table names

RENAME OBJECT [dbo].[DimSalesTerritory] to [DimSalesTerritory_old];
RENAME OBJECT [dbo].[myTable] TO [DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```
 
<a name="ctas-change-to-replicated-bk"></a>

### <a name="d-use-ctas-to-convert-a-table-to-a-replicated-table"></a>D. Usar CTAS para converter uma tabela em uma tabela replicada  
Aplica-se a: SQL Data Warehouse do Azure e Parallel Data Warehouse 

Este exemplo aplica-se para converter tabelas round robin ou distribuídas por hash em uma tabela replicada. Esse exemplo específico avança mais uma etapa do método anterior de alterar o tipo de distribuição.  Como DimSalesTerritory é uma dimensão e provavelmente uma tabela menor, você pode escolher recriar a tabela como replicada para evitar a movimentação de dados ao unir a outras tabelas. 

```
-- DimSalesTerritory is hash-distributed.
-- Copy it to a replicated table.
CREATE TABLE [dbo].[myTable]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = REPLICATE 
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]; 

-- Switch table names

RENAME OBJECT [dbo].[DimSalesTerritory] to [DimSalesTerritory_old];
RENAME OBJECT [dbo].[myTable] TO [DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```
 
### <a name="e-use-ctas-to-create-a-table-with-fewer-columns"></a>E. Usar CTAS para criar uma tabela com menos colunas
Aplica-se a: SQL Data Warehouse do Azure e Parallel Data Warehouse 

O exemplo a seguir cria uma tabela distribuída de round robin denominada `myTable (c, ln)`. A nova tabela tem apenas duas colunas. Ela usa os aliases de coluna na instrução SELECT para os nomes das colunas.  
  
```  
CREATE TABLE myTable  
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = ROUND_ROBIN  
  )  
AS SELECT CustomerKey AS c, LastName AS ln  
    FROM dimCustomer;  
  
```  

<a name="examples-query-hints-bk"></a>

## <a name="examples-for-query-hints"></a>Exemplos de dicas de consulta

<a name="ctas-query-hint-bk"></a>

### <a name="f-use-a-query-hint-with-create-table-as-select-ctas"></a>F. Usar uma dica de consulta com CTAS (CREATE TABLE AS SELECT)  
Aplica-se a: SQL Data Warehouse do Azure e Parallel Data Warehouse
  
Esta consulta mostra a sintaxe básica para usar uma dica de junção de consulta com a instrução CTAS. Depois que a consulta é enviada, o [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] aplica a estratégia de junção de hash ao gerar o plano de consulta para cada distribuição individual. Para obter mais informações sobre a dica de consulta de junção de hash, confira [Cláusula OPTION &#40;Transact-SQL&#41;](../../t-sql/queries/option-clause-transact-sql.md).  
  
```  
CREATE TABLE dbo.FactInternetSalesNew  
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = ROUND_ROBIN   
  )  
AS SELECT T1.* FROM dbo.FactInternetSales T1 JOIN dbo.DimCustomer T2  
ON ( T1.CustomerKey = T2.CustomerKey )  
OPTION ( HASH JOIN );  
```  

<a name="examples-external-tables"></a>

## <a name="examples-for-external-tables"></a>Exemplos de tabelas externas

<a name="ctas-azure-blob-storage-bk"></a>

### <a name="g-use-ctas-to-import-data-from-azure-blob-storage"></a>G. Usar CTAS para importar dados do Armazenamento de Blobs do Azure  
Aplica-se a: SQL Data Warehouse do Azure e Parallel Data Warehouse  

Para importar dados de uma tabela externa, simplesmente use CREATE TABLE AS SELECT para selecionar a tabela externa. A sintaxe para selecionar dados de uma tabela externa no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] é a mesma que a sintaxe para selecionar dados de uma tabela regular.  
  
 O exemplo a seguir define uma tabela externa usando dados em uma conta de Armazenamento de Blobs do Azure. Em seguida, ele usa CREATE TABLE AS SELECT para selecionar na tabela externa. Essa ação importa os dados dos arquivos de texto delimitados do Armazenamento de Blobs do Azure e armazena os dados em uma nova tabela do [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
```  
--Use your own processes to create the text-delimited files on Azure blob storage.  
--Create the external table called ClickStream.  
CREATE EXTERNAL TABLE ClickStreamExt (   
    url varchar(50),  
    event_date date,  
    user_IP varchar(50)  
)  
WITH (  
    LOCATION='/logs/clickstream/2015/',  
    DATA_SOURCE = MyAzureStorage,  
    FILE_FORMAT = TextFileFormat)  
;  
  
--Use CREATE TABLE AS SELECT to import the Azure blob storage data into a new   
--SQL Data Warehouse table called ClickStreamData  
CREATE TABLE ClickStreamData   
WITH  
  (  
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = HASH (user_IP)  
  )  
AS SELECT * FROM ClickStreamExt  
;  
```  

<a name="ctas-import-Hadoop-bk"></a>
  
### <a name="h-use-ctas-to-import-hadoop-data-from-an-external-table"></a>H. Usar CTAS para importar dados do Hadoop de uma tabela externa  
Aplica-se a: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
Para importar dados de uma tabela externa, simplesmente use CREATE TABLE AS SELECT para selecionar a tabela externa. A sintaxe para selecionar dados de uma tabela externa no [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] é a mesma que a sintaxe para selecionar dados de uma tabela regular.  
  
 O exemplo a seguir define uma tabela externa em um cluster do Hadoop. Em seguida, ele usa CREATE TABLE AS SELECT para selecionar na tabela externa. Essa ação importa os dados dos arquivos de texto delimitados do Hadoop e armazena os dados em uma nova tabela do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
```  
-- Create the external table called ClickStream.  
CREATE EXTERNAL TABLE ClickStreamExt (   
    url varchar(50),  
    event_date date,  
    user_IP varchar(50)  
)  
WITH (  
    LOCATION = 'hdfs://MyHadoop:5000/tpch1GB/employee.tbl',  
    FORMAT_OPTIONS ( FIELD_TERMINATOR = '|')  
)  
;  
  
-- Use your own processes to create the Hadoop text-delimited files 
-- on the Hadoop Cluster.  
  
-- Use CREATE TABLE AS SELECT to import the Hadoop data into a new 
-- table called ClickStreamPDW  
CREATE TABLE ClickStreamPDW   
WITH  
  (  
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = HASH (user_IP)  
  )  
AS SELECT * FROM ClickStreamExt  
;   
```  
 
<a name="examples-workarounds-bk"></a>
 
## <a name="examples-using-ctas-to-replace-sql-server-code"></a>Exemplos que usam CTAS para substituir o código do SQL Server

Use CTAS para solucionar a não compatibilidade com alguns recursos. Além de permitir a execução do código no data warehouse, reescrever o código existente para usar CTAS normalmente melhora o desempenho. Este é um resultado de seu design totalmente em paralelo. 

> [!NOTE]
> Tente imaginar "CTAS primeiro". Se você achar que é possível resolver um problema usando `CTAS`, geralmente essa será a melhor maneira de abordá-lo, mesmo que mais dados sejam escritos como resultado.
>

<a name="ctas-replace-select-into-bk"></a>

### <a name="i-use-ctas-instead-of-selectinto"></a>I. Usar CTAS em vez de SELECT..INTO  
Aplica-se a: SQL Data Warehouse do Azure e Parallel Data Warehouse

O código do SQL Server normalmente usa SELECT..INTO para popular uma tabela com os resultados de uma instrução SELECT. Este é um exemplo de uma instrução SELECT..INTO do SQL Server.

```sql
SELECT *
INTO    #tmp_fct
FROM    [dbo].[FactInternetSales]
```

Essa sintaxe não é compatível com o SQL Data Warehouse nem com o Parallel Data Warehouse. Este exemplo mostra como reescrever a instrução SELECT..INTO anterior como uma instrução CTAS. Você pode escolher uma das opções de DISTRIBUTION descritas na sintaxe de CTAS. Este exemplo usa o método de distribuição de ROUND_ROBIN.

```sql
CREATE TABLE #tmp_fct
WITH
(
    DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
;
```

<a name="ctas-replace-implicit-joins-bk"></a>

### <a name="j-use-ctas-and-implicit-joins-to-replace-ansi-joins-in-the-from-clause-of-an-update-statement"></a>J. Usar CTAS e junções implícita para substituir as junções de ANSI na cláusula `FROM` de uma instrução `UPDATE`  
Aplica-se a: SQL Data Warehouse do Azure e Parallel Data Warehouse  

É possível que você tenha uma atualização complexa que una mais de duas tabelas usando a sintaxe de junção ANSI para executar UPDATE ou DELETE.

Imagine que você precisasse atualizar esta tabela:

```sql
CREATE TABLE [dbo].[AnnualCategorySales]
(   [EnglishProductCategoryName]    NVARCHAR(50)    NOT NULL
,   [CalendarYear]                  SMALLINT        NOT NULL
,   [TotalSalesAmount]              MONEY           NOT NULL
)
WITH
(
    DISTRIBUTION = ROUND_ROBIN
)
;
```

A consulta original seria semelhante a esta:

```sql
UPDATE  acs
SET     [TotalSalesAmount] = [fis].[TotalSalesAmount]
FROM    [dbo].[AnnualCategorySales]     AS acs
JOIN    (
        SELECT  [EnglishProductCategoryName]
        ,       [CalendarYear]
        ,       SUM([SalesAmount])              AS [TotalSalesAmount]
        FROM    [dbo].[FactInternetSales]       AS s
        JOIN    [dbo].[DimDate]                 AS d    ON s.[OrderDateKey]             = d.[DateKey]
        JOIN    [dbo].[DimProduct]              AS p    ON s.[ProductKey]               = p.[ProductKey]
        JOIN    [dbo].[DimProductSubCategory]   AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
        JOIN    [dbo].[DimProductCategory]      AS c    ON u.[ProductCategoryKey]       = c.[ProductCategoryKey]
        WHERE   [CalendarYear] = 2004
        GROUP BY
                [EnglishProductCategoryName]
        ,       [CalendarYear]
        ) AS fis
ON  [acs].[EnglishProductCategoryName]  = [fis].[EnglishProductCategoryName]
AND [acs].[CalendarYear]                = [fis].[CalendarYear]
;
```

Como o SQL Data Warehouse não é compatível com junções ANSI na cláusula `FROM` de uma instrução `UPDATE`, não é possível usar esse código do SQL Server sem alterá-lo um pouco.

Você pode usar uma combinação de um `CTAS` e uma junção implícita para substituir este código:

```sql
-- Create an interim table
CREATE TABLE CTAS_acs
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT  ISNULL(CAST([EnglishProductCategoryName] AS NVARCHAR(50)),0)    AS [EnglishProductCategoryName]
,       ISNULL(CAST([CalendarYear] AS SMALLINT),0)                      AS [CalendarYear]
,       ISNULL(CAST(SUM([SalesAmount]) AS MONEY),0)                     AS [TotalSalesAmount]
FROM    [dbo].[FactInternetSales]       AS s
JOIN    [dbo].[DimDate]                 AS d    ON s.[OrderDateKey]             = d.[DateKey]
JOIN    [dbo].[DimProduct]              AS p    ON s.[ProductKey]               = p.[ProductKey]
JOIN    [dbo].[DimProductSubCategory]   AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
JOIN    [dbo].[DimProductCategory]      AS c    ON u.[ProductCategoryKey]       = c.[ProductCategoryKey]
WHERE   [CalendarYear] = 2004
GROUP BY
        [EnglishProductCategoryName]
,       [CalendarYear]
;

-- Use an implicit join to perform the update
UPDATE  AnnualCategorySales
SET     AnnualCategorySales.TotalSalesAmount = CTAS_ACS.TotalSalesAmount
FROM    CTAS_acs
WHERE   CTAS_acs.[EnglishProductCategoryName] = AnnualCategorySales.[EnglishProductCategoryName]
AND     CTAS_acs.[CalendarYear]               = AnnualCategorySales.[CalendarYear]
;

--Drop the interim table
DROP TABLE CTAS_acs
;
```

<a name="ctas-replace-ansi-joins-bk"></a>

### <a name="k-use-ctas-to-specify-which-data-to-keep-instead-of-using-ansi-joins-in-the-from-clause-of-a-delete-statement"></a>K. Usar CTAS para especificar quais dados para manter em vez de usar ANSI junções na cláusula FROM de uma instrução DELETE  
Aplica-se a: SQL Data Warehouse do Azure e Parallel Data Warehouse  

Às vezes, a melhor abordagem para excluir dados é usar `CTAS`. Em vez de excluir os dados, simplesmente selecione os dados que você deseja manter. Isso é verdadeiro principalmente para instruções `DELETE` que usam a sintaxe de junção ANSI, pois o SQL Data Warehouse não é compatível com junções ANSI na cláusula `FROM` de uma instrução `DELETE`.

Um exemplo de uma instrução DELETE convertida está disponível abaixo:

```sql
CREATE TABLE dbo.DimProduct_upsert
WITH
(   Distribution=HASH(ProductKey)
,   CLUSTERED INDEX (ProductKey)
)
AS -- Select Data you wish to keep
SELECT     p.ProductKey
,          p.EnglishProductName
,          p.Color
FROM       dbo.DimProduct p
RIGHT JOIN dbo.stg_DimProduct s
ON         p.ProductKey = s.ProductKey
;

RENAME OBJECT dbo.DimProduct        TO DimProduct_old;
RENAME OBJECT dbo.DimProduct_upsert TO DimProduct;
```

<a name="ctas-simplify-merge-bk"></a>

### <a name="l-use-ctas-to-simplify-merge-statements"></a>L. Usar CTAS para simplificar instruções de mesclagem  
Aplica-se a: SQL Data Warehouse do Azure e Parallel Data Warehouse  

As instruções de mesclagem podem ser substituídas, pelo menos em parte, usando `CTAS`. Você pode consolidar `INSERT` e `UPDATE` em uma única instrução. Os registros excluídos precisariam ser separados em uma segunda instrução.

Um exemplo de um `UPSERT` está disponível abaixo:

```sql
CREATE TABLE dbo.[DimProduct_upsert]
WITH
(   DISTRIBUTION = HASH([ProductKey])
,   CLUSTERED INDEX ([ProductKey])
)
AS
-- New rows and new versions of rows
SELECT      s.[ProductKey]
,           s.[EnglishProductName]
,           s.[Color]
FROM      dbo.[stg_DimProduct] AS s
UNION ALL  
-- Keep rows that are not being touched
SELECT      p.[ProductKey]
,           p.[EnglishProductName]
,           p.[Color]
FROM      dbo.[DimProduct] AS p
WHERE NOT EXISTS
(   SELECT  *
    FROM    [dbo].[stg_DimProduct] s
    WHERE   s.[ProductKey] = p.[ProductKey]
)
;

RENAME OBJECT dbo.[DimProduct]          TO [DimProduct_old];
RENAME OBJECT dbo.[DimpProduct_upsert]  TO [DimProduct];

```

<a name="ctas-data-type-and-nullability-bk"></a>

### <a name="m-explicitly-state-data-type-and-nullability-of-output"></a>M. Declarar explicitamente o tipo de dados e a nulidade de saída  
Aplica-se a: SQL Data Warehouse do Azure e Parallel Data Warehouse  

Ao migrar o código do SQL Server para o SQL Data Warehouse, você poderá encontrar este tipo de padrão de codificação:

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE result
(result DECIMAL(7,2) NOT NULL
)
WITH (DISTRIBUTION = ROUND_ROBIN)

INSERT INTO result
SELECT @d*@f
;
```

Instintivamente você poderá pensar que deve migrar este código para um CTAS, e isso estará correto. No entanto, há um problema oculto aqui.

O código a seguir NÃO produz o mesmo resultado:

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455
;

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT @d*@f as result
;
```

Observe que a coluna "resultado" transfere os valores de tipo de dados e de nulidade da expressão. Se você não tiver cuidado, isso poderá levar a variações sutis nos valores.

Tente o seguinte como exemplo:

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

O valor armazenado para o resultado é diferente. Como o valor persistente na coluna de resultado é usado em outras expressões, o erro torna-se ainda mais significativo.

![Resultados de CREATE TABLE AS SELECT](../../t-sql/statements/media/create-table-as-select-results.png)

Isso é importante principalmente para migrações de dados. Embora a segunda consulta seja indiscutivelmente mais precisa, há um problema. Os dados seriam diferentes em comparação com o sistema de origem, o que levantaria dúvidas sobre a integridade da migração. Este é um dos raros casos em que a resposta "errada" é, na verdade, a melhor!

O motivo pelo qual existe essa discrepância entre os dois resultados, ocorre devido à conversão de tipo implícito. No primeiro exemplo, a tabela define a definição de coluna. Quando a linha é inserida, ocorre uma conversão implícita de tipo. No segundo exemplo não há nenhuma conversão implícita de tipo, pois a expressão define o tipo de dados da coluna. Observe também que a coluna no segundo exemplo foi definida como uma coluna que não permite valor nulo, mas no primeiro exemplo ela não foi. Quando a tabela foi criada no primeiro exemplo, a nulidade da coluna foi definida explicitamente. No segundo exemplo, isso ficou a cargo da expressão, o que, por padrão, resultaria em uma definição NULL.  

Para resolver esses problemas, você precisa definir explicitamente a conversão de tipo e a nulidade na parte `SELECT` da instrução `CTAS`. Não é possível definir essas propriedades na parte create table.

O exemplo abaixo demonstra como corrigir o código:

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

Observe o seguinte:
- CAST ou CONVERT poderia ter sido usado
- ISNULL é usado para forçar a nulidade, não COALESCE
- ISNULL é a função mais distante
- A segunda parte de ISNULL é uma constante, ou seja, 0

> [!NOTE]
> Para que a nulidade seja definida corretamente, é essencial usar `ISNULL` e não `COALESCE`. `COALESCE` não é uma função determinística, portanto, o resultado da expressão sempre permitirá valor nulo. `ISNULL` é diferente. Ele é determinístico. Portanto, quando a segunda parte da função `ISNULL` for uma constante ou um literal, o valor resultante será NOT NULL.

Além dessa dica ser útil para garantir a integridade dos cálculos, ela também é importante para a alternância de partição de tabela. Imagine que você tenha esta tabela definida como o fato:

```sql
CREATE TABLE [dbo].[Sales]
(
    [date]      INT     NOT NULL
,   [product]   INT     NOT NULL
,   [store]     INT     NOT NULL
,   [quantity]  INT     NOT NULL
,   [price]     MONEY   NOT NULL
,   [amount]    MONEY   NOT NULL
)
WITH
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101,20020101
                    ,20030101,20040101,20050101
                    )
                )
)
;
```

No entanto, o campo de valor é uma expressão calculada, ele não faz parte dos dados de origem.

Para criar o conjunto de dados particionado, é possível fazer o seguinte:

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   [quantity]*[price]  AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create')
;
```

A consulta seria executada de forma perfeitamente normal. O problema aparece quando você tenta executar a alternância de partição. As definições de tabela não correspondem. Para fazer com que as definições da tabela correspondam, o CTAS precisa ser modificado.

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   ISNULL(CAST([quantity]*[price] AS MONEY),0) AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create');
```

Portanto, veja que manter a consistência de tipo e manter as propriedades de nulidade em um CTAS são uma prática recomendada de engenharia. Isso ajuda a manter a integridade em seus cálculos e também garante que a alternância de partição seja possível.
 
## <a name="see-also"></a>Consulte Também  
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
 [CREATE EXTERNAL TABLE AS SELECT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
 [CREATE TABLE &#40;SQL Data Warehouse do Azure&#41;](../../t-sql/statements/create-table-azure-sql-data-warehouse.md) [DROP TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [DROP EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-external-table-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [ALTER EXTERNAL TABLE &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/4ae1b23c-67f6-41d0-b614-7a8de914d145)  
  
  


