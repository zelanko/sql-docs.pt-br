---
title: STBoundary (tipo de dados geometry) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- STBoundary (geometry Data Type)
- STBoundary_TSQL
dev_langs: TSQL
helpviewer_keywords: STBoundary (geometry Data Type)
ms.assetid: f0551674-e6e8-4926-9038-df03f2c807d7
caps.latest.revision: "22"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9c7db74c44bd314d23c7452722159b769def5777
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="stboundary-geometry-data-type"></a>STBoundary (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna o limite de uma **geometria** instância.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STBoundary ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geometry**  
  
 Tipo de retorno CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
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
 [Métodos OGC em instâncias geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  
