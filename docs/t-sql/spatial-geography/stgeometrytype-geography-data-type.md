---
title: STGeometryType (tipo de dados geography) | Microsoft Docs
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
- STGeometryType (geography Data Type)
- STGeometryType_TSQL
dev_langs: TSQL
helpviewer_keywords: STGeometryType method
ms.assetid: 3e169ead-a98e-44af-8d33-fd59a955cae4
caps.latest.revision: "17"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7d77afb909987ce56d7922116a954c4f94751bea
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="stgeometrytype-geography-data-type"></a>STGeometryType (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna o nome do tipo Open Geospatial Consortium (OGC) representado por um **geografia** instância.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STGeometryType ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **nvarchar (4000)**  
  
 Tipo de retorno CLR: **SqlString**  
  
## <a name="remarks"></a>Remarks  
 Os nomes de tipo OGC que podem ser retornados por `STGeometryType()` são **ponto**, **LineString**, **CircularString**, **CompoundCurve**, **Polígono**, **CurvePolygon**, **GeometryCollection**, **MultiPoint**, **MultiLineString**, e **MultiPolygon**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância de `Polygon` e usa `STGeometryType()` para confirmar que este é um polígono.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SELECT @g.STGeometryType();  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos OGC em instâncias geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
