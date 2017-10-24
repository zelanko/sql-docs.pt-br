---
title: STConvexHull (tipo de dados geometry) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STConvexHull (geometry Data Type)
- STConvexHull_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STConvexHull (geometry Data Type)
ms.assetid: 60a520a6-1a7c-486b-8d91-34401edf6233
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7bfd196565b33604a02a68b1380f676e7e730c45
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="stconvexhull-geometry-data-type"></a>STConvexHull (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna um objeto que representa a superfície convexa de uma **geometria** instância.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STConvexHull ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geometry**  
  
 Tipo de retorno CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Comentários  
 `STConvexHull()`Retorna o menor polígono convexo que contém o determinado **geometria** instância. **Pontos de** ou **LineString** instâncias produzirá uma instância do mesmo tipo que o da entrada.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `STConvexHull()` para localizar a superfície convexa de uma instância `Polygon``geometry` não convexa.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 0 2, 1 1, 2 2, 2 0, 0 0))', 0);  
SELECT @g.STConvexHull().ToString();  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos do OGC em instâncias de geometria](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


