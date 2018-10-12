---
title: STGeometryType (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STGeometryType (geography Data Type)
- STGeometryType_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STGeometryType method
ms.assetid: 3e169ead-a98e-44af-8d33-fd59a955cae4
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d4f721d552f40fcbb1fe2ae8daac8031c437d35c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47765374"
---
# <a name="stgeometrytype-geography-data-type"></a>STGeometryType (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna o nome do tipo do OGC (Open Geospatial Consortium) representado por uma instância de **geography**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STGeometryType ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **nvarchar(4000)**  
  
 Tipo de retorno do CLR: **SqlString**  
  
## <a name="remarks"></a>Remarks  
 Os nomes de tipo do OGC que podem ser retornados por `STGeometryType()` são **Point**, **LineString**, **CircularString**, **CompoundCurve**, **Polygon**, **CurvePolygon**, **GeometryCollection**, **MultiPoint**, **MultiLineString**, **MultiPolygon** e **FullGlobe**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância de `Polygon` e usa `STGeometryType()` para confirmar que este é um polígono.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SELECT @g.STGeometryType();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos OGC em instâncias geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
