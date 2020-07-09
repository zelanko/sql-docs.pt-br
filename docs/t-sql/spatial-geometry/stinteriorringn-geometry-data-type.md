---
title: STInteriorRingN (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STInteriorRingN_TSQL
- STInteriorRingN (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STInteriorRingN (geometry Data Type)
ms.assetid: 47310f9f-2cdb-41e0-a6da-7c3cfbf139ac
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: a98567d42b701178f0996a82e563e5655a062dac
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85762452"
---
# <a name="stinteriorringn-geometry-data-type"></a>STInteriorRingN (tipo de dados geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Retorna o anel interior especificado de uma instância de **Polygongeometry**.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STInteriorRingN ( expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 É uma expressão **int** entre 1 e o número de anéis interiores na instância de **geometry**.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de retorno do CLR: **SqlGeometry**  
  
 Tipo do OGC (Open Geospatial Consortium): **LineString**  
  
## <a name="remarks"></a>Comentários  
 Esse método retorna **nulo** se a instância de **geometry** não é um polígono. Esse método também gerará uma **ArgumentOutOfRangeException** se a expressão for maior que o número de anéis. O número de anéis pode ser retornado com o uso de `STNumInteriorRing``()`.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância de `Polygon` e usa `STInteriorRingN()` para retornar o anel interior do polígono como uma **LineString**.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0),(2 2, 2 1, 1 1, 1 2, 2 2))', 0);  
SELECT @g.STInteriorRingN(1).ToString();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos OGC em instâncias geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

