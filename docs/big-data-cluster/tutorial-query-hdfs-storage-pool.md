---
title: Consultar dados do HDFS no pool de armazenamento
titleSuffix: SQL Server big data clusters
description: Este tutorial demonstra como consultar dados do HDFS em um [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]. Você cria uma tabela externa sobre os dados no pool de armazenamento e, em seguida, executa uma consulta.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7ba5721ef461fe327a3309431cc994a5ed377be7
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652440"
---
# <a name="tutorial-query-hdfs-in-a-sql-server-big-data-cluster"></a>Tutorial: Consultar o HDFS em um cluster de Big Data do SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este tutorial demonstra como consultar dados do HDFS em um [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)].

Neste tutorial, você aprenderá como:

> [!div class="checklist"]
> * Criar uma tabela externa apontando para os dados do HDFS em um cluster de Big Data.
> * Unir esses dados com os dados de alto valor na instância mestre.

> [!TIP]
> Se preferir, você poderá baixar e executar um script para os comandos neste tutorial. Para obter instruções, confira os [Exemplos de virtualização de dados](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-virtualization) no GitHub.

## <a id="prereqs"></a> Pré-requisitos

- [Ferramentas de Big Data](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **Extensão do SQL Server 2019**
- [Carregar dados de exemplo em seu cluster de Big Data](tutorial-load-sample-data.md)

## <a name="create-an-external-table-to-hdfs"></a>Criar uma tabela externa no HDFS

O pool de armazenamento contém dados de cliques da Web em um arquivo CSV armazenado no HDFS. Use as etapas a seguir para definir uma tabela externa que pode acessar os dados nesse arquivo.

1. No Azure Data Studio, conecte-se à instância mestre do SQL Server do cluster de Big Data. Para obter mais informações, confira [Conectar-se à instância mestre do SQL Server](connect-to-big-data-cluster.md#master).

1. Clique duas vezes na conexão na janela **Servidores** para mostrar o painel do servidor da instância mestre do SQL Server. Selecione **Nova Consulta**.

   ![Consulta da instância mestre do SQL Server](./media/tutorial-query-hdfs-storage-pool/sql-server-master-instance-query.png)

1. Execute o seguinte comando Transact-SQL para alterar o contexto para o banco de dados **Vendas** na instância mestre.

   ```sql
   USE Sales
   GO
   ```

1. Defina o formato do arquivo CSV a ser lido no HDFS. Pressione F5 para executar a instrução.

   ```sql
   CREATE EXTERNAL FILE FORMAT csv_file
   WITH (
       FORMAT_TYPE = DELIMITEDTEXT,
       FORMAT_OPTIONS(
           FIELD_TERMINATOR = ',',
           STRING_DELIMITER = '"',
           FIRST_ROW = 2,
           USE_TYPE_DEFAULT = TRUE)
   );
   ```

1. Crie uma fonte de dados externos para o pool de armazenamento se ela ainda não existir.

   ```sql
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
   BEGIN
     CREATE EXTERNAL DATA SOURCE SqlStoragePool
     WITH (LOCATION = 'sqlhdfs://controller-svc/default');
   END
   ```

1. Crie uma tabela externa que possa ler o `/clickstream_data` do pool de armazenamento. O **SqlStoragePool** pode ser acessado da instância mestre de um cluster de Big Data.

   ```sql
   CREATE EXTERNAL TABLE [web_clickstreams_hdfs]
   ("wcs_click_date_sk" BIGINT , "wcs_click_time_sk" BIGINT , "wcs_sales_sk" BIGINT , "wcs_item_sk" BIGINT , "wcs_web_page_sk" BIGINT , "wcs_user_sk" BIGINT)
   WITH
   (
       DATA_SOURCE = SqlStoragePool,
       LOCATION = '/clickstream_data',
       FILE_FORMAT = csv_file
   );
   GO
   ```

## <a name="query-the-data"></a>Consultar os dados

Execute a consulta a seguir para unir os dados do HDFS na tabela externa `web_clickstream_hdfs` com os dados relacionais no banco de dados `Sales` local.

```sql
SELECT  
    wcs_user_sk,
    SUM( CASE WHEN i_category = 'Books' THEN 1 ELSE 0 END) AS book_category_clicks,
    SUM( CASE WHEN i_category_id = 1 THEN 1 ELSE 0 END) AS [Home & Kitchen],
    SUM( CASE WHEN i_category_id = 2 THEN 1 ELSE 0 END) AS [Music],
    SUM( CASE WHEN i_category_id = 3 THEN 1 ELSE 0 END) AS [Books],
    SUM( CASE WHEN i_category_id = 4 THEN 1 ELSE 0 END) AS [Clothing & Accessories],
    SUM( CASE WHEN i_category_id = 5 THEN 1 ELSE 0 END) AS [Electronics],
    SUM( CASE WHEN i_category_id = 6 THEN 1 ELSE 0 END) AS [Tools & Home Improvement],
    SUM( CASE WHEN i_category_id = 7 THEN 1 ELSE 0 END) AS [Toys & Games],
    SUM( CASE WHEN i_category_id = 8 THEN 1 ELSE 0 END) AS [Movies & TV],
    SUM( CASE WHEN i_category_id = 9 THEN 1 ELSE 0 END) AS [Sports & Outdoors]
  FROM [dbo].[web_clickstreams_hdfs]
  INNER JOIN item it ON (wcs_item_sk = i_item_sk
                        AND wcs_user_sk IS NOT NULL)
GROUP BY  wcs_user_sk;
GO
```

## <a name="clean-up"></a>Limpar

Use o comando a seguir para remover a tabela externa usada neste tutorial.

```sql
DROP EXTERNAL TABLE [dbo].[web_clickstreams_hdfs];
GO
```

## <a name="next-steps"></a>Próximas etapas

Avance para o próximo artigo para saber como consultar o Oracle de um cluster de Big Data.
> [!div class="nextstepaction"]
> [Consultar dados externos no Oracle](tutorial-query-oracle.md)
