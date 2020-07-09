---
title: STIsClosed (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STIsClosed_TSQL
- STIsClosed (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STIsClosed (geometry Data Type)
ms.assetid: 14edbb22-df7b-4b8a-b16c-ac477a5d32c1
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 18c9c3f647bd2121ac7edf65011e0ac6a0038789
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85762421"
---
# <a name="stisclosed-geometry-data-type"></a>STIsClosed (tipo de dados geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Retornará 1 se os pontos inicial e final da instância de **geometry** fornecida forem o mesmo. Retornará 1 para os tipos **geometrycollection** se cada instância de **geometry** contida estiver fechada. Retornará 0 se a instância não for fechada.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STIsClosed ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **bit**  
  
 Tipo de retorno do CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Comentários  
 Esse método retornará 0 se alguma figura de uma instância de **geometry** for um ponto ou se a instância estiver vazia.  
  
 As instâncias de **polígono** são consideradas fechadas.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância `LineString` e usa `STIsClosed()` para testar se `LineString` está fechada.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STIsClosed();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos OGC em instâncias geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

