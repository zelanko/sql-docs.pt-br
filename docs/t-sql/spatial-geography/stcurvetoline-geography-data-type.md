---
title: STCurveToLine (tipo de dados geography) | Microsoft Docs
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
- STCurveToLine_TSQL
- STCurveToLine
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveToLine method (geography)
ms.assetid: 2f863a85-6168-465a-b32f-bb5e3de58dee
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9d2ad93d8bc292ebb86233917dc3f934fbe57dca
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="stcurvetoline-geography-data-type"></a>STCurveToLine (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna uma aproximação poligonal de uma **geografia** instância que contém segmentos de arco circular.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STCurveToLine()  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geografia**  
  
 Tipo de retorno CLR: **SqlGeography**  
  
## <a name="remarks"></a>Comentários  
 Retorna um **LineString** instância para uma **CircularString** ou **CompoundCurve** instância.  
  
 Retorna um **polígono** instância para uma **CurvePolygon** instância.  
  
 Retornar uma cópia do **geografia** instâncias que não contêm **CircularString**, **CompoundCurve**, ou **CurvePolygon** instâncias.  
  
 Ao contrário da especificação SQL MM, esse método não usa valores de coordenada z para calcular a aproximação poligonal. Quaisquer valores de coordenada z presente na chamada **geografia** instância são ignorados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna uma instância de `LineString` que é uma aproximação poligonal de uma instância de `CircularString`:  
  
 `DECLARE @g1 geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';`  
  
 `DECLARE @g2 geography;`  
  
 `SET @g2 = @g1.STCurveToLine();`  
  
 `SELECT @g1.STNumPoints() AS G1, @g2.STNumPoints() AS G2;`  
  
## <a name="see-also"></a>Consulte também  
 [STLength &#40; tipo de dados geography &#41;](../../t-sql/spatial-geography/stlength-geography-data-type.md)   
 [STNumPoints &#40; tipo de dados geography &#41;](../../t-sql/spatial-geography/stnumpoints-geography-data-type.md)   
 [Visão geral de tipos de dados espaciais](../../relational-databases/spatial/spatial-data-types-overview.md)  
  
  
