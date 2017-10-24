---
title: STBoundary (tipo de dados geometry) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STBoundary (geometry Data Type)
- STBoundary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STBoundary (geometry Data Type)
ms.assetid: f0551674-e6e8-4926-9038-df03f2c807d7
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a582d1c730fa8e11b6ddd684494588b69a01bf64
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="stboundary-geometry-data-type"></a>STBoundary (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna o limite de uma **geometria** instância.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STBoundary ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geometry**  
  
 Tipo de retorno CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Comentários  
 `STBoundary()`Retorna vazio **GeometryCollection** quando os pontos de extremidade para uma **LineString**, **CircularString**, ou **CompoundCurve** instância são os mesmos.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-stboundary-on-a-linestring-instance-with-different-endpoints"></a>A. Usando STBoundary() em uma instância de LineString com pontos de extremidade diferentes  
 O exemplo a seguir cria um `LineString``geometry` instância. `STBoundary()`Retorna o limite do `LineString`.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 0 2, 2 0)', 0);  
SELECT @g.STBoundary().ToString();  
```  
  
### <a name="b-using-stboundary-on-a-linestring-instance-with-the-same-endpoints"></a>B. Usando STBoundary() em uma instância de LineString com os mesmos pontos de extremidade  
 O exemplo a seguir cria uma instância de `LineString` válida com os mesmos pontos de extremidade. `STBoundary()` retorna uma `GeometryCollection` vazia.  
  
```
 DECLARE @g geometry;  
 SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 0 2, -2 2, 0 0)', 0);  
 SELECT @g.STBoundary().ToString();
 ```  
  
### <a name="c-using-stboundary-on-a-curvepolygon-instance"></a>C. Usando STBoundary() em uma instância de CurvePolygon  
 O exemplo a seguir usa a instância de `STBoundary()` em uma instância de `CurvePolygon`. `STBoundary()` retorna uma instância de `CircularString`.  
  
```
 DECLARE @g geometry;  
 SET @g = geometry::STGeomFromText('CURVEPOLYGON(CIRCULARSTRING(0 0, 2 2, 0 2, -2 2, 0 0))', 0);  
 SELECT @g.STBoundary().ToString();
 ```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos do OGC em instâncias de geometria](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

