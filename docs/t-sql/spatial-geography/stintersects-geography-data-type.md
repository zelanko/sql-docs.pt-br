---
title: STIntersects (tipo de dados geography) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STIntersects (geography Data Type)
- STIntersects_TSQL
dev_langs: TSQL
helpviewer_keywords: STIntersects method
ms.assetid: c9db8b42-83c7-48c6-8963-fce54eb34c05
caps.latest.revision: "16"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d6ac913a6d199e1b72193431ad1198bcbba11b03
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="stintersects-geography-data-type"></a>STIntersects (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

  Retornará 1 se uma **geografia** instância intercepta outra **geografia** instância. Retornará 0 se isso não ocorrer.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STIntersects ( other_geography )  
```  
  
## <a name="arguments"></a>Argumentos  
 *other_geography*  
 É outra **geografia** instância a ser comparado com a instância na qual `STIntersects()` é invocado.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **bits**  
  
 Tipo de retorno CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Comentários  
 Esse método sempre retornará **nulo** se as IDs de referência espaciais (SRIDs) da **geografia** instâncias não coincidem.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `STIntersects()` para determinar se há interseção entre duas instâncias `geography`.  
  
```  
 DECLARE @g geography;  
 DECLARE @h geography;  
 SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
 SET @h = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
```  
  
 ```
 SELECT CASE @g.STIntersects(@h) 
 WHEN 1 THEN '@g intersects @h'  
 ELSE '@g does not intersect @h'  
 END;
 ```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos OGC em instâncias geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
