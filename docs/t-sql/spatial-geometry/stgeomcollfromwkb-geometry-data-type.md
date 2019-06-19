---
title: STGeomCollFromWKB (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STGeomCollFromWKB (geometry Data Type)
- STGeomCollFromWKB_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STGeomCollFromWKB (geometry Data Type)
ms.assetid: 6c55032c-7f5e-4181-8e67-c0265032db63
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 4177e4b5d41352d511743c422864454a889771b4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65938907"
---
# <a name="stgeomcollfromwkb-geometry-data-type"></a>STGeomCollFromWKB (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna uma instância de **geometrycollection** de uma representação WKB (Well-Known Binary) do OGC (Open Geospatial Consortium).
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
STGeomCollFromWKB ( 'WKB_geometrycollection' , SRID )  
```  
  
## <a name="arguments"></a>Argumentos  
 *WKB_geometrycollection*  
 É a representação WKB da instância de **geometrycollection** que você deseja retornar. *WKB_geometrycollection* é uma expressão **varbinary(max)** .  
  
 *SRID*  
 É uma expressão **int** que representa a SRID (ID de referência espacial) da instância de **geometry** que você deseja retornar.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de retorno CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 O tipo do OGC da instância de **geometry** retornada por `STGeomCollFromWKB()` é definido como **GeomCollection**, **MultiPolygon**, **MultiLineString** ou **MultiPoint**, dependendo da entrada de WKB correspondente.  
  
 Este método lançará uma exceção FormatException se a entrada não estiver bem formatada.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `STGeomCollFromWKB()` para criar uma instância de **geometry**.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomCollFromWKB(0x0107000000020000000103000000010000000400000000000000000014400000000000001440000000000000244000000000000014400000000000002440000000000000244000000000000014400000000000001440010100000000000000000024400000000000002440, 0);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos geometry estáticos OGC](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
