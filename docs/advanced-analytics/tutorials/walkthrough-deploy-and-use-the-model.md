---
title: Implantar um modelo de R para previsões em SQL Server
description: Tutorial mostrando como implantar um modelo R em SQL Server para análise no banco de dados.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 96744b15bef03b7d8badc803b1fa5f5de382e64f
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470542"
---
# <a name="deploy-the-r-model-and-use-it-in-sql-server-walkthrough"></a>Implantar o modelo do R e usá-lo em SQL Server (passo a passos)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Nesta lição, saiba como implantar modelos de R em um ambiente de produção chamando um modelo treinado de um procedimento armazenado. Você pode invocar o procedimento armazenado do R ou de qualquer linguagem de programação [!INCLUDE[tsql](../../includes/tsql-md.md)] de aplicativo que C#ofereça suporte (como Java, Python e assim por diante) e usar o modelo para fazer previsões sobre novas observações.

Este artigo demonstra as duas maneiras mais comuns de usar um modelo em Pontuação:

> [!div class="checklist"]
> * O **modo de Pontuação do lote** gera várias previsões
> * O **modo de Pontuação individual** gera previsões uma de cada vez

## <a name="batch-scoring"></a>Pontuação de lote

Crie um procedimento armazenado, *PredictTipBatchMode*, que gera várias previsões, passando uma consulta ou tabela SQL como entrada. Uma tabela de resultados é retornada, que você pode inserir diretamente em uma tabela ou gravar em um arquivo.

- Obtém um conjunto de dados de entrada como uma consulta SQL
- Chama o modelo de regressão logística treinado salvo na lição anterior
- Prevê a probabilidade de que o driver obtenha qualquer gorjeta diferente de zero

1. Em Management Studio, abra uma nova janela de consulta e execute o seguinte script T-SQL para criar o procedimento armazenado PredictTipBatchMode.
  
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

    + Você usa uma instrução SELECT para chamar o modelo armazenado de uma tabela SQL. O modelo é recuperado da tabela como dados **varbinary (max)** , armazenados na variável  _\@SQL lmodel2_e passado como o parâmetro *mod* para o procedimento armazenado do sistema [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

    + Os dados usados como entradas para pontuação são definidos como uma consulta SQL e armazenados como uma cadeia de caracteres na  _\@entrada_da variável SQL. À medida que os dados são recuperados do banco de dados, eles são armazenados em um data frame chamado *InputDataSet*, que é apenas o nome padrão dos dados de entrada para o procedimento [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) ; Você pode definir outro nome de variável, se necessário, usando o parâmetro  *_\@input_data_1_name_* .

    + Para gerar as pontuações, o procedimento armazenado chama a função rxPredict da biblioteca **RevoScaleR** .

    + O valor de retorno, *Score*, é a probabilidade, dado o modelo, que o driver Obtém uma dica. Opcionalmente, você pode facilmente aplicar algum tipo de filtro aos valores retornados para categorizar os valores de retorno em grupos "Tip" e "sem gorjeta".  Por exemplo, uma probabilidade de menos de 0,5 significaria uma dica improvável.
  
2.  Para chamar o procedimento armazenado no modo de lote, você define a consulta necessária como entrada para o procedimento armazenado. Abaixo está a consulta SQL, que pode ser executada no SSMS para verificar se ele funciona.

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
    q <- paste("EXEC PredictTipBatchMode @inquery = ", input, sep="");
    ```

4. Para executar o procedimento armazenado do R, chame o  método SQLQuery do pacote **RODBC** e use a conexão `conn` SQL que você definiu anteriormente:

    ```R
    sqlQuery (conn, q);
    ```

    Se você receber um erro de ODBC, verifique se há erros de sintaxe e se tem o número correto de aspas. 
    
    Se você receber um erro de permissões, verifique se o logon tem a capacidade de executar o procedimento armazenado.

## <a name="single-row-scoring"></a>Pontuação de linha única

O modo de Pontuação individual gera previsões uma de cada vez, passando um conjunto de valores individuais para o procedimento armazenado como entrada. Os valores correspondem aos recursos no modelo, que o modelo usa para criar uma previsão ou gerar outro resultado, como um valor de probabilidade. Você pode retornar esse valor para o aplicativo ou o usuário.

Ao chamar o modelo para previsão linha por linha, você passa um conjunto de valores que representam recursos para cada caso individual. Em seguida, o procedimento armazenado retorna uma única previsão ou probabilidade. 

O procedimento armazenado *PredictTipSingleMode* demonstra essa abordagem. Ela usa como entrada vários parâmetros que representam valores de recursos (por exemplo, contagem de passageiro e distância de corrida), pontua esses recursos usando o modelo de R armazenado e gera a probabilidade de gorjeta.

1. Execute a seguinte instrução Transact-SQL para criar o procedimento armazenado.

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

2. No SQL Server Management Studio, você pode usar o [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimento **exec** (ou **executar**) para chamar o procedimento armazenado e passá-lo para as entradas necessárias. Por exemplo, tente executar esta instrução no Management Studio:

    ```sql
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

    Os valores passados aqui são, respectivamente, para a contagem de _passageiro\__ das variáveis _, trip_distance_, _tempo\_de\_viagem\_em segundos_, _\_retirar a latitude_, _escolha\_a longitude_, _a\_latitude chegada_e _a\_longitude de chegada_.

3. Para executar essa mesma chamada do código R, você simplesmente define uma variável de R que contém a chamada de procedimento armazenado inteira, como esta:

    ```R
    q2 = "EXEC PredictTipSingleMode 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303 ";
    ```

    Os valores passados aqui são, respectivamente, para as variáveis _\__ _contagem de\_passageiro_, distância da corrida _,\_tempo\_de\_viagem em segundos_, _retirada\_ Latitude_, _retirada\_de longitude_, _latitude\_chegada_e _longitude de\_chegada_.

4. Chame `sqlQuery` (do pacote **RODBC** ) e passe a cadeia de conexão, junto com a variável de cadeia de caracteres que contém a chamada de procedimento armazenado.

    ```R
    # predict with stored procedure in single mode
    sqlQuery (conn, q2);
    ```

    >[!TIP]
    > O Ferramentas do R para Visual Studio (RTVS) fornece uma ótima integração com o SQL Server e o R. Consulte este artigo para obter mais exemplos de como usar o RODBC com uma conexão SQL Server: [Trabalhando com SQL Server e R](https://docs.microsoft.com/visualstudio/rtvs/sql-server)

## <a name="next-steps"></a>Próximas etapas

Agora que você aprendeu como trabalhar com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados e persistir modelos R treinados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o, deve ser relativamente fácil criar novos modelos com base nesse conjunto de dados. Por exemplo, você pode tentar criar esses modelos adicionais:

+ Um modelo de regressão que prevê o valor da gorjeta
+ Um modelo de classificação multiclasse que prevê se a gorjeta é Big, Medium ou Small

Você também pode querer explorar estes exemplos e recursos adicionais:

+ [Cenários de ciência de dados e modelos da solução](data-science-scenarios-and-solution-templates.md)
+ [Análise avançada no banco de dados](sqldev-in-database-r-for-sql-developers.md)
+ [Guias de instruções do Machine Learning Server](https://docs.microsoft.com/machine-learning-server/r/how-to-introduction)
+ [Machine Learning Server recursos adicionais](https://docs.microsoft.com//machine-learning-server/resources-more)
