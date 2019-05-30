---
title: InstanceOf (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- InstanceOf
- InstanceOf_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- InstanceOf (geometry Data Type)
ms.assetid: fdea1248-29a4-4bab-a60d-a1b359b5e109
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 82cc52338771862b580c193353db0bb98453b458
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65939113"
---
# <a name="instanceof-geometry-data-type"></a>InstanceOf (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Um método que testa se a instância de **geometry** é igual ao tipo especificado. Retorna 1 se o tipo de uma instância de **geometry** é igual ao tipo especificado. Esse método também retornará 1 se o tipo especificado for um ancestral do tipo de instância. Caso contrário, este método retornará 0.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.InstanceOf (geometry_type )  
```  
  
## <a name="arguments"></a>Argumentos  
*geometry_type*  
Cadeia de caracteres **nvarchar(4000)** que especifica um dos 15 tipos expostos na hierarquia de tipo **geometry**.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **bit**  
  
 Tipo de retorno CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 A entrada para o método deve ser um dos seguintes tipos: **Geometry**, **Point**, **Curve**, **LineString**, **CircularString**, **CompoundCurve**, **Surface**, **Polygon**, **CurvePolygon**, **GeometryCollection**, **MultiSurface**, **MultiPolygon**, **MultiCurve**, **MultiLineString** e **MultiPoint**. Esse método gera uma **ArgumentException** se outra cadeia de caracteres é usada na entrada.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir criará uma instância `MultiPoint` e usará `InstanceOf()` para consultar se a instância é uma `GeometryCollection`.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('MULTIPOINT(0 0, 13.5 2, 7 19)', 0);  
SELECT @g.InstanceOf('GEOMETRYCOLLECTION');  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos estendidos em instâncias geometry](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

