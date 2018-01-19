---
title: STRelate (tipo de dados geometry) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STRelate (geometry Data Type)
- STRelate_TSQL
dev_langs: TSQL
helpviewer_keywords: STRelate (geometry Data Type)
ms.assetid: 9dcb5f58-35ab-4bb3-86ee-2d29eefba6d3
caps.latest.revision: "19"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 192156b32a4190479515ade197b57f638c14ca62
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="strelate-geometry-data-type"></a>STRelate (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Retornará 1 se uma **geometria** instância está relacionada a outro **geometria** instância, em que a relação é definida por um valor de matriz de padrão de modelo de interseção de 9 dimensionalmente estendido (DE-9IM); caso contrário , retornará 0.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STRelate ( other_geometry, intersection_pattern_matrix )  
```  
  
## <a name="arguments"></a>Argumentos  
 *other_geometry*  
 É outra **geometria** instância a ser comparada com a instância na qual `STRelate()` é invocado.  
  
 *intersection_pattern_matrix*  
 É uma cadeia de caracteres do tipo **nchar(9)** codifica os valores aceitáveis para o dispositivo de matriz de padrão DE-9IM entre as duas **geometria** instâncias.  
  
## <a name="remarks"></a>Remarks  
 Esse método sempre retornará nulo se as IDs de referência espaciais (SRIDs) da **geometria** instâncias não coincidem. Esse método lançará um **ArgumentException** se a matriz não está bem formada.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **bits**  
  
 Tipo de retorno CLR: **SqlBoolean**  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `STRelate()` para testar duas **geometria** instâncias para separação espacial usando um padrão DE-9IM explícito.  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 2 0, 4 2)', 0);  
SET @h = geometry::STGeomFromText('POINT(5 5)', 0);  
SELECT @g.STRelate(@h, 'FF*FF****');  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos OGC em instâncias geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  
