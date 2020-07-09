---
title: STIsSimple (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STIsSimple_TSQL
- STIsSimple (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STIsSimple (geometry Data Type)
ms.assetid: da8f45d4-4f9c-405d-b883-760eb5344a71
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 1d0118528aa926b5750f8e2f1f587cc6e9c14844
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85762390"
---
# <a name="stissimple-geometry-data-type"></a>STIsSimple (tipo de dados geometry)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

Retorna 1 se uma instância de **geometry** é simples, conforme definido pelo OGC (Open Geospatial Consortium). Retorna 0 se uma instância de **geometry** não é simples.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STIsSimple ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **bit**  
  
 Tipo de retorno do CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Comentários  
 Para ser simples, uma instância de **geometry** deve atender aos seguintes requisitos:  
  
-   Não deve haver interseção de nenhuma figura da instância consigo mesma, exceto em seus pontos de extremidade.  
  
-   Não pode haver nenhuma interseção entre duas figuras da instância em nenhum ponto que não esteja nos seus dois limites.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância `LineString` não simples com uma interseção consigo mesma e usa `STIsSimple()` para testar se `LineString` é simples.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 0 2, 2 0)', 0);  
SELECT @g.STIsSimple();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos OGC em instâncias geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

