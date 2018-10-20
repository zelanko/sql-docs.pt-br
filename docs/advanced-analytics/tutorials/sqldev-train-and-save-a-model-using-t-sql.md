---
title: Lição 3 treinar e salvar um modelo usando R e T-SQL (aprendizado de máquina do SQL Server) | Microsoft Docs
description: Tutorial que mostra como incorporar o R no SQL Server procedimentos armazenados e funções T-SQL
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/07/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 73e1b2ef70821af2247de000eba45a495075e614
ms.sourcegitcommit: 3cd6068f3baf434a4a8074ba67223899e77a690b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49463016"
---
# <a name="lesson-3-train-and-save-a-model-using-t-sql"></a>Lição 3: Treinar e salvar um modelo usando o T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo faz parte de um tutorial para desenvolvedores SQL sobre como usar o R no SQL Server.

Nesta lição, você aprenderá a treinar um modelo de aprendizado de máquina usando o R. Você vai treinar o modelo usando os recursos de dados que você criou na lição anterior e, em seguida, salve o modelo treinado em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela. Nesse caso, os pacotes do R já estão instalados no [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], portanto, tudo o que pode ser feito do SQL.

## <a name="create-the-stored-procedure"></a>Criar o procedimento armazenado

Ao chamar o R de T-SQL, você use o procedimento armazenado do sistema [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). No entanto, para processos que você repetir muitas vezes, como a readaptação de um modelo, é mais fácil encapsular a chamada para `sp_execute_exernal_script` em outro procedimento armazenado.

1.  Primeiro, crie um procedimento armazenado que contém o código de R para criar o modelo de previsão de dica. Na [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra uma nova **consulta** e execute a seguinte instrução para criar o procedimento armazenado _TrainTipPredictionModel_. Esse procedimento armazenado define os dados de entrada e usa um pacote do R para criar um modelo de regressão logística.

    ```SQL
    CREATE PROCEDURE [dbo].[TrainTipPredictionModel]
    
    AS
    BEGIN
      DECLARE @inquery nvarchar(max) = N'
        select tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance,
        pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
        from nyctaxi_sample
        tablesample (70 percent) repeatable (98052)
    '
      -- Insert the trained model into a database table
      INSERT INTO nyc_taxi_models
      EXEC sp_execute_external_script @language = N'R',
                                      @script = N'
    
    ## Create model
    logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = InputDataSet)
    summary(logitObj)
    
    ## Serialize model and put it in data frame
    trained_model <- data.frame(model=as.raw(serialize(logitObj, NULL)));
    ',
      @input_data_1 = @inquery,
      @output_data_1_name = N'trained_model'
      ;
    
    END
    GO
    ```

    - No entanto, para garantir que alguns dados é restantes para testar o modelo, 70% dos dados são selecionados aleatoriamente da tabela de dados de táxi.
    
    - A consulta SELECT usa a função escalar personalizada _fnCalculateDistance_ para calcular a distância direta entre os locais de embarque e desembarque de passageiros.  os resultados da consulta são armazenados na variável de entrada padrão do R, `InputDataset`.
  
    - O script do R chama o `rxLogit` função, que é uma das funções avançadas do R incluídas com [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], para criar o modelo de regressão logística.
  
        A variável binária _tipped_ é usada como a coluna *label* ou de resultado, e o modelo é ajustado com o uso destas colunas de recursos:  _passenger_count_, _trip_distance_, _trip_time_in_secs_e _direct_distance_.
  
    -   O modelo treinado, salvo na variável do R `logitObj`, é serializado e colocado em um quadro de dados para a saída no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa saída é inserida na tabela de banco de dados _nyc_taxi_models_, de modo que você possa usá-la para previsões futuras.
  
2.  Execute a instrução para criar o procedimento armazenado, se ele ainda não existir.

## <a name="generate-the-r-model-using-the-stored-procedure"></a>Gerar o modelo de R usando o procedimento armazenado

Como o procedimento armazenado já inclui uma definição dos dados de entrada, você não precisa fornecer uma consulta de entrada.

1. Para gerar o modelo do R, chame o procedimento armazenado sem quaisquer outros parâmetros:

    ```SQL
    EXEC TrainTipPredictionModel
    ```

2. Assista a **mensagens** janela do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para mensagens que serão redirecionadas para do R **stdout** fluxo, como esta mensagem: 

    "Mensagem (NS) STDOUT do script externo: linhas lidas: 1193025, Total de linhas processadas: 1193025, tempo Total: 0.093 segundos"

    Você também poderá ver mensagens específicas de função individual, `rxLogit`, exibindo as variáveis e métricas geradas como parte da criação do modelo de teste.

3.  Quando a instrução for concluída, abra a tabela *nyc_taxi_models*. Processamento de dados e ajuste do modelo podem levar algum tempo.

    Você pode ver que uma nova linha foi adicionada, que contém o modelo serializado na coluna _modelo_.

    ```
    model
    ------
    0x580A00000002000302020....
    ```

Na próxima etapa, você usará o modelo treinado para criar previsões.

## <a name="next-lesson"></a>Próxima lição

[Lição 4: Operacionalizar o modelo](../tutorials/sqldev-operationalize-the-model.md)

## <a name="previous-lesson"></a>Lição anterior

[Lição 2: Criar recursos de dados usando funções de R e T-SQL](..//tutorials/sqldev-create-data-features-using-t-sql.md)

