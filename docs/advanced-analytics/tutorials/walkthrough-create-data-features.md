---
title: Criar recursos de dados usando R e SQL (passo a passo) | Microsoft Docs
ms.custom: 
ms.date: 08/23/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 4981d4eb-0874-4fe9-82e1-edf99890e27a
caps.latest.revision: 21
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ccdcc20a9bb66ba18f74975f725f24deb7028265
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="create-data-features-using-r-and-sql-walkthrough"></a>Criar recursos de dados usando R e SQL (passo a passo)

A engenharia de dados é uma parte importante do aprendizado de máquina. Dados geralmente requerem transformação antes que você pode usá-lo para modelagem de previsão. Se os dados não tiverem os recursos necessários, você deverá criá-los com base em valores existentes.

Para esta tarefa de modelagem, em vez de usar os valores brutos de latitude e longitude dos locais de embarque e desembarque de passageiros, você gostaria de ter a distância em milhas entre os dois locais. Para criar esse recurso, você calcular a distância linear direta entre dois pontos, usando o [haverseno fórmula](https://en.wikipedia.org/wiki/Haversine_formula).

Nesta etapa, vamos comparar dois métodos diferentes para criar um recurso de dados:

- Usando uma função personalizada de R
- Usando uma função personalizada do T-SQL em[!INCLUDE[tsql](../../includes/tsql-md.md)]

O objetivo é criar um novo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjunto de dados que inclui as colunas originais e o novo recurso numérico, *direct_distance*.

## <a name="featurization-using-r"></a>Personalização de R

A linguagem R é bem conhecida por suas bibliotecas estatísticas variadas e avançadas, mas talvez você ainda precise criar transformações de dados personalizadas.

Primeiro, vamos fazer isso os usuários de forma R estão acostumados a: obter os dados em seu laptop e, em seguida, executar uma função personalizada de R, *ComputeDist*, que calcula a distância linear entre dois pontos especificados pelos valores de latitude e longitude.

1. Lembre-se de que o objeto de fonte de dados que você criou anteriormente obtém somente as primeiras 1000 linhas. Portanto, vamos definir uma consulta que obtém todos os dados.

    ```R
    bigQuery <- "SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,  pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude FROM nyctaxi_sample";
    ```

2. Crie uma nova fonte de dados do SQL Server usando a consulta.

    ```R
    featureDataSource <- RxSqlServerData(sqlQuery = bigQuery,colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric", dropoff_longitude = "numeric", dropoff_latitude = "numeric", passenger_count  = "numeric", trip_distance  = "numeric", trip_time_in_secs  = "numeric", direct_distance  = "numeric"), connectionString = connStr);
    ```

    - [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) pode levar a uma consulta consiste em uma consulta SELECT válida, fornecida como o argumento para o _sqlQuery_ parâmetro ou o nome de um objeto de tabela, fornecido como o _tabela_ parâmetro.
    
    - Se você quiser dados de exemplo de uma tabela, você deve usar o _sqlQuery_ parâmetro, definir parâmetros de amostragem usando a cláusula TABLESAMPLE T-SQL e o _rowBuffering_ argumento como FALSE.

3. Execute o seguinte código para criar a função R personalizada. ComputeDist usa dois pares de valores de latitude e longitude e calcula a distância linear entre elas, retornando a distância em milhas.

    ```R
    env <- new.env();
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
  
    + A primeira linha define um novo ambiente. No R, um ambiente pode ser usado para encapsular namespaces em pacotes e assim por diante.  Você pode usar a função `search()` para exibir os ambientes no espaço de trabalho. Para exibir os objetos em um ambiente específico, digite `ls(<envname>)`.
    + As linhas que começam com `$env.ComputeDistance` contém o código que define a fórmula de Haversine, que calcula a *distância de grande círculo* entre dois pontos em uma esfera.

4. Após a definição de função, aplique-o a dados para criar uma nova coluna de recurso, *direct_distance*. mas, antes de executar a transformação, altere o contexto de computação para o local.

    ```R
    rxSetComputeContext("local");
    ```

5. Chamar o [rxDataStep](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) de função para obter o recurso de dados de engenharia e aplicar o `env$ComputeDist` função para os dados na memória.

    ```R
    start.time <- proc.time();
  
    changed_ds <- rxDataStep(inData = featureEngineeringQuery,
    transforms = list(direct_distance=ComputeDist(pickup_longitude,pickup_latitude, dropoff_longitude, dropoff_latitude),
    tipped = "tipped", fare_amount = "fare_amount", passenger_count = "passenger_count",
    trip_time_in_secs = "trip_time_in_secs",  trip_distance="trip_distance",
    pickup_datetime = "pickup_datetime",  dropoff_datetime = "dropoff_datetime"),
    transformEnvir = env,
    rowsPerRead=500,
    reportProgress = 3);
  
    used.time <- proc.time() - start.time;
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""));
    ```

    + A função rxDataStep oferece suporte a vários métodos para modificar dados em vigor. Para obter mais informações, consulte este artigo: [como transformar e o subconjunto de dados em Microsft R](https://docs.microsoft.com/r-server/r/how-to-revoscaler-data-transform)
    
    No entanto, alguns pontos vale a pena observar sobre rxDataStep: 
    
    Em outras fontes de dados, você pode usar os argumentos *varsToKeep* e *varsToDrop*, mas eles não têm suporte para fontes de dados do SQL Server. Portanto, neste exemplo, usamos o _transforma_ argumento para especificar as colunas de passagem e as colunas transformadas. Além disso, quando em execução em um SQL Server contexto de computação, o _inData_ argumento só pode ter uma fonte de dados do SQL Server.

    O código anterior também pode produzir uma mensagem de aviso quando executado em grandes conjuntos de dados. Quando o número de linhas vezes o número de colunas que está sendo criado excede um valor fixo (o padrão é 3,000,000), rxDataStep retorna um aviso e o número de linhas no quadro de dados retornados será truncado. Para remover o aviso, você pode modificar o _maxRowsByCols_ argumento na função rxDataStep. No entanto, se _maxRowsByCols_ é muito grande, você poderá ter problemas ao carregar o quadro de dados na memória.

7. Opcionalmente, você pode chamar [à função rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo) para inspecionar o esquema da fonte de dados transformados.

    ```R
    rxGetVarInfo(data = changed_ds);
    ```

## <a name="featurization-using-transact-sql"></a>Personalização usando Transact-SQL

Agora, crie uma função personalizada do SQL, *ComputeDist*, para realizar a mesma tarefa como a função R personalizada.

1. Defina uma nova função SQL personalizada chamada *fnCalculateDistance*. O código dessa função SQL definida pelo usuário é fornecido como parte do script do PowerShell executado para criar e configurar o banco de dados.  A função já deve existir no banco de dados.

    Se ela não existir, use o SQL Server Management Studio para gerar a função no mesmo banco de dados em que os dados de táxi são armazenados.

    ```sql
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)
    -- User-defined function calculates the direct distance between two geographical coordinates.
    RETURNS
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

2. Execute a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir de qualquer aplicativo que dê suporte a [!INCLUDE[tsql](../../includes/tsql-md.md)], apenas para ver como a função funciona.

    ```sql
    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
    pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
    FROM nyctaxi_sample
    ```
3. Após a definição dessa função, deve ser fácil de criar os recursos que você deseja usando SQL e, em seguida, inserir os valores diretamente em uma nova tabela:

    ```
    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
    pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
    INTO NewFeatureTable
    FROM nyctaxi_sample
    ```

4. No entanto, vamos ver como chamar a função SQL personalizada de código R. Primeiro, armazene a consulta de personalização do SQL em uma variável de R.

    ```R
    featureEngineeringQuery = "SELECT tipped, fare_amount, passenger_count,
        trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
        pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
        FROM nyctaxi_sample
        tablesample (1 percent) repeatable (98052)"
    ```
  
    > [!TIP]
    > Essa consulta foi modificada para obter um exemplo menor de dados, para agilizar a este passo a passo. Você pode remover a cláusula TABLESAMPLE se você deseja obter todos os dados; No entanto, dependendo do seu ambiente, pode não ser possível carregar o conjunto de dados completo em R, resultando em um erro.
  
5. Use as linhas de código a seguir para chamar a função [!INCLUDE[tsql](../../includes/tsql-md.md)] no ambiente do R e aplique-a aos dados definidos em *featureEngineeringQuery*.
  
    ```R
    featureDataSource = RxSqlServerData(sqlQuery = featureEngineeringQuery,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
             dropoff_longitude = "numeric", dropoff_latitude = "numeric",
             passenger_count  = "numeric", trip_distance  = "numeric",
              trip_time_in_secs  = "numeric", direct_distance  = "numeric"),
      connectionString = connStr)
    ```
  
6.  Agora que o novo recurso for criado, chamar **rxGetVarsInfo** para criar um resumo dos dados na tabela de recursos.
  
    ```R
    rxGetVarInfo(data = featureDataSource)
    ```

    *Resultados*

    ```
    Var 1: tipped, Type: integer
    Var 2: fare_amount, Type: numeric
    Var 3: passenger_count, Type: numeric
    Var 4: trip_time_in_secs, Type: numeric
    Var 5: trip_distance, Type: numeric
    Var 6: pickup_datetime, Type: character
    Var 7: dropoff_datetime, Type: character
    Var 8: direct_distance, Type: numeric
    Var 9: pickup_latitude, Type: numeric
    Var 10: pickup_longitude, Type: numeric
    Var 11: dropoff_latitude, Type: numeric
    Var 12: dropoff_longitude, Type: numeric
    ```

    > [!NOTE]
    > Em alguns casos, você poderá receber um erro como este: *executar a permissão foi negada no objeto 'fnCalculateDistance'* nesse caso, certifique-se de que o logon que você está usando tem permissões para executar scripts e criar objetos no banco de dados não apenas na instância.
    > Verifique o esquema para o objeto, fnCalculateDistance. Se o objeto foi criado pelo proprietário do banco de dados e seu logon pertence a função db_datareader, você precisa conceder permissões explícitas para executar o script de logon.

## <a name="comparing-r-functions-and-sql-functions"></a>Comparando funções de R e SQL

Lembre-se este trecho de código usado para o código de R de tempo?

```R
start.time <- proc.time()
<your code here>
used.time <- proc.time() - start.time
print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""))
```

Você pode tentar usar o suplemento com o exemplo de função personalizada do SQL para ver quanto tempo leva para a transformação de dados ao chamar uma função do SQL. Além disso, tente alternar contextos de computação com rxSetComputeContext e compare os intervalos.

Os horários podem variar significativamente, dependendo da velocidade da sua rede e sua configuração de hardware. Nas configurações testamos, o [!INCLUDE[tsql](../../includes/tsql-md.md)] abordagem de função era mais rápida que usar uma função personalizada de R. Portanto, temos que use o [!INCLUDE[tsql](../../includes/tsql-md.md)] função para esses cálculos nas etapas subsequentes.

> [!TIP]
> Frequentemente, recursos de engenharia usando [!INCLUDE[tsql](../../includes/tsql-md.md)] será mais rápido do que R. Por exemplo, o T-SQL inclui janelas rápida e as funções de classificação que podem ser aplicadas para cálculos de ciência de dados comuns como reverter as médias de movimentação e  *n* -lado a lado. Escolha o método mais eficiente com base em seus dados e tarefas.

## <a name="next-lesson"></a>Próxima lição

[Criar um modelo de R e salvar SQL](/walkthrough-build-and-save-the-model.md)

## <a name="previous-lesson"></a>Lição anterior

[Exibir e resumir dados usando R](/walkthrough-view-and-summarize-data-using-r.md)


