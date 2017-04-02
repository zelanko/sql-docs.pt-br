---
title: "Etapa 6: Colocar o modelo em opera&#231;&#227;o (Tutorial de an&#225;lise avan&#231;ada no banco de dados) | Microsoft Docs"
ms.custom: ""
ms.date: "04/19/2016"
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
  - "TSQL"
ms.assetid: 52b05828-11f5-4ce3-9010-59c213a674d1
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# Etapa 6: Colocar o modelo em opera&#231;&#227;o (Tutorial de an&#225;lise avan&#231;ada no banco de dados)
Nesta etapa, você aprenderá a *colocar o modelo em operação* usando um procedimento armazenado. Esse procedimento armazenado pode ser chamado diretamente por outros aplicativos, para fazer previsões sobre novas observações.  
  
Nesta etapa, você aprenderá dois métodos para chamar um modelo do R por meio de um procedimento armazenado:  
  
-   **Modo de pontuação de lote**: use uma consulta SELECT para fornecer várias linhas de dados. O procedimento armazenado retorna uma tabela de observações correspondente aos casos de entrada.  
  
-   **Modo de pontuação individual**: passe um conjunto de valores de parâmetros individuais como entrada.  O procedimento armazenado retorna uma única linha ou valor.  
  
Primeiro, vamos ver como a pontuação funciona em geral.  
  
## Pontuação básica  
O procedimento armazenado _PredictTip_ ilustra a sintaxe básica para encapsular uma chamada de previsão em um procedimento armazenado.  
  
```  
CREATE PROCEDURE [dbo].[PredictTip] @inquery nvarchar(max)  
AS  
BEGIN  
  
  DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model  
  FROM nyc_taxi_models);  
  EXEC sp_execute_external_script @language = N'R',  
                                  @script = N'  
mod <- unserialize(as.raw(model));  
print(summary(mod))  
OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL,   
          predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);  
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
  
-   A instrução SELECT obtém o modelo serializado do banco de dados e armazena o modelo na variável `mod` do R para processamento adicional com o R.  
  
-   Os novos casos que serão pontuados são obtidos por meio da consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] especificada no `@inquery`, o primeiro parâmetro do procedimento armazenado. Conforme os dados da consulta são lidos, as linhas são salvas no quadro de dados padrão, `InputDataSet`. Esse quadro de dados é passado para a função `rxPredict` no R, que gera as pontuações.  
  
    `OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL,            predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);`  
  
    Como um data.frame pode conter uma única linha, você pode usar o mesmo código para a pontuação única ou de lote.  
  
-   O valor retornado pela função `rxPredict` é um **float** que representa a probabilidade de uma gorjeta ser dada (de qualquer valor).  
  
## Pontuação de lote usando uma consulta SELECT  
Agora vamos ver como funciona a pontuação de lote.  
  
1.  Vamos começar obtendo um conjunto menor de dados de entrada com o qual trabalharemos.  
  
    ```  
    select top 10 a.passenger_count as passenger_count,   
        a.trip_time_in_secs as trip_time_in_secs,  
        a.trip_distance as trip_distance,  
        a.dropoff_datetime as dropoff_datetime,    
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) as direct_distance   
    from  
    (  
        select medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance,    
            dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude  
        from nyctaxi_sample  
    )a  
    left outer join  
    (  
    select medallion, hack_license, pickup_datetime  
    from nyctaxi_sample  
    tablesample (70 percent) repeatable (98052)  
    )b  
    on a.medallion=b.medallion and a.hack_license=b.hack_license and a.pickup_datetime=b.pickup_datetime  
    where b.medallion is null  
    ```  
  
    Esta consulta cria uma lista das “10 primeiras” corridas com contagem de passageiros e outros recursos necessários para fazer uma previsão.  
  
 **Resultados**  
  
*passenger_count   trip_time_in_secs    trip_distance  dropoff_datetime   direct_distance*  
*1  283 0.7 2013-03-27 14:54:50.000   0.5427964547*  
*1  289 0.7 2013-02-24 12:55:29.000   0.3797099614*  
*1  214 0.7 2013-06-26 13:28:10.000   0.6970098661*  
*1  276 0.7 2013-06-27 06:53:04.000   0.4478814362*  
*1  282 0.7 2013-02-21 07:59:54.000   0.5340645749*  
*1  260 0.7 2013-03-27 15:40:49.000   0.5513900727*  
*1  230 0.7 2013-02-05 09:47:59.000   0.5161578519*  
*1  250 0.7 2013-05-08 14:35:51.000   0.5626440915*  
*1  280 0.7 2013-05-11 12:22:01.000   0.5598517959*  
*1  308 0.7 2013-04-10 08:06:00.000   0.4478814362*  
  
Você usará essa consulta como entrada para o procedimento armazenado, _PredictTipBatchMode_, que foi fornecido como parte do download.  
  
2.  Primeiro, reserve um minuto para examinar o código do procedimento armazenado _PredictTipBatchMode_ no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
    ```  
    /****** Object:  StoredProcedure [dbo].[PredictTipBatchMode]  ******/  
    SET ANSI_NULLS ON  
    GO  
    SET QUOTED_IDENTIFIER ON  
    GO  
  
    CREATE PROCEDURE [dbo].[PredictTipBatchMode] @inquery nvarchar(max)  
    AS  
    BEGIN  
  
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model  
      FROM nyc_taxi_models);  
      EXEC sp_execute_external_script @language = N'R',  
                                      @script = N'  
    mod <- unserialize(as.raw(model));  
    print(summary(mod))  
    OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL,   
              predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);  
    str(OutputDataSet)  
    print(OutputDataSet)  
    ',  
                                      @input_data_1 = @inquery,  
                                      @params = N'@model varbinary(max)',  
                                      @model = @lmodel2  
      WITH RESULT SETS ((Score float));  
  
    END  
    ```  
  
3.  Para criar previsões, você fornecerá o texto da consulta em uma variável e o passará como um parâmetro para o procedimento armazenado, usando uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] como esta.  
  
    ```  
    -- Specify input query  
  
    DECLARE @query_string nvarchar(max)  
    SET @query_string='  
    select top 10 a.passenger_count as passenger_count,   
        a.trip_time_in_secs as trip_time_in_secs,  
        a.trip_distance as trip_distance,  
        a.dropoff_datetime as dropoff_datetime,    
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) as direct_distance   
    from  
        select medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance,    
            dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude  
        from nyctaxi_sample  
    )a  
    left outer join  
    (  
    select medallion, hack_license, pickup_datetime  
    from nyctaxi_sample  
    tablesample (70 percent) repeatable (98052)  
    )b  
    on a.medallion=b.medallion and a.hack_license=b.hack_license and a.pickup_datetime=b.pickup_datetime  
    where b.medallion is null'  
  
    -- Call stored procedure for scoring  
    EXEC [dbo].[PredictTip] @inquery = @query_string;  
  
    ```  
  
4.  O procedimento armazenado retorna uma série de valores que representam a previsão de cada uma das “10 primeiras corridas”. Observando novamente os valores de entrada, todas as “10 primeiras corridas” são corridas de passageiro único com uma distância de corrida relativamente curta. Com base nos dados, é muito pouco provável que o motorista receba uma gorjeta nessas corridas.  
  
    Em vez de retornar apenas os resultados de Sim-gorjeta/Sem gorjeta, você também pode retornar a pontuação de probabilidade da previsão e aplicar uma cláusula WHERE aos valores de coluna _Pontuar_ para categorizar a pontuação como “propenso a dar gorjeta” ou “não propenso a dar gorjeta”, usando um valor de limite como 0,5 ou 0,7. Essa etapa não está incluída no procedimento armazenado, mas seria fácil de ser implementada.  
  
## Pontuar linhas individuais  
Às vezes, você deseja passar valores individuais de um aplicativo e obter um único resultado com base nesses valores. Por exemplo, você poderá definir uma planilha do Excel, um aplicativo Web ou um relatório do Reporting Services para chamar o procedimento armazenado e fornecer entradas digitadas ou selecionadas por usuários.  
  
Nesta seção, você aprenderá a criar previsões únicas usando um procedimento armazenado.  
  
1.  Reserve um minuto para examinar o código do procedimento armazenado _PredictTipSingleMode_, incluído como parte do download.  
  
    ```  
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
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model  
      FROM nyc_taxi_models);  
      EXEC sp_execute_external_script @language = N'R',  
                                      @script = N'  
    mod <- unserialize(as.raw(model));  
    print(summary(mod))  
    OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL,   
              predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);  
    str(OutputDataSet)  
    print(OutputDataSet)  
    ',  
    @input_data_1 = @inquery,  
    @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,@trip_time_in_secs int ,  
    @pickup_latitude float ,@pickup_longitude float ,@dropoff_latitude float ,@dropoff_longitude float',  
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
  
    -   Esse procedimento armazenado usa vários valores únicos como entrada, como contagem de passageiros, distância da corrida e assim por diante.  
  
        Se você chamar o procedimento armazenado de um aplicativo externo, verifique se os dados correspondem aos requisitos do modelo do R. Isso pode incluir a garantia de que os dados de entrada possam ser convertidos em um tipo de dados do R ou a validação do tipo e comprimento dos dados. Para obter mais informações, consulte [Trabalhando com tipos de dados do R](https://msdn.microsoft.com/library/mt590948.aspx).  
  
    -   O procedimento armazenado cria uma pontuação com base no modelo do R armazenado.  
  
2.  Experimente usá-lo, fornecendo os valores manualmente.  
  
    Abra uma nova janela **Consulta** e chame o procedimento armazenado, digitando parâmetros para cada uma das colunas de recursos.  
  
    ```  
  
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303  
  
    ```  
  
    Estes são os valores para essas colunas de recursos, na ordem:  
  
    -   *trip_time_in_secs*  
    -   *pickup_latitude*  
    -   *pickup_longitude*  
    -   *dropoff_latitude*  
    -   *dropoff_longitude*  
  
3.  Os resultados indicam que a probabilidade de receber uma gorjeta é muito baixa nessas 10 primeiras corridas, que são corridas de passageiro único em uma distância relativamente curta.  
  
## Conclusões  
Neste tutorial, você aprendeu a trabalhar com código do R inserido em procedimentos armazenados. A integração com o [!INCLUDE[tsql](../../includes/tsql-md.md)] torna muito mais fácil a implantação de modelos do R para previsão e incorporação do novo treinamento do modelo como parte de um fluxo de trabalho de dados empresariais.  
  
  
## Etapa anterior  
[Etapa 4: Criar recursos de dados usando o T-SQL](../../advanced-analytics/r-services/step-4-create-data-features-using-t-sql-in-database-advanced-analytics-tutorial.md)  
  
## Consulte também  
[Análise avançada no banco de dados para desenvolvedores do SQL &#40;Tutorial&#41;](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  
[Tutoriais do SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  
