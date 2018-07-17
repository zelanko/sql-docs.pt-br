---
title: STSymDifference (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- STSymDifference (geography Data Type)
- STSymDifference_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STSymDifference (geography Data Type)
ms.assetid: 82bbfa2c-a61b-4f41-9bf8-6f720f363bae
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4dc604d7e30288f71d5f84acce52aee8ee0c5c54
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36255018"
---
# <a name="stsymdifference-geography-data-type"></a>STSymDifference (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna um objeto que representa todos os pontos que estão em uma instância de **geography** ou em outra instância de **geography**, mas não os pontos que estão em ambas as instâncias.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STSymDifference ( other_geography )  
```  
  
## <a name="arguments"></a>Argumentos  
 *other_geography*  
 É outra instância de **geography**, além da instância na qual STSymDistance() está sendo invocado.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de retorno do CLR: **SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 Esse método sempre retorna nulo se os SRIDs (identificadores de referência espacial) das instâncias de **geography** não são correspondentes.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte a instâncias espaciais maiores do que um hemisfério. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o conjunto de possíveis resultados no servidor foi estendido para instâncias de **FullGlobe**.  
  
 O resultado poderá conter segmentos de arco circular apenas se as instâncias de entrada contiverem segmentos de arco circulares.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-computing-the-symmetric-difference-of-two-polygons"></a>A. Computando a diferença simétrica de dois polígonos  
 O exemplo a seguir usa `STSymDifference()` para computar a diferença simétrica entre duas instâncias de `Polygon`.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SET @h = geography::STGeomFromText('POLYGON((-122.351 47.656, -122.341 47.656, -122.341 47.661, -122.351 47.661, -122.351 47.656))', 4326);  
SELECT @g.STSymDifference(@h).ToString();  
```  
  
### <a name="b-computing-the-symmetric-difference-with-fullglobe"></a>B. Computando a diferença simétrica com FullGlobe  
 O exemplo a seguir compara a diferença simétrica de um `Polygon` com `FullGlobe`.  
  
```
 DECLARE @g geography = 'POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.STSymDifference('FULLGLOBE').ToString();
 ```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos OGC em instâncias geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
