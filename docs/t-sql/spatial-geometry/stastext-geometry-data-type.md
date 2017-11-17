---
title: STAsText (tipo de dados geometry) | Microsoft Docs
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
- STAsText_TSQL
- STAsText (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STAsText (geometry Data Type)
ms.assetid: e0decf5e-2858-4c56-b61a-6123f47fb51c
caps.latest.revision: 25
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 127e64908ad9cb768d31e3c1ec42988962289246
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="stastext-geometry-data-type"></a>STAsText (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Retorna a representação de texto do Open Geospatial Consortium (OGC) conhecido (WKT) de um **geometria** instância. Esse texto não conterá nenhum valor Z (elevação) ou M (medida) executado pela instância.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STAsText ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **nvarchar (max)**  
  
 Tipo de retorno CLR: **SqlChars**  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância `LineString` de geometria de (0,0) a (2,3) do texto. `STAsText()` retorna o resultado em texto.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 3)', 0);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos do OGC em instâncias de geometria](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


