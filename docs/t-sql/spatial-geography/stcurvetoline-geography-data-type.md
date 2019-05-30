---
title: STCurveToLine (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STCurveToLine_TSQL
- STCurveToLine
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveToLine method (geography)
ms.assetid: 2f863a85-6168-465a-b32f-bb5e3de58dee
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 7f237da350b47ea0c3141709cd82d083ef509196
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65939187"
---
# <a name="stcurvetoline-geography-data-type"></a>STCurveToLine (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna uma aproximação poligonal de uma instância de **geography** que contém segmentos de arco circulares.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STCurveToLine()  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de retorno CLR: **SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 Retorna uma instância de **LineString** para uma instância de **CircularString** ou de **CompoundCurve**.  
  
 Retorna uma instância de **Polygon** para uma instância de **CurvePolygon**.  
  
 Retornar uma cópia das instâncias de **geografia** que não contêm instâncias de **CircularString**, **CompoundCurve** ou **CurvePolygon**.  
  
 Ao contrário da especificação SQL MM, esse método não usa valores de coordenada z para calcular a aproximação poligonal. Os valores de coordenada z que estiverem presentes na chamada da instância de **geography** serão ignorados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna uma instância de `LineString` que é uma aproximação poligonal de uma instância de `CircularString`:  
  
```
 DECLARE @g1 geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 DECLARE @g2 geography;  
 SET @g2 = @g1.STCurveToLine();  
 SELECT @g1.STNumPoints() AS G1, @g2.STNumPoints() AS G2;
 ```  
  
## <a name="see-also"></a>Consulte Também  
 [STLength &#40;tipo de dados geography&#41;](../../t-sql/spatial-geography/stlength-geography-data-type.md)   
 [STNumPoints &#40;tipo de dados geography&#41;](../../t-sql/spatial-geography/stnumpoints-geography-data-type.md)   
 [Visão geral de tipos de dados espaciais](../../relational-databases/spatial/spatial-data-types-overview.md)  
  
  
