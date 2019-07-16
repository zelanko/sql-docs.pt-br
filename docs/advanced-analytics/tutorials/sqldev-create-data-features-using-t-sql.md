---
title: Lição 2 recursos de dados de criar usando funções de R e T-SQL – SQL Server Machine Learning
description: Tutorial que mostra como adicionar cálculos para procedimentos armazenados para uso em modelos de aprendizado de máquina do R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/19/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 5d304bdf03eaea53ede0cf4b2f8d82f64c3d1021
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961929"
---
# <a name="lesson-2-create-data-features-using-r-and-t-sql"></a>Lição 2: Criar recursos de dados usando R e T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo faz parte de um tutorial para desenvolvedores SQL sobre como usar o R no SQL Server.

Nesta etapa, você aprenderá a criar recursos de dados brutos usando uma função [!INCLUDE[tsql](../../includes/tsql-md.md)] . Você chamará essa função por meio de um procedimento armazenado para criar uma tabela que contém os valores do recurso.

## <a name="about-feature-engineering"></a>Sobre engenharia de recursos

Após várias rodadas de exploração de dados, você reuniu algumas ideias sobre os dados e está pronto para passar para a *engenharia de recursos*. Esse processo de criação de recursos significativos dos dados brutos é uma etapa crítica na criação de modelos analíticos.

Neste conjunto de dados, os valores de distância são com base na distância do medidor relatado e não representam necessariamente a distância geográfica ou da distância real percorrida. Portanto, você precisará calcular a distância direta entre os pontos de embarque e desembarque de passageiros, usando as coordenadas disponíveis no conjunto de dados NYC Taxi de origem. Você pode fazer isso usando a [fórmula de Haversine](https://en.wikipedia.org/wiki/Haversine_formula) em uma função personalizada [!INCLUDE[tsql](../../includes/tsql-md.md)] .

Você usará uma função personalizada do T-SQL, _fnCalculateDistance_, para calcular a distância usando a fórmula de Haversine e usará uma segunda função personalizada do T-SQL, _fnEngineerFeatures_, para criar uma tabela que contém todos os recursos.

O processo geral é da seguinte maneira:

- Crie a função do T-SQL que executa os cálculos

- Chamar a função para gerar os dados do recurso

- Salvar os dados do recurso em uma tabela

## <a name="calculate-trip-distance-using-fncalculatedistance"></a>Calcular a distância da corrida usando fnCalculateDistance

A função _fnCalculateDistance_ deve ter sido baixado e registrado com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como parte da preparação para este tutorial. Reserve um minuto para examinar o código.
  
1. No [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], expanda **Programação**, **Funções** e **Funções de valor escalar**.   

2. Clique com o botão direito do mouse em _fnCalculateDistance_e selecione **Modificar** para abrir o script [!INCLUDE[tsql](../../includes/tsql-md.md)] em uma nova janela de consulta.
  
    ```sql
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)  
    -- User-defined function that calculates the direct distance between two geographical coordinates.  
    RETURNS float  
    AS  
    BEGIN  
      DECLARE @distance decimal(28, 10)  
      -- Convert to radians  
      SET @Lat1 = @Lat1 / 57.2958  
      SET @Long1 = @Long1 / 57.2958  
      SET @Lat2 = @Lat2 / 57.2958  
      SET @Long2 = @Long2 / 57.2958  
      -- Calculate distance  
      SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))  
      --Convert to miles  
      IF @distance <> 0  
      BEGIN  
        SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);  
      END  
      RETURN @distance  
    END
    GO
    ```
  
    - A função é uma função de valor escalar, retornando um único valor de dados de um tipo predefinido.
  
    - Ela usa os valores de latitude e longitude como entradas, obtidos dos locais de embarque e desembarque de passageiros. A fórmula de Haversine converte locais em radianos e usa esses valores para calcular a distância direta em milhas entre os dois locais.

## <a name="generate-the-features-using-fnengineerfeatures"></a>Gerar recursos usando _fnEngineerFeatures_

Para adicionar os valores computados em uma tabela que pode ser usada para treinar o modelo, você usará outra função, _fnEngineerFeatures_. A nova função chama a função de T-SQL criada anteriormente, _fnCalculateDistance_, para obter a distância direta entre os locais de embarque e desembarque de passageiros. 

1. Reserve um minuto para examinar a função personalizada do T-SQL no o código, _fnEngineerFeatures_, que deve ter sido criada como parte da preparação para esse passo a passo.
  
    ```sql
    CREATE FUNCTION [dbo].[fnEngineerFeatures] (  
    @passenger_count int = 0,  
    @trip_distance float = 0,  
    @trip_time_in_secs int = 0,  
    @pickup_latitude float = 0,  
    @pickup_longitude float = 0,  
    @dropoff_latitude float = 0,  
    @dropoff_longitude float = 0)  
    RETURNS TABLE  
    AS
      RETURN
      (
      -- Add the SELECT statement with parameter references here
      SELECT
        @passenger_count AS passenger_count,
        @trip_distance AS trip_distance,
        @trip_time_in_secs AS trip_time_in_secs,
        [dbo].[fnCalculateDistance](@pickup_latitude, @pickup_longitude, @dropoff_latitude, @dropoff_longitude) AS direct_distance
  
      )
    GO
    ```

    + Essa função com valor de tabela que usa várias colunas como entradas e saídas de uma tabela com várias colunas de recurso.

    + A finalidade dessa função é criar novos recursos para uso na criação de um modelo.

2.  Para verificar se essa função funciona, usá-lo para calcular a distância geográfica dessas corridas em que a distância limitada era 0 mas os locais de embarque e desembarque de passageiros eram diferentes.
  
    ```sql
        SELECT tipped, fare_amount, passenger_count,(trip_time_in_secs/60) as TripMinutes,
        trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) AS direct_distance
        FROM nyctaxi_sample
        WHERE pickup_longitude != dropoff_longitude and pickup_latitude != dropoff_latitude and trip_distance = 0
        ORDER BY trip_time_in_secs DESC
    ```
  
    Como você pode ver, a distância relatada pelo medidor nem sempre corresponde à distância geográfica. Por isso a engenharia de recursos é tão importante. Você pode usar esses recursos de dados aprimorados para treinar um modelo de aprendizado de máquina usando o R.

## <a name="next-lesson"></a>Próxima lição

[Lição 3: Treinar e salvar um modelo usando o T-SQL](sqldev-train-and-save-a-model-using-t-sql.md)

## <a name="previous-lesson"></a>Lição anterior

[Lição 1: Explorar e visualizar os dados usando R e procedimentos armazenados](sqldev-explore-and-visualize-the-data.md)
