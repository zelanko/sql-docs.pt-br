---
title: Ingestão de dados com trabalhos do Spark
titleSuffix: SQL Server 2019 big data clusters
description: Este tutorial demonstra como ingestão de dados para o pool de dados de um cluster de big data de 2019 do SQL Server (versão prévia) usando trabalhos do Spark no estúdio de dados do Azure.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/07/2018
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 1e6f75f21a02b30a6f75d79a9da5be0320485c5b
ms.sourcegitcommit: 202ef5b24ed6765c7aaada9c2f4443372064bd60
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/12/2019
ms.locfileid: "54241677"
---
# <a name="tutorial-ingest-data-into-a-sql-server-data-pool-with-spark-jobs"></a>Tutorial: Ingestão de dados para um pool de dados do SQL Server com trabalhos do Spark

Este tutorial demonstra como usar trabalhos do Spark para carregar dados do [pool de dados](concept-data-pool.md) de um cluster de big data do SQL Server 2019 (visualização). 

Neste tutorial, você aprenderá como:

> [!div class="checklist"]
> * Crie uma tabela externa no pool de dados.
> * Crie um trabalho do Spark para carregar dados do HDFS.
> * Consulte os resultados na tabela externa.

> [!TIP]
> Se você preferir, você pode baixar e executar um script para os comandos neste tutorial. Para obter instruções, consulte a [exemplos de pools de dados](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-pool) no GitHub.

## <a id="prereqs"></a> Pré-requisitos

- [Ferramentas de big data](deploy-big-data-tools.md)
   - **Kubectl**
   - **Azure Data Studio**
   - **Extensão do SQL Server de 2019**
- [Carregar dados de exemplo no seu cluster de big data](tutorial-load-sample-data.md)

## <a name="create-an-external-table-in-the-data-pool"></a>Criar uma tabela externa no pool de dados

As seguintes etapas criam uma tabela externa no pool de dados chamado **web_clickstreams_spark_results**. Esta tabela, em seguida, pode ser usada como um local para ingerir dados para o cluster de big data.

1. No estúdio de dados do Azure, conecte-se à instância mestre do SQL Server do seu cluster de big data. Para obter mais informações, consulte [conectar-se a instância mestre do SQL Server](connect-to-big-data-cluster.md#master).

1. Clique duas vezes em que a conexão na **servidores** janela para mostrar o painel do servidor para a instância mestre do SQL Server. Selecione **nova consulta**.

   ![Consulta de instância mestre do SQL Server](./media/tutorial-data-pool-ingest-spark/sql-server-master-instance-query.png)

1. Criar uma tabela externa chamada **web_clickstreams_spark_results** no pool de dados. O `SqlDataPool` fonte de dados é um tipo de fonte de dados especiais que pode ser usado da instância mestre do qualquer cluster de big data.

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
  
1. No CTP 2.2, a criação do pool de dados é assíncrona, mas não há nenhuma maneira de determinar quando ela for concluída ainda. Aguarde dois minutos verificar se que o pool de dados é criado antes de continuar.

## <a name="start-a-spark-streaming-job"></a>Iniciar um trabalho de streaming do Spark

A próxima etapa é criar um trabalho que carrega dados de sequência de cliques da web do pool de armazenamento (HDFS) de streaming do Spark para a tabela externa que você criou no pool de dados.

1. No estúdio de dados do Azure, conecte-se a **gateway HDFS/Spark** do seu cluster de big data. Para obter mais informações, consulte [conectar-se ao gateway de HDFS/Spark](connect-to-big-data-cluster.md#hdfs).

1. Clique duas vezes na conexão de gateway de HDFS/Spark na **servidores** janela. Em seguida, selecione **novo trabalho de Spark**.

   ![Novo trabalho do Spark](media/tutorial-data-pool-ingest-spark/hdfs-new-spark-job.png)

1. No **novo trabalho** janela, digite um nome na **nome do trabalho** campo.

1. No **arquivo Jar/Aj** lista suspensa, selecione **HDFS**. Em seguida, digite o seguinte caminho do arquivo jar:

   ```text
   /jar/mssql-spark-lib-assembly-1.0.jar
   ```

1. No **classe principal** , insira `FileStreaming`.

1. No **argumentos** , insira o texto a seguir, especificando a senha para a instância mestre do SQL Server no `<your_password>` espaço reservado. 

   ```text
   --server mssql-master-pool-0.service-master-pool --port 1433 --user sa --password <your_password> --database sales --table web_clickstreams_spark_results --source_dir hdfs:///clickstream_data --input_format csv --enable_checkpoint false --timeout 380000
   ```

   A tabela a seguir descreve cada argumento:

   | Argumento | Descrição |
   |---|---|
   | nome do servidor | Uso do SQL Server para ler o esquema da tabela |
   | Número da porta | Porta SQL Server está escutando (padrão 1433) |
   | username | Nome de usuário de logon do SQL Server |
   | password | Senha de logon do SQL Server |
   | nome do banco de dados | Banco de dados de destino |
   | nome da tabela externa | Tabela a ser usada para obter os resultados |
   | Diretório de origem de streaming | Isso deve ser um URI completo, como "hdfs: / / / clickstream_data" |
   | formato de entrada | Isso pode ser "csv", "parquet" ou "json" |
   | Habilitar o ponto de verificação | true ou false |
   | tempo limite | tempo para executar o trabalho para em milissegundos antes de sair |

1. Pressione **enviar** para enviar o trabalho.

   ![Envio de trabalho do Spark](media/tutorial-data-pool-ingest-spark/spark-new-job-settings.png)

## <a name="query-the-data"></a>Consultar os dados

As etapas a seguir mostram que o trabalho de streaming do Spark carregou os dados do HDFS para o pool de dados.

1. Antes de consultar os dados ingeridos, examine a saída do histórico de tarefa para ver que o trabalho foi concluído.

   ![Histórico de trabalhos do Spark](media/tutorial-data-pool-ingest-spark/spark-task-history.png)

1. Retornar à janela de consulta de instância mestre do SQL Server que você abriu no início deste tutorial.

1. Execute a seguinte consulta para inspecionar os dados ingeridos.

   ```sql
   USE Sales
   GO
   SELECT count(*) FROM [web_clickstreams_spark_results];
   SELECT TOP 10 * FROM [web_clickstreams_spark_results];
   ```

## <a name="clean-up"></a>Limpar

Use o seguinte comando para remover os objetos de banco de dados criados neste tutorial.

```sql
DROP EXTERNAL TABLE [dbo].[web_clickstreams_spark_results];
```

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre como executar um bloco de anotações de exemplo no Studio de dados do Azure:
> [!div class="nextstepaction"]
> [Executar um exemplo de notebook](tutorial-notebook-spark.md)
