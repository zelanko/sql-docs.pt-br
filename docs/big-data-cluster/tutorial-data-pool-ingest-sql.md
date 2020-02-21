---
title: Ingerir dados em um pool de dados do SQL Server
titleSuffix: SQL Server big data clusters
description: Este tutorial demonstra como ingerir dados no pool de dados de um [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)].
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b389f8ba8e99678f98ef4eb22d3fe51d8b04bee3
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75325411"
---
# <a name="tutorial-ingest-data-into-a-sql-server-data-pool-with-transact-sql"></a>Tutorial: Ingerir dados em um pool de dados do SQL Server com Transact-SQL

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este tutorial demonstra como usar o Transact-SQL para carregar dados no [pool de dados](concept-data-pool.md) de um [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]. Com [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], os dados de uma variedade de fontes podem ser ingeridos e distribuídos entre as instâncias do pool de dados.

Neste tutorial, você aprenderá como:

> [!div class="checklist"]
> * Criar uma tabela externa no pool de dados.
> * Inserir exemplos de dados de cliques da Web na tabela do pool de dados.
> * Unir dados na tabela do pool de dados com tabelas locais.

> [!TIP]
> Se preferir, você poderá baixar e executar um script para os comandos neste tutorial. Para obter instruções, confira os [Exemplos de pools de dados](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-pool) no GitHub.

## <a id="prereqs"></a> Pré-requisitos

- [Ferramentas de Big Data](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **Extensão do SQL Server 2019**
- [Carregar dados de exemplo em seu cluster de Big Data](tutorial-load-sample-data.md)

## <a name="create-an-external-table-in-the-data-pool"></a>Criar uma tabela externa no pool de dados

As etapas a seguir criam uma tabela externa no pool de dados chamado **web_clickstream_clicks_data_pool**. Essa tabela pode ser usada como uma localização para ingerir dados no cluster de Big Data.

1. No Azure Data Studio, conecte-se à instância mestre do SQL Server do cluster de Big Data. Para obter mais informações, confira [Conectar-se à instância mestre do SQL Server](connect-to-big-data-cluster.md#master).

1. Clique duas vezes na conexão na janela **Servidores** para mostrar o painel do servidor da instância mestre do SQL Server. Selecione **Nova Consulta**.

   ![Consulta da instância mestre do SQL Server](./media/tutorial-data-pool-ingest-sql/sql-server-master-instance-query.png)

1. Execute o seguinte comando Transact-SQL para alterar o contexto para o banco de dados **Vendas** na instância mestre.

   ```sql
   USE Sales
   GO
   ```

1. Crie uma fonte de dados externos para o pool de dados se ela ainda não existir.

   ```sql
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
     CREATE EXTERNAL DATA SOURCE SqlDataPool
     WITH (LOCATION = 'sqldatapool://controller-svc/default');
   ```

1. Crie uma tabela externa chamada **web_clickstream_clicks_data_pool** no pool de dados.

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

A criação da tabela externa do pool de dados é uma operação de bloqueio. O controle retorna quando a tabela especificada foi criada em todos os nós do pool de dados do back-end. Se a falha ocorrer durante a operação de criação, uma mensagem de erro será retornada ao chamador.

## <a name="load-data"></a>Carregar dados

As etapas a seguir ingerem exemplos de dados de cliques da Web no pool de dados usando a tabela externa criada nas etapas anteriores.

1. Use uma instrução `INSERT INTO` para inserir os resultados da consulta no pool de dados (a tabela externa **web_clickstream_clicks_data_pool**).

   ```sql
   INSERT INTO web_clickstream_clicks_data_pool
   SELECT wcs_user_sk, i_category_id, COUNT_BIG(*) as clicks
     FROM sales.dbo.web_clickstreams_hdfs
   INNER JOIN sales.dbo.item it ON (wcs_item_sk = i_item_sk
                           AND wcs_user_sk IS NOT NULL)
   GROUP BY wcs_user_sk, i_category_id
   HAVING COUNT_BIG(*) > 100;
   ```

1. Inspecione os dados inseridos com duas consultas SELECT.

   ```sql
   SELECT count(*) FROM [dbo].[web_clickstream_clicks_data_pool]
   SELECT TOP 10 * FROM [dbo].[web_clickstream_clicks_data_pool]  
   ```

## <a name="query-the-data"></a>Consultar os dados

Una os resultados armazenados da consulta no pool de dados com os dados locais na tabela **Vendas**.

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

Use o comando a seguir para remover os objetos de banco de dados criados neste tutorial.

```sql
DROP EXTERNAL TABLE [dbo].[web_clickstream_clicks_data_pool];
```

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre como ingerir dados no pool de dados com trabalhos do Spark:
> [!div class="nextstepaction"]
> [Ingerir dados com trabalhos do Spark](tutorial-data-pool-ingest-spark.md)
