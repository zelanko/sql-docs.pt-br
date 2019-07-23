---
title: ShortestLineTo (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- ShortestLineTo method (geometry)
ms.assetid: 39a2d0e4-4f93-4e94-a27e-6ad9537cfe74
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 4bb425d07d566f4bb06d18a8f74f493a649fa8b4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68101019"
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
  
 Tipo de retorno CLR: **SqlGeometry**  
  
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
  
  

