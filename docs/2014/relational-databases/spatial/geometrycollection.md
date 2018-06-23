---
title: GeometryCollection | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-spatial
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- GeomCollection geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 4445c0d9-a66b-4d7c-88e4-a66fa6f7d9fd
caps.latest.revision: 17
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 1a5c21c01ab776a17d3e160fee51167c426dfa0c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117629"
---
# <a name="geometrycollection"></a>GeometryCollection
  Um `GeometryCollection` é uma coleção de zero ou mais `geometry` ou `geography` instâncias. Um `GeometryCollection` pode estar vazio.  
  
## <a name="geometrycollection-instances"></a>Instâncias de GeometryCollection  
  
### <a name="accepted-instances"></a>Instâncias aceitas  
 Para que uma instância de `GeometryCollection` seja aceita, ela deve ser uma instância de `GeometryCollection` vazia ou todas as instâncias que englobam a instância de `GeometryCollection` devem ser instâncias aceitas. O exemplo a seguir mostra as instâncias aceitas.  
  
```  
DECLARE @g1 geometry = 'GEOMETRYCOLLECTION EMPTY';  
DECLARE @g2 geometry = 'GEOMETRYCOLLECTION(LINESTRING EMPTY,POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g3 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
```  
  
 O exemplo a seguir gera um `System.FormatException` porque o `LinesString` de instância de `GeometryCollection` instância não é aceito.  
  
```  
DECLARE @g geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1), POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
```  
  
### <a name="valid-instances"></a>Instâncias válidas  
 Uma instância de `GeometryCollection` é válida quando todas as instâncias que englobam a instância de `GeometryCollection` são válidas. A seguir mostra três válido `GeometryCollection` instâncias e uma instância que não é válida.  
  
```  
DECLARE @g1 geometry = 'GEOMETRYCOLLECTION EMPTY';  
DECLARE @g2 geometry = 'GEOMETRYCOLLECTION(LINESTRING EMPTY,POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g3 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g4 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, 1 -5, -5 5, -5 -1, -1 -1)))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();  
```  
  
 `@g4` não é válida porque a instância de `Polygon` na instância de `GeometryCollection` não é válida.  
  
 Para obter mais informações sobre instâncias aceitas e válidas, consulte [Point](point.md), [MultiPoint](multipoint.md), [LineString](linestring.md), [MultiLineString](multilinestring.md), [Polygon](polygon.md)e [MultiPolygon](multipolygon.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância de `geometry``GeometryCollection` com valores Z no SRID 1 contendo uma instância de `Point` e uma instância de `Polygon` .  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomCollFromText('GEOMETRYCOLLECTION(POINT(3 3 1), POLYGON((0 0 2, 1 10 3, 1 0 4, 0 0 2)))', 1);  
```  
  
## <a name="see-also"></a>Consulte também  
 [Dados espaciais &#40;SQL Server&#41;](spatial-data-sql-server.md)  
  
  