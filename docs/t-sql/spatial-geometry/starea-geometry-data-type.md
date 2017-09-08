---
title: STArea (tipo de dados geometry) | Microsoft Docs
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
- STArea (geometry Data Type)
- STArea_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STArea (geometry Data Type)
ms.assetid: a7dd6083-c649-4ac3-885d-1234e0db62f1
caps.latest.revision: 25
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5ec0a874d0dc2dd8bb37ce7e04fe71cbea85f860
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="starea-geometry-data-type"></a>STArea (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Retorna a área da superfície total de um **geometria** instância.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STArea ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **float**  
  
 Tipo de retorno CLR: **SqlDouble**  
  
## <a name="remarks"></a>Comentários  
 `STArea()`Retorna 0 se uma **geometria** instância contiver apenas figuras dimensionais 0 e 1-, ou se ela estiver vazia. `STArea()`Retorna **nulo** se o **geometria** instância não foi inicializada.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-computing-the-area-of-a-polygon-instance"></a>A. Computando a área de uma instância de Polígono  
 O exemplo a seguir cria um `Polygon``geometry` de instância e calcula a área do polígono.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0),(2 2, 2 1, 1 1, 1 2, 2 2))', 0);  
SELECT @g.STArea();  
```  
  
### <a name="b-computing-the-area-of-a-curvepolygon-instance"></a>B. Computando a área de uma instância de CurvePolygon  
 O exemplo a seguir calcula a área de uma instância de `CurvePolygon`.  
  
 `DECLARE @g geometry;`  
  
 `SET @g = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(0 2, 2 0, 4 2, 4 2, 0 2))');`  
  
 `SELECT @g.STArea() AS Area;`  
  
## <a name="see-also"></a>Consulte também  
 [Métodos do OGC em instâncias de geometria](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

