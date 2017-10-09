---
title: STIntersection (tipo de dados geometry) | Microsoft Docs
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
- STIntersection_TSQL
- STIntersection (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STIntersection (geometry Data Type)
ms.assetid: 354843f5-cc14-478c-974a-04f363f9530f
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: accdd0fe059521ec45beeb386db6bfa34e66ccc0
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="stintersection-geometry-data-type"></a>STIntersection (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna um objeto que representa os pontos onde uma **geometria** instância intercepta outra **geometria** instância.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STIntersection ( other_geometry )  
```  
  
## <a name="arguments"></a>Argumentos  
 *other_geometry*  
 É outra **geometria** instância a ser comparado com a instância na qual `STIntersection()` está sendo invocado para determinar o local da interseção.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geometry**  
  
 Tipo de retorno CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Comentários  
 `STIntersection()`sempre retornará nulo se as IDs de referência espaciais (SRIDs) da **geometria** instâncias não coincidem. O resultado poderá conter segmentos de arco circular apenas se as instâncias de entrada contêm.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-stintersection-on-polygon-instances"></a>A. Usando STIntersection() em instâncias de Polygon  
 O exemplo a seguir usa `STIntersection()` para computar a interseção de dois polígonos.  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 0 2, 2 2, 2 0, 0 0))', 0);  
SET @h = geometry::STGeomFromText('POLYGON((1 1, 3 1, 3 3, 1 3, 1 1))', 0);  
SELECT @g.STIntersection(@h).ToString();  
```  
  
### <a name="b-using-stintersection-with-curvepolygon-instance"></a>B. Usando STIntersection() com instância de CurvePolygon  
 O exemplo a seguir retorna uma instância que contém um segmento de arco circular.  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON (CIRCULARSTRING (0 -4, 4 0, 0 4, -4 0, 0 -4))';  
 DECLARE @h geometry = 'POLYGON ((1 -1, 5 -1, 5 3, 1 3, 1 -1))';  
 SELECT @h.STIntersection(@g).ToString();
 ```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos do OGC em instâncias de geometria](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


