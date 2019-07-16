---
title: Criar recursos de dados usando funções de R e SQL Server - aprendizagem de máquina do SQL Server
description: Tutorial que mostra como criar recursos de dados usando funções do SQL Server para análise no banco de dados.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 5a17eb0c39e45080de83e39d002d8f6693131688
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961794"
---
# <a name="create-data-features-using-r-and-sql-server-walkthrough"></a>Criar recursos de dados usando R e SQL Server (passo a passo)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

A engenharia de dados é uma parte importante do aprendizado de máquina. Dados muitas vezes requerem transformação antes que você pode usá-lo para modelagem preditiva. Se os dados não tiverem os recursos necessários, você deverá criá-los com base em valores existentes.

Para esta tarefa de modelagem, em vez de usar os valores brutos de latitude e longitude dos locais de embarque e desembarque de passageiros, você gostaria de ter a distância em milhas entre os dois locais. Para criar esse recurso, você computa a distância linear direta entre dois pontos, usando o [fórmula de haversine](https://en.wikipedia.org/wiki/Haversine_formula).

Nesta etapa, você aprenderá dois métodos diferentes para criar um recurso de dados:

> [!div class="checklist"]
> * Usando uma função personalizada do R
> * Usando uma função personalizada do T-SQL em [!INCLUDE[tsql](../../includes/tsql-md.md)]

O objetivo é criar um novo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjunto de dados que inclui o novo recurso numérico, além das colunas originais *direct_distance*.

## <a name="prerequisites"></a>Pré-requisitos

Essa etapa pressupõe que uma sessão de R em andamento, com base nas etapas anteriores neste passo a passo. Ele usa as conexão cadeias de caracteres e dados de origem objetos criados nessas etapas. As ferramentas e os pacotes a seguir são usados para executar o script.

+ Rgui.exe para executar comandos de R
+ Management Studio para executar o T-SQL

## <a name="featurization-using-r"></a>Personalização usando R

A linguagem R é bem conhecida por suas bibliotecas estatísticas variadas e avançadas, mas talvez você ainda precise criar transformações de dados personalizadas.

Primeiro, vamos fazer isso de forma R, os usuários estão acostumados a: obter os dados para o laptop e, em seguida, executar uma função do R personalizada *ComputeDist*, que calcula a distância linear entre dois pontos especificados por valores de latitude e longitude.

1. Lembre-se de que o objeto de fonte de dados que você criou anteriormente obtém somente as primeiras 1000 linhas. Então, vamos definir uma consulta que obtém todos os dados.

    ```R
    bigQuery <- "SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,  pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude FROM nyctaxi_sample";
    ```

2. Crie um novo objeto de fonte de dados usando a consulta.

    ```R
    featureDataSource <- RxSqlServerData(sqlQuery = bigQuery,colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric", dropoff_longitude = "numeric", dropoff_latitude = "numeric", passenger_count  = "numeric", trip_distance  = "numeric", trip_time_in_secs  = "numeric", direct_distance  = "numeric"), connectionString = connStr);
    ```

    - [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) pode levar a uma consulta consiste em uma consulta SELECT válida, fornecida como o argumento para o _sqlQuery_ parâmetro ou o nome de um objeto de tabela, fornecido como o _tabela_ parâmetro.
    
    - Se você quiser dados de exemplo de uma tabela, você deve usar o _sqlQuery_ parâmetro, defina os parâmetros de amostragem usando a cláusula TABLESAMPLE T-SQL e defina as _rowBuffering_ argumento como FALSE.

3. Execute o seguinte código para criar a função personalizada do R. ComputeDist usa dois pares de valores de latitude e longitude e calcula a distância linear entre elas, retornando a distância em milhas.

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

4. Após a definição de função, você aplicá-lo aos dados para criar uma nova coluna de recurso *direct_distance*. mas, antes de executar a transformação, altere o contexto de computação para o local.

    ```R
    rxSetComputeContext("local");
    ```

5. Chame o [rxDataStep](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) função para obter o recurso de dados de engenharia e aplicar o `env$ComputeDist` função aos dados na memória.

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

    + A função rxDataStep dá suporte a vários métodos para modificar dados in-loco. Para obter mais informações, consulte este artigo:  [Como os dados em R Microsft transformação e o subconjunto](https://docs.microsoft.com/r-server/r/how-to-revoscaler-data-transform)
    
    No entanto, alguns pontos que vale a pena observar sobre rxDataStep: 
    
    Em outras fontes de dados, você pode usar os argumentos *varsToKeep* e *varsToDrop*, mas eles não têm suporte para fontes de dados do SQL Server. Portanto, neste exemplo, usamos o _transforma_ argumento para especificar as colunas de passagem e as colunas transformadas. Além disso, quando em execução em um SQL Server contexto de computação, o _inData_ argumento só pode usar uma fonte de dados do SQL Server.

    O código anterior também pode produzir uma mensagem de aviso quando executado em conjuntos de dados maiores. Quando o número de linhas vezes o número de colunas que está sendo criado excede um valor definido (o padrão é 3,000,000), rxDataStep retorna um aviso e o número de linhas no quadro de dados retornado será truncado. Para remover o aviso, você pode modificar os _maxRowsByCols_ argumento na função rxDataStep. No entanto, se _maxRowsByCols_ é muito grande, você poderá ter problemas ao carregar o quadro de dados na memória.

7. Opcionalmente, você pode chamar [rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo) para inspecionar o esquema da fonte de dados transformados.

    ```R
    rxGetVarInfo(data = changed_ds);
    ```

## <a name="featurization-using-transact-sql"></a>Personalização usando Transact-SQL

Neste exercício, saiba como realizar a mesma tarefa usando funções SQL em vez de funções de R personalizadas. 

Alterne para [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) ou outro editor de consultas para executar o script T-SQL.

1. Usar uma função SQL, chamada *fnCalculateDistance*. A função já deve existir no banco de dados NYCTaxi_Sample. No Pesquisador de objetos, verifique se que a função existe navegando neste caminho: Bancos de dados > NYCTaxi_Sample > programabilidade > Funções > funções de valor escalar > dbo.fnCalculateDistance.

    Se a função não existir, use o SQL Server Management Studio para gerar a função no banco de dados NYCTaxi_Sample.

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

2. No Management Studio, em uma nova janela de consulta, execute o seguinte [!INCLUDE[tsql](../../includes/tsql-md.md)] declaração de qualquer aplicativo que dá suporte a [!INCLUDE[tsql](../../includes/tsql-md.md)] para ver como funciona a função.

    ```sql
    USE nyctaxi_sample
    GO

    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) as direct_distance, pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude 
    FROM nyctaxi_sample
    ```
3. Para inserir valores diretamente em uma nova tabela (você precisa criá-lo primeiro), você pode adicionar um **INTO** cláusula especificando o nome da tabela.

    ```sql
    USE nyctaxi_sample
    GO

    SELECT tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) as direct_distance, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude
    INTO NewFeatureTable
    FROM nyctaxi_sample
    ```

4. Você também pode chamar a função SQL do código R. Volte para o Rgui e armazene a consulta de personalização SQL em uma variável do R.

    ```R
    featureEngineeringQuery = "SELECT tipped, fare_amount, passenger_count,
        trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
        pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
        FROM nyctaxi_sample
        tablesample (1 percent) repeatable (98052)"
    ```
  
    > [!TIP]
    > Essa consulta foi modificada para obter uma amostra menor de dados, para agilizar este passo a passo. Você pode remover a cláusula TABLESAMPLE se você quiser obter todos os dados; No entanto, dependendo do seu ambiente, pode não ser possível carregar o conjunto de dados completo em R, resultando em um erro.
  
5. Use as linhas de código a seguir para chamar a função [!INCLUDE[tsql](../../includes/tsql-md.md)] no ambiente do R e aplique-a aos dados definidos em *featureEngineeringQuery*.
  
    ```R
    featureDataSource = RxSqlServerData(sqlQuery = featureEngineeringQuery,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
        dropoff_longitude = "numeric", dropoff_latitude = "numeric",
        passenger_count  = "numeric", trip_distance  = "numeric",
        trip_time_in_secs  = "numeric", direct_distance  = "numeric"),
      connectionString = connStr)
    ```
  
6.  Agora que o novo recurso for criado, chame **rxGetVarsInfo** para criar um resumo dos dados na tabela de recursos.
  
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
    > Em alguns casos, você poderá receber um erro como este: *A permissão EXECUTE foi negada no objeto 'fnCalculateDistance'* nesse caso, certifique-se de que o logon que você está usando tenha permissões para executar scripts e criar objetos no banco de dados, não apenas na instância.
    > Verifique o esquema para o objeto, fnCalculateDistance. Se o objeto foi criado pelo proprietário do banco de dados e seu logon pertence a função db_datareader, você precisa conceder permissões explícitas para executar o script de logon.

## <a name="comparing-r-functions-and-sql-functions"></a>Comparando funções de R e SQL

Lembre-se nessa parte do código usado para o código R de tempo?

```R
start.time <- proc.time()
<your code here>
used.time <- proc.time() - start.time
print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""))
```

Você pode tentar usar com o exemplo de função personalizada do SQL para ver quanto tempo leva para a transformação de dados ao chamar uma função do SQL. Além disso, tente alternar contextos de computação com rxSetComputeContext e compare os intervalos.

Os horários podem variar significativamente, dependendo da velocidade da sua rede e sua configuração de hardware. Nas configurações testados, a [!INCLUDE[tsql](../../includes/tsql-md.md)] abordagem da função foi mais rápida do que usando uma função personalizada do R. Portanto, usamos o [!INCLUDE[tsql](../../includes/tsql-md.md)] função para esses cálculos em etapas subsequentes.

> [!TIP]
> Com muita frequência, engenharia de recursos com [!INCLUDE[tsql](../../includes/tsql-md.md)] será mais rápido do que R. Por exemplo, o T-SQL inclui janelas rápida e as funções de classificação podem ser aplicadas a cálculos comuns de ciência de dados tais como médias móveis e *n*-lado a lado. Escolha o método mais eficiente com base em seus dados e tarefas.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Criar um modelo do R e salvar para SQL](walkthrough-build-and-save-the-model.md)

