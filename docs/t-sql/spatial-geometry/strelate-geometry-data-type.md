---
title: STRelate (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STRelate (geometry Data Type)
- STRelate_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STRelate (geometry Data Type)
ms.assetid: 9dcb5f58-35ab-4bb3-86ee-2d29eefba6d3
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: bb4c4e589ef3f658cee65812e9263a68a3489d2a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65938306"
---
# <a name="strelate-geometry-data-type"></a>STRelate (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Retornará 1 se uma instância de **geometry** tiver relação com outra instância de **geometry**, e a relação for definida por um valor de matriz do padrão DE-9IM (Dimensionally Extended 9 Intersection Model), caso contrário, retornará 0.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STRelate ( other_geometry, intersection_pattern_matrix )  
```  
  
## <a name="arguments"></a>Argumentos  
 *other_geometry*  
 É outra instância de **geometry** a ser comparada com a instância na qual `STRelate()` é invocado.  
  
 *intersection_pattern_matrix*  
 É uma cadeia de caracteres do tipo **nchar(9)** que codifica os valores aceitáveis do dispositivo da matriz do padrão DE-9IM entre as duas instâncias de **geometria**.  
  
## <a name="remarks"></a>Remarks  
 Esse método sempre retornará nulo se as SRIDs (IDs de referência espacial) das instâncias de **geometry** não forem correspondentes. Esse método vai gerar uma **ArgumentException** se a matriz não estiver bem formada.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **bit**  
  
 Tipo de retorno CLR: **SqlBoolean**  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `STRelate()` para testar duas instâncias de **geometria** quanto à separação espacial usando um padrão DE-9IM explícito.  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 2 0, 4 2)', 0);  
SET @h = geometry::STGeomFromText('POINT(5 5)', 0);  
SELECT @g.STRelate(@h, 'FF*FF****');  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos OGC em instâncias geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  
