---
title: "Li&#231;&#227;o 3: Criar recursos de dados (Passo a passo de ponta a ponta sobre a ci&#234;ncia de dados) | Microsoft Docs"
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
ms.assetid: 4981d4eb-0874-4fe9-82e1-edf99890e27a
caps.latest.revision: 21
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 17
---
# Li&#231;&#227;o 3: Criar recursos de dados (Passo a passo de ponta a ponta sobre a ci&#234;ncia de dados)
A engenharia de dados é outra parte importante do aprendizado de máquina. Com frequência, os dados precisam ser transformados antes que você possa usá-los para a modelagem preditiva. Se os dados não tiverem os recursos necessários, você deverá criá-los com base em valores existentes.  
  
Para esta tarefa de modelagem, em vez de usar os valores brutos de latitude e longitude dos locais de embarque e desembarque de passageiros, você gostaria de ter a distância em milhas entre os dois locais. Para criar esse recurso, você calculará a distância linear direta entre dois pontos usando a [fórmula de Haversine](https://en.wikipedia.org/wiki/Haversine_formula).  
Você vai comparar dois métodos diferentes para criar um recurso com base nos dados:  
  
-   Usando o R e a função `rxDataStep`    
-   Usando uma função personalizada no [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
Para os dois métodos, o resultado do código é um objeto de fonte de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , `featureDataSource`, que inclui o novo recurso numérico, `direct_distance`.  
  
## <a name="creating-features-using-r"></a>Criando recursos usando o R  

A linguagem R é bem conhecida por suas bibliotecas estatísticas variadas e avançadas, mas talvez você ainda precise criar transformações de dados personalizadas. 

+ Você criará uma nova função do R, `ComputeDist`, para calcular a distância linear entre dois pontos especificados por valores de latitude e longitude.  
+ Você chamará a função para transformar os dados no objeto de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criado anteriormente e os salvará em uma nova fonte de dados, `featureDataSource`.  

### <a name="create-the-transformation-function"></a>Criar a função de transformação  
1.  Criar uma função do R personalizada, `ComputeDist`. Ela usa dois pares de valores de latitude e longitude e calcula a distância linear entre eles.  A função retorna a distância em milhas.
  
    ```R  
    env <- new.env()  
    env$ComputeDist <- function(pickup_long, pickup_lat, dropoff_long, dropoff_lat){  
      R <- 6371/1.609344 #radius in mile  
      delta_lat <- dropoff_lat - pickup_lat  
      delta_long <- dropoff_long - pickup_long  
      degrees_to_radians = pi/180.0  
      a1 <- sin(delta_lat/2*degrees_to_radians)  
      a2 <- as.numeric(a1)^2  
      a3 <- cos(pickup_lat*degrees_to_radians)  
      a4 <- cos(dropoff_lat*degrees_to_radians)  
      a5 <- sin(delta_long/2*degrees_to_radians)  
      a6 <- as.numeric(a5)^2  
      a <- a2+a3*a4*a6  
      c <- 2*atan2(sqrt(a),sqrt(1-a))  
      d <- R*c  
      return (d)  
    }  
    ```  
  
    + A primeira linha define um novo ambiente. No R, um ambiente pode ser usado para encapsular namespaces em pacotes e assim por diante.
    + Você pode usar a função `search()` para exibir os ambientes no espaço de trabalho. Para exibir os objetos em um ambiente específico, digite `ls(<envname>)`. 
    + As linhas que começam com `$env.ComputeDistance` contém o código que define a fórmula de Haversine, que calcula a *distância de grande círculo* entre dois pontos em uma esfera.  
 
  
### <a name="apply-the-transformation-function-to-data"></a>Aplicar a função de transformação aos dados

Após a definição da função, você a aplicará aos dados para criar uma nova coluna de recurso, *direct_distance*.

1. Criar uma fonte de dados com a qual trabalhar usando o construtor `RxSqlServerData`.  
  
    ```R  
    featureDataSource = RxSqlServerData(table = "features",   
       colClasses = c(pickup_longitude = "numeric", 
       pickup_latitude = "numeric",   
       dropoff_longitude = "numeric", 
       dropoff_latitude = "numeric",  
       passenger_count  = "numeric", 
       trip_distance  = "numeric",  
       trip_time_in_secs  = "numeric", 
       direct_distance  = "numeric"),  
      connectionString = connStr)  
    ```  
  
3.  Chamar a função `rxDataStep` para aplicar a função `env$ComputeDist` aos dados especificados.  
    
    ```R  
    start.time <- proc.time()  
  
    rxDataStep(inData = inDataSource, outFile = featureDataSource,  
         overwrite = TRUE,  
         varsToKeep=c("tipped", "fare_amount", passenger_count", "trip_time_in_secs", 
            "trip_distance", "pickup_datetime", "dropoff_datetime", "pickup_longitude",
            "pickup_latitude", "dropoff_longitude", "dropoff_latitude")
         , transforms = list(direct_distance=ComputeDist(pickup_longitude, 
            pickup_latitude, dropoff_longitude, dropoff_latitude)),
            transformEnvir = env, rowsPerRead=500, reportProgress = 3)  
  
    used.time <- proc.time() - start.time  
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""))    
    ```  
  
    + A função `rxDataStep` pode modificar dados in-loco. Os argumentos incluem um vetor de caractere de colunas de passagem (*varsToKeep*) e uma lista que define as transformações.
    + As colunas transformadas são geradas automaticamente e, portanto, não precisam ser incluídas no argumento *varsToKeep* .
    + Como alternativa, você pode especificar que todas as colunas na fonte sejam incluídas, exceto as variáveis especificadas, usando o argumento *varsToDrop* .  
  
4.  Por fim, chame o `rxGetVarInfo` para inspecionar o esquema da nova fonte de dados:  
  
    ```R  
    rxGetVarInfo(data = featureDataSource)  
    ```  
  
    *Resultados*
    
    *"Demora CPU = 0,74 segundo, Tempo decorrido = 35,75 segundos para gerar recursos."*  
    *Var 1: tipped, Type: integer*   
    *Var 2: fare_amount, Type: numeric*   
    *Var 3: passenger_count, Type: numeric*   
    *Var 4: trip_time_in_secs, Type: numeric*   
    *Var 5: trip_distance, Type: numeric*   
    *Var 6: pickup_datetime, Type: character*   
    *Var 7: dropoff_datetime, Type: character*   
    *Var 8: pickup_longitude, Type: numeric*   
    *Var 9: pickup_latitude, Type: numeric*   
    *Var 10: dropoff_longitude, Type: numeric*   
    *Var 11: dropoff_latitude, Type: numeric*   
    *Var 12: direct_distance, Type: numeric*   
  
## <a name="creating-features-using-transact-sql"></a>Criando recursos usando o Transact-SQL  
Agora que você já viu como criar um recurso usando uma função do R, você usará uma função SQL personalizada, `ComputeDist`, para fazer a mesma coisa. A função SQL `ComputeDist` opera em um objeto de dados `RxSqlServerData` existente para criar os novos recursos de distância com base nos valores de longitude e latitude existentes.  
  
Você salvará os resultados da transformação em um objeto de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , `featureDataSource`, exatamente como fez usando o R.  
  
Com muita frequência, a engenharia de recursos com o [!INCLUDE[tsql](../../includes/tsql-md.md)] será mais rápida do que o R. Escolha o método mais eficiente com base nos dados e nas tarefas.  

### <a name="define-the-t-sql-custom-function"></a>Definir a função personalizada T-SQL
  
1.  Definir uma nova função SQL, `fnCalculateDistance`  
  
    ```tsql  
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)  
    -- User-defined function calculates the direct distance between two geographical coordinates.  
    RETURNS float  
    AS  
    BEGIN  
      DECLARE @distance decimal(28, 10)  
      -- Convert to radians  
      SET @Lat1 = @Lat1 / 57.2958  
      SET @Long1 = @Long1 / 57.2958  
      SET @Lat2 = @Lat2 / 57.2958  
      SET @Long2 = @Long2 / 57.2958  
      -- Calculate distance  
      SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))  
      --Convert to miles  
      IF @distance <> 0  
      BEGIN  
        SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);  
      END  
      RETURN @distance  
    END  
  
    ```  

    + O código dessa *função definida pelo usuário* SQL foi fornecida como parte do script do PowerShell executado para criar e configurar o banco de dados.  A função já deve existir no banco de dados.  Se ela não existir, use o SQL Server Management Studio para gerar a função no mesmo banco de dados onde os dados de táxi são armazenados.

2.  Para ver como funciona a função, a seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] de qualquer aplicativo que oferece suporte a [!INCLUDE[tsql](../../includes/tsql-md.md)].   
  
    ```tsql  
    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,       
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,  
    pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude   
    FROM nyctaxi_sample  
  
    ```  
### <a name="call-the-sql-function-from-r"></a>Chamar a função SQL de R

1. Salve a instrução SQL que chama a função personalizada em uma variável de R.  
  
    ```R  
    featureEngineeringQuery = "SELECT tipped, fare_amount, passenger_count,  
        trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,   
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,  
        pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude  
        FROM nyctaxi_joined_1_percent  
        tablesample (1 percent) repeatable (98052)"    
    ```  
  
    > [!TIP] Observe que esta consulta é um pouco diferente da consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] usada anteriormente. Ela foi modificada para obter uma amostra menor de dados, a fim de agilizar este passo a passo.  
  
4.  Agora, use as linhas de código a seguir para chamar a função [!INCLUDE[tsql](../../includes/tsql-md.md)] no ambiente do R e aplique-a aos dados definidos em `featureEngineeringQuery`.  
  
    ```R  
    featureDataSource = RxSqlServerData(sqlQuery = featureEngineeringQuery,  
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",           
             dropoff_longitude = "numeric", dropoff_latitude = "numeric",  
             passenger_count  = "numeric", trip_distance  = "numeric",  
              trip_time_in_secs  = "numeric", direct_distance  = "numeric"),  
      connectionString = connStr)  
    ```  
  
5.  Agora que o novo recurso foi criado, chame `rxGetVarsInfo` para criar um resumo da tabela de recursos.  
  
    ```R  
    rxGetVarInfo(data = featureDataSource)  
    ```  
  
## <a name="comparing-r-functions-and-sql-functions"></a>Comparação de funções do R e do SQL

Na verdade, para essa tarefa específica, a abordagem da função [!INCLUDE[tsql](../../includes/tsql-md.md)] é mais rápida do que a função personalizada do R. Portanto, você usará a função [!INCLUDE[tsql](../../includes/tsql-md.md)] para esses cálculos nas próximas etapas.  

Vá para a próxima lição para saber como criar um modelo preditivo usando esses dados e salvar o modelo em uma tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="next-lesson"></a>Próxima lição  
[Lição 4: Criar e salvar o modelo &#40;Passo a passo de ponta a ponta sobre a ciência de dados&#41;](../../advanced-analytics/r-services/lesson-4-build-and-save-the-model-data-science-end-to-end-walkthrough.md)  
  
## <a name="previous-lesson"></a>Lição anterior  
[Lição 2: Exibir e explorar os dados &#40;Passo a passo de ponta a ponta sobre a ciência de dados&#41;](../../advanced-analytics/r-services/lesson-2-view-and-explore-the-data-data-science-end-to-end-walkthrough.md)  
  
  
  
