---
title: STAsBinary (tipo de dados geography) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STAsBinary_TSQL
- STAsBinary (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STAsBinary method
ms.assetid: 99602a62-265d-4aa4-a8dc-92992ca55ba4
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c48fc48b7af524e980801a11ac2574f2091823a2
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="stasbinary-geography-data-type"></a>STAsBinary (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Retorna a representação do Open Geospatial Consortium (OGC) Well-Known Binary (WKB) de um **geografia** instância.  
  
 Isso **geografia** método dá suporte ao tipo de dados **FullGlobe** instâncias ou a instâncias espaciais maiores que um hemisfério.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STAsBinary ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **varbinary (max)**  
  
 Tipo de retorno CLR: **SqlBytes**  
  
## <a name="remarks"></a>Comentários  
 O tipo OGC de uma **geografia** instância pode ser determinada invocando [stgeometrytype ()](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `STAsBinary()` para criar um `LineString``geography` da instância de (-122.360, 47.656) a (-122.343, -47.656) de texto. Retorna, então, o resultado em WKB.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING( -122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STAsBinary();  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos do OGC em instâncias de Geografia](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  

