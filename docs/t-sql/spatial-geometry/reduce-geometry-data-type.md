---
title: Reduce (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Reduce_TSQL
- Reduce
dev_langs:
- TSQL
helpviewer_keywords:
- Reduce method
ms.assetid: 132184bf-c4d2-4a27-900d-8373445dce2a
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: f66cdcebb92127486d75de270d93d0507131c4d3
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65937365"
---
# <a name="reduce-geometry-data-type"></a>Reduce (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna uma aproximação da instância de **geometria** fornecida. A aproximação é produzida pela execução de uma extensão do algoritmo Douglas-Peucker na instância com a tolerância especificada.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.Reduce ( tolerance )  
```  
  
## <a name="arguments"></a>Argumentos  
 *tolerance*  
 É um valor do tipo **float**. *tolerance* é a tolerância de entrada para o algoritmo de aproximação.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de retorno CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 Para os tipos de coleção, esse algoritmo opera de forma independente em cada **geometria** contida na instância.  
  
 Esse algoritmo não modifica as instâncias de **Point**.  
  
 Nas instâncias **LineString**, **CircularString** e **CompoundCurve**, o algoritmo de aproximação mantém os pontos originais de início e de término da instância. Em seguida, o algoritmo iterativamente adiciona de volta o ponto da instância original que mais desvia do resultado. Esse processo continua até que nenhum ponto desvie mais do que a tolerância especificada.  
  
 `Reduce()` retorna uma instância de **LineString**, **CircularString** ou **CompoundCurve** para instâncias de **CircularString**.  `Reduce()` retorna um uma instância de **CompoundCurve** ou **LineString** para instâncias de **CompoundCurve**.  
  
 Em instâncias de **polígono**, o algoritmo de aproximação é aplicado de forma independente a cada anel. O método produzirá uma `FormatException` se a instância de **polígono** retornada não for válida. Por exemplo, uma instância inválida de **MultiPolygon** será criada se `Reduce()` for aplicado para simplificar cada anel na instância e se os anéis resultantes se sobrepuserem.  Nas instâncias de **CurvePolygon** com um anel exterior e sem nenhum anel interior, `Reduce()` retorna uma instância de **CurvePolygon**, **LineString** ou **Point**.  Se **CurvePolygon** tiver anéis interiores, uma instância de **CurvePolygon** ou **MultiPoint** será retornada.  
  
 Quando um segmento de arco circular é encontrado, o algoritmo de aproximação verifica se o arco pode ser aproximado por sua corda dentro de metade da tolerância dada. As cordas que satisfazem esses critérios, o arco circular é substituído nos cálculos pela corda. Se uma corda não satisfaz esses critérios, o arco circular é mantido e o algoritmo de aproximação é aplicado aos segmentos restantes.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-reduce-to-simplify-a-linestring"></a>A. Usando Reduce() para simplificar um LineString  
 O exemplo a seguir cria uma instância `LineString` e usa `Reduce()` para simplificar a instância.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 0 1, 1 0, 2 1, 3 0, 4 1)', 0);  
SELECT @g.Reduce(.75).ToString();  
```  
  
### <a name="b-using-reduce-with-varying-tolerance-levels-on-a-circularstring"></a>B. Usando Reduce() com níveis de tolerância variados em um CircularString  
 O exemplo a seguir usa `Reduce()` com três níveis de tolerância em uma instância de **CircularString**:  
  
```
 DECLARE @g geometry = 'CIRCULARSTRING(0 0, 8 8, 16 0, 20 -4, 24 0)'; 
 SELECT @g.Reduce(5).ToString(); 
 SELECT @g.Reduce(15).ToString(); 
 SELECT @g.Reduce(16).ToString();
 ```  
  
 Esse exemplo gera a saída a seguir:  
  
 ```
 CIRCULARSTRING (0 0, 8 8, 16 0, 20 -4, 24 0) 
 COMPOUNDCURVE (CIRCULARSTRING (0 0, 8 8, 16 0), (16 0, 24 0)) 
 LINESTRING (0 0, 24 0)
 ```  
  
 Cada uma das instâncias retornadas contém os pontos de extremidade (0 0) e (24 0).  
  
### <a name="c-using-reduce-with-varying-tolerance-levels-on-a-compoundcurve"></a>C. Usando Reduce() com níveis de tolerância variados em um CompoundCurve  
 O exemplo a seguir usa `Reduce()` com dois níveis de tolerância em uma instância de **CompoundCurve**:  
  
```
 DECLARE @g geometry = 'COMPOUNDCURVE(CIRCULARSTRING(0 0, 8 8, 16 0, 20 -4, 24 0),(24 0, 20 4, 16 0))';  
 SELECT @g.Reduce(15).ToString();  
 SELECT @g.Reduce(16).ToString();
 ```  
  
 Neste exemplo, observe que a segunda instrução **SELECT** retorna a instância de **LineString**: `LineString(0 0, 16 0)`.  
  
### <a name="showing-an-example-where-the-original-start-and-end-points-are-lost"></a>Mostrando um exemplo onde os pontos originais de início e de término são perdidos  
 O exemplo a seguir mostra como os pontos originais de início e de término talvez não sejam retidos pela instância resultante. Esse comportamento ocorre porque manter os pontos originais de início e de extremidade resultaria em uma instância de **LineString** inválida.  
  
```  
DECLARE @g geometry = 'LINESTRING(0 0, 4 0, 2 .01, 1 0)';  
DECLARE @h geometry = @g.Reduce(1);  
SELECT @g.STIsValid() AS Valid  
SELECT @g.ToString() AS Original, @h.ToString() AS Reduced;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos geometry estáticos estendidos](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
