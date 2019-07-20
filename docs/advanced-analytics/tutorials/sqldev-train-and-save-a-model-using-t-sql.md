---
title: Lição 3 treinar e salvar um modelo usando R e T-SQL
description: Tutorial mostrando como treinar, serializar e salvar um modelo R usando SQL Server procedimentos armazenados e funções do T-SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/16/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 0d26f549bcca4860f4febe01a868f360edfa4fa2
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345864"
---
# <a name="lesson-3-train-and-save-a-model-using-t-sql"></a>Lição 3: Treinar e salvar um modelo usando o T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo faz parte de um tutorial para desenvolvedores de SQL sobre como usar o R no SQL Server.

Nesta lição, você aprenderá a treinar um modelo de aprendizado de máquina usando o R. Você treinará o modelo usando os recursos de dados criados na lição anterior e, em seguida, salvará o modelo treinado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma tabela. Nesse caso, os pacotes do R já estão instalados com [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]o, portanto, tudo pode ser feito do SQL.

## <a name="create-the-stored-procedure"></a>Criar o procedimento armazenado

Ao chamar R do T-SQL, você usa o procedimento armazenado do sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). No entanto, para processos que você repete com frequência, como treinar novamente um modelo, é mais fácil encapsular a chamada para sp_execute_exernal_script em outro procedimento armazenado.

1. No [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra uma nova janela de **consulta** .

2. Execute a instrução a seguir para criar o procedimento armazenado **RxTrainLogitModel**. Esse procedimento armazenado define os dados de entrada e usa **rxLogit** de RevoScaleR para criar um modelo de regressão logística.

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

    - Para garantir que alguns dados sejam deixados para testar o modelo, 70% dos dados são selecionados aleatoriamente da tabela de dados de táxi para fins de treinamento.

    - A consulta SELECT usa a função escalar personalizada *fnCalculateDistance* para calcular a distância direta entre os locais de embarque e desembarque de passageiros. Os resultados da consulta são armazenados na variável de entrada padrão do R, `InputDataset`.
  
    - O script R chama a função **rxLogit** , que é uma das funções avançadas do R incluídas no [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], para criar o modelo de regressão logística.
  
        A variável binária _tipped_ é usada como a coluna *label* ou de resultado, e o modelo é ajustado com o uso destas colunas de recursos:  _passenger_count_, _trip_distance_, _trip_time_in_secs_e _direct_distance_.
  
    - O modelo treinado, salvo na variável `logitObj`de R, é serializado e retornado como um parâmetro de saída.

## <a name="train-and-deploy-the-r-model-using-the-stored-procedure"></a>Treinar e implantar o modelo R usando o procedimento armazenado

Como o procedimento armazenado já inclui uma definição dos dados de entrada, você não precisa fornecer uma consulta de entrada.

1. Para treinar e implantar o modelo R, chame o procedimento armazenado e insira-o na tabela de banco de dados _nyc_taxi_models_, para que você possa usá-lo para previsões futuras:

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC RxTrainLogitModel @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('RxTrainLogit_model', @model);
    ```

2. Observe a janela **mensagens** do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para mensagens que seriam canalizadas para o fluxo **stdout** do R, como esta mensagem: 

    "Mensagem (ns) STDOUT do script externo: Linhas lidas: 1193025, total de linhas processadas: 1193025, tempo total da parte: 0, 93 segundos "

    Você também pode ver mensagens específicas para a função individual, `rxLogit`exibindo as variáveis e as métricas de teste geradas como parte da criação do modelo.

3.  Quando a instrução for concluída, abra a tabela *nyc_taxi_models*. O processamento dos dados e a ajuste do modelo pode levar algum tempo.

    Você pode ver que uma nova linha foi adicionada, que contém o modelo serializado no _modelo_ de coluna e o nome do modelo **RxTrainLogit_model** no _nome_da coluna.

    ```sql
    model                        name
    ---------------------------- ------------------
    0x580A00000002000302020....  RxTrainLogit_model
    ```

Na próxima etapa, você usará o modelo treinado para gerar previsões.

## <a name="next-lesson"></a>Próxima lição

[Lição 4: Prever resultados potenciais usando um modelo de R em um procedimento armazenado](../tutorials/sqldev-operationalize-the-model.md)

## <a name="previous-lesson"></a>Lição anterior

[Lição 2: Criar recursos de dados usando o R e o T-SQL Functions](..//tutorials/sqldev-create-data-features-using-t-sql.md)

