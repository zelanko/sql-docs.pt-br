---
title: STEnvelope (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- STEnvelope_TSQL
- STEnvelope (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STEnvelope (geometry Data Type)
ms.assetid: 781d22e9-38df-4c23-836f-6dd0bdef49c5
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 286748d81fc33a0d09a1b9eb99af1baeb9a09d21
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="stenvelope-geometry-data-type"></a>STEnvelope (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna o retângulo delimitador mínimo alinhado por eixo da instância.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
STEnvelope ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de retorno do CLR: **SqlGeometry**  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `STGeomFromText()` para criar uma instância de `LineString` de (0.0) a (2.3) e usa `STEnvelope()` para retornar a caixa delimitadora de `LineString`.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 3)', 0);  
SELECT @g.STEnvelope().ToString();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos OGC em instâncias geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

