---
title: 'Python + T-SQL: Treinar um modelo'
description: Tutorial do Python mostrando como treinar e salvar um modelo usando o Transact-SQL no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/01/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b8bec553502b2e5c8d69436e539437be9a5989aa
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73724880"
---
# <a name="train-and-save-a-python-model-using-t-sql"></a>Treinar e salvar um modelo do Python usando o T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo faz parte de um tutorial, [Análise do Python no banco de dados para desenvolvedores do SQL](sqldev-in-database-python-for-sql-developers.md). 

Nesta etapa, você aprenderá a treinar um modelo de machine learning usando os pacotes do Python **Scikit-learn** e **revoscalepy**. Essas bibliotecas do Python já estão instaladas com os Serviços de Machine Learning do SQL Server.

Você carrega os módulos e chama as funções necessárias para criar e treinar o modelo usando um procedimento armazenado do SQL Server. O modelo requer os recursos de dados que você desenvolveu em lições anteriores. Por fim, você salva o modelo treinado em uma tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
 

## <a name="split-the-sample-data-into-training-and-testing-sets"></a>Divida os dados de exemplo em conjuntos de teste e treinamento

1. Crie um procedimento armazenado chamado **PyTrainTestSplit** para dividir os dados na tabela nyctaxi_sample em duas partes: nyctaxi_sample_training e nyctaxi_sample_testing. 

    Esse procedimento armazenado já deve ter sido criado para você, mas você pode executar o seguinte código para criá-lo:

    ```sql
    DROP PROCEDURE IF EXISTS PyTrainTestSplit;
    GO

    CREATE PROCEDURE [dbo].[PyTrainTestSplit] (@pct int)
    AS
    
    DROP TABLE IF EXISTS dbo.nyctaxi_sample_training
    SELECT * into nyctaxi_sample_training FROM nyctaxi_sample WHERE (ABS(CAST(BINARY_CHECKSUM(medallion,hack_license)  as int)) % 100) < @pct
    
    DROP TABLE IF EXISTS dbo.nyctaxi_sample_testing
    SELECT * into nyctaxi_sample_testing FROM nyctaxi_sample
    WHERE (ABS(CAST(BINARY_CHECKSUM(medallion,hack_license)  as int)) % 100) > @pct
    GO
    ```

2. Para dividir seus dados usando uma divisão personalizada, execute o procedimento armazenado e digite um inteiro que represente o percentual de dados alocados ao conjunto de treinamento. Por exemplo, a instrução a seguir alocará 60% dos dados ao conjunto de treinamento.

    ```sql
    EXEC PyTrainTestSplit 60
    GO
    ```

## <a name="build-a-logistic-regression-model"></a>Criar um modelo de regressão logística

Depois da preparação dos dados, você pode usá-los para treinar um modelo. Você faz isso chamando um procedimento armazenado que executa algum código Python usando a tabela de dados de treinamento como entrada. Para este tutorial, você cria dois modelos, ambos modelos de classificação binária:

+ O procedimento armazenado **PyTrainScikit** cria um modelo de previsão de gorjeta usando o pacote **Scikit-learn**.
+ O procedimento armazenado **TrainTipPredictionModelRxPy** cria um modelo de previsão de gorjeta usando o pacote **revoscalepy**.

Cada procedimento armazenado usa os dados de entrada que você fornece para criar e treinar um modelo de regressão logística. Todo o código Python é encapsulado no procedimento armazenado do sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

Para facilitar o novo treinamento do modelo em novos dados, você encapsula a chamada para sp_execute_external_script em outro procedimento armazenado e passa os novos dados de treinamento como um parâmetro. Esta seção guiará você pelo processo.

### <a name="pytrainscikit"></a>PyTrainScikit

1.  No [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra uma nova janela de **Consulta** e execute a instrução a seguir para criar o procedimento armazenado **PyTrainScikit**.  O procedimento armazenado contém uma definição dos dados de entrada, assim, você não precisa fornecer uma consulta de entrada.

    ```sql
    DROP PROCEDURE IF EXISTS PyTrainScikit;
    GO

    CREATE PROCEDURE [dbo].[PyTrainScikit] (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
    EXEC sp_execute_external_script
      @language = N'Python',
      @script = N'
    import numpy
    import pickle
    from sklearn.linear_model import LogisticRegression
    
    ##Create SciKit-Learn logistic regression model
    X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
    y = numpy.ravel(InputDataSet[["tipped"]])
    
    SKLalgo = LogisticRegression()
    logitObj = SKLalgo.fit(X, y)
    
    ##Serialize model
    trained_model = pickle.dumps(logitObj)
    ',
    @input_data_1 = N'
    select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, 
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
    from nyctaxi_sample_training
    ',
    @input_data_1_name = N'InputDataSet',
    @params = N'@trained_model varbinary(max) OUTPUT',
    @trained_model = @trained_model OUTPUT;
    ;
    END;
    GO
    ```

2. Execute as seguintes instruções SQL para inserir o modelo treinado na tabela nyc\_taxi_models.

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC PyTrainScikit @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('SciKit_model', @model);
    ```

    O processamento dos dados e o ajuste do modelo poderão levar alguns minutos. As mensagens que serão redirecionadas para o fluxo **stdout** do Python são exibidas na janela **Mensagens** do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Por exemplo:

    *Mensagens STDOUT do script externo:* 
  *C:\Arquivos de Programas\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy*

3. Abra a tabela *nyc\_taxi_models*. Você pode ver que uma nova linha foi adicionada, que contém o modelo serializado na coluna _modelo_.

    *SciKit_model* *0x800363736B6C6561726E2E6C696E6561...*

### <a name="traintippredictionmodelrxpy"></a>TrainTipPredictionModelRxPy

Esse procedimento armazenado usa o novo pacote **revoscalepy**, que é um novo pacote para Python. Ele contém objetos, transformação e algoritmos semelhantes aos fornecidos para o pacote **RevoScaleR** da linguagem R. 

Usando **revoscalepy**, você pode criar contextos de computação remota, mover dados entre contextos de computação, transformar dados e treinar modelos de previsão usando algoritmos populares, como regressão logística e linear, árvores de decisão e muito mais. Para obter mais informações, confira o [módulo revoscalepy no SQL Server](../python/ref-py-revoscalepy.md) e a [referência de função revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package).

1. No [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra uma nova janela de **Consulta** e execute a instrução a seguir para criar o procedimento armazenado _TrainTipPredictionModelRxPy_.  Como o procedimento armazenado já inclui uma definição dos dados de entrada, você não precisa fornecer uma consulta de entrada.

    ```sql
    DROP PROCEDURE IF EXISTS TrainTipPredictionModelRxPy;
    GO

    CREATE PROCEDURE [dbo].[TrainTipPredictionModelRxPy] (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
    EXEC sp_execute_external_script 
      @language = N'Python',
      @script = N'
    import numpy
    import pickle
    from revoscalepy.functions.RxLogit import rx_logit
    
    ## Create a logistic regression model using rx_logit function from revoscalepy package
    logitObj = rx_logit("tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance", data = InputDataSet);
    
    ## Serialize model
    trained_model = pickle.dumps(logitObj)
    ',
    @input_data_1 = N'
    select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, 
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
    from nyctaxi_sample_training
    ',
    @input_data_1_name = N'InputDataSet',
    @params = N'@trained_model varbinary(max) OUTPUT',
    @trained_model = @trained_model OUTPUT;
    ;
    END;
    GO
    ```

    Esse procedimento armazenado executa as seguintes etapas como parte do treinamento do modelo:

    - A consulta SELECT aplica a função escalar personalizada _fnCalculateDistance_ para calcular a distância direta entre os locais de embarque e desembarque de passageiros. Os resultados da consulta são armazenados na variável de entrada padrão do Python, `InputDataset`.
    - A variável binária _tipped_ é usada como a coluna *label* ou de resultado e o modelo é ajustado com o uso destas colunas de recursos: _passenger_count_, _trip_distance_, _trip_time_in_secs_e _direct_distance_.
    - O modelo treinado é serializado e armazenado na variável do Python `logitObj`. Ao adicionar a palavra-chave OUTPUT do T-SQL, você pode adicionar a variável como uma saída do procedimento armazenado. Na próxima etapa, essa variável é usada para inserir o código binário do modelo em uma tabela de banco de dados _nyc_taxi_models_. Esse mecanismo torna mais fácil armazenar e reutilizar modelos.

2. Execute o procedimento armazenado da seguinte maneira para inserir o modelo treinado **revoscalepy** na tabela *nyc_taxi_models*.

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC TrainTipPredictionModelRxPy @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('revoscalepy_model', @model);
    ```

    O processamento dos dados e o ajuste do modelo poderão levar algum tempo. As mensagens que serão redirecionadas para o fluxo **stdout** do Python são exibidas na janela **Mensagens** do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Por exemplo:

    *Mensagens STDOUT do script externo:* 
  *C:\Arquivos de Programas\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy*

3. Abra a tabela *nyc_taxi_models*. Você pode ver que uma nova linha foi adicionada, que contém o modelo serializado na coluna _modelo_.

    *revoscalepy_model* *0x8003637265766F7363616c...*

Na próxima etapa, você usará os modelos treinados para criar previsões.

## <a name="next-step"></a>Próxima etapa

[Executar previsões usando o Python inserido em um procedimento armazenado](sqldev-py6-operationalize-the-model.md)

## <a name="previous-step"></a>Etapa anterior

[Criar recursos de dados usando o T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)
