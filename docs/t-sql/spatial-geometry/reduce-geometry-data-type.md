---
title: Reduce (tipo de dados geometry) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Reduce_TSQL
- Reduce
dev_langs:
- TSQL
helpviewer_keywords:
- Reduce method
ms.assetid: 132184bf-c4d2-4a27-900d-8373445dce2a
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fb6c4a66f3233620ef5d24506d41e7659fc3b82d
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="reduce-geometry-data-type"></a>Reduce (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna uma aproximação de determinada instância de **geometry** produzida pela execução de uma extensão do algoritmo Douglas-Peucker na instância com a tolerância especificada.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.Reduce ( tolerance )  
```  
  
## <a name="arguments"></a>Argumentos  
 *tolerance*  
 É um valor do tipo **float**. *tolerance* é a tolerância de entrada para o algoritmo de aproximação.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de retorno do CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 Para os tipos de coleção, esse algoritmo opera de forma independente em cada **geometria** contida na instância.  
  
 Esse algoritmo não modifica as instâncias de **Point**.  
  
 Nas instâncias de **LineString**, **CircularString** e **CompoundCurve**, o algoritmo de aproximação retém os pontos originais de início e de extremidade da instância e adiciona novamente de forma iterativa o ponto da instância original que mais se desvia do resultado, até que nenhum ponto desvie mais do que a tolerância especificada.  
  
 `Reduce()` retorna uma instância de **LineString**, **CircularString** ou **CompoundCurve** para instâncias de **CircularString**.  `Reduce()` retorna um uma instância de **CompoundCurve** ou **LineString** para instâncias de **CompoundCurve**.  
  
 Em instâncias de **polígono**, o algoritmo de aproximação é aplicado de forma independente a cada anel. O método produzirá uma `FormatException` se a instância de **polígono** retornada não for válida. Por exemplo, uma instância inválida de **MultiPolygon** será criada se `Reduce()` for aplicado para simplificar cada anel na instância e se os anéis resultantes se sobrepuserem.  Nas instâncias de **CurvePolygon** com um anel exterior e sem nenhum anel interior, `Reduce()` retorna uma instância de **CurvePolygon**, **LineString** ou **Point**.  Se **CurvePolygon** tiver anéis interiores, uma instância de **CurvePolygon** ou **MultiPoint** será retornada.  
  
 Quando um segmento de arco circular é encontrado, o algoritmo de aproximação verifica se o arco pode ser aproximado por sua corda dentro de metade da tolerância dada.  Se a corda conhecer estes critérios, o arco circular será substituído nos cálculos pela corda. Caso contrário, o arco circular será retido e o algoritmo de aproximação será aplicado aos segmentos restantes.  
  
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
 O exemplo a seguir mostra como os pontos originais de início e de término talvez não sejam retidos pela instância resultante. Isso ocorre porque a retenção dos pontos originais de início e de extremidade resultaria em uma instância de **LineString** inválida.  
  
```  
DECLARE @g geometry = 'LINESTRING(0 0, 4 0, 2 .01, 1 0)';  
DECLARE @h geometry = @g.Reduce(1);  
SELECT @g.STIsValid() AS Valid  
SELECT @g.ToString() AS Original, @h.ToString() AS Reduced;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos geometry estáticos estendidos](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

