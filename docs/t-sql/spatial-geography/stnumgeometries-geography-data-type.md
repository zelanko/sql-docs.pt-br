---
title: STNumGeometries (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STNumGeometries (geography Data Type)
- STNumGeometries_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STNumGeometries method
ms.assetid: 6ae7fac2-62f1-420f-9fc9-a09606be9605
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 978a7fd1d6e0f71a4552fdb8b003bb803453ac37
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86554701"
---
# <a name="stnumgeometries-geography-data-type"></a>STNumGeometries (tipo de dados geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna o número de **geometries** que compõem uma instância de **geography**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STNumGeometries ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **int**  
  
 Tipo de retorno do CLR: **SqlInt32**  
  
## <a name="remarks"></a>Comentários  
 Esse método retorna 1 se a instância de **geography** não é uma instância de **MultiPoint**, **MultiLineString**, **MultiPolygon** ou **GeometryCollection**, ou 0 se a instância de **geography** está vazia.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância de `MultiPoint` e usa `STNumGeometries()` para descobrir quantas **geometries** a instância contém.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('MULTIPOINT((-122.360 47.656), (-122.343 47.656))', 4326);  
SELECT @g.STNumGeometries();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos OGC em instâncias geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
