---
title: A inclusão de dados em um pool de dados do SQL Server com o Transact-SQL | Microsoft Docs
description: Este tutorial demonstra como ingestão de dados para o pool de dados de um cluster de big data de 2019 do SQL Server (versão prévia) com o procedimento armazenado de sp_data_pool_table_insert_data.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/16/2018
ms.topic: tutorial
ms.prod: sql
ms.openlocfilehash: c909379c92b2eb9a98c1c191987570946a8cc002
ms.sourcegitcommit: 38f35b2f7a226ded447edc6a36665eaa0376e06e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49644081"
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

* [Implantar um cluster de big data no Kubernetes](deployment-guidance.md).
* [Instalar o Studio de dados do Azure e a extensão do SQL Server 2019](deploy-big-data-tools.md).
* [Carregar dados de exemplo no cluster](#sampledata).

[!INCLUDE [Load sample data](../includes/big-data-cluster-load-sample-data.md)]

## <a name="create-an-external-table-in-the-data-pool"></a>Criar uma tabela externa no pool de dados

As seguintes etapas criam uma tabela externa no pool de dados chamado **web_clickstream_clicks_data_pool**. Esta tabela, em seguida, pode ser usada como um local para ingerir dados para o cluster de big data.

1. No estúdio de dados do Azure, conecte-se à instância mestre do SQL Server do seu cluster de big data. Para obter mais informações, consulte [conectar-se a instância mestre do SQL Server](deploy-big-data-tools.md#master).

1. Clique duas vezes em que a conexão na **servidores** janela para mostrar o painel do servidor para a instância mestre do SQL Server. Selecione **nova consulta**.

   ![Consulta de instância mestre do SQL Server](./media/tutorial-data-pool-ingest-sql/sql-server-master-instance-query.png)

1. Execute o seguinte comando Transact-SQL para alterar o contexto para o **vendas** banco de dados na instância do mestre.

   ```sql
   USE Sales
   GO
   ```

1. Criar uma tabela externa chamada **web_clickstream_clicks_data_pool** no pool de dados. O `SqlDataPool` fonte de dados é um tipo de fonte de dados especiais que pode ser usado da instância mestre do qualquer cluster de big data.

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
  
1. No CTP 2.0, a criação do pool de dados é assíncrona, mas não há nenhuma maneira de determinar quando ela for concluída ainda. Aguarde dois minutos verificar se que o pool de dados é criado antes de continuar.

## <a name="load-data"></a>Carregar dados

As etapas a seguir ingestão de dados de sequência de cliques de web de exemplo para o pool de dados usando a tabela externa criada nas etapas anteriores.

1. Defina variáveis para a consulta que você deseja usar para inserir dados no pool de dados. Em seguida, use o **modelo... sp_data_pool_table_insert_data** procedimento armazenado para inserir os resultados da consulta no pool de dados (o **web_clickstream_clicks_data_pool** tabela externa).

   ```sql
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
