---
title: ToString (tipo de dados geometry) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ToString (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- ToString (geometry Data Type)
ms.assetid: 2e55fa98-aa22-4baa-a516-7c233a33e212
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4ffe70ad712605222a66dc12ba7af4e330dc12c9
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="tostring-geometry-data-type"></a>ToString (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna a representação WKT (Well-Known Text) do OGC (Open Geospatial Consortium) de uma instância geométrica, aumentada com qualquer valor Z (elevação) e M (medida) presente na instância.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.ToString ()  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **nvarchar (max)**  
  
 Tipo de retorno CLR: **SqlString**  
  
## <a name="remarks"></a>Comentários  
 Esse método retornará a cadeia de caracteres "Nulo" quando chamado em instâncias nulas.  
  
 Em instâncias não nulas, esse método é equivalente a usar `AsTextZM().`  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria um `LineString` instância e usa `ToString()` para buscar a descrição de texto da instância.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 0 1, 1 0)', 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Consulte também  
 [STAsText &#40; tipo de dados geometry &#41;](../../t-sql/spatial-geometry/stastext-geometry-data-type.md)   
 [Métodos estendidos em instâncias de geometria](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  


