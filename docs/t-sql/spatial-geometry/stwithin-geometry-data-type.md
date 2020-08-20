---
description: STWithin (tipo de dados geometry)
title: STWithin (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STWithin_TSQL
- STWithin (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STWithin (geometry Data Type)
ms.assetid: f845d28c-8029-4e2b-bcf0-71c52a592501
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: f0a9d615fcb05ed6b1c9ada74a98038de9f84e66
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488078"
---
# <a name="stwithin-geometry-data-type"></a>STWithin (tipo de dados geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Retorna 1 se uma instância de **geometry** está completamente dentro de outra instância de **geometry**; caso contrário, retorna 0. O comando `STWithin` diferencia maiúsculas de minúsculas.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STWithin ( other_geometry )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *other_geometry*  
 É outra instância de **geometry** a ser comparada com a instância na qual `STWithin()` é invocado.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **bit**  
  
 Tipo de retorno do CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Comentários  
 Esse método sempre retornará nulo se as SRIDs (IDs de referência espacial) das instâncias de **geometry** não forem correspondentes.
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `STWithin()` para testar duas instâncias  `geometry` para verificar se a primeira instância está completamente dentro da segunda.  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 2 0, 2 2, 0 2, 0 0))', 0);  
SET @h = geometry::STGeomFromText('POLYGON((1 1, 3 1, 3 3, 1 3, 1 1))', 0);  
SELECT @g.STWithin(@h);  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral de índices espaciais](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [Métodos OGC em instâncias geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

