---
title: Exibir e resumir dados usando o R (passo a passo) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/02/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 1d6c225b3ec6b2a7a80dea155b564b94ecab60fb
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51032883"
---
# <a name="view-and-summarize-data-using-r"></a>Exibir e resumir dados usando o R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Agora vamos trabalhar com os mesmos dados usando o código R. Nesta lição, você aprenderá a usar as funções do **RevoScaleR** pacote.

Um script do R que inclui todo o código necessário para criar o objeto de dados, gerar resumos e criar modelos é fornecido neste passo a passo. O arquivo de script do R, **RSQL_RWalkthrough.R**, podem ser encontrado no local em que você instalou os arquivos de script.

+ Se estiver familiarizado com R, você poderá executar o script de uma só vez.
+ Para quem está aprendendo a usar o RevoScaleR, este tutorial percorre o script linha por linha.
+ Para executar linhas individuais do script, você pode realçar uma linha ou linhas no arquivo e pressionar Ctrl + ENTER.

> [!TIP]
> Salve o workspace do R caso você deseje concluir o restante do passo a passo mais tarde.  Dessa forma, os objetos de dados e outras variáveis estão prontos para reutilização.

## <a name="define-a-sql-server-compute-context"></a>Definir um contexto de computação do SQL Server

Microsoft R torna mais fácil obter dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para usar em seu código R. O processo é o seguinte:
  
- Criar uma conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]
- Definir uma consulta que contenha os dados de que você precisa, ou especificar uma tabela ou modo de exibição
- Definir um ou mais contextos de computação para usar ao executar o código R
- Opcionalmente, definir as transformações que são aplicadas à fonte de dados enquanto ele está sendo lidos da origem

As etapas a seguir fazem parte do código R e devem ser executados em um ambiente de R. Nós usamos o Microsoft R Client, pois ele inclui todos os pacotes RevoScaleR, bem como um conjunto de ferramentas do R básico, leve.

1. Se o **RevoScaleR** pacote não estiver carregado, execute esta linha de código R:

    ```R
    library("RevoScaleR")
    ```

     As aspas são opcionais, nesse caso, embora seja recomendado.
     
     Se você receber um erro, certifique-se de que seu ambiente de desenvolvimento do R está usando uma biblioteca que inclui o pacote RevoScaleR. Use um comando como `.libPaths()` para exibir o caminho da biblioteca atual.

2. Criar a cadeia de caracteres de conexão para o SQL Server e salvá-la em uma variável do R _connStr_.
    
    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=nyctaxi_sample;Uid=your-sql-login;Pwd=your-login-password"
    ```

    Para o nome do servidor, você poderá usar apenas o nome da instância ou, talvez você precise qualificar totalmente o nome, dependendo da sua rede.

    Para a autenticação do Windows, a sintaxe é um pouco diferente:
    
    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=nyctaxi_sample;Trusted_Connection=True"
    ```

    O script R disponível para download usa somente logons do SQL. Em geral, é recomendável usar a autenticação do Windows sempre que possível, para evitar salvar senhas no seu código R. No entanto, para garantir que o código neste tutorial coincide com o código baixado do Github, vamos usar um logon do SQL para o restante do passo a passo.

3. Definir variáveis a serem usadas ao criar um novo *contexto de computação*. Depois de criar o objeto de contexto de computação, você pode usá-lo para executar código R na instância do SQL Server.

    ```R
    sqlShareDir <- paste("C:\\AllShare\\",Sys.getenv("USERNAME"),sep="")
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```

    - O R usa um diretório temporário ao serializar objetos de R de um lado para outro entre a estação de trabalho e o computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Você pode especificar o diretório local que é usado como *sqlShareDir*, ou aceitar o padrão.
  
    - Use *sqlWait* para indicar se você deseja que o R espere por resultados do servidor.  Para uma discussão sobre aguardar versus não aguardar trabalhos, consulte [distribuído e computação paralela com ScaleR no Microsoft R](https://docs.microsoft.com/r-server/r/how-to-revoscaler-distributed-computing).
  
    - Use o argumento *sqlConsoleOutput* para indicar que você não deseja ver a saída do console do R.


4. Você chama o [RxInSqlServer](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinsqlserver) construtor para criar o objeto de contexto de computação com variáveis e cadeias de caracteres de conexão já definidas e salve o novo objeto na variável do R *sqlcc*.
  
    ```R
    sqlcc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```

5. Por padrão, o contexto de computação é local, portanto, você precisará definir explicitamente o *active* contexto de computação.

    ```R
    rxSetComputeContext(sqlcc)
    ```

    + O`rxSetComputeContext` retorna o contexto de computação anteriormente ativo de forma invisível para que você possa usá-lo
    + O`rxGetComputeContext` retorna o contexto de computação ativo
    
    Observe que definir esse contexto de computação só afeta as operações que usam funções no pacote **RevoScaleR** ; o contexto de computação não afeta a maneira como as operações de software livre do R são executadas.

## <a name="create-a-data-source-using-rxsqlserver"></a>Criar uma fonte de dados usando RxSqlServer

No Microsoft R, uma *fonte de dados* é um objeto que você cria usando funções de RevoScaleR. O objeto de fonte de dados especifica um conjunto de dados que você deseja usar para uma tarefa, como extração de treinamento ou um recurso de modelo. Você pode obter dados de uma variedade de fontes; Para obter a lista de fontes com suporte no momento, consulte [RxDataSource](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource).

Anteriormente você definiu uma cadeia de caracteres de conexão e salvou essas informações em uma variável do R. Novamente, você pode usar essas informações de conexão para especificar os dados que você deseja obter.

1. Salve uma consulta SQL como uma variável de cadeia de caracteres. A consulta define os dados para treinar o modelo.

    ```R
    sampleDataQuery <- "SELECT TOP 1000 tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime, pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude FROM nyctaxi_sample"
    ```

    Usamos uma cláusula TOP aqui para tornar as coisas executado mais rapidamente, mas as linhas reais retornadas pela consulta podem variar dependendo da ordem. Portanto, o resumo de resultados também pode ser diferente daqueles listados abaixo. Fique à vontade remover a cláusula TOP.

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
    
    + O argumento  *colClasses* especifica os tipos de coluna a serem usados ao mover os dados entre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o R. Isso é importante porque o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa tipos de dados diferentes do R e mais tipos de dados. Para obter mais informações, consulte [tipos de dados e bibliotecas do R](../r/r-libraries-and-data-types.md).
  
    + O argumento *rowsPerRead* é importante para gerenciar o uso de memória e cálculos eficientes.  A maioria das funções analíticas avançadas no[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] processa dados em partes e acumula resultados intermediários, retornando os cálculos finais após a leitura de todos os dados.  Adicionando o *rowsPerRead* parâmetro, você pode controlar quantas linhas de dados são lidas em cada bloco para processamento.  Caso o valor desse parâmetro seja muito grande, o acesso aos dados pode ser lento, pois você não tem memória suficiente para processar com eficiência um bloco de dados grande.  Em alguns sistemas, definindo *rowsPerRead* para um valor excessivamente pequeno também pode fornecer o desempenho mais lento.

3. Neste ponto, você criou o *inDataSource* objeto, mas ele não contém nenhum dado. Os dados não são recebidos da consulta SQL no ambiente local até que você executar uma função, como [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) ou [rxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary).

    No entanto, agora que você definiu os objetos de dados, você pode usá-lo como o argumento para outras funções.

## <a name="use-the-sql-server-data-in-r-summaries"></a>Usar os dados do SQL Server nos resumos de R

Nesta seção, você testará várias das funções fornecidas no [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] contextos de computação remota esse suporte. Aplicando funções de R à fonte de dados, você pode explorar, resumir e de gráfico de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados.

1. Chamar a função [rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo) para obter uma lista das variáveis na fonte de dados e seus tipos de dados.

    **rxGetVarInfo** é uma função útil; você pode chamá-lo em qualquer quadro de dados, ou em um conjunto de dados em um objeto de dados remotos obter informações como o máximo e mínimo valores, o tipo de dados e o número de níveis em colunas de fator.
    
    Considere a possibilidade de executar essa função após qualquer espécie de entrada de dados, transformação de recursos ou engenharia de recursos. Ao fazer isso, você pode garantir que todos os recursos que você deseja usar em seu modelo estão os dados esperados de tipo e evitar erros.
  
    ```R
    rxGetVarInfo(data = inDataSource)
    ```

    **Resultados**
    
    ```
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

    rxSummary se baseia no R `summary` funcionar, mas apresenta algumas vantagens e recursos adicionais. rxSummary funciona em vários contextos de computação e dá suporte a agrupamento.  Você também pode usar rxSummary para transformar os valores ou resumir com base nos níveis de fator.
    
    Neste exemplo, você resumir a tarifa com base no número de passageiros.
    
    ```R
    start.time <- proc.time()
    rxSummary(~fare_amount:F(passenger_count,1,6), data = inDataSource)
    used.time <- proc.time() - start.time
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds,
      Elapsed Time=", round(used.time[3],2),
      " seconds to summarize the inDataSource.", sep=""))
    ```
    + O primeiro argumento para rxSummary Especifica a fórmula ou o termo para resumir por. Aqui, o `F()` função é usada para converter os valores de _passageiro\_contagem_ em fatores antes do resumo. Você também precisará especificar o valor mínimo (1) e o valor máximo (6) para o _passageiro\_contagem_ variável de fator.
    + Se você não especificar as estatísticas de saída, por padrão rxSummary gera Mean, StDev, Min, Max e o número de observações válidas e ausentes.
    + Este exemplo também inclui um código para acompanhar o tempo durante o qual a função é iniciada e concluída, para que você possa comparar o desempenho.
  
    **Resultados**

    Se a função rxSummary for executado com êxito, você deve ver resultados como estes, seguido por uma lista de estatísticas por categoria. 

    ```
    rxSummary(formula = ~fare_amount:F(passenger_count, 1,6), data = inDataSource)
    Data: inDataSource (RxSqlServerData Data Source)
    Number of valid observations: 1000
    ```

### <a name="bonus-exercise-on-big-data"></a>Exercício extra em big data

Tente definir uma nova cadeia de caracteres de consulta com todas as linhas. é recomendável que você configure um novo objeto de fonte de dados para esse teste. Você também pode tentar alterar o *rowsToRead* parâmetro para ver como ele afeta a taxa de transferência.

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
> Enquanto isso está em execução, você pode usar uma ferramenta como o [Process Explorer](https://technet.microsoft.com/sysinternals/processexplorer.aspx) ou o SQL Profiler para ver como a conexão é feita e o código R é executado usando os serviços do SQL Server.
> 
> Outra opção é monitorar trabalhos de R em execução no SQL Server usando esses [relatórios personalizados](../r/monitor-r-services-using-custom-reports-in-management-studio.md).

## <a name="next-lesson"></a>Próxima lição

[Criar grafos e gráficos usando o R](walkthrough-create-graphs-and-plots-using-r.md)

## <a name="previous-lesson"></a>Lição anterior

[Explorar os dados usando o SQL](walkthrough-view-and-explore-the-data.md)
