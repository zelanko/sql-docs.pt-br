---
title: InstanceOf (tipo de dados geometry) | Microsoft Docs
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
- InstanceOf
- InstanceOf_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- InstanceOf (geometry Data Type)
ms.assetid: fdea1248-29a4-4bab-a60d-a1b359b5e109
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c53e66f85d614b79e51312dc4404fd19acd69fed
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="instanceof-geometry-data-type"></a>InstanceOf (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

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
  
## <a name="remarks"></a>Remarks  
 A entrada para o método deve ser um dos seguintes: **geometria**, **ponto**, **curva**, **LineString**,  **CircularString**, **CompoundCurve**, **superfície**, **polígono**, **CurvePolygon**, **GeometryCollection**, **MultiSurface**, **MultiPolygon**, **MultiCurve**, **MultiLineString**, e **MultiPoint**. Este método lança um **ArgumentException** se quaisquer outras cadeias de caracteres são usadas para a entrada.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir criará uma instância `MultiPoint` e usará `InstanceOf()` para consultar se a instância é uma `GeometryCollection`.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('MULTIPOINT(0 0, 13.5 2, 7 19)', 0);  
SELECT @g.InstanceOf('GEOMETRYCOLLECTION');  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos estendidos em instâncias geometry](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

