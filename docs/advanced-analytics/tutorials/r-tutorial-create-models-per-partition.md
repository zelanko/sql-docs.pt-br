---
title: Tutorial sobre como criar, treinar e pontuar modelos baseados em partição em R
description: Saiba como modelar, treinar e usar dados particionados que são criados dinamicamente ao usar os recursos de modelagem baseados em partição de SQL Server Machine Learning.
ms.custom: sqlseattle
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/27/2019
ms.topic: tutorial
ms.author: davidph
author: dphansen
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3395b237e08a10033819eeed74057cc7319d7f11
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952018"
---
# <a name="tutorial-create-partition-based-models-in-r-on-sql-server"></a>Tutorial: Criar modelos baseados em partição no R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

No SQL Server 2019, a modelagem baseada em partição é a capacidade de criar e treinar modelos em dados particionados. Para dados de sobreratificação que os segmentos naturalmente em um determinado esquema de classificação, como regiões geográficas, data e hora, idade ou sexo, você pode executar um script em todo o conjunto de dados, com a capacidade de modelar, treinar e pontuar as partições que permanecem intactas em todas essas operações. 

A modelagem baseada em partição é habilitada por meio de dois novos parâmetros no [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql):

+ **input_data_1_partition_by_columns**, que especifica uma coluna pela qual particionar.
+ **input_data_1_order_by_columns** especifica em quais colunas ordenar. 

Neste tutorial, aprenda a modelagem baseada em partição usando os dados de exemplo clássicos NYC táxi e o script R. A coluna de partição é o método de pagamento.

> [!div class="checklist"]
> * As partições são baseadas em tipos de pagamento (5).
> * Crie e treine modelos em cada partição e armazene os objetos no banco de dados.
> * Prever a probabilidade de resultados de gorjeta em cada modelo de partição, usando dados de exemplo reservados para essa finalidade.

## <a name="prerequisites"></a>Pré-requisitos
 
Para concluir este tutorial, você deve ter o seguinte:

+ Recursos do sistema suficientes. O conjunto de dados é grande e as operações de treinamento têm uso intensivo de recursos. Se possível, use um sistema com pelo menos 8 GB de RAM. Como alternativa, você pode usar conjuntos de dados menores para contornar as restrições de recursos. As instruções para reduzir o conjunto de dados são embutidas. 

+ Uma ferramenta para a execução da consulta T-SQL, como [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

+ [NYCTaxi_Sample. bak](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak), que você pode [baixar e restaurar](demo-data-nyctaxi-in-sql.md) para sua instância do mecanismo de banco de dados local. O tamanho do arquivo é de aproximadamente 90 MB.

+ SQL Server instância do mecanismo de banco de dados 2019 Preview, com integração de Serviços de Machine Learning e R.

Verifique a versão executando **`SELECT @@Version`** como uma consulta T-SQL em uma ferramenta de consulta. A saída deve ser "Microsoft SQL Server 2019 (CTP 2,4)-15.0. x".

Verifique a disponibilidade dos pacotes do R retornando uma lista bem formatada de todos os pacotes do R instalados atualmente com a instância do mecanismo de banco de dados:

```sql
EXECUTE sp_execute_external_script
  @language=N'R',
  @script = N'str(OutputDataSet);
  packagematrix <- installed.packages();
  Name <- packagematrix[,1];
  Version <- packagematrix[,3];
  OutputDataSet <- data.frame(Name, Version);',
  @input_data_1 = N''
WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
```

## <a name="connect-to-the-database"></a>Conectar-se ao banco de dados

Inicie Management Studio e conecte-se à instância do mecanismo de banco de dados. No Pesquisador de objetos, verifique se o [banco de dados NYCTaxi_Sample](demo-data-nyctaxi-in-sql.md) existe. 

## <a name="create-calculatedistance"></a>Criar CalculateDistance

O banco de dados de demonstração vem com uma função escalar para calcular a distância, mas nosso procedimento armazenado funciona melhor com uma função com valor de tabela. Execute o script a seguir para criar a função **CalculateDistance** usada na [etapa de treinamento](#training-step) posteriormente.

Para confirmar se a função foi criada, verifique as funções \Programmability\Functions\Table-valued no banco de dados **NYCTaxi_Sample** no Pesquisador de objetos.

```sql
USE NYCTaxi_sample
GO

SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [dbo].[CalculateDistance] (
    @Lat1 FLOAT
    ,@Long1 FLOAT
    ,@Lat2 FLOAT
    ,@Long2 FLOAT
    )
    -- User-defined function calculates the direct distance between two geographical coordinates.
RETURNS TABLE
AS
RETURN

SELECT COALESCE(3958.75 * ATAN(SQRT(1 - POWER(t.distance, 2)) / nullif(t.distance, 0)), 0) AS direct_distance
FROM (
    VALUES (CAST((SIN(@Lat1 / 57.2958) * SIN(@Lat2 / 57.2958)) + (COS(@Lat1 / 57.2958) * COS(@Lat2 / 57.2958) * COS((@Long2 / 57.2958) - (@Long1 / 57.2958))) AS DECIMAL(28, 10)))
    ) AS t(distance)
GO
 ```

## <a name="define-a-procedure-for-creating-and-training-per-partition-models"></a>Definir um procedimento para criar e treinar modelos por partição

Este tutorial encapsula o script R em um procedimento armazenado. Nesta etapa, você cria um procedimento armazenado que usa R para criar um conjunto de dados de entrada, criar um modelo de classificação para prever resultados de gorjeta e, em seguida, armazenar o modelo no banco de dados.

Entre as entradas de parâmetro usadas por esse script, você verá **input_data_1_partition_by_columns** e **input_data_1_order_by_columns**. Lembre-se de que esses parâmetros são o mecanismo pelo qual a modelagem particionada ocorre. Os parâmetros são passados como entradas para [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) para processar partições com o script externo executado uma vez para cada partição. 

Para esse procedimento armazenado, [use o paralelismo](#parallel) para ter um tempo de conclusão mais rápido.

Depois de executar esse script, você deverá ver **train_rxLogIt_per_partition** nos procedimentos do \Programmability\Stored no banco de dados **NYCTaxi_Sample** no Pesquisador de objetos. Você também deve ver uma nova tabela usada para armazenar modelos: **dbo. nyctaxi_models**.

```sql
USE NYCTaxi_Sample
GO

CREATE
    OR

ALTER PROCEDURE [dbo].[train_rxLogIt_per_partition] (@input_query NVARCHAR(max))
AS
BEGIN
    DECLARE @start DATETIME2 = SYSDATETIME()
        ,@model_generation_duration FLOAT
        ,@model VARBINARY(max)
        ,@instance_name NVARCHAR(100) = @@SERVERNAME
        ,@database_name NVARCHAR(128) = db_name();

    EXEC sp_execute_external_script @language = N'R'
        ,@script = 
        N'
    
    # Make sure InputDataSet is not empty. In parallel mode, if one thread gets zero data, an error occurs
    if (nrow(InputDataSet) > 0) {
    # Define the connection string
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    
    # build classification model to predict a tip outcome
    duration <- system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = InputDataSet))[3];

    # First, serialize a model to and put it into a database table
    modelbin <- as.raw(serialize(logitObj, NULL));

    # Create the data source. To reduce data size, add rowsPerRead=500000 to cut the dataset by half.
    ds <- RxOdbcData(table="ml_models", connectionString=connStr);

    # Store the model in the database
    model_name <- paste0("nyctaxi.", InputDataSet[1,]$payment_type);
    
    rxWriteObject(ds, model_name, modelbin, version = "v1",
    keyName = "model_name", valueName = "model_object", versionName = "model_version", overwrite = TRUE, serialize = FALSE);
    } 
    
    '
        ,@input_data_1 = @input_query
        ,@input_data_1_partition_by_columns = N'payment_type'
        ,@input_data_1_order_by_columns = N'passenger_count'
        ,@parallel = 1
        ,@params = N'@instance_name nvarchar(100), @database_name nvarchar(128)'
        ,@instance_name = @instance_name
        ,@database_name = @database_name
    WITH RESULT SETS NONE
END;
GO
```

<a name="parallel"></a>

### <a name="parallel-execution"></a>Execução paralela

Observe que as entradas [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) incluem `@parallel=1`, usadas para habilitar o processamento paralelo. Em contraste com as versões anteriores, no SQL Server 2019, a configuração de `@parallel=1` fornece uma dica mais forte ao otimizador de consulta, tornando a execução paralela um resultado muito mais provável.

Por padrão, o otimizador de consulta tende a operar em `@parallel=1` em tabelas com mais de 256 linhas, mas se você puder tratar isso explicitamente definindo `@parallel=1`, conforme mostrado neste script.

> [!Tip]
> Para treinar o workoads, você pode usar `@parallel` com qualquer script de treinamento arbitrário, mesmo aqueles que usam algoritmos não Microsoft-RX. Normalmente, somente os algoritmos RevoScaleR (com o prefixo RX) oferecem paralelismo em cenários de treinamento no SQL Server. Mas com o novo parâmetro, você pode paralelizar um script que chama funções, incluindo funções de R de software livre, não especificamente projetada com esse recurso. Isso funciona porque as partições têm afinidade com threads específicos, portanto, todas as operações chamadas em um script são executadas em uma base por partição, em atribuir @ no__t-0<a name="training-step"></a>

## <a name="run-the-procedure-and-train-the-model"></a>Executar o procedimento e treinar o modelo

Nesta seção, o script treina o modelo que você criou e salvou na etapa anterior. Os exemplos a seguir demonstram duas abordagens para treinar seu modelo: usando um conjunto de dados inteiro ou dados parciais. 

Espere que essa etapa demore algum tempo. O treinamento é computacionalmente intensivo, levando vários minutos para ser concluído. Se os recursos do sistema, especialmente a memória, forem insuficientes para a carga, use um subconjunto dos dados. O segundo exemplo fornece a sintaxe.

```sql
--Example 1: train on entire dataset
EXEC train_rxLogIt_per_partition N'
SELECT payment_type, tipped, passenger_count, trip_time_in_secs, trip_distance, d.direct_distance
  FROM dbo.nyctaxi_sample CROSS APPLY [CalculateDistance](pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as d
';
GO
```

```sql
--Example 2: Train on 20 percent of the dataset to expedite processing.
EXEC train_rxLogIt_per_partition N'
  SELECT tipped, payment_type, passenger_count, trip_time_in_secs, trip_distance, d.direct_distance
  FROM dbo.nyctaxi_sample TABLESAMPLE (20 PERCENT) REPEATABLE (98074)
  CROSS APPLY [CalculateDistance](pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as d
';
GO
```

> [!NOTE]
> Se você estiver executando outras cargas de trabalho, poderá acrescentar `OPTION(MAXDOP 2)` à instrução SELECT se quiser limitar o processamento de consulta a apenas 2 núcleos.

## <a name="check-results"></a>Verificar resultados

O resultado na tabela de modelos deve ser cinco modelos diferentes, com base em cinco partições segmentadas pelos cinco tipos de pagamento. Os modelos estão na fonte de dados **ml_models** .

```sql
SELECT *
FROM ml_models
```
 
## <a name="define-a-procedure-for-predicting-outcomes"></a>Definir um procedimento para prever resultados

Você pode usar os mesmos parâmetros para pontuação. O exemplo a seguir contém um script R que resultará no uso do modelo correto para a partição que está processando no momento.

Como antes, crie um procedimento armazenado para encapsular o código R.

```sql
USE NYCTaxi_Sample
GO

-- Stored procedure that scores per partition. 
-- Depending on the partition being processed, a model specific to that partition will be used
CREATE
    OR

ALTER PROCEDURE [dbo].[predict_per_partition]
AS
BEGIN
    DECLARE @predict_duration FLOAT
        ,@instance_name NVARCHAR(100) = @@SERVERNAME
        ,@database_name NVARCHAR(128) = db_name()
        ,@input_query NVARCHAR(max);

    SET @input_query = 'SELECT tipped, passenger_count, trip_time_in_secs, trip_distance, d.direct_distance, payment_type
                          FROM dbo.nyctaxi_sample TABLESAMPLE (1 PERCENT) REPEATABLE (98074)
                          CROSS APPLY [CalculateDistance](pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as d'

    EXEC sp_execute_external_script @language = N'R'
        ,@script = 
        N'
    
    if (nrow(InputDataSet) > 0) {

    #Get the partition that is currently being processed
    current_partition <- InputDataSet[1,]$payment_type;

    #Create the SQL query to select the right model
    query_getModel <- paste0("select model_object from ml_models where model_name = ", "''", "nyctaxi.",InputDataSet[1,]$payment_type,"''", ";")
    

    # Define the connection string
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
        
    #Define data source to use for getting the model
    ds <- RxOdbcData(sqlQuery = query_getModel, connectionString = connStr)

    # Load the model
    modelbin <- rxReadObject(ds, deserialize = FALSE)
    # unserialize model
    logitObj <- unserialize(modelbin);

    # predict tipped or not based on model
    predictions <- rxPredict(logitObj, data = InputDataSet, overwrite = TRUE, type = "response", writeModelVars = TRUE
        , extraVarsToWrite = c("payment_type"));        
    OutputDataSet <- predictions
    
    } else {
        OutputDataSet <- data.frame(integer(), InputDataSet[,]);        
    }
    '
        ,@input_data_1 = @input_query
        ,@parallel = 1
        ,@input_data_1_partition_by_columns = N'payment_type'
        ,@params = N'@instance_name nvarchar(100), @database_name nvarchar(128)'
        ,@instance_name = @instance_name
        ,@database_name = @database_name
    WITH RESULT SETS((
                tipped_Pred INT
                ,payment_type VARCHAR(5)
                ,tipped INT
                ,passenger_count INT
                ,trip_distance FLOAT
                ,trip_time_in_secs INT
                ,direct_distance FLOAT
                ));
END;
GO
```

## <a name="create-a-table-to-store-predictions"></a>Criar uma tabela para armazenar previsões

```sql
CREATE TABLE prediction_results (
    tipped_Pred INT
    ,payment_type VARCHAR(5)
    ,tipped INT
    ,passenger_count INT
    ,trip_distance FLOAT
    ,trip_time_in_secs INT
    ,direct_distance FLOAT
    );

TRUNCATE TABLE prediction_results
GO
```

## <a name="run-the-procedure-and-save-predictions"></a>Executar o procedimento e salvar previsões

```sql
INSERT INTO prediction_results (
    tipped_Pred
    ,payment_type
    ,tipped
    ,passenger_count
    ,trip_distance
    ,trip_time_in_secs
    ,direct_distance
    )
EXECUTE [predict_per_partition]
GO
```

## <a name="view-predictions"></a>Exibir previsões

Como as previsões são armazenadas, você pode executar uma consulta simples para retornar um conjunto de resultados.

```sql
SELECT *
FROM prediction_results;
```

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você usou [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) para iterar operações em dados particionados. Para uma análise mais detalhada de como chamar scripts externos em procedimentos armazenados e usar o RevoScaleR functions, continue com o tutorial a seguir.

> [!div class="nextstepaction"]
> [Walkthrough para R e SQL Server](walkthrough-data-science-end-to-end-walkthrough.md)

<!--
## Old intro

**(Not for production workloads)**

One of the more common approaches for executing R or Python code on SQL data is providing script as an input parameter to the [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) stored procedure. In this CTP release, SQL Server 2019 adds new parameters to `sp_execute_external_script` to process partitions with the external script executing once for every partition:

| Parameter | Usage |
|-----------|-------|
| **input_data_1_partition_by_columns** | Specifies which columns to partition by. |
| **input_data_1_order_by_columns** | Specifies which columns to order by.  |

Partitions are an organizational mechanism for stratified data that naturally segments into a given classification scheme. Common examples include partitioning by geographic region, by date and time, by age or gender, and so forth. Given the existence of partitioned data, you might want to execute script over the entire data set, with the ability to model, train, and score partitions that remain intact over all these operations. Calling `sp_execute_external_script` with the new parameters allows you to do just that.

You can run this operation in parallel by combining `partition_by` with `@parallel`. If the input query can be parallelized, set `@parallel=1` as part of your arguments to `sp_execute_external_script`. By default, the query optimizer operates under `@parallel=1` on tables having more than 256 rows.

When the scenario is training, one advantage is that any arbitrary training script, even those using non-Microsoft-rx algorithms, can be parallelized by also using the @parallel parameter. Typically, you would have to use RevoScaleR algorithms (with the rx prefix) to obtain parallelism in training scenarios in SQL Server. But with the new parameter, you can parallelize a script that calls functions not specifically engineered with that capability.
-->
