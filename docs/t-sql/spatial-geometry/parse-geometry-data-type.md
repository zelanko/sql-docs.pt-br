---
title: Parse (tipo de dados geometry) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Parse (geometry Data Type)
ms.assetid: 6e080919-4b64-46cd-8dd2-254a9c232e53
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 64adf9398a6ea63203f75714aa97ccf2653e947b
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="parse-geometry-data-type"></a>Parse (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna um **geometria** instância de uma representação de texto do Open Geospatial Consortium (OGC) conhecido (WKT). `Parse()`é equivalente a [Stgeomfromtext](../../t-sql/spatial-geometry/parse-geometry-data-type.md), com a exceção que assume um SRID (ID) 0 como um parâmetro de referência. A entrada pode transportar valores opcionais Z (elevação) e M (medida).
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Parse ( 'geometry_tagged_text' )  
```  
  
## <a name="arguments"></a>Argumentos  
 *geometry_tagged_text*  
 É a representação WKT do **geometria** instância que você deseja retornar. *geometry_tagged_text* é um **nvarchar** expressão.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geometry**  
  
 Tipo de retorno CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Comentários  
 O tipo OGC do **geometria** instância retornada por `Parse()` é definido como a entrada WKT correspondente.  
  
 A cadeia de caracteres 'Nulo' será interpretado como um valor nulo **geometria** instância.  
  
 Esse método lançará um **FormatException** se a entrada não for bem formatada.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `Parse()` para criar uma instância `geometry`.  
  
```  
DECLARE @g geometry;   
SET @g = geometry::Parse('LINESTRING (100 100, 20 180, 180 180)');  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Consulte também  
 [STGeomFromText](../../t-sql/spatial-geometry/parse-geometry-data-type.md)   
 [Métodos de geometria estática estendidos](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  


