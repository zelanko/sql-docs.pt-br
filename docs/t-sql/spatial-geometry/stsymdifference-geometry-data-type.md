---
title: STSymDifference (tipo de dados geometry) | Microsoft Docs
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
- STSymDifference_TSQL
- STSymDifference (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STSymDifference (geometry Data Type)
ms.assetid: 1d4cf35a-ca89-4aa4-ae30-e61a0ff18b53
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b83e2ef917f76f615588327c8a3c2721f30e347a
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="stsymdifference-geometry-data-type"></a>STSymDifference (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Retorna um objeto que representa todos os pontos que estão em uma **geometria** instância ou outro **geometria** instância, mas não os pontos que residem em ambas as instâncias.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STSymDifference ( other_geometry )  
```  
  
## <a name="arguments"></a>Argumentos  
 *other_geometry*  
 É outra **geometria** instância além da instância na qual `STSymDistance()` está sendo invocado.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geometry**  
  
 Tipo de retorno CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Comentários  
 Esse método sempre retornará nulo se as IDs de referência espaciais (SRIDs) da **geometria** instâncias não coincidem. O resultado poderá conter segmentos de arco circular apenas se as instâncias de entrada contiverem segmentos de arco circulares.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-computing-the-symmetric-difference-of-two-polygon-instances"></a>A. Computando a diferença simétrica de duas instâncias de Polígono  
 O exemplo a seguir usa `STSymDifference()` para computar a diferença simétrica entre duas instâncias de `Polygon`.  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 0 2, 2 2, 2 0, 0 0))', 0);  
SET @h = geometry::STGeomFromText('POLYGON((1 1, 3 1, 3 3, 1 3, 1 1))', 0);  
SELECT @g.STSymDifference(@h).ToString();  
```  
  
### <a name="b-computing-the-symmetric-difference-between-a-curvepolygon-and-a-polygon-instance"></a>B. Computando a diferença simétrica entre um CurvePolygon e uma instância de Polygon  
 O exemplo a seguir retorna um `GeometryCollection` que representa a diferença simétrica entre um `CurvePolygon` e um `Polygon`.  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON (CIRCULARSTRING (0 -4, 4 0, 0 4, -4 0, 0 -4))';  
 DECLARE @h geometry = 'POLYGON ((1 -1, 5 -1, 5 3, 1 3, 1 -1))';  
 SELECT @h.STSymDifference(@g).ToString();
 ```  
  
## <a name="c-using-stsymdifference-on-curvepolygon-instance-with-an-inscribed-polygon-instance"></a>C. Usando STSymDifference() em instância de CurvePolygon com uma instância de Polygon inscrita  
 O exemplo a seguir retorna uma instância de `CurvePolygon` com um anel `Polygon` interior que representa a diferença simétrica entre as duas instâncias comparadas.  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON (CIRCULARSTRING (0 -4, 4 0, 0 4, -4 0, 0 -4))';  
 DECLARE @h geometry = 'POLYGON ((1 -1, 2 -1, 2 1, 1 1, 1 -1))';  
 SELECT @h.STSymDifference(@g).ToString();
 ```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos do OGC em instâncias de geometria](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

