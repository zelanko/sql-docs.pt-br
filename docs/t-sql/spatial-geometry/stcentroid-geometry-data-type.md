---
title: STCentroid (tipo de dados geometry) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STCentroid_TSQL
- STCentroid (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STCentroid (geometry Data Type)
ms.assetid: 4dc5a004-7a53-4cce-81dd-9f5e1dd0db78
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c34e8eb334190b72a560086a9d5e862ba6667dec
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="stcentroid-geometry-data-type"></a>STCentroid (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Retorna o centro Geométrico de uma **geometria** instância que consiste em um ou mais polígonos.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STCentroid ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geometry**  
  
 Tipo de retorno CLR: **SqlGeometry**  
  
 Abra o tipo Geospatial Consortium (OGC): **ponto**  
  
## <a name="remarks"></a>Comentários  
 `STCentroid()`retornará nulo se o **geometria** instância não é um **Polygon, CurvePolygon**, ou **MultiPolygon** tipo.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-computing-the-centroid-of-a-polygon-instance"></a>A. Calculando o centroide de uma instância de Polígono  
 O exemplo a seguir usa `STCentroid()` para calcular o centroide de uma `polygon``geometry` instância:  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0),(2 2, 2 1, 1 1, 1 2, 2 2))', 0);  
SELECT @g.STCentroid().ToString();  
```  
  
### <a name="b-computing-the-centroid-of-a-curvepolygon-instance"></a>B. Calculando o centroide de uma instância de CurvePolygon  
 O exemplo a seguir calcula o centroide de uma instância de `CurvePolygon`:  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(CIRCULARSTRING(0 4, 4 0, 8 4, 4 8, 0 4), CIRCULARSTRING(2 4, 4 2, 6 4, 4 6, 2 4))';  
 SELECT @g.STCentroid().ToString() AS Centroid
 ```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos do OGC em instâncias de geometria](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


