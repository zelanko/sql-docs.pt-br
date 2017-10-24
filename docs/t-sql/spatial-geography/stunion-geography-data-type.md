---
title: STUnion (tipo de dados geography) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STUnion (geography Data Type)
- STUnion_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STUnion method
ms.assetid: 9bf87691-efd8-4c53-bd2f-eefe0acd19ca
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5e200f81a17e9b512986795077fe487e54a489f2
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="stunion-geography-data-type"></a>STUnion (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna um objeto que representa a união de uma **geografia** instância com outra **geografia** instância.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STUnion ( other_geography )  
```  
  
## <a name="arguments"></a>Argumentos  
 *other_geography*  
 É outra **geografia** instância para formar uma união com a instância na qual Stunion está sendo invocado.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geografia**  
  
 Tipo de retorno CLR: **SqlGeography**  
  
## <a name="exceptions"></a>Exceções  
 Este método lança um **ArgumentException** se a instância contiver uma borda oposta.  
  
## <a name="remarks"></a>Comentários  
 Esse método sempre retornará nulo se os identificadores de referência espaciais (SRIDs) do **geografia** instâncias não coincidem.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte a instâncias espaciais maiores do que um hemisfério. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o conjunto de possíveis resultados retornados no servidor foi estendido para **FullGlobe** instâncias.  
  
 O resultado poderá conter segmentos de arco circular apenas se as instâncias de entrada contiverem segmentos de arco circulares.  
  
 Esse método não é preciso.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-computing-the-union-of-two-polygons"></a>A. Calculando a união de dois polígonos  
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
  
### <a name="c-producing-a-triagonal-hole-from-a-union-of-a-curvepolygon-and-a-traigonal-hole"></a>C. Produzindo um orifício triagonal de uma união de um CurvePolygon e um orifício triagonal.  
 O exemplo a seguir gera um orifício triagonal da união de um `CurvePolygon` com uma instância de `Polygon`.  
  
```
 DECLARE @g geography = 'POLYGON ((-0.5 0, 0 1, 0.5 0.5, -0.5 0))';  
 DECLARE @h geography = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 0, 0.7 0.7, 0 1), (0 1, 0 0)))';  
 SELECT @g.STUnion(@h).ToString();
 ```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos do OGC em instâncias de Geografia](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  

