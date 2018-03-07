---
title: STNumPoints (tipo de dados geometry) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- STNumPoints_TSQL
- STNumPoints (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STNumPoints (geometry Data Type)
ms.assetid: a19520fc-7f91-4a2c-856f-4d8b99a7e496
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 51e08f456377ecef45bd26fc53a7a546c95220fb
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="stnumpoints-geometry-data-type"></a>STNumPoints (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Retorna a soma do número de pontos em cada uma das figuras em uma **geometria** instância.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STNumPoints ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **int**  
  
 Tipo de retorno CLR: **SqlInt32**  
  
## <a name="remarks"></a>Remarks  
 Esse método conta os pontos na descrição de um **geometria** instância. Pontos duplicados são contados. Se esta instância for um **coleção** tipo, esse método retorna a soma dos pontos em cada um de seus elementos.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância `LineString` e usa `STNumPoints()`  para determinar quantos pontos foram usados na descrição da instância.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STNumPoints();  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos OGC em instâncias geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  
