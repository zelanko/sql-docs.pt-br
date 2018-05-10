---
title: Parse (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Parse (geometry Data Type)
ms.assetid: 6e080919-4b64-46cd-8dd2-254a9c232e53
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cee8d49fc959a276c086ea5976c3a8ba731160fd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="parse-geometry-data-type"></a>Parse (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna uma instância de **geometry** de uma representação WKT (Well-Known Text) do OGC (Open Geospatial Consortium). `Parse()` é equivalente a [STGeomFromText()](../../t-sql/spatial-geometry/parse-geometry-data-type.md), com a exceção de que ele assume uma SRID (ID de referência espacial) igual a 0 como parâmetro. A entrada pode transportar valores opcionais Z (elevação) e M (medida).
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Parse ( 'geometry_tagged_text' )  
```  
  
## <a name="arguments"></a>Argumentos  
 *geometry_tagged_text*  
 É a representação WKT da instância de **geometry** que você deseja retornar. *geometry_tagged_text* é uma expressão **nvarchar**.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de retorno do CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 O tipo do OGC da instância de **geometry** retornado por `Parse()` é definido como a entrada de WKT correspondente.  
  
 A cadeia de caracteres 'Null' será interpretada como uma instância de **geometry** nula.  
  
 Esse método gerará uma **FormatException** se a entrada não for bem formatada.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `Parse()` para criar uma instância `geometry`.  
  
```  
DECLARE @g geometry;   
SET @g = geometry::Parse('LINESTRING (100 100, 20 180, 180 180)');  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [STGeomFromText](../../t-sql/spatial-geometry/parse-geometry-data-type.md)   
 [Métodos geometry estáticos estendidos](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

