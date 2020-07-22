---
title: STIsValid (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STIsValid method (geography)
ms.assetid: 1bfe787f-ddf0-4fc7-af6a-570a58faab23
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 4549b317f3b6948fd72e0c5c2856255b8a6bd507
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86556093"
---
# <a name="stisvalid-geography-data-type"></a>STIsValid (tipo de dados geography)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  Retornará true se uma instância de **geography** estiver bem formada e for reconhecida como um objeto de geografia válido baseado em seu tipo do OGC (Open Geospatial Consortium). Retornará false se uma instância de **geography** não estiver bem formada. Esse método é preciso.  
  
 Esse método de tipo de dados de geography é compatível com instâncias **FullGlobe** ou instâncias espaciais maiores que um hemisfério.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STIsValid ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **bit**  
  
 Tipo de retorno do CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Comentários  
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
  
  
