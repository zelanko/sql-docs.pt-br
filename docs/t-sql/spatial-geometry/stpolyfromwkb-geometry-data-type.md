---
title: STPolyFromWKB (tipo de dados geometry) | Microsoft Docs
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
f1_keywords:
- STPolyFromWKB_TSQL
- STPolyFromWKB (geometry Data Type)
dev_langs: TSQL
helpviewer_keywords: STPolyFromWKB (geometry Data Type)
ms.assetid: 8e8f0c41-0c62-4919-9d4c-d37c93fdd31c
caps.latest.revision: "18"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: df71b320201b436b40bb15e2c56f67fca9b291d2
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="stpolyfromwkb-geometry-data-type"></a>STPolyFromWKB (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna um **geometryPolygon** instância de uma representação do Open Geospatial Consortium (OGC) Well-Known Binary (WKB).
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
STPolyFromWKB ( 'WKB_polygon' , SRID )  
```  
  
## <a name="arguments"></a>Argumentos  
 *WKB_polygon*  
 É a representação WKB do **geometryPolygon** instância que você deseja retornar. *WKB_polygon* é um **varbinary (max)** expressão.  
  
 *SRID*  
 É um **int** SRID (ID) de fazer referência a expressão que representa o espaciais a **geometryPolygon** instância que você deseja retornar.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geometry**  
  
 Tipo de retorno CLR: **SqlGeometry**  
  
 Tipo OGC: **polígono**  
  
## <a name="remarks"></a>Remarks  
 Esse método lançará um **FormatException** se a entrada não for bem formatada.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `STPolyFromWKB()` para criar uma instância `geometry`.  
  
```  
DECLARE @g geometry;   
SET @g = geometry::STPolyFromWKB(0x0103000000010000000400000000000000000014400000000000001440000000000000244000000000000014400000000000002440000000000000244000000000000014400000000000001440, 0);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos geometry estáticos OGC](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

