---
title: Criar um modelo do R e salvar para o SQL Server (passo a passo) – SQL Server Machine Learning
description: Tutorial que mostra como criar um modelo de linguagem de R usado para análise do SQL Server no banco de dados.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b02b1e0298af6fbb96ba5ddd8d5a18dc8e154598
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645475"
---
# <a name="build-an-r-model-and-save-to-sql-server-walkthrough"></a>Criar um modelo do R e salvar para o SQL Server (passo a passo)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Nesta etapa, saiba como criar um modelo de aprendizado de máquina e salvar o modelo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ao salvar um modelo, você pode chamá-lo diretamente do [!INCLUDE[tsql](../../includes/tsql-md.md)] de código, usando o procedimento armazenado do sistema [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) ou o [função PREDICT (T-SQL)](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql).

## <a name="prerequisites"></a>Prerequisites

Essa etapa pressupõe que uma sessão de R em andamento, com base nas etapas anteriores neste passo a passo. Ele usa as conexão cadeias de caracteres e dados de origem objetos criados nessas etapas. As ferramentas e os pacotes a seguir são usados para executar o script.

+ Rgui.exe para executar comandos de R
+ Management Studio para executar o T-SQL
+ Pacote ROCR
+ Pacote RODBC

### <a name="create-a-stored-procedure-to-save-models"></a>Criar um procedimento armazenado para salvar modelos

Esta etapa usa um procedimento armazenado para salvar um modelo treinado para o SQL Server. Criar um procedimento armazenado para executar essa operação torna a tarefa mais fácil.

Execute o seguinte código T-SQL em uma janela de consulta no Management Studio para criar o procedimento armazenado.

```sql
USE [NYCTaxi_Sample]
GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO

IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'PersistModel')
  DROP PROCEDURE PersistModel
GO

CREATE PROCEDURE [dbo].[PersistModel] @m nvarchar(max)
AS
BEGIN
    -- SET NOCOUNT ON added to prevent extra result sets from
    -- interfering with SELECT statements.
    SET NOCOUNT ON;
    insert into nyc_taxi_models (model) values (convert(varbinary(max),@m,2))
END
GO
```

> [!NOTE]
> Se você receber um erro, certifique-se de que seu logon tem permissão para criar objetos. Você pode conceder permissões explícitas para criar objetos, executando uma instrução T-SQL como esta: `exec sp_addrolemember 'db_owner', '<user_name>'`.

## <a name="create-a-classification-model-using-rxlogit"></a>Criar um modelo de classificação usando rxLogit

O modelo é um classificador binário que prevê se o motorista do táxi tem probabilidade de receber uma gorjeta em uma corrida específica ou não. Você usará a fonte de dados que você criou na lição anterior para treinar o classificador de gorjetas, usando a regressão logística.

1. Chame a função [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit) , incluída no pacote **RevoScaleR** , para criar um modelo de regressão logística. 

    ```R
    system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = featureDataSource));
    ```

    A chamada que cria o modelo é colocada na função system.time. Isso permite que você obtenha o tempo necessário para criar o modelo.

2. Depois de criar o modelo, você poderá inspecioná-lo usando o `summary` de função e exibir os coeficientes.

    ```R
    summary(logitObj);
    ```

    **Resultados**
    
    ```R
     *Logistic Regression Results for: tipped ~ passenger_count + trip_distance + trip_time_in_secs +*
     direct_distance* 
     *Data: featureDataSource (RxSqlServerData Data Source)*
     *Dependent variable(s): tipped*
     *Total independent variables: 5*
     *Number of valid observations: 17068*
     *Number of missing observations: 0*
     *-2\*LogLikelihood: 23540.0602 (Residual deviance on 17063 degrees of freedom)*
     *Coefficients:*
     *Estimate Std. Error z value Pr(>|z|)*
     *(Intercept)       -2.509e-03  3.223e-02  -0.078  0.93793*
     *passenger_count   -5.753e-02  1.088e-02  -5.289 1.23e-07 \*\*\**
     *trip_distance     -3.896e-02  1.466e-02  -2.658  0.00786 \*\**
     *trip_time_in_secs  2.115e-04  4.336e-05   4.878 1.07e-06 \*\*\**
     *direct_distance    6.156e-02  2.076e-02   2.966  0.00302 \*\**
     *---*
     *Signif. codes:  0 ‘\*\*\*’ 0.001 ‘\*\*’ 0.01 ‘\*’ 0.05 ‘.’ 0.1 ‘ ’ 1*
     *Condition number of final variance-covariance matrix: 48.3933*
     *Number of iterations: 4*
   ```

## <a name="use-the-logistic-regression-model-for-scoring"></a>Usar o modelo de regressão logística de pontuação

Agora que o modelo foi criado, você pode usá-lo para prever a probabilidade de o motorista receber uma gorjeta em uma corrida específica.

1. Primeiro, use o [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) função para definir um objeto de fonte de dados para armazenar o resultado de pontuação.

    ```R
    scoredOutput <- RxSqlServerData(
      connectionString = connStr,
      table = "taxiScoreOutput"  )
    ```

    + Para simplificar este exemplo, a entrada para o modelo de regressão logística é a mesma fonte de dados de recurso (`sql_feature_ds`) que você usou para treinar o modelo.  Normalmente, talvez você tenha alguns novos dados para usar na pontuação ou tenha reservado alguns dados para teste versus treinamento.
  
    + Os resultados da previsão serão salvo na tabela, _taxiscoreOutput_. Observe que o esquema para esta tabela não é definido quando você criá-lo usando o rxSqlServerData. O esquema é obtido da saída rxPredict.
  
    + Para criar a tabela que armazena os valores previstos, o logon do SQL executando a função de dados rxSqlServer deve ter privilégios DDL no banco de dados. Se o logon não é possível criar tabelas, a instrução falhará.

2. Chame a função [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict) para gerar resultados.

    ```R
    rxPredict(modelObject = logitObj,
        data = featureDataSource,
        outData = scoredOutput,
        predVarNames = "Score",
        type = "response",
        writeModelVars = TRUE, overwrite = TRUE)
    ```
    
    Se a instrução for bem-sucedida, deve levar algum tempo para ser executado. Ao concluir, você pode abrir o SQL Server Management Studio e verifique se a tabela foi criada e que ele contém a coluna de pontuação e outros a saída esperada.

## <a name="plot-model-accuracy"></a>Gráfico de precisão do modelo

Para obter uma ideia da precisão do modelo, você pode usar o [rxRoc](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxroc) função para plotar a curva operacional do receptor. Como rxRoc é uma das novas funções fornecidas pelo pacote RevoScaleR que dá suporte a contextos de computação remota, você tem duas opções:

+ Você pode usar a função rxRoc para executar a plotagem no contexto de computação remota e, em seguida, retornar a plotagem ao seu cliente local.

+ Você também pode importar os dados para o computador cliente do R e usar outras funções de plotagem do R para criar o gráfico de desempenho.

Nesta seção, você irá experimentar as duas técnicas.

### <a name="execute-a-plot-in-the-remote-sql-server-compute-context"></a>Executar uma plotagem no contexto de computação remota (SQL Server)

1. Chamar a função rxRoc e fornecer os dados definidos anteriormente como entrada.

    ```R
    scoredOutput = rxImport(scoredOutput);
    rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    ```

    Essa chamada retorna os valores usados na computação o gráfico ROC. É a coluna de rótulo _tipped_, que tem os resultados reais que você está tentando prever, enquanto o _pontuação_ coluna tem a previsão.

2. Para plotar, na verdade, o gráfico, você pode salvar o objeto ROC e então desenhá-lo com a função de plotagem. O gráfico é criado no contexto de computação remota e retornado ao seu ambiente de R.

    ```R
    scoredOutput = rxImport(scoredOutput);
    rocObjectOut <- rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    plot(rocObjectOut);
    ```

    Exiba o gráfico abrindo o dispositivo gráfico R ou clicando o **plotar** janela no RStudio.

    ![Plotagem ROC para o modelo](media/rsql-e2e-rocplot.png "Plotagem ROC para o modelo")

### <a name="create-the-plots-in-the-local-compute-context-using-data-from-sql-server"></a>Criar as plotagens no contexto de computação local usando dados do SQL Server

Você pode verificar o contexto de computação é local, executando `rxGetComputeContext()` no prompt de comando. O valor de retorno deve ser "Contexto de computação RxLocalSeq".

1. Para o contexto de computação local, o processo é muito parecido com isso. Você usa o [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) função para trazer os dados especificados para seu ambiente local do R.

    ```R
    scoredOutput = rxImport(scoredOutput)
    ```

2. Usando os dados na memória local, carregue o **ROCR** empacotar e use a função de previsão do que o pacote para criar algumas novas previsões.

    ```R
    library('ROCR');
    pred <- prediction(scoredOutput$Score, scoredOutput$tipped);
    ```

3. Plotar um gráfico de local, com base nos valores armazenados na variável de saída `pred`.

    ```R
    acc.perf = performance(pred, measure = 'acc');
    plot(acc.perf);
    ind = which.max( slot(acc.perf, 'y.values')[[1]] );
    acc = slot(acc.perf, 'y.values')[[1]][ind];
    cutoff = slot(acc.perf, 'x.values')[[1]][ind];
    ```

    ![plotagem de desempenho do modelo usando R](media/rsql-e2e-performanceplot.png "plotagem de desempenho do modelo usando R")

> [!NOTE]
> Os gráficos podem parecer diferentes dos seguintes, dependendo de quantos pontos de dados que você usou.

## <a name="deploy-the-model"></a>Implantar o modelo

Depois que você tiver criado um modelo e determinou que ele tem um bom desempenho, você provavelmente desejará implantá-lo em um site em que os usuários ou as pessoas em sua organização podem fazer usar do modelo, ou talvez treinar novamente e recalibrar o modelo com regularidade. Esse processo às vezes é chamado *operacionalização* um modelo. No SQL Server, a operacionalização é obtida, inserindo código R em um procedimento armazenado. Como o código reside no procedimento, ele pode ser chamado de qualquer aplicativo que pode se conectar ao SQL Server.

Antes de chamar o modelo de um aplicativo externo, você deve salvar o modelo para o banco de dados usado para a produção. Modelos treinados são armazenados em formato binário, em uma única coluna do tipo **varbinary (max)**.

Um fluxo de trabalho de implantação típica consiste as seguintes etapas:

1. Serialize o modelo para uma cadeia de caracteres hexadecimal
2. O objeto serializado para o banco de dados de transmissão
3. Salvar o modelo em uma coluna varbinary (max)

Nesta seção, Aprenda a usar um procedimento armazenado para manter o modelo e torná-lo disponível para previsões. O procedimento armazenado usado nesta seção é PersistModel. A definição de PersistModel está no [pré-requisitos](#prerequisites).

1. Alternar de volta para seu ambiente R local se já não estiver usando ele, serialize o modelo e salvá-lo em uma variável.

    ```R
    rxSetComputeContext("local");
    modelbin <- serialize(logitObj, NULL);
    modelbinstr=paste(modelbin, collapse="");
    ```

2. Abra uma conexão ODBC usando **RODBC**. Se você já tiver o pacote carregado, você pode omitir a chamada para RODBC.

    ```R
    library(RODBC);
    conn <- odbcDriverConnect(connStr);
    ```

3. Chame o procedimento PersistModel armazenado no SQL Server para transmite o objeto serializado para o banco de dados e armazenar a representação binária do modelo em uma coluna. 

    ```R
    q <- paste("EXEC PersistModel @m='", modelbinstr,"'", sep="");
    sqlQuery (conn, q);
    ```

4. Use o Management Studio para verificar se o modelo existe. No Pesquisador de objetos, clique com botão direito no **nyc_taxi_models** tabela e clique em **selecionar 1000 linhas superiores**. Nos resultados, você deve ver uma representação binária na **modelos** coluna.

Salvar um modelo em uma tabela exige apenas uma instrução INSERT. No entanto, é mais fácil quando encapsulado em um procedimento armazenado, tais como *PersistModel*.

## <a name="next-steps"></a>Próximas etapas

A próxima e última lição, aprenderá a executar a pontuação contra o modelo salvo usando [!INCLUDE[tsql](../../includes/tsql-md.md)].

> [!div class="nextstepaction"]
> [Implantar o modelo do R e usar em SQL](walkthrough-deploy-and-use-the-model.md)
