---
title: Treinar e salvar um modelo de Python usando o T-SQL – SQL Server Machine Learning
description: Tutorial do Python que mostra como treinar e salvar um modelo usando Transact-SQL no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/01/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 2e0505cf847a091a5650b392aab56f486cee16aa
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511243"
---
# <a name="train-and-save-a-python-model-using-t-sql"></a>Treinar e salvar um modelo de Python usando o T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo faz parte de um tutorial [análise de Python no banco de dados para desenvolvedores do SQL](sqldev-in-database-python-for-sql-developers.md). 

Nesta etapa, você aprenderá a treinar um modelo de aprendizado de máquina usando os pacotes do Python **scikit-Saiba** e **revoscalepy**. Essas bibliotecas Python já estão instaladas com os serviços do SQL Server Machine Learning.

Você pode carrega os módulos e chama as funções necessárias para criar e treinar o modelo usando um procedimento armazenado do SQL Server. O modelo requer os recursos de dados desenvolvido nas lições anteriores. Por fim, você pode salvar o modelo treinado para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela.
 

## <a name="split-the-sample-data-into-training-and-testing-sets"></a>Dividir os dados de exemplo em treinamento e conjuntos de teste

1. Criar um procedimento armazenado chamado **PyTrainTestSplit** para dividir os dados na tabela nyctaxi_sample em duas partes: nyctaxi_sample_training e nyctaxi_sample_testing. 

    Esse procedimento armazenado deve ser criado para você, mas você pode executar o código a seguir para criá-lo:

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

2. Para dividir seus dados usando uma divisão personalizada, execute o procedimento armazenado e digite um número inteiro que representa a porcentagem dos dados alocados para o conjunto de treinamento. Por exemplo, a instrução a seguir alocará 60% dos dados para o conjunto de treinamento.

    ```sql
    EXEC PyTrainTestSplit 60
    GO
    ```

## <a name="build-a-logistic-regression-model"></a>Criar um modelo de regressão logística

Depois que os dados foram preparados, você pode usá-lo para treinar um modelo. Você pode fazer isso chamando um armazenado procedimento que executa um código do Python, tomando como a tabela de dados de treinamento de entrada. Para este tutorial, você pode criar dois modelos, ambos os modelos de classificação binária:

+ O procedimento armazenado **PyTrainScikit** cria um modelo de previsão de tip usando o **scikit-Saiba** pacote.
+ O procedimento armazenado **TrainTipPredictionModelRxPy** cria um modelo de previsão de tip usando o **revoscalepy** pacote.

Cada procedimento armazenado usa os dados de entrada que você fornece para criar e treinar um modelo de regressão logística. Todo o código Python é encapsulado em um procedimento armazenado do sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

Para tornar mais fácil de treinar novamente o modelo em dados novos, encapsule a chamada para sp_execute_exernal_script em outro procedimento armazenado e passar os novos dados de treinamento como um parâmetro. Esta seção orientará você pelo processo.

### <a name="pytrainscikit"></a>PyTrainScikit

1.  Na [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra uma nova **consulta** e execute a seguinte instrução para criar o procedimento armazenado **PyTrainScikit**.  O procedimento armazenado contiver uma definição dos dados de entrada, portanto você não precisa fornecer uma consulta de entrada.

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

2. Execute as seguintes instruções SQL para inserir o modelo treinado em tabela nyc\_taxi_models.

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC PyTrainScikit @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('SciKit_model', @model);
    ```

    Processamento de dados e ajuste do modelo podem levar alguns minutos. As mensagens que serão redirecionadas para do Python **stdout** fluxo são exibidos na **mensagens** janela de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Por exemplo:

    *STDOUT message(s) from external script:*
  *C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy*

3. Abra a tabela *nyc\_taxi_models*. Você pode ver que uma nova linha foi adicionada, que contém o modelo serializado na coluna _modelo_.

    *SciKit_model* *0x800363736B6C6561726E2E6C696E6561...*

### <a name="traintippredictionmodelrxpy"></a>TrainTipPredictionModelRxPy

Esse procedimento armazenado usa o novo **revoscalepy** pacote, que é um novo pacote para o Python. Ele contém objetos, transformação e algoritmos semelhantes àqueles fornecidos para a linguagem de R **RevoScaleR** pacote. 

Usando **revoscalepy**, você pode criar os contextos de computação remota, mover dados entre contextos de computação, transformar dados e treinar modelos de previsão usando algoritmos populares, como a regressão logística e linear, árvores de decisão, e mais. Para obter mais informações, consulte [módulo revoscalepy no SQL Server](../python/ref-py-revoscalepy.md) e [referência de função revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package).

1. Na [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra uma nova **consulta** e execute a seguinte instrução para criar o procedimento armazenado _TrainTipPredictionModelRxPy_.  Como o procedimento armazenado já inclui uma definição dos dados de entrada, você não precisa fornecer uma consulta de entrada.

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

    Esse procedimento armazenado executa as etapas a seguir como parte do treinamento do modelo:

    - A consulta SELECT aplica-se a função escalar personalizada _fnCalculateDistance_ para calcular a distância direta entre os locais de embarque e desembarque de passageiros. Os resultados da consulta são armazenados na variável de entrada do Python do padrão, `InputDataset`.
    - A variável binária _tipped_ é usado como o *rótulo* ou a coluna resultado e o modelo é ajustado com o uso dessas colunas de recurso: _passenger_count_, _trip_ distância_, _trip_time_in_secs_, e _direct_distance_.
    - O modelo treinado é serializado e armazenado na variável Python `logitObj`. Adicionando a palavra-chave de T-SQL OUTPUT, você pode adicionar a variável como uma saída do procedimento armazenado. Na próxima etapa, essa variável é usada para inserir o código binário do modelo em uma tabela de banco de dados _nyc_taxi_models_. Esse mecanismo torna fácil armazenar e reutilizar modelos.

2. Execute o procedimento armazenado da seguinte maneira para inserir o treinado **revoscalepy** modelo na tabela *nyc_taxi_models*.

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC TrainTipPredictionModelRxPy @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('revoscalepy_model', @model);
    ```

    Processamento de dados e ajuste do modelo podem levar algum tempo. As mensagens que serão redirecionadas para do Python **stdout** fluxo são exibidos na **mensagens** janela de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Por exemplo:

    *STDOUT message(s) from external script:*
  *C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy*

3. Abra a tabela *nyc_taxi_models*. Você pode ver que uma nova linha foi adicionada, que contém o modelo serializado na coluna _modelo_.

    *revoscalepy_model* *0x8003637265766F7363616c....*

Na próxima etapa, você pode usar os modelos treinados para criar previsões.

## <a name="next-step"></a>Próxima etapa

[Execute previsões usando Python inserido em um procedimento armazenado](sqldev-py6-operationalize-the-model.md)

## <a name="previous-step"></a>Etapa anterior

[Criar recursos de dados usando o T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)
