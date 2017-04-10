---
title: "Li&#231;&#227;o 5: Implantar e usar o modelo (Passo a passo de ponta a ponta sobre a ci&#234;ncia de dados) | Microsoft Docs"
ms.custom: ""
ms.date: "11/22/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: f28a7aac-6d08-4781-ad28-b48d18cc16a0
caps.latest.revision: 17
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 17
---
# Li&#231;&#227;o 5: Implantar e usar o modelo (Passo a passo de ponta a ponta sobre a ci&#234;ncia de dados)
Nesta lição, você aprenderá a usar os modelos do R em um ambiente de produção, encapsulando o modelo persistente em um procedimento armazenado. Em seguida, você pode invocar o procedimento armazenado no R ou em uma linguagem de programação de aplicativo que dá suporte ao [!INCLUDE[tsql](../../includes/tsql-md.md)] (como C#, Java, Python, etc.) para usar o modelo a fim de fazer previsões sobre novas observações.  
  
Há duas maneiras diferentes pelas quais você pode chamar um modelo de pontuação:  
  
-   O**modo de pontuação de lote** permite criar várias previsões com base na entrada de uma consulta SELECT.  
  
-   O**modo de pontuação individual** permite criar previsões individualmente, passando um conjunto de valores de recursos de um caso individual para o procedimento armazenado, que retorna uma única previsão ou outro valor como resultado.  
  
Você aprenderá a criar previsões usando métodos de pontuação individual e de lote.  
  
## <a name="batch-scoring"></a>Pontuação do lote  
Para sua conveniência, você pode usar um procedimento armazenado criado quando você executou o script do PowerShell na Lição 1 pela primeira vez. Esse procedimento armazenado faz o seguinte:  
  
-   Obtém um conjunto de dados de entrada como uma consulta SQL    
-   Chama o modelo de regressão logística treinado salvo na lição anterior    
-   Prevê a probabilidade de que o motorista receberá uma gorjeta  
  
### <a name="use-the-stored-procedure-predicttipbatchmode"></a>Usar o procedimento armazenado PredictTipBatchMode

1. Reserve um minuto para examinar o script que define o procedimento armazenado, *PredictTipBatchMode*. Ele ilustra vários aspectos de como um modelo pode ser colocado em operação usando [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].  
  
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

    + Observe a instrução SELECT que chama o modelo armazenado. Você pode armazenar qualquer modelo treinado em uma tabela SQL, usando uma coluna do tipo **varbinary(max)**. Nesse código, o modelo é recuperado da tabela, armazenado na variável SQL _@lmodel2_, e passado como o parâmetro *mod* para o procedimento armazenado do sistema [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).
    + Os dados de entrada usados para pontuação são passados como uma cadeia de caracteres para o procedimento armazenado.  
  
        Para definir os dados de entrada desse modelo específico, crie uma consulta que retorna dados válidos. Como os dados são recuperados do banco de dados, eles são armazenados em um quadro de dados chamado *InputDataSet*. Todas as linhas deste quadro de dados são usadas para a pontuação em lote.
        + *InputDataSet* é o nome padrão de dados de entrada para o procedimento [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md); se necessário, você poderá definir outro nome de variável.
        + Para gerar as pontuações, o procedimento armazenado chama a função *rxPredict* da biblioteca **RevoScaleR**.
    + O valor retornado do procedimento armazenado, *Score*, é uma probabilidade prevista de que o motorista receberá uma gorjeta.  
  
2.  Como opção, você poderia facilmente aplicar algum tipo de filtro aos valores retornados para categorizá-los em grupos “sim – gorjeta” ou “sem gorjeta”.  Por exemplo, uma probabilidade inferior a 0,5 significa que nenhuma gorjeta é provável.  
  
3.  Chame o procedimento armazenado no modo de lote:  
  
    ```R  
    input = "N' 
      SELECT TOP 10 
          a.passenger_count AS passenger_count,   
          a.trip_time_in_secs AS trip_time_in_secs,  
          a.trip_distance AS trip_distance,  
          a.dropoff_datetime AS dropoff_datetime,    
          dbo.fnCalculateDistance(
            pickup_latitude, 
            pickup_longitude, 
            dropoff_latitude,
            dropoff_longitude) AS direct_distance   
      FROM  
      
      (SELECT medallion, hack_license, pickup_datetime,   
      passenger_count,trip_time_in_secs,trip_distance,    
      dropoff_datetime, pickup_latitude, pickup_longitude,   
      dropoff_latitude, dropoff_longitude from nyctaxi_sample)a  
      
      LEFT OUTER JOIN  
 
      ( SELECT medallion, hack_license, pickup_datetime 
        FROM nyctaxi_sample  tablesample (1 percent) repeatable (98052)  )b  

      ON a.medallion=b.medallion 
        AND a.hack_license=b.hack_license 
        AND a.pickup_datetime=b.pickup_datetime  

      WHERE b.medallion is null  
    '"  
    q<-paste("EXEC PredictTipBatchMode @inquery = ", input, sep="")  
    sqlQuery (conn, q)  
  
    ```  
  
## <a name="single-row-scoring"></a>Pontuação de linha simples  

Em vez de usar uma consulta para passar os valores de entrada para o modelo do R salvo, talvez você queira fornecer os recursos como argumentos para o procedimento armazenado.  

### <a name="use-the-stored-procedure-predicttipsinglemode"></a>Usar o procedimento armazenado PredictTipSingleMode
1.  Reserve um minuto para revisar o código a seguir para o procedimento armazenado, *PredictTipSingleMode*, que deve ser criado no banco de dados.  
  
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
        SELECT * FROM [dbo].[fnEngineerFeatures](@passenger_count, 
            @trip_distance,  
            @trip_time_in_secs,  
            @pickup_latitude,  
            @pickup_longitude,  
            @dropoff_latitude,  
            @dropoff_longitude)  
        '  
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
      @params = N'@model varbinary(max),
                @passenger_count int,
                @trip_distance float,
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
    ```  
  
    Esse procedimento armazenado usa valores de recursos como entrada, como contagem de passageiros e distância da corrida, pontua esses recursos usando o modelo do R armazenado e gera uma pontuação.  
  
### <a name="call-the-stored-procedure-and-pass-parameters"></a>Chamar o procedimento armazenado e passar os parâmetros

1. No SQL Server Management Studio, você pode usar o [!INCLUDE[tsql](../../includes/tsql-md.md)] **EXEC** para chamar o procedimento armazenado e passar as entradas necessárias. .  
    ```tsql  
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303   
    ```  
  
    Os valores passados aqui referem-se, respectivamente, às variáveis _passenger_count_, _trip_distance_, _trip_time_in_secs_, _pickup_latitude_, _pickup_longitude_, _dropoff_latitude_e _dropoff_longitude_.  
  
2.  Para executar essa mesma chamada do código de R, você simplesmente define uma variável de R que contenha a chamada de procedimento armazenado inteiro. 
  
    ```R  
    q = "EXEC PredictTipSingleMode 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303 "  
    ```  
  
    Os valores passados aqui referem-se, respectivamente, às variáveis _passenger_count_, _trip_distance_, _trip_time_in_secs_, _pickup_latitude_, _pickup_longitude_, _dropoff_latitude_e _dropoff_longitude_.  
  
### <a name="generate-scores"></a>Gerar pontuações

1. Chame a função *sqlQuery* do pacote **RODBC** e passe a cadeia de conexão e a variável de cadeia de caracteres que contêm a chamada de procedimento armazenado.  
  
    ```R  
    # predict with stored procedure in single mode  
    sqlQuery (conn, q)   
    ```  
  
    Para saber mais sobre **RODBC**, visite [http://www.inside-r.org/packages/cran/RODBC/docs/sqlQuery](http://www.inside-r.org/packages/cran/RODBC/docs/sqlQuery).  
  
## <a name="conclusion"></a>Conclusão  
Agora que você já sabe como trabalhar com dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e persistir modelos treinados do R no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], deve ser relativamente fácil criar alguns modelos adicionais com base nesse conjunto de dados. Por exemplo, você poderá tentar criar modelos como estes:  
  
-   Um modelo de regressão que prevê o valor da gorjeta    
-   Um modelo de classificação de várias classes que prevê se a gorjeta será pequena, média ou grande.  

Também é recomendável que você conheça alguns desses exemplos adicionais e recursos: 
+ [Cenários de ciência de dados e modelos da solução](../../advanced-analytics/r-services/data-science-scenarios-and-solution-templates.md)
+ [Análise avançada no banco de dados](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)
+ [Microsoft R - mergulhando na análise de dados](https://msdn.microsoft.com/microsoft-r/data-analysis-in-microsoft-r)
+ [Recursos adicionais](https://msdn.microsoft.com/microsoft-r/microsoft-r-more-resources)
## <a name="previous-lesson"></a>Lição anterior  
[Lição 4: Criar e salvar o modelo &#40;Passo a passo de ponta a ponta sobre a ciência de dados&#41;](../../advanced-analytics/r-services/lesson-4-build-and-save-the-model-data-science-end-to-end-walkthrough.md)  
  
## <a name="see-also"></a>Consulte também  
[Tutoriais do SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  
