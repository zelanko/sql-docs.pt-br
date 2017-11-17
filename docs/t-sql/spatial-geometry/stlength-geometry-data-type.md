---
title: STLength (tipo de dados geometry) | Microsoft Docs
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
- STLength_TSQL
- STLength (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STLength (geometry Data Type)
ms.assetid: e34dc620-2a65-4248-b099-fff91830ab98
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9eacaffeb5998152e5a87f4cf058aa7374076a92
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="stlength-geometry-data-type"></a>STLength (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna o comprimento total dos elementos em uma **geometria** instância.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STLength ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **float**  
  
 Tipo de retorno CLR: **SqlDouble**  
  
## <a name="remarks"></a>Comentários  
 Se um **geometria** instância está fechada, seu comprimento será calculado como o comprimento total ao redor da instância; o comprimento de qualquer polígono é seu perímetro e o comprimento de um ponto é 0. O comprimento de qualquer **geometrycollection** tipo é a soma dos comprimentos de suas independente **geometria** instâncias.  
  
 STLength () funciona em LineStrings válidos e inválidos. Em geral, um LineString é inválido devido aos segmentos sobrepostos, que podem ser causados por anomalias como rastreamentos de GPS imprecisos. STLength () não remove segmentos sobrepostos ou inválidos. Ele inclui segmentos sobrepostos e inválidos no valor de comprimento que ele retorna. O método MakeValid () pode remover segmentos sobrepostos de um LineString.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância `LineString` e usa `STLength()` para encontrar o comprimento da instância.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STLength();  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos do OGC em instâncias de geometria](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


