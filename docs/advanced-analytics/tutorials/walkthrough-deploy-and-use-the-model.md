---
title: Implantar um modelo do R para previsões no SQL Server - aprendizagem de máquina do SQL Server
description: Tutorial que mostra como implantar um modelo de R no SQL Server para análise no banco de dados.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 7b14b70fc5ba8ac39535d9dd6dedbfa1bd309aa4
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645179"
---
# <a name="deploy-the-r-model-and-use-it-in-sql-server-walkthrough"></a>Implantar o modelo de R e usá-lo no SQL Server (passo a passo)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Nesta lição, saiba como implantar modelos R em um ambiente de produção, chamando um modelo treinado de um procedimento armazenado. Você pode chamar o procedimento armazenado no R ou em qualquer linguagem de programação de aplicativo que dá suporte a [!INCLUDE[tsql](../../includes/tsql-md.md)] (como C#, Java, Python e assim por diante) e usar o modelo para fazer previsões sobre novas observações.

Este artigo demonstra as duas formas mais comuns para usar um modelo de pontuação:

> [!div class="checklist"]
> * **Modo de pontuação em lote** gera várias previsões
> * **Modo de pontuação individual** gera previsões uma por vez

## <a name="batch-scoring"></a>Pontuação do lote

Criar um procedimento armazenado, *PredictTipBatchMode*, que gera várias previsões, passando uma consulta SQL ou tabela como entrada. Uma tabela de resultados é retornada, que você pode inserir diretamente em uma tabela ou gravar em um arquivo.

- Obtém um conjunto de dados de entrada como uma consulta SQL
- Chama o modelo de regressão logística treinado salvo na lição anterior
- Prevê a probabilidade de que o driver obtém qualquer dica diferente de zero

1. No Management Studio, abra uma nova janela de consulta e execute o seguinte script T-SQL para criar o procedimento armazenado de PredictTipBatchMode.
  
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

    + Você pode usar uma instrução SELECT para chamar o modelo armazenado em uma tabela SQL. O modelo é recuperado da tabela de **varbinary (max)** dados armazenados na variável SQL  _\@lmodel2_e passado como o parâmetro *mod* no sistema procedimento armazenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

    + Os dados usados como entradas para a pontuação é definida como uma consulta SQL e armazenado como uma cadeia de caracteres na variável SQL  _\@entrada_. Como os dados são recuperados do banco de dados, ele é armazenado em um quadro de dados chamado *InputDataSet*, que é apenas o nome padrão para dados de entrada para o [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) procedimento; você pode definir outro nome de variável, se necessário, usando o parâmetro   *_\@input_data_1_name_*.

    + Para gerar as pontuações, o procedimento armazenado chama a função de rxPredict do **RevoScaleR** biblioteca.

    + O valor de retorno *pontuação*, é a probabilidade, dado o modelo, o driver obtém uma dica. Opcionalmente, você poderia facilmente aplicar algum tipo de filtro para os valores retornados para categorizar os valores de retorno de "dica" e de grupos de "sem gorjeta".  Por exemplo, uma probabilidade de menos de 0,5 significa que uma dica é improvável.
  
2.  Para chamar o procedimento armazenado no modo de lote, você deve definir a consulta necessária como entrada para o procedimento armazenado. Abaixo está a consulta SQL, que pode ser executada no SSMS para verificar se ele funciona.

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

3. Use esse código R para criar a cadeia de caracteres de entrada da consulta SQL:

    ```R
    input <- "N'SELECT TOP 10 a.passenger_count AS passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS direct_distance FROM (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a LEFT OUTER JOIN ( SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample  tablesample (1 percent) repeatable (98052)  )b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND  a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'";
    q <- paste("EXEC PredictTipBatchMode @inquery = ", input, sep="");
    ```

4. Para executar o procedimento armazenado de R, chame o **sqlQuery** método o **RODBC** empacotar e usar a conexão do SQL `conn` que você definiu anteriormente:

    ```R
    sqlQuery (conn, q);
    ```

    Se você receber um erro ODBC, verificar erros de sintaxe e se você tem o número correto de aspas. 
    
    Se você receber um erro de permissões, verifique se que o logon tem a capacidade de executar o procedimento armazenado.

## <a name="single-row-scoring"></a>Pontuação de linha única

Modo de pontuação individual gera previsões uma por vez, passando um conjunto de valores individuais para o procedimento armazenado como entrada. Os valores correspondem aos recursos no modelo, que usa o modelo para criar uma previsão, ou geram outro resultado como um valor de probabilidade. Em seguida, você pode retornar esse valor para o aplicativo ou usuário.

Ao chamar o modelo de previsão em uma base linha por linha, você passa um conjunto de valores que representam os recursos para cada caso individual. O procedimento armazenado, em seguida, retorna uma única previsão ou a probabilidade. 

O procedimento armazenado *PredictTipSingleMode* demonstra essa abordagem. Ele usa como vários parâmetros que representam valores de recurso (por exemplo, passageiro contagem e distância da corrida) de entrada, pontua esses recursos usando o modelo do R armazenado e, em seguida, gera a probabilidade de dica.

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

2. No SQL Server Management Studio, você pode usar o [!INCLUDE[tsql](../../includes/tsql-md.md)] **EXEC** procedimento (ou **EXECUTE**) para chamar o procedimento armazenado e, em seguida, passe a ele as entradas necessárias. Por exemplo, tente executar essa instrução no Management Studio:

    ```sql
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

    Os valores passados aqui são, respectivamente, para as variáveis _passageiro\_contagem_, _trip_distance_, _viagem\_tempo\_no\_segs_, _pickup\_latitude_, _pickup\_longitude_, _chegada\_latitude_, e _chegada\_longitude_.

3. Para executar essa mesma chamada do código R, você simplesmente define uma variável do R que contém a chamada de procedimento armazenado inteiro, como este:

    ```R
    q2 = "EXEC PredictTipSingleMode 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303 ";
    ```

    Os valores passados aqui são, respectivamente, para as variáveis _passageiro\_contagem_, _viagem\_distância_, _viagem\_tempo\_na\_segs_, _pickup\_latitude_, _pickup\_longitude_, _chegada\_ Latitude_, e _chegada\_longitude_.

4. Chame `sqlQuery` (da **RODBC** pacote) e passar a cadeia de conexão, junto com a variável de cadeia de caracteres que contém a chamada de procedimento armazenado.

    ```R
    # predict with stored procedure in single mode
    sqlQuery (conn, q2);
    ```

    >[!TIP]
    > Ferramentas do R para Visual Studio (RTVS) fornece uma excelente integração com o SQL Server e R. Consulte este artigo para obter mais exemplos de como usar RODBC com uma conexão do SQL Server: [Trabalhar com R e SQL Server](https://docs.microsoft.com/visualstudio/rtvs/sql-server)

## <a name="next-steps"></a>Próximas etapas

Agora que você aprendeu a trabalhar com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados e persistir modelos treinados do R para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ele deve ser relativamente fácil para você criar novos modelos com base no conjunto de dados. Por exemplo, você pode tentar criar esses modelos adicionais:

+ Um modelo de regressão que prevê o valor da gorjeta
+ Um modelo de classificação multiclasse que prevê se a dica é pequeno, médio ou grande

Você também poderá explorar esses exemplos adicionais e recursos:

+ [Cenários de ciência de dados e modelos da solução](data-science-scenarios-and-solution-templates.md)
+ [Análise avançada no banco de dados](sqldev-in-database-r-for-sql-developers.md)
+ [Microsoft R - mergulhando na análise de dados](https://msdn.microsoft.com/microsoft-r/data-analysis-in-microsoft-r)
+ [Recursos adicionais](https://msdn.microsoft.com/microsoft-r/microsoft-r-more-resources)
