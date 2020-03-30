---
title: 'Tutorial do R: Explorar dados'
description: Tutorial mostrando como visualizar e gerar resumos estatísticos usando funções do R para análise no banco de dados no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f279be39a9edc91dd9d8cd6b72183988a607ce31
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "73723750"
---
# <a name="view-and-summarize-sql-server-data-using-r-walkthrough"></a>Exibir e resumir dados do SQL Server usando o R (passo a passo)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Esta lição apresenta as funções no pacote **RevoScaleR** e conduz você pelas seguintes tarefas:

> [!div class="checklist"]
> * Conecte-se ao SQL Server
> * Definir uma consulta que contenha os dados de que você precisa, ou especificar uma tabela ou modo de exibição
> * Definir um ou mais contextos de computação para usar ao executar o código R
> * Opcionalmente, defina transformações que são aplicadas à fonte de dados enquanto eles estão sendo lidos da fonte

## <a name="define-a-sql-server-compute-context"></a>Definir um contexto de computação do SQL Server

Execute as seguintes instruções do R em um ambiente do R na estação de trabalho cliente. Esta seção pressupõe uma [estação de trabalho de ciência de dados com Microsoft R Client](../r/set-up-a-data-science-client.md), pois ela inclui todos os pacotes RevoScaleR, bem como um conjunto básico e leve de ferramentas do R. Por exemplo, você pode usar Rgui.exe para executar o script do R nesta seção.

1. Se o pacote **RevoScaleR** ainda não estiver carregado, execute esta linha de código R:

    ```R
    library("RevoScaleR")
    ```

     Neste caso, as aspas são opcionais, embora recomendadas.
     
     Se você receber um erro, verifique se o ambiente de desenvolvimento do R está usando uma biblioteca que inclui o pacote RevoScaleR. Use um comando como `.libPaths()` para exibir o caminho atual da biblioteca.

2. Crie a cadeia de conexão para o SQL Server e salve-a em uma variável do R, *connStr*.

   Você deve alterar o espaço reservado "your_server_name" para um nome de instância do SQL Server válido. Para o nome do servidor, talvez você possa usar apenas o nome da instância ou precise qualificar totalmente o nome, dependendo de sua rede.
    
   Para autenticação do SQL Server, a sintaxe de conexão é a seguinte:

    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=nyctaxi_sample;Uid=your-sql-login;Pwd=your-login-password"
    ```

    Para a autenticação do Windows, a sintaxe é um pouco diferente:
    
    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=nyctaxi_sample;Trusted_Connection=True"
    ```

    Em geral, é recomendável usar autenticação do Windows sempre que possível para evitar salvar senhas no seu código R.

3. Defina as variáveis a serem usadas em um novo *contexto de computação*. Depois de criar o objeto do contexto de computação, você pode usá-lo para executar o código R na instância do SQL Server.

    ```R
    sqlShareDir <- paste("C:\\AllShare\\",Sys.getenv("USERNAME"),sep="")
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```

    - O R usa um diretório temporário ao serializar objetos de R de um lado para outro entre a estação de trabalho e o computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Você pode especificar o diretório local que é usado como *sqlShareDir*, ou aceitar o padrão.
  
    - Use *sqlWait* para indicar se deseja que o R espere resultados do servidor.  Para uma discussão de trabalhos com espera versus sem espera, confira [Computação distribuída e paralela com RevoScaleR no Microsoft R](https://docs.microsoft.com/r-server/r/how-to-revoscaler-distributed-computing).
  
    - Use o argumento *sqlConsoleOutput* para indicar que você não deseja ver a saída do console de R.

4. Chame o construtor [RxInSqlServer](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinsqlserver) para criar o objeto de contexto de computação com as variáveis e cadeias de conexão já definidas e salve o novo objeto na variável *sqlcc* do R.
  
    ```R
    sqlcc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```

5. Por padrão, o contexto de computação é local, portanto, você precisa definir explicitamente o *contexto de computação ativo*.

    ```R
    rxSetComputeContext(sqlcc)
    ```

    + [rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) retorna o contexto de computação anteriormente ativo de forma invisível para que você possa usá-lo
    + [rxGetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) retorna o contexto de computação ativo
    
    Observe que definir esse contexto de computação só afeta as operações que usam funções no pacote **RevoScaleR**; o contexto de computação não afeta a maneira como as operações de software livre do R são executadas.

## <a name="create-a-data-source-using-rxsqlserver"></a>Criar uma fonte de dados usando o RxSqlServer

Ao usar as bibliotecas do Microsoft R como RevoScaleR e MicrosoftML, uma *fonte de dados* é um objeto que você cria usando funções RevoScaleR. O objeto de fonte de dados especifica um conjunto de dados que você deseja usar para uma tarefa, como treinamento de modelo ou extração de recursos. Você pode obter dados de diversas fontes, incluindo o SQL Server. Para obter a lista de fontes com suporte no momento, confira [RxDataSource](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource).

Antes, você definiu uma cadeia de conexão e salvou essas informações em uma variável do R. Você pode usar novamente essas informações de conexão para especificar os dados que deseja obter.

1. Salve uma consulta do SQL como uma variável de cadeia de caracteres. A consulta define os dados para treinar o modelo.

    ```R
    sampleDataQuery <- "SELECT TOP 1000 tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime, pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude FROM nyctaxi_sample"
    ```

    Usamos uma cláusula TOP aqui para agilizar a execução, mas as linhas reais retornadas pela consulta podem variar conforme a ordem. Portanto, os resultados de resumo também podem ser diferentes daqueles listados abaixo. Você pode remover a cláusula TOP se quiser.

2. Passe a definição de consulta como um argumento para a função [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata).

    ```R
    inDataSource <- RxSqlServerData(
      sqlQuery = sampleDataQuery,
      connectionString = connStr,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
      dropoff_longitude = "numeric", dropoff_latitude = "numeric"),
      rowsPerRead=500
      )
    ```
    
    + O argumento  *colClasses* especifica os tipos de coluna a serem usados ao mover os dados entre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o R. Isso é importante porque o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa tipos de dados diferentes do R e mais tipos de dados. Para obter mais informações, confira [Tipos de dados e bibliotecas do R](../r/r-libraries-and-data-types.md).
  
    + O argumento *rowsPerRead* é importante para gerenciar o uso de memória e cálculos eficientes.  A maioria das funções analíticas avançadas no[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] processa dados em partes e acumula resultados intermediários, retornando os cálculos finais após a leitura de todos os dados.  Ao adicionar o parâmetro *rowsPerRead*, você pode controlar a quantidade de linhas de dados lidas em cada bloco de processamento.  Caso o valor desse parâmetro seja muito grande, o acesso a dados pode ser lento, pois você não tem memória suficiente para processar com eficiência um bloco de dados grande.  Em alguns sistemas, definir *rowsPerRead* para um valor excessivamente pequeno também pode causar um desempenho mais lento.

3. Neste ponto, você criou o objeto *inDataSource*, mas ele não contém nenhum dado. Os dados não são capturados da consulta SQL para o ambiente local até você executar uma função como [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) ou [rxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary).

    No entanto, agora que você definiu os objetos de dados, pode usá-los como o argumento para outras funções.

## <a name="use-the-sql-server-data-in-r-summaries"></a>Usar os dados do SQL Server em resumos do R

Nesta seção, você testará várias das funções fornecidas no [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] que dão suporte a contextos de computação remota. Ao aplicar funções do R à fonte de dados, você pode explorar, resumir e traçar um gráfico dos dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

1. Chame a função [rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo) para obter uma lista das variáveis na fonte de dados e seus tipos de dados.

    **rxGetVarInfo** é uma função prática. Você pode chamá-la em qualquer quadro de dados ou em um conjunto de dados em um objeto de dados remoto para obter informações como os valores mínimo e máximo, o tipo de dados e o número de níveis em colunas de fator.
    
    Considere a possibilidade de executar essa função após qualquer espécie de entrada de dados, transformação de recursos ou engenharia de recursos. Ao fazer isso, você pode garantir que todos os recursos que você deseja usar no modelo são do tipo de dados esperado e evitar erros.
  
    ```R
    rxGetVarInfo(data = inDataSource)
    ```

    **Resultados**
    
    ```R
    Var 1: tipped, Type: integer
    Var 2: fare_amount, Type: numeric
    Var 3: passenger_count, Type: integer
    Var 4: trip_time_in_secs, Type: numeric, Storage: int64
    Var 5: trip_distance, Type: numeric
    Var 6: pickup_datetime, Type: character
    Var 7: dropoff_datetime, Type: character
    Var 8: pickup_longitude, Type: numeric
    Var 9: pickup_latitude, Type: numeric
    Var 10: dropoff_longitude, Type: numeric
    ```

2. Agora, chame a função [rxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary) do RevoScaleR para obter estatísticas mais detalhadas sobre variáveis individuais.

    O rxSummary é baseado na função `summary` do R, mas tem alguns recursos e vantagens adicionais. O rxSummary funciona em vários contextos de computação e dá suporte a agrupamentos.  Você também pode usar o rxSummary para transformar valores ou resumir com base em níveis de fator.
    
    Neste exemplo, você resume o valor da tarifa com base no número de passageiros.
    
    ```R
    start.time <- proc.time()
    rxSummary(~fare_amount:F(passenger_count,1,6), data = inDataSource)
    used.time <- proc.time() - start.time
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds,
      Elapsed Time=", round(used.time[3],2),
      " seconds to summarize the inDataSource.", sep=""))
    ```
    + O primeiro argumento para rxSummary especifica a fórmula ou o termo no qual o resumo se baseará. Neste exemplo, a função `F()` é usada para converter os valores de _passenger\_count_ em fatores antes do resumo. Você também precisa especificar o valor mínimo (1) e o valor máximo (6) para a variável de fator _passenger\_count_.
    + Se você não especificar as estatísticas a serem geradas, por padrão, rxSummary vai gerar Mean, StDev, Min, Max e o número de observações válidas e ausentes.
    + Este exemplo também inclui um código para acompanhar o tempo durante o qual a função é iniciada e concluída, para que você possa comparar o desempenho.
  
    **Resultados**

    Se a função rxSummary for executada com êxito, você deverá ver os resultados como estes, seguidos por uma lista de estatísticas por categoria. 

    ```R
    rxSummary(formula = ~fare_amount:F(passenger_count, 1,6), data = inDataSource)
    Data: inDataSource (RxSqlServerData Data Source)
    Number of valid observations: 1000
    ```

### <a name="bonus-exercise-on-big-data"></a>Exercício de bônus sobre Big Data

Tente definir uma nova cadeia de consulta com todas as linhas. Recomendamos configurar um novo objeto de fonte de dados para este experimento. Você também pode tentar alterar o parâmetro *rowsToRead* para ver como ele afeta a taxa de transferência.

```R
bigDataQuery  <- "SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime, pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude FROM nyctaxi_sample"

bigDataSource <- RxSqlServerData(
      sqlQuery = bigDataQuery,
      connectionString = connStr,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
      dropoff_longitude = "numeric", dropoff_latitude = "numeric"),
      rowsPerRead=500
      )

start.time <- proc.time()
rxSummary(~fare_amount:F(passenger_count,1,6), data = bigDataSource)
used.time <- proc.time() - start.time
print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds,
  Elapsed Time=", round(used.time[3],2),
  " seconds to summarize the inDataSource.", sep=""))
```

> [!TIP]
> Enquanto isso estiver em execução, você poderá usar uma ferramenta como o [Explorador de Processos](https://technet.microsoft.com/sysinternals/processexplorer.aspx) ou o SQL Profiler para ver como a conexão é feita e o código R é executado usando o SQL Server Services.
> 
> Outra opção é monitorar os trabalhos do R em execução no SQL Server usando esses [relatórios personalizados](../r/monitor-r-services-using-custom-reports-in-management-studio.md).

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Criar grafos e gráficos usando o R](walkthrough-create-graphs-and-plots-using-r.md)