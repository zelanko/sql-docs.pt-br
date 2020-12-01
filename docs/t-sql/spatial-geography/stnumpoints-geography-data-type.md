---
description: STNumPoints (tipo de dados geography)
title: STNumPoints (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STNumPoints (geography Data Type)
- STNumPoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STNumPoints method
ms.assetid: 25ff7ad1-ba5f-4cfb-816a-59255ac1591d
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 6dbbf84ae21589d6428528d1599fe65eba7704f6
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88445144"
---
# <a name="stnumpoints-geography-data-type"></a>STNumPoints (tipo de dados geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna o número total de pontos em cada uma das figuras em uma instância de **geography**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STNumPoints ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **int**  
  
 Tipo de retorno do CLR: **SqlInt32**  
  
## <a name="remarks"></a>Comentários  
 Esse método conta os pontos na descrição de uma instância de **geography**. Pontos duplicados são contados. No entanto, os pontos de conexão entre segmentos são contados apenas uma vez. Se a instância for uma coleção, esse método retornará o número total de pontos na coleção.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-retrieving-the-total-number-of-points-in-a-linestring"></a>a. Recuperando o número total de pontos em um LineString  
 O exemplo a seguir cria uma instância `LineString` e usa `STNumPoints()`  para determinar quantos pontos foram usados na descrição da instância.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STNumPoints();  
```  
  
### <a name="b-retrieving-the-total-number-of-points-in-a-geometrycollection"></a>B. Recuperando o número total de pontos em um GeometryCollection  
 O exemplo a seguir retorna uma soma dos pontos de todos os elementos no `GeometryCollection`.  
  
```  
DECLARE @g geography = 'GEOMETRYCOLLECTION(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)  
    ,CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)))';  
SELECT @g.STNumPoints();  
```  
  
### <a name="c-returning-the-number-of-points-in-a-compoundcurve"></a>C. Retornando o número de pontos em um CompoundCurve  
 O exemplo a seguir retorna o número de pontos em uma instância de CompoundCurve. A consulta retorna 5 em vez de 6 porque STNumPoints() conta o ponto de conexão entre os segmentos apenas uma vez.  
  
```
 DECLARE @g geography = 'COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658),( -122.348 47.658, -121.56 48.12, -122.358 47.653))'  
 SELECT @g.STNumPoints();
 ```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos do OGC em instâncias de geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
