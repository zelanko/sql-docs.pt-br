---
title: Exportar modelos de AM do Spark com MLeap
titleSuffix: SQL Server big data clusters
description: Saiba como exportar modelos com MLeap de aprendizado de máquina do Spark.
author: lgongmsft
ms.author: shivprashant
ms.reviewer: jroth
manager: craigg
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: a2a834ff8b841c515b9d3481a961306b721f194d
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860135"
---
# <a name="export-spark-machine-learning-models-with-mleap"></a>Exportar modelos com MLeap de aprendizado de máquina do Spark

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Um cenário de aprendizado de máquina típica envolve o treinamento do modelo no Spark e pontuação fora do Spark. Exporte modelos em um formato portátil, de modo que ele pode ser usado fora do Spark. [MLeap](https://github.com/combust/mleap) é um formato de troca esse modelo. Ele permite que o Spark pipelines de aprendizado de máquina e modelos para ser exportado como formatos portátil e usado em qualquer sistema baseado em JVM com o `Mleap` tempo de execução.

Este guia demonstra como você pode exportar seus modelos de spark usando Mleap. As etapas são resumidas abaixo e detalhadas com o código na seção a seguir.

1. Comece criando um modelo do Spark. Esse uso **de treinamento e aprendizado de máquina de criação de modelo com o Spark [aqui.](train-and-create-machinelearning-models-with-spark.md)**
2. Como uma próxima etapa vamos **importar os dados de training\test e o modelo**
3. **Exportar o modelo como `Mleap` pacote**. Este pacote exportado agora pode ser usado para pontuar fora do spark.
4. Para validar, importaremos o `Mleap` agrupar back novamente e usá-lo para pontuação no Spark.

## <a name="step-1---start-by-creating-a-spark-model"></a>Etapa 1: iniciar com a criação de um modelo do Spark
Execute [de treinamento e aprendizado de máquina de criação de modelo com o Spark](train-and-create-machinelearning-models-with-spark.md) para criar conjuntos de treinamento/teste e o modelo e persistir para armazenamento HDFS. O modelo deve ser exportado como `AdultCensus.mml` sob o `spark_ml` directory.

## <a name="step-2---import-the-trainingtest-data-and-the-model"></a>Etapa 2: importar os dados de training\test e o modelo

Etapa 1 criada o `AdultCensus.mml`, que é um modelo do spark. 

Nesta etapa, importe o modelo do spark.

```python
import mleap.pyspark
from mleap.pyspark.spark_support import SimpleSparkSerializer
from pyspark.ml import PipelineModel

model_name = "AdultCensus.mml"
model_fs = "/spark_ml/" + model_name

print("load pyspark model from hbfs")
model = PipelineModel.load(model_fs)
print("Model is " , model)
print("Model stages", model.stages)
```

## <a name="step-3---export-the-model-as-mleap-bundle"></a>Etapa 3 - exportar o modelo como `Mleap` pacote

Exportar o modelo do Spark como um portátil `Mleap` modelar e mantê-lo no armazenamento local. Após essa etapa, o modelo está disponível em um computador portátil `Mleap` Formatar e pode ser usado fora do Spark.

```python
import os

#Get the train and test datasets

# Write the train and test data sets to intermediate storage

train_data_path = "/spark_ml/AdultCensusIncomeTrain"
test_data_path = "/spark_ml/AdultCensusIncomeTest"

train = spark.read.orc(train_data_path)
test = spark.read.orc(test_data_path)

print("train: ({}, {})".format(train.count(), len(train.columns)))
train.printSchema()

print("test: ({}, {})".format(test.count(), len(test.columns)))
test.printSchema()

# serialize the model to a zip file in JSON format
model_name_export = "adult_census_pipeline.zip"
model_name_path = os.getcwd()
model_file = os.path.join(model_name_path, model_name_export)

# serialize the model to a zip file in JSON format
model_name_export = "adult_census_pipeline.zip"
model_name_path = os.getcwd()
model_file = os.path.join(model_name_path, model_name_export)

# remove an old model file, if needed.
try:
    os.remove(model_file)
except OSError:
    pass

model_file_path = "jar:file:{}".format(model_file)
model.serializeToBundle(model_file_path, model.transform(train))

```

Manter o `Mleap` pacote do local para o hdfs

```python
print("persist the mleap bundle from local to hdfs")
from subprocess import Popen, PIPE
proc = Popen(["hadoop", "fs", "-put", "-f", model_file, os.path.join("/spark_ml", model_name_export)], stdout=PIPE, stderr=PIPE)
s_output, s_err = proc.communicate()
if(s_err):
    print("Error when storing to HDFS")
```

## <a name="step-3---validate-by-importing-the-mleap-bundle-and-scoring-in-spark"></a>Etapa 3: Valide, importando o `Mleap` pontuação no Spark e pacote
Na etapa 2, nós já ter exportado o modelo para um computador portátil `Mleap` formato que pode ser usado fora do Spark. Nesta etapa, podemos importar o `Mleap` serializado no Spark e usá-lo no Spark para pontuação no conjunto de teste.
   
```python
model_deserialized = PipelineModel.deserializeFromBundle(model_file_path)
print("The deserialized model is ", model_deserialized)
print("The deserialized model stages are", model_deserialized.stages)

from pyspark.ml.evaluation import BinaryClassificationEvaluator

# make prediction
pred = model_deserialized.transform(test)


# evaluate. note only 2 metrics are supported out of the box by Spark ML.
bce = BinaryClassificationEvaluator(rawPredictionCol='rawPrediction')
au_roc = bce.setMetricName('areaUnderROC').evaluate(pred)
au_prc = bce.setMetricName('areaUnderPR').evaluate(pred)

print("Results of using the model score test set")
print("Area under ROC: {}".format(au_roc))
print("Area Under PR: {}".format(au_prc))
```

## <a name="references"></a>Referências

* [Guia de Introdução com notebooks do PySpark](notebooks-guidance.md)
* [Treinamento e de criação de modelo de machine learning com Spark](train-and-create-machinelearning-models-with-spark.md)
