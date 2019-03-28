---
title: Ingestão de dados para um pool de dados do SQL Server
titleSuffix: SQL Server 2019 big data clusters
description: Este tutorial demonstra como ingestão de dados para o pool de dados de um cluster de big data do SQL Server 2019 (visualização).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/27/2018
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 5ae0777c2bc98e99c83bca35fa2aab8efc8b57a5
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58509933"
---
# <a name="tutorial-ingest-data-into-a-sql-server-data-pool-with-transact-sql"></a>Tutorial: Ingestão de dados para um pool de dados do SQL Server com o Transact-SQL

Este tutorial demonstra como usar o Transact-SQL para carregar dados do [pool de dados](concept-data-pool.md) de um cluster de big data do SQL Server 2019 (visualização). Com clusters de grandes dados do SQL Server, dados de uma variedade de fontes podem ser ingeridos e distribuídos entre instâncias do pool de dados.

Neste tutorial, você aprenderá como:

> [!div class="checklist"]
> * Crie uma tabela externa no pool de dados.
> * Inseri dados de sequência de cliques de web de exemplo na tabela de pool de dados.
> * Unir dados na tabela de pool de dados com tabelas locais.

> [!TIP]
> Se você preferir, você pode baixar e executar um script para os comandos neste tutorial. Para obter instruções, consulte a [exemplos de pools de dados](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-pool) no GitHub.

## <a id="prereqs"></a> Pré-requisitos

- [Ferramentas de big data](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **Extensão do SQL Server de 2019**
- [Carregar dados de exemplo no seu cluster de big data](tutorial-load-sample-data.md)

## <a name="create-an-external-table-in-the-data-pool"></a>Criar uma tabela externa no pool de dados

As seguintes etapas criam uma tabela externa no pool de dados chamado **web_clickstream_clicks_data_pool**. Esta tabela, em seguida, pode ser usada como um local para ingerir dados para o cluster de big data.

1. No estúdio de dados do Azure, conecte-se à instância mestre do SQL Server do seu cluster de big data. Para obter mais informações, consulte [conectar-se a instância mestre do SQL Server](connect-to-big-data-cluster.md#master).

1. Clique duas vezes em que a conexão na **servidores** janela para mostrar o painel do servidor para a instância mestre do SQL Server. Selecione **nova consulta**.

   ![Consulta de instância mestre do SQL Server](./media/tutorial-data-pool-ingest-sql/sql-server-master-instance-query.png)

1. Execute o seguinte comando Transact-SQL para alterar o contexto para o **vendas** banco de dados na instância do mestre.

   ```sql
   USE Sales
   GO
   ```

1. Crie uma fonte de dados externa ao pool de dados se ele ainda não existir.

   ```sql
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
     CREATE EXTERNAL DATA SOURCE SqlDataPool
     WITH (LOCATION = 'sqldatapool://service-mssql-controller:8080/datapools/default');
   ```

1. Criar uma tabela externa chamada **web_clickstream_clicks_data_pool** no pool de dados.

   ```sql
   IF NOT EXISTS(SELECT * FROM sys.external_tables WHERE name = 'web_clickstream_clicks_data_pool')
      CREATE EXTERNAL TABLE [web_clickstream_clicks_data_pool]
      ("wcs_user_sk" BIGINT , "i_category_id" BIGINT , "clicks" BIGINT)
      WITH
      (
         DATA_SOURCE = SqlDataPool,
         DISTRIBUTION = ROUND_ROBIN
      );
   ```
  
1. No CTP 2.4 a criação do pool de dados é assíncrona, mas não há nenhuma maneira de determinar quando ela for concluída ainda. Aguarde dois minutos verificar se que o pool de dados é criado antes de continuar.

## <a name="load-data"></a>Carregar dados

As etapas a seguir ingestão de dados de sequência de cliques de web de exemplo para o pool de dados usando a tabela externa criada nas etapas anteriores.

1. Defina variáveis para a consulta que você deseja usar para inserir dados no pool de dados. Para o CTP 2.3 ou anterior, o **modelo... sp_data_pool_table_insert_data** procedimento armazenado é necessária. Para o CTP 2.4 e versões posteriores, você pode usar um `INSERT INTO` instrução para inserir os resultados da consulta no pool de dados (o **web_clickstream_clicks_data_pool** tabela externa).

   ```sql
   IF SERVERPROPERTY('ProductLevel') = 'CTP2.4'
   BEGIN
      INSERT INTO web_clickstream_clicks_data_pool
      SELECT wcs_user_sk, i_category_id, COUNT_BIG(*) as clicks
        FROM sales.dbo.web_clickstreams_hdfs_parquet
      INNER JOIN sales.dbo.item it ON (wcs_item_sk = i_item_sk
                              AND wcs_user_sk IS NOT NULL)
      GROUP BY wcs_user_sk, i_category_id
      HAVING COUNT_BIG(*) > 100;
   END

   ELSE IF SERVERPROPERTY('ProductLevel') = 'CTP2.3'
   BEGIN
      DECLARE @db_name SYSNAME = 'Sales'
      DECLARE @schema_name SYSNAME = 'dbo'
      DECLARE @table_name SYSNAME = 'web_clickstream_clicks_data_pool'
      DECLARE @query NVARCHAR(MAX) = '
      SELECT wcs_user_sk, i_category_id, COUNT_BIG(*) as clicks
      FROM sales.dbo.web_clickstreams
      INNER JOIN sales.dbo.item it ON (wcs_item_sk = i_item_sk
         AND wcs_user_sk IS NOT NULL)
      GROUP BY wcs_user_sk, i_category_id
      HAVING COUNT_BIG(*) > 100;'

      EXEC model..sp_data_pool_table_insert_data @db_name, @schema_name, @table_name, @query
   END
   ```

1. Inspecione os dados inseridos com duas consultas SELECT.

   ```sql
   SELECT count(*) FROM [dbo].[web_clickstream_clicks_data_pool]
   SELECT TOP 10 * FROM [dbo].[web_clickstream_clicks_data_pool]  
   ```

## <a name="query-the-data"></a>Consultar os dados

Junte-se os resultados armazenados da consulta no pool de dados com dados locais na **vendas** tabela.

```sql
SELECT TOP (100)
   w.wcs_user_sk,
   SUM( CASE WHEN i.i_category = 'Books' THEN 1 ELSE 0 END) AS book_category_clicks,
   SUM( CASE WHEN w.i_category_id = 1 THEN 1 ELSE 0 END) AS [Home & Kitchen],
   SUM( CASE WHEN w.i_category_id = 2 THEN 1 ELSE 0 END) AS [Music],
   SUM( CASE WHEN w.i_category_id = 3 THEN 1 ELSE 0 END) AS [Books],
   SUM( CASE WHEN w.i_category_id = 4 THEN 1 ELSE 0 END) AS [Clothing & Accessories],
   SUM( CASE WHEN w.i_category_id = 5 THEN 1 ELSE 0 END) AS [Electronics],
   SUM( CASE WHEN w.i_category_id = 6 THEN 1 ELSE 0 END) AS [Tools & Home Improvement],
   SUM( CASE WHEN w.i_category_id = 7 THEN 1 ELSE 0 END) AS [Toys & Games],
   SUM( CASE WHEN w.i_category_id = 8 THEN 1 ELSE 0 END) AS [Movies & TV],
   SUM( CASE WHEN w.i_category_id = 9 THEN 1 ELSE 0 END) AS [Sports & Outdoors]
FROM [dbo].[web_clickstream_clicks_data_pool] as w
INNER JOIN (SELECT DISTINCT i_category_id, i_category FROM item) as i
   ON i.i_category_id = w.i_category_id
GROUP BY w.wcs_user_sk;
```

## <a name="clean-up"></a>Limpar

Use o seguinte comando para remover os objetos de banco de dados criados neste tutorial.

```sql
DROP EXTERNAL TABLE [dbo].[web_clickstream_clicks_data_pool];
```

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre como ingestão de dados no pool de dados com trabalhos do Spark:
> [!div class="nextstepaction"]
> [Ingestão de dados com trabalhos do Spark](tutorial-data-pool-ingest-spark.md)
