---
title: STDifference (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STDifference_TSQL
- STDifference (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STDifference (geography Data Type)
ms.assetid: 1cde5054-b91a-41bb-812a-08c9308738af
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 8165c78e7eced334e31ed7b0ccb0d2bfbab74af4
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552881"
---
# <a name="stdifference-geography-data-type"></a>STDifference (tipo de dados geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna um objeto que representa o conjunto de pontos de uma instância de **geography** que reside fora de outra instância de **geography**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STDifference ( other_geography )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *other_geography*  
 É outra instância de **geography** que indica quais pontos devem ser removidos da instância na qual STDifference() está sendo invocado.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de retorno do CLR: **SqlGeography**  
  
## <a name="exceptions"></a>Exceções  
 Esse método gera uma **ArgumentException** se a instância contém uma borda oposta.  
  
## <a name="remarks"></a>Comentários  
 Esse método sempre retorna nulo se os SRIDs (identificadores de referência espacial) das instâncias de **geography** não são correspondentes.  
  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o conjunto de possíveis resultados retornado no servidor foi estendido para instâncias **FullGlobe**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte a instâncias espaciais maiores do que um hemisfério. O resultado poderá conter segmentos de arco circular apenas se as instâncias de entrada contiverem segmentos de arco circulares. Esse método não é preciso.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-computing-the-difference-between-two-geography-instances"></a>a. Computando a diferença entre duas instâncias de geografia  
 O exemplo a seguir usa `STDifference()` para calcular a diferença entre duas instâncias de **geography**.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SET @h = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STDifference(@h).ToString();  
```  
  
### <a name="b-using-a-fullglobe-with-stdifference"></a>B. Usando um FullGlobe com STDifference()  
 O exemplo a seguir usa a instância de `FullGlobe`. O primeiro resultado é uma `GeometryCollection` vazia e o segundo resultado é uma instância de `Polygon`. `STDifference()` retorna uma `GeometryCollection` vazia quando uma instância de `FullGlobe` for o parâmetro. Todo ponto em uma instância de `geography` de invocação é contido em uma instância de `FullGlobe`.  
  
```
 DECLARE @g geography = 'POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 DECLARE @h geography = 'FULLGLOBE';  
 SELECT @g.STDifference(@h).ToString(),  
 @h.STDifference(@g).ToString();
 ```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos OGC em instâncias geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
