---
title: STInteriorRingN (tipo de dados geometry) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STInteriorRingN_TSQL
- STInteriorRingN (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STInteriorRingN (geometry Data Type)
ms.assetid: 47310f9f-2cdb-41e0-a6da-7c3cfbf139ac
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a973ba1a1f3092c6a973ce4db0b5188615075922
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="stinteriorringn-geometry-data-type"></a>STInteriorRingN (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna o anel interior especificado de uma **Polygongeometry** instância.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STInteriorRingN ( expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 É um **int** expressão entre 1 e o número de anéis interiores no **geometria** instância.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geometry**  
  
 Tipo de retorno CLR: **SqlGeometry**  
  
 Abra o tipo Geospatial Consortium (OGC): **LineString**  
  
## <a name="remarks"></a>Comentários  
 Este método retorna **nulo** se o **geometria** instância não é um polígono. Esse método também lançará um **ArgumentOutOfRangeException** se a expressão for maior do que o número de anéis. O número de anéis pode ser retornado usando `STNumInteriorRing``()`.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria um `Polygon` instância e usa `STInteriorRingN()` para retornar o anel interior do polígono como uma **LineString**.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0),(2 2, 2 1, 1 1, 1 2, 2 2))', 0);  
SELECT @g.STInteriorRingN(1).ToString();  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos do OGC em instâncias de geometria](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


