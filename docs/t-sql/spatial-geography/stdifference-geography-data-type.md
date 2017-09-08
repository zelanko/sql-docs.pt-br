---
title: STDifference (tipo de dados geography) | Microsoft Docs
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
- STDifference_TSQL
- STDifference (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STDifference (geography Data Type)
ms.assetid: 1cde5054-b91a-41bb-812a-08c9308738af
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5afb37eb29e63d8cf08e9c158b94385a66d4c41f
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="stdifference-geography-data-type"></a>STDifference (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna um objeto que representa o conjunto de pontos de um **geografia** instância que está fora de outra **geografia** instância.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STDifference ( other_geography )  
```  
  
## <a name="arguments"></a>Argumentos  
 *other_geography*  
 É outra **geografia** instância que indica quais pontos devem ser removidos da instância em que está sendo invocado stdifference ().  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geografia**  
  
 Tipo de retorno CLR: **SqlGeography**  
  
## <a name="exceptions"></a>Exceções  
 Este método lança um **ArgumentException** se a instância contiver uma borda oposta.  
  
## <a name="remarks"></a>Comentários  
 Esse método sempre retornará nulo se os identificadores de referência espaciais (SRIDs) do **geografia** instâncias não coincidem.  
  
 Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o conjunto de possíveis resultados retornados no servidor foi estendido para **FullGlobe** instâncias. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte a instâncias espaciais maiores do que um hemisfério. O resultado poderá conter segmentos de arco circular apenas se as instâncias de entrada contiverem segmentos de arco circulares. Esse método não é preciso.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-computing-the-difference-between-two-geography-instances"></a>A. Computando a diferença entre duas instâncias de geografia  
 O exemplo a seguir usa `STDifference()` para computar a diferença entre dois **geografia** instâncias.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SET @h = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STDifference(@h).ToString();  
```  
  
### <a name="b-using-a-fullglobe-with-stdifference"></a>B. Usando um FullGlobe com STDifference()  
 O exemplo a seguir usa a instância de `FullGlobe`. O primeiro resultado é uma `GeometryCollection` vazia e o segundo resultado é uma instância de `Polygon`. `STDifference()` retorna uma `GeometryCollection` vazia quando uma instância de `FullGlobe` for o parâmetro. Todo ponto em uma instância de `geography` de invocação é contido em uma instância de `FullGlobe`.  
  
 `DECLARE @g geography = 'POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';`  
  
 `DECLARE @h geography = 'FULLGLOBE';`  
  
 `SELECT @g.STDifference(@h).ToString(),`  
  
 `@h.STDifference(@g).ToString();`  
  
## <a name="see-also"></a>Consulte também  
 [Métodos do OGC em instâncias de Geografia](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
