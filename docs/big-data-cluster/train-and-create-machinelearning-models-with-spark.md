---
title: Modelos de ML Train/criar com o Spark
titleSuffix: SQL Server big data clusters
description: Use o PySpark para treinar e criar modelos de aprendizado de máquina com o Spark em clusters de grandes dados do SQL Server (versão prévia).
author: lgongmsft
ms.author: shivprashant
ms.manager: craigg
ms.reviewer: jroth
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: b9217b56da2e00ba50288f1643df809f482c2517
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860557"
---
# <a name="train-and-create-machine-learning-models-with-spark"></a>Treinar e criar modelos de aprendizado de máquina com o Spark

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O Spark no cluster de big data do SQL Server permite que a inteligência Artificial e aprendizado de máquina. O exemplo demonstra como para treinar um modelo de aprendizado de máquina usando o Python no Spark (PySpark) usando dados armazenados em HDFS. 

O exemplo é uma guia passo a passo com os trechos de código que pode ser usado de um bloco de anotações do Studio de dados do Azure e cada etapa de uma execução de célula por vez. Para obter mais informações sobre como conectar-se com o Spark do bloco de anotações consulte [aqui](notebooks-guidance.md)

No exemplo:

1. Comece com **Noções básicas sobre os dados e a previsão desejado**
2. **Carregar dados para o HDFS e preparar os dados** para criar o modelo
3. **Selecione os recursos a serem usados**
4. **Dividir os dados como conjunto de treinamento e teste**
5. Juntar uma **pipeline ml e um modelo de compilação**
6. Use o modelo criado para **fazer previsões**
7. Como etapa final, **persistir o modelo criado para uso posterior na**.

Aprendizado de máquina E2E envolve várias etapas adicionais, por exemplo, exploração de dados, análise de componente de seleção e a entidade de segurança do recurso, seleção de modelo. Muitas dessas etapas são ignoradas aqui para fins de brevidade.

## <a name="step-1---understanding-the-data-and-prediction-desired"></a>Etapa 1: Noções básicas sobre os dados e a previsão desejado

Este exemplo usa dados de renda de censo adulto da [aqui]( https://amldockerdatasets.azureedge.net/AdultCensusIncome.csv ). No `AdultCensusIncome.csv`, cada linha representa um intervalo de renda e outras características, como idade, horas por semana, educação, ocupação etc para um determinado adulto. Criar um modelo que possa prever se o intervalo de renda. O modelo levará a idade e horas por semana, como recursos e prever se a renda seria > 50 mil ou < k 50. 

## <a name="step-2---upload-the-data-to-hdfs-and-basic-explorations-on-data"></a>Etapa 2: carregar os dados no HDFS e explorações básicas nos dados
No Studio de dados do Azure se conectar ao gateway de HDFS/Spark e crie um diretório chamado `spark_ml` em HDFS. Baixe [AdultCensusIncome.csv]( https://amldockerdatasets.azureedge.net/AdultCensusIncome.csv ) para seu computador local e o carregue no HDFS. Carregar `AdultCensusIncome.csv` para a pasta que você criou.


Agora, escreva um código. Você pode copiar o código a seguir e cole-o em células individuais de um bloco de anotações no estúdio de dados do Azure. 

O código a seguir lê o arquivo CSV para o quadro de dados do Spark. Para que ele conta o número de linhas e colunas e exibir os dados carregados.

```python
datafile = "/spark_ml/AdultCensusIncome.csv"

#Read the data to a spark data frame.
data_all = spark.read.format('csv').options(header='true', inferSchema='true', ignoreLeadingWhiteSpace='true', ignoreTrailingWhiteSpace='true').load(datafile)
print("Number of rows: {},  Number of coulumns : {}".format(data_all.count(), len(data_all.columns)))

#Replace "-" with "_" in column names
columns_new = [col.replace("-", "_") for col in data_all.columns]
data_all = data_all.toDF(*columns_new)

#Print Schema and show top 5 row
data_all.printSchema() 
data_all.show(5)
```

## <a name="step-3---select-features-to-use"></a>Etapa 3: selecionar recursos para usar

Nesta etapa, use o seguinte dois termos
1. `Label`    -Se refere ao valor a ser previsto. Isso é representado como uma coluna nos dados.  
2. `Features` -Refere-se às características nos dados para prever. Também chamado de algum tempo como `predictors` 

Neste exemplo `Label`, é o **renda** coluna. Para manter a simplicidade, escolha **idade** e **hours_per_week** como `Features`. Na realidade os recursos são escolhidos, aplicando algumas técnicas de correlação para entender o que melhor caracterizam o rótulo de previsão.

```python
# Choose feature columns and the label column.
label = "income"
xvars = ["age", "hours_per_week"] #all numeric

print("label = {}".format(label))
print("features = {}".format(xvars))

select_cols = xvars
select_cols.append(label)
data = data_all.select(select_cols)

```

## <a name="step-4---split-as-training-and-test-set"></a>Etapa 4 - dividir como conjuntos de treinamento e teste

Use a 75% das linhas para treinar o modelo e o restante dos 25% para avaliar o modelo. Além disso, persistir de treinamento e teste a conjuntos de dados para armazenamento HDFS. A etapa não é necessário, mas é mostrado para demonstrar como salvar e carregar com o formato ORC. Outros formatos, por exemplo, `Parquet` também podem ser usados.

Postar esta etapa, que você deverá ver dois diretórios criados com o nome AdultCensusIncomeTrain e AdultCensusIncomeTest

```python

# Split data into train and test.
train, test = data.randomSplit([0.75, 0.25], seed=123)

print("train ({}, {})".format(train.count(), len(train.columns)))
print("test ({}, {})".format(test.count(), len(test.columns)))

train_data_path = "/spark_ml/AdultCensusIncomeTrain"
test_data_path = "/spark_ml/AdultCensusIncomeTest"

train.write.mode('overwrite').orc(train_data_path)
test.write.mode('overwrite').orc(test_data_path)
print("train and test datasets saved to {} and {}".format(train_data_path, test_data_path))

```

## <a name="step-5---put-together-a-pipeline-and-build-a-model"></a>Etapa 5 – juntar-se de que um pipeline e criar um modelo
[Pipeline ML do Spark](https://spark.apache.org/docs/2.3.1/ml-pipeline.html) permitir todas as etapas de sequência como um fluxo de trabalho e torná-lo mais fácil de fazer experiências com vários algoritmos e seus parâmetros. O código a seguir primeiro constrói os estágios e, em seguida, reúne esses estágios no pipeline de Ml.  LogisticRegression é usado para criar o modelo.

```python
from pyspark.ml import Pipeline, PipelineModel
from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler
from pyspark.ml.classification import LogisticRegression

reg = 0.1
print("Using LogisticRegression model with Regularization Rate of {}.".format(reg))

# create a new Logistic Regression model.
lr = LogisticRegression(regParam=reg)

dtypes = dict(train.dtypes)
dtypes.pop(label)

si_xvars = []
ohe_xvars = []
featureCols = []
for idx,key in enumerate(dtypes):
    if dtypes[key] == "string":
        featureCol = "-".join([key, "encoded"])
        featureCols.append(featureCol)
        
        tmpCol = "-".join([key, "tmp"])
        si_xvars.append(StringIndexer(inputCol=key, outputCol=tmpCol, handleInvalid="skip")) #, handleInvalid="keep"
        ohe_xvars.append(OneHotEncoder(inputCol=tmpCol, outputCol=featureCol))
    else:
        featureCols.append(key)

# string-index the label column into a column named "label"
si_label = StringIndexer(inputCol=label, outputCol='label')

# assemble the encoded feature columns in to a column named "features"
assembler = VectorAssembler(inputCols=featureCols, outputCol="features")

```

Agora, juntar o pipeline. 

```python
# put together the pipeline
stages = []
stages.extend(si_xvars)
stages.extend(ohe_xvars)
stages.append(si_label)
stages.append(assembler)
stages.append(lr)
pipe = Pipeline(stages=stages)
print("Pipeline Created")

```

Agora que o pipeline é criado, use que para treinar o modelo.

```python
# train the model
model = pipe.fit(train)
print("Model Trained")
print("Model is ", model)
print("Model Stages", model.stages)

```

## <a name="step-6---predict-using-the-model-and-evaluate-the-model-accuracy"></a>Etapa 6 - usando o modelo de previsão e avaliar a precisão do modelo
O código a seguir usa o conjunto de dados de teste para prever o resultado usando o modelo criado na etapa anterior. Ele mede a precisão do modelo com `areaUnderROC` e `areaUnderPR` métrica.

```python
from pyspark.ml.evaluation import BinaryClassificationEvaluator
# make prediction
pred = model.transform(test)

# evaluate. note only 2 metrics are supported out of the box by Spark ML.
bce = BinaryClassificationEvaluator(rawPredictionCol='rawPrediction')
au_roc = bce.setMetricName('areaUnderROC').evaluate(pred)
au_prc = bce.setMetricName('areaUnderPR').evaluate(pred)

print("Area under ROC: {}".format(au_roc))
print("Area Under PR: {}".format(au_prc))
```


## <a name="step-7---persist-the-models-to-hdfs"></a>Etapa 7: manter os modelos para o HDFS
Por fim, persistir o modelo no HDFS para uso posterior. Postar esta etapa salvo o modelo criado como /spark_ml/AdultCensus.mml

```python
##NOTE: by default the model is saved to and loaded from path

model_name = "AdultCensus.mml"
model_fs = "/spark_ml/" + model_name

model.write().overwrite().save(model_fs)
print("saved model to {}".format(model_fs))

# load the model file (from dbfs)
model2 = PipelineModel.load(model_fs)
assert str(model2) == str(model)
print("loaded model from {}".format(model_fs))
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como começar com notebooks do PySpark, confira [como usar notebooks](notebooks-guidance.md).