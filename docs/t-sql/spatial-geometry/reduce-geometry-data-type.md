---
title: Reduzir (tipo de dados geometry) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Reduce_TSQL
- Reduce
dev_langs: TSQL
helpviewer_keywords: Reduce method
ms.assetid: 132184bf-c4d2-4a27-900d-8373445dce2a
caps.latest.revision: "30"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d843ac0c2e9374cf8b22d404f943ea1c598c8b7b
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="reduce-geometry-data-type"></a>Reduce (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna uma aproximação do determinado **geometria** instância produzida pela execução de uma extensão do algoritmo Douglas-Peucker na instância com a tolerância especificada.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.Reduce ( tolerance )  
```  
  
## <a name="arguments"></a>Argumentos  
 *tolerance*  
 É um valor do tipo **float**. *tolerância* é a tolerância de entrada para o algoritmo de aproximação.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geometry**  
  
 Tipo de retorno CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 Para tipos de coleção, esse algoritmo funciona independentemente em cada **geometria** contidos na instância.  
  
 Esse algoritmo não modifica **ponto** instâncias.  
  
 Em **LineString**, **CircularString**, e **CompoundCurve** instâncias, o algoritmo de aproximação retém os pontos de início e final da instância, e iterativamente adiciona de volta o ponto da instância original que mais se desvia do resultado, até que nenhum ponto desvie mais do que a tolerância especificada.  
  
 `Reduce()`Retorna um **LineString**, **CircularString**, ou **CompoundCurve** instância para **CircularString** instâncias.  `Reduce()`Retorna um uma **CompoundCurve** ou **LineString** instância para **CompoundCurve** instâncias.  
  
 Em **polígono** instâncias, o algoritmo de aproximação é aplicado independentemente a cada anel. O método produzirá uma `FormatException` se retornado **polígono** instância não é válida; por exemplo, um não válido **MultiPolygon** instância é criada se `Reduce()` for aplicado para simplificar cada anel na instância e o anéis resultantes se sobrepuserem.  Em **CurvePolygon** instâncias com um anel exterior e nenhum anel interior, `Reduce()` retorna um **CurvePolygon**, **LineString**, ou **ponto** instância.  Se o **CurvePolygon** tiver anéis interiores, um **CurvePolygon** ou **MultiPoint** instância será retornada.  
  
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
 O exemplo a seguir usa `Reduce()` com três níveis de tolerância em uma **CircularString** instância:  
  
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
 O exemplo a seguir usa `Reduce()` com dois níveis de tolerância em uma **CompoundCurve** instância:  
  
```
 DECLARE @g geometry = 'COMPOUNDCURVE(CIRCULARSTRING(0 0, 8 8, 16 0, 20 -4, 24 0),(24 0, 20 4, 16 0))';  
 SELECT @g.Reduce(15).ToString();  
 SELECT @g.Reduce(16).ToString();
 ```  
  
 Neste exemplo, observe que a segunda **selecione** instrução retorna o **LineString** instância: `LineString(0 0, 16 0)`.  
  
### <a name="showing-an-example-where-the-original-start-and-end-points-are-lost"></a>Mostrando um exemplo onde os pontos originais de início e de término são perdidos  
 O exemplo a seguir mostra como os pontos originais de início e de término talvez não sejam retidos pela instância resultante. Isso ocorre porque a retenção originais de início e pontos de extremidade resultaria em inválido **LineString** instância.  
  
```  
DECLARE @g geometry = 'LINESTRING(0 0, 4 0, 2 .01, 1 0)';  
DECLARE @h geometry = @g.Reduce(1);  
SELECT @g.STIsValid() AS Valid  
SELECT @g.ToString() AS Original, @h.ToString() AS Reduced;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos geometry estáticos estendidos](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

