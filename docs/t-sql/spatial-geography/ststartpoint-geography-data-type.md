---
title: STStartPoint (tipo de dados geography) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STStartPoint_TSQL
- STStartPoint (geography Data Type)
dev_langs: TSQL
helpviewer_keywords: STStartPoint method
ms.assetid: 7df18a5f-b9ee-4e36-b765-a0790c1dee3d
caps.latest.revision: "13"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2feca278967f4fe7bdacf2da9c21f0f1a2cc59c5
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="ststartpoint-geography-data-type"></a>STStartPoint (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna o ponto inicial de um **geografia** instância.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STStartPoint ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geografia**  
  
 Tipo de retorno CLR: **SqlGeography**  
  
 Abra o tipo Geospatial Consortium (OGC): **ponto**  
  
## <a name="remarks"></a>Comentários  
 STStartPoint() é o equivalente de [STPointN](../../t-sql/spatial-geometry/stpointn-geometry-data-type.md)`(1)`.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância de `LineString` e usa `STStartPoint()` para recuperar o ponto inicial da instância.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STStartPoint().ToString();  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos OGC em instâncias geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
