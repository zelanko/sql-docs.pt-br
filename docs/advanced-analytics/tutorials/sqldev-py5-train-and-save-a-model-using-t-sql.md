---
title: 'Etapa 5: Treinar e salvar um modelo de Python usando o T-SQL | Microsoft Docs'
ms.custom: 
ms.date: 10/17/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: "2"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 07777ff0752a68e574c5f7f1a0021a8817eb7ea0
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="step-5-train-and-save-a-python-model-using-t-sql"></a>Etapa 5: Treinar e salvar um modelo de Python usando o T-SQL

Este artigo faz parte de um tutorial, [análise Python no banco de dados para desenvolvedores em SQL](sqldev-in-database-python-for-sql-developers.md). 

Nesta etapa, você aprenderá a treinar um modelo de aprendizado de máquina usando os pacotes do Python **scikit-Saiba** e **revoscalepy**. Essas bibliotecas Python já estão instaladas com os serviços de aprendizado de máquina do SQL Server.

Carregar os módulos e chamar as funções necessárias para criar e treinar o modelo usando um procedimento armazenado do SQL Server. O modelo requer os recursos de dados criadas nas lições anteriores. Por fim, você pode salvar o modelo treinado para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela.

> [!IMPORTANT]
> Houve diversas alterações no **revoscalepy** pacote, que são necessárias pequenas alterações no código para este tutorial. Consulte o [changelist](sqldev-py6-operationalize-the-model.md#changes) no final deste tutorial. 
> 
> Se você instalou os serviços de Python usando uma versão de pré-lançamento do SLq Server 2017, recomendamos que você atualize para a versão mais recente. 

## <a name="split-the-sample-data-into-training-and-testing-sets"></a>Dividir os dados de exemplo em treinamento e conjuntos de teste

1. Você pode usar o procedimento armazenado **TrainTestSplit** para dividir os dados a nyctaxi\_tabela de exemplo em duas partes: nyctaxi\_exemplo\_treinamento e nyctaxi\_deexemplo\_testes. 

    Esse procedimento armazenado já deve ser criado para você, mas você pode executar o código a seguir para criá-la:

    ```SQL
    CREATE PROCEDURE [dbo].[TrainTestSplit] (@pct int)
    AS
    
    DROP TABLE IF EXISTS dbo.nyctaxi_sample_training
    SELECT * into nyctaxi_sample_training FROM nyctaxi_sample WHERE (ABS(CAST(BINARY_CHECKSUM(medallion,hack_license)  as int)) % 100) < @pct
    
    DROP TABLE IF EXISTS dbo.nyctaxi_sample_testing
    SELECT * into nyctaxi_sample_testing FROM nyctaxi_sample
    WHERE (ABS(CAST(BINARY_CHECKSUM(medallion,hack_license)  as int)) % 100) > @pct
    GO
    ```

2. Para dividir os dados usando uma divisão personalizada, execute o procedimento armazenado e digite um inteiro que representa a porcentagem de dados alocadas para o conjunto de treinamento. Por exemplo, a instrução a seguir alocará 60% dos dados para o conjunto de treinamento.

    ```SQL
    EXEC TrainTestSplit 60
    GO
    ```

## <a name="build-a-logistic-regression-model"></a>Criar um modelo de regressão logística

Depois que os dados preparados, você pode usá-lo para treinar um modelo. Você pode fazer isso chamando um armazenado entrada de procedimento que seja executado algum código Python, tirando como a tabela de dados de treinamento. Para este tutorial, você pode criar dois modelos, os dois modelos de classificação binária:

+ O procedimento armazenado **TrainTipPredictionModelRxPy** cria um modelo de previsão de dica usando o **revoscalepy** pacote.
+ O procedimento armazenado **TrainTipPredictionModelSciKitPy** cria um modelo de previsão de dica usando o **scikit-Saiba** pacote.

Cada procedimento armazenado usa os dados de entrada é fornecer para criar e treinar um modelo de regressão logística. Todo o código Python é encapsulado em um procedimento armazenado do sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

Para tornar mais fácil treinar novamente o modelo em dados novos, encapsule a chamada para sp_execute_exernal_script em outro procedimento armazenado e passar os novos dados de treinamento como um parâmetro. Esta seção o orientará durante esse processo.

### <a name="traintippredictionmodelscikitpy"></a>TrainTipPredictionModelSciKitPy

1.  Em [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra uma nova **consulta** janela e execute a seguinte instrução para criar o procedimento armazenado _TrainTipPredictionModelSciKitPy_.  O procedimento armazenado contém uma definição dos dados de entrada, portanto você não precisa fornecer uma consulta de entrada.

    ```SQL
    DROP PROCEDURE IF EXISTS TrainTipPredictionModelSciKitPy;
    GO

    CREATE PROCEDURE [dbo].[TrainTipPredictionModelSciKitPy] (@trained_model varbinary(max) OUTPUT)
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

2. Execute os seguintes instruções SQL para inserir o modelo treinado em tabela nyc\_taxi_models.

    ```SQL
    DECLARE @model VARBINARY(MAX);
    EXEC TrainTipPredictionModelSciKitPy @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('SciKit_model', @model);
    ```

    Processamento de dados e ajustar o modelo podem demorar alguns minutos. As mensagens que poderiam ser canalizadas do Python **stdout** fluxo são exibidos no **mensagens** janela de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Por exemplo:

    *Mensagem (NS) STDOUT do script externo:*
  *C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\lib\site packages\revoscalepy*

3. Abra a tabela *nyc\_taxi_models*. Você pode ver que uma nova linha foi adicionada, que contém o modelo serializado na coluna _modelo_.

    *linear_model* *0x800363736B6C6561726E2E6C696E6561....*

### <a name="traintippredictionmodelrxpy"></a>TrainTipPredictionModelRxPy

Esse procedimento armazenado usa o novo **revoscalepy** pacote, que é um novo pacote da Python. Ele contém objetos, transformação e algoritmos semelhantes àqueles fornecidos para a linguagem de R **RevoScaleR** pacote. 

Usando **revoscalepy**, você pode criar contextos de computação remota, computação de mover dados entre contextos, transformar dados e treinar modelos de previsão usando algoritmos populares, como a regressão logística e linear, árvores de decisão, e mais. Para obter mais informações, consulte [novidades revoscalepy?](../python/what-is-revoscalepy.md)

1. Em [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra uma nova **consulta** janela e execute a seguinte instrução para criar o procedimento armazenado _TrainTipPredictionModelRxPy_.  Como o procedimento armazenado já inclui uma definição dos dados de entrada, você não precisa fornecer uma consulta de entrada.

    ```SQL
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

    - A consulta SELECT aplica-se a função escalar personalizada _fnCalculateDistance_ para calcular a distância direta entre os locais de coleta e entrega. Os resultados da consulta são armazenados na variável de entrada do Python do padrão, `InputDataset`.
    - A variável binária _Oblíquo_ é usado como o *rótulo* ou coluna de resultado e o modelo é ajustar usando estas colunas de recurso: _passenger_count_, _trip_ distância_, _trip_time_in_secs_, e _direct_distance_.
    - O modelo treinado é serializado e armazenado na variável Python `logitObj`. Adicionando a palavra-chave T-SQL OUTPUT, você pode adicionar a variável como uma saída do procedimento armazenado. Na próxima etapa, essa variável é usada para inserir o código binário do modelo em uma tabela de banco de dados _nyc_taxi_models_. Esse mecanismo torna fácil armazenar e reutilizar modelos.

2. Execute o procedimento armazenado da seguinte maneira para inserir o treinado **revoscalepy** modelo para a tabela _nyc\_táxi\_modelos.

    ```SQL
    DECLARE @model VARBINARY(MAX);
    EXEC TrainTipPredictionModelRxPy @model OUTPUT;
    
    INSERT INTO nyc_taxi_models (name, model) VALUES('revoscalepy_model', @model);
    ```

    Processamento de dados e ajustar o modelo podem demorar um pouco. As mensagens que poderiam ser canalizadas do Python **stdout** fluxo são exibidos no **mensagens** janela de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Por exemplo:

    *Mensagem (NS) STDOUT do script externo:*
  *C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\lib\site packages\revoscalepy*

3. Abra a tabela *nyc_taxi_models*. Você pode ver que uma nova linha foi adicionada, que contém o modelo serializado na coluna _modelo_.

    *rx_model* *0x8003637265766F7363616c....*

Na próxima etapa, você pode usar os modelos treinados para criar previsões.

## <a name="next-step"></a>Próxima etapa

[Etapa 6: Colocar o modelo de Python usando o SQL Server](sqldev-py6-operationalize-the-model.md)

## <a name="previous-step"></a>Etapa anterior

[Etapa 4: Criar recursos de dados usando o T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)
