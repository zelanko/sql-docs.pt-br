---
title: STGeomCollFromText (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- STGeomCollFromText_TSQL
- STGeomCollFromText (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STGeomCollFromText method
ms.assetid: a5b3c344-1045-43a4-82fa-47f6206a288e
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 22fcc6138ac75f6012c69caa141b1343c9d02152
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="stgeomcollfromtext-geography-data-type"></a>STGeomCollFromText (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna uma instância de **geography** de uma representação WKT (Well-Known Text) do OGC (Open Geospatial Consortium), aumentada com valores Z (elevação) e M (medida) presentes na instância.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
STGeomCollFromText ( 'geometrycollection_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>Argumentos  
 *geometrycollection_tagged_text*  
 É a representação WKT da instância de **geography** que você deseja retornar. *geometrycollection_tagged_text* é uma expressão **nvarchar(max)**.  
  
 *SRID*  
 É uma expressão **int** que representa a SRID (ID de referência espacial) da instância de **geography** que você deseja retornar.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de retorno do CLR: **SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 O tipo do OGC da instância de **geography** retornado por STGeomCollFromText() é definido como a entrada de WKT correspondente.  
  
 Este método gerará uma **ArgumentException** se a entrada não for válida.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `STGeomCollFromText()` para criar uma instância `geography`.  
  
```  
DECLARE @g geography;  
DECLARE @g geography;  
SET @g = geography::STGeomCollFromText('GEOMETRYCOLLECTION ( POINT(-122.34900 47.65100), LINESTRING(-122.360 47.656, -122.343 47.656) )', 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [OGC Static Geography Methods](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
