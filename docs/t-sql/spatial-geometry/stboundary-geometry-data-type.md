---
title: STBoundary (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STBoundary (geometry Data Type)
- STBoundary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STBoundary (geometry Data Type)
ms.assetid: f0551674-e6e8-4926-9038-df03f2c807d7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 234745a66d37083599f30243ab7974550193e5b2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47779115"
---
# <a name="stboundary-geometry-data-type"></a>STBoundary (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna o limite de uma instância de **geometry**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STBoundary ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de retorno do CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 `STBoundary()` retorna uma **GeometryCollection** vazia quando os pontos de extremidade de uma instância de **LineString**, **CircularString** ou **CompoundCurve** são os mesmos.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-stboundary-on-a-linestring-instance-with-different-endpoints"></a>A. Usando STBoundary() em uma instância de LineString com pontos de extremidade diferentes  
 O exemplo a seguir cria uma instância de `LineString``geometry`. `STBoundary()` retorna o limite de `LineString`.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Métodos OGC em instâncias geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  
