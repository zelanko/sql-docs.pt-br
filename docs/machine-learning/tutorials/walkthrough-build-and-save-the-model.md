---
title: 'Tutorial do R: Criar e salvar modelo'
description: Saiba mais sobre como criar um modelo de machine learning de linguagem R usado para análise no banco de dados do SQL Server.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9ab81bc27b2dfd8f32004b9289ab02a8ce1d3007
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88178703"
---
# <a name="build-an-r-model-and-save-to-sql-server-walkthrough"></a>Criar um modelo do R e salvar no SQL Server (passo a passo)
[!INCLUDE [SQL Server 2016](../../includes/applies-to-version/sqlserver2016.md)]

Nesta etapa, você aprenderá a criar um modelo de machine learning e salvá-lo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ao salvar um modelo, você pode chamá-lo diretamente do código [!INCLUDE[tsql](../../includes/tsql-md.md)] usando o procedimento armazenado do sistema [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) ou a função [PREDICT (T-SQL)](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql).

## <a name="prerequisites"></a>Pré-requisitos

Esta etapa pressupõe uma sessão do R em andamento com base nas etapas anteriores neste passo a passos. Ela usa as cadeias de conexão e os objetos de fonte de dados criados nessas etapas. As seguintes ferramentas e pacotes são usados para executar o script.

+ Rgui.exe para executar comandos do R
+ Management Studio para executar T-SQL
+ Pacote ROCR
+ Pacote RODBC

### <a name="create-a-stored-procedure-to-save-models"></a>Crie um procedimento armazenado para salvar modelos

Esta etapa usa um procedimento armazenado para salvar um modelo treinado no SQL Server. A criação de um procedimento armazenado para executar essa operação facilita a tarefa.

Execute o seguinte código do T-SQL em uma janela de consulta no Management Studio para criar o procedimento armazenado.

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
> Se você receber um erro, verifique se o logon tem permissão para criar objetos. Você pode conceder permissões explícitas para criar objetos executando uma instrução T-SQL como esta: `exec sp_addrolemember 'db_owner', '<user_name>'`.

## <a name="create-a-classification-model-using-rxlogit"></a>Criar um modelo de classificação usando rxLogit

O modelo é um classificador binário que prevê a probabilidade de o motorista do táxi receber ou não uma gorjeta em uma corrida específica. Você usará a fonte de dados criada na lição anterior para treinar o classificador de gorjetas, usando a regressão logística.

1. Chame a função [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit) , incluída no pacote **RevoScaleR** , para criar um modelo de regressão logística. 

    ```R
    system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = featureDataSource));
    ```

    A chamada que cria o modelo é colocada na função system.time. Isso permite que você obtenha o tempo necessário para criar o modelo.

2. Depois de criar o modelo, inspecione-o usando a função `summary` e exiba os coeficientes.

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

1. Primeiro, use a função [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) para definir um objeto de fonte de dados para armazenar o resultado da pontuação.

    ```R
    scoredOutput <- RxSqlServerData(
      connectionString = connStr,
      table = "taxiScoreOutput"  )
    ```

    + Para simplificar este exemplo, a entrada para o modelo de regressão logística é a mesma fonte de dados de recurso (`sql_feature_ds`) usada para treinar o modelo.  Normalmente, talvez você tenha alguns novos dados para usar na pontuação ou tenha reservado alguns dados para teste versus treinamento.
  
    + Os resultados da previsão serão salvos na tabela _taxiscoreOutput_. Observe que o esquema desta tabela não é definido quando você a cria usando rxSqlServerData. O esquema é obtido da saída do rxPredict.
  
    + Para criar a tabela que armazena os valores previstos, o logon do SQL que executa a função de dados rxSqlServer deve ter privilégios DDL no banco de dados. Se o logon não consegue criar tabelas, a instrução falha.

2. Chame a função [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict) para gerar resultados.

    ```R
    rxPredict(modelObject = logitObj,
        data = featureDataSource,
        outData = scoredOutput,
        predVarNames = "Score",
        type = "response",
        writeModelVars = TRUE, overwrite = TRUE)
    ```
    
    Se a instrução obtém sucesso, ela deve levar algum tempo para ser executada. Ao concluir, você pode abrir o SQL Server Management Studio e verificar se a tabela foi criada e contém a coluna Pontuação e outra saída esperada.

## <a name="plot-model-accuracy"></a>Plotar a precisão do modelo

Para obter uma ideia da precisão do modelo, você pode usar a função [rxRoc](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxroc) para plotar a Curva Operacional do Receptor. Com rxRoc é uma das novas funções fornecidas pelo pacote RevoScaleR que dá suporte a contextos de computação remota, você tem duas opções:

+ Você pode usar a função rxRoc para executar o gráfico no contexto de computação remota e retornar o gráfico ao cliente local.

+ Você também pode importar os dados para o computador cliente do R e usar outras funções de plotagem do R para criar o gráfico de desempenho.

Nesta seção, você experimentará ambas as técnicas.

### <a name="execute-a-plot-in-the-remote-sql-server-compute-context"></a>Executar uma plotagem no contexto de computação remota (SQL Server)

1. Chame a função rxRoc e forneça os dados definidos anteriormente como entrada.

    ```R
    scoredOutput = rxImport(scoredOutput);
    rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    ```

    Essa chamada retorna os valores usados na computação do gráfico ROC. A coluna de rótulo é _gorjeta dada_, que tem os resultados reais que você está tentando prever, enquanto a coluna _Pontuação_ tem a previsão.

2. Para realmente plotar o gráfico, você pode salvar o objeto ROC e, em seguida, desenhá-lo com a função plot. O gráfico é criado no contexto de computação remota e retornado a seu ambiente do R.

    ```R
    scoredOutput = rxImport(scoredOutput);
    rocObjectOut <- rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    plot(rocObjectOut);
    ```

    Veja o gráfico abrindo o dispositivo gráfico do R ou clicando na janela **Plotar** no RStudio.

    ![Gráfico de ROC para o modelo](media/rsql-e2e-rocplot.png "Gráfico de ROC para o modelo")

### <a name="create-the-plots-in-the-local-compute-context-using-data-from-sql-server"></a>Criar as plotagens no contexto de computação local usando dados do SQL Server

Você pode verificar se o contexto de computação é local executando `rxGetComputeContext()` no prompt de comando. O valor retornado deve ser "Contexto de Computação RxLocalSeq".

1. Para o contexto de computação local, o processo é basicamente o mesmo. Use a função [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) para levar os dados especificados para seu ambiente local do R.

    ```R
    scoredOutput = rxImport(scoredOutput)
    ```

2. Usando os dados na memória local, você carrega o pacote **ROCR** e usa a função de previsão desse pacote para criar algumas previsões.

    ```R
    library('ROCR');
    pred <- prediction(scoredOutput$Score, scoredOutput$tipped);
    ```

3. Gere um gráfico local com base nos valores armazenados na variável de saída `pred`.

    ```R
    acc.perf = performance(pred, measure = 'acc');
    plot(acc.perf);
    ind = which.max( slot(acc.perf, 'y.values')[[1]] );
    acc = slot(acc.perf, 'y.values')[[1]][ind];
    cutoff = slot(acc.perf, 'x.values')[[1]][ind];
    ```

    ![como plotar o desempenho do modelo usando o R](media/rsql-e2e-performanceplot.png "como plotar o desempenho do modelo usando o R")

> [!NOTE]
> Seus gráficos podem ser diferentes dependendo de quantos pontos de dados você usou.

## <a name="deploy-the-model"></a>Implantar o modelo

Depois de criar um modelo e determinar que ele está funcionando bem, você provavelmente vai querer implantá-lo em um site em que os usuários ou pessoas em sua organização possam usá-lo ou talvez treinar novamente e recalibrar o modelo regularmente. Esse processo às vezes é chamado de *operacionalizar* um modelo. No SQL Server, a operacionalização é obtida inserindo o código R em um procedimento armazenado. Como o código reside no procedimento, ele pode ser chamado de qualquer aplicativo que possa se conectar ao SQL Server.

Antes de poder chamar o modelo de um aplicativo externo, você deve salvar o modelo no banco de dados usado para produção. Os modelos treinados são armazenados em formato binário, em uma única coluna do tipo **varbinary(max)** .

Um fluxo de trabalho de implantação típico consiste nas seguintes etapas:

1. Como serializar o modelo em uma cadeia de caracteres hexadecimal
2. Como transmitir o objeto serializado para o banco de dados
3. Como salvar o modelo em uma coluna varbinary(max)

Nesta seção, saiba como usar um procedimento armazenado para manter o modelo e disponibilizá-lo para previsões. O procedimento armazenado usado nesta seção é PersistModel. A definição de PersistModel está em [Pré-requisitos](#prerequisites).

1. Volte para o ambiente do R local se você ainda não o estiver usando. Serialize o modelo e salve-o em uma variável.

    ```R
    rxSetComputeContext("local");
    modelbin <- serialize(logitObj, NULL);
    modelbinstr=paste(modelbin, collapse="");
    ```

2. Abra uma conexão ODBC usando **RODBC**. Você poderá omitir a chamada para RODBC se já tiver o pacote carregado.

    ```R
    library(RODBC);
    conn <- odbcDriverConnect(connStr);
    ```

3. Chame o procedimento armazenado PersistModel no SQL Server para transmitir o objeto serializado para o banco de dados e armazenar a representação binária do modelo em uma coluna. 

    ```R
    q <- paste("EXEC PersistModel @m='", modelbinstr,"'", sep="");
    sqlQuery (conn, q);
    ```

4. Use o Management Studio para verificar se o modelo existe. No Pesquisador de Objetos, clique com o botão direito do mouse na tabela **nyc_taxi_models** e clique em **Selecionar as 1.000 Primeiras Linhas**. Nos resultados, você deverá ver uma representação binária na coluna **modelos**.

Salvar um modelo em uma tabela exige apenas uma instrução INSERT. No entanto, geralmente é mais fácil quando encapsulado em um procedimento armazenado, como *PersistModel*.

## <a name="next-steps"></a>Próximas etapas

Na próxima e última lição, você aprenderá a realizar a pontuação no modelo salvo usando [!INCLUDE[tsql](../../includes/tsql-md.md)].

> [!div class="nextstepaction"]
> [Implantar o modelo do R e usar no SQL](walkthrough-deploy-and-use-the-model.md)
