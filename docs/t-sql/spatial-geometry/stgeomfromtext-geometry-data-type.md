---
title: STGeomFromText (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STGeomFromText (geometry Data Type)
- STGeomFromText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STGeomFromText (geometry Data Type)
ms.assetid: 20cace39-02e5-46c1-a9a5-841d04d0da16
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 6d8a79e1bc9ddbbfc86243df0be1caf4f8d8b1c8
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552792"
---
# <a name="stgeomfromtext-geometry-data-type"></a>STGeomFromText (tipo de dados geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Retorna uma instância de **geometry** de uma representação WKT (Well-Known Text) do OGC (Open Geospatial Consortium) aumentada com valores Z (elevação) e M (medida) presentes na instância.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
STGeomFromText ( 'geometry_tagged_text' , SRID )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *geometry_tagged_text*  
 É a representação WKT da instância de **geometry** que você deseja retornar. *geometry_tagged_text* é uma expressão **nvarchar(max)** .  
  
 *SRID*  
 É uma expressão **int** que representa a SRID (ID de referência espacial) da instância de **geometry** que você deseja retornar.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de retorno do CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Comentários  
 O tipo do OGC da instância de **geometry** retornado por `STGeomFromText()` é definido como a entrada de WKT correspondente.  
  
 Esse método gerará uma **FormatException** se a entrada não for bem formatada.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `STGeomFromText()` para criar uma instância `geometry`.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING (100 100, 20 180, 180 180)', 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos geometry estáticos OGC](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

