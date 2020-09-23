---
title: 'Tutorial do Python: Criar recursos de dados'
titleSuffix: SQL machine learning
description: Na terceira parte desta série de tutoriais em cinco partes, você adicionará cálculos a procedimentos armazenados para usar em modelos de machine learning do Python com o aprendizado de máquina do SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/29/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||>=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: b50750368dd5c8b9d558a587699fde1e7d94af15
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88180330"
---
# <a name="python-tutorial-create-data-features-using-t-sql"></a>Tutorial do Python: Criar recursos de dados usando o T-SQL
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

Na terceira parte desta série de tutoriais em cinco partes, você aprenderá a criar recursos a partir de dados brutos usando uma função do [!INCLUDE[tsql](../../includes/tsql-md.md)]. Você chamará essa função por meio de um procedimento armazenado do SQL para criar uma tabela que contém os valores de recurso.

O processo de *engenharia de recursos*, que consiste na criação de recursos a partir de dados brutos, pode ser uma etapa crítica na modelagem de análise avançada.

Neste artigo, você vai:

> [!div class="checklist"]
> + Modificar uma função personalizada para calcular a distância de viagem
> + Salvar os recursos usando outra função personalizada

Na [parte um](python-taxi-classification-introduction.md), você instalou os pré-requisitos e restaurou o banco de dados de exemplo.

Na [parte dois](python-taxi-classification-explore-data.md), você explorou os dados de exemplo e gerou alguns gráficos.

Na [parte quatro](python-taxi-classification-train-model.md), você carregará os módulos e chamará as funções necessárias para criar e treinar o modelo usando um procedimento armazenado do SQL Server.

Na [parte cinco](python-taxi-classification-deploy-model.md), você aprenderá a operacionalizar os modelos treinados e salvos na parte quatro.

## <a name="define-the-function"></a>Definir a função

Os valores de distância relatados nos dados originais baseiam-se na distância do medidor relatado e não representam necessariamente a distância geográfica nem a distância percorrida. Portanto, você precisará calcular a distância direta entre os pontos de embarque e desembarque de passageiros, usando as coordenadas disponíveis no conjunto de dados NYC Taxi de origem. Você pode fazer isso usando a [fórmula de Haversine](https://en.wikipedia.org/wiki/Haversine_formula) em uma função personalizada [!INCLUDE[tsql](../../includes/tsql-md.md)] .

Você usará uma função personalizada do T-SQL, _fnCalculateDistance_, para calcular a distância usando a fórmula de Haversine e usará uma segunda função personalizada do T-SQL, _fnEngineerFeatures_, para criar uma tabela que contém todos os recursos.

### <a name="calculate-trip-distance-using-fncalculatedistance"></a>Calcular a distância da corrida usando fnCalculateDistance

1. A função _fnCalculateDistance_ está incluída no banco de dados de exemplo. Reserve um minuto para examinar o código.
  
2. No [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], expanda **Programação**, **Funções** e **Funções de valor escalar**.
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

+ A função é uma função de valor escalar, retornando um único valor de dados de um tipo predefinido.
+ Ela usa os valores de latitude e longitude como entradas, obtidos dos locais de embarque e desembarque de passageiros. A fórmula de Haversine converte locais em radianos e usa esses valores para calcular a distância direta em milhas entre os dois locais.

Para adicionar o valor calculado a uma tabela que pode ser usada para treinar o modelo, você usará outra função, _fnEngineerFeatures_.

### <a name="save-the-features-using-_fnengineerfeatures_"></a>Salvar os recursos usando _fnEngineerFeatures_

1. Reserve um minuto para examinar o código para a função do T-SQL personalizada, _fnEngineerFeatures_, que está incluída no banco de dados de exemplo.
  
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
  
   Como você pode ver, a distância relatada pelo medidor nem sempre corresponde à distância geográfica. Por isso a engenharia de recursos é importante.

Na próxima parte, você aprenderá a usar esses recursos de dados para criar e treinar um modelo de machine learning usando o Python.

## <a name="next-steps"></a>Próximas etapas

Neste artigo você:

> [!div class="checklist"]
> + Modificou uma função personalizada para calcular a distância de viagem
> + Salvou os recursos usando outra função personalizada

> [!div class="nextstepaction"]
> [Tutorial do Python: Treinar e salvar um modelo do Python usando o T-SQL](python-taxi-classification-train-model.md)