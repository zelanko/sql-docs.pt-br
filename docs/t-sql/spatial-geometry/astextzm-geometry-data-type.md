---
title: AsTextZM (tipo de dados geometry) | Microsoft Docs
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
- AsTextZM_TSQL
- AsTextZM
- AsTextZM (geometry Data Type)
- AsTextZM_(geometry_Data_Type)_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- AsTextZM (geometry Data Type)
ms.assetid: 08ac8aa0-aff7-4b22-87e0-1a1d55dcbc04
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 91f77bd684d79bbef2530307aa65fc0d92b91c5e
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="astextzm-geometry-data-type"></a>AsTextZM (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna a representação de texto do Open Geospatial Consortium (OGC) conhecido (WKT) de uma instância de geometria, aumentada com qualquer **Z** (elevação) e **M** (medida) transportado pela instância.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.AsTextZM ()  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **nvarchar (max)**  
  
 Tipo de retorno CLR: **SqlChars**  
  
## <a name="remarks"></a>Comentários  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria um `Point` instância que contém **Z** (elevação) e **M** valores (medida). `STAsText()`Seleciona os valores WKT, (1, 2); `AsTextZM()` seleciona os mesmos valores WKT e também retorna os valores para **Z** e **M**, produzindo (1 2 3 4).  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(1 2 3 4)', 0);  
SELECT @g.STAsText();  
SELECT @g.AsTextZM();  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos estendidos em instâncias de geometria](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [M &#40; tipo de dados geometry &#41;](../../t-sql/spatial-geometry/m-geometry-data-type.md)   
 [Z &#40; tipo de dados geometry &#41;](../../t-sql/spatial-geometry/z-geometry-data-type.md)  
  
  


