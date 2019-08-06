---
title: Criar e exportar modelos de aprendizado de máquina do Spark com MLeap
titleSuffix: SQL Server big data clusters
description: Use o PySpark para treinar e criar modelos de aprendizado de máquina com o Spark em clusters de Big Data SQL Server (versão prévia). Exportar com MLeap e, em seguida, pontuar o modelo com Java em SQL Server.
author: RogPodge
ms.author: roliu
ms.reviewer: mikeray
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9e139e76e5f5f756b57a9366cc896716cda58959
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811212"
---
# <a name="create-export-and-score-spark-machine-learning-models-on-sql-server-big-data-clusters"></a>Criar, exportar e pontuar modelos de aprendizado de máquina do Spark em clusters SQL Server Big Data

O exemplo a seguir mostra como criar um modelo com um [ml do Spark](https://spark.apache.org/docs/latest/ml-guide.html), exportar o modelo para [MLeap](http://mleap-docs.combust.ml/)e pontuar o modelo em SQL Server com sua [extensão de linguagem Java](../language-extensions/language-extensions-overview.md). Isso é feito no contexto de um cluster SQL Server Big Data 2019.

O diagrama a seguir ilustra o trabalho executado neste exemplo:

![Treinar a exportação de pontuação com o Spark](./media/spark-create-machine-learning-model/train-score-export-with-spark.png)

## <a name="prerequisites"></a>Pré-requisitos

Todos os arquivos deste exemplo estão localizados em [https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark/sparkml](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark/sparkml).

Para executar o exemplo, você também deve ter os seguintes pré-requisitos:

- Um [cluster SQL Server Big data](deploy-get-started.md)

- [Ferramentas de Big data](deploy-big-data-tools.md)
   - **kubectl**
   - **curl**
   - **Azure Data Studio**

## <a name="model-training-with-spark-ml"></a>Treinamento de modelo com ML do Spark

Para este exemplo, os dados de censo (**AdultCensusIncome. csv**) são usados para criar um modelo de pipeline de ml do Spark.

1. Use o arquivo [mleap_sql_test/setup. sh](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mleap_sql_test/setup.sh) para baixar o conjunto de dados da Internet e colocá-lo no HDFS no cluster SQL Server Big Data. Isso permite que ele seja acessado pelo Spark.

1. Em seguida, baixe o bloco de anotações de exemplo [train_score_export_ml_models_with_spark. ipynb](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/train_score_export_ml_models_with_spark.ipynb). Em uma linha de comando do PowerShell ou bash, execute o seguinte comando para baixar o bloco de anotações:

   ```PowerShell
   curl -o mssql_spark_connector.ipynb "https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/sparkml/train_score_export_ml_models_with_spark.ipynb"
   ```

   Este bloco de anotações contém células com os comandos necessários para esta seção do exemplo.

1. Abra o bloco de anotações em Azure Data Studio e execute cada bloco de código. Para obter mais informações sobre como trabalhar com blocos de anotações, consulte [como usar blocos de anotações na visualização do SQL Server 2019](notebooks-guidance.md).

Os dados são lidos primeiro no Spark e divididos em conjuntos de dados de treinamento e teste. Em seguida, o código treina um modelo de pipeline com os dados de treinamento. Por fim, ele exporta o modelo para um pacote MLeap.

> [!TIP]
> Você também pode revisar ou executar o código Python associado a essas etapas fora do bloco de notas no arquivo [mleap_sql_test/mleap_pyspark. py](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mleap_sql_test/mleap_pyspark.py) .

## <a name="model-scoring-with-sql-server"></a>Pontuação de modelo com SQL Server

Agora que o modelo de pipeline de ML do Spark está em um formato de [pacote MLeap](http://mleap-docs.combust.ml/core-concepts/mleap-bundles.html) de serialização comum, você pode pontuar o modelo em Java sem a presença do Spark. 

Este exemplo usa a [extensão de linguagem Java](../language-extensions/language-extensions-overview.md) no SQL Server. Para pontuar o modelo em SQL Server, primeiro você precisa criar um aplicativo Java que possa carregar o modelo em Java e pontua-lo. Você pode encontrar o código de exemplo para este aplicativo Java na [pasta MSSQL-mleap-app](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mssql-mleap-app).

Depois de criar o exemplo, você pode usar o Transact-SQL para chamar o aplicativo Java e pontuar o modelo com uma tabela de banco de dados. Isso pode ser visto no arquivo de origem três [mleap_sql_test/mleap_sql_tests. py](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mleap_sql_test/mleap_sql_tests.py) .

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de Big Data, consulte [como implantar SQL Server Big data clusters no kubernetes](deployment-guidance.md)
