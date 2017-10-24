---
title: STGeomCollFromText (tipo de dados geography) | Microsoft Docs
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f20e9259aad1f2a4ca87c8a684157b93c44b8b59
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="stgeomcollfromtext-geography-data-type"></a>STGeomCollFromText (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna um **geografia** instância de uma representação de texto do Open Geospatial Consortium (OGC) conhecido (WKT), aumentada com qualquer valor Z (elevação) e m (medida) transportados pela instância.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
STGeomCollFromText ( 'geometrycollection_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>Argumentos  
 *geometrycollection_tagged_text*  
 É a representação WKT do **geografia** instância que você deseja retornar. *geometrycollection_tagged_text* é um **nvarchar (max)** expressão.  
  
 *SRID*  
 É um **int** SRID (ID) de fazer referência a expressão que representa o espaciais a **geografia** instância que você deseja retornar.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geografia**  
  
 Tipo de retorno CLR: **SqlGeography**  
  
## <a name="remarks"></a>Comentários  
 O tipo OGC do **geografia** instância retornada por STGeomCollFromText() é definida como a entrada WKT correspondente.  
  
 Este método lança um **ArgumentException** se a entrada não é válida.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `STGeomCollFromText()` para criar uma instância `geography`.  
  
```  
DECLARE @g geography;  
DECLARE @g geography;  
SET @g = geography::STGeomCollFromText('GEOMETRYCOLLECTION ( POINT(-122.34900 47.65100), LINESTRING(-122.360 47.656, -122.343 47.656) )', 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos de Geografia estática do OGC](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  

