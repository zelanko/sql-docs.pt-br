---
title: STConvexHull (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STConvexHull (geometry Data Type)
- STConvexHull_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STConvexHull (geometry Data Type)
ms.assetid: 60a520a6-1a7c-486b-8d91-34401edf6233
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: c8e05b92fdbbcfb34d4e1eb82c4bf159d911b628
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86555619"
---
# <a name="stconvexhull-geometry-data-type"></a>STConvexHull (tipo de dados geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Retorna um objeto que representa a envoltória convexa de uma instância de **geometry**.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STConvexHull ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de retorno do CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Comentários  
 `STConvexHull()` retorna o polígono convexo menor que contém a instância de **geometry** especificada. As instâncias de **Points** ou **LineString** colineares gerarão uma instância do mesmo tipo da entrada.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `STConvexHull()` para localizar a superfície convexa de uma instância `Polygon``geometry` não convexa.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 0 2, 1 1, 2 2, 2 0, 0 0))', 0);  
SELECT @g.STConvexHull().ToString();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos OGC em instâncias geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

