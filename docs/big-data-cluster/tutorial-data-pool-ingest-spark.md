---
title: Ingerir dados com trabalhos do Spark
titleSuffix: SQL Server big data clusters
description: Este tutorial demonstra como ingerir dados no pool de dados de um [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] usando trabalhos do Spark no Azure Data Studio.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: shivsood
ms.date: 08/21/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5325b44512d2dc1522d4bc49478e65ae4c0999e0
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653294"
---
# <a name="tutorial-ingest-data-into-a-sql-server-data-pool-with-spark-jobs"></a>Tutorial: Ingerir dados em um pool de dados do SQL Server com trabalhos do Spark

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este tutorial demonstra como usar trabalhos do Spark para carregar dados no [pool de dados](concept-data-pool.md) de um [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]. 

Neste tutorial, você aprenderá como:

> [!div class="checklist"]
> * Criar uma tabela externa no pool de dados.
> * Crie um trabalho do Spark para carregar dados do HDFS.
> * Consultar os resultados na tabela externa.

> [!TIP]
> Se preferir, você poderá baixar e executar um script para os comandos neste tutorial. Para obter instruções, confira os [Exemplos de pools de dados](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-pool) no GitHub.

## <a id="prereqs"></a> Pré-requisitos

- [Ferramentas de Big Data](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **Extensão do SQL Server 2019**
- [Carregar dados de exemplo em seu cluster de Big Data](tutorial-load-sample-data.md)

## <a name="create-an-external-table-in-the-data-pool"></a>Criar uma tabela externa no pool de dados

As etapas a seguir criam uma tabela externa no pool de dados chamado **web_clickstreams_spark_results**. Essa tabela pode ser usada como uma localização para ingerir dados no cluster de Big Data.

1. No Azure Data Studio, conecte-se à instância mestre do SQL Server do cluster de Big Data. Para obter mais informações, confira [Conectar-se à instância mestre do SQL Server](connect-to-big-data-cluster.md#master).

1. Clique duas vezes na conexão na janela **Servidores** para mostrar o painel do servidor da instância mestre do SQL Server. Selecione **Nova Consulta**.

   ![Consulta da instância mestre do SQL Server](./media/tutorial-data-pool-ingest-spark/sql-server-master-instance-query.png)

1. Crie uma fonte de dados externos para o pool de dados se ela ainda não existir.

   ```sql
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
     CREATE EXTERNAL DATA SOURCE SqlDataPool
     WITH (LOCATION = 'sqldatapool://controller-svc/default');
   ```

1. Crie uma tabela externa chamada **web_clickstreams_spark_results** no pool de dados.

   ```sql
   USE Sales
   GO
   IF NOT EXISTS(SELECT * FROM sys.external_tables WHERE name = 'web_clickstreams_spark_results')
      CREATE EXTERNAL TABLE [web_clickstreams_spark_results]
      ("wcs_click_date_sk" BIGINT , "wcs_click_time_sk" BIGINT , "wcs_sales_sk" BIGINT , "wcs_item_sk" BIGINT , "wcs_web_page_sk" BIGINT , "wcs_user_sk" BIGINT)
      WITH
      (
         DATA_SOURCE = SqlDataPool,
         DISTRIBUTION = ROUND_ROBIN
      );
   ```
  
1. No CTP 3.1, a criação do pool de dados é assíncrona, mas ainda não há como determinar quando ele é concluído. Aguarde dois minutos para verificar se o pool de dados foi criado antes de continuar.

## <a name="start-a-spark-streaming-job"></a>Iniciar um trabalho de streaming do Spark

A próxima etapa é criar um trabalho de streaming do Spark que carregue dados de cliques da Web do pool de armazenamento (HDFS) na tabela externa que você criou no pool de dados.

1. No Azure Data Studio, conecte-se à instância mestre do cluster de Big Data. Para obter mais informações, confira [Conectar-se a um cluster de Big Data](connect-to-big-data-cluster.md).

1. Clique duas vezes na conexão do gateway HDFS/Spark na janela **Servidores**. Em seguida, selecione **Novo Trabalho do Spark**.

   ![Novo trabalho do Spark](media/tutorial-data-pool-ingest-spark/hdfs-new-spark-job.png)

1. Na janela **Novo Trabalho**, insira um nome no campo **Nome do trabalho**.

1. Na lista suspensa **Jar/py File**, selecione **HDFS**. Em seguida, insira o seguinte caminho de arquivo jar:

   ```text
   /jar/mssql-spark-lib-assembly-1.0.jar
   ```

1. No campo **Classe Principal**, digite `FileStreaming`.

1. No campo **Argumentos**, insira o texto a seguir, especificando a senha para a instância mestre do SQL Server no espaço reservado `<your_password>`. 

   ```text
   --server mssql-master-pool-0.service-master-pool --port 1433 --user sa --password <your_password> --database sales --table web_clickstreams_spark_results --source_dir hdfs:///clickstream_data --input_format csv --enable_checkpoint false --timeout 380000
   ```

   A tabela a seguir descreve cada argumento:

   | Argumento | Descrição |
   |---|---|
   | nome do servidor | Uso do SQL Server para ler o esquema de tabela |
   | número da porta | SQL Server da porta está escutando (padrão 1433) |
   | username | Nome de usuário de logon do SQL Server |
   | password | Senha de logon do SQL Server |
   | nome do banco de dados | Banco de dados de destino |
   | nome da tabela externa | Tabela a ser usada para resultados |
   | Diretório de origem para streaming | Esse deve ser um URI completo, como "hdfs:///clickstream_data" |
   | formato de entrada | Pode ser "csv", "parquet" ou "json" |
   | habilitar ponto de verificação | true ou false |
   | timeout | tempo para executar o trabalho em milissegundos antes de sair |

1. Pressione **Enviar** para enviar o trabalho.

   ![Envio de trabalho do Spark](media/tutorial-data-pool-ingest-spark/spark-new-job-settings.png)

## <a name="query-the-data"></a>Consultar os dados

As etapas a seguir mostram que o trabalho de streaming do Spark carregou os dados do HDFS no pool de dados.

1. Antes de consultar os dados ingeridos, examine a saída do histórico de tarefas para ver se o trabalho foi concluído.

   ![Histórico de trabalhos do Spark](media/tutorial-data-pool-ingest-spark/spark-task-history.png)

1. Retorne à janela de consulta da instância mestre do SQL Server que você abriu no início deste tutorial.

1. Execute a consulta a seguir para inspecionar os dados ingeridos.

   ```sql
   USE Sales
   GO
   SELECT count(*) FROM [web_clickstreams_spark_results];
   SELECT TOP 10 * FROM [web_clickstreams_spark_results];
   ```

## <a name="clean-up"></a>Limpar

Use o comando a seguir para remover os objetos de banco de dados criados neste tutorial.

```sql
DROP EXTERNAL TABLE [dbo].[web_clickstreams_spark_results];
```

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre como executar um notebook de exemplo no Azure Data Studio:
> [!div class="nextstepaction"]
> [Executar um notebook de exemplo](tutorial-notebook-spark.md)
