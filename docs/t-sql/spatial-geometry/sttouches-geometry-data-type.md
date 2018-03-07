---
title: STTouches (tipo de dados geometry) | Microsoft Docs
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
- STTouches (geometry Data Type)
- STTouches_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STTouches (geometry Data Type)
ms.assetid: af3650b4-26da-4600-9cc2-1be71dd76a14
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5be445ecd219fa681a8c2fcc97ab80c4bb12c2f2
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="sttouches-geometry-data-type"></a>STTouches (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retornará 1 se uma **geometria** instância toca espacialmente outra **geometria** instância. Retornará 0 se isso não ocorrer.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STTouches ( other_geometry )  
```  
  
## <a name="arguments"></a>Argumentos  
 *other_geometry*  
 É outra **geometria** instância a ser comparada com a instância na qual `STTouches()` é invocado.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **bits**  
  
 Tipo de retorno CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 Dois **geometria** instâncias touch se interseção de seus conjuntos de pontos, mas não se cruzam seus interiores.  
  
 Esse método sempre retornará nulo se as IDs de referência espaciais (SRIDs) da **geometria** instâncias não coincidem.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `STTouches()` para testar duas instâncias `geometry` e consultar se elas se encontram.  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 2 0, 4 2)', 0);  
SET @h = geometry::STGeomFromText('POINT(1 1)', 0);  
SELECT @g.STTouches(@h);  
```  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral de índices espaciais](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [Métodos OGC em instâncias geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

