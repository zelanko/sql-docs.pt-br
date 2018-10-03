---
title: STArea (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STArea (geometry Data Type)
- STArea_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STArea (geometry Data Type)
ms.assetid: a7dd6083-c649-4ac3-885d-1234e0db62f1
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1e5ecf4856cc0fd2e17e56c876cf40d0bb1db9b9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47719594"
---
# <a name="starea-geometry-data-type"></a>STArea (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Retorna uma área de superfície total de uma instância de **geometry**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STArea ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
 Tipo de retorno do CLR: **SqlDouble**  
  
## <a name="remarks"></a>Remarks  
 `STArea()` retorna 0 se uma instância de **geometry** contém apenas valores dimensionais 0- e 1- ou se ela está vazia. `STArea()` retorna **NULL** se a instância de **geometry** não foi inicializada.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-computing-the-area-of-a-polygon-instance"></a>A. Computando a área de uma instância de Polígono  
 O exemplo a seguir cria uma instância de `Polygon``geometry` e calcula a área do polígono.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0),(2 2, 2 1, 1 1, 1 2, 2 2))', 0);  
SELECT @g.STArea();  
```  
  
### <a name="b-computing-the-area-of-a-curvepolygon-instance"></a>B. Computando a área de uma instância de CurvePolygon  
 O exemplo a seguir calcula a área de uma instância de `CurvePolygon`.  
  
```
 DECLARE @g geometry;  
 SET @g = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(0 2, 2 0, 4 2, 4 2, 0 2))');  
 SELECT @g.STArea() AS Area;
 ```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos OGC em instâncias geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  
