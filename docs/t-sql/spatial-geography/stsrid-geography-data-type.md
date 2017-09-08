---
title: STSrid (tipo de dados geography) | Microsoft Docs
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
- STSrid (geography Data Type)
- STSrid_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STSrid method
ms.assetid: 6b04f5a7-2e69-4d34-901e-b61ba6ca9c14
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c93ccfc28eb3dfe3b24a817394bf3481a86e89d3
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="stsrid-geography-data-type"></a>STSrid (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  **STSrid** é um inteiro que representa o identificador de referência espacial (SRID) da instância.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STSrid  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo: **int**  
  
 Tipo CLR: **SqlInt32**  
  
## <a name="remarks"></a>Comentários  
 Essa propriedade pode ser modificada.  
  
## <a name="examples"></a>Exemplos  
 O primeiro exemplo cria uma instância de `geography` com o valor 4326 de SRID (WGS84) e usa `STSrid` para confirmar o SRID.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STSrid;  
```  
  
 O segundo exemplo usa `STSrid` para alterar o valor de SRID da instância para 4267 (NAD27) e confirma o valor de SRID modificado.  
  
```  
SET @g.STSrid = 4267;  
SELECT @g.STSrid;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos do OGC em instâncias de Geografia](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)   
 [Identificadores de referência espacial &#40; SRIDs &#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)  
  
  
