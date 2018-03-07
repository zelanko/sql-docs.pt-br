---
title: STMPointFromWKB (tipo de dados geometry) | Microsoft Docs
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
f1_keywords:
- STMPointFromWKB (geometry Data Type)
- STMPointFromWKB_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STMPointFromWKB (geometry Data Type)
ms.assetid: 01d4117f-01a0-4bc3-8762-7382a1cdbd6c
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 927d87e812bfec327dee6a477757587b026432ef
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="stmpointfromwkb-geometry-data-type"></a>STMPointFromWKB (tipo de dados de geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna um **geometryMultiPoint** instância de uma representação do Open Geospatial Consortium (OGC) Well-Known Binary (WKB).
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
STMPointFromWKB ( 'WKB_multipoint' , SRID )  
```  
  
## <a name="arguments"></a>Argumentos  
 *WKB_multipoint*  
 É a representação WKB do **geometryMultiPoint** instância que você deseja retornar. *WKB_multipoint* é um **varbinary (max)** expressão.  
  
 *SRID*  
 É um **int** SRID (ID) de fazer referência a expressão que representa o espaciais a **geometryMultiPoint** instância que você deseja retornar.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geometry**  
  
 Tipo de retorno CLR: **SqlGeometry**  
  
 Tipo OGC: **MultiPoint**  
  
## <a name="remarks"></a>Remarks  
 Esse método lançará um **FormatException** se a entrada não for bem formatada.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `STMPointFromWKB()` para criar uma instância `geometry`.  
  
```  
DECLARE @g geometry;   
SET @g = geometry::STMPointFromWKB(0x010400000002000000010100000000000000000059400000000000005940010100000000000000000069400000000000006940, 0);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos geometry estáticos OGC](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

