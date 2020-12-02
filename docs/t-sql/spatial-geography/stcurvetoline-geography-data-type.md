---
description: STCurveToLine (tipo de dados geography)
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
ms.openlocfilehash: 2c8674e1e7ccafd59fa550fca690553050f68ffb
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88479296"
---
# <a name="stcurvetoline-geography-data-type"></a>STCurveToLine (tipo de dados geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna uma aproximação poligonal de uma instância de **geography** que contém segmentos de arco circulares.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STCurveToLine()  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de retorno do CLR: **SqlGeography**  
  
## <a name="remarks"></a>Comentários  
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
  
  
