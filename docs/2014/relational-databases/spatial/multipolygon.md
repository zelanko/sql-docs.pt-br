---
title: MultiPolygon | Microsoft Docs
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- MultiPolygon geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 2c5db358-2a16-49d9-aac5-a74e86813932
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: ccb2689b24914a0a953c1b9f7325cd5aa9c75d0d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014116"
---
# <a name="multipolygon"></a>MultiPolygon
  Uma instância `MultiPolygon` é uma coleção de zero ou mais instâncias `Polygon`.  
  
## <a name="polygon-instances"></a>Instâncias de polígono  
 A ilustração a seguir mostra exemplos de instâncias `MultiPolygon`.  
  
 ![Exemplos das instâncias geométricas MultiPolygon](../../database-engine/media/multipolygon.gif "Exemplos das instâncias geométricas MultiPolygon")  
  
 Conforme mostrado na ilustração:  
  
-   A Figura 1 é uma instância `MultiPolygon` com dois elementos `Polygon`. O limite é definido pelos dois anéis exteriores e os três anéis interiores.  
  
-   A Figura 2 é uma instância `MultiPolygon` com dois elementos `Polygon`. O limite é definido pelos dois anéis exteriores e os três anéis interiores. Os dois elementos `Polygon` cruzam em um ponto de tangente.  
  
### <a name="accepted-instances"></a>Instâncias aceitas  
 Uma instância de `MultiPolygon` é aceita quando uma das condições a seguir é atendida.  
  
-   É uma instância de `MultiPolygon` vazia.  
  
-   Todas as instâncias que englobam a instância de `MultiPolygon` são instâncias de `Polygon` aceitas. Para obter mais informações sobre aceitas `Polygon` instâncias, consulte [polígono](../spatial/polygon.md).  
  
 Os exemplos a seguir mostram as instâncias de `MultiPolygon` aceitas.  
  
```  
DECLARE @g1 geometry = 'MULTIPOLYGON EMPTY';  
DECLARE @g2 geometry = 'MULTIPOLYGON(((1 1, 1 -1, -1 -1, -1 1, 1 1)),((1 1, 3 1, 3 3, 1 3, 1 1)))';  
DECLARE @g3 geometry = 'MULTIPOLYGON(((2 2, 2 -2, -2 -2, -2 2, 2 2)),((1 1, 3 1, 3 3, 1 3, 1 1)))';  
```  
  
 O exemplo a seguir mostra uma instância de MultiPolygon que emitirá um `System.FormatException`.  
  
```  
DECLARE @g geometry = 'MULTIPOLYGON(((1 1, 1 -1, -1 -1, -1 1, 1 1)),((1 1, 3 1, 3 3)))';  
```  
  
 A segunda instância no MultiPolygon é uma instância de LineString e não uma instância de Polygon aceita.  
  
### <a name="valid-instances"></a>Instâncias válidas  
 Uma instância de `MultiPolygon` será válida se for uma instância de `MultiPolygon` vazia ou se atender aos critérios a seguir.  
  
1.  Todas as instâncias que englobam a instância de `MultiPolygon` são instâncias de `Polygon` válidas. Para válido `Polygon` instâncias, consulte [polígono](../spatial/polygon.md).  
  
2.  Nenhuma das instâncias de `Polygon` que englobe a instância de `MultiPolygon` se sobreporá.  
  
 O exemplo a seguir mostra duas instâncias de `MultiPolygon` válidas e uma instância de `MultiPolygon` inválida.  
  
```  
DECLARE @g1 geometry = 'MULTIPOLYGON EMPTY';  
DECLARE @g2 geometry = 'MULTIPOLYGON(((1 1, 1 -1, -1 -1, -1 1, 1 1)),((1 1, 3 1, 3 3, 1 3, 1 1)))';  
DECLARE @g3 geometry = 'MULTIPOLYGON(((2 2, 2 -2, -2 -2, -2 2, 2 2)),((1 1, 3 1, 3 3, 1 3, 1 1)))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid();  
```  
  
 `@g2` é válido porque as duas instâncias `Polygon` tocam somente um ponto tangente. `@g3` não é válido porque os interiores das duas instâncias `Polygon` sobrepõem-se.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra a criação de uma instância de `geometry``MultiPolygon` e retorna o WKT (Well-Known Text) do segundo componente.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTIPOLYGON(((0 0, 0 3, 3 3, 3 0, 0 0), (1 1, 1 2, 2 1, 1 1)), ((9 9, 9 10, 10 9, 9 9)))');  
SELECT @g.STGeometryN(2).STAsText();  
```  
  
 Este exemplo cria uma instância `MultiPolygon` vazia.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTIPOLYGON EMPTY');  
```  
  
## <a name="see-also"></a>Consulte também  
 [Polygon](../spatial/polygon.md)   
 [STArea &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/starea-geometry-data-type)   
 [STCentroid &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stcentroid-geometry-data-type)   
 [STPointOnSurface &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stpointonsurface-geometry-data-type)   
 [Dados espaciais &#40;SQL Server&#41;](../spatial/spatial-data-sql-server.md)  
  
  
