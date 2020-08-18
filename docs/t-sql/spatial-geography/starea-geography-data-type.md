---
description: STArea (tipo de dados geography)
title: STArea (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STArea (geography Data Type)
- STArea_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STArea method
ms.assetid: cfc0b0e0-7fde-431a-863f-d13f3b1b1bef
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: a8581700ea3145840684cce1e18e24c2f2e1cd3e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88359732"
---
# <a name="starea-geography-data-type"></a>STArea (tipo de dados geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Retorna a área total da superfície de uma instância de **geography**. Resultados para STArea() são a unidade de medida quadrada usada pelo identificador de referência espacial da instância **geography**. Por exemplo, se o SRID da instância for 4326, STArea() retornará resultados em metros quadrados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STArea ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno
Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
Tipo de retorno do CLR: **SqlDouble**  
  
## <a name="remarks"></a>Comentários  
STArea() retornará 0 se uma instância de **geography** contiver apenas figuras sem dimensões ou unidimensionais, ou se estiver vazia.  
  
> [!NOTE]  
>  Os métodos com o tipo de dados **geography** que geram um valor retornado métrico terão resultados diferentes com base na SRID da instância usada no método. Para obter mais informações sobre SRIDs, confira [SRIDs &#40;Spatial Reference Identifiers&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md).  
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir usa `STArea()` para criar uma instância de `Polygon geography` e calcula a área do polígono.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SELECT @g.STArea();  
```  
  
## <a name="see-also"></a>Consulte Também  
[Métodos do OGC em instâncias de geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
