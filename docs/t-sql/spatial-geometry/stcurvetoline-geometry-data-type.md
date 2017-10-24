---
title: STCurveToLine (tipo de dados geometry) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveToLine method (geometry)
ms.assetid: abc80b32-4152-4e10-b816-798b901e0ac5
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2a0601e93e3763ca184ecf599da2cc7f9b36dd6f
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="stcurvetoline-geometry-data-type"></a>STCurveToLine (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Retorna uma aproximação poligonal de uma **geometria** instância que contém segmentos de arco circular.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STCurveToLine ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geometry**  
  
 Tipo de retorno CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Comentários  
 Retorna vazio **GeometryCollection**instância vazia **geometria** instância variáveis e retorna **nulo** para não inicializado **geometria** variáveis.  
  
 A aproximação poligonal que o método retorna depende de **geometria** instância que você usa para chamar o método:  
  
-   Retorna um **LineString** instância para uma **CircularString** ou **CompoundCurve** instância.  
  
-   Retorna um **polígono** instância para uma **CurvePolygon** instância.  
  
-   Retorna uma cópia do **geometria** instância se essa instância não é um **CircularString**, **CompoundCurve**, ou **CurvePolygon** instância . Por exemplo, o `STCurveToLine` método retorna um **ponto** instância para uma **geometria** instância que é um **ponto** instância.  
  
 Ao contrário da especificação SQL/MM, o `STCurveToLine` método não usa valores de coordenada z para calcular a aproximação poligonal. O método ignora quaisquer valores de coordenada z presentes na chamada **geometria** instância.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-an-uninitialized-geometry-variable-and-empty-instance"></a>A. Usando uma variável de geometria não inicializada e instância vazia  
 No exemplo a seguir, a primeira **selecione** instrução usa um não inicializada **geometria** instância para chamar o `STCurveToLine` método e o segundo **selecione** instrução usa vazio **geometria** instância. Assim, o método retorna **nulo** para a primeira instrução e um **GeometryCollection** coleção para a segunda instrução.  
  
```
 DECLARE @g geometry; 
 SET @g = @g.STCurveToLine(); 
 SELECT @g.STGeometryType(); 
 SET @g = geometry::Parse('LINESTRING EMPTY'); 
 SELECT @g.STGeometryType();
 ```  
  
### <a name="b-using-a-linestring-instance"></a>B. Usando uma instância de LineString  
 O **selecione** instrução no exemplo a seguir usa uma **LineString** instância para chamar o método STCurveToLine. Assim, o método retorna um **LineString** instância.  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('LINESTRING(1 3, 5 5, 4 3, 1 3)'); 
 SET @g = @g.STCurveToLine(); 
 SELECT @g.STGeometryType();
 ```  
  
### <a name="c-using-a-circularstring-instance"></a>C. Usando uma instância de CircularString  
 A primeira **selecione** instrução no exemplo a seguir usa uma **CircularString** instância para chamar o método STCurveToLine. Assim, o método retorna um **LineString** instância. Isso **selecione** instrução também compara os comprimentos das duas instâncias, que são aproximadamente os mesmos.  Por fim, a segunda **selecione** instrução retorna o número de pontos para cada instância.  Ele retorna apenas 5 pontos para a **CircularString** instância, mas 65 pontos para a **LineString**instância.  
  
```
 DECLARE @g1 geometry, @g2 geometry; 
 SET @g1 = geometry::Parse('CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0)'); 
 SET @g2 = @g1.STCurveToLine(); 
 SELECT @g1.STGeometryType() AS [G1 Type], @g2.STGeometryType() AS [G2 Type], @g1.STLength() AS [G1 Perimeter], @g2.STLength() AS [G2 Perimeter], @g2.ToString() AS [G2 Def]; 
 SELECT @g1.STNumPoints(), @g2.STNumPoints();
 ```  
  
### <a name="d-using-a-curvepolygon-instance"></a>D. Usando uma instância de CurvePolygon  
 O **selecione** instrução no exemplo a seguir usa uma **CurvePolygon** instância para chamar o método STCurveToLine. Assim, o método retorna um **polígono** instância.  
  
```
 DECLARE @g1 geometry, @g2 geometry; 
 SET @g1 = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0))'); 
 SET @g2 = @g1.STCurveToLine(); 
 SELECT @g1.STGeometryType() AS [G1 Type], @g2.STGeometryType() AS [G2 Type];
 ```  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral de tipos de dados espaciais](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [STLength &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stlength-geometry-data-type.md)   
 [STNumPoints &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stnumpoints-geometry-data-type.md)   
 [STGeometryType &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)  
  
  


