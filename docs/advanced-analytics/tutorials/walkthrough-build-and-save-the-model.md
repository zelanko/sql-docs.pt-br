---
title: Criar um modelo de R e salvar para o SQL Server | Microsoft Docs
ms.custom: 
ms.date: 07/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 69b374c1-2042-4861-8f8b-204a6297c0db
caps.latest.revision: "21"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: e2fc182a273a9b6adee4a59729b023d3113507a8
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="build-an-r-model-and-save-to-sql-server"></a>Criar um modelo de R e salvar para o SQL Server

Nesta etapa, você aprenderá como criar um modelo de aprendizado de máquina e salvar o modelo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

## <a name="create-a-classification-model-using-rxlogit"></a>Criar um modelo de classificação usando rxLogit

O modelo que você cria é um classificador binário que prevê se o driver táxi é provavelmente obter uma dica sobre uma determinado jornada ou não. Você usará a fonte de dados que você criou na lição anterior para treinar o classificador de ponta, usando Regressão logística.

1. Chame a função [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit) , incluída no pacote **RevoScaleR** , para criar um modelo de regressão logística. 

    ```R
    system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = sql_feature_ds));
    ```

    A chamada que cria o modelo é colocada na função system.time. Isso permite que você obtenha o tempo necessário para criar o modelo.

2. Depois de criar o modelo, você pode verificar isso usando o `summary` de função e exibir os coeficientes.

    ```R
    summary(logitObj);
    ```

     *Resultados*

     *Resultados de regressão logística para:-Oblíquo ~ passenger_count + trip_distance + trip_time_in_secs +*
     <br/>*direct_distance*
     <br/>*Dados: featureDataSource (RxSqlServerData de fonte de dados)*
     <br/>*Dependent Variable(s): Oblíquo*
     <br/>*Total de variáveis independentes: 5*
     <br/>*Número de observações válidos: 17068*
     <br/>*Número de observações ausentes: 0*
     <br/>*-2\*LogLikelihood: 23540.0602 (desvio Residual em graus de 17063 liberdade)*
     <br/>*Coeficientes:*
     <br/>*Estimate Std. O valor de erro z Pr (> | z |)*
     <br/>*(Intercept)       -2.509e-03  3.223e-02  -0.078  0.93793*
     <br/>*passenger_count   -5.753e-02  1.088e-02  -5.289 1.23e-07 \*\*\**
     <br/>*trip_distance     -3.896e-02  1.466e-02  -2.658  0.00786 \*\**
     <br/>*trip_time_in_secs 2.115e-04 4.336e-05 4.878 1.07e-06\*\*\**
     <br/>*direct_distance    6.156e-02  2.076e-02   2.966  0.00302 \*\**
     <br/>*---*
     <br/>*Signif. codes:  0 ‘\*\*\*’ 0.001 ‘\*\*’ 0.01 ‘\*’ 0.05 ‘.’ 0.1 ‘ ’ 1*
     <br/>*Número de matriz de covariância de variação final de condição: 48.3933*
     <br/>*Number of iterations: 4*

## <a name="use-the-logistic-regression-model-for-scoring"></a>Usar o modelo de regressão logística de pontuação

Agora que o modelo foi criado, você pode usá-lo para prever a probabilidade de o motorista receber uma gorjeta em uma corrida específica.

1. Primeiro, use o [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) função para definir um objeto de fonte de dados para armazenar a pontuação resul

    ```R
    scoredOutput <- RxSqlServerData(
      connectionString = connStr,
      table = "taxiScoreOutput"  )
    ```

    + Para simplificar este exemplo, a entrada para o modelo de regressão logística é a mesma fonte de dados de recurso (`sql_feature_ds`) que você usou para treinar o modelo.  Normalmente, talvez você tenha alguns novos dados para usar na pontuação ou tenha reservado alguns dados para teste versus treinamento.
  
    + Os resultados da previsão serão salvo na tabela, _taxiscoreOutput_. Observe que o esquema para esta tabela não é definido quando você cria usando rxSqlServerData. O esquema é obtido da saída rxPredict.
  
    + Para criar a tabela que armazena os valores previstos, o logon do SQL que executa a função de dados rxSqlServer deve ter privilégios DDL no banco de dados. Se o logon não é possível criar tabelas, a instrução falhará.

2. Chame a função [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict) para gerar resultados.

    ```R
    rxPredict(modelObject = logitObj,
        data = sql_feature_ds,
        outData = scoredOutput,
        predVarNames = "Score",
        type = "response",
        writeModelVars = TRUE, overwrite = TRUE)
    ```
    
    Se a instrução for bem-sucedida, ela deverá levar algum tempo para ser executado. Ao concluir, pode abrir o SQL Server Management Studio e verifique se a tabela foi criada e que contém a coluna de pontuação e outros esperado de saída.

## <a name="plot-model-accuracy"></a>Gráfico de precisão do modelo

Para obter uma ideia do que a precisão do modelo, você pode usar o [rxRoc](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxroc) função para plotar a curva de operação do receptor. Como rxRoc é uma das novas funções fornecidas pelo pacote RevoScaleR que dá suporte a contextos de computação remota, você tem duas opções:

+ Você pode usar a função rxRoc para executar a plotagem no contexto de computação remota e, em seguida, retorna a plotagem para seu cliente local.

+ Você também pode importar os dados para o computador cliente do R e usar outras funções de plotagem do R para criar o gráfico de desempenho.

Nesta seção, você experimentará com ambas as técnicas.

### <a name="execute-a-plot-in-the-remote-sql-server-compute-context"></a>Executar uma plotagem no contexto de computação remota (SQL Server)

1. Chame a função rxRoc e fornecer os dados definidos anteriormente como entrada.

    ```R
    scoredOutput = rxImport(scoredOutput);
    rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    ```

    Essa chamada retorna os valores usados no gráfico ROC de computação. A coluna de rótulo é _Oblíquo_, que tem os resultados reais que você está tentando prever, enquanto o _pontuação_ coluna tem a previsão.

2. Para plotar, na verdade, o gráfico, você pode salvar o objeto ROC e desenhe-o com o `plot` função. O gráfico é criado no contexto de computação remota e retornado ao seu ambiente de R.

    ```R
    scoredOutput = rxImport(scoredOutput);
    rocObjectOut <- rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    plot(rocObjectOut);
    ```

    Exibir o gráfico, abrir o dispositivo de gráficos de R, ou clicando o **plotar** janela no RStudio.

    ![Plotagem ROC para o modelo](media/rsql-e2e-rocplot.png "Plotagem ROC para o modelo")

### <a name="create-the-plots-in-the-local-compute-context-using-data-from-sql-server"></a>Criar as plotagens no contexto de computação local usando dados do SQL Server

1. Para o contexto de computação local, o processo é semelhante a. Você usa o [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) função para colocar os dados especificados no seu ambiente local do R.

    ```R
    scoredOutput = rxImport(scoredOutput)
    ```

2. Usando os dados na memória local, você carrega o **ROCR** empacotar e use a função de previsão do que o pacote para criar algumas novas previsões.

    ```R
    library('ROCR');
    pred <- prediction(scoredOutput$Score, scoredOutput$tipped);
    ```

3. Gerar um gráfico de local, com base nos valores armazenados na variável de saída `pred`.

    ```R
    acc.perf = performance(pred, measure = 'acc');
    plot(acc.perf);
    ind = which.max( slot(acc.perf, 'y.values')[[1]] );
    acc = slot(acc.perf, 'y.values')[[1]][ind];
    cutoff = slot(acc.perf, 'x.values')[[1]][ind];
    ```

    ![plotagem de desempenho do modelo usando R](media/rsql-e2e-performanceplot.png "plotagem de desempenho do modelo usando R")

> [!NOTE]
> Os gráficos podem ser diferentes dos seguintes, dependendo de quantos pontos de dados que você usou.

## <a name="deploy-the-model"></a>Implantar o modelo

Depois de ter criado um modelo e determinou que ele está sendo executada adequadamente, você provavelmente desejará implantá-lo em um site onde os usuários ou pessoas na sua organização podem fazer uso do modelo, ou talvez treinar novamente e calibrar novamente o modelo regularmente. Esse processo às vezes é chamado *operacionalização* um modelo.

Porque [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] permite a invocação de um modelo de R usando um [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimento armazenado, é fácil de usar o R em um aplicativo cliente.

No entanto, antes de poder chamar o modelo de um aplicativo externo, você deve salvar o modelo no banco de dados usado para produção. No [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], os modelos treinados são armazenados em formato binário, em uma única coluna do tipo **varbinary(max)**.

Portanto, mover um modelo treinado de R para o SQL Server inclui as seguintes etapas:

+ Serializando o modelo em uma cadeia de caracteres hexadecimal

+ Transmitindo o objeto serializado para o banco de dados

+ Salvando o modelo em uma coluna varbinary(max)

Nesta seção, você aprenderá como manter o modelo e como chamá-lo para fazer previsões.

1. Alternar de volta para seu ambiente de R local se já não estiver usando ele, serialize o modelo e salvá-lo em uma variável.

    ```R
    rxSetComputeContext("local");
    modelbin <- serialize(logitObj, NULL);
    modelbinstr=paste(modelbin, collapse="");
    ```

2. Abrir uma conexão ODBC usando **RODBC**.

    ```R
    library(RODBC);
    conn <- odbcDriverConnect(connStr);
    ```

    Você pode omitir a chamada para RODBC se você já tiver o pacote carregado.

3. Chame o procedimento armazenado criado pelo script do PowerShell, para armazenar a representação binária do modelo em uma coluna no banco de dados.

    ```R
    q <- paste("EXEC PersistModel @m='", modelbinstr,"'", sep="");
    sqlQuery (conn, q);
    ```

    Salvar um modelo em uma tabela exige apenas uma instrução INSERT. No entanto, é mais fácil quando encapsulado em um procedimento armazenado, como _PersistModel_.

    > [!NOTE]
    > Se você receber um erro como "a permissão EXECUTE foi negada no objeto PersistModel", certifique-se de que o logon tenha permissão. Você pode conceder permissões explícitas no procedimento armazenado executando uma instrução T-SQL como esta:`GRANT EXECUTE ON [dbo].[PersistModel] TO <user_name>`

4. Depois que você criou um modelo e o salvou em um banco de dados, você pode chamá-lo diretamente do [!INCLUDE[tsql](../../includes/tsql-md.md)] de código, usando o procedimento armazenado do sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

    No entanto, com qualquer modelo usados com frequência, é mais fácil encapsular a consulta de entrada e a chamada para o modelo, juntamente com outros parâmetros em um procedimento armazenado personalizado.

    Aqui está o código completo de um tal procedimento armazenado. É recomendável criar um procedimento armazenado como este para tornar mais fácil de gerenciar e atualizar os modelos de R no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

    ```tsql
    CREATE PROCEDURE [dbo].[PersistModel]  @m nvarchar(max)
    AS
    BEGIN
      SET NOCOUNT ON;
      INSERT INTO nyc_taxi_models (model) values (convert(varbinary(max),@m,2))
    END
    ```

  > [!NOTE]
  > Use o **SET NOCOUNT ON** define a cláusula para evitar resultados extras de interferir com instruções SELECT.


A próxima e final lição, você aprenderá a executar pontuação usando o modelo de salvo [!INCLUDE[tsql](../../includes/tsql-md.md)].

## <a name="next-lesson"></a>Próxima lição

[Implantar o modelo de R e usar em SQL](walkthrough-deploy-and-use-the-model.md)

## <a name="previous-lesson"></a>Lição anterior

[Criar recursos de dados usando R e SQL](walkthrough-create-data-features.md)

