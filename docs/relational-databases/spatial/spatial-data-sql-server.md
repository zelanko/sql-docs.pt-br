---
description: Dados espaciais (SQL Server)
title: Dados espaciais (SQL Server) | Microsoft Docs
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 43ec99d77ea10b33dd06427f97444c995534dba2
ms.sourcegitcommit: 9386ae1b90705a39d37d5541b70c5e8a6564f253
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2020
ms.locfileid: "91662135"
---
# <a name="spatial-data-sql-server"></a>Dados espaciais (SQL Server)
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  Os dados espaciais representam informações sobre a localização física e a forma dos objetos geométricos. Esses objetos podem ser localizações de pontos ou objetos mais complexos como países, estradas ou lagos.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a dois tipos de dados espaciais: **geometria** e **geografia** .  
  
-   O tipo **geometria** representa dados em um sistema de coordenadas euclidiano (plano).  
  
-   O tipo **geografia** representa dados em um sistema de coordenadas esféricas.  
  
 Os dois tipos de dados são implementados como tipos de dados CLR (Common Language Runtime) do .NET no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
##  <a name="related-tasks"></a><a name="reltasks"></a> Tarefas relacionadas  
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
  
-   [Polygon](../../relational-databases/spatial/polygon.md)  
  
-   [CurvePolygon](../../relational-databases/spatial/curvepolygon.md)  
  
-   [MultiPoint](../../relational-databases/spatial/multipoint.md)  
  
-   [MultiLineString](../../relational-databases/spatial/multilinestring.md)  
  
-   [MultiPolygon](../../relational-databases/spatial/multipolygon.md)  
  
-   [GeometryCollection](../../relational-databases/spatial/geometrycollection.md)  
  
 [Visão geral de índices espaciais](../../relational-databases/spatial/spatial-indexes-overview.md)  
 Introduz índices espaciais e descreve mosaico e esquemas de mosaico.  
  
  
