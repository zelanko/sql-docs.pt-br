---
title: STIsRing (tipo de dados geometry) | Microsoft Docs
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
- STIsRing_TSQL
- STIsRing (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STIsRing (geometry Data Type)
ms.assetid: ea0063be-1c74-4cc4-ac6f-b65321ddfa54
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3417f5da487ea7de5d7c51820316dae3caf8bb0e
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="stisring-geometry-data-type"></a>STIsRing (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retornará 1 se uma **geometria** instância atende aos seguintes requisitos:
-   É um **LineString** instância.  
-   É fechada.  
-   É simples.  
-   Retorna 0 se o **LineString** instância não atende aos requisitos.  

 Para uma **geometria** instância seja fechada e simples, ambos [stisclosed ()](../../t-sql/spatial-geometry/stisclosed-geometry-data-type.md) e [stissimple ()](../../t-sql/spatial-geometry/stissimple-geometry-data-type.md) devem retornar 1 quando invocados na instância. Para determinar o tipo de instância de um **geometria**, use [stgeometrytype ()](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STIsRing ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **bits**  
  
 Tipo de retorno CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Comentários  
 Esse método retornará nulo se a instância não é um **LineString**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância `LineString` vazia e usa `STIsRing()` para testar se a instância é um anel.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0, 0 0)', 0);  
SELECT @g.STIsRing();  
```  
  
## <a name="see-also"></a>Consulte também  
 [STIsClosed &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stisclosed-geometry-data-type.md)   
 [STGeometryType &#40; tipo de dados geometry &#41;](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)   
 [STIsSimple &#40; tipo de dados geometry &#41;](../../t-sql/spatial-geometry/stissimple-geometry-data-type.md)   
 [Métodos do OGC em instâncias de geometria](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


