---
title: "Li&#231;&#227;o 4: Criar e salvar o modelo (Passo a passo de ponta a ponta sobre a ci&#234;ncia de dados) | Microsoft Docs"
ms.custom: ""
ms.date: "11/22/2016"
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
ms.assetid: 69b374c1-2042-4861-8f8b-204a6297c0db
caps.latest.revision: 20
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 18
---
# Li&#231;&#227;o 4: Criar e salvar o modelo (Passo a passo de ponta a ponta sobre a ci&#234;ncia de dados)
Nesta lição, você aprenderá a criar um modelo de aprendizado de máquina e salvá-lo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="creating-a-classification-model"></a>Criando um modelo de classificação  
O modelo que você criará é um classificador binário que prevê a probabilidade de o motorista do táxi receber uma gorjeta em uma corrida específica. Você usará a fonte de dados criada na lição anterior, `featureDataSource,` para treinar o classificador de gorjetas, usando a regressão logística.  
  
Estes são os recursos que você usará no modelo:  
  
-   passenger_count  
  
-   trip_distance  
  
-   trip_time_in_secs  
  
-   direct_distance  

### <a name="create-the-model-using-rxlogit"></a>Criar o modelo usando rxLogit  
1.  Chame a função *rxLogit*, incluída no pacote **RevoScaleR**, para criar um modelo de regressão logística.  
  
    ```R  
    system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = featureDataSource))    
    ```  
  
2.  Depois de criar o modelo, inspecione-o usando a função `summary` e exiba os coeficientes.  
  
    ```  
    summary(logitObj)  
    ```  

     *Resultados*

     *Resultados de regressão logística para: tipped ~ passenger_count + trip_distance + trip_time_in_secs +*  
     *direct_distance*  
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
  
### <a name="use-the-logistic-regression-model-for-scoring"></a>Usar o modelo de regressão logística de pontuação  
Agora que o modelo foi criado, você pode usá-lo para prever a probabilidade de o motorista receber uma gorjeta em uma corrida específica.  
  
1.  Primeiro, defina o objeto de dados a ser usado para armazenar os resultados da pontuação  
  
    ```R  
    scoredOutput <- RxSqlServerData(  
      connectionString = connStr,  
      table = "taxiScoreOutput"  )  
    ```  
    + Para simplificar este exemplo, a entrada para o modelo de regressão logística é a mesma `featureDataSource` usada para treinar o modelo.  Normalmente, talvez você tenha alguns novos dados para usar na pontuação ou tenha reservado alguns dados para teste versus treinamento.  
  
    + Os resultados da previsão são salvos na tabela _taxiscoreOutput_. Observe que o esquema desta tabela não é definido durante sua criação usando `rxSqlServerData`, mas é obtido por meio da saída do objeto *scoredOutput* de `rxPredict`.  
  
    + Para criar a tabela que armazena os valores previstos, o logon do SQL que executa a função de dados `rxSqlServer` deve ter privilégios DDL no banco de dados. Se o logon não conseguir criar tabelas, a instrução falhará.  
  
2.  Chame a função *rxPredict* para gerar resultados.  
  
    ```R  
    rxPredict(modelObject = logitObj, data = featureDataSource, outData = scoredOutput,   
                       predVarNames = "Score", type = "response",   
                       writeModelVars = TRUE, overwrite = TRUE)  
    ```  

  
## <a name="plotting-model-accuracy"></a>Plotagem de precisão do modelo  
Para obter uma ideia da precisão do modelo, você pode usar a função *rxRocCurve* para plotar a Curva Operacional do Receptor. Como *rxRocCurve* é uma das novas funções fornecidas pelo pacote RevoScaleR que dá suporte a contextos de computação remota, você tem duas opções:  
  
+ Você pode usar a função `rxRocCurve` para executar a plotagem no contexto do computador remoto e retornar a plotagem ao cliente local.
+ Você também pode importar os dados para o computador cliente do R e usar outras funções de plotagem do R para criar o gráfico de desempenho.  
  
Nesta seção, você usará as duas técnicas.  
  
### <a name="execute-a-plot-in-the-remote-sql-server-compute-context"></a>Executar uma plotagem no contexto de computação remota (SQL Server)  
  
1.  Chame a função *rxRocCurve* e forneça os dados definidos anteriormente como entrada.  
  
    ```R  
    rxRocCurve( "tipped", "Score", scoredOutput)  
    ```  
  
    Observe que você também deve especificar a coluna de rótulo tipped (a variável que você está tentando prever) e o nome da coluna que armazena a previsão (_Score_).  
  
2.  Exiba o gráfico gerado abrindo o dispositivo gráfico R ou clicando na janela **Plotar** no RStudio.  
  
    ![ROC plot for the model](../../advanced-analytics/r-services/media/rsql-e2e-rocplot.png "ROC plot for the model")  

    O gráfico é criado no contexto de computação remota e retornado ao seu ambiente do R.   
    
### <a name="create-the-plots-in-the-local-compute-context-using-data-from-sql-server"></a>Criar as plotagens no contexto de computação local usando dados do SQL Server  
  
1.  Use a função *rxImport* para levar os dados especificados para seu ambiente local do R.  
  
    ```R  
    scoredOutput = rxImport(scoredOutput)  
    ```  
  
2.  Depois de carregar os dados na memória local, você poderá chamar a biblioteca **ROCR** para criar algumas previsões e gerar a plotagem.  
  
    ```R  
    library('ROCR')  
    pred <- prediction(scoredOutput$Score, scoredOutput$tipped)  
  
    acc.perf = performance(pred, measure = 'acc')  
    plot(acc.perf)  
    ind = which.max( slot(acc.perf, 'y.values')[[1]] )  
    acc = slot(acc.perf, 'y.values')[[1]][ind]  
    cutoff = slot(acc.perf, 'x.values')[[1]][ind]  
    ```  
  
3.  O gráfico a seguir é gerado em ambos os casos.  
  
    ![plotting model performance using R](../../advanced-analytics/r-services/media/rsql-e2e-performanceplot.png "plotting model performance using R")  
  
## <a name="deploying-a-model"></a>Implantando um modelo  

Depois de criar um modelo e decidir que ele tem um bom desempenho, talvez você queira *colocar o modelo em operação*. Como o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] permite invocar um modelo do R usando um procedimento armazenado do [!INCLUDE[tsql](../../includes/tsql-md.md)] , é extremamente fácil de usar o R em um aplicativo cliente.  
  
No entanto, antes de poder chamar o modelo de um aplicativo externo, você deve salvar o modelo no banco de dados usado para produção. No [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], os modelos treinados são armazenados em formato binário, em uma única coluna do tipo **varbinary(max)**.

Portanto, mover um modelo treinado de R para o SQL Server inclui as seguintes etapas:  
  
+ Serializando o modelo em uma cadeia de caracteres hexadecimal
+ Transmitindo o objeto serializado para o banco de dados
+ Salvando o modelo em uma coluna varbinary(max)  
  
Nesta seção, você aprenderá a persistir o modelo e como chamá-lo para fazer previsões.  
  
### <a name="serialize-the-model"></a>Serializar o modelo  
  
+  Em seu ambiente de R local, serialize o modelo e salve-o em uma variável.  
  
    ```R  
    modelbin <- serialize(logitObj, NULL)  
    modelbinstr=paste(modelbin, collapse="")  
    ```  
  
    A função *serialize* é incluída no pacote **base** do R, e fornece uma interface simples de baixo nível para serializar para conexões. Para obter mais informações, visite [http://www.inside-r.org/r-doc/base/serialize](http://www.inside-r.org/r-doc/base/serialize).  
  
### <a name="move-the-model-to-sql-server"></a>Mover o modelo para o SQL Server

+ Abra uma conexão ODBC e chame um procedimento armazenado para salvar a representação binária do modelo em uma coluna no banco de dados. 
  
    ```R  
    library(RODBC)  
    conn <- odbcDriverConnect(connStr )  
  
    # persist model by calling a stored procedure from SQL  
    q<-paste("EXEC PersistModel @m='", modelbinstr,"'", sep="")  
    sqlQuery (conn, q)    
    ```  

Salvar um modelo em uma tabela exige apenas uma instrução INSERT. No entanto, para facilitar, usamos aqui o procedimento armazenado _PersistModel_. 
 
Para referência, este é o código completo do procedimento armazenado:  
  
```tsql  
CREATE PROCEDURE [dbo].[PersistModel]  @m nvarchar(max)  
AS  
BEGIN  
        -- SET NOCOUNT ON added to prevent extra result sets from  
        -- interfering with SELECT statements.  
        SET NOCOUNT ON;  
        insert into nyc_taxi_models (model) values (convert(varbinary(max),@m,2))  
END   
```  
> [!TIP] Recomendamos criar funções auxiliares como esse procedimento armazenado para facilitar o gerenciamento e a atualização dos modelos do R no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
  
### <a name="invoke-the-saved-model"></a>Invocar o modelo salvo  
Depois de salvar o modelo no banco de dados, você poderá chamá-lo diretamente por meio do código [!INCLUDE[tsql](../../includes/tsql-md.md)], usando o procedimento armazenado do sistema [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).  
  
Por exemplo, para gerar previsões, basta conectar-se ao banco de dados e executar um procedimento armazenado que usa o modelo salvo como uma entrada, juntamente com alguns dados de entrada.  
  
No entanto, se você tiver um modelo que usa com frequência, será mais fácil encapsular a consulta de entrada e a chamada para o modelo, bem como outros parâmetros, em um procedimento armazenado personalizado.  
  
Na próxima lição, você aprenderá a realizar a pontuação no modelo salvo usando [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="next-lesson"></a>Próxima lição  
[Lição 5: Implantar e usar o modelo &#40;Passo a passo de ponta a ponta sobre a ciência de dados&#41;](../../advanced-analytics/r-services/lesson-5-deploy-and-use-the-model-data-science-end-to-end-walkthrough.md)  
  
## <a name="previous-lesson"></a>Lição anterior  
[Lição 3: Criar recursos de dados &#40;Passo a passo de ponta a ponta sobre a ciência de dados&#41;](../../advanced-analytics/r-services/lesson-3-create-data-features-data-science-end-to-end-walkthrough.md)  
  
  
  
