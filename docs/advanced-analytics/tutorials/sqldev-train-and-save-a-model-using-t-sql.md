---
title: Lição 3 treinar e salvar um modelo usando R e T-SQL – SQL Server Machine Learning
description: Tutorial que mostra como treinar, serializar e salvar um modelo do R usando o SQL Server procedimentos armazenados e funções T-SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/16/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: f3abe58aac4d5920e64337f63a40dc8f87fb12d9
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645105"
---
# <a name="lesson-3-train-and-save-a-model-using-t-sql"></a>Lição 3: Treinar e salvar um modelo usando o T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo faz parte de um tutorial para desenvolvedores SQL sobre como usar o R no SQL Server.

Nesta lição, você aprenderá a treinar um modelo de aprendizado de máquina usando o R. Você vai treinar o modelo usando os recursos de dados que você criou na lição anterior e, em seguida, salve o modelo treinado em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela. Nesse caso, os pacotes do R já estão instalados no [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], portanto, tudo o que pode ser feito do SQL.

## <a name="create-the-stored-procedure"></a>Criar o procedimento armazenado

Ao chamar o R de T-SQL, você use o procedimento armazenado do sistema [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). No entanto, para processos que você repetir muitas vezes, como a readaptação de um modelo, é mais fácil encapsular a chamada para sp_execute_exernal_script em outro procedimento armazenado.

1. Na [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra uma nova **consulta** janela.

2. Execute a seguinte instrução para criar o procedimento armazenado **RxTrainLogitModel**. Esse procedimento armazenado define os dados de entrada e usa **rxLogit** do RevoScaleR para criar um modelo de regressão logística.

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

    - Para garantir que alguns dados é restantes para testar o modelo, 70% dos dados são selecionados aleatoriamente da tabela de dados de táxi para fins de treinamento.

    - A consulta SELECT usa a função escalar personalizada *fnCalculateDistance* para calcular a distância direta entre os locais de embarque e desembarque de passageiros. os resultados da consulta são armazenados na variável de entrada padrão do R, `InputDataset`.
  
    - O script do R chama o **rxLogit** função, que é uma das funções avançadas do R incluídas com [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], para criar o modelo de regressão logística.
  
        A variável binária _tipped_ é usada como a coluna *label* ou de resultado, e o modelo é ajustado com o uso destas colunas de recursos:  _passenger_count_, _trip_distance_, _trip_time_in_secs_e _direct_distance_.
  
    - O modelo treinado, salvo na variável do R `logitObj`, é serializado e retornado como um parâmetro de saída.

## <a name="train-and-deploy-the-r-model-using-the-stored-procedure"></a>Treinar e implantar o modelo do R usando o procedimento armazenado

Como o procedimento armazenado já inclui uma definição dos dados de entrada, você não precisa fornecer uma consulta de entrada.

1. Para treinar e implantar o modelo do R, chame o procedimento armazenado e inseri-lo para a tabela de banco de dados _nyc_taxi_models_, de modo que você pode usá-lo para previsões futuras:

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC RxTrainLogitModel @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('RxTrainLogit_model', @model);
    ```

2. Assista a **mensagens** janela do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para mensagens que serão redirecionadas para do R **stdout** fluxo, como esta mensagem: 

    "Mensagem (NS) STDOUT do script externo: Linhas lidas: 1193025, total de linhas processadas: 1193025, total tempo: 0.093 segundos"

    Você também poderá ver mensagens específicas de função individual, `rxLogit`, exibindo as variáveis e métricas geradas como parte da criação do modelo de teste.

3.  Quando a instrução for concluída, abra a tabela *nyc_taxi_models*. Processamento de dados e ajuste do modelo podem levar algum tempo.

    Você pode ver que uma nova linha tiver sido adicionada, que contém o modelo serializado na coluna _modelo_ e o nome do modelo **RxTrainLogit_model** na coluna _nome_.

    ```sql
    model                        name
    ---------------------------- ------------------
    0x580A00000002000302020....  RxTrainLogit_model
    ```

A próxima etapa, você usará o modelo treinado para gerar previsões.

## <a name="next-lesson"></a>Próxima lição

[Lição 4: Prever resultados possíveis, usando um modelo do R em um procedimento armazenado](../tutorials/sqldev-operationalize-the-model.md)

## <a name="previous-lesson"></a>Lição anterior

[Lição 2: Criar recursos de dados usando funções de R e T-SQL](..//tutorials/sqldev-create-data-features-using-t-sql.md)

