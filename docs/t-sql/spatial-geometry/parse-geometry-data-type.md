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
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords: Parse (geometry Data Type)
ms.assetid: 6e080919-4b64-46cd-8dd2-254a9c232e53
caps.latest.revision: "19"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 97fa8dad6e879cf976a3f790422b12cb09255a13
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
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
  
## <a name="remarks"></a>Remarks  
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
 [Métodos geometry estáticos estendidos](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

