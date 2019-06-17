---
title: STStartPoint (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STStartPoint_TSQL
- STStartPoint (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STStartPoint method
ms.assetid: 7df18a5f-b9ee-4e36-b765-a0790c1dee3d
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: b2af68b46abc31d7025e0b8b03fa6b18f5e9403c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65939154"
---
# <a name="ststartpoint-geography-data-type"></a>STStartPoint (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna o ponto inicial de uma instância de **geography**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STStartPoint ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de retorno CLR: **SqlGeography**  
  
 Tipo OGC (Open Geospatial Consortium): **Ponto**  
  
## <a name="remarks"></a>Remarks  
 STStartPoint() é o equivalente a [STPointN](../../t-sql/spatial-geometry/stpointn-geometry-data-type.md)`(1)`.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância de `LineString` e usa `STStartPoint()` para recuperar o ponto inicial da instância.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STStartPoint().ToString();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos OGC em instâncias geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
