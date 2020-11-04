---
title: 'Tutorial do R: Treinar e salvar o modelo'
titleSuffix: SQL machine learning
description: Na parte quatro desta série de tutoriais de cinco partes, você treinará e salvará um modelo em R usando o Transact-SQL no SQL Server com o aprendizado de máquina do SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/15/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||>=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: d42d51371b0641fe460150e68fe96c5eb68e09cb
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92412544"
---
# <a name="r-tutorial-train-and-save-model"></a>Tutorial do R: Treinar e salvar o modelo
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

Na parte quatro desta série de tutoriais de cinco partes, você aprenderá a treinar um modelo de machine learning usando o R. Você treinará o modelo usando os recursos de dados criados na parte anterior e salvará o modelo treinado em uma tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Neste caso, os pacotes do R já estão instalados com o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], portanto, tudo pode ser feito do SQL.

Neste artigo você vai:

> [!div class="checklist"]
> + Criar e treinar um modelo usando um procedimento armazenado do SQL
> + Salvar o modelo treinado em uma tabela SQL

Na [parte um](r-taxi-classification-introduction.md), você instalou os pré-requisitos e restaurou o banco de dados de exemplo.

Na [parte dois](r-taxi-classification-explore-data.md), você examinou os dados de exemplo e gerou alguns gráficos.

Na [parte três](r-taxi-classification-create-features.md), você aprendeu a criar recursos de dados brutos usando uma função Transact-SQL. Em seguida, você chamou essa função por meio de um procedimento armazenado para criar uma tabela que contém os valores do recurso.

Na [parte cinco](r-taxi-classification-deploy-model.md), você aprenderá a operacionalizar os modelos treinados e salvos na parte quatro.

## <a name="create-the-stored-procedure"></a>Criar o procedimento armazenado

Ao chamar o R do T-SQL, você usa o procedimento armazenado do sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). No entanto, para processos que você repete com frequência, como treinar novamente um modelo, é mais fácil encapsular a chamada para `sp_execute_external_script` em outro procedimento armazenado.

1. No [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra uma nova janela de **Consulta**.

2. Execute a instrução a seguir para criar o procedimento armazenado **RTrainLogitModel**. Esse procedimento define os dados de entrada e usa **glm** para criar um modelo de regressão logística.

   ```sql
   CREATE PROCEDURE [dbo].[RTrainLogitModel] (@trained_model varbinary(max) OUTPUT)
   
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
   logitObj <- glm(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = InputDataSet, family = binomial)
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

   + Para garantir que há alguns dados para testar o modelo, 70% dos dados são selecionados aleatoriamente da tabela de dados de táxi para fins de treinamento.

   + A consulta SELECT usa a função escalar personalizada *fnCalculateDistance* para calcular a distância direta entre os locais de embarque e desembarque de passageiros. Os resultados da consulta são armazenados na variável de entrada padrão do R, `InputDataset`.
  
   + O script R chama a função **glm** do R para criar o modelo de regressão logística.
  
     A variável binária _tipped_ é usada como a coluna *label* ou de resultado, e o modelo é ajustado com o uso destas colunas de recursos:  _passenger_count_ , _trip_distance_ , _trip_time_in_secs_ e _direct_distance_.
  
   + O modelo treinado, salvo no `logitObj` da variável do R, é serializado e retornado como um parâmetro de saída.

## <a name="train-and-deploy-the-r-model-using-the-stored-procedure"></a>Treinar e implantar o modelo do R usando o procedimento armazenado

Como o procedimento armazenado já inclui uma definição dos dados de entrada, você não precisa fornecer uma consulta de entrada.

1. Para treinar e implantar o modelo do R, chame o procedimento armazenado e insira-o na tabela de banco de dados _nyc_taxi_models_ para que você possa usá-lo para previsões futuras:

   ```sql
   DECLARE @model VARBINARY(MAX);
   EXEC RTrainLogitModel @model OUTPUT;
   INSERT INTO nyc_taxi_models (name, model) VALUES('RTrainLogit_model', @model);
   ```

2. Assista à janela **Mensagens** de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para mensagens que seriam canalizadas para o fluxo **stdout** do R, como esta mensagem: 

   "Mensagem(ns) STDOUT do script externo: Linhas lidas: 1193025, Total de Linhas Processadas: 1193025, Tempo Total da Parte: 0,093 segundos"

3. Quando a instrução tiver sido concluída, abra a tabela *nyc_taxi_models*. O processamento dos dados e o ajuste do modelo poderão levar algum tempo.

   Você pode ver que foi adicionada uma nova linha contendo o modelo serializado na coluna _model_ e o nome do modelo **TrainLog_model** na coluna _name_.

   ```text
   model                        name
   ---------------------------- ------------------
   0x580A00000002000302020....  RTrainLogit_model
   ```

Na próxima parte deste tutorial, você usará o modelo treinado para gerar previsões.

## <a name="next-steps"></a>Próximas etapas

Neste artigo você:

> [!div class="checklist"]
> + Criou e treinou um modelo usando um procedimento armazenado do SQL
> + Salvou o modelo treinado em uma tabela SQL

> [!div class="nextstepaction"]
> [Tutorial do R: executar previsões em procedimentos armazenados do SQL](r-taxi-classification-deploy-model.md)
