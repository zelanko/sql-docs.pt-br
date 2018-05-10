---
title: STIsValid (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STIsValid method (geography)
ms.assetid: 1bfe787f-ddf0-4fc7-af6a-570a58faab23
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ff503496643a012cc75cbce300327fb73284419d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="stisvalid-geography-data-type"></a>STIsValid (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Retornará true se uma instância de **geography** estiver bem formada e for reconhecida como um objeto de geografia válido baseado em seu tipo do OGC (Open Geospatial Consortium). Retornará false se uma instância de **geography** não estiver bem formada. Esse método é preciso.  
  
 Esse método de tipo de dados de geography é compatível com instâncias **FullGlobe** ou instâncias espaciais maiores que um hemisfério.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STIsValid ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **bit**  
  
 Tipo de retorno do CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 O tipo OGC de uma instância de **geography** pode ser determinado com a invocação de [STGeometryType()](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md).  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] produz somente instâncias de **geografia** válidas, mas permite o armazenamento e a recuperação de instâncias inválidas. Uma instância válida que representa o mesmo conjunto de pontos de uma instância inválida pode ser recuperada por meio do método `MakeValid()`.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância de `geography` e usa `STIsValid()` para testar se a instância é válida.  
  
```  
DECLARE @g geography = geography::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 4326);  
SELECT @g.STIsValid();  
DECLARE @g geography  
```  
  
## <a name="see-also"></a>Consulte Também  
 [STGeometryType &#40;tipo de dados geography&#41;](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md)   
 [MakeValid &#40;tipos de dados geography&#41;](../../t-sql/spatial-geography/makevalid-geography-data-type.md)   
 [Métodos OGC em instâncias geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
