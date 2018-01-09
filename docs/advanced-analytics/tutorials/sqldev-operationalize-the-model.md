---
title: "Lição 6: Colocar o modelo R | Microsoft Docs"
ms.custom: 
ms.date: 11/10/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2016
dev_langs:
- R
- TSQL
ms.assetid: 52b05828-11f5-4ce3-9010-59c213a674d1
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 2bd62e41c82f1468dfb6a358001eda90b5a21777
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="lesson-6-operationalize-the-r-model"></a>Lição 6: Colocar o modelo R

Este artigo faz parte de um tutorial para desenvolvedores em SQL sobre como usar o R no SQL Server.

Nesta etapa, você aprenderá a *operacionalizar* o modelo usando um procedimento armazenado. Esse procedimento armazenado pode ser chamado diretamente por outros aplicativos, para fazer previsões sobre novas observações. Passo a passo demonstra duas maneiras de executar pontuação usando um modelo de R em um procedimento armazenado:

- **Modo de pontuação em lote**: usar uma consulta SELECT como uma entrada para o procedimento armazenado. O procedimento armazenado retorna uma tabela de observações correspondente aos casos de entrada.

- **Modo de pontuação individual**: passe um conjunto de valores de parâmetros individuais como entrada.  O procedimento armazenado retorna uma única linha ou valor.

Primeiro, vamos ver como a pontuação funciona em geral.

## <a name="basic-scoring"></a>A pontuação básica

O procedimento armazenado _PredictTip_ ilustra a sintaxe básica para encapsular uma chamada de previsão em um procedimento armazenado.

```SQL
CREATE PROCEDURE [dbo].[PredictTip] @inquery nvarchar(max) 
AS 
BEGIN 
  
DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model FROM nyc_taxi_models);  
EXEC sp_execute_external_script @language = N'R',
  @script = N' 
    mod <- unserialize(as.raw(model)); 
    print(summary(mod)) 
    OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE); 
    str(OutputDataSet) 
    print(OutputDataSet) 
    ', 
  @input_data_1 = @inquery, 
  @params = N'@model varbinary(max)',
  @model = @lmodel2 
  WITH RESULT SETS ((Score float));
END
GO
```

+ A instrução SELECT obtém o modelo serializado do banco de dados e armazena o modelo na variável R `mod` para processamento adicional usando o R.

+ Os novos casos de pontuação são obtidos de [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta especificada no `@inquery`, o primeiro parâmetro para o procedimento armazenado. Conforme os dados da consulta são lidos, as linhas são salvas no quadro de dados padrão, `InputDataSet`. Esse quadro de dados é passado para a função `rxPredict` no R, que gera as pontuações.
  
    `OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);`
  
    Como um data.frame pode conter uma única linha, você pode usar o mesmo código para a pontuação única ou de lote.
  
+ O valor retornado pelo `rxPredict` função é um **float** que representa a probabilidade de que o driver obtém uma dica de qualquer valor.

## <a name="batch-scoring"></a>A pontuação do lote

Agora vamos ver como funciona a pontuação de lote.

1.  Vamos começar obtendo um conjunto menor de dados de entrada com o qual trabalharemos. Esta consulta cria uma lista das “10 primeiras” corridas com contagem de passageiros e outros recursos necessários para fazer uma previsão.
  
    ```SQL
    SELECT TOP 10 a.passenger_count AS passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) AS direct_distance
    
    FROM (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a

    LEFT OUTER JOIN

    (SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample TABLESAMPLE (70 percent) REPEATABLE (98052)    )b

    ON a.medallion=b.medallion AND a.hack_license=b.hack_license 
    AND a.pickup_datetime=b.pickup_datetime
    WHERE b.medallion IS NULL
    ```

    **Resultados de exemplo**
    
    ```
    passenger_count   trip_time_in_secs    trip_distance  dropoff_datetime   direct_distance
    1  283 0.7 2013-03-27 14:54:50.000   0.5427964547
    1  289 0.7 2013-02-24 12:55:29.000   0.3797099614
    1  214 0.7 2013-06-26 13:28:10.000   0.6970098661
    ```

    Essa consulta pode ser usada como entrada para o procedimento armazenado, _PredictTipBatchMode_, fornecido como parte do download.

2. Reserve um minuto para examinar o código do procedimento armazenado _PredictTipBatchMode_ em [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].

    ```SQL
    /****** Object:  StoredProcedure [dbo].[PredictTipBatchMode]  ******/
    CREATE PROCEDURE [dbo].[PredictTipBatchMode] @inquery nvarchar(max)
    AS
    BEGIN
    DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model FROM nyc_taxi_models);
    EXEC sp_execute_external_script 
      @language = N'R',
      @script = N'
        mod <- unserialize(as.raw(model));
        print(summary(mod))
        OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);
        str(OutputDataSet)
        print(OutputDataSet)
      ',
      @input_data_1 = @inquery,
      @params = N'@model varbinary(max)',
      @model = @lmodel2
      WITH RESULT SETS ((Score float));
    END
    ```

3.  Forneça o texto da consulta em uma variável e passá-lo como um parâmetro para o procedimento armazenado:

    ```SQL
    -- Define the input data
    DECLARE @query_string nvarchar(max)
    SET @query_string='SELECT TOP 10 a.passenger_count as passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) AS direct_distance FROM  (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample  )a   LEFT OUTER JOIN (SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample TABLESAMPLE (70 percent) REPEATABLE (98052))b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'

    -- Call the stored procedure for scoring and pass the input data
    EXEC [dbo].[PredictTip] @inquery = @query_string;
    ```
  
4. O procedimento armazenado retorna uma série de valores que representam a previsão para cada uma das viagens 10 principais. No entanto, os principais percursos também são viagens passageiro único com uma distância de viagem relativamente curto, para o qual o driver é improvável obter uma dica.
  

> [!TIP]
> 
> Em vez de retornar apenas a "dica Sim" e "nenhuma dica" resultados, você pode também retornar a pontuação de probabilidade da previsão e, em seguida, aplicar uma cláusula WHERE para o _pontuação_ valores de coluna para classificar pontuação como "propenso a dica" ou " provavelmente não dica", usando um valor de limite como 0,5 ou 0,7. Essa etapa não está incluída no procedimento armazenado, mas seria fácil de ser implementada.

## <a name="single-row-scoring"></a>Pontuação de única linha

Às vezes, você deseja passar valores individuais de um aplicativo e obter um único resultado com base nesses valores. Por exemplo, você poderá definir uma planilha do Excel, um aplicativo Web ou um relatório do Reporting Services para chamar o procedimento armazenado e fornecer entradas digitadas ou selecionadas por usuários.

Nesta seção, você aprenderá como criar previsões únicas usando um procedimento armazenado.

1. Reserve um minuto para examinar o código do procedimento armazenado _PredictTipSingleMode_, incluído como parte do download.
  
    ```SQL
    CREATE PROCEDURE [dbo].[PredictTipSingleMode] @passenger_count int = 0, @trip_distance float = 0, @trip_time_in_secs int = 0, @pickup_latitude float = 0, @pickup_longitude float = 0, @dropoff_latitude float = 0, @dropoff_longitude float = 0
    AS
    BEGIN
    DECLARE @inquery nvarchar(max) = N'SELECT * FROM [dbo].[fnEngineerFeatures](@passenger_count, @trip_distance, @trip_time_in_secs,  @pickup_latitude, @pickup_longitude, @dropoff_latitude, @dropoff_longitude)';
    DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model FROM nyc_taxi_models);
    EXEC sp_execute_external_script  
      @language = N'R',
      @script = N'  
        mod <- unserialize(as.raw(model));  
        print(summary(mod));  
        OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);  
        str(OutputDataSet);
        print(OutputDataSet); 
        ',  
      @input_data_1 = @inquery,  
      @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,@trip_time_in_secs int ,  @pickup_latitude float ,@pickup_longitude float ,@dropoff_latitude float ,@dropoff_longitude float', @model = @lmodel2, @passenger_count =@passenger_count, @trip_distance=@trip_distance, @trip_time_in_secs=@trip_time_in_secs, @pickup_latitude=@pickup_latitude, @pickup_longitude=@pickup_longitude, @dropoff_latitude=@dropoff_latitude, @dropoff_longitude=@dropoff_longitude  
      WITH RESULT SETS ((Score float));  
    END
    ```
  
    - Esse procedimento armazenado usa vários valores únicos como entrada, como contagem de passageiros, distância da corrida e assim por diante.
  
        Se você chamar o procedimento armazenado de um aplicativo externo, certifique-se de que os dados correspondem aos requisitos do modelo de R. Isso pode incluir a garantia de que os dados de entrada possam ser convertidos em um tipo de dados do R ou a validação do tipo e comprimento dos dados. 
  
    -   O procedimento armazenado cria uma pontuação com base no modelo do R armazenado.
  
2. Experimente usá-lo, fornecendo os valores manualmente.
  
    Abra uma nova **consulta** janela e chame o procedimento armazenado, fornecendo valores para cada um dos parâmetros. Os parâmetros representam as colunas de recursos usadas pelo modelo e são necessários.

    ```
    EXEC [dbo].[PredictTipSingleMode] @passenger_count = 0,
    @trip_distance = 2.5,
    @trip_time_in_secs = 631,
    @pickup_latitude = 40.763958,
    @pickup_longitude = -73.973373,
    @dropoff_latitude =  40.782139,
    @dropoff_longitude = 73.977303
    ```

    Ou, use este formulário mais curto com suporte para [parâmetros para um procedimento armazenado](https://docs.microsoft.com/sql/relational-databases/stored-procedures/specify-parameters):
  
    ```SQL
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

3. Os resultados indicam que a probabilidade de obter uma dica é baixa nessas 10 viagens principais, já que todos são viagens passageiro único em uma distância relativamente curta.

## <a name="conclusions"></a>Conclusões

Isso conclui o tutorial. Agora que você aprendeu a inserir código R em procedimentos armazenados, você pode estender essas práticas recomendadas para criar modelos de sua preferência. A integração com o [!INCLUDE[tsql](../../includes/tsql-md.md)] torna muito mais fácil a implantação de modelos do R para previsão e incorporação do novo treinamento do modelo como parte de um fluxo de trabalho de dados empresariais.

## <a name="previous-lesson"></a>Lição anterior

[Lição 5: Treinar e salvar um modelo de R usando o T-SQL](../r/sqldev-train-and-save-a-model-using-t-sql.md)
