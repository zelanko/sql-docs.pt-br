---
title: Prever resultados potenciais usando modelos Python
description: Tutorial mostrando como colocar em operação o script PYthon incorporado em SQL Server procedimentos armazenados com funções T-SQL
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/02/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: b04e57c45c6113d4a0404a3a338e6beba4cda813
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68468592"
---
# <a name="run-predictions-using-python-embedded-in-a-stored-procedure"></a>Executar previsões usando o Python Embedded em um procedimento armazenado
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo faz parte de um tutorial, [análise do Python no banco de dados para desenvolvedores do SQL](sqldev-in-database-python-for-sql-developers.md). 

Nesta etapa, você aprenderá a colocar em *operação* os modelos treinados e salvos na etapa anterior.

Nesse cenário, a operacionalização significa implantar o modelo na produção para pontuação. A integração com o SQL Server torna isso razoavelmente fácil, pois você pode inserir o código Python em um procedimento armazenado. Para obter previsões do modelo com base em novas entradas, basta chamar o procedimento armazenado de um aplicativo e passar os novos dados.

Esta lição demonstra dois métodos para criar previsões com base em um modelo Python: Pontuação de lote e pontuação linha por linha.

- **Pontuação do lote:** Para fornecer várias linhas de dados de entrada, passe uma consulta SELECT como um argumento para o procedimento armazenado. O resultado é uma tabela de observações correspondentes aos casos de entrada.
- **Pontuação individual:** Passe um conjunto de valores de parâmetro individuais como entrada.  O procedimento armazenado retorna uma única linha ou valor.

Todo o código Python necessário para pontuação é fornecido como parte dos procedimentos armazenados.

## <a name="batch-scoring"></a>Pontuação de lote

Os dois primeiros procedimentos armazenados ilustram a sintaxe básica para encapsular uma chamada de previsão de Python em um procedimento armazenado. Ambos os procedimentos armazenados exigem uma tabela de dados como entradas.

- O nome do modelo exato a ser usado é fornecido como parâmetro de entrada para o procedimento armazenado. O procedimento armazenado carrega o modelo serializado da tabela `nyc_taxi_models`de banco de dados. tabela, usando a instrução SELECT no procedimento armazenado.
- O modelo serializado é armazenado na variável `mod` do Python para processamento adicional usando o Python.
- Os novos casos que precisam ser pontuados são obtidos da [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta especificada em. `@input_data_1` Conforme os dados da consulta são lidos, as linhas são salvas no quadro de dados padrão, `InputDataSet`.
- Ambos os procedimentos armazenados usam funções `sklearn` do para calcular uma métrica de precisão, AUC (área sob curva). Métricas de precisão como AUC só podem ser geradas se você também fornecer o rótulo de destino (a coluna de _gorjeta_ ). As previsões não precisam do rótulo de destino (variável `y`), mas o cálculo da métrica de precisão faz.

    Portanto, se você não tiver rótulos de destino para os dados a serem pontuados, poderá modificar o procedimento armazenado para remover os cálculos de auc e retornar apenas as probabilidades de gorjeta dos recursos (variável `X` no procedimento armazenado).

### <a name="predicttipscikitpy"></a>PredictTipSciKitPy

Rrun as seguintes instruções T-SQL para criar os procedimentos armazenados. Esse procedimento armazenado requer um modelo baseado no pacote scikit-learn, pois ele usa funções específicas para esse pacote:

+ O quadro de dados que contém entradas é passado `predict_proba` para a função do modelo de regressão `mod`logística,. A `predict_proba` função (`probArray = mod.predict_proba(X)`) retorna um **float** que representa a probabilidade de que uma Tip (de qualquer valor) seja fornecida.

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

Esse procedimento armazenado usa as mesmas entradas e cria o mesmo tipo de pontuações que o procedimento armazenado anterior, mas usa funções do pacote **revoscalepy** fornecido com SQL Server Machine Learning.

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

- A consulta que recupera os dados para Pontuação
- O nome de um modelo treinado

Ao passar esses argumentos para o procedimento armazenado, você pode selecionar um modelo específico ou alterar os dados usados para pontuação.

1. Para usar o modelo **scikit-Learn** para pontuação, chame o procedimento armazenado **PredictTipSciKitPy**, passando o nome do modelo e a cadeia de caracteres de consulta como entradas.

    ```sql
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipSciKitPy] 'SciKit_model', @query_string;
    ```

    O procedimento armazenado retorna probabilidades previstas para cada viagem passada como parte da consulta de entrada. 
    
    Se você estiver usando o SSMS (SQL Server Management Studio) para executar consultas, as probabilidades serão exibidas como uma tabela no painel de **resultados** . O painel **mensagens** gera a métrica de precisão (AUC ou área abaixo da curva) com um valor de cerca de 0,56.

2. Para usar o modelo **revoscalepy** para pontuação, chame o procedimento armazenado **PredictTipRxPy**, passando o nome do modelo e a cadeia de caracteres de consulta como entradas.

    ```sql
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipRxPy] 'revoscalepy_model', @query_string;
    ```

## <a name="single-row-scoring"></a>Pontuação de linha única

Às vezes, em vez de Pontuação de lote, você pode querer passar um único caso, obter valores de um aplicativo e retornar um único resultado com base nesses valores. Por exemplo, você pode configurar uma planilha do Excel, um aplicativo Web ou um relatório para chamar o procedimento armazenado e passá-lo para entradas digitadas ou selecionadas por usuários.

Nesta seção, você aprenderá a criar previsões únicas chamando dois procedimentos armazenados:

+ [PredictTipSingleModeSciKitPy](#predicttipsinglemodescikitpy) é projetado para Pontuação de linha única usando o modelo scikit-learn.
+ [PredictTipSingleModeRxPy](#predicttipsinglemoderxpy) é projetado para a pontuação de linha única usando o modelo revoscalepy.
+ Se você ainda não tiver treinado um modelo, volte para a [etapa 5](sqldev-py5-train-and-save-a-model-using-t-sql.md)!

Ambos os modelos utilizam como entrada uma série de valores únicos, como contagem de passageiro, distância de corrida e assim por diante. Uma função com valor de tabela `fnEngineerFeatures`,, é usada para converter os valores de latitude e longitude das entradas em um novo recurso, a distância direta. A [lição 4](sqldev-py4-create-data-features-using-t-sql.md) contém uma descrição dessa função com valor de tabela.

Ambos os procedimentos armazenados criam uma pontuação com base no modelo Python.

> [!NOTE]
> 
> É importante que você forneça todos os recursos de entrada exigidos pelo modelo Python ao chamar o procedimento armazenado de um aplicativo externo. Para evitar erros, pode ser necessário converter ou converter os dados de entrada em um tipo de dados do Python, além de validar o tipo de dados e o comprimento dos dados.

### <a name="predicttipsinglemodescikitpy"></a>PredictTipSingleModeSciKitPy

Reserve um minuto para examinar o código do procedimento armazenado que executa a pontuação usando o modelo **scikit-Learn** .

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

O procedimento armazenado a seguir executa a pontuação usando o modelo **revoscalepy** .

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

Depois que os procedimentos armazenados tiverem sido criados, será fácil gerar uma pontuação com base em qualquer um dos modelos. Basta abrir uma nova janela de **consulta** e digitar ou colar parâmetros para cada uma das colunas de recurso. Os sete valores necessários são para essas colunas de recursos, na ordem:
    
+ *passenger_count*
+ *trip_distance* v*trip_time_in_secs*
+ *pickup_latitude*
+ *pickup_longitude*
+ *dropoff_latitude*
+ *dropoff_longitude*

1. Para gerar uma previsão usando o modelo **revoscalepy** , execute esta instrução:
  
    ```sql
    EXEC [dbo].[PredictTipSingleModeRxPy] 'revoscalepy_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

2. Para gerar uma pontuação usando o modelo **scikit-Learn** , execute esta instrução:

    ```sql
    EXEC [dbo].[PredictTipSingleModeSciKitPy] 'SciKit_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

A saída de ambos os procedimentos é uma probabilidade de uma gorjeta ser paga pela viagem de táxi com os parâmetros ou recursos especificados.

## <a name="conclusions"></a>Conclusões

Neste tutorial, você aprendeu a trabalhar com o código Python inserido em procedimentos armazenados. A integração com [!INCLUDE[tsql](../../includes/tsql-md.md)] o torna muito mais fácil implantar modelos Python para previsão e incorporar o retreinamento de modelos como parte de um fluxo de trabalho de dados corporativos.

## <a name="previous-step"></a>Etapa anterior

[Treinar e salvar um modelo Python](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="see-also"></a>Confira também

[Extensão do Python no SQL Server](../concepts/extension-python.md)
