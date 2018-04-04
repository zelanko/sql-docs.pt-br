---
title: Implantar o modelo de R e usá-lo no SQL (passo a passo) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: de43bd77f7a5537265fb7cb74a59e326010a9f71
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2018
---
# <a name="deploy-the-r-model-and-use-it-in-sql"></a>Implantar o modelo de R e usá-lo no SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Nesta lição, você usar os modelos R em um ambiente de produção, chamando um modelo treinado de um procedimento armazenado. Em seguida, você pode chamar o procedimento armazenado de R ou em qualquer linguagem de programação de aplicativo que oferece suporte a [!INCLUDE[tsql](../../includes/tsql-md.md)] (como c#, Java, Python, etc.), para usar o modelo para fazer previsões sobre novos observações.

Este exemplo demonstra as duas formas mais comuns de usar um modelo de pontuação:

- **Modo de pontuação em lote** é usado quando você precisa criar várias previsões muito rápidos, passando um SQL de consulta ou tabela como entrada. Uma tabela de resultados é retornada, que você pode inserir diretamente em uma tabela ou gravar em um arquivo.

- **Modo de pontuação individual** é usado quando você precisa criar uma previsão de cada vez. Você passa um conjunto de valores individuais para o procedimento armazenado. Os valores correspondem aos recursos no modelo, que usa o modelo para criar uma previsão, ou geram outro resultado como um valor de probabilidade. Em seguida, você pode retornar esse valor para o aplicativo ou usuário.

## <a name="batch-scoring"></a>A pontuação do lote

Um procedimento armazenado para a pontuação do lote foi criado quando você inicialmente executou o script do PowerShell. Esse procedimento armazenado, *PredictTipBatchMode*, faz o seguinte:

- Obtém um conjunto de dados de entrada como uma consulta SQL
- Chama o modelo de regressão logística treinado salvo na lição anterior
- Prevê a probabilidade de que o driver obtém qualquer dica diferente de zero

1. Reserve um minuto para examinar o script para o procedimento armazenado, *PredictTipBatchMode*. Ele ilustra vários aspectos de como um modelo pode ser colocado em operação usando [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].
  
    ```tsql
    CREATE PROCEDURE [dbo].[PredictTipBatchMode]
    @input nvarchar(max)
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

    + Você pode usar uma instrução SELECT para chamar o modelo armazenado em uma tabela SQL. O modelo é recuperado da tabela de **varbinary (max)** dados armazenados na variável SQL _@lmodel2_e passado como o parâmetro *mod* para o sistema armazenado procedimento [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

    + Os dados usados como entradas para a pontuação é definida como uma consulta SQL e armazenada como uma cadeia de caracteres na variável SQL _@input_. Os dados são recuperados do banco de dados, são armazenados em um quadro de dados chamado *InputDataSet*, que é apenas o nome padrão para dados de entrada para o [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) procedimento; você pode definir outro nome de variável, se necessário, usando o parâmetro *_@input_data_1_name_*.

    + Para gerar as pontuações, o procedimento armazenado chama a função `rxPredict` da biblioteca **RevoScaleR** .

    + O valor de retorno, *pontuação*, é a probabilidade, considerando o modelo, o driver obtém uma dica. Opcionalmente, você pode aplicar facilmente algum tipo de filtro para os valores retornados para categorizar os valores de retorno em "dica" e "nenhuma dica".  Por exemplo, uma probabilidade de menos de 0,5 significa que uma dica é improvável.
  
2.  Para chamar o procedimento armazenado no modo de lote, você deve definir a consulta necessária como entrada para o procedimento armazenado. Aqui está a consulta SQL. Você pode executá-lo no SSMS para verificar se ele funciona.

    ```SQL
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

3. Use este código de R para criar a cadeia de caracteres de entrada da consulta SQL:

    ```R
    input <- "N'SELECT TOP 10 a.passenger_count AS passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS direct_distance FROM (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a LEFT OUTER JOIN ( SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample  tablesample (1 percent) repeatable (98052)  )b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND  a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'";
    q <- paste("EXEC PredictTipBatchMode @inquery = ", input, sep="");
    ```

4. Para executar o procedimento armazenado de R, chame o **sqlQuery** método o **RODBC** do pacote e usar a conexão de SQL `conn` definido anteriormente:

    ```R
    sqlQuery (conn, q);
    ```

    Se você receber um erro de ODBC, verifique a sintaxe da consulta, e se você tem o número correto de aspas. 
    
    Se você receber um erro de permissões, verifique se que o logon tem a capacidade de executar o procedimento armazenado.

## <a name="single-row-scoring"></a>Pontuação de única linha

Ao chamar o modelo de previsão em uma base linha por linha, você pode passar um conjunto de valores que representam recursos para cada caso individual. O procedimento armazenado retorna uma única previsão ou a probabilidade. 

O procedimento armazenado *PredictTipSingleMode* demonstra essa abordagem. Ele usa como vários parâmetros que representam valores de recurso (por exemplo, passageiro contagem e viagem distância) de entrada, classifica esses recursos usando o modelo R armazenado e gera a probabilidade de dica.

1. Se o procedimento armazenado *PredictTipSingleMode* não foi criado pelo script do PowerShell inicial, você pode executar a seguinte instrução Transact-SQL para criá-lo agora.

    ```tsql
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

2. No SQL Server Management Studio, você pode usar o [!INCLUDE[tsql](../../includes/tsql-md.md)] **EXEC** procedimento (ou **EXECUTE**) para chamar o procedimento armazenado e passe as entradas necessárias. Por exemplo, tente executar essa instrução no Management Studio:

    ```SQL
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

    Os valores passados aqui são, respectivamente, para as variáveis _passageiro\_contagem_, _trip_distance_, _viagem\_tempo\_em\_s_, _retirada\_latitude_, _retirada\_longitude_, _redução\_latitude_, e _redução\_longitude_.

3. Para executar essa mesma chamada de código R, você simplesmente definir uma variável de R que contém a chamada de procedimento armazenado inteiro, como este:

    ```R
    q2 = "EXEC PredictTipSingleMode 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303 ";
    ```

    Os valores passados aqui são, respectivamente, para as variáveis _passageiro\_contagem_, _viagem\_distância_, _viagem\_tempo\_em\_s_, _retirada\_latitude_, _retirada\_longitude_, _redução\_ Latitude_, e _redução\_longitude_.

4. Chamar `sqlQuery` (da **RODBC** pacote) e passe a cadeia de caracteres de conexão, junto com a variável de cadeia de caracteres que contém a chamada de procedimento armazenado.

    ```R
    # predict with stored procedure in single mode
    sqlQuery (conn, q2);
    ```

    >[!TIP]
    > Ferramentas de R para Visual Studio (RTVS) fornece uma excelente integração com o SQL Server e R. Consulte este artigo para obter mais exemplos de como usar RODBC com uma conexão do SQL Server: [trabalhando com o SQL Server e do R](https://docs.microsoft.com/en-us/visualstudio/rtvs/sql-server)

## <a name="summary"></a>Resumo

Agora que você aprendeu como trabalhar com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados e manter modelos treinados de R para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], deve ser relativamente fácil para você criar novos modelos com base no conjunto de dados. Por exemplo, você pode tentar criar esses modelos adicionais:

- Um modelo de regressão que prevê o valor da gorjeta

- Um modelo de classificação multiclasse que prevê se a dica é pequeno, médio ou grande

Também é recomendável que você conheça alguns desses exemplos adicionais e recursos:

+ [Cenários de ciência de dados e modelos da solução](data-science-scenarios-and-solution-templates.md)

+ [Análise avançada no banco de dados](sqldev-in-database-r-for-sql-developers.md)

+ [Microsoft R - mergulhando na análise de dados](https://msdn.microsoft.com/microsoft-r/data-analysis-in-microsoft-r)

+ [Recursos adicionais](https://msdn.microsoft.com/microsoft-r/microsoft-r-more-resources)

## <a name="previous-lesson"></a>Lição anterior

[Criar um modelo de R e salvá-lo no SQL Server](walkthrough-build-and-save-the-model.md)

## <a name="next-steps"></a>Próximas etapas

[Tutoriais do SQL Server R](sql-server-r-tutorials.md)

[Como criar um procedimento armazenado usando sqlrutils](../r/how-to-create-a-stored-procedure-using-sqlrutils.md)
