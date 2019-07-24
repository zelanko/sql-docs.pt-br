---
title: Exibir e resumir dados de SQL Server usando as funções do R
description: Tutorial mostrando como Visualizar e gerar resumos estatísticos usando funções do R para análise no banco de dados no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 52ba1a8f036037ade42c8483b1735c84cc72867e
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345785"
---
# <a name="view-and-summarize-sql-server-data-using-r-walkthrough"></a>Exibir e resumir dados de SQL Server usando o R (Walkthrough)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Esta lição apresenta as funções no pacote **RevoScaleR** e percorre as seguintes tarefas:

> [!div class="checklist"]
> * Conecte-se ao SQL Server
> * Definir uma consulta que contenha os dados de que você precisa, ou especificar uma tabela ou modo de exibição
> * Definir um ou mais contextos de computação para usar ao executar o código R
> * Opcionalmente, defina as transformações que são aplicadas à fonte de dados enquanto ela está sendo lida da origem

## <a name="define-a-sql-server-compute-context"></a>Definir um contexto de computação SQL Server

Execute as seguintes instruções do R em um ambiente de R na estação de trabalho cliente. Esta seção pressupõe uma [estação de trabalho de ciência de dados com Microsoft R Client](../r/set-up-a-data-science-client.md), pois inclui todos os pacotes RevoScaleR, bem como um conjunto básico e leve de ferramentas de R. Por exemplo, você pode usar Rgui. exe para executar o script R nesta seção.

1. Se o pacote **RevoScaleR** ainda não estiver carregado, execute esta linha de código R:

    ```R
    library("RevoScaleR")
    ```

     As aspas são opcionais, nesse caso, embora recomendado.
     
     Se você receber um erro, verifique se o ambiente de desenvolvimento R está usando uma biblioteca que inclui o pacote RevoScaleR. Use um comando como `.libPaths()` para exibir o caminho da biblioteca atual.

2. Crie a cadeia de conexão para SQL Server e salve-a em uma variável de R, *connStr*.

   Você deve alterar o espaço reservado "your_server_name" para um nome de instância de SQL Server válido. Para o nome do servidor, você pode usar apenas o nome da instância ou pode precisar qualificar totalmente o nome, dependendo de sua rede.
    
   Para SQL Server autenticação, a sintaxe de conexão é a seguinte:

    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=nyctaxi_sample;Uid=your-sql-login;Pwd=your-login-password"
    ```

    Para a autenticação do Windows, a sintaxe é um pouco diferente:
    
    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=nyctaxi_sample;Trusted_Connection=True"
    ```

    Em geral, recomendamos que você use a autenticação do Windows sempre que possível, para evitar salvar senhas em seu código R.

3. Defina as variáveis a serem usadas na criação de um novo *contexto de computação*. Depois de criar o objeto de contexto de computação, você pode usá-lo para executar o código R na instância de SQL Server.

    ```R
    sqlShareDir <- paste("C:\\AllShare\\",Sys.getenv("USERNAME"),sep="")
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```

    - O R usa um diretório temporário ao serializar objetos de R de um lado para outro entre a estação de trabalho e o computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Você pode especificar o diretório local que é usado como *sqlShareDir*, ou aceitar o padrão.
  
    - Use *sqlwait* para indicar se deseja que o R aguarde os resultados do servidor.  Para uma discussão de espera em comparação com trabalhos não esperados, consulte [computação paralela e distribuída com o RevoScaleR no Microsoft R](https://docs.microsoft.com/r-server/r/how-to-revoscaler-distributed-computing).
  
    - Use o argumento *sqlConsoleOutput* para indicar que você não deseja ver a saída do console do R.

4. Você chama o construtor [RxInSqlServer](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinsqlserver) para criar o objeto de contexto de computação com as variáveis e cadeias de conexão já definidas e salva o novo objeto na variável de R *sqlcc*.
  
    ```R
    sqlcc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```

5. Por padrão, o contexto de computação é local, portanto, você precisa definir explicitamente o contexto de computação *ativo* .

    ```R
    rxSetComputeContext(sqlcc)
    ```

    + [rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) retorna o contexto de computação anteriormente ativo de forma invisível para que você possa usá-lo
    + [rxGetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) retorna o contexto de computação ativo
    
    Observe que a configuração de um contexto de computação afeta apenas as operações que usam funções no pacote **RevoScaleR** ; o contexto de computação não afeta a maneira como as operações de software livre do R são executadas.

## <a name="create-a-data-source-using-rxsqlserver"></a>Criar uma fonte de dados usando RxSqlServer

Ao usar as bibliotecas do Microsoft R como RevoScaleR e MicrosoftML, uma *fonte de dados* é um objeto que você cria usando funções RevoScaleR. O objeto de fonte de dados especifica um conjunto de dados que você deseja usar para uma tarefa, como treinamento de modelo ou extração de recursos. Você pode obter dados de uma variedade de fontes, incluindo SQL Server. Para obter a lista de fontes com suporte no momento, consulte [RxDataSource](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource).

Anteriormente, você definiu uma cadeia de conexão e salvou essas informações em uma variável do R. Você pode usar novamente essas informações de conexão para especificar os dados que deseja obter.

1. Salve uma consulta SQL como uma variável de cadeia de caracteres. A consulta define os dados para treinar o modelo.

    ```R
    sampleDataQuery <- "SELECT TOP 1000 tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime, pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude FROM nyctaxi_sample"
    ```

    Usamos uma cláusula TOP aqui para fazer com que as coisas sejam executadas mais rapidamente, mas as linhas reais retornadas pela consulta podem variar dependendo da ordem. Portanto, os resultados de resumo também podem ser diferentes daqueles listados abaixo. Sinta-se à vontade para remover a cláusula TOP.

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
    
    + O argumento  *colClasses* especifica os tipos de coluna a serem usados ao mover os dados entre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o R. Isso é importante porque o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa tipos de dados diferentes do R e mais tipos de dados. Para obter mais informações, consulte [bibliotecas e tipos de dados do R](../r/r-libraries-and-data-types.md).
  
    + O argumento *rowsPerRead* é importante para gerenciar o uso de memória e cálculos eficientes.  A maioria das funções analíticas avançadas no[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] processa dados em partes e acumula resultados intermediários, retornando os cálculos finais após a leitura de todos os dados.  Ao adicionar o parâmetro *rowsPerRead* , você pode controlar quantas linhas de dados são lidas em cada parte para processamento.  Se o valor desse parâmetro for muito grande, o acesso aos dados poderá ser lento porque você não tem memória suficiente para processar com eficiência um bloco de dados tão grande.  Em alguns sistemas, definir *rowsPerRead* como um valor excessivamente pequeno também pode fornecer um desempenho mais lento.

3. Neste ponto, você criou o objeto indataname, mas ele não contém nenhum dado. Os dados não são extraídos da consulta SQL para o ambiente local até que você execute uma função como [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) ou [rxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary).

    No entanto, agora que você definiu os objetos de dados, você pode usá-lo como o argumento para outras funções.

## <a name="use-the-sql-server-data-in-r-summaries"></a>Usar os dados de SQL Server em resumos de R

Nesta seção, você experimentará várias das funções fornecidas no [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] que dão suporte a contextos de computação remota. Ao aplicar as funções do R à fonte de dados, você pode explorar, resumir e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fazer o gráfico dos dados.

1. Chame a função [rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo) para obter uma lista das variáveis na fonte de dados e seus tipos de dados.

    **rxGetVarInfo** é uma função útil; Você pode chamá-lo em qualquer quadro de dados ou em um conjunto de dados em um objeto de dados remoto, para obter informações como os valores máximo e mínimo, o tipo de dados e o número de níveis em colunas de fator.
    
    Considere a possibilidade de executar essa função após qualquer espécie de entrada de dados, transformação de recursos ou engenharia de recursos. Ao fazer isso, você pode garantir que todos os recursos que você deseja usar em seu modelo sejam do tipo de dados esperado e evitar erros.
  
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

2. Agora, chame a função RevoScaleR [rxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary) para obter estatísticas mais detalhadas sobre variáveis individuais.

    o rxSummary é baseado na função `summary` R, mas tem alguns recursos e vantagens adicionais. o rxSummary funciona em vários contextos de computação e dá suporte a agrupamentos.  Você também pode usar rxSummary para transformar valores ou resumir com base em níveis de fator.
    
    Neste exemplo, você resume o valor da tarifa com base no número de passageiros.
    
    ```R
    start.time <- proc.time()
    rxSummary(~fare_amount:F(passenger_count,1,6), data = inDataSource)
    used.time <- proc.time() - start.time
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds,
      Elapsed Time=", round(used.time[3],2),
      " seconds to summarize the inDataSource.", sep=""))
    ```
    + O primeiro argumento para rxSummary especifica a fórmula ou o termo pelo qual resumir. Aqui, a `F()` função é usada para converter os valores na _contagem\_de passageiros_ em fatores antes de resumir. Você também precisará especificar o valor mínimo (1) e o valor máximo (6) para a variável fator de _passageiro\__ .
    + Se você não especificar as estatísticas para saída, por padrão, as saídas rxSummary significam, DESVPAD, min, Max e o número de observações válidas e ausentes.
    + Este exemplo também inclui um código para acompanhar o tempo durante o qual a função é iniciada e concluída, para que você possa comparar o desempenho.
  
    **Resultados**

    Se a função rxSummary for executada com êxito, você deverá ver os resultados como esses, seguidos por uma lista de estatísticas por categoria. 

    ```R
    rxSummary(formula = ~fare_amount:F(passenger_count, 1,6), data = inDataSource)
    Data: inDataSource (RxSqlServerData Data Source)
    Number of valid observations: 1000
    ```

### <a name="bonus-exercise-on-big-data"></a>Exercício de bônus no Big Data

Tente definir uma nova cadeia de caracteres de consulta com todas as linhas. Recomendamos que você configure um novo objeto de fonte de dados para este experimento. Você também pode tentar alterar o parâmetro *rowsToRead* para ver como ele afeta a taxa de transferência.

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
> Enquanto isso estiver em execução, você poderá usar uma ferramenta como o [Process Explorer](https://technet.microsoft.com/sysinternals/processexplorer.aspx) ou o SQL Profiler para ver como a conexão é feita e o código R é executado usando SQL Server Services.
> 
> Outra opção é monitorar os trabalhos do R em execução no SQL Server usando esses [relatórios personalizados](../r/monitor-r-services-using-custom-reports-in-management-studio.md).

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Criar grafos e gráficos usando o R](walkthrough-create-graphs-and-plots-using-r.md)