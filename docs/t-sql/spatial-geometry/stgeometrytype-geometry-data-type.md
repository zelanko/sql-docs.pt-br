---
title: STGeometryType (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STGeometryType_TSQL
- STGeometryType (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STGeometryType (geometry Data Type)
ms.assetid: 224cdc83-aa83-4ad4-bb82-b7481031e910
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: a90fc5bc9f86f475d68ce3c07544969e91b46e46
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65938905"
---
# <a name="stgeometrytype-geometry-data-type"></a>STGeometryType (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna o nome do tipo do OGC (Open Geospatial Consortium) representado por uma instância de **geometry**.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STGeometryType ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **nvarchar(4000)**  
  
 Tipo de retorno CLR: **SqlString**  
  
## <a name="remarks"></a>Remarks  
 Os nomes de tipo do OGC que podem ser retornados por `STGeometryType()` são **Point**, **LineString**, **CircularString**, **CompoundCurve**, **Polígono, CurvePolygon**, **GeometryCollection**, **MultiPoint**, **MultiLineString** e  **MultiPolygon**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância de `Polygon` e usa `STGeometryType()` para confirmar que este é um polígono.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0))', 0);  
SELECT @g.STGeometryType();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos OGC em instâncias geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

