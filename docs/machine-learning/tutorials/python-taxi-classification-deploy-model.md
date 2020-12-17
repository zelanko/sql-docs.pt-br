---
title: 'Tutorial do Python: executar previsões nos procedimentos armazenados do SQL'
titleSuffix: SQL machine learning
description: Na quinta parte desta série de tutoriais em cinco partes, você operacionalizará o script Python incorporado em procedimentos armazenados do SQL com as funções do T-SQL e o aprendizado de máquina do SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/29/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||>=azuresqldb-mi-current'
ms.openlocfilehash: 4e101a017197d83217a574ca6521dd60328f536a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470327"
---
# <a name="python-tutorial-run-predictions-using-python-embedded-in-a-stored-procedure"></a>Tutorial do Python: Executar previsões usando o Python inserido em um procedimento armazenado
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

Na quinta parte desta série de tutoriais em cinco partes, você aprenderá a *operacionalizar* os modelos treinados e salvos na parte anterior.

Nesse cenário, operacionalização significa implantar o modelo em produção para pontuação. A integração ao SQL Server torna isso razoavelmente fácil, pois você pode inserir o código Python em um procedimento armazenado. Para obter previsões do modelo com base em novas entradas, basta chamar o procedimento armazenado de um aplicativo e passar os novos dados.

Esta parte do tutorial demonstra dois métodos para criar previsões com base em um modelo do Python: pontuação em lote e pontuação linha a linha.

+ **Pontuação do lote:** para fornecer várias linhas de dados de entrada, passe uma consulta SELECT como um argumento para o procedimento armazenado. O resultado é uma tabela de observações correspondentes aos casos de entrada.
+ **Pontuação individual:** Passe um conjunto de valores de parâmetro individuais como entrada.  O procedimento armazenado retorna uma única linha ou valor.

todo o código Python necessário para pontuação é fornecido como parte dos procedimentos armazenados.

Neste artigo, você vai:

> [!div class="checklist"]
> + Criar e usar procedimentos armazenados para executar a pontuação em lote
> + Criar e usar procedimentos armazenados para executar a pontuação em uma única linha

Na [parte um](python-taxi-classification-introduction.md), você instalou os pré-requisitos e restaurou o banco de dados de exemplo.

Na [parte dois](python-taxi-classification-explore-data.md), você explorou os dados de exemplo e gerou alguns gráficos.

Na [parte três](python-taxi-classification-create-features.md), você aprendeu a criar recursos a partir de dados brutos usando uma função do Transact-SQL. Você chamou essa função por meio de um procedimento armazenado para criar uma tabela que continha os valores de recurso.

Na [parte quatro](python-taxi-classification-train-model.md), você carregou os módulos e chamou as funções necessárias para criar e treinar o modelo usando um procedimento armazenado do SQL Server.

## <a name="batch-scoring"></a>Pontuação do lote

Os dois primeiros procedimentos armazenados ilustram a sintaxe básica para encapsular uma chamada de previsão do Python em um procedimento armazenado. Ambos os procedimentos armazenados exigem uma tabela de dados como entradas.

+ O nome do modelo exato a ser usado é fornecido como parâmetro de entrada para o procedimento armazenado. O procedimento armazenado carrega o modelo serializado da tabela de banco de dados `nyc_taxi_models`.table usando a instrução SELECT no procedimento armazenado.
+ O modelo serializado é armazenado na variável do Python `mod` para processamento adicional usando o Python.
+ Os novos casos que precisam ser pontuados são obtidos da consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] especificada em `@input_data_1`. Conforme os dados da consulta são lidos, as linhas são salvas no quadro de dados padrão, `InputDataSet`.
+ Ambos os procedimentos armazenados usam funções de `sklearn` para calcular uma métrica de precisão, AUC (área sob curva). As métricas de precisão, como AUC, só podem ser geradas se você também fornecer o rótulo de destino (a coluna _gorjeta dada_). As previsões não precisam do rótulo de destino (variável `y`), mas o cálculo da métrica de precisão precisa.

  Portanto, se você não tiver rótulos de destino para os dados a serem pontuados, poderá modificar o procedimento armazenado para remover os cálculos de AUC e retornar apenas as probabilidades de gorjeta dos recursos (variável `X` no procedimento armazenado).

### <a name="predicttipscikitpy"></a>PredictTipSciKitPy

Execute as instruções do T-SQL a seguir para criar os procedimentos armazenados. Este procedimento armazenado exige um modelo baseado no pacote scikit-learn, pois usa funções específicas para o pacote.

O quadro de dados que contém entradas é passado para a função `predict_proba` do modelo de regressão logística, `mod`. A função `predict_proba` (`probArray = mod.predict_proba(X)`) retorna um **float** que representa a probabilidade de uma gorjeta ser dada (de qualquer valor).

```sql
DROP PROCEDURE IF EXISTS PredictTipSciKitPy;
GO

CREATE PROCEDURE [dbo].[PredictTipSciKitPy] (@model varchar(50), @inquery nvarchar(max))
AS
BEGIN
DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models where name = @model);
EXEC sp_execute_external_script
  @language = N'Python',
  @script = N'
import pickle;
import numpy;
from sklearn import metrics

mod = pickle.loads(lmodel2)
X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
y = numpy.ravel(InputDataSet[["tipped"]])

probArray = mod.predict_proba(X)
probList = []
for i in range(len(probArray)):
  probList.append((probArray[i])[1])

probArray = numpy.asarray(probList)
fpr, tpr, thresholds = metrics.roc_curve(y, probArray)
aucResult = metrics.auc(fpr, tpr)
print ("AUC on testing data is: " + str(aucResult))

OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
',  
  @input_data_1 = @inquery,
  @input_data_1_name = N'InputDataSet',
  @params = N'@lmodel2 varbinary(max)',
  @lmodel2 = @lmodel2
WITH RESULT SETS ((Score float));
END
GO
```

### <a name="predicttiprxpy"></a>PredictTipRxPy

Esse procedimento armazenado usa as mesmas entradas e cria o mesmo tipo de pontuação que o procedimento armazenado anterior, mas usa funções do pacote **revoscalepy** fornecido com o aprendizado de máquina do SQL Server.

```sql
DROP PROCEDURE IF EXISTS PredictTipRxPy;
GO

CREATE PROCEDURE [dbo].[PredictTipRxPy] (@model varchar(50), @inquery nvarchar(max))
AS
BEGIN
DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models where name = @model);
EXEC sp_execute_external_script 
  @language = N'Python',
  @script = N'
import pickle;
import numpy;
from sklearn import metrics
from revoscalepy.functions.RxPredict import rx_predict;

mod = pickle.loads(lmodel2)
X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
y = numpy.ravel(InputDataSet[["tipped"]])

probArray = rx_predict(mod, X)
probList = probArray["tipped_Pred"].values 

probArray = numpy.asarray(probList)
fpr, tpr, thresholds = metrics.roc_curve(y, probArray)
aucResult = metrics.auc(fpr, tpr)
print ("AUC on testing data is: " + str(aucResult))

OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
',
  @input_data_1 = @inquery,
  @input_data_1_name = N'InputDataSet',
  @params = N'@lmodel2 varbinary(max)',
  @lmodel2 = @lmodel2
WITH RESULT SETS ((Score float));
END
GO
```

## <a name="run-batch-scoring-using-a-select-query"></a>Executar pontuação em lote usando uma consulta SELECT

Os procedimentos armazenados **PredictTipSciKitPy** e **PredictTipRxPy** exigem dois parâmetros de entrada:

+ A consulta que recupera os dados para pontuação
+ O nome de um modelo treinado

Ao passar esses argumentos para o procedimento armazenado, você pode selecionar um modelo específico ou alterar os dados usados para pontuação.

1. Para usar o modelo **Scikit-learn** para pontuação, chame o procedimento armazenado **PredictTipSciKitPy**, passando o nome do modelo e a cadeia de consulta como entradas.

   ```sql
   DECLARE @query_string nvarchar(max) -- Specify input query
     SET @query_string='
     select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
     dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
     from nyctaxi_sample_testing'
   EXEC [dbo].[PredictTipSciKitPy] 'SciKit_model', @query_string;
   ```

   O procedimento armazenado retorna probabilidades previstas para cada corrida passada como parte da consulta de entrada. 

   Se você estiver usando o SSMS (SQL Server Management Studio) para executar consultas, as probabilidades serão exibidas como uma tabela no painel **Resultados**. O painel **Mensagens** gera a métrica de precisão (AUC ou área sob a curva) com um valor de cerca de 0,56.

2. Para usar o modelo **revoscalepy** para pontuação, chame o procedimento armazenado **PredictTipRxPy**, passando o nome do modelo e a cadeia de consulta como entradas.

   ```sql
   DECLARE @query_string nvarchar(max) -- Specify input query
     SET @query_string='
     select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
     dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
     from nyctaxi_sample_testing'
   EXEC [dbo].[PredictTipRxPy] 'revoscalepy_model', @query_string;
   ```

## <a name="single-row-scoring"></a>Pontuação de uma única linha

Às vezes, em vez de pontuação de lote, você pode querer passar um único caso, obtendo valores de um aplicativo e retornando um único resultado com base nesses valores. Por exemplo, você poderá definir uma planilha do Excel, um aplicativo Web ou um relatório para chamar o procedimento armazenado e passá-lo a ele entradas digitadas ou selecionadas por usuários.

Nesta seção, você aprenderá a criar previsões únicas chamando dois procedimentos armazenados:

+ [PredictTipSingleModeSciKitPy](#predicttipsinglemodescikitpy) foi projetado para a pontuação de uma única linha usando o modelo Scikit-learn.
+ [PredictTipSingleModeRxPy](#predicttipsinglemoderxpy) foi projetado para a pontuação de uma única linha usando o modelo revoscalepy.
+ Se você ainda não tiver treinado um modelo, volte para [parte 5](python-taxi-classification-train-model.md).

Ambos os modelos utilizam como entrada uma série de valores únicos, como contagem de passageiros, distância da corrida e assim por diante. Uma função com valor de tabela, `fnEngineerFeatures`, é usada para converter valores de latitude e longitude das entradas em um novo recurso, distância direta. A [parte quatro](python-taxi-classification-create-features.md) contém uma descrição dessa função com valor de tabela.

Ambos os procedimentos armazenados criam uma pontuação com base no modelo do Python.

> [!NOTE]
>
> É importante que você forneça todos os recursos de entrada exigidos pelo modelo do Python ao chamar o procedimento armazenado a partir de um aplicativo externo. Para evitar erros, pode ser necessário converter os dados de entrada em um tipo de dados do Python, além de validar o tipo de dados e o comprimento dos dados.

### <a name="predicttipsinglemodescikitpy"></a>PredictTipSingleModeSciKitPy

Reserve um minuto para examinar o código do procedimento armazenado que executa a pontuação usando o modelo **Scikit-learn**.

```sql
DROP PROCEDURE IF EXISTS PredictTipSingleModeSciKitPy;
GO

CREATE PROCEDURE [dbo].[PredictTipSingleModeSciKitPy] (@model varchar(50), @passenger_count int = 0,
  @trip_distance float = 0,
  @trip_time_in_secs int = 0,
  @pickup_latitude float = 0,
  @pickup_longitude float = 0,
  @dropoff_latitude float = 0,
  @dropoff_longitude float = 0)
AS
BEGIN
  DECLARE @inquery nvarchar(max) = N'
  SELECT * FROM [dbo].[fnEngineerFeatures]( 
    @passenger_count,
    @trip_distance,
    @trip_time_in_secs,
    @pickup_latitude,
    @pickup_longitude,
    @dropoff_latitude,
    @dropoff_longitude)
    '
DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models where name = @model);
EXEC sp_execute_external_script 
  @language = N'Python',
  @script = N'
import pickle;
import numpy;

# Load model and unserialize
mod = pickle.loads(model)

# Get features for scoring from input data
X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]

# Score data to get tip prediction probability as a list (of float)
probList = []
probList.append((mod.predict_proba(X)[0])[1])

# Create output data frame
OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
',
  @input_data_1 = @inquery,
  @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,
    @trip_time_in_secs int ,
    @pickup_latitude float ,
    @pickup_longitude float ,
    @dropoff_latitude float ,
    @dropoff_longitude float',
    @model = @lmodel2,
    @passenger_count =@passenger_count ,
    @trip_distance=@trip_distance,
    @trip_time_in_secs=@trip_time_in_secs,
    @pickup_latitude=@pickup_latitude,
    @pickup_longitude=@pickup_longitude,
    @dropoff_latitude=@dropoff_latitude,
    @dropoff_longitude=@dropoff_longitude
WITH RESULT SETS ((Score float));
END
GO
```

### <a name="predicttipsinglemoderxpy"></a>PredictTipSingleModeRxPy

O procedimento armazenado a seguir executa a pontuação usando o modelo **revoscalepy**.

```sql
DROP PROCEDURE IF EXISTS PredictTipSingleModeRxPy;
GO

CREATE PROCEDURE [dbo].[PredictTipSingleModeRxPy] (@model varchar(50), @passenger_count int = 0,
  @trip_distance float = 0,
  @trip_time_in_secs int = 0,
  @pickup_latitude float = 0,
  @pickup_longitude float = 0,
  @dropoff_latitude float = 0,
  @dropoff_longitude float = 0)
AS
BEGIN
DECLARE @inquery nvarchar(max) = N'
  SELECT * FROM [dbo].[fnEngineerFeatures]( 
    @passenger_count,
    @trip_distance,
    @trip_time_in_secs,
    @pickup_latitude,
    @pickup_longitude,
    @dropoff_latitude,
    @dropoff_longitude)
  '
DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models where name = @model);
EXEC sp_execute_external_script 
  @language = N'Python',
  @script = N'
import pickle;
import numpy;
from revoscalepy.functions.RxPredict import rx_predict;

# Load model and unserialize
mod = pickle.loads(model)

# Get features for scoring from input data
X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]

# Score data to get tip prediction probability as a list (of float)

probArray = rx_predict(mod, X)

probList = []
probList = probArray["tipped_Pred"].values

# Create output data frame
OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
',
  @input_data_1 = @inquery,
  @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,
    @trip_time_in_secs int ,
    @pickup_latitude float ,
    @pickup_longitude float ,
    @dropoff_latitude float ,
    @dropoff_longitude float',
    @model = @lmodel2,
    @passenger_count =@passenger_count ,
    @trip_distance=@trip_distance,
    @trip_time_in_secs=@trip_time_in_secs,
    @pickup_latitude=@pickup_latitude,
    @pickup_longitude=@pickup_longitude,
    @dropoff_latitude=@dropoff_latitude,
    @dropoff_longitude=@dropoff_longitude
WITH RESULT SETS ((Score float));
END
GO
```

### <a name="generate-scores-from-models"></a>Gerar pontuações de modelos

Depois da criação dos procedimentos armazenados, é fácil gerar uma pontuação com base em qualquer um dos modelos. Basta abrir uma nova janela de **Consulta** e digitar ou colar os parâmetros para cada uma das colunas do recurso. Os sete valores obrigatórios são para essas colunas de recursos, na ordem:

+ *passenger_count*
+ *trip_distance*
+ *trip_time_in_secs*
+ *pickup_latitude*
+ *pickup_longitude*
+ *dropoff_latitude*
+ *dropoff_longitude*

1. Para gerar uma previsão usando o modelo **revoscalepy**, execute esta instrução:
  
   ```sql
   EXEC [dbo].[PredictTipSingleModeRxPy] 'revoscalepy_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
   ```

2. Para gerar uma pontuação usando o modelo **Scikit-Learn**, execute esta instrução:

   ```sql
   EXEC [dbo].[PredictTipSingleModeSciKitPy] 'SciKit_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
   ```

A saída de ambos os procedimentos é uma probabilidade de uma gorjeta ser paga pela corrida de táxi com os parâmetros ou recursos especificados.

## <a name="conclusions"></a>Conclusões

Nesta série de tutoriais, você aprendeu a trabalhar com código do Python integrado em procedimentos armazenados. A integração com o [!INCLUDE[tsql](../../includes/tsql-md.md)] torna muito mais fácil a implantação de modelos do Python para previsão e incorporação do novo treinamento do modelo como parte de um fluxo de trabalho de dados empresariais.

## <a name="next-steps"></a>Próximas etapas

Neste artigo você:

> [!div class="checklist"]
> + Criou e usou procedimentos armazenados para executar a pontuação em lote
> + Criou e usou procedimentos armazenados para executar a pontuação em uma única linha

Confira mais informações sobre o Python em [Extensão do Python no SQL Server](../concepts/extension-python.md).
