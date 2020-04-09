---
title: 'Criar, exportar modelos de ML do Spark: MLeap'
titleSuffix: SQL Server Big Data Clusters
description: Use PySpark para treinar e criar modelos de machine learning com o Spark em Clusters de Big Data do SQL Server. Exporte com MLeap e, em seguida, pontue o modelo com Java no SQL Server.
author: RogPodge
ms.author: roliu
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9d51cc4164cbb40ff647cad337240e689696b449
ms.sourcegitcommit: 1124b91a3b1a3d30424ae0fec04cfaa4b1f361b6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/01/2020
ms.locfileid: "80531123"
---
# <a name="create-export-and-score-spark-machine-learning-models-on-big-data-clusters-2019"></a>Criar, exportar e pontuar modelos de machine learning do Spark em [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

O exemplo a seguir mostra como criar um modelo com [ML do Spark](https://spark.apache.org/docs/latest/ml-guide.html), exportar o modelo para [MLeap](http://mleap-docs.combust.ml/) e pontuar o modelo no SQL Server com sua [Extensão de Linguagem Java](../language-extensions/language-extensions-overview.md). Isso é feito no contexto de um Cluster de Big Data do SQL Server 2019.

O diagrama a seguir ilustra o trabalho executado neste exemplo:

![Treinar a exportação de pontuação com o Spark](./media/spark-create-machine-learning-model/train-score-export-with-spark.png)

## <a name="prerequisites"></a>Pré-requisitos

Todos os arquivos deste exemplo ficam localizados em [https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark/sparkml](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark/sparkml).

Para executar o exemplo, você também precisa ter os seguintes pré-requisitos:

- Um [cluster de Big Data do SQL Server](deploy-get-started.md)

- [Ferramentas de Big Data](deploy-big-data-tools.md)
   - **kubectl**
   - **curl**
   - **Azure Data Studio**

## <a name="model-training-with-spark-ml"></a>Treinamento de modelo com ML do Spark

Para este exemplo, dados de censo (**AdultCensusIncome.csv**) são usados para criar um modelo de pipeline de ML do Spark.

1. Use o arquivo [mleap_sql_test/setup.sh](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/mleap_sql_test/setup.sh) para baixar o conjunto de dados da Internet e colocá-lo no HDFS em seu cluster de Big Data do SQL Server. Isso permite que ele seja acessado pelo Spark.

1. Em seguida, baixe o notebook de exemplo [train_score_export_ml_models_with_spark. ipynb](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/train_score_export_ml_models_with_spark.ipynb). Em uma linha de comando do PowerShell ou Bash, execute o seguinte comando para baixar o notebook de exemplo:

   ```PowerShell
   curl -o mssql_spark_connector.ipynb "https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/sparkml/train_score_export_ml_models_with_spark.ipynb"
   ```

   Este notebook contém células com os comandos necessários para esta seção do exemplo.

1. Abra o notebook no Azure Data Studio e execute cada bloco de código. Para saber mais sobre como trabalhar com notebooks, confira [Como usar notebooks com o SQL Server](../azure-data-studio/notebooks-guidance.md).

Os dados são lidos primeiro no Spark e são divididos em conjuntos de dados de treinamento e teste. Em seguida, o código treina um modelo de pipeline com os dados de treinamento. Por fim, ele exporta o modelo para um pacote MLeap.

> [!TIP]
> Você também pode revisar ou executar o código Python associado a essas etapas fora do notebook no arquivo [mleap_sql_test/mleap_pyspark. py](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/mleap_sql_test/mleap_pyspark.py).

## <a name="model-scoring-with-sql-server"></a>Pontuação de modelo com o SQL Server

Agora que o modelo de pipeline de ML do Spark está em um formato de [pacote MLeap](http://mleap-docs.combust.ml/core-concepts/mleap-bundles.html) de serialização comum, você pode pontuar o modelo no Java sem a presença do Spark.

Este exemplo usa a [Extensão de Linguagem Java](../language-extensions/language-extensions-overview.md) no SQL Server. Para pontuar o modelo no SQL Server, primeiro você precisa criar um aplicativo Java que possa carregar o modelo em Java e pontuá-lo. Você pode encontrar o código de exemplo para este aplicativo Java na pasta [MSSQL-mleap-app](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/mssql-mleap-app).

Depois de criar o exemplo, você pode usar o Transact-SQL para chamar o aplicativo Java e pontuar o modelo com uma tabela de banco de dados. Isso pode ser visto no arquivo de origem [mleap_sql_test/mleap_sql_tests.py](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/mleap_sql_test/mleap_sql_tests.py).

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de Big Data, confira [Como implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no Kubernetes](deployment-guidance.md)
