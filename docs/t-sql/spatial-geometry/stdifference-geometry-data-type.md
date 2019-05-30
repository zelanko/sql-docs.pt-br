---
title: STDifference (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STDifference_TSQL
- STDifference (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STDifference (geometry Data Type)
ms.assetid: 737f39bb-8750-4ffb-8594-23febc2f1075
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: f817c09333e895650760441f14d7967d0db120df
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65938997"
---
# <a name="stdifference-geometry-data-type"></a>STDifference (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna um objeto que representa os conjuntos de pontos de uma instância de **geometry** que não estão dentro de outra instância de **geometry**.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STDifference ( other_geometry )  
```  
  
## <a name="arguments"></a>Argumentos  
 *other_geometry*  
 É outra instância de **geography** que indica quais pontos devem ser removidos da instância na qual `STDifference()` está sendo invocado.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de retorno CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 Esse método sempre retornará nulo se as SRIDs (IDs de referência espacial) das instâncias de **geometry** não forem correspondentes.   O resultado poderá conter segmentos de arco circular apenas se as instâncias de entrada contiverem segmentos de arco circulares.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-computing-the-difference-between-two-polygon-instances"></a>A. Computando a diferença entre duas instâncias de polígono  
 O exemplo a seguir usa `STDifference()` para computar a diferença entre dois polígonos.  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 0 2, 2 2, 2 0, 0 0))', 0);  
SET @h = geometry::STGeomFromText('POLYGON((1 1, 3 1, 3 3, 1 3, 1 1))', 0);  
SELECT @g.STDifference(@h).ToString();  
```  
  
### <a name="b-invoking-stdifference-on-a-curvepolygon-instance"></a>B. Invocando STDifference() em uma instância de CurvePolygon  
 O exemplo seguinte usa STDifference () em uma instância de CurvePolygon.  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON (CIRCULARSTRING (0 -4, 4 0, 0 4, -4 0, 0 -4))';  
 DECLARE @h geometry = 'POLYGON ((1 -1, 5 -1, 5 3, 1 3, 1 -1))';  
 -- Note the different results returned by the two SELECT statements  
 SELECT @h.STDifference(@g).ToString(), @g.STDifference(@h).ToString();
 ```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos OGC em instâncias geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

