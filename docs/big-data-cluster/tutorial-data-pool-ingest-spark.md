---
title: Ingerir dados com trabalhos do Spark
titleSuffix: SQL Server Big Data Clusters
description: Este tutorial demonstra como ingerir dados no pool de dados de um cluster de Big Data do SQL Server usando trabalhos do Spark no Azure Data Studio.
author: rajmera3
ms.author: raajmera
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ff4038fd5a09b0776533c2ffa94cb6c1afeb567b
ms.sourcegitcommit: 1124b91a3b1a3d30424ae0fec04cfaa4b1f361b6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/01/2020
ms.locfileid: "80531130"
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

## <a name="prerequisites"></a><a id="prereqs"></a> Pré-requisitos

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

1. Crie permissões para o Conector MSSQL-Spark.
   ```sql
   USE Sales
   CREATE LOGIN sample_user  WITH PASSWORD ='password123!#' 
   CREATE USER sample_user FROM LOGIN sample_user

   -- To create external tables in data pools
   GRANT ALTER ANY EXTERNAL DATA SOURCE TO sample_user;

   -- To create external table
   GRANT CREATE TABLE TO sample_user;
   GRANT ALTER ANY SCHEMA TO sample_user;

   ALTER ROLE [db_datareader] ADD MEMBER sample_user
   ALTER ROLE [db_datawriter] ADD MEMBER sample_user
   ```

1. Crie uma fonte de dados externos para o pool de dados se ela ainda não existir.

   ```sql
   USE Sales
   GO
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
   
1. Crie um logon para os pools de dados e forneça permissões para o usuário.
   ```sql 
   EXECUTE( ' Use Sales; CREATE LOGIN sample_user  WITH PASSWORD = ''password123!#'' ;') AT  DATA_SOURCE SqlDataPool;

   EXECUTE('Use Sales; CREATE USER sample_user; ALTER ROLE [db_datareader] ADD MEMBER sample_user;  ALTER ROLE [db_datawriter] ADD MEMBER sample_user;') AT DATA_SOURCE SqlDataPool;
   ```
   
A criação da tabela externa do pool de dados é uma operação de bloqueio. O controle retorna quando a tabela especificada foi criada em todos os nós do pool de dados do back-end. Se a falha ocorrer durante a operação de criação, uma mensagem de erro será retornada ao chamador.

## <a name="start-a-spark-streaming-job"></a>Iniciar um trabalho de streaming do Spark

A próxima etapa é criar um trabalho de streaming do Spark que carregue dados de cliques da Web do pool de armazenamento (HDFS) na tabela externa que você criou no pool de dados. Esses dados foram adicionados a /clickstream_data em [Carregar dados de exemplo no cluster de Big Data](tutorial-load-sample-data.md).

1. No Azure Data Studio, conecte-se à instância mestre do cluster de Big Data. Para obter mais informações, confira [Conectar-se a um cluster de Big Data](connect-to-big-data-cluster.md).

2. Crie um notebook e selecione Spark | Scala como o kernel.

3. Executar o trabalho de ingestão do Spark
   1. Configurar os parâmetros do conector Spark-SQL
      ```
      import org.apache.spark.sql.types._
      import org.apache.spark.sql.{SparkSession, SaveMode, Row, DataFrame}

      // Change per your installation
      val user= "username"
      val password= "****"
      val database =  "MyTestDatabase"
      val sourceDir = "/clickstream_data"
      val datapool_table = "web_clickstreams_spark_results"
      val datasource_name = "SqlDataPool"
      val schema = StructType(Seq(
      StructField("wcs_click_date_sk",LongType,true), StructField("wcs_click_time_sk",LongType,true), 
      StructField("wcs_sales_sk",LongType,true), StructField("wcs_item_sk",LongType,true),
      StructField("wcs_web_page_sk",LongType,true), StructField("wcs_user_sk",LongType,true)
      ))

      val hostname = "master-0.master-svc"
      val port = 1433
      val url = s"jdbc:sqlserver://${hostname}:${port};database=${database};user=${user};password=${password};"
      ```
   2. Definir e executar o trabalho do Spark
      * Cada trabalho tem duas partes: readStream e writeStream. Abaixo, criamos um quadro de dados usando o esquema definido acima e, em seguida, fizemos uma gravação na tabela externa no pool de dados.
      ```
      import org.apache.spark.sql.{SparkSession, SaveMode, Row, DataFrame}
      
      val df = spark.readStream.format("csv").schema(schema).option("header", true).load(sourceDir)
      val query = df.writeStream.outputMode("append").foreachBatch{ (batchDF: DataFrame, batchId: Long) => 
                batchDF.write
                 .format("com.microsoft.sqlserver.jdbc.spark")
                 .mode("append")
                  .option("url", url)
                  .option("dbtable", datapool_table)
                  .option("user", user)
                  .option("password", password)
                  .option("dataPoolDataSource",datasource_name).save()
               }.start()

      query.awaitTermination(40000)
      query.stop()
      ```
## <a name="query-the-data"></a>Consultar os dados

As etapas a seguir mostram que o trabalho de streaming do Spark carregou os dados do HDFS no pool de dados.

1. Antes de consultar os dados ingeridos, examine o Status de Execução do Spark, incluindo ID do Aplicativo do YARN, Interface do Usuário do Spark e Logs do Driver. Essas informações serão exibidas no notebook quando você iniciar o aplicativo Spark pela primeira vez.

   ![Detalhes da execução do Spark](./media/tutorial-data-pool-ingest-spark/Spark-Joblog-sparkui-yarn.png)

1. Retorne à janela de consulta da instância mestre do SQL Server que você abriu no início deste tutorial.

1. Execute a consulta a seguir para inspecionar os dados ingeridos.

   ```sql
   USE Sales
   GO
   SELECT count(*) FROM [web_clickstreams_spark_results];
   SELECT TOP 10 * FROM [web_clickstreams_spark_results];
   ```
1. Os dados também podem ser consultados no Spark. Por exemplo, o código abaixo imprime o número de registros na tabela:
   ```
   def df_read(dbtable: String,
                url: String,
                dataPoolDataSource: String=""): DataFrame = {
        spark.read
             .format("com.microsoft.sqlserver.jdbc.spark")
             .option("url", url)
             .option("dbtable", dbtable)
             .option("user", user)
             .option("password", password)
             .option("dataPoolDataSource", dataPoolDataSource)
             .load()
             }

   val new_df = df_read(datapool_table, url, dataPoolDataSource=datasource_name)
   println("Number of rows is " +  new_df.count)
   ```
## <a name="clean-up"></a>Limpar

Use o comando a seguir para remover os objetos de banco de dados criados neste tutorial.

```sql
DROP EXTERNAL TABLE [dbo].[web_clickstreams_spark_results];
```

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre como executar um notebook de exemplo no Azure Data Studio:
> [!div class="nextstepaction"]
> [Executar um notebook de exemplo](notebooks-tutorial-spark.md)
