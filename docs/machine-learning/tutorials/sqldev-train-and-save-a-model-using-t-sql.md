---
title: 'Tutorial de R + T-SQL: Treinar um modelo'
description: Tutorial mostrando como treinar, serializar e salvar um modelo do R usando procedimentos armazenados do SQL Server e funções do T-SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/16/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 406f8e1c60c5820f9edaaf7760b7aeed321d2611
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2020
ms.locfileid: "81115779"
---
# <a name="lesson-3-train-and-save-a-model-using-t-sql"></a>Lição 3: Treinar e salvar um modelo usando o T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo faz parte de um tutorial para desenvolvedores de SQL sobre como usar o R no SQL Server.

Nesta lição, você aprenderá a treinar um modelo de machine learning usando o R. Você treinará o modelo usando os recursos de dados criados na lição anterior e, em seguida, salvará o modelo treinado em uma tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Neste caso, os pacotes do R já estão instalados com o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], portanto, tudo pode ser feito do SQL.

## <a name="create-the-stored-procedure"></a>Criar o procedimento armazenado

Ao chamar o R do T-SQL, você usa o procedimento armazenado do sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). No entanto, para processos que você repete com frequência, como treinar novamente um modelo, é mais fácil encapsular a chamada para sp_execute_exernal_script em outro procedimento armazenado.

1. No [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra uma nova janela de **Consulta**.

2. Execute a instrução a seguir para criar o procedimento armazenado **RxTrainLogitModel**. Esse procedimento armazenado define os dados de entrada e usa o **rxLogit** do RevoScaleR para criar um modelo de regressão logística.

    ```sql
    CREATE PROCEDURE [dbo].[RxTrainLogitModel] (@trained_model varbinary(max) OUTPUT)
    
    AS
    BEGIN
      DECLARE @inquery nvarchar(max) = N'
        select tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance,
        pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
        from nyctaxi_sample
        tablesample (70 percent) repeatable (98052)
    '
    
      EXEC sp_execute_external_script @language = N'R',
                                      @script = N'
    ## Create model
    logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = InputDataSet)
    summary(logitObj)
    
    ## Serialize model 
    trained_model <- as.raw(serialize(logitObj, NULL));
    ',
      @input_data_1 = @inquery,
      @params = N'@trained_model varbinary(max) OUTPUT',
      @trained_model = @trained_model OUTPUT; 
    END
    GO
    ```

    - Para garantir que há alguns dados para testar o modelo, 70% dos dados são selecionados aleatoriamente da tabela de dados de táxi para fins de treinamento.

    - A consulta SELECT usa a função escalar personalizada *fnCalculateDistance* para calcular a distância direta entre os locais de embarque e desembarque de passageiros. Os resultados da consulta são armazenados na variável de entrada padrão do R, `InputDataset`.
  
    - O script do R chama a função **rxLogit**, que é uma das funções avançadas do R incluídas no [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], para criar o modelo de regressão logística.
  
        A variável binária _tipped_ é usada como a coluna *label* ou de resultado, e o modelo é ajustado com o uso destas colunas de recursos:  _passenger_count_, _trip_distance_, _trip_time_in_secs_e _direct_distance_.
  
    - O modelo treinado, salvo no `logitObj` da variável do R, é serializado e retornado como um parâmetro de saída.

## <a name="train-and-deploy-the-r-model-using-the-stored-procedure"></a>Treinar e implantar o modelo do R usando o procedimento armazenado

Como o procedimento armazenado já inclui uma definição dos dados de entrada, você não precisa fornecer uma consulta de entrada.

1. Para treinar e implantar o modelo do R, chame o procedimento armazenado e insira-o na tabela de banco de dados _nyc_taxi_models_ para que você possa usá-lo para previsões futuras:

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC RxTrainLogitModel @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('RxTrainLogit_model', @model);
    ```

2. Assista à janela **Mensagens** de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para mensagens que seriam canalizadas para o fluxo **stdout** do R, como esta mensagem: 

    "Mensagem(ns) STDOUT do script externo: Linhas lidas: 1193025, Total de Linhas Processadas: 1193025, Tempo Total da Parte: 0,093 segundos"

    Você também pode ver mensagens específicas para a função individual, `rxLogit`, exibindo as variáveis e as métricas de teste geradas como parte da criação do modelo.

3.  Quando a instrução tiver sido concluída, abra a tabela *nyc_taxi_models*. O processamento dos dados e o ajuste do modelo poderão levar algum tempo.

    Você pode ver que foi adicionada uma nova linha contendo o modelo serializado na coluna _modelo_ e o nome do modelo **RxTrainLogit_model** na coluna _nome_.

    ```sql
    model                        name
    ---------------------------- ------------------
    0x580A00000002000302020....  RxTrainLogit_model
    ```

Na próxima etapa, você usará o modelo treinado para gerar previsões.

## <a name="next-lesson"></a>Próxima lição

[Lição 4: Prever os resultados potenciais usando um modelo do R em um procedimento armazenado](../tutorials/sqldev-operationalize-the-model.md)

## <a name="previous-lesson"></a>Lição anterior

[Lição 2: Criar recursos de dados usando funções do R e T-SQL](..//tutorials/sqldev-create-data-features-using-t-sql.md)

