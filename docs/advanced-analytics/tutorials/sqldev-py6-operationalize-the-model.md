---
title: 'Etapa 6: Colocar o modelo | Microsoft Docs'
ms.custom: 
ms.date: 05/25/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- python-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b33f3876f054d7e7150a18967d5cfa37dd2d82bf
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="step-6-operationalize-the-model"></a>Etapa 6: Colocar o modelo em operação

Nesta etapa, você aprenderá a *operacionalizar* os modelos treinados e salvo na etapa anterior. Nesse caso colocar significa "implantação do modelo para a produção de pontuação". Isso é fácil se seu código Python está contido em um procedimento armazenado. Em seguida, você pode chamar o procedimento armazenado de aplicativos, para fazer previsões sobre novos observações.

Você aprenderá dois métodos para chamar um modelo de Python de um procedimento armazenado:

- **Modo de pontuação de lote**: use uma consulta SELECT para fornecer várias linhas de dados. O procedimento armazenado retorna uma tabela de observações correspondente aos casos de entrada.
- **Modo de pontuação individual**: passe um conjunto de valores de parâmetros individuais como entrada.  O procedimento armazenado retorna uma única linha ou valor.

## <a name="scoring-using-the-scikit-learn-model"></a>Pontuação usando o scikit-Saiba modelo

O procedimento armazenado _PredictTipSciKitPy_ usa o scikit-aprender o modelo. Esse procedimento armazenado ilustra a sintaxe básica para quebra automática de uma chamada de previsão Python em um procedimento armazenado.

- O nome do modelo para usar é fornecido como parâmetro de entrada para o procedimento armazenado. 
- O procedimento armazenado, em seguida, carregará o modelo serializado da tabela de banco de dados `nyc_taxi_models`.table, usando a instrução SELECT no procedimento armazenado.
- O modelo serializado é armazenado na variável Python `mod` para processamento adicional usando Python.
- Os novos casos que precisam ser classificados são obtidos de [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta especificada no `@input_data_1`. Conforme os dados da consulta são lidos, as linhas são salvas no quadro de dados padrão, `InputDataSet`.
- Este quadro de dados é passado para o `predict_proba` função do modelo de regressão logística, `mod`, que foi criado usando scikit-aprender o modelo. 
- O `predict_proba` função (`probArray = mod.predict_proba(X)`) retorna um **float** que representa a probabilidade de que você terá uma dica (de qualquer valor).
- O procedimento armazenado também calcula uma métrica de exatidão, AUC (área sob a curva). Métricas de precisão, como AUC só podem ser geradas se você fornecer também o rótulo de destino (ou seja, a coluna Oblíquo). Previsões não é necessário o rótulo de destino (variável `y`), mas não o cálculo de métricas de precisão.

  Portanto, se você não tem rótulos de destino para os dados a ser pontuado, você pode modificar o procedimento armazenado para remover os cálculos AUC e simplesmente retornar as probabilidades de dica de recursos (variável `X` no procedimento armazenado).

```SQL
CREATE PROCEDURE [dbo].[PredictTipSciKitPy] (@model varchar(50), @inquery nvarchar(max))
AS
BEGIN
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models where name = @model);
  EXEC sp_execute_external_script
    @language = N'Python',
    @script = N'
        import pickle;
        import numpy;
        import pandas;
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

## <a name="scoring-using-the-revoscalepy-model"></a>Usando o modelo de revoscalepy de pontuação

O procedimento armazenado _PredictTipRxPy_ usa um modelo que foi criado usando o **revoscalepy** biblioteca. Ele funciona da mesma maneira que o _PredictTipSciKitPy_ procedimento, mas com algumas alterações para o **revoscalepy** funções.

```SQL
CREATE PROCEDURE [dbo].[PredictTipRxPy] (@model varchar(50), @inquery nvarchar(max))
AS
BEGIN
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models2 where name = @model);
  
  EXEC sp_execute_external_script 
    @language = N'Python',
    @script = N'
      import pickle;
      import numpy;
      import pandas;
      from sklearn import metrics
      from revoscalepy.functions.RxPredict import rx_predict_ex;
      
      mod = pickle.loads(lmodel2)
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      y = numpy.ravel(InputDataSet[["tipped"]])
      
      probArray = rx_predict_ex(mod, X)
      probList = []
      for i in range(len(probArray._results["tipped_Pred"])):
        probList.append((probArray._results["tipped_Pred"][i]))
      
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

## <a name="batch-scoring-using-a-select-query"></a>Pontuação de lote usando uma consulta SELECT

Os procedimentos armazenados **PredictTipSciKitPy** e **PredictTipRxPy** exigem dois parâmetros de entrada: 

- A consulta que recupera os dados de pontuação
- O nome de um modelo treinado

Nesta seção, você aprenderá como passar os argumentos para o procedimento armazenado para alterar facilmente o modelo e os dados usados para pontuação.

1. Definir os dados de entrada e chamar os procedimentos armazenados para pontuação da seguinte maneira. Este exemplo usa o procedimento armazenado PredictTipSciKitPy para pontuação e passa o nome do modelo e uma cadeia de caracteres de consulta

    ```SQL
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipSciKitPy] 'SciKit_model', @query_string;
    ```

    O procedimento armazenado retorna as probabilidades previstas para cada viagem que foi passada como parte da consulta de entrada. Se você estiver usando o SSMS (SQL Server Management Studio) para executar consultas, as probabilidades aparecerá como uma tabela no **resultados** painel. O **mensagens** painel produz a métrica de exatidão (AUC ou área na curva) com um valor de aproximadamente 0.56.

2. Para usar o **revoscalepy** do modelo de pontuação, chame o procedimento armazenado **PredictTipRxPy**, passando a cadeia de caracteres de nome e consulta de modelo.

    ```SQL
    EXEC [dbo].[PredictTipRxPy] 'revoscalepy_model', @query_string;
    ```

## <a name="score-individual-rows-using-scikit-learn-model"></a>Classificar linhas individuais usando scikit-Saiba modelo

Às vezes, em vez de pontuação de lote, você pode desejar transmitir um único caso, obtendo valores de um aplicativo e obter um único resultado com base nesses valores. Por exemplo, você poderá definir uma planilha do Excel, um aplicativo Web ou um relatório do Reporting Services para chamar o procedimento armazenado e fornecer entradas digitadas ou selecionadas por usuários.

Nesta seção, você aprenderá a criar previsões únicas chamando um procedimento armazenado.

1. Reserve um minuto para examinar o código de procedimentos armazenados [PredictTipSingleModeSciKitPy](#PredictTipSingleModeSciKitPy) e [PredictTipSingleModeRxPy](#PredictTipSingleModeRxPy), que são incluídos como parte do download. Esses procedimentos armazenados, use o scikit-Saiba mais e revoscalepy modelos e executar a pontuação da seguinte maneira:

  - Nome do modelo e vários valores únicos são fornecidos como entrada. Essas entradas incluem contagem de passageiro, distância de viagem e assim por diante.
  - Uma função com valor de tabela, `fnEngineerFeatures`, usa valores de entrada e converte o latitudes e longitudes para direcionar a distância. [Lição 4](sqldev-py4-create-data-features-using-t-sql.md) contém uma descrição dessa função com valor de tabela.
  - Se você chamar o procedimento armazenado de um aplicativo externo, certifique-se de que os dados de entrada coincide com os recursos necessários de entrada do modelo de Python. Isso pode incluir a conversão ou converter os dados de entrada para um tipo de dados do Python, ou a validação de tipo de dados e o comprimento de dados.
  - O procedimento armazenado cria uma pontuação com base no modelo de Python armazenado.

### <a name="predicttipsinglemodescikitpy"></a>PredictTipSingleModeSciKitPy

Esta é a definição do procedimento armazenado que executa a pontuação usando o **scikit-Saiba** modelo.

```SQL
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
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models2 where name = @model);
  EXEC sp_execute_external_script 
    @language = N'Python',
    @script = N'
      import pickle;
      import numpy;
      import pandas;
      
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

Esta é a definição do procedimento armazenado que executa a pontuação usando o **revoscalepy** modelo.

```SQL
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
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models2 where name = @model);
  EXEC sp_execute_external_script 
    @language = N'Python',
    @script = N'
      import pickle;
      import numpy;
      import pandas;
      from revoscalepy.functions.RxPredict import rx_predict_ex;
      
      # Load model and unserialize
      mod = pickle.loads(model)
      
      # Get features for scoring from input data
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      
      # Score data to get tip prediction probability as a list (of float)
      
      probArray = rx_predict_ex(mod, X)
      
      probList = []
      probList.append(probArray._results["tipped_Pred"])
      
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

2.  Para testar, abra uma nova **consulta** janela e chame o procedimento armazenado, digitando os parâmetros para cada uma das colunas de recursos.

    ```SQL
    -- Call stored procedure PredictTipSingleModeSciKitPy to score using SciKit-Learn model
    EXEC [dbo].[PredictTipSingleModeSciKitPy] 'linear_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    -- Call stored procedure PredictTipSingleModeRxPy to score using revoscalepy model
    EXEC [dbo].[PredictTipSingleModeRxPy] 'revoscalepy_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```
    
    São os sete valores para essas colunas de recurso, em ordem:
    
    -   *passenger_count*
    -   *trip_distance*
    -   *trip_time_in_secs*
    -   *pickup_latitude*
    -   *pickup_longitude*
    -   *dropoff_latitude*
    -   *dropoff_longitude*

3. A saída de ambos os procedimentos é uma probabilidade de uma dica sendo paga para a viagem táxi com os parâmetros ou recursos acima.

## <a name="conclusions"></a>Conclusões

Neste tutorial, você aprendeu como trabalhar com o código Python incorporado em procedimentos armazenados. A integração com [!INCLUDE[tsql](../../includes/tsql-md.md)] torna mais fácil implantar Python modelos para previsão e incorporar o treinamento do modelo como parte de um fluxo de trabalho de dados corporativos.

## <a name="previous-step"></a>Etapa anterior
[Etapa 6: Colocar o modelo em operação](sqldev-py6-operationalize-the-model.md)

## <a name="see-also"></a>Consulte também

[Serviços de aprendizado de máquina com Python](../python/sql-server-python-services.md)

