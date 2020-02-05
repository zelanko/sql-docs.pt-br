---
title: STGeomFromWKB (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STGeomFromWKB (geometry Data Type)
- STGeomFromWKB_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STGeomFromWKB (geometry Data Type)
ms.assetid: 6546ddb0-4a5f-46e5-ba04-8007486c95ec
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 769b48c99e59c8bfcf38fa96cd60d6ef11cd3237
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67950140"
---
# <a name="stgeomfromwkb-geometry-data-type"></a>STGeomFromWKB (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna uma instância de **geometry** de uma representação WKB (Well-Known Binary) do OGC (Open Geospatial Consortium).
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
STGeomFromWKB ( 'WKB_geometry' , SRID )  
```  
  
## <a name="arguments"></a>Argumentos  
 *WKB_geometry*  
 É a representação WKB da instância de **geometry** que você deseja retornar. *WKB_geometry* é uma expressão **varbinary(max)** .  
  
 *SRID*  
 É uma expressão **int** que representa a SRID (ID de referência espacial) da instância de **geometry** que você deseja retornar.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de retorno do CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Comentários  
 O tipo do OGC da instância de **geometry** retornado por `STGeomFromText()` é definido como a entrada de WKB correspondente.  
  
 Esse método gerará uma **FormatException** se a entrada não for bem formatada.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `STGeomFromWKB()` para criar uma instância de **geometry**.  
  
```  
DECLARE @g geometry;   
SET @g = geometry::STGeomFromWKB(0x010200000003000000000000000000594000000000000059400000000000003440000000000080664000000000008066400000000000806640, 0);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos geometry estáticos OGC](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

