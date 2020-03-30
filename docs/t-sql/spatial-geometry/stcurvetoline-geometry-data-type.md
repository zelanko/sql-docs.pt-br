---
title: STCurveToLine (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveToLine method (geometry)
ms.assetid: abc80b32-4152-4e10-b816-798b901e0ac5
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 5bc1bdb1ece65113422af1e9a8ebe09de0db1fa1
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67930303"
---
# <a name="stcurvetoline-geometry-data-type"></a>STCurveToLine (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Retorna uma aproximação poligonal de uma instância de **geometry** que contém segmentos de arco circulares.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STCurveToLine ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de retorno do CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Comentários  
 Retorna uma instância de **GeometryCollection** vazia para variáveis da instância de **geometry** vazia e retorna **NULL** para variáveis de **geometry** não inicializadas.  
  
 A aproximação poligonal que o método retorna depende da instância de **geometry** que você usa para chamar o método:  
  
-   Retorna uma instância de **LineString** para uma instância de **CircularString** ou de **CompoundCurve**.  
  
-   Retorna uma instância de **Polygon** para uma instância de **CurvePolygon**.  
  
-   Retorna uma cópia da instância de **geometry** se essa instância não é uma instância de **CircularString**, **CompoundCurve** ou **CurvePolygon**. Por exemplo, o método `STCurveToLine` retorna uma instância de **Point** para uma instância de **geometry** que é uma instância de **Point**.  
  
 Ao contrário da especificação SQL/MM, o método `STCurveToLine` não usa valores da coordenada Z para calcular a aproximação poligonal. O método ignora os valores da coordenada Z presentes na instância de **geometry** de chamada.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-an-uninitialized-geometry-variable-and-empty-instance"></a>a. Usando uma variável de geometria não inicializada e instância vazia  
 No exemplo a seguir, a primeira instrução **SELECT** usa uma instância de **geometry** não inicializada para chamar o método `STCurveToLine` e a segunda instrução **SELECT** usa uma instância de **geometry** vazia. Portanto, o método retorna **NULL** para a primeira instrução e uma coleção **GeometryCollection** para a segunda.  
  
```
 DECLARE @g geometry; 
 SET @g = @g.STCurveToLine(); 
 SELECT @g.STGeometryType(); 
 SET @g = geometry::Parse('LINESTRING EMPTY'); 
 SELECT @g.STGeometryType();
 ```  
  
### <a name="b-using-a-linestring-instance"></a>B. Usando uma instância de LineString  
 A instrução **SELECT** no exemplo a seguir usa uma instância de **LineString** para chamar o método STCurveToLine. Portanto, o método retorna uma instância de **LineString**.  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('LINESTRING(1 3, 5 5, 4 3, 1 3)'); 
 SET @g = @g.STCurveToLine(); 
 SELECT @g.STGeometryType();
 ```  
  
### <a name="c-using-a-circularstring-instance"></a>C. Usando uma instância de CircularString  
 A primeira instrução **SELECT** no exemplo a seguir usa uma instância de **CircularString** para chamar o método STCurveToLine. Portanto, o método retorna uma instância de **LineString**. Esta instrução **SELECT** também compara os tamanhos das duas instâncias, que são aproximadamente os mesmos.  Finalmente, a segunda instrução **SELECT** retorna o número de pontos para cada instância.  Retorna apenas 5 pontos para a instância de **CircularString**, mas 65 pontos para a instância de **LineString**.  
  
```
 DECLARE @g1 geometry, @g2 geometry; 
 SET @g1 = geometry::Parse('CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0)'); 
 SET @g2 = @g1.STCurveToLine(); 
 SELECT @g1.STGeometryType() AS [G1 Type], @g2.STGeometryType() AS [G2 Type], @g1.STLength() AS [G1 Perimeter], @g2.STLength() AS [G2 Perimeter], @g2.ToString() AS [G2 Def]; 
 SELECT @g1.STNumPoints(), @g2.STNumPoints();
 ```  
  
### <a name="d-using-a-curvepolygon-instance"></a>D. Usando uma instância de CurvePolygon  
 A instrução **SELECT** no exemplo a seguir usa uma instância de **CurvePolygon** para chamar o método STCurveToLine. Portanto, o método retorna uma instância de **Polygon**.  
  
```
 DECLARE @g1 geometry, @g2 geometry; 
 SET @g1 = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0))'); 
 SET @g2 = @g1.STCurveToLine(); 
 SELECT @g1.STGeometryType() AS [G1 Type], @g2.STGeometryType() AS [G2 Type];
 ```  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral de tipos de dados espaciais](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [STLength &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stlength-geometry-data-type.md)   
 [STNumPoints &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stnumpoints-geometry-data-type.md)   
 [STGeometryType &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)  
  
  

