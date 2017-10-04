---
title: Criar tabela como SELECT (Azure SQL Data Warehouse) | Microsoft Docs
ms.custom: 
ms.date: 10/07/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.service: sql-data-warehouse
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d1e08f88-64ef-4001-8a66-372249df2533
caps.latest.revision: 40
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2f95f9bc6975593f2536848e2bb3a2b346eca538
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="create-table-as-select-azure-sql-data-warehouse"></a>Criar tabela como SELECT (depósito de dados do SQL Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

Criar tabela como selecionar (CTAS) é um dos recursos mais importantes do T-SQL disponíveis. É uma operação totalmente em paralelo que cria uma nova tabela com base na saída de uma instrução SELECT. CTAS é a maneira mais rápida e simples para criar uma cópia de uma tabela.   
 
 Por exemplo, use CTAS para:  
  
-   Recrie uma tabela com uma coluna de distribuição hash diferente.
-   Recriar uma tabela como replicados.   
-   Crie um índice columnstore em apenas algumas das colunas na tabela.  
-   Consulta ou importar dados externos.  

> [!NOTE]  
> Como CTAS adiciona aos recursos de criação de uma tabela, este tópico tenta não repita o tópico CREATE TABLE. Em vez disso, ele descreve as diferenças entre as instruções CTAS e CREATE TABLE. Para obter os detalhes de CREATE TABLE, consulte [CREATE TABLE (Azure SQL Data Warehouse)](https://msdn.microsoft.com/library/mt203953/) instrução. 
  
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
Para obter detalhes, consulte o [seção argumentos](https://msdn.microsoft.com/library/mt203953/#Arguments) em CREATE TABLE.  

<a name="column-options-bk"></a>

### <a name="column-options"></a>Opções de coluna
`column_name` [ ,...`n` ]   
 Nomes de coluna não permitir a [opções de coluna](https://msdn.microsoft.com/library/mt203953/#ColumnOptions) mencionado em CREATE TABLE.  Em vez disso, você pode fornecer uma lista opcional de um ou mais nomes de coluna para a nova tabela. As colunas na nova tabela usará os nomes que você especificar. Quando você especificar nomes de coluna, o número de colunas na lista de colunas deve corresponder ao número de colunas nos resultados da seleção. Se você não especificar os nomes de coluna, a nova tabela de destino usará os nomes de coluna nos resultados da instrução select. 
  
 Você não pode especificar quaisquer outras opções de coluna, como tipos de dados, agrupamento ou nulidade. Cada um desses atributos é derivada dos resultados do `SELECT` instrução. No entanto, você pode usar a instrução SELECT para alterar os atributos. Para obter um exemplo, consulte [CTAS Use para alterar os atributos de coluna](#ctas-change-column-attributes-bk).   

<a name="table-distribution-options-bk"></a>

### <a name="table-distribution-options"></a>Opções de distribuição da tabela

`DISTRIBUTION` = `HASH`( *distribution_column_name* ) | ROUND_ROBIN | REPLICAR      
A instrução CTAS requer uma opção de distribuição e não têm valores padrão. Isso é diferente de CREATE TABLE, que tem padrões. 

Para obter detalhes e para entender como escolher a melhor coluna de distribuição, consulte o [tabela opções de distribuição](https://msdn.microsoft.com/library/mt203953/#TableDistributionOptions) seção em CREATE TABLE. 

<a name="table-partition-options-bk"></a>

### <a name="table-partition-options"></a>Opções de partição de tabela
A instrução CTAS cria uma tabela não particionada por padrão, mesmo se a tabela de origem está particionada. Para criar uma tabela particionada com a instrução CTAS, você deve especificar a opção de partição. 

Para obter detalhes, consulte o [opções de partição de tabela](https://msdn.microsoft.com/library/mt203953/#TablePartitionOptions) seção em CREATE TABLE.

<a name="select-options-bk"></a>

### <a name="select-options"></a>Selecione as opções
A instrução select é a diferença fundamental entre CTAS e CREATE TABLE.  

 `WITH`*common_table_expression*  
 Especifica um conjunto de resultados nomeado temporário, conhecido como uma CTE (expressão de tabela comum). Para obter mais informações, consulte [com common_table_expression &#40; Transact-SQL &#41; ](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 `SELECT`*select_criteria*  
 Preenche a nova tabela com os resultados de uma instrução SELECT. *select_criteria* é o corpo da instrução SELECT que determina quais dados a serem copiados para a nova tabela. Para obter informações sobre instruções SELECT, consulte [SELECT &#40; Transact-SQL &#41; ](../../t-sql/queries/select-transact-sql.md).  
  
<a name="permissions-bk"></a>  
  
## <a name="permissions"></a>Permissões  
Requer CTAS `SELECT` permissão em todos os objetos referenciados no *select_criteria*.

Para obter permissões criar uma tabela, consulte [permissões](https://msdn.microsoft.com/library/mt203953/#Permissions) em CREATE TABLE. 
  
<a name="general-remarks-bk"></a>
  
## <a name="general-remarks"></a>Comentários gerais
Para obter detalhes, consulte [comentários gerais](https://msdn.microsoft.com/library/mt203953/#GeneralRemarks) em CREATE TABLE.

<a name="limitations-bk"></a>

## <a name="limitations-and-restrictions"></a>Limitações e restrições  
SQL Data Warehouse do Azure faz ainda não suporte automático criar ou automática de estatísticas de atualização.  Para obter o melhor desempenho de suas consultas, é importante criar estatísticas em todas as colunas de todas as tabelas depois de executar CTAS e depois da ocorrência de quaisquer alterações significativas nos dados. Para obter mais informações, veja [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md).

[Número de linhas do conjunto de &#40; Transact-SQL &#41; ](../../t-sql/statements/set-rowcount-transact-sql.md) não tem efeito sobre CTAS. Para obter um comportamento semelhante, use [TOP &#40; Transact-SQL &#41; ](../../t-sql/queries/top-transact-sql.md).  
 
Para obter detalhes, consulte [limitações e restrições](https://msdn.microsoft.com/library/mt203953/#LimitationsRestrictions) em CREATE TABLE.

<a name="locking-behavior-bk"></a>
  
## <a name="locking-behavior"></a>Comportamento de bloqueio  
 Para obter detalhes, consulte [comportamento de bloqueio](https://msdn.microsoft.com/library/mt203953/#LockingBehavior) em CREATE TABLE.
 
<a name="performance-bk"></a>
 
 ## <a name="performance"></a>Desempenho 

Para uma tabela de hash distribuída, você pode usar CTAS para escolher uma coluna de distribuição diferente para melhorar o desempenho de junções e agregações. Se escolher que uma coluna de distribuição diferente não for seu objetivo, você terá melhor desempenho de CTAS se você especificar a mesma coluna de distribuição já que isso evitará novamente distribuir as linhas. 

Se você estiver usando CTAS para criar a tabela e o desempenho não é um fator, você pode especificar `ROUND_ROBIN` para evitar que decidir, em uma coluna de distribuição.

Para evitar a movimentação de dados em consultas subsequentes, você pode especificar `REPLICATE` às custas de maior armazenamento para carregar uma cópia completa da tabela em cada nó de computação.  


<a name="examples-copy-table-bk"></a>

## <a name="examples-for-copying-a-table"></a>Exemplos para copiar uma tabela

<a name="ctas-copy-table-bk"></a>

### <a name="a-use-ctas-to-copy-a-table"></a>A. Use CTAS para copiar uma tabela 
Aplica-se a: Azure SQL Data Warehouse e o Parallel Data Warehouse

Talvez um dos mais comuns usa de `CTAS` está criando uma cópia de uma tabela para que você possa alterar o DDL. Se por exemplo você criou a tabela como `ROUND_ROBIN` e agora deseja alterá-la para uma tabela distribuída em uma coluna, `CTAS` é como a coluna de distribuição deve ser alterada. `CTAS`também pode ser usado para alterar os tipos de particionamento, indexação ou coluna.

Digamos que você criou esta tabela usando o tipo de distribuição padrão do `ROUND_ROBIN` distribuída porque nenhuma coluna de distribuição foi especificada no `CREATE TABLE`.

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

Agora você deseja criar uma nova cópia da tabela com um índice columnstore clusterizado para que você pode tirar proveito do desempenho de tabelas columnstore clusterizado. Você também deseja distribuir essa tabela na ProductKey como antecipando a junções nessa coluna e para evitar a movimentação de dados durante a junções em ProductKey. Por fim também deseja adicionar o particionamento em OrderDateKey para que você pode excluir dados antigos, soltando partições antigas. Aqui está a instrução CTAS que copie a tabela antiga para uma nova tabela.

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

Por fim, você pode renomear tabelas para trocar na nova tabela e, em seguida, remova a tabela antiga.

```sql
RENAME OBJECT FactInternetSales TO FactInternetSales_old;
RENAME OBJECT FactInternetSales_new TO FactInternetSales;

DROP TABLE FactInternetSales_old;
```

<a name="examples-column-bk"></a>

## <a name="examples-for-column-options"></a>Exemplos de opções de coluna

<a name="ctas-change-column-attributes-bk"></a>

### <a name="b-use-ctas-to-change-column-attributes"></a>B. Use CTAS para alterar atributos de coluna 
Aplica-se a: Azure SQL Data Warehouse e o Parallel Data Warehouse

Este exemplo usa CTAS para alterar os tipos de dados, nulidade e agrupamento para várias colunas na tabela DimCustomer2.  
  
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
 
Como etapa final, você pode usar [RENOMEAÇÃO &#40; Transact-SQL &#41; ](../../t-sql/statements/rename-transact-sql.md) para alternar os nomes de tabela. Isso torna DimCustomer2 ser a nova tabela.

```
RENAME OBJECT DimCustomer2 TO DimCustomer2_old;
RENAME OBJECT test TO DimCustomer2;

DROP TABLE DimCustomer2_old;
```

<a name="examples-table-distribution-bk"></a>

## <a name="examples-for-table-distribution"></a>Exemplos de distribuição da tabela

<a name="ctas-change-distribution-method-bk"></a>

### <a name="c-use-ctas-to-change-the-distribution-method-for-a-table"></a>C. Use CTAS para alterar o método de distribuição para uma tabela
Aplica-se a: Azure SQL Data Warehouse e o Parallel Data Warehouse

Esse exemplo simples mostra como alterar o método de distribuição para uma tabela. Para mostrar a mecânica de como fazer isso, altera uma tabela de hash distribuída para round robin e, em seguida, altera a tabela de round-robin para hash distribuída. A tabela final faz a correspondência da tabela original. 

Na maioria dos casos, você não precisa alterar uma tabela de hash distribuída para uma tabela de round-robin. Com mais frequência, talvez seja necessário alterar uma tabela de round-robin para uma tabela de hash distribuído. Por exemplo, você pode inicialmente carregar uma nova tabela como round robin e, em seguida, movê-lo posteriormente para uma tabela de hash distribuída para obter um melhor desempenho de junção.

Este exemplo usa o banco de dados de exemplo AdventureWorksDW. Para carregar a versão do SQL Data Warehouse, consulte [carregar dados de exemplo no SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-load-sample-databases/)
 
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
Em seguida, alterá-la para uma tabela de hash distribuído.

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

### <a name="d-use-ctas-to-convert-a-table-to-a-replicated-table"></a>D. Use CTAS para converter uma tabela em uma tabela replicada  
Aplica-se a: Azure SQL Data Warehouse e o Parallel Data Warehouse 

Este exemplo aplica-se para converter tabelas round-robin ou distribuída de hash em uma tabela replicada. Esse exemplo específico usa o método anterior de alterar a distribuição tipo uma etapa posterior.  Como DimSalesTerritory é uma dimensão e provavelmente uma tabela menor, você pode escolher recriar a tabela como replicados para evitar a movimentação de dados ao serem unidas a outras tabelas. 

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
 
### <a name="e-use-ctas-to-create-a-table-with-fewer-columns"></a>E. Use CTAS para criar uma tabela com menos colunas
Aplica-se a: Azure SQL Data Warehouse e o Parallel Data Warehouse 

O exemplo a seguir cria uma tabela de distribuída de round-robin denominada `myTable (c, ln)`. A nova tabela tem apenas duas colunas. Ele usa os aliases de coluna na instrução SELECT para os nomes das colunas.  
  
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

### <a name="f-use-a-query-hint-with-create-table-as-select-ctas"></a>F. Use uma dica de consulta com a criação de tabela como selecionar (CTAS)  
Aplica-se a: Azure SQL Data Warehouse e o Parallel Data Warehouse
  
Esta consulta mostra a sintaxe básica para usar uma dica de consulta de junção com a instrução CTAS. Depois que a consulta é enviada, [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] aplica-se a estratégia de junção de hash ao gerar o plano de consulta para cada distribuição individuais. Para obter mais informações sobre a dica de consulta de junção de hash, consulte [cláusula OPTION &#40; Transact-SQL &#41; ](../../t-sql/queries/option-clause-transact-sql.md).  
  
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

## <a name="examples-for-external-tables"></a>Exemplos para tabelas externas

<a name="ctas-azure-blob-storage-bk"></a>

### <a name="g-use-ctas-to-import-data-from-azure-blob-storage"></a>G. Use CTAS para importar dados do armazenamento de BLOBs do Azure  
Aplica-se a: Azure SQL Data Warehouse e o Parallel Data Warehouse  

Para importar dados de uma tabela externa, simplesmente use CREATE TABLE AS SELECT selecionem a tabela externa. A sintaxe para selecionar dados em uma tabela externa em [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] é o mesmo que a sintaxe para selecionar dados de uma tabela normal.  
  
 O exemplo a seguir define uma tabela externa em dados em uma conta de armazenamento de BLOBs do Azure. Ele então usa CREATE TABLE AS SELECT selecionem a tabela externa. Isso importa os dados de arquivos de texto delimitado de armazenamento de BLOBs do Azure e armazena os dados em um novo [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] tabela.  
  
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
  
### <a name="h-use-ctas-to-import-hadoop-data-from-an-external-table"></a>H. Use CTAS para importar dados do Hadoop de uma tabela externa  
Aplica-se a:[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
Para importar dados de uma tabela externa, simplesmente use CREATE TABLE AS SELECT selecionem a tabela externa. A sintaxe para selecionar dados em uma tabela externa em [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] é o mesmo que a sintaxe para selecionar dados de uma tabela normal.  
  
 O exemplo a seguir define uma tabela externa em um cluster Hadoop. Ele então usa CREATE TABLE AS SELECT selecionem a tabela externa. Isso importa os dados de arquivos de texto delimitado por Hadoop e armazena os dados em um novo [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] tabela.  
  
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

Use CTAS para solucionar alguns recursos sem suporte. Além de ser capaz de executar seu código no data warehouse, reescrever o código existente para usar CTAS normalmente melhora o desempenho. Este é um resultado de seu design totalmente em paralelo. 

> [!NOTE]
> Tente imaginar "CTAS primeiro". Se você achar que é possível resolver um problema usando `CTAS` , em seguida, que geralmente é a melhor maneira de abordar-mesmo que você está gravando os dados mais como resultado.
>

<a name="ctas-replace-select-into-bk"></a>

### <a name="i-use-ctas-instead-of-selectinto"></a>I. Use CTAS em vez de SELECT... EM  
Aplica-se a: Azure SQL Data Warehouse e o Parallel Data Warehouse

Código do SQL Server normalmente usa SELECT... INTO para popular uma tabela com os resultados de uma instrução SELECT. Este é um exemplo de um servidor SQL SELECT... NA instrução.

```sql
SELECT *
INTO    #tmp_fct
FROM    [dbo].[FactInternetSales]
```

Essa sintaxe não é suportada no SQL Data Warehouse e o Parallel Data Warehouse. Este exemplo mostra como reconfigurar o SELECT anterior. NA instrução como uma instrução CTAS. Você pode escolher qualquer uma das opções de distribuição descritas na sintaxe CTAS. Este exemplo usa o método de distribuição de ROUND_ROBIN.

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

### <a name="j-use-ctas-and-implicit-joins-to-replace-ansi-joins-in-the-from-clause-of-an-update-statement"></a>J. Use CTAS e junções implícita para substituir as junções de ANSI no `FROM` cláusula de um `UPDATE` instrução  
Aplica-se a: Azure SQL Data Warehouse e o Parallel Data Warehouse  

Você pode achar que uma atualização complexa que une mais de duas tabelas usando ANSI ingressar na sintaxe para executar a atualização ou exclusão.

Imagine que você precisava atualizar esta tabela:

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

A consulta original pode se parecer com isso:

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

Desde que não oferece suporte a SQL Data Warehouse ANSI junções no `FROM` cláusula de um `UPDATE` instrução, você não pode usar esse código de SQL Server sobre sem alterá-lo um pouco.

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

### <a name="k-use-ctas-to-specify-which-data-to-keep-instead-of-using-ansi-joins-in-the-from-clause-of-a-delete-statement"></a>K. Use CTAS para especificar quais dados para manter em vez de usar ANSI junções na cláusula FROM de uma instrução DELETE  
Aplica-se a: Azure SQL Data Warehouse e o Parallel Data Warehouse  

Às vezes, a melhor abordagem para exclusão de dados é usar `CTAS`. Em vez de exclusão de dados simplesmente selecione os dados que você deseja manter. Este especialmente verdadeiro para `DELETE` instruções que usam ansi sintaxe de junção como SQL Data Warehouse não oferece suporte para ANSI junções no `FROM` cláusula de um `DELETE` instrução.

Um exemplo de uma instrução DELETE convertido está disponível abaixo:

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

### <a name="l-use-ctas-to-simplify-merge-statements"></a>L. Use CTAS para simplificar a instruções merge  
Aplica-se a: Azure SQL Data Warehouse e o Parallel Data Warehouse  

Instruções de mesclagem podem ser substituídas, pelo menos em parte, usando `CTAS`. Você pode consolidar o `INSERT` e `UPDATE` em uma única instrução. Quaisquer registros excluídos precisaria ser fechadas em uma segunda instrução.

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
Aplica-se a: Azure SQL Data Warehouse e o Parallel Data Warehouse  

Ao migrar o código do SQL Server para SQL Data Warehouse, você pode considerar que executar entre esse tipo de codificação padrão:

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

Instintivamente você pode pensar que você deve migrar este código para um CTAS e você está correto. No entanto, há um problema ocultado aqui.

O código a seguir produz o mesmo resultado:

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

Observe que a coluna "resultado" carrega com os valores de tipo e a nulidade de dados da expressão. Isso pode levar a diferenças sutis nos valores se você não tiver cuidado.

Tente o seguinte exemplo:

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

O valor armazenado para o resultado é diferente. Como o valor persistente na coluna de resultado é usado em outras expressões o erro se torna ainda mais significativo.

![CREATE TABLE AS SELECT resultados](../../t-sql/statements/media/create-table-as-select-results.png)

Isso é particularmente importante para migrações de dados. Embora a segunda consulta é indiscutivelmente mais precisa, há um problema. Os dados deve ser diferentes em comparação com o sistema de origem e que leva a questões de integridade da migração. Esta é uma das raros casos em que a resposta "incorreta" é, na verdade, a melhor!

O motivo pelo qual que essa discrepância entre os dois resultados, vemos estiver abaixo de conversão de tipo implícito. No primeiro exemplo, a tabela define a definição de coluna. Quando a linha é inserida ocorre uma conversão implícita de tipo. No segundo exemplo não há nenhuma conversão implícita de tipo como a expressão define o tipo de dados da coluna. Observe também que a coluna no segundo exemplo tenha sido definida como uma coluna anulável, enquanto no primeiro exemplo não tem. Quando a tabela foi criada na nulidade da coluna primeiro exemplo foi definida explicitamente. O segundo exemplo apenas estava à expressão e, por padrão isso resultaria em uma definição de NULL.  

Para resolver esses problemas você deve definir explicitamente a conversão de tipo e a nulidade no `SELECT` parte do `CTAS` instrução. Você não pode definir essas propriedades na parte criar tabela.

O exemplo a seguir demonstra como corrigir o código:

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
- ISNULL é usado para forçar a nulidade não ADESÃO
- ISNULL é a função mais externa
- A segunda parte do ISNULL é uma constante ou seja, 0

> [!NOTE]
> Para a nulidade corretamente seja definida é essencial para usar `ISNULL` e não `COALESCE`. `COALESCE`não é uma função determinística e o resultado da expressão será sempre ser NULLable. `ISNULL`é diferente. É determinístico. Portanto, quando a segunda parte do `ISNULL` função é uma constante ou um literal, o valor resultante será não nulo.

Esta dica não é apenas útil para garantir a integridade de seus cálculos. Também é importante para a alternância de partição de tabela. Imagine que você tenha esta tabela definida como o fato:

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

No entanto, o campo de valor é uma expressão calculada não faz parte da fonte de dados.

Para criar o conjunto de dados particionado, que talvez você queira fazer isso:

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

A consulta será executado perfeitamente normal. O problema é fornecida quando você tentar executar a alternância de partição. As definições de tabela não correspondem. Para fazer com que as definições da tabela corresponde a CTAS precisa ser modificada.

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

Você pode ver, portanto, que tipo consistência e manter as propriedades de nulidade em um CTAS é uma boa prática recomendada de engenharia. Ele ajuda a manter a integridade de seus cálculos e também garante que a alternância de partição é possível.
 
## <a name="see-also"></a>Consulte também  
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
 [Criar tabela externa como SELECT &#40; Transact-SQL &#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
 [Criar tabela &#40; Depósito de dados SQL do Azure &#41; ](../../t-sql/statements/create-table-azure-sql-data-warehouse.md) [DROP TABLE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [Remover tabela externa &#40; Transact-SQL &#41;](../../t-sql/statements/drop-external-table-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [ALTER EXTERNAL TABLE &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/4ae1b23c-67f6-41d0-b614-7a8de914d145)  
  
  



