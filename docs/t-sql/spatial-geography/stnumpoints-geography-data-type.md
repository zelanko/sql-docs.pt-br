---
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
manager: craigg
ms.openlocfilehash: 92fa22099ef88861986be34832d3bde1165d2d77
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65935739"
---
# <a name="stnumpoints-geography-data-type"></a>STNumPoints (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna o número total de pontos em cada uma das figuras em uma instância de **geography**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STNumPoints ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **int**  
  
 Tipo de retorno CLR: **SqlInt32**  
  
## <a name="remarks"></a>Remarks  
 Esse método conta os pontos na descrição de uma instância de **geography**. Pontos duplicados são contados. No entanto, os pontos de conexão entre segmentos são contados apenas uma vez. Se a instância for uma coleção, esse método retornará o número total de pontos na coleção.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-retrieving-the-total-number-of-points-in-a-linestring"></a>A. Recuperando o número total de pontos em um LineString  
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
 [Métodos OGC em instâncias geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
