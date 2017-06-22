---
title: Dados espaciais (SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-spatial
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- geography data type [SQL Server], spatial storage design
- planar spatial data [SQL Server], designing
- spatial data types [SQL Server]
- geodetic spatial data [SQL Server]
- geometry data type [SQL Server], spatial storage design
- spatial storage [SQL Server]
- geodetic spatial data [SQL Server], designing
ms.assetid: 41a132a1-09e2-4426-b9df-225270cb8e15
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a7ed039271847202c8c84a03ec56d55a96593089
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="spatial-data-sql-server"></a>Dados espaciais (SQL Server)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Os dados espaciais representam informações sobre o local físico e a forma de objetos geométricos. Esses objetos podem ser locais de pontos ou objetos mais complexos como países, estradas ou lagos.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a dois tipos de dados espaciais: **geometria** e **geografia** .  
  
-   O tipo **geometria** representa dados em um sistema de coordenadas euclidiano (plano).  
  
-   O tipo **geografia** representa dados em um sistema de coordenadas esféricas.  
  
 Os dois tipos de dados são implementados como tipos de dados CLR (Common Language Runtime) do .NET no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Para obter uma descrição detalhada e exemplos de recursos espaciais introduzidos no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], baixe o white paper [Novos recursos espaciais no SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=226407).  
  
##  <a name="reltasks"></a> Tarefas relacionadas  
 [Criar, construir e consultar instâncias de geometria](../../relational-databases/spatial/create-construct-and-query-geometry-instances.md)  
 Descreve os métodos que você pode usar com instâncias do tipo de dados de geometria.  
  
 [Criar, construir e consultar instâncias de geografia](../../relational-databases/spatial/create-construct-and-query-geography-instances.md)  
 Descreve os métodos que você pode usar com instâncias do tipo de dados de geografia.  
  
 [Consultar dados espaciais de vizinho mais próximo](../../relational-databases/spatial/query-spatial-data-for-nearest-neighbor.md)  
 Descreve o padrão de consulta comum usado para localizar os objetos espaciais mais próximos a um objeto espacial específico.  
  
 [Criar, modificar e remover índices espaciais](../../relational-databases/spatial/create-modify-and-drop-spatial-indexes.md)  
 Fornece informações sobre como criar, alterar e remover um índice espacial.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Visão geral de tipos de dados espaciais](../../relational-databases/spatial/spatial-data-types-overview.md)  
 Introduz os tipos de dados espaciais.  
  
-   [Ponto](../../relational-databases/spatial/point.md)  
  
-   [LineString](../../relational-databases/spatial/linestring.md)  
  
-   [CircularString](../../relational-databases/spatial/circularstring.md)  
  
-   [CompoundCurve](../../relational-databases/spatial/compoundcurve.md)  
  
-   [Polígono](../../relational-databases/spatial/polygon.md)  
  
-   [CurvePolygon](../../relational-databases/spatial/curvepolygon.md)  
  
-   [MultiPoint](../../relational-databases/spatial/multipoint.md)  
  
-   [MultiLineString](../../relational-databases/spatial/multilinestring.md)  
  
-   [MultiPolygon](../../relational-databases/spatial/multipolygon.md)  
  
-   [GeometryCollection](../../relational-databases/spatial/geometrycollection.md)  
  
 [Visão geral de índices espaciais](../../relational-databases/spatial/spatial-indexes-overview.md)  
 Introduz índices espaciais e descreve mosaico e esquemas de mosaico.  
  
  
