---
title: "Etapa 5: Treinar e salvar um modelo usando o T-SQL (Tutorial de an&#225;lise avan&#231;ada no banco de dados) | Microsoft Docs"
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
ms.assetid: 3282e8ed-b515-4ed5-8543-fcef68629a92
caps.latest.revision: 10
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# Etapa 5: Treinar e salvar um modelo usando o T-SQL (Tutorial de an&#225;lise avan&#231;ada no banco de dados)
Nesta etapa, você aprenderá a treinar um modelo de aprendizado de máquina usando o R. Os pacotes do R já estão instalados no [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] para que você possa chamar o algoritmo por meio de um procedimento armazenado. Você treinará o modelo usando os recursos de dados que acabou de criar e salvará o modelo treinado em uma tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## Criando um modelo do R usando procedimentos armazenados  
Todas as chamadas para o tempo de execução do R que são instaladas com o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] são feitas usando o procedimento armazenado do sistema [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). No entanto, se você precisar treinar um modelo novamente, provavelmente será mais fácil encapsular a chamada para sp_execute_exernal_script em outro procedimento armazenado.  
  
Nesta seção, você criará um procedimento armazenado que pode ser usado para criar um modelo usando os dados que você acabou de preparar. Esse procedimento armazenado define os dados de entrada e usa um pacote do R para criar um modelo de regressão logística.  
  
#### Para criar o procedimento armazenado  
  
1.  No [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra uma nova janela de Consulta e execute a instrução a seguir para criar o procedimento armazenado _TrainTipPredictionModel_.  
  
    Observe que, como o procedimento armazenado já inclui uma definição dos dados de entrada, você não precisa fornecer uma consulta de entrada.  
  
    ```  
    CREATE PROCEDURE [dbo].[TrainTipPredictionModel]  
  
    AS  
    BEGIN  
      DECLARE @inquery nvarchar(max) = N'  
        select tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance,   
        pickup_datetime, dropoff_datetime,   
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance  
        from nyctaxi_sample  
        tablesample (70 percent) repeatable (98052)  
    '  
      -- Insert the trained model into a database table  
      INSERT INTO nyc_taxi_models  
      EXEC sp_execute_external_script @language = N'R',  
                                      @script = N'  
  
    ## Create model  
    logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = InputDataSet)  
    summary(logitObj)  
  
    ## Serialize model and put it in data frame  
    trained_model <- data.frame(model=as.raw(serialize(logitObj, NULL)));  
    ',  
                                      @input_data_1 = @inquery,  
                                      @output_data_1_name = N'trained_model'  
      ;  
  
    END  
    GO  
  
    ```  
  
    Esse procedimento armazenado executa estas atividades como parte do treinamento do modelo:  
  
    -   Para garantir que há alguns dados para testar o modelo, 70% dos dados são selecionados aleatoriamente da tabela de dados de táxi.  
  
    -   A consulta SELECT usa a função escalar personalizada _fnCalculateDistance_ para calcular a distância direta entre os locais de embarque e desembarque de passageiros.  os resultados da consulta são armazenados na variável de entrada padrão do R, `InputDataset`.  
  
    -   o script do R chama a função `rxLogit`, que é uma das funções avançadas do R incluídas no [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], para criar o modelo de regressão logística.  
  
        A variável binária _tipped_ é usada como a coluna *label* ou de resultado, e o modelo é ajustado com o uso destas colunas de recursos: _passenger_count_, _trip_distance_, _trip_time_in_secs_ e _direct_distance_.  
  
    -   O modelo treinado, salvo na variável do R `logitObj`, é serializado e colocado em um quadro de dados para a saída no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa saída é inserida na tabela de banco de dados _nyc_taxi_models_, de modo que você possa usá-la para previsões futuras.  
  
2.  Execute a instrução para criar o procedimento armazenado.  
  
#### Para criar o modelo do R usando o procedimento armazenado  
  
1.  No [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], execute esta instrução.  
  
    ```  
    EXEC TrainTipPredictionModel  
    ```  
  
    O processamento dos dados e o ajuste do modelo poderão levar algum tempo. As mensagens que serão redirecionadas para o fluxo **stdout** do R são exibidas na janela **Mensagens** do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Por exemplo:  
  
  
*Mensagem(ns) STDOUT do script externo: Linhas lidas: 1193025, Total de Linhas Processadas: 1193025, Tempo Total: 0.093 segundos*       
  
Partes sucessivas dos dados são lidas e processadas. Você também pode ver mensagens específicas da função individual, `rxLogit`, indicando a variável e métricas de teste.  
  
2.  Abra a tabela *nyc_taxi_models*. Você pode ver que uma nova linha foi adicionada, que contém o modelo serializado na coluna _modelo_.  
  
  
  
*modelo*  
*0x580A00000002000302020....*  
  
Na próxima etapa, você usará o modelo treinado para criar previsões.  
  
## Próxima etapa  
[Etapa 6: Colocar o modelo em operação](../../advanced-analytics/r-services/step-6-operationalize-the-model-in-database-advanced-analytics-tutorial.md)  
  
## Etapa anterior  
[Etapa 4: Criar recursos de dados usando o T-SQL](../../advanced-analytics/r-services/step-4-create-data-features-using-t-sql-in-database-advanced-analytics-tutorial.md)  
  
## Consulte também  
[Análise avançada no banco de dados para desenvolvedores do SQL &#40;Tutorial&#41;](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  
[Tutoriais do SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  
