---
title: STIsSimple (tipo de dados geometry) | Microsoft Docs
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
- STIsSimple_TSQL
- STIsSimple (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STIsSimple (geometry Data Type)
ms.assetid: da8f45d4-4f9c-405d-b883-760eb5344a71
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 12b150546378ef76c0165c6d8e3c166e93db304b
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="stissimple-geometry-data-type"></a>STIsSimple (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Retornará 1 se uma **geometria** instância é simples, conforme definido pelo Open geoespaciais Consortium (OGC). Retorna 0 se uma **geometria** instância não é simple.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STIsSimple ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **bits**  
  
 Tipo de retorno CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Comentários  
 Para ser simples, um **geometria** instância deve atender aos seguintes requisitos:  
  
-   Não deve haver interseção de nenhuma figura da instância consigo mesma, exceto em seus pontos de extremidade.  
  
-   Não pode haver nenhuma interseção entre duas figuras da instância em nenhum ponto que não esteja nos seus dois limites.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância `LineString` não simples com uma interseção consigo mesma e usa `STIsSimple()` para testar se `LineString` é simples.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 0 2, 2 0)', 0);  
SELECT @g.STIsSimple();  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos do OGC em instâncias de geometria](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


