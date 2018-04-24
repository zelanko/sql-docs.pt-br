---
title: MultiPoint | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: spatial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-spatial
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- MultiPoint geometry subtype [SQL Server]
ms.assetid: 2aaab211-3aba-4dbd-90b7-095d997b1f62
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f5e2ec469c2429c6e1e97862048a9465e39e4449
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="multipoint"></a>MultiPoint
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Um **MultiPoint** é uma coleção de zero ou mais pontos. O limite de uma instância **MultiPoint** é vazio.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância `geometry MultiPoint` com SRID 23 e dois pontos: um ponto com as coordenadas (2, 3), um ponto com as coordenadas (7, 8) e um valor Z de 9,5.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('MULTIPOINT((2 3), (7 8 9.5))', 23);  
```  
  
 Essa instância `MultiPoint` também pode ser expressada usando `STMPointFromText()` conforme mostrado a seguir.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STMPointFromText('MULTIPOINT((2 3), (7 8 9.5))', 23);  
```  
  
 O exemplo a seguir usa o método `STGeometryN()` para recuperar uma descrição do primeiro ponto na coleção.  
  
```  
SELECT @g.STGeometryN(1).STAsText();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Ponto](../../relational-databases/spatial/point.md)   
 [Dados espaciais &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
