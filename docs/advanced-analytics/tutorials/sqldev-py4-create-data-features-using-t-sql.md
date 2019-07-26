---
title: Criar recursos de dados usando funções T-SQL e Python
description: Tutorial mostrando como adicionar cálculos a procedimentos armazenados para uso em modelos de aprendizado de máquina Python.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/01/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: f1e07ffa4423ccfc2cc0082910a2ca8aff8fd087
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68468676"
---
# <a name="create-data-features-using-t-sql"></a>Criar recursos de dados usando o T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Após a exploração de dados, você coletou algumas informações dos dados e está pronto para passar para a engenharia de *recursos*. Esse processo de criação de recursos dos dados brutos pode ser uma etapa crítica na modelagem de análise avançada.

Este artigo faz parte de um tutorial, [análise do Python no banco de dados para desenvolvedores do SQL](sqldev-in-database-python-for-sql-developers.md). 

Nesta etapa, você aprenderá a criar recursos de dados brutos usando uma função [!INCLUDE[tsql](../../includes/tsql-md.md)] . Você chamará essa função por meio de um procedimento armazenado para criar uma tabela que contém os valores do recurso.

## <a name="define-the-function"></a>Definir a função

Os valores de distância relatados nos dados originais baseiam-se na distância do medidor relatado e não representam necessariamente a distância geográfica nem a distância percorrida. Portanto, você precisará calcular a distância direta entre os pontos de embarque e desembarque de passageiros, usando as coordenadas disponíveis no conjunto de dados NYC Taxi de origem. Você pode fazer isso usando a [fórmula de Haversine](https://en.wikipedia.org/wiki/Haversine_formula) em uma função personalizada [!INCLUDE[tsql](../../includes/tsql-md.md)] .

Você usará uma função personalizada do T-SQL, _fnCalculateDistance_, para calcular a distância usando a fórmula de Haversine e usará uma segunda função personalizada do T-SQL, _fnEngineerFeatures_, para criar uma tabela que contém todos os recursos.

### <a name="calculate-trip-distance-using-fncalculatedistance"></a>Calcular a distância de viagem usando fnCalculateDistance

1.  A função _fnCalculateDistance_ deve ter sido baixada e registrada no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como parte da preparação para esse passo a passo. Reserve um minuto para examinar o código.
  
    No [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], expanda **Programação**, **Funções** e **Funções de valor escalar**.
    Clique com o botão direito do mouse em _fnCalculateDistance_e selecione **Modificar** para abrir o script [!INCLUDE[tsql](../../includes/tsql-md.md)] em uma nova janela de consulta.
  
    ```sql
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)
    -- User-defined function that calculates the direct distance between two geographical coordinates
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
**Observações:**

- A função é uma função de valor escalar, retornando um único valor de dados de um tipo predefinido.
- Ela usa os valores de latitude e longitude como entradas, obtidos dos locais de embarque e desembarque de passageiros. A fórmula de Haversine converte locais em radianos e usa esses valores para calcular a distância direta em milhas entre os dois locais.

Para adicionar o valor calculado a uma tabela que pode ser usada para treinar o modelo, você usará outra função, _fnEngineerFeatures_.

### <a name="save-the-features-using-fnengineerfeatures"></a>Salve os recursos usando o _fnEngineerFeatures_

1.  Reserve um minuto para examinar a função personalizada do T-SQL no o código, _fnEngineerFeatures_, que deve ter sido criada como parte da preparação para esse passo a passo.
  
    Essa função é uma função com valor de tabela que usa várias colunas como entradas e gerar uma tabela com várias colunas de recurso.  A finalidade dessa função é criar um conjunto de recursos para uso na criação de um modelo. A função _fnEngineerFeatures_ chama a função T-SQL criada anteriormente, _fnCalculateDistance_, para obter a distância direta entre os locais de embarque e desembarque de passageiros.
  
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
  
2. Para verificar se essa função funciona, você pode usá-la para calcular a distância geográfica dessas corridas em que a distância limitada era 0, mas os locais de embarque e desembarque de passageiros eram diferentes.
  
    ```sql
        SELECT tipped, fare_amount, passenger_count,(trip_time_in_secs/60) as TripMinutes,
        trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) AS direct_distance
        FROM nyctaxi_sample
        WHERE pickup_longitude != dropoff_longitude and pickup_latitude != dropoff_latitude and trip_distance = 0
        ORDER BY trip_time_in_secs DESC
    ```
  
    Como você pode ver, a distância relatada pelo medidor nem sempre corresponde à distância geográfica. É por isso que a engenharia de recursos é importante.

Na próxima etapa, você aprenderá a usar esses recursos de dados para criar e treinar um modelo de aprendizado de máquina usando o Python.

## <a name="next-step"></a>Próxima etapa

[Treinar e salvar um modelo Python usando o T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="previous-step"></a>Etapa anterior

[Explorar e visualizar os dados](sqldev-py3-explore-and-visualize-the-data.md)


