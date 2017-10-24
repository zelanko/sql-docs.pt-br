---
title: STArea (tipo de dados geography) | Microsoft Docs
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
- STArea (geography Data Type)
- STArea_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STArea method
ms.assetid: cfc0b0e0-7fde-431a-863f-d13f3b1b1bef
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e96ee94983746e162990b8eadad4f6affb4f92fd
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="starea-geography-data-type"></a>STArea (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna a área da superfície total de um **geografia** instância. Resultados de STArea() são retornados no quadrado da unidade de medida usada pelo identificador de referência espacial o **geografia** instância; por exemplo, se o SRID da instância for 4326, o STArea() retorna resultados em metros quadrados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STArea ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **float**  
  
 Tipo de retorno CLR: **SqlDouble**  
  
## <a name="remarks"></a>Comentários  
 STArea() retornará 0 se uma **geografia** instância contiver apenas figuras dimensionais 0 e 1-, ou se ela estiver vazia.  
  
> [!NOTE]  
>  Métodos de **geografia** que produzem uma métrica de valor terão resultados diferentes com base na SRID da instância usada no método de retorno de tipo de dados. Para obter mais informações sobre SRIDs, consulte [Spatial Reference Identifiers &#40; SRIDs &#41; ](../../relational-databases/spatial/spatial-reference-identifiers-srids.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `STArea()` para criar um `Polygon``geography` de instância e calcula a área do polígono.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SELECT @g.STArea();  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos do OGC em instâncias de Geografia](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  

