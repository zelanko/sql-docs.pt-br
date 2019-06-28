---
title: Criar e exportar modelos com MLeap de aprendizado de máquina do Spark
titleSuffix: SQL Server big data clusters
description: Use o PySpark para treinar e criar modelos de aprendizado de máquina com o Spark em clusters de grandes dados do SQL Server (versão prévia). Exportar com MLeap e, em seguida, pontuar o modelo com o Java no SQL Server.
author: lgongmsft
ms.author: lgong
ms.manager: craigg
ms.reviewer: jroth
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 709d74ef33ab6b54ac688763b006d66e4210006d
ms.sourcegitcommit: 0a4879dad09c6c42ad1ff717e4512cfea46820e9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67412875"
---
# <a name="create-export-and-score-spark-machine-learning-models-on-sql-server-big-data-clusters"></a>Criar, exportar e pontuar modelos de aprendizado de máquina do Spark em clusters de grandes dados do SQL Server

O exemplo a seguir mostra como criar um modelo com [Spark ML](https://spark.apache.org/docs/latest/ml-guide.html), exporte o modelo para [MLeap](http://mleap-docs.combust.ml/)e pontuar o modelo no SQL Server com seu [extensão da linguagem Java](../language-extensions/language-extensions-overview.md). Isso é feito no contexto de um cluster de big data do SQL Server de 2019.

O diagrama a seguir ilustra o trabalho executado neste exemplo:

![Exportação de pontuação de treinamento com spark](./media/spark-create-machine-learning-model/train-score-export-with-spark.png)

## <a name="prerequisites"></a>Prerequisites

Todos os arquivos para este exemplo estão localizados em [ https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark/sparkml ](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark/sparkml).

Para executar o exemplo, você também deve ter os seguintes pré-requisitos:

- Um [cluster de big data do SQL Server](deploy-get-started.md)

- [Ferramentas de big data](deploy-big-data-tools.md)
   - **kubectl**
   - **curl**
   - **Azure Data Studio**

## <a name="model-training-with-spark-ml"></a>Treinamento do modelo com o Spark ML

Para este exemplo, dados de censo (**AdultCensusIncome.csv**) é usado para criar um modelo de pipeline ML do Spark.

1. Use o [mleap_sql_test/setup.sh](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mleap_sql_test/setup.sh) arquivo para baixar o conjunto de dados da internet e coloque-o no HDFS em seu cluster de big data do SQL Server. Isso permite que ela seja acessada pelo Spark.

1. Em seguida, baixe o exemplo de notebook [train_score_export_ml_models_with_spark.ipynb](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/train_score_export_ml_models_with_spark.ipynb). Em uma linha de comando do PowerShell ou bash, execute o seguinte comando para baixar o notebook:

   ```PowerShell
   curl -o mssql_spark_connector.ipynb "https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/sparkml/train_score_export_ml_models_with_spark.ipynb"
   ```

   Este bloco de anotações contém células com os comandos necessários para essa seção do exemplo.

1. Abra o bloco de anotações no estúdio de dados do Azure e execute cada bloco de código. Para obter mais informações sobre como trabalhar com blocos de anotações, consulte [como usar blocos de anotações na visualização do SQL Server 2019](notebooks-guidance.md).

Primeiro, os dados são lidos no Spark e divididos em conjuntos de dados de treinamento e teste. Em seguida, o código prepara um modelo de pipeline com os dados de treinamento. Por fim, ele exporta o modelo a um pacote MLeap.

> [!TIP]
> Você também pode examinar ou executar o código de Python associado com estas etapas fora do bloco de anotações na [mleap_sql_test/mleap_pyspark.py](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mleap_sql_test/mleap_pyspark.py) arquivo.

## <a name="model-scoring-with-sql-server"></a>Modelo de pontuação com o SQL Server

Agora que o modelo de pipeline de ML do Spark está em uma serialização comum [MLeap pacote](http://mleap-docs.combust.ml/core-concepts/mleap-bundles.html) formato, você pode pontuar o modelo em Java sem a presença do Spark. 

Este exemplo usa o [extensão da linguagem Java](../language-extensions/language-extensions-overview.md) no SQL Server. Para pontuar o modelo no SQL Server, você precisa primeiro criar um aplicativo Java que pode carregar o modelo no Java e pontuá-lo. Você pode encontrar o código de exemplo para esse aplicativo Java na [mssql-mleap-app pasta](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mssql-mleap-app).

Depois de criar o exemplo, você pode usar o Transact-SQL para chamar o aplicativo Java e pontuar o modelo com uma tabela de banco de dados. Isso pode ser visto em três [mleap_sql_test/mleap_sql_tests.py](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mleap_sql_test/mleap_sql_tests.py) arquivo de origem.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de big data, consulte [como implantar grandes de dados do SQL Server clusters no Kubernetes](deployment-guidance.md)
