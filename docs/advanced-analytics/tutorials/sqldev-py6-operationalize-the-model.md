---
title: Prever resultados possíveis usando modelos do Python - aprendizagem de máquina do SQL Server
description: Tutorial que mostra como colocar o script de PYthon incorporado no SQL Server em procedimentos armazenados com funções T-SQL
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/02/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: e5f88beb2c429091fcea8ce66e4defa291e718d6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961841"
---
# <a name="run-predictions-using-python-embedded-in-a-stored-procedure"></a>Execute previsões usando Python inserido em um procedimento armazenado
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo faz parte de um tutorial [análise de Python no banco de dados para desenvolvedores do SQL](sqldev-in-database-python-for-sql-developers.md). 

Nesta etapa, você aprenderá a *operacionalizar* os modelos treinados e salvo na etapa anterior.

Nesse cenário, a operacionalização significa implantar o modelo em produção para pontuação. A integração com o SQL Server torna isso muito fácil, porque você pode incorporar código Python em um procedimento armazenado. Para obter previsões do modelo com base em novas entradas, basta chamar o procedimento armazenado de um aplicativo e passar os novos dados.

Esta lição demonstra dois métodos para criar previsões com base em um modelo de Python: pontuação e a linha por linha de pontuação do lote.

- **Pontuação do lote:** Para fornecer várias linhas de dados de entrada, passe uma consulta SELECT como um argumento para o procedimento armazenado. O resultado é uma tabela de observações correspondente aos casos de entrada.
- **Indivíduo de pontuação:** Passe um conjunto de valores de parâmetro individuais como entrada.  O procedimento armazenado retorna uma única linha ou valor.

Todo o código de Python necessário para a pontuação é fornecido como parte dos procedimentos armazenados.

## <a name="batch-scoring"></a>Pontuação do lote

Os primeiros dois procedimentos armazenados ilustram a sintaxe básica para encapsular uma chamada de previsão de Python em um procedimento armazenado. Ambos os procedimentos armazenados exigem uma tabela de dados como entradas.

- O nome do modelo exato para usar é fornecido como parâmetro de entrada para o procedimento armazenado. O procedimento armazenado carrega o modelo serializado da tabela de banco de dados `nyc_taxi_models`.table, usando a instrução SELECT no procedimento armazenado.
- O modelo serializado é armazenado na variável Python `mod` para processamento adicional usando o Python.
- Os novos casos que precisam ser pontuados são obtidos a partir de [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta especificada no `@input_data_1`. Conforme os dados da consulta são lidos, as linhas são salvas no quadro de dados padrão, `InputDataSet`.
- Ambos os procedimento armazenado usar funções de `sklearn` para calcular uma métrica de precisão, AUC (área sob a curva). Métricas de precisão, como AUC só podem ser geradas se você fornecer também o rótulo de destino (o _tipped_ coluna). Previsões não é necessário o rótulo de destino (variável `y`), mas não o cálculo de métricas de precisão.

    Portanto, se você não tem rótulos de destino para os dados a serem pontuados, você pode modificar o procedimento armazenado para remover os cálculos de AUC e retornar apenas as probabilidades de dica de recursos (variável `X` no procedimento armazenado).

### <a name="predicttipscikitpy"></a>PredictTipSciKitPy

Instruções de Rrun o T-SQL a seguir para criar os procedimentos armazenados. Este procedimento armazenado exige um modelo baseado no scikit-Saiba o pacote, pois ela usa funções específicas para que o pacote:

+ O quadro de dados que contém entradas é passado para o `predict_proba` função do modelo de regressão logística, `mod`. O `predict_proba` função (`probArray = mod.predict_proba(X)`) retorna um **float** que representa a probabilidade de que você terá uma dica (de qualquer valor).

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

Esse procedimento armazenado usa as mesmas entradas e cria o mesmo tipo de pontuações que o procedimento armazenado anterior, mas usa funções a partir de **revoscalepy** pacote fornecido com o aprendizado de máquina do SQL Server.

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

## <a name="run-batch-scoring-using-a-select-query"></a>Executar a pontuação de lote usando uma consulta SELECT

Os procedimentos armazenados **PredictTipSciKitPy** e **PredictTipRxPy** exigem dois parâmetros de entrada: 

- A consulta que recupera os dados de pontuação
- O nome de um modelo treinado

Ao passar esses argumentos para o procedimento armazenado, você pode selecionar um modelo específico ou alterar os dados usados para pontuação.

1. Para usar o **scikit-Saiba** do modelo de pontuação, chame o procedimento armazenado **PredictTipSciKitPy**, passando o nome do modelo e a cadeia de caracteres de consulta como entradas.

    ```sql
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipSciKitPy] 'SciKit_model', @query_string;
    ```

    O procedimento armazenado retorna as probabilidades previstas para cada corrida que foi passada como parte da consulta de entrada. 
    
    Se você estiver usando o SSMS (SQL Server Management Studio) para a execução de consultas, as probabilidades serão exibido como uma tabela na **resultados** painel. O **mensagens** painel produz a métrica de precisão (área sob a curva ou AUC) com um valor de aproximadamente 0.56.

2. Para usar o **revoscalepy** do modelo de pontuação, chame o procedimento armazenado **PredictTipRxPy**, passando o nome do modelo e a cadeia de caracteres de consulta como entradas.

    ```sql
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipRxPy] 'revoscalepy_model', @query_string;
    ```

## <a name="single-row-scoring"></a>Uma única linha de pontuação

Às vezes, em vez de pontuação em lote, você talvez queira passar em um único caso, obtendo valores de um aplicativo e retornar um único resultado com base nesses valores. Por exemplo, você pode configurar um Excel planilha, aplicativo web ou relatório para chamar o procedimento armazenado e passe para ele entradas digitadas ou selecionadas por usuários.

Nesta seção, você aprenderá a criar previsões únicas chamando dois procedimentos armazenados:

+ [PredictTipSingleModeSciKitPy](#predicttipsinglemodescikitpy) foi projetado para uma única linha de pontuação usando o scikit-aprender o modelo.
+ [PredictTipSingleModeRxPy](#predicttipsinglemoderxpy) foi projetado para uma única linha de pontuação usando o modelo revoscalepy.
+ Se você ainda não tiver um modelo treinado ainda, retorne ao [etapa 5](sqldev-py5-train-and-save-a-model-using-t-sql.md)!

Take ambos os modelos como entrada uma série de valores únicos, como contagem de passageiros, distância da corrida e assim por diante. Uma função com valor de tabela, `fnEngineerFeatures`, é usado para converter valores de latitude e longitude de entradas para um novo recurso, a distância direta. [Lição 4](sqldev-py4-create-data-features-using-t-sql.md) contém uma descrição dessa função com valor de tabela.

Ambos os procedimentos armazenados criam uma pontuação com base no modelo de Python.

> [!NOTE]
> 
> É importante que você forneça todos os recursos de entrada exigidos pelo modelo Python quando você chama o procedimento armazenado de um aplicativo externo. Para evitar erros, talvez você precise converter os dados de entrada para um tipo de dados do Python, além de validação do tipo e comprimento de dados.

### <a name="predicttipsinglemodescikitpy"></a>PredictTipSingleModeSciKitPy

Reserve um minuto para examinar o código do procedimento armazenado que executa a pontuação usando o **scikit-Saiba** modelo.

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

O seguinte procedimento armazenado executa a pontuação usando o **revoscalepy** modelo.

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

Depois que os procedimentos armazenados foram criados, é fácil gerar uma pontuação com base em qualquer um dos modelos. Basta abrir uma nova **consulta** janela e digite ou cole parâmetros para cada uma das colunas de recursos. As sete necessários são de valores para essas colunas de recurso, na ordem:
    
+ *passenger_count*
+ *trip_distance* v*trip_time_in_secs*
+ *pickup_latitude*
+ *pickup_longitude*
+ *dropoff_latitude*
+ *dropoff_longitude*

1. Para gerar uma previsão usando o **revoscalepy** modelo, execute esta instrução:
  
    ```sql
    EXEC [dbo].[PredictTipSingleModeRxPy] 'revoscalepy_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

2. Para gerar uma pontuação usando o **scikit-Saiba** modelo, execute esta instrução:

    ```sql
    EXEC [dbo].[PredictTipSingleModeSciKitPy] 'SciKit_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

A saída de ambos os procedimentos é uma probabilidade de uma dica que está sendo paga para a viagem de táxi com os parâmetros especificados ou recursos.

## <a name="conclusions"></a>Conclusões

Neste tutorial, você aprendeu como trabalhar com o código Python inserido em procedimentos armazenados. A integração com o [!INCLUDE[tsql](../../includes/tsql-md.md)] torna muito mais fácil para implantar modelos em Python para previsão e incorporar a reciclagem de modelos como parte de um fluxo de trabalho de dados empresariais.

## <a name="previous-step"></a>Etapa anterior

[Treinar e salvar um modelo de Python](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="see-also"></a>Confira também

[Extensão do Python no SQL Server](../concepts/extension-python.md)
