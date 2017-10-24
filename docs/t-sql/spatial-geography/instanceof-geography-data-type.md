---
title: InstanceOf (tipo de dados geography) | Microsoft Docs
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
- InstanceOf
- InstanceOf_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- InstanceOf method
ms.assetid: 1eaed0e4-1c72-45a9-9926-5b513335cf33
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0edbebbb6754fd09ff834e4ffe8d453853b6f240
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="instanceof-geography-data-type"></a>InstanceOf (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Testa se o **geografia** instância é o mesmo que o tipo especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.InstanceOf ( 'geography_type')  
```  
  
## <a name="arguments"></a>Argumentos  
 *geography_type*  
 É um **nvarchar (4000)** cadeia de caracteres especificando um dos 16 tipos expostos no **geografia** hierarquia de tipo.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **bits**  
  
 Tipo de retorno CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Comentários  
 Retornará 1 se o tipo de um **geografia** instância é o mesmo que o tipo especificado ou se o tipo especificado for um ancestral do tipo de instância; caso contrário, retornará 0.  
  
 Isso **geografia** método dá suporte ao tipo de dados **FullGlobe** instâncias ou a instâncias espaciais maiores que um hemisfério.  
  
 A entrada para o método deve ser um dos seguintes: Geometry, Point, curva, LineString, CircularString, superfície, Polygon, CurvePolygon, **GeometryCollection**, **MultiSurface**,  **MultiPolygon, MultiCurve, MultiLineString**, **MultiPoint**, ou **FullGlobe**.  
  
 Esse método lançará uma `ArgumentException` se qualquer outra cadeia de caracteres for usada na entrada.  
  
 Esse método não é preciso.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir criará uma instância de `MultiPoint` e usará `InstanceOf()` para verificar se a instância é uma `GeometryCollection`.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('MULTIPOINT(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.InstanceOf('GEOMETRYCOLLECTION');  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos estendidos em instâncias de Geografia](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  

