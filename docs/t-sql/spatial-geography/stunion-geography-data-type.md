---
description: STUnion (tipo de dados geography)
title: STUnion (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STUnion (geography Data Type)
- STUnion_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STUnion method
ms.assetid: 9bf87691-efd8-4c53-bd2f-eefe0acd19ca
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: ba22383c52908e44ed69efa0d54464290ace86ab
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488243"
---
# <a name="stunion-geography-data-type"></a>STUnion (tipo de dados geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna um objeto que representa a união de uma instância de **geography** com outra instância de **geography**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STUnion ( other_geography )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *other_geography*  
 É outra instância de **geography** para formar uma união com a instância na qual STUnion() está sendo invocado.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de retorno do CLR: **SqlGeography**  
  
## <a name="exceptions"></a>Exceções  
 Esse método gera uma **ArgumentException** se a instância contém uma borda oposta.  
  
## <a name="remarks"></a>Comentários  
 Esse método sempre retorna nulo se os SRIDs (identificadores de referência espacial) das instâncias de **geography** não são correspondentes.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte a instâncias espaciais maiores do que um hemisfério. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o conjunto de possíveis resultados retornado no servidor foi estendido para instâncias **FullGlobe**.  
  
 O resultado poderá conter segmentos de arco circular apenas se as instâncias de entrada contiverem segmentos de arco circulares.  
  
 Esse método não é preciso.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-computing-the-union-of-two-polygons"></a>a. Calculando a união de dois polígonos  
 O exemplo a seguir usa `STUnion()` para computar a união de duas instâncias de `Polygon`.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SET @h = geography::STGeomFromText('POLYGON((-122.351 47.656, -122.341 47.656, -122.341 47.661, -122.351 47.661, -122.351 47.656))', 4326);  
SELECT @g.STUnion(@h).ToString();  
```  
  
### <a name="b-producing-a-fullglobe-result"></a>B. Produzindo um resultado de FullGlobe  
 O exemplo a seguir gera um `FullGlobe` quando `STUnion()` combina duas instâncias de `Polygon`.  
  
```
 DECLARE @g geography = 'POLYGON ((-122.358 47.653, -122.358 47.658,-122.348 47.658, -122.348 47.649, -122.358 47.653))';  
 DECLARE @h geography = 'POLYGON ((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.STUnion(@h).ToString();
 ```  
  
### <a name="c-producing-a-triagonal-hole-from-a-union-of-a-curvepolygon-and-a-triagonal-hole"></a>C. Produzindo um espaço trigonal de uma união de um CurvePolygon e um espaço trigonal.  
 O exemplo a seguir gera um orifício triagonal da união de um `CurvePolygon` com uma instância de `Polygon`.  
  
```
 DECLARE @g geography = 'POLYGON ((-0.5 0, 0 1, 0.5 0.5, -0.5 0))';  
 DECLARE @h geography = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 0, 0.7 0.7, 0 1), (0 1, 0 0)))';  
 SELECT @g.STUnion(@h).ToString();
 ```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos do OGC em instâncias de geografia](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
