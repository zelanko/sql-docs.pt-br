---
title: Criar recursos de dados usando o R e o SQL Server Functions
description: Tutorial mostrando como criar recursos de dados usando funções de SQL Server para análise no banco de dados.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f12c20a54c0811e392eaa85684d7fac1a209c396
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714692"
---
# <a name="create-data-features-using-r-and-sql-server-walkthrough"></a>Criar recursos de dados usando R e SQL Server (explicação)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

A engenharia de dados é uma parte importante do aprendizado de máquina. Geralmente, os dados exigem transformação antes que você possa usá-los para modelagem preditiva. Se os dados não tiverem os recursos necessários, você deverá criá-los com base em valores existentes.

Para esta tarefa de modelagem, em vez de usar os valores brutos de latitude e longitude dos locais de embarque e desembarque de passageiros, você gostaria de ter a distância em milhas entre os dois locais. Para criar esse recurso, você computa a distância linear direta entre dois pontos, usando a [fórmula Haversine](https://en.wikipedia.org/wiki/Haversine_formula).

Nesta etapa, aprenda dois métodos diferentes para criar um recurso a partir dos dados:

> [!div class="checklist"]
> * Usando uma função de R personalizada
> * Usando uma função T-SQL personalizada no[!INCLUDE[tsql](../../includes/tsql-md.md)]

O objetivo é criar um novo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjunto de dados que inclua as colunas originais mais o novo recurso numérico, *direct_distance*.

## <a name="prerequisites"></a>Pré-requisitos

Esta etapa pressupõe uma sessão de R em andamento com base nas etapas anteriores neste passo a passos. Ele usa as cadeias de conexão e os objetos de fonte de dados criados nessas etapas. As seguintes ferramentas e pacotes são usados para executar o script.

+ Rgui. exe para executar comandos do R
+ Management Studio executar o T-SQL

## <a name="featurization-using-r"></a>Personalização usando o R

A linguagem R é bem conhecida por suas bibliotecas estatísticas variadas e avançadas, mas talvez você ainda precise criar transformações de dados personalizadas.

Primeiro, vamos fazer a maneira como os usuários do R estão acostumados: obter os dados para seu laptop e, em seguida, executar uma função personalizada do R, *ComputeDist*, que calcula a distância linear entre dois pontos especificados pelos valores de latitude e longitude.

1. Lembre-se de que o objeto de fonte de dados que você criou anteriormente obtém apenas as 1000 principais linhas. Então, vamos definir uma consulta que obtém todos os dados.

    ```R
    bigQuery <- "SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,  pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude FROM nyctaxi_sample";
    ```

2. Crie um novo objeto de fonte de dados usando a consulta.

    ```R
    featureDataSource <- RxSqlServerData(sqlQuery = bigQuery,colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric", dropoff_longitude = "numeric", dropoff_latitude = "numeric", passenger_count  = "numeric", trip_distance  = "numeric", trip_time_in_secs  = "numeric", direct_distance  = "numeric"), connectionString = connStr);
    ```

    - [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) pode usar uma consulta que consiste em uma consulta SELECT válida, fornecida como o argumento para o parâmetro SQLQuery ou o nome de um objeto Table, fornecido como o parâmetro _Table_ .
    
    - Se você quiser obter dados de exemplo de uma tabela, deverá usar o parâmetro SQLQuery, definir parâmetros de amostragem usando a cláusula TABLESAMPLE T-SQL e definir o argumento _armazenado em buffer_ como false.

3. Execute o código a seguir para criar a função personalizada do R. O ComputeDist usa dois pares de valores de latitude e longitude e calcula a distância linear entre eles, retornando a distância em milhas.

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
  
    + A primeira linha define um novo ambiente. No R, um ambiente pode ser usado para encapsular namespaces em pacotes e assim por diante. Você pode usar a função `search()` para exibir os ambientes no workspace. Para exibir os objetos em um ambiente específico, digite `ls(<envname>)`.
    + As linhas que começam com `$env.ComputeDist` contém o código que define a fórmula de Haversine, que calcula a *distância de grande círculo* entre dois pontos em uma esfera.

4. Depois de definir a função, você a aplica aos dados para criar uma nova coluna de recursos, *direct_distance*. Mas antes de executar a transformação, altere o contexto de computação para local.

    ```R
    rxSetComputeContext("local");
    ```

5. Chame a função [rxDataStep](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) para obter os dados de engenharia de recurso e aplique `env$ComputeDist` a função aos dados na memória.

    ```R
    start.time <- proc.time();
  
    changed_ds <- rxDataStep(inData = featureDataSource,
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

    + A função rxDataStep dá suporte a vários métodos para modificar dados no local. Para obter mais informações, consulte este artigo:  [Como transformar e subagrupar dados no Microsft R](https://docs.microsoft.com/r-server/r/how-to-revoscaler-data-transform)
    
    No entanto, vale a pena observar alguns pontos em relação a rxDataStep: 
    
    Em outras fontes de dados, você pode usar os argumentos *varsToKeep* e *varsToDrop*, mas eles não têm suporte para SQL Server fontes de dados. Portanto, neste exemplo, usamos o argumento transformações para especificar as colunas de passagem e as colunas transformadas. Além disso, ao executar em um contexto de computação SQL Server , o argumento Indata só pode pegar uma fonte de dados SQL Server.

    O código anterior também pode produzir uma mensagem de aviso quando executado em conjuntos de dados maiores. Quando o número de linhas vezes que o número de colunas que está sendo criado excede um valor definido (o padrão é 3 milhões), rxDataStep retorna um aviso e o número de linhas no quadro de dados retornado será truncado. Para remover o aviso, você pode modificar o argumento _maxRowsByCols_ na função rxDataStep. No entanto, se _maxRowsByCols_ for muito grande, você poderá enfrentar problemas ao carregar o quadro de dados na memória.

7. Opcionalmente, você pode chamar [rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo) para inspecionar o esquema da fonte de dados transformada.

    ```R
    rxGetVarInfo(data = changed_ds);
    ```

## <a name="featurization-using-transact-sql"></a>Personalização usando Transact-SQL

Neste exercício, saiba como realizar a mesma tarefa usando funções SQL em vez de funções personalizadas do R. 

Alterne para [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) ou outro editor de consultas para executar o script T-SQL.

1. Use uma função SQL, chamada *fnCalculateDistance*. A função já deve existir no banco de dados NYCTaxi_Sample. No Pesquisador de objetos, verifique se a função existe navegando neste caminho: Os bancos de dados > NYCTaxi_Sample > programabilidade > funções > funções com valor escalar > dbo. fnCalculateDistance.

    Se a função não existir, use SQL Server Management Studio para gerar a função no banco de dados NYCTaxi_Sample.

    ```sql
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)
    -- User-defined function calculates the direct distance between two geographical coordinates.
    RETURNS decimal(28, 10)
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

2. No Management Studio, em uma nova janela de consulta, execute a [!INCLUDE[tsql](../../includes/tsql-md.md)] seguinte instrução de qualquer aplicativo que [!INCLUDE[tsql](../../includes/tsql-md.md)] ofereça suporte para ver como a função funciona.

    ```sql
    USE nyctaxi_sample
    GO

    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) as direct_distance, pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude 
    FROM nyctaxi_sample
    ```
3. Para inserir valores diretamente em uma nova tabela (você precisa criá-lo primeiro), você pode adicionar uma cláusula **into** especificando o nome da tabela.

    ```sql
    USE nyctaxi_sample
    GO

    SELECT tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) as direct_distance, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude
    INTO NewFeatureTable
    FROM nyctaxi_sample
    ```

4. Você também pode chamar a função SQL do código R. Volte para Rgui e armazene a consulta personalização do SQL em uma variável do R.

    ```R
    featureEngineeringQuery = "SELECT tipped, fare_amount, passenger_count,
        trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
        pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
        FROM nyctaxi_sample
        tablesample (1 percent) repeatable (98052)"
    ```
  
    > [!TIP]
    > Esta consulta foi modificada para obter uma amostra menor de dados, a fim de tornar este tutorial mais rápido. Você pode remover a cláusula TABLESAMPLE se quiser obter todos os dados; no entanto, dependendo do seu ambiente, talvez não seja possível carregar o conjunto completo em R, resultando em um erro.
  
5. Use as linhas de código a seguir para chamar a função [!INCLUDE[tsql](../../includes/tsql-md.md)] no ambiente do R e aplique-a aos dados definidos em *featureEngineeringQuery*.
  
    ```R
    featureDataSource = RxSqlServerData(sqlQuery = featureEngineeringQuery,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
        dropoff_longitude = "numeric", dropoff_latitude = "numeric",
        passenger_count  = "numeric", trip_distance  = "numeric",
        trip_time_in_secs  = "numeric", direct_distance  = "numeric"),
      connectionString = connStr)
    ```
  
6.  Agora que o novo recurso foi criado, chame **rxGetVarsInfo** para criar um resumo dos dados na tabela de recursos.
  
    ```R
    rxGetVarInfo(data = featureDataSource)
    ```

    **Resultados**

    ```R
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
    > Em alguns casos, você pode receber um erro como este: *A permissão de execução foi negada no objeto ' fnCalculateDistance '* Nesse caso, verifique se o logon que você está usando tem permissões para executar scripts e criar objetos no banco de dados, não apenas na instância do.
    > Verifique o esquema do objeto, fnCalculateDistance. Se o objeto tiver sido criado pelo proprietário do banco de dados e seu logon pertencer à função db_datareader, você precisará conceder ao logon permissões explícitas para executar o script.

## <a name="comparing-r-functions-and-sql-functions"></a>Comparando funções do R e do SQL

Lembra-se desta parte do código usado para cronometrar o código R?

```R
start.time <- proc.time()
<your code here>
used.time <- proc.time() - start.time
print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""))
```

Você pode tentar usá-lo com o exemplo de função personalizada do SQL para ver quanto tempo a transformação de dados leva ao chamar uma função SQL. Além disso, tente alternar contextos de computação com rxSetComputeContext e comparar os intervalos.

Seus horários podem variar significativamente, dependendo da velocidade da sua rede e da configuração de hardware. Nas configurações que testamos, a [!INCLUDE[tsql](../../includes/tsql-md.md)] abordagem de função era mais rápida do que usar uma função de R personalizada. Portanto, usamos a [!INCLUDE[tsql](../../includes/tsql-md.md)] função para esses cálculos em etapas subsequentes.

> [!TIP]
> Com muita frequência, a engenharia [!INCLUDE[tsql](../../includes/tsql-md.md)] de recursos usando será mais rápida do que R. Por exemplo, o T-SQL inclui as funções rápidas de janela e classificação que podem ser aplicadas a cálculos comuns de ciência de dados, como médias de movimentação sem interrupção e *n*blocos. Escolha o método mais eficiente com base em seus dados e tarefas.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Criar um modelo de R e salvar no SQL](walkthrough-build-and-save-the-model.md)

