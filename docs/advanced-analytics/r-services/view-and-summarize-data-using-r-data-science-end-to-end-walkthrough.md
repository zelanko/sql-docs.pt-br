---
title: "Exibir e resumir dados usando o R (Passo a passo de ponta a ponta sobre a ci&#234;ncia de dados) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
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
ms.assetid: 358e1431-8f47-4d32-a02f-f90e519eef49
caps.latest.revision: 21
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# Exibir e resumir dados usando o R (Passo a passo de ponta a ponta sobre a ci&#234;ncia de dados)
Agora você trabalhará com os mesmos dados usando o código do R. Você também aprenderá a usar as funções do pacote **RevoScaleR** incluídas no [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] para gerar resumos de dados no contexto do servidor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e enviar os resultados de volta para o ambiente do R.  

Um script do R que inclui todo o código necessário para criar o objeto de dados, gerar resumos e criar modelos é fornecido neste passo a passo. O arquivo de script do R, **RSQL_RWalkthrough.R**, podem ser encontrado no local em que você instalou os arquivos de script.  
+ Se estiver familiarizado com R, você poderá executar o script de uma só vez.
+ Para quem está aprendendo a usar o RevoScaleR, este tutorial percorre o script linha por linha
+ Para executar linhas individuais do script, você pode realçar uma linha ou linhas no arquivo e pressionar Ctrl + ENTER.    
  
> [!TIP]  Salve o espaço de trabalho do R caso você deseje concluir o restante do passo a passo mais tarde.  Dessa forma, os objetos de dados e outras variáveis estarão prontos para reutilização.   

## <a name="defining-sql-server-data-sources-and-compute-contexts"></a>Definindo fontes de dados e contextos de computação do SQL Server
Para obter dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para usar em seu código de R, você precisa:  
  
- Criar uma conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
- Definir uma consulta que contenha os dados de que você precisa, ou especificar uma tabela ou modo de exibição    
- = Definir um ou mais contextos de computação para usar ao executar o código do R    
-   Opcionalmente, definir funções que podem ser aplicadas à fonte de dados  
 

### <a name="load-the-revoscaler-library"></a>Carregar a biblioteca RevoScaleR

+  Se o pacote **RevoScaleR** ainda não estiver carregado, execute:
    ```R
    library("RevoScaleR")`.  
    ```  
    Se você receber um erro, verifique se o ambiente de desenvolvimento do R está usando a biblioteca que inclui o pacote RevoScaleR. Usar um comando como `.libPaths())` para exibir o caminho atual:  

    Se esta for a primeira vez que você usa o pacote **RevoScaleR**, obtenha ajuda online no ambiente do R, digitando `help("RevoScaleR")` ou `help("RxSqlServerData")`.  

### <a name="create-connection-strings"></a>Criar cadeias de conexão


1. Defina as cadeias de conexão. Para este passo a passo, fornecemos exemplos de logons do SQL Server e autenticação integrada do Windows. É recomendável que você use autenticação do Windows sempre que possível, para evitar salvar senhas no seu código do R.

    A conta que você usa deve ter permissões para ler dados e criar novas tabelas no banco de dados especificado. Para obter informações sobre como adicionar usuários ao banco de dados SQL e lhes conceder as permissões corretas, consulte [Configuração do servidor pós-instalação &#40;SQL Server R Services&#41;](../Topic/Post-Installation%20Server%20Configuration%20(SQL%20Server%20R%20Services).md). 

    ```R  
    # SQL authentication  
    connStrSql <- "Driver=SQL Server;Server=<SQL_instance_name>;Database=<database_name>;    Uid=<user_name>;Pwd=<user password>"  

    # Windows authentication  
    connStrWin <- "Driver=SQL Server;Server=<SQL_instance_name>;Database=<database_name>;Trusted_Connection=Yes" 
    
    # Use one of the connection strings
    connStr <- connStrWin 
    ```
    > [!NOTE] Lembre-se de editar o nome do servidor, o nome do banco de dados, o nome de usuário e a senha, conforme necessário. 
      
  
### <a name="define-and-set-a-compute-context"></a>Definir e configurar um contexto de computação  

Em seguida, você definirá um *contexto de computação* que permite que o código de R seja executado no computador do SQL Server. Normalmente, quando você estiver usando o R, todas as operações são executadas na memória do computador. No entanto, indicando que as operações de R devem ser executadas na instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode executar algumas tarefas em paralelo e tirar proveito dos recursos do servidor.  

Por padrão, o contexto de computação é local, portanto, você precisará definir explicitamente o contexto de computação, dependendo da operação.  


1.  Comece definindo algumas das variáveis usadas para criar o contexto de computação.  
  
    ```R    
    sqlShareDir <- paste("C:\\AllShare\\",Sys.getenv("USERNAME"),sep="")  
    sqlWait <- TRUE  
    sqlConsoleOutput <- FALSE    
    ```    
    -   O R usa um diretório temporário ao serializar objetos de R de um lado para outro entre a estação de trabalho e o computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode especificar o diretório local que é usado como *sqlShareDir*, ou aceitar o padrão.  
  
    -   Use *sqlWait* para indicar se deseja que o R espere por resultados ou não.  Para obter uma discussão sobre aguardar versus não aguardar trabalhos, veja [Computação distribuída do ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing).
  
    -   Use o argumento *sqlConsoleOutput* para indicar que você não deseja ver a saída do console de R.  
  
2.  Crie o objeto de contexto de computação com variáveis e cadeias de conexão já definidas, e salve-o na variável de R *sqlcc*.  
  
    ```  
    sqlcc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir,   
                        wait = sqlWait, consoleOutput = sqlConsoleOutput)  
    ```  

4. Defina o contexto de computação.
    ```R
    rxSetComputeContext(sqlcc)  
    ```  
   + O `rxSetComputeContext` retorna o contexto de computação anteriormente ativo de forma invisível para que você possa usá-lo
   + O `rxGetComputeContext` retorna o contexto de computação ativo  
  
    Observe que definir esse contexto de computação só afeta as operações que usam funções no pacote **RevoScaleR** ; o contexto de computação não afeta a maneira como as operações de software livre do R são executadas.  
  
### <a name="create-an-rxsqlserver-data-object"></a>Criar um objeto de dados RxSqlServer  

Agora que definiu a conexão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com a qual vai trabalhar, você poderá usar esse objeto de conexão de dados como a base para definir fontes de dados diferentes. Uma *fonte de dados* especifica um conjunto de dados que você deseja usar para uma tarefa, tal como, treinamento, exploração, classificação ou gerenciamento de recursos.  
    
Você define conjuntos de dados do SQL Server usando a função *RxSqlServer* e passando uma cadeia de conexão e a definição de dados a serem obtidos.  
  
1. Salve a instrução SQL como uma variável de cadeia de caracteres. Essa consulta define os dados que você usará para treinar o modelo.    
    ```R
    sampleDataQuery <- "SELECT TOP 1000 tipped, fare_amount, 
           passenger_count,trip_time_in_secs,trip_distance,   
           pickup_datetime, dropoff_datetime, pickup_longitude, 
           pickup_latitude, dropoff_longitude,    
           dropoff_latitude 
           FROM nyctaxi_sample"  
    ```

2. Passe a definição de consulta como um argumento para a fonte de dados do SQL Server. O argumento *colClasses* especifica o esquema dos dados a ser retornado, por meio de mapeamento do SQL 

    ```R  
    inDataSource <- RxSqlServerData(sqlQuery = sampleDataQuery, 
         connectionString = connStr,
         colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
         dropoff_longitude = "numeric", dropoff_latitude = "numeric"),  
         rowsPerRead=500)  
    ```
    
    + O argumento *colClasses* especifica os tipos de coluna a serem usados ao mover os dados entre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o R. Isso é importante porque o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa tipos de dados diferentes do R e mais tipos de dados. Para obter mais informações, consulte [Trabalhando com tipos de dados do R](../../advanced-analytics/r-services/working-with-r-data-types.md).  
  
    + O argumento *rowsPerRead* é importante para lidar com o uso de memória e cálculos eficientes.  A maioria das funções analíticas avançadas no[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] processa dados em partes e acumula resultados intermediários, retornando os cálculos finais após a leitura de todos os dados.  Ao adicionar o parâmetro `rowsPerRead` , você pode controlar a quantidade de linhas de dados lidas em cada bloco de processamento.  Caso o valor desse parâmetro seja muito grande, o acesso aos dados pode ser lento, pois você não tem memória suficiente para processar com eficiência um bloco de dados grande.  Em alguns sistemas, a definição de `rowsPerRead` com um valor muito pequeno também pode causar um desempenho mais lento.  

> [!TIP] Após a criação do objeto *inDataSource*, você poderá reutilizar esse objeto quantas vezes for necessário, para obter informações básicas sobre os dados e as variáveis usadas, a fim de manipular e transformar os dados ou usá-los para treinar um modelo.  No entanto, o próprio objeto *inDataSource* ainda não contém dados da consulta SQL. Os dados não são recebidos no ambiente local até que você execute uma função como *rxImport* ou *rxSummary*.          
  
## <a name="using-the-sql-server-data-in-r"></a>Usando os dados do SQL Server em R  
Agora você pode aplicar funções do R à fonte de dados para explorar, resumir e traçar um gráfico dos dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Nesta seção, você testará várias das funções fornecidas no [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] que dão suporte a contextos de computação remota.  
  
-   `rxGetVarInfo`: use essa função com qualquer quadro de dados ou conjunto de dados em um objeto de dados remoto (também com algumas listas e matrizes) para obter informações como os valores mínimo e máximo, o tipo de dados e o número de níveis em colunas de fator.  
  
    Considere a possibilidade de executar essa função após qualquer espécie de entrada de dados, transformação de recursos ou engenharia de recursos. Ao fazer isso, você pode garantir que todos os recursos que você deseja usar no modelo são do tipo de dados esperado e evitar erros.  
 
  
-   `rxSummary`: use essa função para obter estatísticas mais detalhadas sobre variáveis individuais. Você também pode transformar os valores, calcular resumos usando níveis de fator e salvar os resumos para reutilização.  
  
  
### <a name="inspect-variables-in-the-data-source"></a>Inspecionar variáveis na fonte de dados  
    
+ Chame a função `rxGetVarInfo`, usando a fonte de dados  `inDataSource` como um argumento, para obter uma lista das variáveis na fonte de dados e seus tipos de dados.  
  
    ```R  
    rxGetVarInfo(data = inDataSource)  
    ```  
  
    *Resultados:*  
    *Var 1: tipped, Type: integer*  
    *Var 2: fare_amount, Type: numeric*  
    *Var 3: passenger_count, Type: integer*  
    *Var 4: trip_time_in_secs, Type: numeric, Storage: int64*  
    *Var 5: trip_distance, Type: numeric*  
    *Var 6: pickup_datetime, Type: character*  
    *Var 7: dropoff_datetime, Type: character*  
    *Var 8: pickup_longitude, Type: numeric*  
    *Var 9: pickup_latitude, Type: numeric*  
    *Var 10: dropoff_longitude, Type: numeric*  
  
### <a name="create-a-summary-using-r"></a>Criar um resumo usando R

+ Chame a função RevoScaleR `rxSummary` para resumir a tarifa, com base no número de passageiros. 
    ```R  
    start.time <- proc.time()  
    rxSummary(~fare_amount:F(passenger_count), data = inDataSource)  
    used.time <- proc.time() - start.time  
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds,
      Elapsed Time=", round(used.time[3],2), 
      " seconds to summarize the inDataSource.", sep=""))
    ```  
 
    + O primeiro argumento para `rxSummary` especifica a fórmula ou o termo no qual o resumo se baseará. Neste exemplo, a função `F()` é usada para converter os valores de passenger_count em fatores antes do resumo.  
    + Se você não especificar as estatísticas a serem geradas, por padrão, `rxSummary` vai gerar Mean, StDev, Min, Max e o número de observações válidas e ausentes.  
    + Este exemplo também inclui um código para acompanhar o tempo durante o qual a função é iniciada e concluída, para que você possa comparar o desempenho.  
  
    *Resultados*  
    *rxSummary(formula = ~fare_amount:F(passenger_count), data = inDataSource)*  
    *Summary Statistics Results for: ~fare_amount:F(passenger_count)*  
    *Data: inDataSource (RxSqlServerData Data Source)*  
    *Number of valid observations: 1000*   
    *Name                          Mean    StdDev   Min Max ValidObs MissingObs*  
    *fare_amount:F_passenger_count 12.4875 9.682605 2.5 64  1000     0*   
    *Statistics by category (6 categories):   *Category                             F_passenger_count Means    StdDev    Min*   
    *fare_amount for F(passenger_count)=1 1                 12.00901  9.219458  2.5*  
    *fare_amount for F(passenger_count)=2 2                 11.61893  8.858739  3.0*  
    *fare_amount for F(passenger_count)=3 3                 14.40196 10.673340  3.5*  
    *fare_amount for F(passenger_count)=4 4                 13.69048  8.647942  4.5*  
    *fare_amount for F(passenger_count)=5 5                 19.30909 14.122969  3.5*  
    *fare_amount for F(passenger_count)=6 6                 12.00000        NA 12.0*  
    *Max ValidObs*  
    *55  666*   
    *52  206*   
    *52   51*   
    *39   21*   
    *64   55*   
    *12    1*   
    *"It takes CPU Time=0.5 seconds, Elapsed Time=4.59 seconds to summarize the inDataSource."*  
  

  
## <a name="next-step"></a>Próxima etapa  
[Criar gráficos e plotagens usando o R &#40;Passo a passo de ponta a ponta sobre a ciência de dados&#41;](../../advanced-analytics/r-services/create-graphs-and-plots-using-r-data-science-end-to-end-walkthrough.md)  
  
## <a name="previous-lesson"></a>Lição anterior  
[Lição 1: Preparar os dados &#40;Passo a passo de ponta a ponta sobre a ciência de dados&#41;](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)  
  
  
  
