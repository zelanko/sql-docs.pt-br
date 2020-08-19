---
description: STLineFromText (tipo de dados geometry)
title: STLineFromText (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STLineFromText (geometry Data Type)
- STLineFromText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STLineFromText (geometry Data Type)
ms.assetid: 430508ad-207b-4dee-a4d1-4ddf25e6b4a9
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 77d76ddaeab5952db35f6395d0d2b14a5b904290
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88427038"
---
# <a name="stlinefromtext-geometry-data-type"></a>STLineFromText (tipo de dados geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Retorna uma instância de **geometry** de uma representação WKT (Well-Known Text) do OGC (Open Geospatial Consortium) aumentada com valores Z (elevação) e M (medida) presentes na instância.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
STLineFromText ( 'linestring_tagged_text' , SRID )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *linestring_tagged_text*  
 É a representação WKT da instância de **geometryLineString** que você deseja retornar. *linestring_tagged_text* é uma expressão **nvarchar(max)**.  
  
 *SRID*  
 É uma expressão **int** que representa a SRID (ID de referência espacial) da instância de **geometryLineString** que você deseja retornar.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de retorno do CLR: **SqlGeometry**  
  
 Tipo do OGC: **LineString**  
  
## <a name="remarks"></a>Comentários  
Esse método gerará uma **FormatException** se a entrada não estiver bem formatada. Não há suporte para a notação de WKT de geometria calculada e de três dimensões dos recursos simples do OGC (Open Geospatial Consortium) para a Especificação do SQL versão 1.2.1. Veja exemplos da representação de valores Z (elevação) e M (medida) com suporte.
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `STLineFromText()` para criar uma instância `geometry`.

### <a name="example-1-two-dimension-geometry-wkt"></a>Exemplo 1: WKT de geometria bidimensional
```  
DECLARE @g geometry;  
SET @g = geometry::STLineFromText('LINESTRING (100 100, 200 200)', 0);  
SELECT @g.ToString();  
```  
  
### <a name="example-2-three-dimension-geometry-wkt"></a>Exemplo 2: WKT de geometria tridimensional
```  
DECLARE @g geometry;  
SET @g = geometry::STLineFromText('LINESTRING (100 100 100, 200 200 200)', 0);  
SELECT @g.ToString();  
``` 

### <a name="example-3-two-dimension-measured-geometry-wkt"></a>Exemplo 3: WKT de geometria bidimensional calculada
```  
DECLARE @g geometry;  
SET @g = geometry::STLineFromText('LINESTRING (100 100 NULL 100, 200 200 NULL 200)', 0);  
SELECT @g.ToString();  
``` 

### <a name="example-4-three-dimension-measured-geometry-wkt"></a>Exemplo 4: WKT de geometria tridimensional calculada
```  
DECLARE @g geometry;  
SET @g = geometry::STLineFromText('LINESTRING (100 100 100 100, 200 200 200 200)', 0);  
SELECT @g.ToString();  
``` 
## <a name="see-also"></a>Consulte Também  
 [Métodos de geometria estática do OGC](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

