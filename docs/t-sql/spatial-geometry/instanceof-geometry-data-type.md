---
title: InstanceOf (tipo de dados geometry) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2017
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
- InstanceOf (geometry Data Type)
ms.assetid: fdea1248-29a4-4bab-a60d-a1b359b5e109
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a7106339cc346cbd49b3cbfc3905ea3a2a941c15
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="instanceof-geometry-data-type"></a>InstanceOf (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Um método que testa se o **geometria** instância é o mesmo que o tipo especificado. Retornará 1 se o tipo de um **geometria** instância é o mesmo que o tipo especificado ou se o tipo especificado for um ancestral do tipo de instância; caso contrário, retornará 0.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.InstanceOf (geometry_type )  
```  
  
## <a name="arguments"></a>Argumentos  
 *geometry_type*  
 É um **nvarchar (4000)** cadeia de caracteres especificando um dos 15 tipos expostos no **geometria** hierarquia de tipo.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **bits**  
  
 Tipo de retorno CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Comentários  
 A entrada para o método deve ser um dos seguintes: **geometria**, **ponto**, **curva**, **LineString**,  **CircularString**, **CompoundCurve**, **superfície**, **polígono**, **CurvePolygon**, **GeometryCollection**, **MultiSurface**, **MultiPolygon**, **MultiCurve**, **MultiLineString**, e **MultiPoint**. Este método lança um **ArgumentException** se quaisquer outras cadeias de caracteres são usadas para a entrada.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir criará uma instância `MultiPoint` e usará `InstanceOf()` para consultar se a instância é uma `GeometryCollection`.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('MULTIPOINT(0 0, 13.5 2, 7 19)', 0);  
SELECT @g.InstanceOf('GEOMETRYCOLLECTION');  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos estendidos em instâncias de geometria](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  


