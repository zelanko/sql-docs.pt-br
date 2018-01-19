---
title: STMLineFromWKB (tipo de dados geometry) | Microsoft Docs
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
- STMLineFromWKB (geometry Data Type)
- STMLineFromWKB_TSQL
dev_langs: TSQL
helpviewer_keywords: STMLineFromWKB (geometry Data Type)
ms.assetid: 00a8a8e7-11d6-47a0-b971-00e60f7877ce
caps.latest.revision: "17"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e6934e2488e2cdff0526d7e66dbe5f13a459df1c
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="stmlinefromwkb-geometry-data-type"></a>STMLineFromWKB (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna um **geometryMultiLineString** instância de uma representação do Open Geospatial Consortium (OGC) Well-Known Binary (WKB).
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
STMLineFromWKB ( 'WKB_multilinestring' , SRID )  
```  
  
## <a name="arguments"></a>Argumentos  
 *WKB_multilinestring*  
 É a representação WKB do **geometryMultiLineString** instância a ser retornada. *WKB_multilinestring* é um **varbinary (max)** expressão.  
  
 *SRID*  
 É um **int** SRID (ID) de fazer referência a expressão que representa o espaciais a **geometryMultiLineString** instância a ser retornada.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geometry**  
  
 Tipo de retorno CLR: **SqlGeometry**  
  
 Tipo OGC: **MultiLineString**  
  
## <a name="remarks"></a>Remarks  
 Esse método lançará um **FormatException** se a entrada não for bem formatada.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `STMLineFromWKB()` para criar uma instância `geometry`.  
  
```  
DECLARE @g geometry;   
SET @g = geometry::STMLineFromWKB(0x0105000000020000000102000000020000000000000000005940000000000000594000000000000069400000000000006940010200000003000000000000000000084000000000000010400000000000001C40000000000000204000000000000024400000000000002440, 0);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos geometry estáticos OGC](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

