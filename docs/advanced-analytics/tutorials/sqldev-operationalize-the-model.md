---
title: Lição 4 prever resultados potenciais usando modelos de R
description: Tutorial mostrando como colocar em operação o script R inserido em SQL Server procedimentos armazenados com funções T-SQL
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/16/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 159fb29bf560e755fdc605330d7d20369f55ba08
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345892"
---
# <a name="lesson-4-run-predictions-using-r-embedded-in-a-stored-procedure"></a>Lição 4: Executar previsões usando o R Embedded em um procedimento armazenado
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo faz parte de um tutorial para desenvolvedores de SQL sobre como usar o R no SQL Server.

Nesta etapa, você aprenderá a usar o modelo contra novas observações para prever possíveis resultados. O modelo é encapsulado em um procedimento armazenado que pode ser chamado diretamente por outros aplicativos. O tutorial demonstra várias maneiras de executar a Pontuação:

- **Modo de Pontuação do lote**: Use uma consulta SELECT como uma entrada para o procedimento armazenado. O procedimento armazenado retorna uma tabela de observações correspondente aos casos de entrada.

- **Modo de Pontuação individual**: Passe um conjunto de valores de parâmetro individuais como entrada.  O procedimento armazenado retorna uma única linha ou valor.

Primeiro, vamos ver como a pontuação funciona em geral.

## <a name="basic-scoring"></a>Pontuação básica

O procedimento armazenado **RxPredict** ilustra a sintaxe básica para encapsular uma chamada RxPredict RevoScaleR em um procedimento armazenado.

```sql
CREATE PROCEDURE [dbo].[RxPredict] (@model varchar(250), @inquery nvarchar(max))
AS 
BEGIN 

DECLARE @lmodel2 varbinary(max) = (SELECT model FROM nyc_taxi_models WHERE name = @model);  
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

+ A instrução SELECT Obtém o modelo serializado do banco de dados e armazena o modelo na variável `mod` de R para processamento adicional usando o R.

+ Os novos casos de pontuação são obtidos da [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta especificada em `@inquery`, o primeiro parâmetro para o procedimento armazenado. Conforme os dados da consulta são lidos, as linhas são salvas no quadro de dados padrão, `InputDataSet`. Esse quadro de dados é passado para a função [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) em [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler), que gera as pontuações.
  
    `OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);`
  
    Como um data.frame pode conter uma única linha, você pode usar o mesmo código para a pontuação única ou de lote.
  
+ O valor retornado pela `rxPredict` função é um **float** que representa a probabilidade de o driver obter uma gorjeta de qualquer valor.

## <a name="batch-scoring-a-list-of-predictions"></a>Pontuação de lote (uma lista de previsões)

Um cenário mais comum é gerar previsões para várias observações no modo de lote. Nesta etapa, vamos ver como funciona a pontuação em lote.

1.  Comece obtendo um conjunto menor de dados de entrada com os quais trabalhar. Esta consulta cria uma lista das “10 primeiras” corridas com contagem de passageiros e outros recursos necessários para fazer uma previsão.
  
    ```sql
    SELECT TOP 10 a.passenger_count AS passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) AS direct_distance
    
    FROM (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a

    LEFT OUTER JOIN

    (SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample TABLESAMPLE (70 percent) REPEATABLE (98052)    )b

    ON a.medallion=b.medallion AND a.hack_license=b.hack_license 
    AND a.pickup_datetime=b.pickup_datetime
    WHERE b.medallion IS NULL
    ```

    **Resultados de exemplo**
    
    ```sql
    passenger_count   trip_time_in_secs    trip_distance  dropoff_datetime   direct_distance
    1  283 0.7 2013-03-27 14:54:50.000   0.5427964547
    1  289 0.7 2013-02-24 12:55:29.000   0.3797099614
    1  214 0.7 2013-06-26 13:28:10.000   0.6970098661
    ```

2. Crie um procedimento armazenado chamado **RxPredictBatchOutput** no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].

    ```sql
    CREATE PROCEDURE [dbo].[RxPredictBatchOutput] (@model varchar(250), @inquery nvarchar(max))
    AS
    BEGIN
    DECLARE @lmodel2 varbinary(max) = (SELECT model FROM nyc_taxi_models WHERE name = @model);
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

3.  Forneça o texto da consulta em uma variável e passe-o como um parâmetro para o procedimento armazenado:

    ```sql
    -- Define the input data
    DECLARE @query_string nvarchar(max)
    SET @query_string='SELECT TOP 10 a.passenger_count as passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) AS direct_distance FROM  (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample  )a   LEFT OUTER JOIN (SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample TABLESAMPLE (70 percent) REPEATABLE (98052))b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'
    
    -- Call the stored procedure for scoring and pass the input data
    EXEC [dbo].[RxPredictBatchOutput] @model = 'RxTrainLogit_model', @inquery = @query_string;
    ```
  
O procedimento armazenado retorna uma série de valores que representam a previsão para cada uma das 10 principais viagens. No entanto, as principais viagens também são viagens de passageiro simples com uma distância de corrida relativamente curta, para a qual o driver é improvável de receber uma dica.
  

> [!TIP]
> 
> Em vez de retornar apenas os resultados de "Sim-dica" e "sem gorjeta", você também pode retornar a pontuação de probabilidade para a previsão e, em seguida, aplicar uma cláusula WHERE aos valores da coluna de _Pontuação_ para categorizar a Pontuação como "probabilidade de Tip" ou "improvável de gorjeta", usando um valor de limite, como 0,5 ou 0,7. Essa etapa não está incluída no procedimento armazenado, mas seria fácil de ser implementada.

## <a name="single-row-scoring-of-multiple-inputs"></a>Pontuação de linha única de várias entradas

Às vezes, você deseja passar vários valores de entrada e obter uma única previsão com base nesses valores. Por exemplo, você pode configurar uma planilha do Excel, um aplicativo Web ou um relatório Reporting Services para chamar o procedimento armazenado e fornecer entradas digitadas ou selecionadas por usuários desses aplicativos.

Nesta seção, você aprenderá a criar previsões únicas usando um procedimento armazenado que usa várias entradas, como contagem de passageiros, distância de viagem e assim por diante. O procedimento armazenado cria uma pontuação com base no modelo de R armazenado anteriormente.
  
Se você chamar o procedimento armazenado de um aplicativo externo, certifique-se de que os dados correspondem aos requisitos do modelo do R. Isso pode incluir a garantia de que os dados de entrada possam ser convertidos em um tipo de dados do R ou a validação do tipo e comprimento dos dados. 

1. Crie um procedimento armazenado **RxPredictSingleRow**.
  
    ```sql
    CREATE PROCEDURE [dbo].[RxPredictSingleRow] @model varchar(50), @passenger_count int = 0, @trip_distance float = 0, @trip_time_in_secs int = 0, @pickup_latitude float = 0, @pickup_longitude float = 0, @dropoff_latitude float = 0, @dropoff_longitude float = 0
    AS
    BEGIN
    DECLARE @inquery nvarchar(max) = N'SELECT * FROM [dbo].[fnEngineerFeatures](@passenger_count, @trip_distance, @trip_time_in_secs,  @pickup_latitude, @pickup_longitude, @dropoff_latitude, @dropoff_longitude)';
    DECLARE @lmodel2 varbinary(max) = (SELECT model FROM nyc_taxi_models WHERE name = @model);
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

2. Experimente usá-lo, fornecendo os valores manualmente.
  
    Abra uma nova janela de **consulta** e chame o procedimento armazenado, fornecendo valores para cada um dos parâmetros. Os parâmetros representam colunas de recursos usadas pelo modelo e são necessários.

    ```sql
    EXEC [dbo].[RxPredictSingleRow] @model = 'RxTrainLogit_model',
    @passenger_count = 1,
    @trip_distance = 2.5,
    @trip_time_in_secs = 631,
    @pickup_latitude = 40.763958,
    @pickup_longitude = -73.973373,
    @dropoff_latitude =  40.782139,
    @dropoff_longitude = -73.977303
    ```

    Ou use essa forma mais curta com suporte para [parâmetros para um procedimento armazenado](https://docs.microsoft.com/sql/relational-databases/stored-procedures/specify-parameters):
  
    ```sql
    EXEC [dbo].[RxPredictSingleRow] 'RxTrainLogit_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

3. Os resultados indicam que a probabilidade de obter uma gorjeta é baixa (zero) nessas 10 principais viagens, já que todas são viagens de passageiro único em uma distância relativamente curta.

## <a name="conclusions"></a>Conclusões

Isso conclui o tutorial. Agora que você aprendeu a inserir o código R em procedimentos armazenados, você pode estender essas práticas para criar modelos próprios. A integração com o [!INCLUDE[tsql](../../includes/tsql-md.md)] torna muito mais fácil a implantação de modelos do R para previsão e incorporação do novo treinamento do modelo como parte de um fluxo de trabalho de dados empresariais.

## <a name="previous-lesson"></a>Lição anterior

[Lição 3: Treinar e salvar um modelo de R usando o T-SQL](sqldev-train-and-save-a-model-using-t-sql.md)
