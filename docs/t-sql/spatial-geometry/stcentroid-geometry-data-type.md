---
title: STCentroid (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STCentroid_TSQL
- STCentroid (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STCentroid (geometry Data Type)
ms.assetid: 4dc5a004-7a53-4cce-81dd-9f5e1dd0db78
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 3693c6a80c6482ec6677a21983f53d338da500f9
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65939063"
---
# <a name="stcentroid-geometry-data-type"></a>STCentroid (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Retorna o centro geométrico de uma instância de **geometry** que consiste em um ou mais polígonos.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STCentroid ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de retorno CLR: **SqlGeometry**  
  
 Tipo OGC (Open Geospatial Consortium): **Ponto**  
  
## <a name="remarks"></a>Remarks  
 `STCentroid()` retorna nulo se a instância de **geometry** não é um tipo **Polygon, CurvePolygon** ou **MultiPolygon**.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-computing-the-centroid-of-a-polygon-instance"></a>A. Calculando o centroide de uma instância de Polígono  
 O seguinte exemplo usa `STCentroid()` para calcular o centroide de uma instância de `polygon``geometry`:  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Métodos OGC em instâncias geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

