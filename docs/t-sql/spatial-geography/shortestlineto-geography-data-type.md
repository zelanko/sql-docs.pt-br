---
title: ShortestLineTo (tipo de dados geography) | Microsoft Docs
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
- ShortestLineTo_TSQL
- ShortestLineTo
dev_langs:
- TSQL
helpviewer_keywords:
- ShortestLineTo method (geography)
ms.assetid: 9d7c9885-5d1b-49ae-af31-5ef9fb8acaba
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: acb6d16fbf1413a81a05582bc203a7e768b70c75
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="shortestlineto-geography-data-type"></a>ShortestLineTo (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Retorna um **LineString** instância com dois pontos que representam a distância mais curta entre as duas **geografia** instâncias. O comprimento do **LineString** instância retornada é a distância entre os dois **geografia** instâncias.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.ShortestLineTo ( geography_other )  
```  
  
## <a name="arguments"></a>Argumentos  
 *geography_other*  
 Especifica o segundo **geografia** instância chamada **geografia** instância está tentando determinar a distância mais curta.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geografia**  
  
 Tipo de retorno CLR: **SqlGeography**  
  
## <a name="remarks"></a>Comentários  
 O método retorna um **LineString** instância com pontos de extremidade nas bordas dos dois sem interseção **geografia** instâncias que estão sendo comparadas. O comprimento do **LineString** é igual a distância mais curta entre as duas **geografia** instâncias. Vazio **LineString** instância é retornada quando as duas **geografia** instâncias se cruzam entre si.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-calling-shortestlineto-on-non-intersecting-instances"></a>A. Chamando ShortestLineTo() em instâncias sem interseção  
 Este exemplo localiza a distância mais curta entre uma instância de `CircularString` e uma instância de `LineString` e retorna a instância de `LineString` que conecta os dois pontos:  
  
 `DECLARE @g1 geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';`  
  
 `DECLARE @g2 geography = 'LINESTRING(-119.119263 46.183634, -119.273071 47.107523, -120.640869 47.569114, -122.200928 47.454094)';`  
  
 `SELECT @g1.ShortestLineTo(@g2).ToString();`  
  
### <a name="b-calling-shortestlineto-on-intersecting-instances"></a>B. Chamando ShortestLineTo() em instâncias com interseção  
 Este exemplo retorna uma instância de `LineString` vazia porque a instância de `LineString` cruza a instância de `CircularString`:  
  
 `DECLARE @g1 geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';`  
  
 `DECLARE @g2 geography = 'LINESTRING(-119.119263 46.183634, -119.273071 47.107523, -120.640869 47.569114, -122.348 47.649, -122.681 47.655)';`  
  
 `SELECT @g1.ShortestLineTo(@g2).ToString();`  
  
## <a name="see-also"></a>Consulte também  
 [Métodos estendidos em instâncias de Geografia](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
