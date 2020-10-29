---
title: 'Tutorial do R: Implantar modelo'
description: Saiba como implantar modelos do R em um ambiente de produção chamando um modelo treinado de um procedimento armazenado.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 5585f26247ad360fa848a24109416a59c49c94a6
ms.sourcegitcommit: ef20f39a17fd4395dd2dd37b8dd91b57328a751c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/28/2020
ms.locfileid: "92793773"
---
# <a name="deploy-the-r-model-and-use-it-in-sql-server-walkthrough"></a>Implantar o modelo do R e usá-lo no SQL Server (passo a passo)
[!INCLUDE [SQL Server 2016](../../includes/applies-to-version/sqlserver2016.md)]

Nesta lição, saiba como implantar modelos do R em um ambiente de produção chamando um modelo treinado de um procedimento armazenado. Você pode invocar o procedimento armazenado no R ou em uma linguagem de programação de aplicativo que dá suporte ao [!INCLUDE[tsql](../../includes/tsql-md.md)] (como C#, Java, Python e assim por diante) e usar o modelo a fim de fazer previsões sobre novas observações.

Este artigo demonstra as duas maneiras mais comuns de usar um modelo em pontuação:

> [!div class="checklist"]
> * O **modo de pontuação em lote** gera várias previsões
> * O **modo de pontuação individual** gera uma previsão de cada vez

## <a name="batch-scoring"></a>Pontuação do lote

Crie um procedimento armazenado, *PredictTipBatchMode* , que gera várias previsões, passando uma consulta ou tabela SQL como entrada. É retornada uma tabela de resultados, que você pode inserir diretamente em uma tabela ou gravar em um arquivo.

- Obtém um conjunto de dados de entrada como uma consulta SQL
- Chama o modelo de regressão logística treinado salvo na lição anterior
- Prevê a probabilidade de que o motorista receba qualquer gorjeta diferente de zero

1. No Management Studio, abra uma nova janela de consulta e execute o seguinte script do T-SQL para criar o procedimento armazenado PredictTipBatchMode.
  
    ```sql
    USE [NYCTaxi_Sample]
    GO

    SET ANSI_NULLS ON
    GO
    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'PredictTipBatchMode')
    DROP PROCEDURE v
    GO

    CREATE PROCEDURE [dbo].[PredictTipBatchMode] @input nvarchar(max)
    AS
    BEGIN
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model  FROM nyc_taxi_models);
      EXEC sp_execute_external_script @language = N'R',
         @script = N'
           mod <- unserialize(as.raw(model));
           print(summary(mod))
           OutputDataSet<-rxPredict(modelObject = mod,
             data = InputDataSet,
             outData = NULL,
             predVarNames = "Score", type = "response",
             writeModelVars = FALSE, overwrite = TRUE);
           str(OutputDataSet)
           print(OutputDataSet)',
      @input_data_1 = @input,
      @params = N'@model varbinary(max)',
      @model = @lmodel2
      WITH RESULT SETS ((Score float));
    END
    ```

    + Você usa uma instrução SELECT para chamar o modelo armazenado de uma tabela SQL. O modelo é recuperado da tabela como dados **varbinary(max)** , armazenado na variável SQL _\@lmodel2_ e passado como o parâmetro *mod* para o procedimento armazenado do sistema [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

    + Os dados usados como entradas para pontuação são definidos como uma consulta SQL e armazenados como uma cadeia de caracteres na variável SQL _\@input_ . À medida que os dados são recuperados do banco de dados, eles são armazenados em uma estrutura de dados chamada *InputDataSet* , que é apenas o nome padrão dos dados de entrada para o procedimento [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Você pode definir outro nome de variável, se necessário, usando o parâmetro _\@input_data_1_name_ .

    + Para gerar as pontuações, o procedimento armazenado chama a função rxPredict da biblioteca **RevoScaleR** .

    + O valor retornado, *Pontuação* , é a probabilidade, considerando o modelo, de o motorista receber uma gorjeta. Como opção, você poderia facilmente aplicar algum tipo de filtro aos valores retornados para categorizá-los em grupos "gorjeta" e "sem gorjeta".  Por exemplo, uma probabilidade inferior a 0,5 significa que uma gorjeta é improvável.
  
2.  Para chamar o procedimento armazenado no modo de lote, você define a consulta obrigatória como entrada para o procedimento armazenado. Abaixo está a consulta SQL, que pode ser executada no SSMS para verificar se ela funciona.

    ```sql
    SELECT TOP 10
      a.passenger_count AS passenger_count,
      a.trip_time_in_secs AS trip_time_in_secs,
      a.trip_distance AS trip_distance,
      a.dropoff_datetime AS dropoff_datetime,
      dbo.fnCalculateDistance( pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS direct_distance
      FROM 
        (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude 
        FROM nyctaxi_sample)a 
      LEFT OUTER JOIN
      ( SELECT medallion, hack_license, pickup_datetime
      FROM nyctaxi_sample  tablesample (1 percent) repeatable (98052)  )b
      ON a.medallion=b.medallion
      AND a.hack_license=b.hack_license
      AND a.pickup_datetime=b.pickup_datetime
      WHERE b.medallion is null
    ```

3. Use este código R para criar a cadeia de caracteres de entrada da consulta SQL:

    ```R
    input <- "N'SELECT TOP 10 a.passenger_count AS passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS direct_distance FROM (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a LEFT OUTER JOIN ( SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample  tablesample (1 percent) repeatable (98052)  )b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND  a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'";
    q <- paste("EXEC PredictTipBatchMode @input = ", input, sep="");
    ```

4. para executar o procedimento armazenado do R, chame o método **sqlQuery** do pacote **RODBC** e use a conexão SQL `conn` que você definiu anteriormente:

    ```R
    sqlQuery (conn, q);
    ```

    Se você receber um erro do ODBC, verifique se há erros de sintaxe e se há o número correto de aspas. 
    
    Se você receber um erro de permissões, verifique se o logon tem a capacidade de executar o procedimento armazenado.

## <a name="single-row-scoring"></a>Pontuação de uma única linha

O modo de pontuação individual gera previsões uma de cada vez, passando um conjunto de valores individuais para o procedimento armazenado como entrada. Os valores correspondem aos recursos no modelo, que o modelo usa para criar uma previsão ou gerar outro resultado, como um valor de probabilidade. Você pode retornar esse valor para o aplicativo ou o usuário.

Ao chamar o modelo para previsão linha a linha, você passa um conjunto de valores que representam recursos para cada caso individual. Em seguida, o procedimento armazenado retorna uma única previsão ou probabilidade. 

O procedimento armazenado *PredictTipSingleMode* demonstra essa abordagem. Ele usa como entrada vários parâmetros que representam valores de recursos (por exemplo, contagem de passageiro e distância da corrida), pontua esses recursos usando o modelo do R armazenado e gera a probabilidade de gorjeta.

1. Execute a seguinte instrução do Transact-SQL para criar o procedimento armazenado.

    ```sql
    USE [NYCTaxi_Sample]
    GO

    SET ANSI_NULLS ON
    GO
    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'PredictTipSingleMode')
    DROP PROCEDURE v
    GO

    CREATE PROCEDURE [dbo].[PredictTipSingleMode] @passenger_count int = 0,
    @trip_distance float = 0,
    @trip_time_in_secs int = 0,
    @pickup_latitude float = 0,
    @pickup_longitude float = 0,
    @dropoff_latitude float = 0,
    @dropoff_longitude float = 0
    AS
    BEGIN
      DECLARE @inquery nvarchar(max) = N'
        SELECT * FROM [dbo].[fnEngineerFeatures](@passenger_count, @trip_distance, @trip_time_in_secs, @pickup_latitude, @pickup_longitude, @dropoff_latitude, @dropoff_longitude)'
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model FROM nyc_taxi_models);

      EXEC sp_execute_external_script @language = N'R',  @script = N'
            mod <- unserialize(as.raw(model));
            print(summary(mod))
            OutputDataSet<-rxPredict(
              modelObject = mod,
              data = InputDataSet,
              outData = NULL,
              predVarNames = "Score",
              type = "response",
              writeModelVars = FALSE,
              overwrite = TRUE);
            str(OutputDataSet)
            print(OutputDataSet)
            ',
      @input_data_1 = @inquery,
      @params = N'
      -- passthrough columns
      @model varbinary(max) ,
      @passenger_count int ,
      @trip_distance float ,
      @trip_time_in_secs int ,
      @pickup_latitude float ,
      @pickup_longitude float ,
      @dropoff_latitude float ,
      @dropoff_longitude float',
      -- mapped variables
      @model = @lmodel2 ,
      @passenger_count =@passenger_count ,
      @trip_distance=@trip_distance ,
      @trip_time_in_secs=@trip_time_in_secs ,
      @pickup_latitude=@pickup_latitude ,
      @pickup_longitude=@pickup_longitude ,
      @dropoff_latitude=@dropoff_latitude ,
      @dropoff_longitude=@dropoff_longitude
      WITH RESULT SETS ((Score float));
    END
    ```

2. No SQL Server Management Studio, você pode usar o procedimento [!INCLUDE[tsql](../../includes/tsql-md.md)] **EXEC** (ou **EXECUTE** ) para chamar o procedimento armazenado e passar as entradas necessárias. Por exemplo, tente executar esta instrução no Management Studio:

    ```sql
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

    Os valores passados aqui referem-se, respectivamente, às variáveis _passenger\_count_ , _trip_distance_ , _trip\_time\_in\_secs_ , _pickup\_latitude_ , _pickup\_longitude_ , _dropoff\_latitude_ e _dropoff\_longitude_ .

3. Para executar essa mesma chamada do código de R, você simplesmente define uma variável de R que contenha a chamada de procedimento armazenado inteiro, como este:

    ```R
    q2 = "EXEC PredictTipSingleMode 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303 ";
    ```

    Os valores passados aqui referem-se, respectivamente, às variáveis _passenger\_count_ , _trip\_distance_ , _trip\_time\_in\_secs_ , _pickup\_latitude_ , _pickup\_longitude_ , _dropoff\_latitude_ e _dropoff\_longitude_ .

4. Chame `sqlQuery` (do pacote **RODBC** ) e passe a cadeia de conexão junto com a variável de cadeia de caracteres que contêm a chamada de procedimento armazenado.

    ```R
    # predict with stored procedure in single mode
    sqlQuery (conn, q2);
    ```

    >[!TIP]
    > O RTVS (Ferramentas do R para Visual Studio) fornece uma ótima integração com o SQL Server e o R. Confira este artigo para obter mais exemplos de como usar o RODBC com uma conexão SQL Server: [Como trabalhar com SQL Server e R](/visualstudio/rtvs/sql-server)

## <a name="next-steps"></a>Próximas etapas

Agora que você já sabe como trabalhar usando dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e persistir modelos treinados do R no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], deve ser relativamente fácil criar modelos com base nesse conjunto de dados. Por exemplo, você pode tentar criar estes modelos adicionais:

+ Um modelo de regressão que prevê o valor da gorjeta
+ Um modelo de classificação de várias classes que prevê se a gorjeta é pequena, média ou grande

Também pode ser útil explorar estes exemplos e recursos adicionais:

+ [Cenários de ciência de dados e modelos da solução](data-science-scenarios-and-solution-templates.md)
+ [Análise avançada no banco de dados](r-taxi-classification-introduction.md)
+ [Guias de instruções do Machine Learning Server](/machine-learning-server/r/how-to-introduction)
+ [Recursos adicionais do Machine Learning Server](/machine-learning-server/resources-more)