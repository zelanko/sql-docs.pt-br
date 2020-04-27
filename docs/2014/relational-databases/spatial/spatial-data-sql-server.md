---
title: Dados espaciais (SQL Server) | Microsoft Docs
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- geography data type [SQL Server], spatial storage design
- planar spatial data [SQL Server], designing
- spatial data types [SQL Server]
- geodetic spatial data [SQL Server]
- geometry data type [SQL Server], spatial storage design
- spatial storage [SQL Server]
- geodetic spatial data [SQL Server], designing
ms.assetid: 41a132a1-09e2-4426-b9df-225270cb8e15
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 7bd529f67f9184f86d4a9ec704e9cf7af972f3f3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66014055"
---
# <a name="spatial-data-sql-server"></a>Dados espaciais (SQL Server)
  Os dados espaciais representam informações sobre a localização física e a forma dos objetos geométricos. Esses objetos podem ser localizações de pontos ou objetos mais complexos como países, estradas ou lagos.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte a dois tipos de dados espaciais: `geometry` e `geography`.  
  
-   O tipo `geometry` representa dados em um sistema de coordenadas euclidiano (plano).  
  
-   O tipo `geography` representa dados em um sistema de coordenadas de globo terrestre.  
  
 Os dois tipos de dados são implementados como tipos de dados CLR (Common Language Runtime) do .NET no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Para obter uma descrição detalhada e exemplos de recursos espaciais introduzidos no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], baixe o white paper [Novos recursos espaciais no SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=226407).  
  
##  <a name="related-tasks"></a><a name="reltasks"></a> Tarefas relacionadas  
 [Criar, construir e consultar instâncias de geometria](create-construct-and-query-geometry-instances.md)  
 Descreve os métodos que você pode usar com instâncias do tipo de dados de geometria.  
  
 [Criar, construir e consultar instâncias de geografia](create-construct-and-query-geography-instances.md)  
 Descreve os métodos que você pode usar com instâncias do tipo de dados de geografia.  
  
 [Consultar dados espaciais de vizinho mais próximo](query-spatial-data-for-nearest-neighbor.md)  
 Descreve o padrão de consulta comum usado para localizar os objetos espaciais mais próximos a um objeto espacial específico.  
  
 [Criar, modificar e remover índices espaciais](create-modify-and-drop-spatial-indexes.md)  
 Fornece informações sobre como criar, alterar e remover um índice espacial.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Visão geral de tipos de dados espaciais](spatial-data-types-overview.md)  
 Introduz os tipos de dados espaciais.  
  
-   [Point](point.md)  
  
-   [LineString](linestring.md)  
  
-   [CircularString](circularstring.md)  
  
-   [CompoundCurve](compoundcurve.md)  
  
-   [Polygon](polygon.md)  
  
-   [CurvePolygon](curvepolygon.md)  
  
-   [MultiPoint](multipoint.md)  
  
-   [MultiLineString](multilinestring.md)  
  
-   [MultiPolygon](multipolygon.md)  
  
-   [GeometryCollection](geometrycollection.md)  
  
 [Visão geral de índices espaciais](spatial-indexes-overview.md)  
 Introduz índices espaciais e descreve mosaico e esquemas de mosaico.  
  
  
