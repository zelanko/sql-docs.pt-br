---
title: STAsBinary (tipo de dados geometry) | Microsoft Docs
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
- STAsBinary (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STAsBinary (geometry Data Type)
ms.assetid: 65353777-e3e6-461c-9504-ea4d83312692
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0dc8039808e3a2a83c576c384f1c2e8c6186c718
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="stasbinary-geometry-data-type"></a>STAsBinary (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna a representação WKB (Well-Known Binary) do OGC (Open Geospatial Consortium) de uma instância de geometria.  
 
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STAsBinary ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **varbinary (max)**  
  
 Tipo de retorno CLR: **SqlBytes**  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância `LineString` de geometria de (0,0) a (2,3) do texto. `STAsBinary()` retorna o resultado em WKB.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 3)', 0);  
SELECT @g.STAsBinary();  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos do OGC em instâncias de geometria](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

