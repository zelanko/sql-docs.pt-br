---
title: STDimension (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STDimension_TSQL
- STDimension (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STDimension (geometry Data Type)
ms.assetid: 4fbd27dd-317b-4916-a8ae-4df1b8a6f27c
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 1f84bd8cd53f68bd45cf91307968b45923e53280
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65938994"
---
# <a name="stdimension-geometry-data-type"></a>STDimension (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna a dimensão máxima de uma instância de **geometry**.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STDimension ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **int**  
  
 Tipo de retorno CLR: **SqlInt32**  
  
## <a name="remarks"></a>Remarks  
 `STDimension()` retornará -1 se a instância de **geometry** estiver vazia.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma variável de tabela para manter as instâncias de **geometry** e insere um `Point`, um `LineString` e um `Polygon`.  Em seguida, ele usa `STDimension()` para retornar as dimensões de cada instância de **geometry**.  
  
```  
DECLARE @temp table ([name] varchar(10), [geom] geometry);  
INSERT INTO @temp values ('Point', geometry::STGeomFromText('POINT(3 3)', 0));  
INSERT INTO @temp values ('LineString', geometry::STGeomFromText('LINESTRING(0 0, 3 3)', 0));  
INSERT INTO @temp values ('Polygon', geometry::STGeomFromText('POLYGON((0 0, 3 0, 0 3, 0 0))', 0));  
SELECT [name], [geom].STDimension() as [dim]  
FROM @temp;  
```  
  
 O exemplo, então, retorna as dimensões de cada instância de `geometry`.  
  
|NAME|dim|  
|----------|---------|  
|Ponto|0|  
|LineString|1|  
|Polygon|2|  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos OGC em instâncias geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

