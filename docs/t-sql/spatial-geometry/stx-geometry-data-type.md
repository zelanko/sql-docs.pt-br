---
title: STX (tipo de dados geometry) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2017
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
- STX (geometry Data Type)
- STX_TSQL
dev_langs: TSQL
helpviewer_keywords: STX (geometry Data Type)
ms.assetid: 2aef77e8-0460-43f9-bad6-2aae6d8c36f9
caps.latest.revision: "22"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: be3ec1bf7941113ddd2d21612fffd7eb8f331b78
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="stx-geometry-data-type"></a>STX (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

A propriedade de coordenada X de um **ponto**instância.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STX  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo: **float**  
  
 Tipo CLR: **SqlDouble**  
  
## <a name="remarks"></a>Remarks  
 O valor dessa propriedade será nulo se o **geometria** instância não é um ponto.  
  
 Esta propriedade é somente leitura.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância de `Point` e usa `STX` para recuperar a coordenada X da instância.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(3 8)', 0);  
SELECT @g.STX;  
```  
  
## <a name="see-also"></a>Consulte também  
 [STY &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/sty-geometry-data-type.md)   
 [STSrid &#40; tipo de dados geometry &#41;](../../t-sql/spatial-geometry/stsrid-geometry-data-type.md)   
 [Métodos OGC em instâncias geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

