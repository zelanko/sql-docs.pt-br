---
title: STArea (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STArea (geography Data Type)
- STArea_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STArea method
ms.assetid: cfc0b0e0-7fde-431a-863f-d13f3b1b1bef
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 49919caaf30bb425e90b286cb3c8e7877067ae6d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65936236"
---
# <a name="starea-geography-data-type"></a>STArea (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna a área total da superfície de uma instância de **geography**. Resultados para STArea() são a unidade de medida quadrada usada pelo identificador de referência espacial da instância **geography**. Por exemplo, se o SRID da instância for 4326, STArea() retornará resultados em metros quadrados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STArea ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
Tipo de retorno CLR: **SqlDouble**  
  
## <a name="remarks"></a>Remarks  
STArea() retornará 0 se uma instância de **geography** contiver apenas figuras sem dimensões ou unidimensionais, ou se estiver vazia.  
  
> [!NOTE]  
>  Os métodos com o tipo de dados **geography** que geram um valor retornado métrico terão resultados diferentes com base na SRID da instância usada no método. Para obter mais informações sobre SRIDs, confira [SRIDs &#40;Spatial Reference Identifiers&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md).  
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir usa `STArea()` para criar uma instância de `Polygon geography` e calcula a área do polígono.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SELECT @g.STArea();  
```  
  
## <a name="see-also"></a>Consulte Também  
[Métodos OGC em instâncias geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
