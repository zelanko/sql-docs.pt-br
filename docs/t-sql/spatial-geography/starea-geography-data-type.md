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
ms.openlocfilehash: 817a6325b956f5fc4214597b0b8bc46f6aff49f3
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68042511"
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
  
Tipo de retorno do CLR: **SqlDouble**  
  
## <a name="remarks"></a>Comentários  
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
  
