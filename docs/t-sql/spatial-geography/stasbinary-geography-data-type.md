---
description: STAsBinary (tipo de dados geography)
title: STAsBinary (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STAsBinary_TSQL
- STAsBinary (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STAsBinary method
ms.assetid: 99602a62-265d-4aa4-a8dc-92992ca55ba4
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 7ae9c800cffd7df80ba8447c2e16de745a0009bc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88359442"
---
# <a name="stasbinary-geography-data-type"></a>STAsBinary (tipo de dados geography)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  Retorna a representação WKB (Well-Known Binary) do OGC (Open Geospatial Consortium) de uma instância de **geography**.  
  
 Esse método de tipo de dados de **geography** é compatível com instâncias **FullGlobe** ou instâncias espaciais maiores que um hemisfério.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STAsBinary ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **varbinary(max)**  
  
 Tipo de retorno do CLR: **SqlBytes**  
  
## <a name="remarks"></a>Comentários  
 O tipo OGC de uma instância de **geography** pode ser determinado com a invocação de [STGeometryType()](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `STAsBinary()` para criar uma instância de `LineString``geography` de (-122.360, 47.656) a (-122.343, -47.656) com base no texto. Retorna, então, o resultado em WKB.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING( -122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STAsBinary();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos do OGC em instâncias de geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
