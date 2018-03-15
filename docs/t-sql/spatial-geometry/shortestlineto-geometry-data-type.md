---
title: ShortestLineTo (tipo de dados geometry) | Microsoft Docs
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
dev_langs:
- TSQL
helpviewer_keywords:
- ShortestLineTo method (geometry)
ms.assetid: 39a2d0e4-4f93-4e94-a27e-6ad9537cfe74
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 08e83f7bb1993d3b55a48e5e3714c75d4bd33429
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="shortestlineto-geometry-data-type"></a>ShortestLineTo (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Retorna uma instância de **LineString** com dois pontos que representam a distância mais curta entre as duas instâncias de **geometria**. O comprimento da instância de **LineString** retornado é a distância entre as duas instâncias de **geometria**.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.ShortestLineTo ( geometry_other )  
```  
  
## <a name="arguments"></a>Argumentos  
 *geometry_other*  
 A segunda instância de **geometry** para a qual a instância de **geometry** de chamada está tentando determinar a distância mais curta.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de retorno do CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 O método retorna uma instância de **LineString** com pontos de extremidade nas bordas das duas instâncias de **geometria** sem intersecção que estão sendo comparadas. O comprimento de **LineString** retornado é igual à distância mais curta entre as duas instâncias de **geometria**. Uma instância de **LineString** vazia é retornada quando as duas instâncias de **geometria** se interseccionam.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-calling-shortestlineto-on-non-intersecting-instances"></a>A. Chamando ShortestLineTo() em instâncias sem interseção  
 Este exemplo localiza a distância mais curta entre uma instância de `CircularString` e uma instância de `LineString` e retorna a instância de `LineString` que conecta os dois pontos:  
  
```
 DECLARE @g1 geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';  
 DECLARE @g2 geometry = 'LINESTRING(-4 7, 7 10, 3 7)';  
 SELECT @g1.ShortestLineTo(@g2).ToString();
 ```  
  
### <a name="b-calling-shortestlineto-on-intersecting-instances"></a>B. Chamando ShortestLineTo() em instâncias com interseção  
 Este exemplo retorna uma instância de `LineString` vazia porque a instância de `LineString` cruza a instância de `CircularString`:  
  
```
 DECLARE @g1 geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';  
 DECLARE @g2 geometry = 'LINESTRING(0 5, 7 10, 3 7)';  
 SELECT @g1.ShortestLineTo(@g2).ToString();
 ```  
  
## <a name="see-also"></a>Consulte Também  
 [ShortestLineTo &#40;tipo de dados geography&#41;](../../t-sql/spatial-geography/shortestlineto-geography-data-type.md)  
  
  

