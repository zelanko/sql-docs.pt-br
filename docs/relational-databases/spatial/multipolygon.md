---
title: MultiPolygon | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-spatial
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MultiPolygon geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 2c5db358-2a16-49d9-aac5-a74e86813932
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 06a27579c5e54406093daf4eb318c2e004a9763b
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="multipolygon"></a>MultiPolygon
  Uma instância **MultiPolygon** é uma coleção de zero ou mais instâncias **Polygon** .  
  
## <a name="polygon-instances"></a>Instâncias de polígono  
 A ilustração a seguir mostra exemplos de instâncias **MultiPolygon** .  
  
 ![Exemplos das instâncias geométricas MultiPolygon](../../relational-databases/spatial/media/multipolygon.gif "Exemplos das instâncias geométricas MultiPolygon")  
  
 Conforme mostrado na ilustração:  
  
-   A Figura 1 é uma instância **MultiPolygon** com dois elementos **Polygon** . O limite é definido pelos dois anéis exteriores e os três anéis interiores.  
  
-   A Figura 2 é uma instância **MultiPolygon** com dois elementos **Polygon** . O limite é definido pelos dois anéis exteriores e os três anéis interiores. Os dois elementos **Polygon** cruzam em um ponto de tangente.  
  
### <a name="accepted-instances"></a>Instâncias aceitas  
 Uma instância de **MultiPolygon** é aceita quando uma das condições a seguir é atendida.  
  
-   Ela é uma instância **MultiPolygon** vazia.  
  
-   Todas as instâncias que englobam a instância de **MultiPolygon** são instâncias de **Polygon** aceitas. Para obter mais informações sobre instâncias de **Polygon** aceitas, consulte [Polygon](../../relational-databases/spatial/polygon.md).  
  
 Os exemplos a seguir mostram as instâncias de **MultiPolygon** aceitas.  
  
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
 Uma instância de **MultiPolygon** será válida se for uma instância de **MultiPolygon** vazia ou se atender aos critérios a seguir.  
  
1.  Todas as instâncias que englobam a instância de **MultiPolygon** são instâncias de **Polygon** válidas. Para instâncias de **Polygon** válidas, consulte [Polygon](../../relational-databases/spatial/polygon.md).  
  
2.  Nenhuma das instâncias de **Polygon** que englobam a sobreposição da instância de **MultiPolygon** .  
  
 O exemplo a seguir mostra duas instâncias de **MultiPolygon** válidas e uma instância de **MultiPolygon** inválida.  
  
```  
DECLARE @g1 geometry = 'MULTIPOLYGON EMPTY';  
DECLARE @g2 geometry = 'MULTIPOLYGON(((1 1, 1 -1, -1 -1, -1 1, 1 1)),((1 1, 3 1, 3 3, 1 3, 1 1)))';  
DECLARE @g3 geometry = 'MULTIPOLYGON(((2 2, 2 -2, -2 -2, -2 2, 2 2)),((1 1, 3 1, 3 3, 1 3, 1 1)))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid();  
```  
  
 `@g2` é válido porque as duas instâncias **Polygon** se tocam somente em um ponto tangente. `@g3` não é válido porque os interiores das duas instâncias de **Polygon** sobrepõem-se.  
  
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
 [Polygon](../../relational-databases/spatial/polygon.md)   
 [STArea &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/starea-geometry-data-type.md)   
 [STCentroid &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stcentroid-geometry-data-type.md)   
 [STPointOnSurface &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stpointonsurface-geometry-data-type.md)   
 [Dados espaciais &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
