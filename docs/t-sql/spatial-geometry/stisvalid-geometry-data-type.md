---
title: STIsValid (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- STIsValid (geometry Data Type)
- STIsValid_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STIsValid (geometry Data Type)
ms.assetid: 6da39bea-0f67-4660-98fc-d7214f9b2138
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b856d37a31bdadf75eeadaa817968eaddbd687b7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33062343"
---
# <a name="stisvalid-geometry-data-type"></a>STIsValid (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retornará true se uma instância de **geometry** estiver bem formada, com base em seu tipo do OGC (Open Geospatial Consortium). Retornará false se uma instância de **geometry** não estiver bem formada.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STIsValid ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **bit**  
  
 Tipo de retorno do CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 O tipo do OGC de uma instância de **geometry** pode ser determinado com a invocação de [STGeometryType()](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md).  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] produz somente instâncias de **geometry** válidas, mas permite o armazenamento e a recuperação de instâncias inválidas. Uma instância válida que representa o mesmo conjunto de pontos de qualquer instância inválida pode ser recuperada usando o método `MakeValid()`.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância de `geometry` e usa `STIsValid()` para testar se a instância é válida.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STIsValid();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [STGeometryType &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)   
 [MakeValid &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/makevalid-geometry-data-type.md)   
 [Métodos OGC em instâncias geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

