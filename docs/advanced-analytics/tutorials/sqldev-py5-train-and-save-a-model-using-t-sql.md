---
title: 'Etapa 5: Treinar e salvar um modelo usando o T-SQL | Microsoft Docs'
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- python-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 80a47819dfbb2e96162a49730e0dcf0b1b340f07
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="step-5-train-and-save-a-model-using-t-sql"></a>Etapa 5: Treinar e salvar um modelo usando o T-SQL

Nesta etapa, você aprenderá a treinar um modelo de aprendizado de máquina usando os pacotes do Python **scikit-Saiba** e **revoscalepy**. Essas bibliotecas Python já estão instaladas com os serviços de aprendizado de máquina do SQL Server, você pode carregar os módulos e chamar as funções necessárias de dentro de um procedimento armazenado. Você treinará o modelo usando os recursos de dados que acabou de criar e salvará o modelo treinado em uma tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

## <a name="split-the-sample-data-into-training-and-testing-sets"></a>Dividir os dados de exemplo em treinamento e conjuntos de teste

1. Execute os seguintes comandos T-SQL para criar um procedimento armazenado que divide os dados a nyctaxi\_tabela de exemplo em duas partes: nyctaxi\_exemplo\_treinamento e nyctaxi\_exemplo\_teste.

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

2. Execute o procedimento armazenado e digite um inteiro que representa a porcentagem de dados alocadas para o conjunto de treinamento. Por exemplo, a instrução a seguir alocará 60% dos dados para o conjunto de treinamento. Dados de teste e treinamento são armazenados em duas tabelas separadas.

    ```SQL
    EXEC TrainTestSplit 60
    GO
    ```

## <a name="build-a-logistic-regression-model-using-scikit-learn"></a>Criar um modelo de regressão logística usando scikit-Saiba mais

Nesta seção, você deve criar um procedimento armazenado que pode ser usado para treinar um modelo usando dados de treinamento que você preparou. Esse procedimento armazenado define os dados de entrada e usa um **scikit-Saiba** função para treinar um modelo de regressão logística. Chame o tempo de execução do Python que é instalado com o SQL Server usando o procedimento armazenado do sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

Para tornar mais fácil treinar novamente o modelo, você pode encapsulam a chamada para sp_execute_exernal_script em outro procedimento armazenado e passar os novos dados de treinamento como um parâmetro. Esta seção o orientará durante esse processo.

1.  Em [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra uma nova **consulta** janela e execute a seguinte instrução para criar o procedimento armazenado _TrainTipPredictionModelSciKitPy_.  Observe que o procedimento armazenado contém uma definição dos dados de entrada, portanto você não precisa fornecer uma consulta de entrada.

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
      import pandas
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

    *linear_model* *0x800363736B6C6561726E2E6C696E6561...*

## <a name="build-a-logistic-model-using-the-revoscalepy-package"></a>Criar um modelo de logística usando o _revoscalepy_ pacote

Agora, crie um procedimento armazenado diferente que usa o novo **revoscalepy** pacote para treinar um modelo de regressão logística. O **revoscalepy** para Python contém algoritmos semelhantes àqueles fornecidos para a linguagem de R, transformação e objetos de pacote **RevoScaleR** pacote. Com essa biblioteca, você pode criar um contexto de computação, mover dados entre contextos de computação, transformam dados e treinar modelos de previsão usando algoritmos populares, como a regressão logística e linear, árvores de decisão e muito mais. Para obter mais informações, consulte [novidades revoscalepy?](../python/what-is-revoscalepy.md)

1. Em [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra uma nova **consulta** janela e execute a seguinte instrução para criar o procedimento armazenado _TrainTipPredictionModelRxPy_.  Esse modelo também usa os dados de treinamento que você preparou. Como o procedimento armazenado já inclui uma definição dos dados de entrada, você não precisa fornecer uma consulta de entrada.

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
    import pandas
    from revoscalepy.functions.RxLogit import rx_logit_ex
    
    ## Create a logistic regression model using rx_logit_ex function from revoscalepy package
    logitObj = rx_logit_ex("tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance", data = InputDataSet);
    
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

    - Treinar um modelo de regressão logística usando o pacote de revoscalepy nyctaxi\_exemplo\_dados de treinamento.
    - A consulta SELECT usa a função escalar personalizada _fnCalculateDistance_ para calcular a distância direta entre os locais de embarque e desembarque de passageiros. Os resultados da consulta são armazenados na variável de entrada do Python do padrão, `InputDataset`.
    - O script de Python chama a função de LogisticRegression do revoscalepy, que está incluída no [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], para criar o modelo de regressão logística.
    - A variável binária _tipped_ é usada como a coluna *label* ou de resultado, e o modelo é ajustado com o uso destas colunas de recursos:  _passenger_count_, _trip_distance_, _trip_time_in_secs_e _direct_distance_.
    - O modelo treinado, contido na variável Python `logitObj`, é serializado e colocá-lo como um parâmetro de saída [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Que a saída é inserida na tabela de banco de dados _nyc_taxi_models_, juntamente com seu nome, como uma nova linha, para que você possa recuperar e usá-lo para previsões futuras.

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

    *rx_model* *0x8003637265766F7363616c...*

Na próxima etapa, você pode usar os modelos treinados para criar previsões.

## <a name="next-step"></a>Próxima etapa

[Etapa 6: Colocar o modelo](sqldev-py6-operationalize-the-model.md)

## <a name="previous-step"></a>Etapa anterior

[Etapa 4: Criar recursos de dados usando o T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

