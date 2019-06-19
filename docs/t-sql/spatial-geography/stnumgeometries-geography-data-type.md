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
manager: craigg
ms.openlocfilehash: 1a5cf36976538bc264ec96ea7a3f5835dc9ad9bf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65935735"
---
# <a name="stnumgeometries-geography-data-type"></a>STNumGeometries (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna o número de **geometries** que compõem uma instância de **geography**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STNumGeometries ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **int**  
  
 Tipo de retorno CLR: **SqlInt32**  
  
## <a name="remarks"></a>Remarks  
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
  
  
