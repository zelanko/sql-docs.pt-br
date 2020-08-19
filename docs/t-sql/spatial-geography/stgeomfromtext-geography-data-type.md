---
description: STGeomFromText (tipo de dados geography)
title: STGeomFromText (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STGeomFromText (geography Data Type)
- STGeomFromText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full globe
- STGeomFromText method
ms.assetid: 3717987b-77d8-4ccf-a1db-5a8016ac1083
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 584b34c02bde76293654b0a0bef8c006ad3c38b1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88445273"
---
# <a name="stgeomfromtext-geography-data-type"></a>STGeomFromText (tipo de dados geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Retorna uma instância de **geography** de uma representação WKT (Well-Known Text) do OGC (Open Geospatial Consortium) aumentada com os valores de Z (elevação) e de M (medida) presentes na instância.
  
Esse método de tipo de dados de **geography** é compatível com instâncias **FullGlobe** ou instâncias espaciais maiores que um hemisfério.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
STGeomFromText ( 'geography_tagged_text' , SRID )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *geography_tagged_text*  
 É a representação WKT da instância de **geography** a ser retornada. *geography_tagged_text* é uma expressão **nvarchar(max)**.  
  
 *SRID*  
 É uma expressão **int** que representa a SRID (ID de referência espacial) da instância de **geography** que você deseja retornar.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de retorno do CLR: **SqlGeography**  
  
## <a name="remarks"></a>Comentários  
 O tipo do OGC da instância de **geography** retornado por STGeomFromText() é definido como a entrada de WKT correspondente.  
  
 Esse método gerará uma **ArgumentException** se a entrada contiver uma borda oposta.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `STGeomFromText()` para criar uma instância `geography`.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [OGC Static Geography Methods](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
